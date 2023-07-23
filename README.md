# ubuntu-self-clone
Procedure to clone a ubuntu istallation

## Commands
* save partition table with fdisk O command
* edit the file adjusting the size of root partition to the size of the destination disk
* replicate partition table with fdisk I command recalling the file where saved previously
* format efi partition with mkfs.fat -F 32 /dev/sd
* format root partition: mkfs.ext4 /dev/sdX
* mount the root destination partiition on /mnt: sudo mount /dev/sdX /mnt
* sudo rsync -ahPHAXx --delete --exclude={/dev/*,/proc/*,/sys/*,/tmp/*,/run/*,/mnt/*,/media/*,/lost+found} / /mnt
* for i in /dev /dev/pts /proc /sys /run; do sudo mount -B $i /mnt$i; done
* sudo chroot /mnt
* format swap partition with: mkswap /dev/sdX
* sudo grub-install --recheck /dev/sdX
* sudo update-grub
* with blkid che the UUID of varius partitions, edit and adjust /etc/fstab in the destination drive
