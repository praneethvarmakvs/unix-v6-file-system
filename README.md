OPERATING SYSTEM PROJECT 2 PART B- Create a Modified Version of the UNIX V6 File System
===========================================================================================================
Team Members:
Safal Tyagi skt180001
Praneeth Varma vxk180026
Pallavi Pandey pxp170009
===========================================================================================================
Redesign Summary:
1. redesigned the inode structure where maximum allowed size is 64 bytes.
2. redesigned the superblock structure where maximum allowed size is 1024 bytes and the superblock used is 1018 bytes.
3. Size of free array is 250.
4. Size of inode array is 250.
5. Maximum file size allowed is 4GB
6. Size of the inode is 64bytes.
7. inodes in each block is 16.
===========================================================================================================
Methods Used:

1. main
 INPUT:
a. Asks the user to enter any two of the commands initfs or quit.
 OUTPUT:
a. If initfs is entered by the user,it checks if the file exists.
b. Throws an error if the file doesn't exists.
c. Throws an error if the user requests more than the maximum allowed blocks.
d. If blocks requested is less than 4GB, it initializes the file system.
e. If the command entered is quit, it exits the program.
f. If the user enters any other command, it throws an error.
g. Prints the total number of commands executed.
===========================================================================================================
2. initfs(long nBlocks, int nInodes)
 INPUT:
a. Path of the file that has to be created.
b. Number of blocks in the disk.
c. Number of i-nodes in the disk.
 WORKING:
a. Initializes the file system with zeroes to all the blocks using a char buffer.
b. Fills the buffer values with zeroes.
c. Calculates the number of blocks required by the inode.
d. If inodes is not perfectly divisible by 16 , uses another block to fit the remaining i-nodes.
e. Initializes the freelist array to zero.
f. Initializes the inode array to null.
g. Writes the superblock to the file system.
h. Sets the first free block as the data block.
i. Call the add free block function to add free blocks to the next free data block.
j. Initializes the flag by telling that the file is allocated and it is of the type directory.
k. Creates a root directory and sets offset to first i-node.
l. Points the first i-node to file directory.
=====================================================================================================================================
3. AddFreeBlock(long BlockNumber)

 INPUT:
a.Block Number 
b.File system

WORKING:
a. Reads the super block and if the free array is full,writes the content of super block to new block and adds the next free blocks to the free array.
b. If the free array is not full,adds the next free blocks to free array.
c. Finally, writes the updated superblock to the file system.
==========================================================================================================================================
4. cpin( Source file, destination file)

 INPUT:
a.The newly created file whose contents have to copied(v6 file).
b.The external file where content is filled for the v6 file.

WORKING:
a. Get the inode of the source file and check if the file already exists.
b. Open the external file and confirm its size.
c. Add the file name to the directory.
d. Copy the contents of the external file by moving to the beginning of the block and reading one block at a time from the source file.
e. Check if the file size is large or small and write one block at a time to the beginning of the block.
=======================================================================================================================================
5. cpout(Source File, Destination file)

 INPUT:
a.The newly created file whose contents have to copied(v6 file).
b.The external file where content is filled for the v6 file.

WORKING:
a.Get the inode of the source file and check if the file already exists.
b.If the file size is large, read block number of second indirect block, Read third indirect block number from second indirect block.
c.Finally read target block number from third indirect block.
d.If the file size is small, directly read from the direct blocks.
=====================================================================================================================================
6.  mkdir(Directory)

 INPUT: 
a.Name of the v6 directory.

WORKING:
a.Check if the directory already exists.
b.If the directory does not exists. Create a new directory and move to the end of the directory file.
c.Update the directory file inode to increment size by one record.
d.Initialize the new file direcory inode by setting the first two entires as . and ..
=======================================================================================================================================
7. rm(filename)

 INPUT:
a. The v6 file that has to be removed.

WORKING:
a.Check if the v6 file already exists.
b.If the file exists,get the inode of the file and the size of the file.
c.Free the blocks by adding the data blocks to the free list.
d.Initialize the inode flag and make it unallocated.
e.Update the inode by setting it free and remove the file from the directory.

