Download Link: https://assignmentchef.com/product/solved-cs342-project-4-linux-file-system-experiments
<br>
In this project you will write several simple programs and do some simple experiments. You will put everything, the programs (source codes), their various outputs, the outputs of utilities, and your descriptions and interpretations into a report (i.e. document them) that will be submitted as a <strong>pdf</strong> file. You will also upload the program sources and a Makefile. We should be able to just type make and obtain the executable files. All these files (pdf report, README, Makefile, program sources) will be put into a folder, tarred and gzipped and submitted as a single file in Moodle.




1) Write a simple <strong>program</strong> <strong>p1</strong> that will create a file and will put into the file N blocks of information where each block is of size 4094 bytes. Hence file size will be N * 4096 bytes. N is a parameter to the  program. We will run the program as p1 N. The information to write to the file can be all zeros. In your program, you will use open, read, write, close  system calls (Linux low-level I/O functions). In this program you will just use the write system call, not the read system call.




Run the program to <strong>generate a file</strong> that is large enough (10s or 100s of MB). It will act as a disk. i.e.,  it will be a <strong>virtual disk</strong>.




Then <strong>format</strong> the virtual disk with Linux <strong>ext4</strong> file system (i.e., create an ext4 file system on the virtual disk). You can do this by <strong>mkfs.ext4</strong> command in Linux.  You will use  4096 (bytes) as the block size. See the output of mkfs command. How many inodes are generated?  In Linux file system,  inodes  are put into an inode table that occupies some number of contiguous disk blocks (portions of the table can be in different groups of blocks). There is also an inode bitmap that shows which inodes in the inode table are used and which inodes are free.




Then, <strong>mount</strong> the ext4 file system in the virtual disk using the mount command to an empty subdirectory (let us call this as your <em>mount directory</em>). Then change to that mount directory. Create some files there. Then unmount the virtual disk (use umount command). Change to the mount directory again.  Are you seeing the files? Now mount again. Are you seeing the files now in the mount directory? Now unmount again.




Using the <strong>dumpe2fs</strong> command, dump information about the ext4 file system in the virtual disk. See the output. How many blocks are free?  Ext4 file system divides the blocks of the disk into groups. Each group has 32K blocks. How many groups are there? In group 0, where is the bitmap (on which block)? Is the bitmap big enough to contain information about all blocks in that group? Where is the inode bitmap (indicates if an inode in the inode table is used or not)? How many blocks are

1          occupied by the inode bitmap? Where is the inode table in group 0? How many blocks are occupied by the inode table? How many blocks are free in group 0?




<ul>

 <li>Write a <strong>program</strong> p2 that will list all files and subdirectories in a given directory. We will run the program as: p2 P. P is the pathname of the directory. Your program will use <strong>opendir</strong> and <strong>readdir</strong> functions to read the <em>directory entries</em> of the given directory. For each directory entry,  which can correspond to a file or a subdirectory, you will use the <strong>stat</strong> function to learn more about the attributes of the related file or subdirectory. For each file (or subdirectory) we need to print the following information to the screen: name of the file (or subdirectory), inode number, file type, number of blocks, size in bytes, userid.</li>

</ul>




<ul>

 <li>Write a <strong>program p3</strong> that will do <strong>random access</strong> (read operation) to a file where each access is of K bytes. We will run the program as: p3 K F. F is the name of the binary file which you will access in the program. Random access can be done by use of <strong>lseek</strong> You will use again Linux low-level I/O functions: open, <strong>read</strong>, write, close.  In your program will measure the time it takes to do an access (a read operation of specified size). You can measure it using the <strong>gettimeofday</strong> function. Your program will do a lot of  random accesses (say 100s). At the end, your program will print out the <strong>average</strong> random access time.</li>

</ul>




To do this, first create a large file. The run your program. Record the time output.




Reboot your machine and run the program again. Record the time output.




Clear the disk case (which is caching file data). You can do this by executing the following command:

sudo  echo  3     &gt;     /proc/sys/vm/drop_caches




Then run your program again. Record the time output.  Compare and interpret the results.




Include all outputs and your explanations, discussions into your report.


