# Valgrind

Valgrind[1] is a great way to profile heap, stack and file descriptors within a C/C++ program.

## Usage

### Long running

    valgrind --tool=massif prog

Output: massif.out.<pid>

The output can be viewed via the command-line or `massif-visualizer`[2]::

    ms_print massif.out.<pid>

### Full memory check

    valgrind --tool=memcheck --leak-check=full --show-leak-kinds=all prog

### Track file descriptors

Ensure file descriptors are being properly managed.

    valgrind --track-fds=yes prog

### Threading

    valgrind --tool=helgrind prog

## Annoyances

### C epoll

If not using `struct epoll_event`.`data`.`u64`, must set it to 0 or Valgrind will
output a warning.

    e.data.u64 = 0;

## References

1. http://valgrind.org/docs/manual/QuickStart.html
2. http://milianw.de/tag/massif-visualizer
