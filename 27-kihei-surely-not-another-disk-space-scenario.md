# Scenario
Description: There is a /home/admin/kihei program. Make the changes necessary so it runs succesfully, without deleting the /home/admin/datafile file.

Test: Running /home/admin/kihei returns Done..

# Solution
```
# Find the error.
./kihei -v

# Identify if there are extra disks attached to the system.
lsblk -l

# We found two additional disks that can be used to create a logical volume.
pvcreate /dev/nvme1n1 /dev/nvme2n1
vgcreate vg /dev/nvme1n1 /dev/nvme2n1
lvcreate -n lv -l 100%FREE vg
mkfs.ext4 /dev/vg/lv

# Mount the newly created logical volume to the data folder. and provide proper permissions.
mount /dev/vg/lv /home/admin/data
chown -R admin: /home/admin/data

# rerun the program
./kihei
```