slabtop
===

Display kernel slab cache information in real-time.

## Description

The **slabtop command** displays detailed information about the kernel "slab" buffer in real-time.

### Syntax

```shell
slabtop [option]
```

### Options

```shell
--delay=n, -d n: Update the display every n seconds (default is 3 seconds);
--sort=S, -s S: Sort the display by the specified criteria (see below or refer to the man page);
--once, -o: Display information once and exit;
--version, -V: Display version information;
--help: Display help information.
```

Sort criteria:

*   a: Sort by number of active objects
*   b: Sort by objects per slab
*   c: Sort by cache size
*   l: Sort by number of slabs
*   v: Sort by number of active slabs
*   n: Sort by name
*   o: Sort by number of objects
*   p: Sort by pages per slab
*   s: Sort by object size
*   u: Sort by cache utilization

### Knowledge Expansion

When kernel modules allocate resources, they use the slab allocator to improve efficiency and resource utilization. By examining slab information and combining it with source code analysis, you can get a rough understanding of system performance—for example, detecting if certain resources are abnormally high or if there are leaks. The Linux system exposes slab usage via `/proc/slabinfo`.

The slab allocator used by Linux is based on an algorithm first introduced by Jeff Bonwick for the SunOS operating system. Jeff's allocator is centered around object caching. In the kernel, a large amount of memory is allocated for a limited set of objects (such as file descriptors and other common structures). Jeff found that the time required to initialize a common object in the kernel exceeded the time required to allocate and release it. Therefore, he concluded that instead of releasing memory back to a global pool, it should be kept in a state initialized for a specific purpose. The Linux slab allocator uses this and other ideas to build a memory allocator that is efficient in both space and time.

The file containing information on all active slab caches in the system is `/proc/slabinfo`.

### Example

```shell
slabtop

 Active / Total Objects (% used)    : 897519 / 1245930 (72.0%)
 Active / Total Slabs (% used)      : 38605 / 38605 (100.0%)
 Active / Total Caches (% used)     : 94 / 145 (64.8%)
 Active / Total Size (% used)       : 129558.22K / 153432.58K (84.4%)
 Minimum / Average / Maximum Object : 0.01K / 0.12K / 128.00K

  OBJS ACTIVE  USE OBJ SIZE  SLABS OBJ/SLAB CACHE SIZE NAME                   
440136 171471  38%    0.05K   6113       72     24452K buffer_head
190086 148576  78%    0.05K   2437       78      9748K selinux_inode_security
151840 146366  96%    0.48K  18980        8     75920K ext3_inode_cache
144333 144143  99%    0.02K    711      203      2844K avtab_node
130529 128488  98%    0.13K   4501       29     18004K dentry_cache
 99214  99071  99%    0.03K    878      113      3512K size-32
 43834  28475  64%    0.27K   3131       14     12524K radix_tree_node
 17818   9450  53%    0.06K    302       59      1208K size-64
  4602   4562  99%    0.05K     59       78       236K sysfs_dir_cache
  3220   2855  88%    0.08K     70       46       280K vm_area_struct
  2460   2114  85%    0.12K     82       30       328K size-128
  1564   1461  93%    0.04K     17       92        68K Acpi-Operand
  1540   1540 100%    0.33K    140       11       560K inode_cache
  1524    466  30%    0.01K      6      254        24K anon_vma
  1440    515  35%    0.05K     20       72        80K avc_node
  1440   1154  80%    0.19K     72       20       288K filp
  1170   1023  87%    0.05K     15       78        60K ext3_xattr
   845    724  85%    0.02K      5      169        20K Acpi-Namespace
   638    315  49%    0.35K     58       11       232K proc_inode_cache
   450    434  96%    0.25K     30       15       120K size-256
   424    386  91%    0.50K     53        8       212K size-512
   312    107  34%    0.05K      4       78        16K delayacct_cache
   306    284  92%    0.43K     34        9       136K shmem_inode_cache
   303    108  35%    0.04K      3      101        12K pid
   300    261  87%    0.19K     15       20        60K skbuff_head_cache
   300    300 100%    0.12K     10       30        40K bio
   260    260 100%   32.00K    260        1      8320K size-32768
   254      6   2%    0.01K      1      254         4K revoke_table
   236     55  23%    0.06K      4       59        16K fs_cache
   216    203  93%    1.00K     54        4       216K size-1024
   214    214 100%    2.00K    107        2       428K size-2048
   203     83  40%    0.02K      1      203         4K biovec-1
```
