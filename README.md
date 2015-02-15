# liveroot
Initcpio hooks for overlayfs ontop of root

Add one of them to the kernel command line and /etc/mkinitcpio.conf hooks.
Add oroot=raw for a tmpfs overlay on root with a swap of half of system ram.
Add oroot=compressed for a compressed overlay on root with a swap of half of system ram.