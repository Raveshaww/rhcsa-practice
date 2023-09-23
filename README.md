# RHCSA Practice Exams
Rough little exams I made for myself prior to the actual RHCSA exam centered around RHEL 8. For obvious reasons, the answers will not be supplied.
## Requirements
- You have a working RHEL 8 system, ideally a virtual machine.
- The user being used for most of this exam is called `rhcsa`
- You have a secondary server acting as an SMB and NFS host. In the following exams, this is refered to as `Alma`, due to the fact that it was running on Alma Linux.
## Exam 1
- Assume that you have lost access to the root account and need to reset the root password
- Loop mount the install ISO that you used to set up RHEL8 and configure the loop-mounted ISO as a repository
    - Configure the system to use this repo as the only repo
- In the remaining space of the disk, add a 1GiB partition and do it in such a way that it is possible to add more partitions later
- Format this partition with the ext4 file system and set the label `dbfiles` on the partition. Configure the system to mount this partition persistently on the directory `/dbfiles` using the partition label
- Create a 2GIB LVM Volume Group with the name `vgdata` with physical extents of 16MiB
- In this volume group, create a 1GIB logical volume with the name `lvdata`
- Format this LV with the XFS filesystem and mount it persistently in the directory `/lvdata`
- Restart the computer, and after a restart add another 500MiB to the xfs file system that was created on top of this LV
- Set passwords to expire after 90 days, also ensure that passwords must have a length of at least 6 characters
- Ensure that while creating new users, an empty file with the name `newfile` is created in their home directories 
- Create users `red` and `blue`. Make them a member of the group students as a secondary group membership
- Create users `elm` and `birch`. Make them a member of the group profs as a secondary group membership
- Create shared group directories `/data/students` and `/data/profs` and ensure that members of the group students have full access to `/data/students` and that members of profs have full access to `/data/profs`. The others entity should have no access at all
- Ensure that all new files in these directories are automatically group-owned by the group owner of the directory
- Ensure that the only owner of a file is allowed to remove files
- User `elm` is the head-master and should be allowed to remove all files
- All users from the group `profs` should have read permissions on all files in `/data/students`
- Schedule a cron job to automatically write the text `hello world` to syslog at every 10th minute after the hour. Ensure that this message is written with the `notice` priority 
- Find all files that are owned by the user `rhcsa` in the `/home/rhcsa` directory and copy them to the directory `/rhcsafiles`
- New directories made by `elm` should be `drwx—---`, and files should be `-rwx—--`-
- Disable the interactive shell for user `blue`
## Exam 2
- On the 10GIB virtual disk, add a VDO volume with a size of 20GB and mount it persistently
- Set your server to use the `recommended` tuned profile
- Verify that NTP time synchronization is active, and enable it if it is not. 
- Change NTP time server to `time.cloudflare.com`
- Modify the bootloader program and set the default autoboot timer value to 2 seconds
- Add http port `8400/udp` to the public zone persistently
- Add http port `8300/tcp `to the SELinux policy database persistently
- Create a directory `/direct01` and apply the SELinux context for `/root` to it
- Configure journald to store messages permanently
- Install postgresql version 9.6 (or a different non-default version)
- Create a stratis pool called `pool1` and volume `str1` on a 1GB disk and mount it to `/mnt/str1`
- Mount `alma:/data` on `/data`
- Create a nginx container that starts as a systemd unit upon the start of the computer as a rootless user account
- Update the kernel
- Using the container created earlier, create a bind mount to `/bindMount`
- Mount a samba share from Alma to `/smb`
## Exam 3
- Add 500mb of swap from a new partition
- Make an archive of `/home/rhcsa` and zip it with gzip
- Copy that archive to Alma at `/home/rhcsa`
- Schedule the VM to shutdown at the top of the hour 
- Enable ipv4 forwarding
