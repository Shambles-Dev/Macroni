> [!NOTE]
> Macroni is in its design phase.  There is no implementation yet.

Macroni
=======

[Macroni](docs/Name.md) is an operating system (that can also run as a process) with an integrated development environment for a Lisp dialect.

Macroni combines many solutions to problems most computing systems have.

<table>
  <tr>
    <th colspan="2">Social Features</th>
  </tr>
  <tr>
    <th>Problem</th>
    <th>Solution</th>
  </tr>
  <tr>
    <td><p>Untrustworthy computing is ubiquitous.</p></td>
    <td><p>Macroni is <a href="https://en.wikipedia.org/wiki/Open_source">open source</a>.</p></td>
  </tr>
  <tr>
    <td><p>Plutocrats deprive others of freedom.</p></td>
    <td><p>Macroni is licensed under the <a href="LICENSE.txt">AGPLv3</a>.</p></td>
  </tr>
  <tr>
    <td><p>Human replacement technology is destroying livelihoods, privacy, autonomy, security, freedom, creativity, and progress.</p></td>
    <td><p>Macroni promotes <a href="docs/Evolutionary_Problems_and_Solutions.md">intelligence augmentation technology</a> by exposing all software as a toolbox instead of a black box and leaving consequential decisions to humans.</p></td>
  </tr>
  <tr>
    <td>
      <p>Most governments and computing cartels seem to believe they have the right to observe and interfere with all data storage and communication.</p>
      <p>Most computing cartels seem to believe they alone own the hardware, software, electricity, and Internet service their customers pay for and the content their customers create.</p>
      <p>Most computing cartels seem to believe they have the right to extort or forbid others from selling, gifting, or repairing hardware or software.</p>
    </td>
    <td><p>Macroni’s design respects human rights and sane property rights by helping the person who paid for or was gifted the hardware stay in control of their computer.</p></td>
  </tr>
  <tr>
    <td><p>Unaccountability causes software to get worse over time.</p></td>
    <td><p>Macroni exposes the sources of unreliability and inefficiency to cause software to get better over time.</p></td>
  </tr>
</table>

<table>
  <tr>
    <th colspan="2">Operating System Features</th>
  </tr>
  <tr>
    <th>Problem</th>
    <th>Solution</th>
  </tr>
  <tr>
    <td><p>Most attempts to improve upon currently popular operating systems do not attempt to remain compatible with them.</p></td>
    <td><p>Macroni remains <a href="docs/Compatibility.md">compatible</a> with currently popular operating systems.</p></td>
  </tr>
  <tr>
    <td><p>Most operating systems use the obsolete and insecure concept of system-wide accounts.</p></td>
    <td>
      <p>Macroni supports multiple usage models:
        <ul>
          <li>personal computing – where there are no accounts</li>
          <li>network services – where each network server may define its own concept of accounts and provide accounts to a different set of users</li>
        </ul>
      </p>
      <p>The usage models can coexist.  For example, the owner-user can host and play an online game.</p>
    </td>
  </tr>
  <tr>
    <td><p>Most operating systems require a lot of manual management.</p></td>
    <td>
      <p>Hardware interfaces and network protocols allowing, Macroni is self-managing:
        <ul>
          <li>self-configuring</li>
          <li>self-protecting</li>
          <li>self-healing</li>
          <li>self-optimizing</li>
        </ul>
      </p>
      <p>This only minimizes manual management.  It does not automate consequential decisions because the owner-user could disagree with its decisions.</p>
    </td>
  </tr>
  <tr>
    <td>
      <p>Most file systems are inefficient to search and do not allow tagging contents to improve search.</p>
      <p>Most file systems cannot ensure a mutation, which may affect multiple files or directories, occurs completely or not at all (“<a href="https://en.wikipedia.org/wiki/ACID#Atomicity">atomicity</a>”).</p>
      <p>Most file systems cannot ensure their contents are not corrupt (“<a href="https://en.wikipedia.org/wiki/ACID#Consistency">consistency</a>”).</p>
      <p>Most file systems cannot ensure their contents are shared among multiple threads safely (“<a href="https://en.wikipedia.org/wiki/ACID#Isolation">isolation</a>”).</p>
      <p>Most file systems cannot ensure a mutation, which may affect multiple files or directories, is stored completely before they report success (“<a href="https://en.wikipedia.org/wiki/ACID#Durability">durability</a>”).</p>
      <p>Most file systems cannot adapt to differences in storage devices (e.g. mechanical drives’ slow seeking, shingled mechanical drives’ slow writing, and flash drives’ finite endurance).</p>
      <p>Most file systems cannot adapt to changes in the space delegated to them or the storage devices they are spread across (including I/O parallelism).</p>
      <p>Most file systems cannot compress, deduplicate, <a href="https://en.wikipedia.org/wiki/Block_suballocation">tail pack</a>, defragment, and encrypt contents.</p>
      <p>Most file systems cannot be mounted read-only and store writes elsewhere (e.g. to a RAM drive).  This is useful for live media (e.g. system recovery tools).</p>
      <p>Most file systems cannot perform backups while the file system is in use.</p>
      <p>Most file systems cannot detect and correct bit rot.</p>
      <p>Most file systems do not require file system paths to be <a href="https://www.unicode.org/reports/tr15/">NFC</a> <a href="https://www.unicode.org/versions/latest/">UTF-8</a> without a <a href="https://en.wikipedia.org/wiki/Byte_order_mark">BOM</a>.</p>
      <p>Most file systems do not forbid file system path components from containing unterminated bidirectional control characters.</p>
      <p>Most file systems use harmful attributes (e.g. access time and hidden) and obsolete permissions (e.g. readable, writable, and executable by user, group, and others).</p>
      <p>Most file systems cannot undo accidents by recovering old <a href="https://en.wikipedia.org/wiki/Versioning_file_system">versions</a> of files or directories.</p>
    </td>
    <td>
      <p>Macroni’s <a href="docs/File_System.md">database file system</a> solves these problems.</p>
      <p><a href="https://en.wikipedia.org/wiki/Extensible_Metadata_Platform">XMP</a> <a href="https://en.wikipedia.org/wiki/Sidecar_file">sidecar files</a> store metadata when exporting to or importing from currently popular file systems.</p>
    </td>
  </tr>
  <tr>
    <td>
      <p>Software is often monolithic, causing maintenance, satisfaction, and efficiency problems.</p>
      <p>Some packaging systems can only install or update packages from a single repository, causing a single point of failure for package management and security.</p>
      <p>Most packaging systems distribute executables, causing repository bloat and making trust difficult.</p>
      <p>Some packaging systems allow packages to be spoofed or tampered with to spread malware.</p>
      <p>Manually handling package dependencies is annoying.</p>
      <p>Most packaging systems allow packages to damage other packages’ or users’ files, (un)install other packages without the owner-user’s consent, and annoy users with prompts (e.g. about licensing, configuration, or feedback) upon (un)installation.</p>
      <p>Package upgrades can break software.</p>
    </td>
    <td><p>Macroni’s <a href="docs/Packages.md">packaging system</a> solves these problems.</p></td>
  </tr>
  <tr>
    <td><p>Most operating systems suffer from versioning hell.</p></td>
    <td><p>Macroni enforces the use of <a href="docs/Versioning.md">Simplified Semantic Versioning</a>.</p></td>
  </tr>
  <tr>
    <td><p>Some software <a href="https://www.gnu.org/philosophy/who-does-that-server-really-serve.en.html">only works when it can periodically or constantly connect to a network server</a>.  This is incompatible with unreliable network connections, air gaps, and software preservation.</p></td>
    <td><p>Macroni is not a Service as a Software Substitute.  It works offline indefinitely.</p></td>
  </tr>
  <tr>
    <td>
      <p>Processes crashing or hanging can cause data loss.</p>
      <p>Restarting processes to update them is annoying.</p>
    </td>
    <td><p>Macroni uses <a href="docs/Microrebooting.md">microrebooting</a> to solve these problems.</p></td>
  </tr>
  <tr>
    <td>
      <p>Power loss or operating systems crashing or hanging can cause data loss.</p>
      <p>Some operating systems force, often unexpected, reboots to update themselves, which can cause data loss.</p>
      <p>Restarting operating systems to update them is annoying.</p>
    </td>
    <td>
      <p>Macroni uses <a href="docs/Transparent_Persistence.md">transparent persistence</a> to solve these problems.</p>
      <p>Macroni will never force a reboot because the owner-user could disagree with that decision.  When the owner-user chooses to reboot, transparent persistence will restore all process’ local state.</p>
    </td>
  </tr>
  <tr>
    <td><p>Most code is vulnerable to attacks on integrity and confidentiality.</p></td>
    <td>
      <p>Macroni uses <a href="docs/Capability_Security_Model.md">the capability security model</a> between processes.</p>
      <p>The rest of this problem is solved at the programming language level.</p>
    </td>
  </tr>
  <tr>
    <td><p>Most code is vulnerable to attacks on availability.</p></td>
    <td><p>The operating system constructs that consume space or time have been identified and minimized and their <a href="docs/Availability.md">availability problems solved</a>.</p></td>
  </tr>
  <tr>
    <td>
      <p>Most <a href="https://en.wikipedia.org/wiki/Graphical_user_interface">GUIs</a> are resolution dependent, making them scale poorly.</p>
      <p>Secure user interaction is usually unnatural and annoying.</p>
      <p>Lack of a common, consistent, rich set of <a href="https://en.wikipedia.org/wiki/Graphical_widget">widgets</a> and <a href="https://en.wikipedia.org/wiki/Flat_design">flat design</a> have caused GUI usability to regress to early 1980s norms.</p>
    </td>
    <td><p>Macroni’s <a href="docs/User_Interface.md">user interface</a> solves these problems.</p></td>
  </tr>
</table>

<table>
  <tr>
    <th colspan="2">Integrated Development Environment Features</th>
  </tr>
  <tr>
    <th>Problem</th>
    <th>Solution</th>
  </tr>
  <tr>
    <td><p>Manually matching brackets is difficult.</p></td>
    <td><p>Macroni’s <a href="docs/Source_Code_Editor.md">source code editor</a> is a structure editor that can toggle highlighting based on the depth of bracket nesting around the cursor.</p></td>
  </tr>
  <tr>
    <td><p>Noticing changes damaged code is usually difficult.</p></td>
    <td><p>Macroni’s source code editor performs <a href="docs/Analyses_for_Code_Quality.md">analyses to warn about bad practices and defects</a> in the background.</p></td>
  </tr>
  <tr>
    <td>
      <p>Discovering code is usually difficult.</p>
      <p>Auditing code is usually difficult.</p>
    </td>
    <td>
      <p>Macroni’s source code editor can <a href="docs/Code_Searching.md">search for code</a>.</p>
      <p>Macroni supports <a href="https://en.wikipedia.org/wiki/Docstring">docstrings</a>.</p>
      <p>Auditing code is easier when you can search for type definitions and untainting procedures.</p>
    </td>
  </tr>
  <tr>
    <td><p>Comprehending code is usually difficult.</p></td>
    <td><p>Macroni’s source code editor can <a href="docs/Code_Cross-Referencing.md">cross-reference code</a>.</p></td>
  </tr>
  <tr>
    <td><p>Manually refactoring code is difficult.</p></td>
    <td><p>Macroni’s source code editor provides <a href="docs/Automated_Refactoring.md">automated refactoring</a>.</p></td>
  </tr>
  <tr>
    <td><p>Most development environments suffer from build system hell.</p></td>
    <td><p>Macroni is self-building.  Package building is standardized.</p></td>
  </tr>
  <tr>
    <td>
      <p>Testing your comprehension of code is usually difficult.</p>
      <p>When a programming language provides listeners, their transcripts are usually unsuited for use as source code.</p>
    </td>
    <td>
      <p>Macroni provides <a href="docs/Listeners.md">listeners</a> (a.k.a. REPLs) for interactively testing code.</p>
      <p>Macroni’s listeners’ transcripts require minimal editing to use as source code.</p>
    </td>
  </tr>
  <tr>
    <td><p>Discovering all relevant invariants is usually difficult.</p></td>
    <td><p>Macroni provides an <a href="docs/Invariant_Detector.md">invariant detector</a>.</p></td>
  </tr>
  <tr>
    <td><p>Discovering defects by testing is usually difficult.</p></td>
    <td><p>Macroni provides a <a href="docs/Property-Based_Tester.md">property-based tester</a>.</p></td>
  </tr>
  <tr>
    <td><p>Locating unreliable code is usually difficult.</p></td>
    <td>
      <p>Macroni’s <a href="docs/Debugger.md">debugger</a> can display modules sorted by how often they caused crashes, hangs, or corruption.  Macroni automatically reports crashing and hanging.  A sandbox can report corruption as the reason for destructing a sub-sandbox.  A module is blamed for crashing or hanging when the program counter was in it at the time of destruction, and the debugger can display the source locations of those program counters.  A module is blamed for corruption when it was loaded directly into a sandbox destructed for that reason, but no source locations can be displayed, so convert corruption to crashing via assertions.</p>
      <p>The program package responsible for each error report is recorded.  This exposes which modules are causing problems for a program.  It also exposes malware attempting to defame modules in other packages and makes removing false reports possible.</p>
    </td>
  </tr>
  <tr>
    <td><p>Comprehending defects is usually difficult.</p></td>
    <td><p>Macroni’s debugger records the last several steps of execution and their resulting values along with the memory dump.  How many to record can be configured by the owner-user.</p></td>
  </tr>
  <tr>
    <td><p>Locating wasted space and memory leaks is usually difficult.</p></td>
    <td><p>Macroni provides a <a href="docs/Space_Profiler.md">space profiler</a>.</p></td>
  </tr>
  <tr>
    <td><p>Locating wasted time is usually difficult.</p></td>
    <td><p>Macroni provides a <a href="docs/Time_Profiler.md">time profiler</a>.</p></td>
  </tr>
  <tr>
    <td><p>Comprehending defects in regular expressions is usually difficult.</p></td>
    <td><p>Macroni provides a <a href="docs/Regular_Expression_Debugger.md">regular expression debugger</a>.</p></td>
  </tr>
  <tr>
    <td><p>Specifying a GUI by programming is like painting by typing.</p></td>
    <td><p>Macroni provides a <a href="docs/GUI_Builder.md">GUI builder</a>.</p></td>
  </tr>
</table>

<table>
  <tr>
    <th colspan="2">Lisp Features</th>
  </tr>
  <tr>
    <th>Problem</th>
    <th>Solution</th>
  </tr>
  <tr>
    <td>
      <p>Different programming languages have different strengths, so programmers should use the right tool for the job.</p>
      <p>Unfortunately, different programming languages usually do not link together.</p>
    </td>
    <td>
      <p>Lisp’s strength is extending itself, including embedding other programming languages in itself, so it is the right tool for every job.  It can generate code to define its runtime system or for computing systems too limited to host it.</p>
      <p>Lisp links with itself.</p>
    </td>
  </tr>
  <tr>
    <td><p>Discovering defects is usually difficult.</p></td>
    <td><p>Lisp macros can perform any static or dynamic analysis.</p></td>
  </tr>
  <tr>
    <td><p>Debugging macros and external code generators is usually difficult.</p></td>
    <td><p>Lisp macros are no more difficult to debug than functions.  Errors report the macro call location, not a location in the generated code.</p></td>
  </tr>
  <tr>
    <td><p>Programming languages that use implicit grouping often cause unintended evaluation and order of evaluation defects.</p></td>
    <td><p>Lisp uses only explicit grouping.</p></td>
  </tr>
</table>

<table>
  <tr>
    <th colspan="2">Lisp Dialect Features</th>
  </tr>
  <tr>
    <th>Problem</th>
    <th>Solution</th>
  </tr>
  <tr>
    <td><p>Most programming languages and computing systems are designed for obsolete batch processing.</p></td>
    <td><p>Macroni is <a href="docs/Events.md">event-driven</a>, ultimately by hardware interrupts.</p></td>
  </tr>
  <tr>
    <td><p>Some programming languages ignore errors, maximizing the destructiveness of defects and the difficulty of debugging.</p></td>
    <td><p>Macroni does not ignore <a href="docs/Errors.md">errors</a>.</p></td>
  </tr>
  <tr>
    <td><p>Most programming languages overcomplicate error handling.</p></td>
    <td><p>Macroni handles defect errors by microrebooting and represents system errors as values.</p></td>
  </tr>
  <td><p>Most code is vulnerable to attacks on integrity and confidentiality.</p></td>
  <td>
    <p>Macroni uses the capability security model and <a href="docs/Taint_Checking.md">taint checking</a> within processes.</p>
    <p>The rest of this problem is solved at the operating system level.</p>
  </td>
  <tr>
    <td><p>Most macro systems are dangerous, limited, or verbose.</p></td>
    <td><p>Macroni uses an implicit renaming <a href="docs/Macros.md">macro system</a> that is hygienic by default, procedural, and concise.</p></td>
  </tr>
  <tr>
    <td><p>Some programming languages use mutable literals, causing copying or shared state when copying was intended.</p></td>
    <td><p>Macroni uses immutable literals.</p></td>
  </tr>
  <tr>
    <td><p>Lists waste space and time.</p></td>
    <td><p>Macroni uses immutable <a href="docs/Vectors.md">vectors</a> (trees of short arrays) instead of lists.  Immutable vectors support structure sharing and efficient random access with less pointer overhead and more locality of reference, and they can be efficiently constructed forward.</p></td>
  </tr>
  <tr>
    <td><p>Some programming languages use 1-based array indexing, making computing indices error-prone and verbose.</p></td>
    <td><p>Macroni uses 0-based vector indexing.</p></td>
  </tr>
  <tr>
    <td><p>Some programming languages do not perform bounds checking, causing <a href="https://en.wikipedia.org/wiki/Buffer_overflow">buffer overflow</a> vulnerabilities.</p></td>
    <td><p>Macroni performs bounds checking.</p></td>
  </tr>
  <tr>
    <td>
      <p>Most Lisp dialects conflate the empty list, the null pointer, and false, causing <a href="https://en.wikipedia.org/wiki/Semipredicate_problem">the semipredicate problem</a>.</p>
      <p>Some programming languages conflate the null pointer and 0, causing the semipredicate problem.</p>
    </td>
    <td><p>Macroni distinguishes between <code>'()</code> (the empty immutable vector), <a href="docs/Null.md"><code>#null</code></a>, <code>0</code>, and <code>#f</code>.</p></td>
  </tr>
  <tr>
    <td><p>Most Lisp dialects are case-insensitive, unlike math and most computing systems.</p></td>
    <td><p>Macroni is case-sensitive, but uppercase in identifiers is intended to only be used for math transcription and interoperability.</p></td>
  </tr>
  <tr>
    <td><p>Some programming languages do not allow modules to control what they import or export, causing name collisions and exposing implementation details.</p></td>
    <td>
      <p>Macroni only imports and exports what <a href="docs/Modules.md">modules</a> explicitly request with the exception of built-ins.</p>
      <p>Built-ins are locally implicitly redefined instead of causing name collision defects so that built-ins can be extended without breaking code.</p>
      <p>There is no way to import or export everything from a module so that modules can be extended without breaking code.</p>
      <p>Imported and exported constructs can be locally renamed for readability and compatibility.</p>
    </td>
  </tr>
  <tr>
    <td><p>Global scope causes maintenance problems.</p></td>
    <td><p>Macroni’s widest scope is module scope.</p></td>
  </tr>
  <tr>
    <td><p>Some programming languages do not support shadowing, breaking composition.</p></td>
    <td><p>Macroni supports static scope and inner scopes shadowing outer scopes (i.e. lexical scope).</p></td>
  </tr>
  <tr>
    <td><p>Dynamic scope does not compose.</p></td>
    <td><p>Macroni does not support dynamic scope.</p></td>
  </tr>
  <tr>
    <td><p>Some Lisp dialects use separate namespaces for variables and procedures, making functional programming verbose.</p></td>
    <td><p>Macroni uses the same namespace for variables and procedures.</p></td>
  </tr>
  <tr>
    <td><p>Some programming languages’ built-in constructs are unnecessarily inconsistent with user-defined constructs, interrupting the programmer’s <a href="https://en.wikipedia.org/wiki/Flow_(psychology)">flow</a> and causing <a href="https://en.wikipedia.org/wiki/No_Silver_Bullet">accidental complexity</a>.</p></td>
    <td><p>Macroni’s <a href="docs/Built-Ins.md">built-in constructs</a> are as consistent as possible with user-defined constructs.</p></td>
  </tr>
  <tr>
    <td><p>Most programming languages suffer from <a href="https://en.wikipedia.org/wiki/Expression_problem">the expression problem</a>.</p></td>
    <td><p>Macroni’s <a href="docs/Object_System.md">object system</a> can separately define types and generic functions while enforcing encapsulation.</p></td>
  </tr>
  <tr>
    <td><p>Asserting all relevant invariants is usually error-prone and verbose.</p></td>
    <td><p>Macroni supports <a href="docs/Design_by_Contract.md">design by contract</a>.</p></td>
  </tr>
  <tr>
    <td>
      <p>Most Lisp dialects coerce the empty list and false to false and all other values to true in Boolean contexts, which is useless.</p>
      <p>Most Lisp dialects do not coerce false to 0 and true to 1 in arithmetic contexts, which prevents the use of bitwise operations and branchless programming.</p>
    </td>
    <td>
      <p>In Macroni, the <code>bool&lt;-</code> generic function converts empty data structures, <code>""</code>, <code>#null</code>, zero, and <code>#f</code> to <code>#f</code> and all other values to <code>#t</code>.  Values are coerced that way in <a href="docs/Booleans.md">Boolean</a> contexts.  Boolean special forms (<code>and</code> and <code>or</code>) always return a Boolean value.  This is useful for bitwise operations, branchless programming, and processing strings and data structures.</p>
      <p>Macroni promotes <code>#f</code> to <code>0</code> and <code>#t</code> to <code>1</code>.</p>
    </td>
  </tr>
  <tr>
    <td><p>Some programming languages use Boolean operators that do not <a href="https://en.wikipedia.org/wiki/Short-circuit_evaluation">short-circuit</a> (stop evaluating subexpressions when the result is known), making programming error-prone, verbose, and inefficient.</p></td>
    <td><p>Macroni’s Boolean special forms short-circuit.</p></td>
  </tr>
  <tr>
    <td>
      <p>Some programming languages only provide floating-point numbers, making working with binary files and network protocols error-prone and verbose.</p>
      <p>Some programming languages do not follow conventions for numeric promotion, making arithmetic verbose.</p>
      <p>Some programming languages do not support syntax for integers in binary and hexadecimal and floating-point numbers in scientific notation without a decimal point, making arithmetic error-prone.</p>
    </td>
    <td>
      <p>Macroni provides the full <a href="docs/Numeric_Tower.md">numeric tower<a>.</p>
      <p>Macroni follows conventions for numeric promotion (e.g. integers are promoted to floating-point numbers when used in arithmetic with them).</p>
      <p>Macroni supports syntax for integers in binary (e.g. <code>#b-101</code>) and hexadecimal (e.g. <code>#x-F00</code>) and floating-point numbers in scientific notation without a decimal point (e.g. <code>-1e-1</code>).</p>
    </td>
  </tr>
  <tr>
    <td><p>Most programming languages ignore arithmetic errors.</p></td>
    <td>
      <p>In Macroni, integer underflow and overflow causes promotion to bignum.  Modular fixnum arithmetic is supported via built-in functions but is not the default.</p>
      <p>In Macroni, integer and floating-point division by zero, floating-point underflow and overflow, and floating-point invalid operations are defects.</p>
    </td>
  </tr>
  <tr>
    <td><p>Most programming languages ignore dimension and unit errors.</p></td>
    <td><p>Macroni performs <a href="docs/Dimensional_Analysis.md">dimensional analysis</a>.</p></td>
  </tr>
  <tr>
    <td><p>Some programming languages use biased rounding or truncation, causing <a href="https://en.wikipedia.org/wiki/Round-off_error">cumulative error</a>.</p></td>
    <td><p>Macroni uses unbiased rounding (round half to even) but provides explicit truncation.</p></td>
  </tr>
  <tr>
    <td><p>Some programming languages define 0⁰ as always being a defect, breaking several branches of math.</p></td>
    <td><p>Macroni defines 0⁰ as 1 for discrete (integer) exponents and as a defect for continuous (non-integer) exponents, following math conventions.</p></td>
  </tr>
  <tr>
    <td>
      <p>Most programming languages only provide quotient (a.k.a. truncating division) and remainder (a.k.a. truncating modulo) despite floor division and modulo being more useful.</p>
      <p>When floor division is provided, sometimes it does not return an integer, making using it error-prone and verbose.</p>
    </td>
    <td><p>Macroni provides floor division returning an integer and (flooring) modulo.</p></td>
  </tr>
  <tr>
    <td><p>Some programming languages use mutable strings despite their mutability being useless and it preventing strings from being hashable or internable.</p></td>
    <td><p>Macroni uses immutable strings.</p></td>
  </tr>
  <tr>
    <td><p>Some programming languages do not support UTF-8, breaking modern text.</p></td>
    <td><p>Macroni source code and dynamically constructed characters, strings, and symbols are NFC UTF-8 without a BOM.  Characters are <a href="https://www.unicode.org/reports/tr29/">extended grapheme clusters</a>.  Positions within a string are measured in such characters, but strings are not random access.  Macroni source code uses LF line endings.  Comments, strings, and symbols cannot contain <a href="https://trojansource.codes/">unterminated bidirectional control characters</a>.  File system path components are represented as byte vectors instead of strings because foreign file system path components may not be valid strings in Macroni.</p></td>
  </tr>
  <tr>
    <td><p>Some Lisp dialects allow whitespace and special characters in symbols, which is only useful for obfuscation.</p></td>
    <td><p>Macroni’s symbols are <a href="https://www.unicode.org/reports/tr31/">UAX #31</a> identifiers (which disallow whitespace and special characters) with adjustments to allow conventional Lisp symbols, but characters outside the <a href="https://en.wikipedia.org/wiki/ASCII">ASCII</a> range in identifiers are intended to only be used for math transcription and interoperability.</p></td>
  </tr>
  <tr>
    <td><p>Regular expressions are usually difficult for humans to read and for structure editors to edit, and they usually support non-regular features that are inefficient.</p></td>
    <td><p>Macroni uses something similar to <a href="docs/sre.txt">SREs</a>.</p></td>
  </tr>
  <tr>
    <td><p>Generators use mutation, so they cannot backtrack.</p></td>
    <td><p>Macroni uses something similar to <a href="https://htmlpreview.github.io/?https://github.com/Shambles-Dev/Macroni/blob/master/docs/SRFI%2041%20%20Streams.htm">Scheme streams</a>.</p></td>
  </tr>
  <tr>
    <td><p>Most programming languages do not represent random access data structures as functions, making using them verbose.</p></td>
    <td><p>Macroni represents random access data structures as functions.</p></td>
  </tr>
  <tr>
    <td><p>Most Lisp dialects have poor support for sets and dictionaries.</p></td>
    <td>
      <p>Macroni provides immutable, mutable, and weak key <a href="docs/Sets_and_Dictionaries.md">dictionaries</a>.</p>
      <p>The syntax for dictionary literals is easy for humans to read and for structure editors to edit (e.g. <code>{("key a" "value a") ("key b" "value b")}</code>).</p>
      <p>Macroni’s dictionaries are insertion order preserving and order insignificant (i.e. dictionaries with equal contents in different orders are equal).  Insertion order is the only order that makes sense when keys are not required to be ordered.  Order preservation in dictionaries is often desired.  Order significance in dictionaries is rarely desired and often surprising.  Dictionary sorting and order significance are easily implemented when dictionaries are insertion order preserving.</p>
      <p>Macroni’s immutable and mutable dictionaries are indexed by value for immutable keys and by identity for mutable keys.  To be clear, they are not indexed by string representation and string keys are compared case-sensitively.  Macroni’s weak key dictionaries are indexed by identity for immutable and mutable keys.  This prevents vulnerability to malicious definitions of hashing and value equality.</p>
      <p>Macroni’s dictionaries can be processed as functions, sets, dictionaries, or sequences of vectors containing key-value pairs.  Set operations on key-value pairs have their uses.</p>
      <p>Implementing Macroni’s environments efficiently in itself and the capability security model require these definitions.</p>
    </td>
  </tr>
  <tr>
    <td><p>State often becomes corrupt.</p></td>
    <td><p>Macroni minimizes state by only allowing <a href="docs/Effect_System.md">mutation</a> where it is necessary (state must survive across events and revocation and confinement of capabilities must work) or unobservable and useful (temporary local state sometimes improves elegance and efficiency).</p></td>
  </tr>
  <tr>
    <td><p>Some programming languages separate allocation and initialization, causing <a href="https://en.wikipedia.org/wiki/Uninitialized_variable">uninitialized values</a> in variables and data structures.</p></td>
    <td><p>Macroni combines allocation and initialization.</p></td>
  </tr>
  <tr>
    <td><p>Most programming languages use the same form for binding and mutation, causing typoed variable names to go undetected and mutation when binding was intended.</p></td>
    <td><p>Macroni uses different forms for binding and mutation.</p></td>
  </tr>
  <tr>
    <td><p>Most Lisp dialects overcomplicate equality.</p></td>
    <td>
      <p>Macroni defines only two equality predicates: <code>is</code> and <code>=</code>.</p>
      <p><code>is</code> tests identity equality (a.k.a. physical equality).  Be aware that <code>is</code> cannot be extended, unlike most built-ins, because security requires identity equality to be trustworthy!</p>
      <p><code>=</code> tests value equality (a.k.a. structural equality).  Be aware that testing the value equality of types incompatible with value equality (e.g. different but equivalent immutable closures) or each other (e.g. most different non-numeric types) will return <code>#f</code> instead of crashing!</p>
      <p>Macroni’s dictionaries require these definitions.</p>
    </td>
  </tr>
  <tr>
    <td><p>Tail calls usually waste space.</p></td>
    <td><p>Macroni performs tail call elimination.</p></td>
  </tr>
  <tr>
    <td><p>Optional and keyword parameters do not fit the execution model.</p></td>
    <td><p>Macroni does not support optional or keyword parameters.  It does support generic functions with different definitions for different arities and variadic parameters.</p></td>
  </tr>
  <tr>
    <td><p>Most programming languages do not define the order of evaluation of all subexpressions, making programming error-prone.</p></td>
    <td><p>Macroni evaluates all non-macro subexpressions once from left to right.  To be clear, the functional position is evaluated the same way as a function argument before any arguments.  Special forms may skip some subexpressions.  Optimizers may use a different order only if the difference would be unobservable.  The behavior of macros is defined by their author, but they should evaluate subexpressions once from left to right unless they have good reason to deviate.</p></td>
  </tr>
  <tr>
    <td><p><a href="https://en.wikipedia.org/wiki/Structured_programming">Unstructured control flow</a> (not single entry, single exit) usually does not compose, makes ensuring initialization and cleanup code is executed correctly difficult, and makes static analyses difficult for humans and computers.</p></td>
    <td><p>Macroni supports only structured control flow.</p></td>
  </tr>
  <tr>
    <td><p>Multiple return values do not fit the <a href="https://en.wikipedia.org/wiki/Execution_model">execution model</a>.</p></td>
    <td><p>Macroni uses <a href="docs/Pattern_Matching_for_Destructuring.md">pattern matching for destructuring</a> instead.</p></td>
  </tr>
  <tr>
    <td><p>Some programming languages do not use stable sorting procedures, breaking composition (nesting sorting criteria).</p></td>
    <td><p>Macroni uses stable sorting procedures.</p></td>
  </tr>
  <tr>
    <td><p>Some programming languages’ pseudorandom number generators make it impossible to regenerate sequences or are insecure.</p></td>
    <td>
      <p>Macroni provides a fast pseudorandom number generator whose state can be read and written so that it is possible to regenerate sequences.</p>
      <p>Macroni provides a separate cryptographically secure pseudorandom number generator using entropy pools.</p>
    </td>
  </tr>
  <tr>
    <td><p>Most optimizers cannot optimize Lisp dialects well.</p></td>
    <td>
      <p>Macroni’s restrictions on mutation and exposure from modules and types make static analyses easier for humans and computers.</p>
      <p>Macroni’s optimizer does not use a programming language independent intermediate representation so that it does not lose semantic data.</p>
    </td>
  </tr>
  <tr>
    <td><p>Optimizers are slow.</p></td>
    <td>
      <p>Macroni’s module dependencies form a directed acyclic graph.  This enables incremental static analyses and incremental compilation.</p>
      <p>Initially packages are compiled without optimization and with instrumentation.</p>
      <p>Data inferred about a module is stored with it so that analyses are not reperformed needlessly.</p>
      <p>Packages can be recompiled with profile-guided aggressive optimization in the background.  The improved code can be hot-swapped in.</p>
      <p>Packages can include profiling data so that other installations can be efficient immediately.  They cannot include other inferred data because that would be insecure (e.g. it could incorrectly eliminate dynamic bounds and type checks).</p>
    </td>
  </tr>
  <tr>
    <td><p>Most garbage collectors cause pauses.</p></td>
    <td><p>Macroni’s <a href="docs/Garbage_Collector.md">garbage collector</a> is incremental.</p></td>
  </tr>
  <tr>
    <td><p>Most garbage collectors are slow.</p></td>
    <td>
      <p>Macroni’s garbage collector is fast for several reasons:
        <ul>
          <li>Macroni avoids allocating on the heap when possible.</li>
          <li>It is quiescent when not allocating on or reading the heap, and it only mutates a variable during most heap reads.</li>
          <li>It uses a semi-space algorithm, so it only traverses reachable objects, unlike mark-and-sweep.</li>
          <li>It uses a bump allocator, the fastest kind of allocator.</li>
          <li>It self-optimizes for locality of reference.</li>
          <li>Destructing a sandbox deallocates its memory without performing garbage collection.</li>
        </ul>
      </p>
    </td>
  </tr>
  <tr>
    <td><p>Most garbage collectors do not scale.</p></td>
    <td><p>Macroni’s sandboxes’ heaps are separate.  Garbage collection between them is potentially parallel.</p></td>
  </tr>
</table>

Macroni is [influenced](docs/Influences.md) by several other projects.
