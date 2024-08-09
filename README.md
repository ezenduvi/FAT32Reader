# FAT32 File System Reader

This project is a C program designed to read and interact with a FAT32-formatted drive. It provides various functionalities, including fetching drive information, listing directories and files, and extracting files from the drive.

## Overview

The program interacts with a FAT32 disk image (or optionally a USB flash drive) to perform the following operations:

1. **Print Drive Information:** Display details such as drive name, free space, usable space, and cluster size.
2. **List Files and Directories:** Recursively list all files and directories, mimicking the output format of the `tree` command.
3. **Fetch Files:** Extract a specified file from the FAT32 drive and save it locally.

## Features

- **Low-Level Disk Access:** Uses low-level, unbuffered system calls (`open`, `read`, `lseek`, `write`, `close`) for direct interaction with the disk image.
- **FAT32 Structure Parsing:** Parses FAT32 structures such as boot sectors, FSInfo, and directory entries.
- **File and Directory Handling:** Handles long filenames, directory spanning across multiple clusters, and recognizes end-of-directory markers.

## Prerequisites

- C Compiler (e.g., GCC)
- Make utility
- A FAT32 disk image

## Compilation

To compile the program, ensure you are in the directory containing the `Makefile`, and run:
make

## Display Drive Information
./fat32 <disk_image> info

Output:
Drive name
Free space on the drive in KB
Usable storage on the drive in KB
Cluster size in sectors and KB

## List Files and Directories
./fat32 <disk_image> list

Output:
Tree-like structure of directories and files on the drive.
Example:
file.txt
Directory: FOLDER
-Directory: FOLDER2
--Directory: FOLDER3
---File: THEFILE.TXT
file2.txt

## Fetch a File
./fat32 <disk_image> get <path/to/file.txt>

Output:
The specified file is written to the current working directory.

## Clean Up
To remove the compiled executable and other temporary files, run:
make clean

## Technical Details
Sector and Cluster-Based Operations: The program operates at the sector and cluster level for efficiency.
FAT32 Structure: The disk layout includes the Reserved Area (boot sector and BPB), FAT Area (File Allocation Table), and Data Area (file and directory storage).
Compiler Flags
The program is compiled with the following flags to ensure code quality:
-Wall -Wpedantic -Wextra -Werror
These flags enable all warnings and treat them as errors to prevent potential issues.

## Important Notes
Memory Handling: Special care is taken to avoid integer overflows and alignment issues using uint32_t and off_t data types.
