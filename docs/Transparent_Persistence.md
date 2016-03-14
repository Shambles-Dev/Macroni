Transparent Persistence
=======================

## Overview

Transparent persistence causes all memory, including processor and device state, to appear to be non-volatile.


## Details

The checkpoint interval can be configured by the owner-user.

Macroni recovers from low memory and high load situations by terminating processes whose GUI is not in focus when they are not intended to keep executing in the background.


## Implementation

### The Correct Way




### On Currently Popular Hardware

Macroni reuses its microrebooting mechanism to periodically extract all the hard state of the computing system then writes it to the drive in a location that only the kernel or runtime system can read or write.


## See Also
* [Availability](Availability.md)
* [Capability Security Model](Capability_Security_Model.md)
* [File System](File_System.md)
* [Microrebooting](Microrebooting.md)
* [User Interface](User_Interface.md)
