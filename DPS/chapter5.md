# Chapter 5: File I/O - Further Details

This chapter builds on the foundational concepts of file I/O introduced earlier, extending them with more advanced topics and techniques used in Linux system programming.

## 1. Atomicity and Race Conditions
- **Atomicity** in file I/O means that an operation is performed as a single, uninterruptible action.
- **Race conditions** occur when multiple processes are trying to access or modify a file at the same time, potentially leading to inconsistent or incorrect results.
- **open()** with `O_EXCL`: The flag ensures the file is only created if it does not exist, preventing race conditions during file creation.

## 2. File Control Operations: `fcntl()`
- The **`fcntl()` system call** provides various file control operations for managing open files.
- **Key uses**:
  - **Changing file descriptor flags**: Flags like `O_APPEND` and `O_NONBLOCK` can be modified dynamically after opening the file.
  - **Duplicating file descriptors**: `dup()` and `dup2()` operations can be done through `fcntl()` as well.

### Example usage:
```c
int flags = fcntl(fd, F_GETFL);
if (flags == -1) errExit("fcntl");
flags |= O_APPEND;
if (fcntl(fd, F_SETFL, flags) == -1) errExit("fcntl");
