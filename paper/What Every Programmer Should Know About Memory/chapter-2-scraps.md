Overall Summary of Section 2 (Commodity Hardware Today):
This section describes the typical hardware architecture found in modern commodity computers, focusing on how CPUs connect to memory and other devices. It explains the traditional Northbridge/Southbridge architecture and its limitations, leading to the development of systems with integrated memory controllers and the rise of Non-Uniform Memory Access (NUMA). It introduces the fundamental differences between RAM types (SRAM vs. DRAM) and the technical details of DRAM access, highlighting the latency and bandwidth constraints that programmers need to understand.

Subsection Summaries:

Introduction (pp. 3-4):

Discusses the prevalence of commodity hardware and multi-core/multi-socket systems.
Details the traditional Northbridge/Southbridge architecture (Figure 2.1), where CPUs connect via a Front Side Bus (FSB) to the Northbridge (memory controller), which connects to RAM and the Southbridge (I/O).
Identifies bottlenecks: shared FSB, single RAM port via Northbridge.
Explains Direct Memory Access (DMA) allowing devices to bypass the CPU for RAM access, but still consuming Northbridge bandwidth.
Introduces alternative designs like external memory controllers (Figure 2.2) and integrated memory controllers (Figure 2.3), which increase bandwidth but introduce NUMA (Non-Uniform Memory Access), where access time depends on memory location relative to the CPU.
2.1 RAM Types (pp. 5-7):

Contrasts Static RAM (SRAM) and Dynamic RAM (DRAM).
SRAM: Uses a 6-transistor cell (Figure 2.4), is fast, retains data as long as powered (no refresh needed), but is complex and expensive. Used primarily for CPU caches.
DRAM: Uses a simple 1-transistor, 1-capacitor cell (Figure 2.5). It's dense and cheap, making it suitable for main memory. However, it's slower, the capacitor charge leaks (requiring constant refresh cycles), and reading the cell discharges the capacitor (requiring recharge).
Explains DRAM addressing uses multiplexing (sending row then column address) to reduce pin count (Figure 2.7).
2.2 DRAM Access Technical Details (pp. 8-12):

Focuses on Synchronous DRAM (SDRAM) and its successors (DDR, DDR2, DDR3).
Explains the read access timing protocol: activate row (RAS), wait tRCD, select column (CAS), wait CAS Latency (CL), then transfer data (Figure 2.8).
Details the precharge command (Figure 2.9) required before activating a new row (delay tRP) and the minimum time a row must be active (tRAS), adding latency.
Describes how DDR generations increase bandwidth (transferring 2, 4, or 8 bits per clock cycle via I/O buffers) without proportionally increasing core array frequency (Figures 2.10-2.13, Tables 2.1, 2.2).
Mentions Fully Buffered DRAM (FB-DRAM) as a serial bus alternative allowing more channels and DIMMs per channel (p. 11-12).
Concludes DRAM access involves significant protocol overhead and latency, making sequential access much more efficient than random access.
2.3 Other Main Memory Users (pp. 12-13):

Points out that high-performance devices (network cards, storage controllers) use DMA to access main memory directly, competing with the CPU(s) for memory bandwidth (Figure 2.1).
Notes that systems using main memory as Video RAM for integrated graphics suffer significant performance and latency impacts due to frequent graphics access.


### Abbreviations
CPU (Central Processing Unit): The main processing unit of the computer. (p. 3)
FSB (Front Side Bus): The common bus connecting the CPU(s) to the Northbridge in older architectures. (p. 3)
RAM (Random-Access Memory): The main memory of the computer. (p. 3)
Northbridge: A traditional chipset component connecting the CPU(s), RAM, and sometimes high-speed graphics (like AGP). It contains the memory controller in this architecture. (p. 3)
Southbridge: A traditional chipset component connected to the Northbridge, handling lower-speed devices and I/O buses. (p. 3)
PCI-E / PCIe (PCI Express): A high-speed serial bus standard for connecting peripherals, successor to PCI and AGP. (p. 3, 25)
SATA (Serial AT Attachment): A bus interface for connecting storage devices like hard drives and SSDs, successor to PATA. (p. 3)
USB (Universal Serial Bus): A common interface standard for connecting various peripheral devices. (p. 3)
I/O (Input/Output): Refers to communication between the computer system and external devices. The Southbridge is often called the I/O bridge. (p. 3)
PCI (Peripheral Component Interconnect): An older parallel bus standard for connecting peripherals. (p. 3)
PATA (Parallel AT Attachment): An older parallel bus interface standard for storage devices, predecessor to SATA. (p. 3)
IEEE 1394: A serial bus interface standard, also known as FireWire or i.Link. (p. 3)
AGP (Accelerated Graphics Port): An older high-speed point-to-point channel specifically for graphics cards, usually connected to the Northbridge. (p. 3)
DMA (Direct Memory Access): A feature allowing hardware devices (like network cards or disk controllers) to read/write RAM directly without involving the CPU, using the Northbridge/memory controller. (p. 3, 12)
DDR / DDR1 / DDR2 / DDR3 (Double Data Rate SDRAM): Generations of synchronous dynamic RAM that transfer data multiple times per clock cycle (double-pumped, quad-pumped). DDR2 and DDR3 achieve higher speeds mainly by speeding up the I/O buffer relative to the core memory array. (p. 3, 8, 10, 11)
FB-DRAM (Fully Buffered DRAM): A type of DRAM module that uses a serial bus instead of a parallel bus, allowing more modules per channel and potentially more channels. (p. 3, 11)
MC (Memory Controller): The circuitry (part of the Northbridge or integrated into the CPU) that handles communication with the RAM modules. (p. 4)
SMP (Symmetric Multi-Processing): Systems with multiple CPUs that share the same memory and I/O resources. (p. 4)
NUMA (Non-Uniform Memory Architecture): An architecture, often resulting from integrated memory controllers, where the time to access memory depends on its physical location relative to the accessing processor (local vs. remote). (p. 4)
CSI (Common System Interface): Intel's technology name (at the time of writing) for an architecture with integrated memory controllers, similar to AMD's Opteron approach. (p. 4)
SRAM (Static RAM): A type of RAM that uses flip-flops (typically 6 transistors) to store bits. It's faster than DRAM and doesn't need refreshing but is less dense and more expensive. Used for CPU caches. (p. 5)
DRAM (Dynamic RAM): A type of RAM that uses a capacitor and transistor to store bits. It's dense and cheap but slower than SRAM and requires constant refreshing. Used for main memory. (p. 5)
6-T / 1-T (6-Transistor / 1-Transistor): Refers to the number of transistors used in a standard SRAM (6-T) or DRAM (1-T) memory cell. (p. 5)
WL (Word Line): The control line in an SRAM or DRAM cell array used to select a row of cells for reading or writing. (p. 5)
BL /  
BL
  (Bit Line / Inverted Bit Line): Complementary data lines used to read from or write to SRAM cells. (p. 5)
Vdd: Standard notation for the positive power supply voltage in electronic circuits. (p. 5)
AL (Access Line): The control line in a DRAM cell (connected to the transistor gate) used to enable access to the capacitor. (p. 5)
DL (Data Line): The line used to read the charge from or write charge to a DRAM cell's capacitor. (p. 5)
RC (Resistance-Capacitance): Refers to the time constant (Resistance × Capacitance) that determines the charge/discharge rate of the capacitor in a DRAM cell. (p. 6)
RAS ( 
RAS
 , Row Address Strobe/Selection): Signal used to latch the row address part when accessing DRAM. The bar indicates it's typically active low. (p. 7, 8)
CAS ( 
CAS
 , Column Address Strobe/Selection): Signal used to latch the column address part when accessing DRAM. Active low. (p. 7, 8)
SDRAM (Synchronous DRAM): DRAM that operates synchronized to a clock signal provided by the memory controller. (p. 8)
MHz (Megahertz): Unit of frequency (millions of cycles per second). (p. 8)
GB/s (Gigabytes per second): Unit of data transfer rate (bandwidth). (p. 8)
Mb/s (Megabits per second): Unit of data transfer rate. (p. 10)
MB/s (Megabytes per second): Unit of data transfer rate. (p. 10)
CLK (Clock): The timing signal used to synchronize operations in SDRAM. (p. 8)
tRCD (RAS-to-CAS Delay): The minimum time delay required between asserting RAS and asserting CAS. (p. 8)
CL (CAS Latency): The delay, in clock cycles, from asserting CAS to the first data becoming available on the bus. (p. 8)
WE ( 
WE
 , Write Enable): Signal used (often in combination with RAS/CAS) to indicate a write operation to DRAM. Active low. (p. 9)
tRP (Row Precharge time): The time required to deactivate the current row and prepare for activating a new row. (p. 9)
tRAS (Active to Precharge delay): The minimum time a row must remain active after a RAS signal before a precharge command can be issued. (p. 9)
SDR (Single Data Rate): Refers to early SDRAM that transferred data once per clock cycle. (p. 10)
I/O Buffer: Circuitry on the DRAM module that interfaces between the internal memory cell array and the external memory bus. In DDRx technologies, this buffer operates at a higher effective frequency than the cell array. (p. 10)
DIMM (Dual In-line Memory Module): The standard physical form factor for RAM modules used in desktops and servers. (p. 11, implied)