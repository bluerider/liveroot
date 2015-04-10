# liveroot
Initcpio hooks for overlayfs ontop of root

Tired of the slow I/O when running Linux on a USB OS?
Liveroot greatly speeds up USB based Linux by writing to ram instead of to the USB. Flushing the ram to the USB stick can be controlled by the user by calling /usr/bin/overlay_flush.

Liveroot has 3 modes of operation that can be triggered by adding to the kernel cmdline:
  1) oroot=raw        : use a tmpfs overlay
  2) oroot=compressed : use a lzo compressed zram overlay
  3) oroot=live       : load root into a lzo compressed ram overlay (need as much ram as root drive size)

You will want to move these files to the appropriate directory:

In Repo                 |   On Root
------------------------|------------------------------------
initcpio/hooks/oroot    |    /usr/lib/initcpio/hooks/oroot
initcpio/install/oroot  |    /usr/lib/initcpio/install/oroot

Add oroot to the hooks array of /etc/mkinitcpio.conf (after udev and possibly encrypt) and run # mkinitcpio -p linux to run oroot at boot.

*In addition, liveroot now has a compiler that can create a more customized liveroot script. If you pass "btrfs" to the compiler it'll produce a version of liveroot that uses btrfs snapshotting abilities for overlay_flush. Note, to use the btrfs mode, you will need to have a a btrfs root and a subvolume at /snapshots for snapshots.
To use the compiler :
   chmod u+x compiler
   ./compiler
 or
   ./compiler btrfs
This will generate two files : oroot
                             : oroot_install
You will want to move these files to the appropriate directory :

In Repo                 |   On Root
------------------------|------------------------------------
oroot                   |    /usr/lib/initcpio/hooks/oroot
oroot_install           |    /usr/lib/initcpio/install/oroot