# Understanding Swap Space and Paging

Swap space, a reserved area on a computer's storage device, supplements physical RAM by serving as virtual memory when RAM is full. Through a process called paging, the operating system moves less frequently accessed data from RAM to swap space. While swap prevents memory exhaustion, excessive swapping can degrade performance. It's configured during installation and vital for systems with limited RAM or memory-intensive applications.

## Steps to create a swap partation with `parted`

1. **List Available Disks and Partitions:**  
   Determine the available disks and their partitions by using either the `lsblk` or `fdisk -l` command.

2. **Launch Parted with Root Privileges:**  
   Open a terminal and launch the `parted` command with root privileges or using `sudo`. For example:
   ```bash
   sudo parted /dev/sdX
   ```
   Replace `/dev/sdX` with the actual device name.

3. **Create a Partition Table:**  
   If the disk does not have a partition table, create one. Choose between `msdos` (MBR) or `gpt` (GUID Partition Table) based on your requirements:
   ```bash
   mklabel msdos   # For MBR
   mklabel gpt     # For GPT
   ```
   print free space using:
   ```
   print space
   ```
   Make partition:
   ```
   mkpart
   ```
   Select primary/extended:
   ```
   primary
   ```
   file system
   ```
   linux-swap
   ```
   Give start and end size
   ```
   check previous partition and define start and end, if completely new use 0% at the start
   ```
   print command to see space
   ```
   print
   ```
   Run udevadm settle command
   ```
   udevadm settle
   ```
4. **Assign file system using mkswap**
   ```
   mkswap /dev/sdax
   ```
   see UID using blkid
   ```
   blkid
   ```
5. **Add entry to /etc/fstab file**
   ```
   vim /etc/fstab
   ```
   run systemctl deamon-reload
   ```
   systemctl deamon-reload
   ```
   swapon status
   ```
   swapon -s
   ```
   Enable swapon
   ```
   swapon -a
   ```


## Steps to remove a swap partation with `parted`
1. **swapoff /dev/sdax is a Linux command used to deactivate the swap space located on the device /dev/sdax:**
  ```
    swapoff /dev/sdax
  ```
2. **commentout swap mount from /etc/fstab file:**
  ```
    vim /etc/fstab
  ```
3.**Follow below steps to remove swap partation:**
  ```
    parted /dev/sdax
  ```
 print all partation
   ```
    print
   ```
Remove partation using rm
  ```
    rm Y # where Y is the number for partation
  ```


   
   
   

   
   
   
