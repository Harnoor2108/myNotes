
# Chapter 4: File I/O - The Universal I/O Model

This chapter of *The Linux Programming Interface* covers the concepts and system calls involved in performing file input and output (I/O) operations in UNIX/Linux systems. The **universal I/O model** is central to the UNIX philosophy, allowing flexible and consistent handling of different types of files and devices.

## 4.1 Overview
In UNIX and Linux, file I/O is built around **file descriptors**. These are small non-negative integers that reference open files. Every process has its own set of file descriptors. Standard file descriptors include:
- **stdin (0)**: Standard input
- **stdout (1)**: Standard output
- **stderr (2)**: Standard error

These are opened by the shell before the program starts.

## 4.2 Universality of I/O
The UNIX system is known for the **universality of I/O**, meaning that the same system calls (`open()`, `read()`, `write()`, `close()`) can be used for all types of files—regular files, pipes, sockets, and devices like terminals. This abstraction allows programs to work with different types of files in a consistent way without specialized code.

### Example: 
Copying files or reading from a terminal:

```bash
$ ./copy test test.old
$ ./copy /dev/tty b.txt
```

This is achieved by the kernel abstracting device-specific details.

## 4.3 Opening a File: `open()`
The `open()` system call opens an existing file or creates a new one. It takes the following arguments:
- `pathname`: The path to the file.
- `flags`: A bitmask specifying access mode, such as `O_RDONLY`, `O_WRONLY`, `O_RDWR`.
- `mode`: (Optional) The permissions to use if a new file is created.

On success, `open()` returns a file descriptor, used for subsequent I/O operations. The file can be created if it doesn't exist by passing the `O_CREAT` flag.

## 4.4 Reading from a File: `read()`
`read()` reads data from a file into a buffer. Its arguments are:
- `fd`: File descriptor of the file.
- `buffer`: Pointer to the memory where data will be stored.
- `count`: Maximum number of bytes to read.

The return value is the number of bytes read. If the end of the file is reached, `read()` returns 0.

## 4.5 Writing to a File: `write()`
`write()` writes data to a file. It takes the following arguments:
- `fd`: File descriptor of the file.
- `buffer`: Data to be written.
- `count`: Number of bytes to write.

The return value is the number of bytes written, which may be less than `count` if an error occurs.

## 4.6 Closing a File: `close()`
After all file I/O operations are completed, `close()` is called to release the file descriptor and any resources it uses.

## 4.7 Changing the File Offset: `lseek()`
`lseek()` changes the file offset, determining where the next `read()` or `write()` operation will occur. This can be used to move to a specific position in a file.

## 4.8 Operations Outside the Universal I/O Model: `ioctl()`
`ioctl()` is a special system call used for device-specific operations not covered by the universal I/O model. It allows programs to perform low-level device control.

## 4.9 Summary
The **universal I/O model** in UNIX/Linux systems provides a consistent interface for handling various file types. The `ioctl()` system call extends this model to cover device-specific operations, adding flexibility to how I/O is handled across devices.
