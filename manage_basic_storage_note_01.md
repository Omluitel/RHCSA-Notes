# Partition Management Guide

## Steps to create a Partition with `parted`

1. **List Available Disks and Partitions:**  
   Determine the available disks and their partitions by using either the `lsblk` or `fdisk -l` command.

2. **Launch Parted with Root Privileges:**  
   Open a terminal and launch the `parted` command with root privileges or using `sudo`. For example:
   ```bash
   sudo parted /dev/sdX
   ```
   Replace `/dev/sdX` with the actual device name.

3. **Create a Partition Table (if Needed):**  
   If the disk does not have a partition table, create one. Choose between `msdos` (MBR) or `gpt` (GUID Partition Table) based on your requirements:
   ```bash
   mklabel msdos   # For MBR
   mklabel gpt     # For GPT
   ```
4. **print free space using:**
   ```bash
   print space
   ```
5. **Make partition:** test 
   ```bash
   mkpart
   ```
6. **Select primary/extended:**
   ```bash
   primary
   ```
   
7. **Assign the File System:**  
   ```bash
   xfs
   ```
8. **File size range** test
   ```bash
   If disk is new, use 0% at start and end with 1.2 G (upto you)
   ```
9. **If you need to create another partation**
   ```bash
   Start would be the end of the previous partition, and the end you can define yourself.
   ```
10. **Run udevadm settle command to ensure completion of device initialization and configuration tasks:**
     ```bash
       udevadm settle
      ```
11. **Assign file system using mkfs.xxx command:**
    ```bash
     mkfs.xfs /dev/sda1 # if you want to assign xfs
    ```
12. **How to check if filesystem is assigned or not:**
    ```bash
      blkid # blkid is a Linux command-line utility used to locate or print block device attribute
     ```
13. **Create a Mount Point:**  
      Use the `mkdir` command to create a mount point for the partition. For instance:
    ```bash
     sudo mkdir /mnt/mountpoint
      ```
14. **Make the Mount Permanent:**  
      Append an entry for the partition in the `/etc/fstab` file to ensure it is mounted automatically on boot.

    ```bash
     UUID=01234567-89ab-cdef-0123-456789abcdef / ext4 defaults 0 1
     ```
15. **Enable Mounting:**  
    Enable the mounting process by running the following command:
      ```bash
        sudo mount -a
       ```
15. **run systemctl daemon-reload to load fstab file:**  
    
      ```bash
        systemctl daemon-reload
       ```

Following these steps will allow you to create a partition using the `parted` command in Linux while ensuring proper file system assignment, mount point creation, and permanent mounting.
#### **Notes: **
```bash
 parted /dev/sda print free
 ```

## Steps to Remove a Linux Partition

1. **Unmount the Partition:**
   Use the `umount` command to unmount the partition. For example:
   ```bash
   sudo umount /mountpoint
   ```

2. **Remove the Entry from `/etc/fstab`:**
   Edit the `/etc/fstab` file and remove the entry corresponding to the partition you want to delete. Use a text editor such as `nano` or `vim` to edit the file:
   ```bash
   sudo nano /etc/fstab
   ```
   commentout the entry for the partition, then save and exit the editor. Once done run

   ```bash
    systemctl deamon-reload
   ```

4. **Delete the Partition:**
   Use the `parted` command to delete the partition. Launch `parted` with root privileges:
   ```bash
   sudo parted /dev/sdX
   ```
   Replace `/dev/sdX` with the device name containing the partition you want to delete.
   
   Inside `parted`, list the partitions:
   ```
   print
   ```
   
   Identify the partition you want to delete based on its size and file system type.
   
   Delete the partition using the `rm` command followed by the partition number. For example:
   ```
   rm Y
   ```
   Replace `Y` with the partition number you want to delete.

   quit using
   ```
   quit
   ```
   run udevadm settle
   ```
   udevadm settle
   ```

Following these steps will allow you to properly remove a Linux partition, including unmounting it, removing its entry from `/etc/fstab`, and deleting it using the `parted` command.

