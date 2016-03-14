Built-Ins
=========

## Overview

Macroni’s built-ins include only what is necessary for maintainability, safety, security, or efficiency.


## Details

The only observable differences between built-in and user-defined constructs are built-ins are implicitly defined and have no associated source code (e.g. both use the object system) because that ensures consistency.

The built-in environment is immutable because that ensures all state is encapsulated.


### Immutable, Code-Free Types

Only the following are immutable, code-free types:
* null
* number (including Boolean)
* character
* string
* symbol
* immutable vector
* immutable set
* immutable dictionary
* system error

The numeric tower is described in its own document.  Note that quantities are not considered code-free because they may be user-defined.

There is a distinct character type because some valid characters are not valid strings or symbols (e.g. bidirectional control characters).

Immutable, code-free types are the only types that may be passed between macros because that ensures code is immutable and no state survives macro expansion.  Ensuring no state survives macro expansion also requires the effect system.


### Sandboxes

Sandboxes are described in their own document.

Immutable, code-free types and sandboxes are normally the only types that may be passed between sandboxes because that ensures thread safety, no code and only exported state survives microrebooting, and code can be hot-swapped easily and efficiently.  Ensuring no code and only exported state survives microrebooting and code can be hot-swapped easily and efficiently also requires state export to return only immutable, code-free types (no sandboxes).  Sandboxes are passed between sandboxes by identity (sharing), not by value (copying) like immutable types, because that is required for correct semantics.


### This Document Is Incomplete!




## Implementation

### When Running as a Process

When running as a process, Macroni does not change or include additional built-ins because that ensures code compatible when running as a process is compatible when running on bare metal.


### When Running on Bare Metal

When running on bare metal, Macroni includes additional built-in types for defining drivers:
* IRQ
* PIO address range
* MMIO address range
* DMA buffer
* DMA channel

These types may be passed between sandboxes.

Some types may be passed between sandboxes but cannot be shared in the sense that more than one sandbox can use them.  Any sandbox other than the one that allocated a value that cannot be shared will crash from a defect error when attempting to use it.

IRQs may be shared.  All sandboxes using a shared IRQ agree to share it or crash from a defect error.

Address ranges are closed intervals.

MMIO address ranges and DMA buffers cannot move, which is why the kernel uses a free list allocator for them.  They are passed between sandboxes by identity (sharing), not by value (copying) like immutable types, because that is required for correct semantics.

PIO address ranges, MMIO address ranges, DMA buffers, and DMA channels cannot be shared.  Sandboxes may be shared instead of DMA buffers.


## See Also
* [Booleans](Booleans.md)
* [Characters and Strings](Characters_and_Strings.md)
* [Compiler](Compiler.md)
* [Design by Contract](Design_by_Contract.md)
* [Dimensional Analysis](Dimensional_Analysis.md)
* [Effect System](Effect_System.md)
* [Errors](Errors.md)
* [Events](Events.md)
* [Macros](Macros.md)
* [Microrebooting](Microrebooting.md)
* [Modules](Modules.md)
* [Naming and Parameter Order Conventions](Naming_and_Parameter_Order_Conventions.md)
* [Null](Null.md)
* [Numeric Tower](Numeric_Tower.md)
* [Object System](Object_System.md)
* [Pattern Matching for Destructuring](Pattern_Matching_for_Destructuring.md)
* [SREs](sre.txt)
* [Sandboxes](Sandboxes.md)
* [Sets and Dictionaries](Sets_and_Dictionaries.md)
* [Taint Checking](Taint_Checking.md)
* [Vectors](Vectors.md)
