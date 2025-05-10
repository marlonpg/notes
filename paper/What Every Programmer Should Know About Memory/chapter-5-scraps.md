Overall Summary of Section 5 (NUMA Support):
This section focuses on Non-Uniform Memory Access (NUMA) architectures, where the time it takes to access memory varies based on its physical location relative to the CPU making the request. It begins by describing different NUMA hardware configurations, from CPUs with local memory to more complex interconnected multi-node systems (Figure 5.1). The section then discusses the crucial role of the Operating System (OS) in managing NUMA systems, particularly in terms of memory allocation strategies and process scheduling to minimize costly remote memory accesses. It details how the Linux kernel exposes NUMA topology information through the sysfs filesystem (Tables 5.1-5.4, Figure 5.2), and concludes by quantifying the performance degradation associated with accessing remote memory (Figures 5.3, 5.4).

Subsection Summaries:

5.1 NUMA Hardware (p. 43):

This subsection explains that NUMA architectures are increasingly common. In such systems, processors have "local" memory that is faster to access than "remote" memory attached to other processors.
It describes how systems like AMD's Opteron use interconnects (e.g., HyperTransport) to connect CPUs, allowing access to each other's local memory, and how these nodes can be arranged in topologies like hypercubes (Figure 5.1) to manage connectivity.
It also mentions larger, specialized NUMA machines (e.g., IBM x445, SGI Altix) where interconnects can be more complex and NUMA factors (the cost difference for remote access) can be significant.
5.2 OS Support for NUMA (pp. 43-44):

This part discusses the OS's role in managing NUMA systems. Ideally, the OS should allocate memory for a process from the node local to the CPU it's running on.
It highlights the challenge of process migration: moving a process to a different node can make its existing memory remote and thus slower to access, unless the memory pages are also migrated (which is a costly operation).
The default OS behavior might be to stripe memory allocations across all nodes to ensure even utilization and predictable average access costs, but this is generally not optimal for performance. Linux allows applications to specify memory allocation policies to override this default.
5.3 Published Information (pp. 44-45):

This subsection details how the Linux kernel makes NUMA topology and cache information available to user space via the /sys pseudo filesystem.
Information on CPU caches (type, level, sharing) is found under /sys/devices/system/cpu/cpu*/cache (Tables 5.1, 5.2).
CPU topology (core IDs, physical package) is under /sys/devices/system/cpu/cpu*/topology (Table 5.3).
NUMA node information (CPUs per node, distance/cost to other nodes) is located in /sys/devices/system/node/node* (Table 5.4).
The kernel also provides per-process NUMA memory mapping information in /proc/PID/numa_maps (Figure 5.2), showing which nodes the process's memory pages are allocated on.
5.4 Remote Access Costs (pp. 45-47):

This part quantifies the performance penalty of accessing remote memory in NUMA systems.
It references an AMD document (Figure 5.3) showing that remote memory accesses (1-hop or 2-hops away) can be significantly slower (e.g., 2-hop writes being 32% slower than local writes, 2-hop reads 30% slower than local reads).
Own benchmark results (Figure 5.4) show that remote read operations can consistently be around 20% slower. For write and copy operations, the slowdown is also about 20% if the data fits in caches. If the working set is much larger than the caches, the interconnect speed for remote writes might be sufficient if the main memory itself is the bottleneck.