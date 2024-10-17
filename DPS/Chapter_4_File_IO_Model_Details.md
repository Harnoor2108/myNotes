
# Chapter 4: File I/O - The Universal I/O Model

This chapter provides a deep dive into the **universal I/O model** of UNIX/Linux systems, which underpins how input and output operations are performed. File descriptors, system calls for reading, writing, opening, and closing files are covered, along with advanced operations such as changing the file offset and using the `ioctl()` system call.

## 4.1 Overview
In UNIX and Linux systems, **file descriptors** are used to reference open files, whether they are regular files, devices, pipes, sockets, or terminals. Every process has its own set of file descriptors.

- File descriptors are non-negative integers.
- By default, the shell provides three standard file descriptors:
  - **stdin (0)**: Standard input, usually the keyboard.
  - **stdout (1)**: Standard output, usually the terminal.
  - **stderr (2)**: Standard error, usually for error messages.

Programs use these file descriptors to interact with files, devices, and other I/O resources.

## 4.2 Universality of I/O
The **universal I/O model** in UNIX/Linux ensures that the same system calls are used for all types of files, whether they are regular files, devices, pipes, or sockets. This model abstracts away the differences in file types, allowing developers to use the same code to handle different I/O resources.

- **Key I/O System Calls**:
  - `open()`: Open or create a file.
  - `read()`: Read data from a file or device.
  - `write()`: Write data to a file or device.
  - `close()`: Close an open file descriptor.

This consistency is one of the strengths of UNIX/Linux, allowing applications to interact with various file types seamlessly.

### Example:
```bash
$ ./copy file.txt file_copy.txt  # Copy a file
$ ./copy /dev/tty b.txt         # Copy data from a terminal device
```

The kernel handles device-specific details, abstracting away the complexity from user-space programs.

## 4.3 Opening a File: `open()`
The `open()` system call opens an existing file or creates a new one. It returns a file descriptor that can be used in subsequent I/O operations.

- **Arguments**:
  - `pathname`: The path to the file.
  - `flags`: The mode in which to open the file (e.g., `O_RDONLY`, `O_WRONLY`, `O_RDWR`).
  - `mode`: The permissions to use if a new file is created (this is optional and only used when creating a file).

- **Common flags**:
  - `O_CREAT`: Create the file if it does not exist.
  - `O_TRUNC`: Truncate the file to zero length if it already exists.
  - `O_APPEND`: Append data to the file.
  - `O_EXCL`: Ensure that the file is created and doesn't already exist (used with `O_CREAT`).

The return value is a file descriptor that represents the opened file.

### Example:
```c
int fd = open("file.txt", O_RDWR | O_CREAT, S_IRUSR | S_IWUSR);
```
In this example, `file.txt` is opened with read/write permissions. If the file does not exist, it is created with read/write permissions for the user.

## 4.4 Reading from a File: `read()`
The `read()` system call reads data from a file into a buffer. It returns the number of bytes read, or `0` if the end of the file is reached.

- **Arguments**:
  - `fd`: The file descriptor of the file.
  - `buffer`: A pointer to the memory where the read data will be stored.
  - `count`: The maximum number of bytes to read.

The return value is the number of bytes actually read, or `0` if the end of the file has been reached.

### Example:
```c
ssize_t bytesRead = read(fd, buffer, sizeof(buffer));
```

### Error Handling:
If `read()` encounters an error, it returns `-1`, and `errno` is set appropriately.

## 4.5 Writing to a File: `write()`
The `write()` system call writes data from a buffer to a file. It returns the number of bytes written.

- **Arguments**:
  - `fd`: The file descriptor of the file.
  - `buffer`: The data to be written.
  - `count`: The number of bytes to write.

The return value is the number of bytes successfully written, which may be less than `count` if an error occurs.

### Example:
```c
ssize_t bytesWritten = write(fd, buffer, sizeof(buffer));
```

### Error Handling:
If `write()` encounters an error, it returns `-1`, and `errno` is set.

## 4.6 Closing a File: `close()`
The `close()` system call is used to close an open file descriptor and release any resources associated with it.

### Example:
```c
close(fd);
```

After calling `close()`, the file descriptor is no longer valid and should not be used in further operations.

### Errors:
- If an error occurs (e.g., closing an already closed file descriptor), `close()` returns `-1` and sets `errno`.

## 4.7 Changing the File Offset: `lseek()`
The `lseek()` system call changes the file offset for a file descriptor. The file offset determines where the next `read()` or `write()` operation will occur.

- **Arguments**:
  - `fd`: The file descriptor.
  - `offset`: The new offset, relative to `whence`.
  - `whence`: Determines the reference point for the offset (`SEEK_SET`, `SEEK_CUR`, or `SEEK_END`).

### Example:
```c
off_t newOffset = lseek(fd, 0, SEEK_END);  // Move to the end of the file
```

The `lseek()` system call is often used to move to a specific location in a file, such as the end or beginning.

### Common Uses:
- Seeking to the end of a file to append data.
- Skipping over portions of a file during reading.

## 4.8 Operations Outside the Universal I/O Model: `ioctl()`
The `ioctl()` system call provides a mechanism for performing device-specific operations that do not fit into the universal I/O model. It allows low-level control over devices by sending control commands.

- **Arguments**:
  - `fd`: The file descriptor of the device.
  - `request`: The operation to be performed (varies by device).
  - `argp`: A pointer to a device-specific argument.

### Example Uses:
- Configuring terminal settings.
- Controlling network interfaces.
- Performing low-level operations on hardware devices.

### Example:
```c
ioctl(fd, request, &arg);
```

### Advanced Notes:
`ioctl()` is highly device-specific, and its behavior varies depending on the device being controlled. It is commonly used for hardware control, such as configuring a modem or setting terminal attributes.

## 4.9 Summary
The **universal I/O model** in UNIX/Linux provides a consistent interface for interacting with files, devices, and other I/O resources. System calls like `open()`, `read()`, `write()`, and `close()` are used to handle the vast majority of I/O operations in a simple and flexible manner. For device-specific operations, `ioctl()` is used to provide additional control and functionality outside the basic I/O model.
