# Guide to fix bug causing Linux to mount the Windows EFI partition instead of its own seperate EFI partion during installation on T2 Macs.

This bug has been observed in Ubuntu till now.

## Consequences of this bug

This bug causes Linux to overwrite the Windows Bootloader in the Windows EFI partition on updating your Linux distro and thus breaking the Windows Bootloader.

## Fixing the bug

In order to fix the bug, you need to modify the `/etc/fstab` file. It can be done using a text editor. Alternatively you may also edit using the terminal by running `sudo nano /etc/fstab`. A sample of the file before editing is shown here :-
![Before](https://github.com/AdityaGarg8/efi-mount-bug-fix/raw/main/Before.png)

Now to solve this problem, we need to prevent Linux to scan the line instructing it to mount the Windows EFI partition. In the above figure, the file shows two EFI partitions, one being `/dev/nvme0n1p1` and other being `/dev/sda1`. The `/dev/nvme0n1p1` partition is the Windows EFI Partition. In most of the cases, this partition is used for Windows. The `/dev/sda1` partition is the partition I had assigned the Linux installer to use as the seperate EFI partition for Linux thus the path of seperate EFI partition may vary from user to user.

So, to prevent Linux to scan the line instructing it to mount the Windows EFI partition, we need to comment that line (put a `#` in front of the line). After commenting, it looks something like this :-
![After](https://github.com/AdityaGarg8/efi-mount-bug-fix/raw/main/After.png)

Now save the file and restart your Mac. The bug should be fixed. In order to confirm, check that `/dev/nvme0n1p1` is not mounted as `/boot/efi` by running `lsblk` or using a disk utility program.
