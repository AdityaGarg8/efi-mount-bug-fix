# Guide to fix bug causing Linux to mount the Windows EFI partition instead of its own seperate EFI partion during installation on T2 Macs.

This bug has been observed in Ubuntu till now.

## Consequences of this bug

This bug causes Linux to overwrite the Windows Bootloader in the Windows EFI partition on updating your Linux distro and thus breaking the Windows Bootloader.

## Fixing the bug

In order to fix the bug, you need to modify the `/etc/fstab` file. A sample of the file is shown here :-
