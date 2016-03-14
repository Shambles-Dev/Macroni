Packages
========

## Overview




## Details

### Solving the Monolithic Problem

Commercial software is often designed to maximize integration, to minimize customer choice, to minimize competition.

Macroni is made of encapsulated, swappable, (un)installable packages to maximize maintainability, user satisfaction, and efficiency.


### Solving the (Un)Installation and Update Problem

The owner-user can install or update software from package files.

Dependencies are auto-installed.

Packages are architecture independent.  They contain source code instead of executable code.

There are normally no prompts (e.g. licence, configuration, or feedback prompts) when (un)installing or updating.  If the package is not cryptographically signed by a key the owner-user trusts, there is an [installation endowment](Capability_Security_Model.md#using-capabilities) authorization prompt when installing or updating.


### Solving the Upgrade Problem

By default, to improve security, Macroni auto-updates daily all packages that are cryptographically signed by a key the owner-user trusts.  The previous and new versions must be signed by the same key.

Data loss is prevented via transparent persistence (for kernel or runtime system updates) or microrebooting (for other updates).  Macroni requires authorization by the owner-user before each reboot for kernel or runtime system updates because it is observable and it breaks network connections.

Package (un)installation and updating can only affect that package’s files.  It can indirectly cause other packages to be installed, but only if they are depended upon and the owner-user trusts the key they are cryptographically signed with.  It can indirectly cause other packages to be uninstalled, but only if they are no longer depended upon and the owner-user did not manually install them (e.g. because they intend to write code that depends upon them).

Auto-updates can be delayed by a number of days configured by the owner-user.  This gives updates time to be vetted.

Auto-updates can be disabled by the owner-user.  The owner-user can manually update packages.

By default, Macroni retains 1 previous version of each package and their hard state.

Auto-update delays or disabling and how many previous versions to retain can be configured by the owner-user on a per-package basis or globally.  Per-package configurations override the global configuration.

If an update damaged Macroni but it is still usable, the owner-user can revert the offending packages to previous versions, which will disable auto-updates of those packages.

If an update rendered Macroni unusable but the file system is intact, the owner-user can revert all packages to a snapshot via a prompt when booting after an unclean shutdown or via boot media, which will disable auto-updates globally.  This only affects system, not user, files.  Snapshots work by retaining previous versions of packages and their hard state.  Macroni takes a snapshot before packages update.  By default, it retains 1 snapshot.  How many snapshots to retain can be configured by the owner-user.


## See Also
* [Availability](Availability.md)
* [Capability Security Model](Capability_Security_Model.md)
* [Events](Events.md)
* [File System](File_System.md)
* [Microrebooting](Microrebooting.md)
* [Modules](Modules.md)
* [Source Code Editor](Source_Code_Editor.md)
* [System Structure](System_Structure.md)
* [Versioning](Versioning.md)
