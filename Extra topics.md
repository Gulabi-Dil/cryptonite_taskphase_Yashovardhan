# **INDEX**
- [File Linking in Unix-Like Systems](https://github.com/Gulabi-Dil/cryptonite_taskphase_Yashovardhan/blob/main/Extra%20topics.md#file-linking-in-unix-like-systems)
   - [Hard Links](https://github.com/Gulabi-Dil/cryptonite_taskphase_Yashovardhan/blob/main/Extra%20topics.md#1-hard-links)
   - [Soft Links](https://github.com/Gulabi-Dil/cryptonite_taskphase_Yashovardhan/blob/main/Extra%20topics.md#2-symbolic-links-soft-links)
   - [Differences between hard and soft links](https://github.com/Gulabi-Dil/cryptonite_taskphase_Yashovardhan/blob/main/Extra%20topics.md#differences-between-hard-links-and-symbolic-links)
- [Metadata](https://github.com/Gulabi-Dil/cryptonite_taskphase_Yashovardhan/blob/main/Extra%20topics.md#metadata)
- [Piping and Process Substitutions](https://github.com/Gulabi-Dil/cryptonite_taskphase_Yashovardhan/blob/main/Extra%20topics.md#piping-and-process-substitutions)
   - [Unnamed Pipes](https://github.com/Gulabi-Dil/cryptonite_taskphase_Yashovardhan/blob/main/Extra%20topics.md#unnamed-pipes)
   - [Named Pipes](https://github.com/Gulabi-Dil/cryptonite_taskphase_Yashovardhan/blob/main/Extra%20topics.md#named-pipes)
   - [FIFOs and Blocking Behavior in Pipes](https://github.com/Gulabi-Dil/cryptonite_taskphase_Yashovardhan/blob/main/Extra%20topics.md#fifos-and-blocking-behavior-in-pipes)
   - [Process Substitution](https://github.com/Gulabi-Dil/cryptonite_taskphase_Yashovardhan/blob/main/Extra%20topics.md#process-substitution)
   - [Differences among them](https://github.com/Gulabi-Dil/cryptonite_taskphase_Yashovardhan/blob/main/Extra%20topics.md#differences-amongn-unnamed-pipes-named-pipes-and-process-substitutions)
- [Processes and Jobs](https://github.com/Gulabi-Dil/cryptonite_taskphase_Yashovardhan/blob/main/Extra%20topics.md#processes-and-jobs)
   - [Session Heads, Process Groups, and Group Heads in Linux](https://github.com/Gulabi-Dil/cryptonite_taskphase_Yashovardhan/blob/main/Extra%20topics.md#session-heads-process-groups-and-group-heads-in-linux)
   - [Summary of TTY, Shells and Terminal Emulators](https://github.com/Gulabi-Dil/cryptonite_taskphase_Yashovardhan/blob/main/Extra%20topics.md#summary-of-tty-shells-and-terminal-emulator)
- [File Types](https://github.com/Gulabi-Dil/cryptonite_taskphase_Yashovardhan/blob/main/Extra%20topics.md#file-types)
  - [Types of files in Linux](https://github.com/Gulabi-Dil/cryptonite_taskphase_Yashovardhan/blob/main/Extra%20topics.md#types-of-files-in-linux)
- [Understanding File Permissions](https://github.com/Gulabi-Dil/cryptonite_taskphase_Yashovardhan/blob/main/Extra%20topics.md#understanding-file-permissions)
   - [setuid and setgid](https://github.com/Gulabi-Dil/cryptonite_taskphase_Yashovardhan/blob/main/Extra%20topics.md#setuid)
   - [sticky bit](https://github.com/Gulabi-Dil/cryptonite_taskphase_Yashovardhan/blob/main/Extra%20topics.md#sticky-bit)
- [Types of Variables in Linux](https://github.com/Gulabi-Dil/cryptonite_taskphase_Yashovardhan/blob/main/Extra%20topics.md#types-of-variables-in-linux)
- [Padding in base64 encoding](https://github.com/Gulabi-Dil/cryptonite_taskphase_Yashovardhan/blob/main/Extra%20topics.md#explanation-of-padding-in-base64-encoding)
- [Understanding GDB and ELF Files](https://github.com/Gulabi-Dil/cryptonite_taskphase_Yashovardhan/blob/main/Extra%20topics.md#understanding-gdb-and-elf-files)
  
**Some External Links**
- [Exit Status Variable in Linux](https://www.geeksforgeeks.org/exit-status-variable-in-linux/)
- [Grep Command](https://www.hostinger.in/tutorials/grep-command-in-linux-useful-examples/?utm_campaign=Generic-Tutorials-DSA|NT:Se|LO:IN-t5&utm_medium=ppc&gad_source=1&gclid=CjwKCAjwgfm3BhBeEiwAFfxrG8x2xPsN_OXGiqnhGabISx__S58VeXv6dzU5d6bKa4tyIorNARuIMRoCJ3oQAvD_BwE)
- [Difference between ; && and || and info about some other operators](https://github.com/Gulabi-Dil/cryptonite_taskphase_Yashovardhan/blob/main/Operators%20differences%20(extra).md#differences-between---and--in-linux)
- [Signals and Signal Handling](https://www.geeksforgeeks.org/signal-handling-in-linux-through-the-signal-function/)

# File Linking in Unix-like Systems

File linking in Unix-like operating systems allows you to create multiple references or "links" to the same file. These references can either be **hard links** or **symbolic (soft) links**, and they serve different purposes. 

## Types of File Links
1. **Hard Links**
2. **Symbolic Links (Soft Links)**

---

## 1. Hard Links

A **hard link** is essentially an additional name for an existing file. When you create a hard link, you are creating a reference to the same **inode** (the data structure storing the metadata and disk location of file data). Hard links point to the same physical data on the disk as the original file, meaning the file can be accessed via either its original name or any hard links created for it.

### Key Characteristics of Hard Links:
- **Same inode**: Hard links share the same inode number as the original file.
- **Data sharing**: All hard links refer to the same file data. If one link modifies the file, the changes are visible to all other hard links.
- **File removal**: The file is only truly deleted from the filesystem when all hard links (including the original filename) are removed. Until then, the data remains accessible.
- **Cannot span file systems**: Hard links must be on the same file system because they refer to the same inode.
- **No directories**: Hard links cannot be created for directories, only files (with some rare exceptions for superusers).

### Creating a Hard Link:
```bash
ln original_file hard_link
```

### Example:
```bash
$ echo "Hello World" > original.txt
$ ln original.txt hardlink.txt
$ cat hardlink.txt
Hello World
```
In this example, `hardlink.txt` is a hard link to `original.txt`. Both refer to the same data on disk, so changes to one file reflect in the other.

---

## 2. Symbolic Links (Soft Links)

A **symbolic link**, or **soft link**, does not point directly to the data on the disk; instead, it acts as a shortcut or pointer to another file or directory. A symbolic link contains the path to the target file or directory, not the file's inode.

### Key Characteristics of Symbolic Links:
- **Different inode**: A symbolic link has its own inode and points to the pathname of the target file.
- **Can span file systems**: Unlike hard links, symbolic links can reference files on different file systems or partitions.
- **Can link to directories**: Symbolic links can be created to point to both files and directories.
- **Broken links**: If the target file or directory is moved or deleted, the symbolic link becomes "broken" and no longer works, as it still points to the now-nonexistent pathname.

### Creating a Symbolic Link:
```bash
ln -s target_file symbolic_link
```

### Example:
```bash
$ echo "Hello World" > original.txt
$ ln -s original.txt symlink.txt
$ cat symlink.txt
Hello World
```
In this example, `symlink.txt` is a symbolic link to `original.txt`. If `original.txt` is moved or deleted, `symlink.txt` will point to a non-existent file and display an error when accessed.

---

## Differences Between Hard Links and Symbolic Links

| Feature                        | Hard Links                                                 | Symbolic Links (Soft Links)                                       |
|---------------------------------|------------------------------------------------------------|------------------------------------------------------------------|
| **Reference**                   | Direct reference to the same inode (same data on disk)     | Points to the pathname of the target file or directory            |
| **File system**                 | Must be on the same file system                            | Can point to files or directories on different file systems       |
| **Directories**                 | Cannot link to directories (except for superusers)         | Can link to both files and directories                            |
| **Inode sharing**               | Shares the inode with the original file                    | Has a different inode, as it just points to the target file       |
| **File removal behavior**       | File is only deleted when all hard links are removed       | If the target file is removed, the symbolic link becomes broken   |
| **File system impact**          | Directly references the file data, no extra disk space     | Only requires disk space for storing the link itself (the pathname) |
| **Example command**             | `ln original_file hard_link`                               | `ln -s target_file symbolic_link`                                 |

---

## How Linking Files Work

Here’s a deeper look into how linking files work under the hood:

### Inodes and Hard Links:
When a file is created, the operating system assigns it an **inode**. This inode contains metadata about the file. Key Components of an Inode:
- File Type: Indicates whether the inode represents a regular file, directory, symbolic link, or other types of files.

- Permissions: Contains information about the file’s permissions (read, write, execute) for the owner, group, and others.

- Owner Information: Stores the user ID (UID) and group ID (GID) of the file's owner.

- File Size: Represents the size of the file in bytes.

- Timestamps:
  - Creation Time (ctime): The time the inode was created.

  - Modification Time (mtime): The time the file's content was last modified.

  - Access Time (atime): The time the file was last accessed.

- Link Count: Indicates how many hard links point to the inode. When this count reaches zero (i.e., all hard links are deleted), the inode and its associated data are freed.

- Pointers to Data Blocks: Contains addresses (pointers) to the actual data blocks on the disk where the file's content is stored.
### How Inodes Work:
When you create a file, the filesystem allocates an inode for that file and fills it with the appropriate metadata.
Each file has a unique inode number within its filesystem, which the operating system uses to access and manage the file.
Directories also use inodes. Each entry in a directory points to the inode of a file or subdirectory.
### Important Points:
- Inode Limit: Filesystems have a fixed number of inodes. If all inodes are used up, no new files can be created, even if there is free space on the disk.
- File Names vs. Inodes: The name you use to access a file is not stored in the inode; it is stored in the directory that points to the inode. This separation allows multiple filenames (hard links) to refer to the same inode.
- Viewing Inode Information: You can view inode information using commands like ls -i in Linux, which shows the inode number alongside file names.

A **hard link** is simply an additional directory entry that points to this same inode. The operating system uses the inode to locate and manage the file's data. Since all hard links to a file share the same inode, they also share the same file content.

### Symbolic Links and Pathnames:
A **symbolic link**, on the other hand, is a small file that stores a pathname to another file or directory. The system interprets the symbolic link and redirects access to the target file via the pathname. If the pathname changes (e.g., the target file is deleted or moved), the symbolic link breaks.

### File System Impact:
- **Hard Links**: Do not create additional copies of the file; they merely add another pointer to the existing file data. As a result, hard links are more efficient in terms of disk space but are limited to the same file system.
- **Symbolic Links**: Only store the pathname of the target, so they take up less space but do not directly point to the file's data. They can span file systems, making them more versatile.

---

## Summary of Differences:
- **Hard Links**: Directly reference file data via the inode. All hard links are treated as the same file, so deleting the original file does not affect other hard links.
- **Symbolic Links**: Point to a file or directory via its pathname. They are more flexible since they can reference files across different file systems and directories, but they can break if the target is deleted or moved.

By using links effectively, you can manage files, save disk space, and create flexible references across the filesystem without duplicating data.


===========================================================================


# Metadata

**Metadata** is data that provides information about other data. It helps to describe the characteristics, context, and attributes of a particular piece of information, making it easier to understand, manage, and retrieve that data. Here’s a deeper look into what metadata is, its types, and its significance:

## Types of Metadata

1. **Descriptive Metadata**: 
   - Provides information about the content of the data. 
   - **Examples**: title, author, date of creation, and keywords.
   - **Use**: Helps users find and identify specific data.

2. **Structural Metadata**: 
   - Describes how different components of a data set are organized.
   - **Examples**: the organization of chapters in a book, the relationship between tables in a database, or the order of tracks in a music album.
   - **Use**: Helps in understanding how to access or navigate the data.

3. **Administrative Metadata**: 
   - Contains information about the management of the data.
   - **Examples**: file type, creation date, access rights, and preservation information.
   - **Use**: Helps with data governance, resource management, and digital preservation.

4. **Statistical Metadata**: 
   - Provides information about data collection and analysis.
   - **Examples**: sampling methods, data collection processes, and definitions of variables.
   - **Use**: Aids researchers in understanding how data was gathered and its validity.

5. **Technical Metadata**: 
   - Describes the technical characteristics of the data.
   - **Examples**: file format, resolution, and encoding.
   - **Use**: Helps software applications understand how to process or display the data correctly.

## Importance of Metadata

- **Data Organization**: Metadata enables efficient organization of data, making it easier to locate and manage files, especially in large datasets or databases.
- **Searchability**: Well-defined metadata enhances searchability, allowing users to quickly find relevant information through keywords and filters.
- **Contextual Understanding**: Metadata provides context to data, helping users understand its origin, purpose, and how it should be used.
- **Interoperability**: In systems where data needs to be shared or combined, metadata ensures that different systems can understand and use the data appropriately.
- **Data Management**: Effective metadata management supports data governance, compliance, and regulatory requirements, ensuring data quality and integrity.

## Examples of Metadata in Various Contexts

1. **Digital Images**:
   - **Descriptive Metadata**: Image title, photographer's name, and date taken.
   - **Technical Metadata**: Image resolution, file format (JPEG, PNG), and camera settings (aperture, exposure).

2. **Web Pages**:
   - **Descriptive Metadata**: Page title, description, and keywords in HTML meta tags.
   - **Structural Metadata**: Hierarchy of content (headings, subheadings).

3. **Databases**:
   - **Descriptive Metadata**: Table names, column names, and data types.
   - **Administrative Metadata**: Creation date, last modified date, and access permissions.

4. **Documents**:
   - **Descriptive Metadata**: Document title, author, and summary.
   - **Administrative Metadata**: File format (PDF, DOCX), size, and creation date.

## Conclusion

Metadata plays a crucial role in data management and utilization. By providing context and structure to data, it enhances accessibility, searchability, and understanding, ultimately making data more valuable and usable for various applications.


===========================================================================

# Piping and Process Substitutions
## Unnamed Pipes:
Unnamed pipes are one of the simplest forms of inter-process communication (IPC) in Unix-like operating systems. They are typically used to connect two related processes (such as a parent process and its child process), allowing the output of one process to be sent directly to another.

### Key Characteristics of Unnamed Pipes
- **Temporary and Anonymous**: Unnamed pipes exist only as long as the process that created them is running. They do not have a name in the filesystem and cannot be accessed by unrelated processes.

- **One-way Communication**: Unnamed pipes are unidirectional, meaning data flows in one direction—from one process to another.
- **Parent-Child Communication**: Often used to pass data between a parent process and a child process created via fork() in C programming, or between commands connected in a pipeline in the shell.
- **File Descriptors**: Unnamed pipes use file descriptors to handle reading and writing. The process writing to the pipe uses one file descriptor (fd) for writing, and the process reading uses another for reading.

### Syntax in the Shell (Pipelines):
```command1 | command2```

The | symbol represents an unnamed pipe, sending the output of command1 directly into the input of command2.

Example:

```ls | grep "file"```

Here, the output of ls is passed directly to grep, and no intermediate file is created.
## Named Pipes:
Named pipes, also known as FIFOs (First In, First Out), are a special type of file in Unix-like operating systems that facilitate inter-process communication (IPC). Unlike unnamed pipes, which are temporary and exist only in memory while the communicating processes are running, named pipes have a presence in the filesystem and can be accessed by multiple processes, even if they are not related (i.e., they do not share a common ancestor).

### Key Characteristics of Named Pipes
- **Persistent in Filesystem**: Named pipes are created as special files in the filesystem, which allows them to persist beyond the life of the processes that created them. They are identified by a name in the filesystem, making them accessible for reading and writing by any process that knows the name.
- **Unidirectional Communication**: Named pipes are typically unidirectional, meaning data flows in one direction—from the writing process to the reading process. However, you can create two named pipes to allow for bidirectional communication.
- **Blocking Behavior**: When a process attempts to read from a named pipe, it will block (i.e., wait) until there is data available to read. Conversely, if a process tries to write to a named pipe that has no readers, it may also block until a reader is available.
- **FIFO Structure**: The name "FIFO" indicates that data is read in the order it was written. The first piece of data written to the pipe is the first to be read, following a first-in, first-out structure.

### How to Create and Use Named Pipes
1. Creating a Named Pipe
You can create a named pipe using the mkfifo command in the terminal or using the mkfifo() system call in a C program.

Using the Command Line:
```mkfifo mypipe```

This command creates a named pipe called mypipe in the current directory.

Using C programming:
```
#include <sys/types.h>
#include <sys/stat.h>
#include <fcntl.h>
#include <unistd.h>

int main() {
    mkfifo("/tmp/mypipe", 0666);  // Create a named pipe with read/write permissions
    return 0;
}
```
2. Writing to a Named Pipe

A process can write data to a named pipe using standard file I/O functions like open(), write(), and close().

Example in shell:
```echo "Hello" > mypipe  # Write "Hello" to the named pipe```

Example in C:
```
#include <fcntl.h>
#include <unistd.h>

int main() {
    int fd = open("/tmp/mypipe", O_WRONLY);  // Open the named pipe for writing
    write(fd, "Hello", 5);                    // Write data to the pipe
    close(fd);                                // Close the pipe
    return 0;
}
```
3. Reading from a Named Pipe

To read from a named pipe, a process opens the pipe for reading. The read operation will block until data is available.

Example in shell:
```cat < mypipe  # Read data from the named pipe```

Example in C:
```
#include <fcntl.h>
#include <unistd.h>
#include <stdio.h>

int main() {
    char buffer[100];
    int fd = open("/tmp/mypipe", O_RDONLY);  // Open the named pipe for reading
    read(fd, buffer, sizeof(buffer));         // Read data from the pipe
    printf("Received: %s\n", buffer);         // Print received data
    close(fd);                                 // Close the pipe
    return 0;
}
```
#### Use Cases for Named Pipes
- Inter-Process Communication:

Named pipes allow separate processes to communicate with each other without sharing a common ancestor. This is useful for coordinating tasks, exchanging data, and synchronizing operations.
- Data Streaming:

Named pipes are suitable for streaming data between processes, such as sending log messages from one application to another or processing data in a pipeline fashion.
- Temporary Data Storage:

Named pipes can act as a temporary storage mechanism for data being generated and consumed in a controlled manner

### Limitations of Named Pipes
- Blocking Behavior:

The blocking nature of named pipes can lead to deadlocks if not managed properly. If the writer writes to a pipe that has no reader, it can block indefinitely.
- No Random Access:

Named pipes do not support random access. You can only read and write in a sequential manner.
- Limited Buffering:

Named pipes have a limited amount of buffer space. If the buffer fills up, the writing process may block until there is space available.


## FIFOs and Blocking Behavior in Pipes
### FIFO (First In, First Out)

A FIFO is a special type of named pipe in Unix-like systems. It behaves as a First In, First Out structure, meaning that the data is read in the same order it was written. Unlike unnamed pipes, which are temporary and exist only as long as the process is running, FIFOs can exist as persistent files in the filesystem, allowing for communication between processes that do not share a common parent process.

#### Example of FIFO:

1. A process creates a FIFO named "data_pipe" using `mkfifo`.
2. Process A writes "Hello" into "data_pipe."
3. Process B reads "Hello" from "data_pipe."
4. Process A writes "World" into "data_pipe."
5. Process B reads "World" from "data_pipe."

In this scenario, the data written by Process A is read by Process B in the exact order it was written, demonstrating the First In, First Out behavior of FIFOs.

_**All named pipes are FIFOs because they allow data to be read in the order it was written (first in, first out) and have a name in the file system for access. However, not all FIFOs are named pipes because unnamed (or anonymous) pipes exist only for communication between related processes and do not have a name in the file system. Thus, while every named pipe is a FIFO, some FIFOs lack a name and are temporary.**_

### Example of Blocking Behavior

#### Example 1: Reader Blocks Until Data is Written
When a process tries to read from a pipe, and no data is available, it blocks (waits) until another process writes data into the pipe. The reader is suspended until the writer writes data.

**Scenario:**
1. Process A (reader) tries to read from a pipe.
2. No data is currently available in the pipe.
3. Process A is blocked, waiting for data.
4. Process B (writer) writes data to the pipe.
5. Process A can now continue and read the data.

#### Example 2: Writer Blocks Until Space is Available
When a process tries to write data to a pipe, and the pipe is full (it has a limited buffer size), the writing process blocks until there is space available.

**Scenario:**
1. Process A (writer) tries to write data to a pipe.
2. The pipe's buffer is full, as no one has read the data yet.
3. Process A is blocked, waiting for space in the pipe.
4. Process B (reader) reads data from the pipe.
5. Process A can now continue and write more data.


## Process Substitution:
Process substitution is a feature in Unix-like operating systems that allows the output of a command to be treated as if it were a file. This enables processes to communicate with each other without the need for intermediate files on disk. It's particularly useful for passing data between commands in a pipeline or for providing input to commands that expect file names.

Key Characteristics of Process Substitution:
- Temporary File Creation:

Process substitution creates a temporary file or named pipe (FIFO) that holds the output of a command. This temporary file can then be accessed by other commands as if it were a regular file.
- File Descriptor Access:

The process substitution syntax allows a command to read from the standard output of another command. The shell takes care of creating the temporary file and directing the output to it.
- Syntax Variants:

There are two common syntaxes for process substitution:
`<(command)`: This syntax creates a named pipe and allows the command's output to be read as if it were a file.
`>(command)`: This syntax creates a named pipe and allows the command to write its output to the output of the specified command.

Process Substitution Syntax

-- Input Process Substitution (<(command)): The output of command is sent to a temporary file (or named pipe), and the path to this file can be used as an argument to other commands.
-- Output Process Substitution (>(command)): The output of a command can be redirected to a named pipe that is processed by another command.
### Benefits of Process Substitution
- Efficiency:

Process substitution allows commands to run concurrently without the overhead of writing intermediate results to disk. This can lead to improved performance, especially with large datasets.
- Simplicity:

It simplifies scripts by reducing the need for temporary files and complex redirection. You can achieve more complex command-line operations in a concise manner.
- Cleaner Code:

By using process substitution, scripts and command lines become cleaner and more readable, as they avoid cluttering the filesystem with temporary files.
Limitations of Process Substitution
- Not Supported in All Shells:

While process substitution is supported in Bash and some other shells, it may not be available in all Unix-like shells (e.g., older versions of sh or dash).
- Resource Consumption:

Process substitution uses system resources for temporary files or named pipes. While this is generally not a problem, it can add overhead if used excessively in resource-constrained environments.
- Blocking Behavior:

If the output process is slower than the input process, the output may block, which can lead to unexpected behavior if not managed properly.

### Differences among Unnamed Pipes, Named Pipes and Process Substitutions:

| Feature                    | Unnamed Pipes                                                 | Named Pipes (FIFOs)                                             | Process Substitution                                                     |
|----------------------------|---------------------------------------------------------------|-----------------------------------------------------------------|--------------------------------------------------------------------------|
| Persistence                 | Temporary, in-memory, only lasts as long as the process       | Persistent, exists in the filesystem until removed              | Temporary, exists only while the shell command is running                |
| Naming                      | Anonymous (no name in the filesystem)                         | Named (has a file path)                                          | No explicit name (file descriptor or temporary file managed by the shell) |
| Inter-process Communication | Between related processes (e.g., parent-child)                | Between any processes with access to the pipe                   | Between commands within a shell pipeline                                 |
| Direction of Communication  | Unidirectional                                                | Unidirectional (but can simulate bidirectional using two pipes) | Can simulate either input or output substitution depending on the syntax |
| Creation                    | Implicitly created using `|` between commands                | Created manually using `mkfifo`                                  | Created by the shell using `<(command)` or `>(command)`                  |
| Filesystem                  | Does not appear in the filesystem                             | Appears as a special file (FIFO) in the filesystem               | Temporary file or file descriptor created by the shell                   |
| Concurrency                 | Commands connected by a pipe run concurrently                 | Commands using the pipe must coordinate to avoid blocking        | Commands run concurrently, and the shell handles communication           |
| Use Case                    | Simple pipelines between commands                            | IPC between unrelated processes (or across multiple terminals)   | Passing command output or input as a file for comparison, manipulation   |
| Example                     | `ls \| grep file`                                              | `mkfifo mypipe` + `echo "Hello" > mypipe`                       | `diff <(ls dir1) <(ls dir2)`                                             |

===========================================================================

# Processes and Jobs

## Session Heads, Process Groups, and Group Heads in Linux

In Linux, processes are organized in a hierarchical structure, and terms like **session heads**, **process groups**, and **group heads** describe the way these processes are grouped and managed, especially when it comes to handling signals and controlling terminals. Here's a breakdown of each concept:

### 1. Session Heads (Session Leaders)
A **session** in Linux is a collection of one or more processes. The **session head** (or **session leader**) is the process that starts a session and leads it. Sessions are often associated with terminal control (for instance, all processes started from a single terminal session).

- The **session head** is typically the first process in the session, such as the shell when you log in to a terminal.
- All processes in the same session are typically related, for instance, they might be part of a command pipeline or background job.

**Example**: When you open a terminal, the shell (like `bash` or `zsh`) becomes the session leader. If you run commands in the terminal, those commands belong to the same session.

### 2. Process Groups
A **process group** is a collection of one or more processes that are related and can be controlled together. Each process group has a **group leader**, which is the first process in the group (usually the parent process that spawns other child processes).

- Process groups are used to manage sets of processes, especially in job control. For example, if you run a pipeline of commands (e.g., `cat file | grep something | sort`), all processes involved in the pipeline belong to the same process group.
- A **process group** allows signals (like `SIGINT`, triggered by pressing `Ctrl+C`) to be sent to all processes in the group.

**Example**: If you run a background job in a shell using `&`, all processes involved in that job form a process group, and you can manage them together (e.g., stop or resume them with signals).

### 3. Group Heads (Process Group Leaders)
The **group head** or **process group leader** is the process that starts a process group. It’s the first process in the group and typically controls the other processes in the group.

- The group leader’s PID (Process ID) is also the **process group ID (PGID)** for the entire group.
- If the group leader exits, the group still exists as long as there are other processes in it, but no new processes can join it.

**Example**: When you run a pipeline of commands, the first command in the pipeline is usually the group leader, and its PID becomes the process group ID for all the processes in that pipeline.

### How They Work Together
- **Session Leader**: Leads a session, which may contain one or more process groups.
- **Process Group**: A subset of processes in the session that can be managed together.
- **Process Group Leader**: The head of a process group, often the first process in a pipeline or job.

#### Visual Representation:
1. **Session Head (Leader)**  
   - Shell (`bash`) is the session leader.

2. **Process Group**  
   - You run a pipeline of commands (`cat file | grep something | sort`). All processes involved in this pipeline form a process group. The first command (`cat`) is the **group leader**, and all the processes are part of the same group.
   
3. **Session Example**:
   - Session Head (Shell)  
     - Process Group 1 (Pipeline or Background Job 1)  
       - Group Head (First command in the group)  
       - Other processes in the group (subsequent commands in the pipeline)  
     - Process Group 2 (Pipeline or Background Job 2)  
       - Group Head  
       - Other processes
   
### Why It Matters:
- **Job Control**: Sessions and process groups allow you to control jobs in your shell. For example, you can suspend, resume, or kill entire groups of processes.
- **Signal Handling**: Signals like `SIGTERM`, `SIGINT`, or `SIGHUP` can be sent to entire process groups. This is useful for controlling processes as a whole, especially in terminal sessions.
- **Terminal Management**: In terminal sessions, the session leader controls the terminal. If you close the terminal, it sends a `SIGHUP` signal to all processes in the session, typically causing them to terminate.

### Summary:
- **Session Leader**: The first process in a session, typically the shell.
- **Process Group**: A group of related processes that can be controlled together, usually formed by pipelines or background jobs.
- **Process Group Leader**: The first process in a process group, often the first command in a pipeline.

This structure allows for efficient job control, signal handling, and process management in Linux.

## Summary of TTY, Shells, and Terminal Emulator
### TTY (Teletypewriter)
Originally referred to hardware devices providing direct access to the operating system. In modern usage, TTY often represents terminal devices in Unix-like systems.

### Pseudo-Terminal (PTY)
In graphical environments, users interact with a pseudo-terminal (PTY), which emulates the behavior of a physical TTY, allowing command-line interactions within terminal emulators.

### Shell
A command-line interface (CLI) that interprets user commands. Shells can be:
- **Interactive**: When a user runs an executable and receives a prompt for input.
- **Non-Interactive**: When a script is executed without requiring user input during its execution.

### Terminal
Acts as a connection between the user and the shell, allowing users to input commands and receive output.

### Script
A file containing a set of commands that can be executed by the shell.

### TTY Group
On most systems, this is a default group that does not have special permissions for managing TTY devices. Management of TTY devices is generally handled by root or administrative privileges, allowing regular users to access TTYs without being in a specific group.

#### Key Points
- When using a graphical terminal emulator, you are interacting with a PTY, not a physical TTY.
- TTYs represent the connection to the OS, while PTYs provide a virtual interface that mimics TTY functionality.


===========================================================================

# File Types
There are different file types in linux which is identified by the first character of the file permissions string. 

# Types of Files in Linux

The following table shows the types of files in Linux and what will be output using ls and file command.

| The file type using "ls -l" is denoted using | File Type      | Description                                    | Command to create the File | Located in   | FILE command output                       |
|----------------------------------------------|-----------------|------------------------------------------------|-----------------------------|--------------|-------------------------------------------|
| -                                            | Regular File    | Common files that store user data.            | touch                       | Any directory | PNG Image data, ASCII Text, etc.         |
| d                                            | Directory File   | A folder that contains files and directories.  | mkdir                       | It is a directory | Directory                                 |
| b                                            | Block Files     | Files that manage data in blocks.             | fdisk                      | /dev         | Block special                             |
| c                                            | Character Files  | Files that manage data as a stream of characters. | mknod                   | /dev         | Character special                         |
| p                                            | Pipe Files      | Used for inter-process communication.          | mkfifo                     | /dev         | FIFO                                      |
| l                                            | Symbol Link Files | A shortcut to another file.                    | ln                          | /dev         | Symbol link to <linkname>                |
| s                                            | Socket Files    | Used for network communication.                | socket() system call       | /dev         | Socket                                    |

===========================================================================

# Understanding File Permissions
Understanding file permissions as numbers:

**4 = r (read)      2 = w (write)      1 = x (execute)**

For each group, you add the three numbers together to create a single-digit representation of the permissions for that group. For example:

- 0 means no permissions

- 4 means read only (4)

- 5 means read and execute (4 + 1)

- 6 means read and write (4 + 2)

- 7 means all permissions (read, write, and execute, or 4 + 2 + 1)

When using numeric representation, the numbers can be three or four digits. In the case of a four-digit number, the first digit is used to set setuid, setgid, or sticky bit. The last three digits represent a combination of read, write, and execute added together (as shown above).


**4 = setuid      2 = setgid      1 = sticky bit**

## setuid: 
A bit that makes an executable run with the *privileges* of the owner of the file.

In some cases, you may need a user to run a program with more privileges — usually root privileges — than they have by default. The textbook case for this is the passwd command that allows users to change their own password. Changing your password inherently requires changing the `/etc/shadow` file. However, only the root user has write access to `/etc/shadow`.
```
cooluser@LAPTOP-5V55HON5:~$ ls -l /etc/shadow
-rw-r—– 1 root shadow 1824 Oct 18 19:49 /etc/shadow
cooluser@LAPTOP-5V55HON5:~$
```
Under normal circumstances, that suggests we'd need to be root or have sudo privileges to change our password. However, normal users can execute the passwd command to change their own password without sudo or root permissions but only on the condition that the permissions will have a character `s` instead of that of executable `x`. 
```
cooluser@LAPTOP-5V55HON5:~$ passwd
Changing password for cooluser.
Current password:
New password:
Retype new password:
passwd: password updated successfully
cooluser@LAPTOP-5V55HON5:~1$
```
To understand why passwd seemingly grants root-level access but ls doesn't, let's take a look at the permissions on those two executables.
```
cooluser@LAPTOP-5V55HON5:~$ ls -l /bin/ls
-rwxr-xr-x 1 root root 142144 Sep  5  2019 /bin/ls
cooluser@LAPTOP-5V55HON5:~$ ls -l /bin/passwd
-rwsr-xr-x 1 root root 68208 May 28 01:37 /bin/passwd
cooluser@LAPTOP-5V55HON5:~$
```
The passwd executable has character `s` instead of `x` in the root executable permissions whereas the other executable has `x`.

If we try to execute the one with `x`, it won't let us do so but we can execute the one with `s`.

It basically means that when we run the `passwd` command it is automatically executed as the **OWNER** of the file **WITHOUT** giving the user the **root or sudo access**.

## setgid:
A bit that makes an executable run with the *privileges* of the group of the file. It is the same as setuid but the s will be present in the position of the group.

## sticky bit: 
A bit set on directories that allows only the owner or root to delete or rename files and subdirectories. It does not affect other operations like reading, writing, or executing files.

Like we have `s` for **setuid** and **setgid**, we have `t` for **sticky bit**.

If there's a `t` included at the end of all 9 permission characters, it means the **sticky bit** is set.

A user (_except_ root, owner or the command, sudo) **CAN add** files or subdirectories inside the directory which has sticky bit set but **cannot delete or rename** the existing files or subdirectories.

While setting **setuid**, **setgid** and **sticky bit**, we append `4`,`2` and `1` respectively to the already existing `3 digit` numeric representation of file permissions in the beginning.
For example:
chmod 4755 <file name>

Here, 4 denotes setuid, 7 = all perms to owner, 5 and 5= read and execute perms to group and other users.
Similarly, 2 and 1 will denote their respective setting.

We can also set setuid, setgid and sticky bit by simply writing u+s, g+s, +t in the options respectively.


===========================================================================

# Types of Variables in Linux

In Linux, variables are used to store data or values that can be referenced or manipulated by commands and scripts. There are several types of variables in Linux, each serving different purposes and having distinct behaviors.

## 1. Environment Variables

- **Definition**: These are global variables that are available to all processes and subshells spawned from the shell. They affect the behavior of the shell and other system processes.
- **Scope**: System-wide (available to all users and processes).
- **Usage**: Typically used to configure the environment for applications and the shell.

**Examples**:

- `$HOME` – The home directory of the current user.
- `$PATH` – Directories searched for executable commands.
- `$USER` – The name of the current user.
- `$SHELL` – The current shell in use.

**How to Set**:
```bash
export VARIABLE_NAME=value
```

**How to Access**:
```bash
echo $VARIABLE_NAME
```

**Persistence**: To make environment variables persistent across sessions, add the `export` command to files like `~/.bashrc` or `~/.profile`.

---

## 2. Shell (Local) Variables

- **Definition**: These are variables that are only available in the current shell session. They are not passed to other processes or subshells.
- **Scope**: Local to the current shell.
- **Usage**: Used for temporary data or within shell scripts.

**Examples**:

- `greeting="Hello"`
- `count=5`

**How to Set**:
```bash
VARIABLE_NAME=value
```

**How to Access**:
```bash
echo $VARIABLE_NAME
```

**Difference from Environment Variables**: Shell variables are not exported to subshells or child processes unless explicitly done using `export`. For example:
```bash
name="Yash"
export name
```

---

## 3. Positional Parameters

- **Definition**: These are special variables that store arguments passed to a shell script or command. They are indexed numerically.
- **Scope**: Local to the script or function in which they are used.
- **Usage**: Commonly used in scripts to handle input arguments.

**Examples**:

- `$0` – The name of the script or command being executed.
- `$1`, `$2`, `$3`, etc. – The first, second, third, and so on, arguments passed to the script.
- `$@` – All the arguments passed to the script.
- `$#` – The number of arguments passed to the script.

---

## 4. Special Variables

- **Definition**: These are predefined variables that hold specific information and are used by the shell to manage processes and outputs.
- **Scope**: System-wide or shell-specific.
- **Usage**: Automatically updated by the system or shell.

**Examples**:

- `$$` – The process ID (PID) of the current shell.
- `$?` – The exit status of the last command.
- `$!` – The PID of the last background process.
- `$*` – All arguments passed to the script as a single string.

---

## 5. Array Variables

- **Definition**: These are variables that can store multiple values in an indexed format, available in shells like `bash`.
- **Scope**: Local to the current shell or script.
- **Usage**: Useful for handling lists of data within a script.

**Example**:
```bash
my_array=(apple banana cherry)
echo ${my_array[1]}  # Outputs "banana"
```

---

## 6. Readonly Variables

- **Definition**: These variables cannot be changed once they are set. They are often used to protect critical values.
- **Scope**: Local or global.
- **Usage**: Used for values that should not be modified.

**Example**:
```bash
readonly VAR="immutable"
VAR="newvalue"  # This will cause an error
```

---

## 7. Global Variables

- **Definition**: These are variables that are defined as `export`ed variables in the shell and are available to all subshells or processes spawned by the shell.
- **Scope**: The entire shell session, including child processes.
- **Usage**: Useful when you need the same variable to be accessible across multiple scripts or commands.

**Example**:
```bash
export GLOBAL_VAR="I am global"
```

---

## Key Differences Between Types

- **Environment vs Shell Variables**: Environment variables are inherited by child processes, whereas shell variables are only available within the shell that defines them.
- **Local vs Global Variables**: Global variables can be accessed by any subshell, while local variables are confined to the shell in which they were created.
- **Readonly Variables**: These are protected from modification after they are set.
- **Positional Parameters**: These handle arguments passed to shell scripts (`$1`, `$2`, etc.).

---

## Summary

- **Environment Variables**: Global and inherited by all processes.
- **Shell Variables**: Local to the current shell.
- **Positional Parameters**: Handle script arguments (`$1`, `$2`, etc.).
- **Special Variables**: Predefined system variables (`$$`, `$?`, etc.).
- **Array Variables**: Store multiple indexed values.
- **Readonly Variables**: Cannot be modified after assignment.

Each type of variable in Linux has specific use cases, and understanding their scope and behavior is essential for effective shell scripting and system administration.


---

## Comparison Table

| **Type of Variable**    | **Scope**                         | **Persistence**                           | **Examples**                           |
|-------------------------|-----------------------------------|-------------------------------------------|----------------------------------------|
| **Environment Variables**| System-wide, inherited by processes | Persistent (if added to config files)      | `$HOME`, `$PATH`, `$USER`, `$SHELL`    |
| **Shell Variables**      | Local to the current shell        | Not persistent unless exported            | `greeting="Hello"`, `count=5`          |
| **Positional Parameters**| Local to script or command        | Temporary (only during script execution)   | `$0`, `$1`, `$@`, `$#`                 |
| **Special Variables**    | Shell-wide or system-specific     | Temporary (updated by the system/shell)    | `$$`, `$?`, `$!`, `$*`                 |
| **Array Variables**      | Local to the current shell/script | Persistent during script/shell execution   | `my_array=(apple banana cherry)`       |
| **Readonly Variables**   | Local or global                  | Cannot be changed after assignment         | `readonly VAR="immutable"`             |
| **Global Variables**     | Available across subshells        | Persistent within the shell session        | `export GLOBAL_VAR="I am global"`      |


===========================================================================


# Explanation of Padding in Base64 Encoding

In the context of **Base64 encoding**, **padding** refers to the use of one or more `=` characters added to the end of the encoded output to ensure that the final encoded string has a length that is a multiple of 4 characters.

## Why Padding Is Needed in Base64 Encoding:

- **Base64 encoding** works by converting **every 3 bytes (24 bits)** of input data into **4 groups of 6 bits**. Each of those 6-bit groups is then represented by a character from the Base64 alphabet (64 characters in total).
- If the input data is not a multiple of 3 bytes, the encoding process cannot complete the final group of 4 Base64 characters, and padding (`=`) is used to fill the gap.

## When Padding Occurs:
- **No padding**: When the input length is a multiple of 3 (e.g., 6 bytes, 9 bytes, 12 bytes), the encoded output is naturally a multiple of 4 Base64 characters, so no padding is required.
  
- **One `=` padding**: If the input is **2 bytes more than a multiple of 3** (e.g., 5 bytes, 8 bytes), Base64 will output 3 Base64 characters and add **one `=`** to complete the 4-character block.

- **Two `=` padding**: If the input is **1 byte more than a multiple of 3** (e.g., 4 bytes, 7 bytes), Base64 will output 2 Base64 characters and add **two `=` characters** to complete the 4-character block.

## Example:

Let’s take an example of encoding the string `Man` in Base64.

1. **"Man"** (3 bytes):
   - In binary: `M` = 01001101, `a` = 01100001, `n` = 01101110.
   - Grouped as 24 bits: `01001101 01100001 01101110`.
   - Convert to 4 groups of 6 bits and represent each with a Base64 character: `TWFu`.
   - **No padding needed**, as 3 bytes make a perfect 4-character Base64 block.

2. **"Ma"** (2 bytes):
   - In binary: `M` = 01001101, `a` = 01100001.
   - Grouped as 16 bits: `01001101 01100001`.
   - Convert to 3 Base64 characters (`TWE`), but to make it a valid 4-character group, **one `=` is added**: `TWE=`.

3. **"M"** (1 byte):
   - In binary: `M` = 01001101.
   - Grouped as 8 bits: `01001101`.
   - Convert to 2 Base64 characters (`TQ`), and to make it a 4-character group, **two `=` characters are added**: `TQ==`.

## Purpose of Padding:

- Padding ensures that the Base64-encoded string has a standard length that is a multiple of 4 characters.
- It is only used when the length of the input data is not divisible by 3, filling in the remaining space in the last 4-character group.

## Summary:

- Padding (`=`) in Base64 is used to ensure that the encoded output always has a length that is a multiple of 4 characters, even when the input length isn’t a multiple of 3 bytes.
- One `=` or two `==` are added at the end of the encoded output if the input data doesn’t perfectly fill the 4-character groups.

===========================================================================

# Understanding GDB and ELF Files
**_NOTE: This is in reference to [GDB Baby Step 1](https://github.com/Gulabi-Dil/cryptonite_taskphase_Yashovardhan/blob/b01dc85753652b05cdfb19959c27241f1f32fc1e/PICOCTF/Reverse%20Engineering/GDB%20Baby%20Step%201.md)_**
## What is GDB?
GDB stands for **GNU Debugger**, a tool that allows you to examine what’s happening inside a program while it runs or what it was doing just before it crashed. You can see the contents of variables, step through each line of code, and inspect memory, among other things. It's especially useful for debugging low-level code, like C or assembly.

## Running ELF Files
An **ELF file** (Executable and Linkable Format) is a standard file format for executables, object code, and shared libraries in Linux. When you try to run an ELF file directly (e.g., `./filename`), the system usually executes it. However, if there's an issue, like missing permissions or dependencies, it might not run directly.

Sometimes, you may open an ELF file with GDB instead, especially if you want to **debug** it. By using GDB, you can see the inner workings of the ELF file step-by-step.

## Why Use GDB to Run an ELF File?
When a program doesn't behave as expected, you can use GDB to run it in a controlled environment. This allows you to:
1. Pause execution at specific points (breakpoints).
2. Examine the state of variables, memory, and registers.
3. Understand why it crashes or produces incorrect output.

If you had trouble running the ELF file directly with `./filename`, using GDB helps identify issues, like missing files or incorrect paths, by giving detailed error messages.

## Symbols in GDB
Symbols are names in the code, like function and variable names, that GDB uses to reference specific parts of the program. When you **load a program with symbols** in GDB, you get more readable information—like function names instead of just memory addresses.

For example, without symbols, you might see something like `0x00401122`, which is hard to understand. With symbols, GDB can tell you that `0x00401122` is inside a function called `main`, making debugging easier.

### Debugging Basics
Debugging is the process of identifying and fixing issues in a program. GDB helps you:
- Step through the program line-by-line to see what it does.
- Check if variables hold expected values.
- Inspect memory and register contents.

### GDB Command: `info functions`
When you run `info functions`, GDB lists all the functions available in the program. This includes:
- **Non-debugging symbols**: These are essential functions, but they don't have extra debugging info.
- **Debugging symbols**: If the program was compiled with debugging info (like with `-g` flag), you'll see more detailed function names and variable names.

### Disassembling Code in GDB
The `disassemble` command shows the low-level assembly instructions of a function, letting you see what’s happening under the hood.

For example, `disassemble main` shows the assembly code of the `main` function.

### GDB Command: `print`
The `print` command in GDB allows you to examine values in memory or in registers.

For example, `print $eax` displays the contents of the `eax` register, which is a place where the CPU stores data during execution.

## Commonly Used Commands
- **break [location]**: Set a breakpoint at a specific line or function.
- **run**: Start the program.
- **next**: Step to the next line of code, but don't go into functions.
- **step**: Step to the next line of code and go into functions if possible.
- **continue**: Resume execution until the next breakpoint or program end.

---

## Example GDB Session
Here’s a sample GDB session based on the screenshot provided:

1. **Start GDB**: Run `gdb ./filename` to start debugging.
2. **View Functions**: Use `info functions` to list all functions.
3. **Disassemble**: Use `disassemble main` to see the assembly instructions of `main`.
4. **Inspect Values**: Use commands like `print` to check values in memory or registers.

This session helps in understanding what each part of the program does, especially useful for debugging complex issues.


