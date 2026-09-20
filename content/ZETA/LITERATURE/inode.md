---
up:
tags:
  - atomic
  - todo
created: 2026-05-12 11:29
---
- Data structure that describes a file-system object (file, directory, etc.)
- includes metadata
- directory is a list of inodes, including an entry for itself, its parent and all of its children
- data may be called stat data (reference to `stat` syscall that provides the data to programs)
- `ls -i` prints the inode number in the first column

POSIX:
- device ID
- file serial numbers
- file mode
- link count (how many hard links point to the inode)
- user id
- group id
- device id if it is a device file
- size of file
- timestamps
- preferred I/O block size
- number of blocks allocated to this file
