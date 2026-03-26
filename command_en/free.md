free
===

Display amount of free and used memory in the system.

## Description

The **free command** displays the amount of free and used physical memory and swap memory in the system, as well as the buffers and caches used by the kernel.

### Syntax

```shell
free (options)
```

### Options

```shell
-b # Display the amount of memory in bytes.
-k # Display the amount of memory in kilobytes (default).
-m # Display the amount of memory in megabytes.
-g # Display the amount of memory in gigabytes.
-o # Old format (do not display the buffer-adjusted line).
-s <seconds> # Continuously display the output every <seconds> seconds.
-t # Display a line showing the column totals.
-V # Display version information.
-h, --human # Automatically scale to shortest three-digit unit and display unit suffix.
```

### Examples

```shell
free -t    # Show memory usage totals.
free -s 10 # Periodically query memory usage every 10 seconds.
```

Display memory usage:

```shell
free -m
             total       used       free     shared    buffers     cached
Mem:          2016       1973         42          0        163       1497
-/+ buffers/cache:        312       1703
Swap:         4094          0       4094
```

**Explanation of the first part (Mem line):**

```shell
total: Total installed memory.
used: Used memory (calculated as total - free - buffers - cache).
free: Unused memory.
shared: Memory used (mostly) by tmpfs.
buffers: Memory used by kernel buffers.
cached: Memory used by the page cache.
```

Relationship: `total = used + free`

**Explanation of the second part (-/+ buffers/cache):**

```shell
(-buffers/cache) used memory: used - buffers - cached (from the first part).
(+buffers/cache) free memory: free + buffers + cached (from the first part).
```

The `-buffers/cache` value represents the memory actually used by programs, while `+buffers/cache` represents the total memory available for applications to use.

The third part refers to Swap space (virtual memory).

**Key Difference:**
The difference between the `used/free` values in the second line (Mem) and the third line (-/+ buffers/cache) depends on the perspective. From the OS perspective (first line), `buffers/cached` memory is considered "used". From the Application perspective (third line), `buffers/cached` memory is considered "available" because the kernel will quickly reclaim this memory if an application needs it.

Application perspective available memory = `system free memory + buffers + cached`.
In the example above: `18007156 = 2098428KB + 4545340KB + 11363424KB`.

### When does Swap occur?

Swap occurs when the available memory drops below a certain threshold. You can check detailed memory info here:

```shell
cat /proc/meminfo
```

Swap reduces physical page usage through three main ways:
1. Reducing the size of buffers and the page cache.
2. Swapping out System V shared memory pages.
3. Swapping out or discarding application memory pages (when physical memory is insufficient).

In fact, using a small amount of swap does not significantly impact system performance.

### Difference between Buffers and Cached:

To improve disk I/O efficiency, Linux uses two types of caches:

**Buffer Cache** and **Page Cache**. The former is for raw disk blocks, while the latter is for filesystem inodes (files). These caches significantly reduce the time required for I/O system calls (like `read`, `write`, `getdents`).

- **Page Cache**: Caches file data at the filesystem level.
- **Buffer Cache**: Caches raw disk blocks. When Page Cache data needs to be written to disk, it is passed to the Buffer Cache.

In modern kernels (2.6+), these are largely integrated. Page cache caches file data, while buffer cache caches metadata and raw block data (e.g., if you use `dd` to write directly to a device).

**Summary**: As long as the system is not heavily using Swap, you don't need to worry about low "free" memory. If Swap usage is consistently high, you should consider adding physical RAM. For application servers, primarily monitor the `+buffers/cache` value; if that is low, it's time to optimize the application or add memory.
