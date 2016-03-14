Taint Checking
==============

## Overview

Taint checking controls indirect access to values via tracking provenance.

It should be used with the capability security model (which controls direct access to values) and sandboxing (which controls access to space and time).


## Details

### Why Use Taint Checking?

Taint checking can detect when code does not [validate](https://en.wikipedia.org/wiki/Data_validation) input or [sanitize](https://en.wikipedia.org/wiki/Data_sanitization) output.

Taint checking can detect software processing [side-channels](https://en.wikipedia.org/wiki/Side-channel_attack).  Eliminating modulation or the ability to measure space or time consumption is impractical, but eliminating modulation correlated with secrets or values that might aid in inferring secrets is practical.


### The Mechanism

Taint checking is provenance-based blacklisting, the complement of [trademark checking](Capability_Security_Model.md#notaryinspector).

Taint checking is local to a sandbox because this prevents an availability vulnerability (specifically, a crash vulnerability) and serendipitously improves efficiency.  Mutable types that may be passed between sandboxes are passed by copying their mutable representations, not their mutable contents.

There are two varieties of taint: input and secret.  An input tainted value is an integrity risk.  A secret tainted value is a confidentiality risk.

A value may be tainted explicitly or implicitly.  Tainting is not recursive.  This is consistent with trademark checking.  Tainting only inserts the specified variety of taint because the value might already be tainted.

Taint spreads to derived values.  For example, if two numbers are added and either of them is tainted, the sum is tainted with the union of the summands’ varieties of taint.  If a value becomes input and secret tainted, that is a defect because it could be a confidentiality vulnerability (specifically, an [oracle vulnerability](https://en.wikipedia.org/wiki/Oracle_attack)).

A value may only be untainted explicitly.  Untainting is not recursive.  This prevents laundering internal tainted values.  Untainting only removes the specified variety of taint because the programmer must have known how the variable was tainted to have performed the appropriate validation or sanitization.

Immutable types are tainted and untainted by copying.  Mutable types are tainted and untainted by mutating.

Parameters and return values may be untaintable.  Untaintability is recursive.  If a value is tainted or contains any values that are tainted (e.g. in a closure’s environment frames, in an object’s fields, or in a data structure’s elements) and it is passed to an untaintable parameter or returned by a procedure with an untaintable return value, that is a defect because it could be an integrity or confidentiality vulnerability.  Parameters and return values are not untaintable by default so that data flow is not hindered when taint is irrelevant, which is most of the time.  If most code forbade the use of tainted values, most code could not be used to perform the required validation or sanitization.

If a string is tainted and it is used as the name of a module to (un)load, that is a defect because it could be an integrity or confidentiality vulnerability.

If an integer is tainted and it is used as the amount of space (bytes or elements) to allocate, that is a defect because it could be a confidentiality vulnerability (specifically, a space and time consumed side-channel vulnerability) or an availability vulnerability (specifically, a space exhaustion vulnerability).  Input size may determine allocation size, but programs should ensure allocation sizes are reasonable.

If an operation is performed on a secret tainted value that is not a fixnum, that is a defect because only fixnums can be processed in [constant time](https://en.wikipedia.org/wiki/Timing_attack).  If an operation other than bitwise not, arithmetic negation, bitwise and, arithmetic or logical shift left or right by a constant amount [0, 63], rotate left or right by a constant amount [0, 63], bitwise xor, bitwise or, addition, subtraction, equality comparison, ordered comparison, minimum or maximum of two numbers, absolute value, or assignment is performed on a secret tainted value, that is a defect because it could be a confidentiality vulnerability (specifically, a time consumed side-channel vulnerability).  Arithmetic or logical shift left or right by a variable amount [0, 63], rotate left or right by a variable amount [0, 63], carry-less multiplication (a.k.a. xor multiplication), and multiplication could be supported if old hardware is not supported.  These operations correspond to constant-time opcodes.

If a value is secret tainted and it is used in a conditional (branch or loop) or data structure indexing (assignment or lookup) expression, that is a defect because it could be a confidentiality vulnerability (specifically, a time consumed side-channel vulnerability).


### Using Taint Checking

Taint checking should be built-in.  The possible combinations of taint will cause a combinatorial explosion of required definitions if it is built atop phantom types and typestate.  Taint checking is built-in in Macroni.

Procedures that perform input should input taint their return values.

Procedures that process secrets (e.g. passwords or cryptography) should normally secret taint their secrets and have untaintable return values.

Procedures that perform output should have only untaintable parameters.

Macroni’s event system enforces these rules.  Events received will be input tainted because they cannot be trusted.  This does not apply to sender values because they must be trusted and the kernel or runtime system ensures they are trustworthy.  Events sent must be untainted because their contents should be validated and sanitized before being sent.  This removes most of the burden from the programmer.

If the programmer insists on storing secrets in a data structure (e.g. to implement a [cryptographic keyring](https://en.wikipedia.org/wiki/Keyring_(cryptography))), the programmer must secret untaint the secrets before storing them and the programmer should secret taint the secrets when retrieving them.  The programmer should manually ensure storing the secrets in the data structure does not cause a time consumed side-channel vulnerability.

Be aware that taint checking cannot detect hardware side-channels!  Commodity computer hardware usually makes no attempt to eliminate space consumed, time consumed, power consumed, and radiation produced side-channels.

Be aware that taint checking cannot detect I/O side-channels!  Ways to eliminate I/O side-channels are described in the I/O document.


## Implementation

All currently popular CPUs use frequency boosting to improve time efficiency, which causes a confidentiality vulnerability (specifically, a [Hertzbleed vulnerability](https://www.hertzbleed.com/)).  1s consume more power and produce more heat than 0s.  When frequency boosting is in use, the count of 1s in the secret is revealed by how quickly the core throttles to prevent itself from overheating.  This makes guessing the respective secret practical by reducing the search space from all permutations of 0s and 1s to all permutations of a specific count of 0s and 1s.

In other words, when frequency boosting is in use, constant-time opcodes are not constant-time.  Their timing becomes data operand dependent.

All currently popular CPUs provide a way to disable frequency boosting on specific cores.  Cores can take hundreds of milliseconds to change frequencies, so dynamically disabling frequency boosting is impractical, but statically disabling frequency boosting on one or more cores and only processing secrets on those cores is practical.


### When Running as a Process

No currently popular operating systems provide a way to disable frequency boosting on specific cores, but all currently popular operating systems provide a way to disable frequency boosting globally.

When running as a process, the owner-user can either tell the operating system to disable frequency boosting globally or tolerate this vulnerability.


### When Running on Bare Metal

When running on bare metal, Macroni can statically disable frequency boosting on one or more cores and only execute sandboxes processing secrets on those cores.  The compiler preserves the information necessary for the scheduler to do that.


## See Also
* [Analyses for Code Quality](Analyses_for_Code_Quality.md)
* [Built-Ins](Built-Ins.md)
* [Capability Security Model](Capability_Security_Model.md)
* [Compiler](Compiler.md)
* [Events](Events.md)
* [Garbage Collector](Garbage_Collector.md)
* [I/O](Input_Output.md)
* [Sandboxes](Sandboxes.md)
* [Scheduler](Scheduler.md)
