I/O
===

## Overview

Macroni represents all I/O, including I/O errors, as values.  This makes all I/O first-class and accurately represents how I/O hardware works (reading and writing I/O addresses).

All I/O is performed via Macroni’s event system.  This makes all I/O asynchronous.


## Details

### I/O Servers




### I/O Scheduling




### Fingerprinting

[Fingerprinting](https://en.wikipedia.org/wiki/Device_fingerprint) should be eliminated because that makes targeting potential victims of other attacks more difficult.

Fingerprinting is performed via noting uncommon behaviors or properties or via file formats or network protocols that demand information they do not need to know.

Implementations should imitate the behavior of the currently most popular implementation that is not problematic.  This serendipitously improves compatibility.  Implementations of file formats or network protocols that demand information they do not need to know and cannot validate should lie about that information.


### I/O Side-Channels

I/O can cause side-channels.  For example, if a program sends what a user types across a network as they type it, it is possible to fingerprint and track that user via their [keystroke dynamics](https://en.wikipedia.org/wiki/Keystroke_dynamics) and [infer what they are typing even when it is encrypted](https://people.eecs.berkeley.edu/~daw/papers/ssh-use01.pdf).  In this example, the secrets are encrypted, so they should no longer be secret tainted, so taint checking cannot detect these vulnerabilities.

Space consumed side-channels and time consumed side-channels are the only side-channels that are usually observable remotely.  Space consumed I/O side-channels are eliminated by adding dummy data.  Time consumed I/O side-channels are eliminated by adding delays.  The programmer should manually ensure that adding and removing dummy data does not cause a time consumed side-channel.

Side-channels can be eliminated by eliminating correlation.  The correlation in I/O side-channels can be eliminated by adding enough noise to make recognizing the signal impractical for eavesdroppers.  The noise required depends on the nature of the signal.  Be aware that this is only effective when the noise imitates all the statistical patterns of the signal across all channels the eavesdroppers can observe and the eavesdroppers cannot cause the signal to repeat!  If the noise does not imitate all the statistical patterns of the signal across all channels the eavesdroppers can observe, the noise can be removed by ignoring invalid patterns.  Statistical patterns include history analogous to the way that only certain following characters could form valid words.  Channels are not independent (e.g. if no valid message matches the observed space and time consumption, it is obviously noise, even if the space and time consumption are plausible independently).  If the eavesdroppers can cause the signal to repeat, the noise can be removed by averaging enough samples.

Side-channels can be eliminated by eliminating modulation.  The modulation in space consumed I/O side-channels can be eliminated by padding messages with dummy data to make them all consume the same amount of space.  The modulation in time consumed I/O side-channels can be eliminated by delaying messages to make them all consume the same amount of time.  When eliminating modulation is impossible because the space or time consumption of messages is unbounded, it is usually possible to quantize the space and time consumption of messages enough to make recovering the secrets impractical.  The quantizing required depends on how much the space and time consumption reveal about the secrets.

Sometimes I/O side-channels can be eliminated with a generic solution.  For example, storage I/O side-channels can be eliminated by using per-program storage throughput reservations/quotas, using per-program storage space reservations/quotas, and denying most programs the capability to read the space consumed or the space free on storage devices.

Sometimes I/O side-channels can only be eliminated with a custom solution.  For example, network I/O side-channels can be eliminated by using per-program network throughput reservations/quotas and designing network protocols to add sufficient space and time noise to messages, eliminate modulation of the space and time consumption of messages, or sufficiently quantize the space and time consumption of messages.

Sometimes I/O side-channels are impossible to eliminate.  For example, human interface I/O side-channels cannot be eliminated because the latency (added to input) would make programs like video games and visual art editors unusable.

The cure is usually worse than the disease.  Eliminating storage and network I/O side-channels would drastically worsen the throughput and latency of storage and network devices.  That could cause more data to be lost if a computer failed (e.g. from a power outage), which would be unacceptable in many environments (e.g. financial, medical, or military).

It is probably impossible to obtain the cooperation necessary to eliminate network I/O side-channels.  Most people do not care enough about security.

For these reasons, Macroni does not attempt to eliminate I/O side-channels.

Note that observable modulation does not always cause a side-channel vulnerability.  It only causes a side-channel vulnerability if it is correlated with secrets such that recovering the secrets is practical.

Programmers should be aware that these vulnerabilities exist and attempt to recognize them in their software.  If they are practical to eliminate, they should be eliminated.  If they are not practical to eliminate, users should be warned of their presence.

Users should decide if the risks of using software with these vulnerabilities outweigh the benefits.  If the risks outweigh the benefits, users should consider using low-tech alternatives because those are usually much less vulnerable.


## Implementation

### When Running as a Process




### When Running on Bare Metal




## See Also
* [Availability](Availability.md)
* [Capability Security Model](Capability_Security_Model.md)
* [Compatibility](Compatibility.md)
* [File System](File_System.md)
* [Sandboxes](Sandboxes.md)
* [System Structure](System_Structure.md)
* [Taint Checking](Taint_Checking.md)
* [User Interface](User_Interface.md)
