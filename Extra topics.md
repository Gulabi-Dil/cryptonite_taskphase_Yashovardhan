- [Exit Status Variable in Linux](https://www.geeksforgeeks.org/exit-status-variable-in-linux/)
- [Grep Command](https://www.hostinger.in/tutorials/grep-command-in-linux-useful-examples/?utm_campaign=Generic-Tutorials-DSA|NT:Se|LO:IN-t5&utm_medium=ppc&gad_source=1&gclid=CjwKCAjwgfm3BhBeEiwAFfxrG8x2xPsN_OXGiqnhGabISx__S58VeXv6dzU5d6bKa4tyIorNARuIMRoCJ3oQAvD_BwE)
- [Difference between ;, && and |
# Unnamed Pipes:
Unnamed pipes are one of the simplest forms of inter-process communication (IPC) in Unix-like operating systems. They are typically used to connect two related processes (such as a parent process and its child process), allowing the output of one process to be sent directly to another.

## Key Characteristics of Unnamed Pipes
- **Temporary and Anonymous**: Unnamed pipes exist only as long as the process that created them is running. They do not have a name in the filesystem and cannot be accessed by unrelated processes.

- **One-way Communication**: Unnamed pipes are unidirectional, meaning data flows in one direction—from one process to another.
- **Parent-Child Communication**: Often used to pass data between a parent process and a child process created via fork() in C programming, or between commands connected in a pipeline in the shell.
- **File Descriptors**: Unnamed pipes use file descriptors to handle reading and writing. The process writing to the pipe uses one file descriptor (fd) for writing, and the process reading uses another for reading.

## Syntax in the Shell (Pipelines):
```command1 | command2```

The | symbol represents an unnamed pipe, sending the output of command1 directly into the input of command2.

Example:

```ls | grep "file"```

Here, the output of ls is passed directly to grep, and no intermediate file is created.
# Named Pipes:
Named pipes, also known as FIFOs (First In, First Out), are a special type of file in Unix-like operating systems that facilitate inter-process communication (IPC). Unlike unnamed pipes, which are temporary and exist only in memory while the communicating processes are running, named pipes have a presence in the filesystem and can be accessed by multiple processes, even if they are not related (i.e., they do not share a common ancestor).

## Key Characteristics of Named Pipes
- **Persistent in Filesystem**: Named pipes are created as special files in the filesystem, which allows them to persist beyond the life of the processes that created them. They are identified by a name in the filesystem, making them accessible for reading and writing by any process that knows the name.
- **Unidirectional Communication**: Named pipes are typically unidirectional, meaning data flows in one direction—from the writing process to the reading process. However, you can create two named pipes to allow for bidirectional communication.
- **Blocking Behavior**: When a process attempts to read from a named pipe, it will block (i.e., wait) until there is data available to read. Conversely, if a process tries to write to a named pipe that has no readers, it may also block until a reader is available.
- **FIFO Structure**: The name "FIFO" indicates that data is read in the order it was written. The first piece of data written to the pipe is the first to be read, following a first-in, first-out structure.

## How to Create and Use Named Pipes
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
### Use Cases for Named Pipes
- Inter-Process Communication:

Named pipes allow separate processes to communicate with each other without sharing a common ancestor. This is useful for coordinating tasks, exchanging data, and synchronizing operations.
- Data Streaming:

Named pipes are suitable for streaming data between processes, such as sending log messages from one application to another or processing data in a pipeline fashion.
- Temporary Data Storage:

Named pipes can act as a temporary storage mechanism for data being generated and consumed in a controlled manner

## Limitations of Named Pipes
- Blocking Behavior:

The blocking nature of named pipes can lead to deadlocks if not managed properly. If the writer writes to a pipe that has no reader, it can block indefinitely.
- No Random Access:

Named pipes do not support random access. You can only read and write in a sequential manner.
- Limited Buffering:

Named pipes have a limited amount of buffer space. If the buffer fills up, the writing process may block until there is space available.

# Process Substitution:
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
## Benefits of Process Substitution
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

## Difference between Unnamed Pipes, Named Pipes and Process Substitutions:

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
| Example                     | `ls | grep file`                                              | `mkfifo mypipe` + `echo "Hello" > mypipe`                       | `diff <(ls dir1) <(ls dir2)`                                             |


