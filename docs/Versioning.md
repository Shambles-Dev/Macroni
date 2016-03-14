Versioning
==========

## Overview

Simplified Semantic Versioning adopts [Semantic Versioning](https://semver.org/)’s major, minor, and patch numbering scheme, but it removes the inconsistencies and unnecessary features.

Macroni uses this versioning scheme to avoid [path dependence](https://en.wikipedia.org/wiki/Path_dependence).  Each file format and network protocol that Macroni defines uses a fixed header that indicates its data type and version.  The rest of their format is determined by their version.  The header may be stored externally if necessary.  For example, Macroni source code is stored in text files for compatibility, so the headers of the source code files are stored in their package file.  The version is used to select the code to process the data.  The Macroni programming language can change arbitrarily so long as the [ABI](https://en.wikipedia.org/wiki/Application_binary_interface) remains fixed because the headers of the source code files can be used to select the correct compiler to compile them with.  Other file formats and network protocols can change while maintaining [backward compatibility](https://en.wikipedia.org/wiki/Backward_compatibility) the same way.  This eases migration.

Macroni enforces the use of this versioning scheme so that programmers’ idiosyncrasies cannot cause versioning hell.  Versioning hell is a situation in which a computing system cannot safely select code to process data or cannot safely upgrade code because there is no standard versioning scheme that it understands.


## Details

Simplified Semantic Versioning differs from Semantic Versioning in that major version 0 is not handled specially, the minor version is initially 0, and there is no support for pre-release or build metadata.

The major, minor, and patch numbers are all non-negative integers.  They are all initially 0.

The major version increments by 1 when changing or removing observable behavior.  The major version must be equal to that required for a dependency to be satisfied.  Multiple major versions of the same software can be installed and used so that backward compatibility can be maintained.

The minor version increments by 1 when including new observable behavior.  The minor version must be greater than or equal to that required for a dependency to be satisfied.  Only the greatest installed minor version can be used.

The patch version increments by 1 when a defect is corrected.  The patch version must be greater than or equal to that required for a dependency to be satisfied.  Only the greatest installed patch version can be used.  Most file formats and network protocols that do not contain code do not use a patch version because they do not have a notion of defects.

A version is represented by concatenating the major, minor, and patch numbers in that order with periods between them (e.g. `0.0.0`).  Decimal notation is always used.  There are never signs or leading 0s.  There is never a leading v.


## See Also
* [Analyses for Code Quality](Analyses_for_Code_Quality.md)
* [Compiler](Compiler.md)
* [Packages](Packages.md)
