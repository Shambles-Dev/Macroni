Naming and Parameter Order Conventions
======================================

## Overview

Macroni’s naming conventions are similar to Scheme’s.  The most significant deviation is procedure names are abbreviated instead of parameter names because that prevents obscuring the structure of expressions with long names while reserving long names for the less familiar variables in definitions.

Macroni is a [verb-object-subject word order](https://en.wikipedia.org/wiki/Verb%E2%80%93object%E2%80%93subject_word_order) language because it is a Lisp dialect and that is the parameter order that is most useful for [partial application](https://en.wikipedia.org/wiki/Partial_application).  Note that indexing forms accept the index before the data structure because that is implied by verb-subject-object word order and that is the parameter order that is most useful for partial application, and partial application is not automatic in Macroni because variadic procedures are supported.


## Details




## See Also
* [Analyses for Code Quality](Analyses_for_Code_Quality.md)
* [Compiler](Compiler.md)
