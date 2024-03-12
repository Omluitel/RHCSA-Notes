# Creating a Partition with `parted`

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

4. **Assign the File System:**  
   Format the partition with the desired file system. For example, to format with XFS:
   ```bash
   mkfs.xfs /dev/sdX1
   ```

5. **Create a Mount Point:**  
   Use the `mkdir` command to create a mount point for the partition. For instance:
   ```bash
   sudo mkdir /mnt/mountpoint
   ```

6. **Make the Mount Permanent:**  
   Append an entry for the partition in the `/etc/fstab` file to ensure it is mounted automatically on boot.

7. **Enable Mounting:**  
   Enable the mounting process by running the following command:
   ```bash
   sudo mount -a
   ```

Following these steps will allow you to create a partition using the `parted` command in Linux while ensuring proper file system assignment, mount point creation, and permanent mounting.
