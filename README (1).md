# Linux Root Directories --- Quick Notes

The `/` directory is the **root of the Linux filesystem**.

  -----------------------------------------------------------------------
  Directory                           Purpose
  ----------------------------------- -----------------------------------
  `/bin`                              Essential user commands, such as
                                      `ls` and `cp`.

  `/sbin`                             Essential system-administration
                                      commands.

  `/lib`                              Essential shared libraries and
                                      kernel modules.

  `/lib64`                            64-bit system libraries on systems
                                      that use this directory.

  `/boot`                             Files needed to start Linux,
                                      including kernel and bootloader
                                      files.

  `/dev`                              Device files representing hardware
                                      and virtual devices.

  `/etc`                              System-wide configuration files.

  `/home`                             Personal directories for regular
                                      users.

  `/root`                             Home directory of the `root`
                                      administrator account.

  `/media`                            Common mount points for removable
                                      media, such as USB drives.

  `/mnt`                              Temporary mount point for manually
                                      mounted filesystems.

  `/opt`                              Optional or third-party application
                                      software.

  `/proc`                             Virtual filesystem containing
                                      process and kernel information.

  `/run`                              Temporary runtime data created
                                      since boot.

  `/srv`                              Data served by system services,
                                      such as web or file servers.

  `/sys`                              Virtual filesystem exposing device
                                      and kernel information.

  `/tmp`                              Temporary files; contents may be
                                      deleted automatically.

  `/usr`                              Most applications, utilities,
                                      libraries, and documentation.

  `/var`                              Variable data, such as logs,
                                      caches, mail, and databases.

  `/lost+found`                       Recovered file fragments on some
                                      Linux filesystems after filesystem
                                      checks.
  -----------------------------------------------------------------------

## Quick Tips

-   `/` is the top-level directory; every file and directory is under
    it.
-   `/proc` and `/sys` are virtual filesystems, not ordinary folders of
    regular files.
-   On modern Linux systems, `/bin`, `/sbin`, `/lib`, and `/lib64` may
    be symbolic links into `/usr`.
-   The exact directory layout can vary by Linux distribution.
