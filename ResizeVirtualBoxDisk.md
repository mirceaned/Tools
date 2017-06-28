# run modiyhd command, if you have a vmdk you will need also the conversion to and from vmdk
VBoxManage clonehd "source.vmdk" "cloned.vdi" --format vdi
VBoxManage modifyhd "cloned.vdi" --resize 51200
VBoxManage clonehd "cloned.vdi" "resized.vmdk" --format vmdk

# use gparted to resize the partition
https://tvi.al/resize-sda1-disk-of-your-vagrant-virtualbox-vm/

# find name of physical volume
fidsk -l

# use physical volume name (e.g. /dev/sda2) to resize it
pvresize /dev/sda2

# check the name of logical volume
df -h

# extend logical volume (e.g. /dev/mapper/centos-root)
lvextend -r -l +100%FREE /dev/mapper/centos-root
