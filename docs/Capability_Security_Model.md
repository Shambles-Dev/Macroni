The Capability Security Model
=============================

## Overview

The capability security model controls direct access to values via [thread safety](https://en.wikipedia.org/wiki/Thread_safety), [memory safety](https://en.wikipedia.org/wiki/Memory_safety), [type safety](https://en.wikipedia.org/wiki/Type_safety), and [encapsulation](https://en.wikipedia.org/wiki/Encapsulation_(computer_programming)).

It should be used with taint checking (which controls indirect access to values) and sandboxing (which controls access to space and time).


## Details

### Why Use Capabilities?

The capability security model is better than [the access control list security model](https://en.wikipedia.org/wiki/Access-control_list) that all currently popular computing systems use:
* Access control lists are vulnerable to [the confused deputy problem](https://en.wikipedia.org/wiki/Confused_deputy_problem), where code is tricked into misusing its authority to affect a designation provided by less privileged code, because they separate designation and authorization.  Capabilities do not make this mistake.
* Access control lists are coarse-grained and inextensible.  Capabilities are fine-grained and extensible.  If access control lists were made fine-grained and extensible, security policies using them would be too difficult to specify and audit.  Security policies using capabilities are easy to specify and audit because the only static permissions involved are those in the [installation endowments](Capability_Security_Model.md#using-capabilities) of programs the owner-user chose to install.
* Access control lists are static.  Capabilities are dynamic.  If access control lists were made dynamic, computing systems using them would execute at the speed the users involved react to the bombardment of authorization prompts.  Capabilities automate authorization.


### The Mechanism

Capabilities are unforgeable values (i.e. “knowing is not having”) that both designate and authorize access to objects (i.e. “designation is authorization”).  A capability is normally a reference to an object in a thread-safe, memory-safe, and type-safe programming language that enforces encapsulation.  Capabilities implemented this way are described as “object capabilities” to distinguish them from other ways of implementing capabilities.

Encapsulation ensures integrity and confidentiality (i.e. “tell, don’t ask”).  Getters and setters are only provided for low-level data structures.  Internal data structures are never exposed.

The object graph provides the only authority to read or write state, including performing I/O (i.e. there is no “ambient authority”).  Objects are constructed with just enough authority to work correctly, and further authorization occurs via secure user interaction (the “principle of least authority”).

Capabilities are securely (de)serialized via transparent persistence.


### Using Capabilities

An installation endowment is the set of capabilities an instance of a program (a process, which is a capability) must always have to work correctly.  The owner-user grants it via an authorization prompt when installing a program.

Other authorization prompts are unnecessary because operations are authorized by designating their operands, which must be done anyway.

Most capabilities should be single-use capabilities.


## Patterns

### C-list Capabilities

To share capabilities across [trust boundaries](https://en.wikipedia.org/wiki/Trust_boundary), we implement C-list capabilities.

A C-list capability is normally an integer key designating the capability in a mutable dictionary, a C-list, used to authorize a process to access the capabilities within.  The unique integers can be obtained by incrementing a counter.  Each process is associated with its own C-list.  A protocol using the integer keys to refer to capabilities sends operations and results across the trust boundaries.

The values in the C-lists might forward messages to and from other processes instead of directly implementing the capabilities.

The C-lists being stored on the side of the trust boundaries opposite their respective processes ensures the processes cannot tamper with the C-lists.  Mutually distrusting processes may provide C-list capabilities to each other.

To revoke a C-list capability, we remove it from the C-list.

To confine a C-list capability, we do not insert it in the C-lists of processes that should not be authorized to access it.

C-list capabilities are traditionally used to share capabilities across [memory protection boundaries](https://en.wikipedia.org/wiki/Memory_protection) in capability-based operating systems.  C-list capabilities are normally used to share capabilities across sandbox boundaries in Macroni.


### Distributed Capabilities

To share capabilities across network connections, we implement distributed capabilities.

Distributed capabilities work like C-list capabilities except the trust boundaries are network connections and each process must be authenticated via password or public-key cryptography.  Network connections should be encrypted.  Passwords should be salted and hashed.

Distributed capabilities are normally used to implement accounts.

Be aware that distributed capabilities are vulnerable to forgery and [the communicating conspirators problem](http://erights.org/elib/capability/conspire.html), where someone or something with legitimate access uses it on an attacker’s behalf!  Knowing the password or private encryption key of a process is having all its distributed capabilities.  Capabilities and data cannot be confined outside hardware the owner-user alone controls.  These are not arguments against the use of distributed capabilities.  Access control lists would be even less secure.  These are arguments against the unnecessary use of distributed computing systems.


### Notary/Inspector

To authenticate capabilities, we implement a notary and an inspector.

A notary and an inspector are normally a pair of types that are instantiated such that they share a weak set indexed by identity.  The notary inserts a capability in the weak set.  The inspector returns whether a capability is in the weak set.

The notary/inspector pattern is analogous to cryptographic signing.  It is dynamic trademark checking (provenance-based whitelisting, the complement of taint checking).  Note that trademark does not spread to derived values.

The notary/inspector pattern is normally used for secure information flow or to avoid time-consuming validation.  For example, it could be used to efficiently decide whether a value received from untrustworthy code is trustworthy.

Be aware that only untainted immutable values and mutable values that are designed to remain trustworthy should be notarized!


### Sealer/Unsealer

To prevent capabilities from being used except by the intended recipient, we implement a sealer and an unsealer.

A sealer and an unsealer are normally a pair of types that are instantiated such that they share a weak key dictionary indexed by identity.  The sealed type is useless except for unsealing.  The sealer constructs a sealed capability, then it inserts a key-value pair containing the sealed and original capabilities (respectively) in the weak key dictionary, and then it returns the sealed capability.  The unsealer looks the sealed capability up in the weak key dictionary and returns the original capability.

The sealer/unsealer pattern is analogous to encryption.

The sealer/unsealer pattern is normally used to authorize someone or something to perform an operation that is accessible to a subset of those that have access to a capability.  For example, it could be used to authorize the owner-user to write to a capability, by unsealing a read-write instance of that capability, whereas other users can only read from that capability.

Be aware that the sealer/unsealer pattern does not prevent referencing (copying)!  Sealed capabilities used to identify a capability should be encapsulated in what they identify to prevent identity theft.


### Facet

To attenuate a type of capability, we implement a facet.

A facet is normally a type that forwards messages to and from the type to be attenuated.  Attenuation is accomplished by thinning or augmenting.

Thinning is providing an interface that accepts less messages.  Be aware that facets should deny messages by default!  This ensures the facet will not accept more messages if the interface of the type they attenuate changes.

For example, thinning could be used to attenuate a file capability to make it read-only.

Augmenting is making doing the right thing unavoidable.

For example, augmenting could be used to attenuate a window capability to make it prefix the window title with the name of the program that opened it to prevent [spoofing vulnerabilities](https://en.wikipedia.org/wiki/Spoofing_attack).


### Caretaker

To make a capability revocable, we implement a caretaker.

A caretaker is normally a pair of types, a forwarding facet type and a revoking facet type, that are instantiated such that they share a mutable record containing a reference to the capability to be made revocable.  The forwarding facet forwards messages to and from the capability referred to in the mutable record.  The revoking facet sets the reference in the mutable record to null.

For example, caretakers could be used to revoke a process’ access to the microphone and webcam when the user ends a video call.


### Single-Use Capabilities

To prevent capabilities from accumulating authority, we implement single-use capabilities.

A single-use capability works like the forwarding facet of a caretaker except it revokes itself after use.

For example, a single-use capability could be used to authorize a process to write to a file once.


### Membrane

To potentially affect the behavior of all capabilities flowing to and from some capabilities, we implement a membrane.

The inside of the membrane and capabilities originating from inside the membrane are described as “wet”.  The outside of the membrane and capabilities originating from outside the membrane are described as “dry”.

A membrane is normally a membrane type and two sets of forwarding proxy types, one for wet capabilities and one for dry capabilities.

The membrane constructor accepts any capabilities the membrane will initially wrap, it instantiates a membrane, then it passes the membrane and the capabilities to wrap to the wet forwarding proxy constructors for those types of capabilities, and then it returns the capabilities wrapped in wet forwarding proxies.

The membrane is instantiated such that it encapsulates two weak key dictionaries indexed by identity.  They are bimaps that map original capabilities to proxied capabilities and proxied capabilities to original capabilities.  One stores wet capabilities, and the other stores dry capabilities.

When a capability attempts to cross the membrane, the membrane is passed the capability and the side it is crossing to, which implies the side it is crossing from.  If the capability is not found in either bimap, the membrane constructs a proxied capability for the side it is crossing from, then the membrane inserts the original and proxied capabilities in the bimap for the side it is crossing from, and then the membrane returns the proxied capability.  If the capability is found in the bimap for the side it is crossing from, the membrane looks it up in that bimap then the membrane returns the existing proxied capability.  If the capability is found in the bimap for the side it is crossing to, the membrane looks it up in that bimap then the membrane returns the original capability.  This ensures capabilities are always wrapped on the side they did not originate on, the same proxied capability is always used for the same original capability, and capabilities are never wrapped on the side they originated on.  This assumes the membrane allows the capability to cross and proxies that type of capability, which it might not do.

The forwarding proxies are instantiated such that they share the membrane and any other state they need for coordination.

The forwarding proxies use the membrane to coerce their arguments to their side and their return values to the other side (e.g. a wet forwarding proxy wets its arguments and dries its return values).  They implement the interface and behavioral differences the other side uses.

When a membrane is used for security, it is said to perform deep attenuation.

When a membrane is used for revocation, it works like a caretaker except the forwarding facets and the revoking facet are instantiated such that they share a weak set indexed by identity that contains the mutable records and the revoking facet uses the weak set of mutable records to set the references to null.

When a membrane is used for confinement, it crashes, throws an exception (which Macroni does not support), or passes an error value instead of the capability when a wet restricted capability attempts to escape it.

Membranes are useful for more than security.  They are useful any time a programmer wants types to behave differently on different sides of a boundary.  Membranes are traditionally used to make C-list capabilities or distributed capabilities behave like object capabilities in capability-based operating systems where <a href="https://en.wikipedia.org/wiki/Inter-process_communication">IPC</a> and I/O cause <a href="https://en.wikipedia.org/wiki/Blocking_(computing)">blocking</a> (which Macroni does not support).  Membranes could be used to avoid breaking interfaces used by the rest of the system while refactoring subsystems.

Be aware that membranes normally cannot affect side effects!  Side effects should be represented as values that are passed to the object whose state they read or write where they are ‘interpreted’ to perform the side effects.  This ensures membranes can affect side effects when that is secure.


## See Also
* [Built-Ins](Built-Ins.md)
* [Debugger](Debugger.md)
* [File System](File_System.md)
* [Microrebooting](Microrebooting.md)
* [Object System](Object_System.md)
* [Packages](Packages.md)
* [Sandboxes](Sandboxes.md)
* [Sets and Dictionaries](Sets_and_Dictionaries.md)
* [System Structure](System_Structure.md)
* [Taint Checking](Taint_Checking.md)
* [Transparent Persistence](Transparent_Persistence.md)
* [User Interface](User_Interface.md)
