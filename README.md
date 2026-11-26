## Smartlabs 482 HD Base / Broadcom 7230 mainline

Mainline Linux port, Device Tree, and reverse-engineering notes for the SmartLabs SML-482 HD Base and other Broadcom BCM7230 / BMIPS4380 set-top boxes.

<img width="483" height="224" alt="image" src="https://github.com/user-attachments/assets/503e45b2-c471-439b-9ba0-c3c9c5a57224" />

Warning! This project is using AI code. If you don't like it, don't use it, please

## Hardware Specifications

| Component | Details |
| :--- | :--- |
| **SoC** | Broadcom BCM7230 (Dual-core BMIPS4380 @ 750 MHz) |
| **RAM** | 512 MiB DDR3 |
| **Storage** | 256 MiB NAND Flash |
| **Networking** | 10/100 Mbps Ethernet (RJ-45) + optional Wi-Fi module |
| **Ports** | HDMI 1.4a, USB 2.0 Host, TRRS AV / Analog Audio, IR Receiver |

## Progress
It's still a WIP, but the kernel already boots:
<details>
<summary>Click to expand full <code>dmesg</code> boot log</summary>

```text
CFE> boot -elf usbdisk0:/vmlinux-gentoo
Loader:elf Filesys:fat Dev:usbdisk0 File:/vmlinux-gentoo Options:(null)
Loading: Failed with error code -4
Could not load /vmlinux-gentoo: I/O error
Trying again with '-nz' option
Loading: prog_seg: 0x80010000/21197936 bss: 0x81447470/341552 Entry address is 0x80e26784
Starting program at 0x80e26784

[    0.000000] Linux version 7.3.1 (vitaliy@toolbx) (mipsel-buildroot-linux-gnu-gcc.br_real (toolchains.bootlin.com 2026.08-1) 15.3.0, GNU ld (GNU Binutils) 2.45.1) #9 SMP Mon Nov  2 11:46:00 +07 2026
[    0.000000] CPU0 revision is: 0002a064 (Broadcom BMIPS4380)
[    0.000000] FPU revision is: 00130001
[    0.000000] MIPS: machine is SmartLabs SML-482 HD Base
[    0.000000] earlycon: ns16550a0 MMIO32:0x10406980 (options '115200n8')
[    0.000000] printk: legacy bootconsole [ns16550a0] enabled
[    0.000000] Initrd not found or empty - disabling initrd
[    0.000000] OF: reserved mem: Reserved memory: No reserved-memory node in the DT
[    0.000000] Primary instruction cache 32kB, VIPT, 2-way, linesize 64 bytes.
[    0.000000] Primary data cache 64kB, 4-way, VIPT, cache aliases, linesize 64 bytes
[    0.000000] This processor doesn't support highmem. 262144k highmem ignored
[    0.000000] Zone ranges:
[    0.000000]   Normal   [mem 0x0000000000000000-0x000000001fffffff]
[    0.000000]   HighMem  empty
[    0.000000] Movable zone start for each node
[    0.000000] Early memory node ranges
[    0.000000]   node   0: [mem 0x0000000000000000-0x000000000fffffff]
[    0.000000]   node   0: [mem 0x0000000020000000-0x000000002fffffff]
[    0.000000] Initmem setup node 0 [mem 0x0000000000000000-0x000000002fffffff]
[    0.000000] On node 0, zone Normal: 131072 pages in unavailable ranges
[    0.000000] percpu: Embedded 18 pages/cpu s42000 r8192 d23536 u73728
[    0.000000] Kernel command line: earlycon console=ttyS2,115200 irqpoll
[    0.000000] Misrouted IRQ fixup and polling support enabled
[    0.000000] This may significantly impact system performance
[    0.000000] printk: log buffer data + meta data: 131072 + 409600 = 540672 bytes
[    0.000000] Dentry cache hash table entries: 32768 (order: 5, 131072 bytes, linear)
[    0.000000] Inode-cache hash table entries: 16384 (order: 4, 65536 bytes, linear)
[    0.000000] Built 1 zonelists, mobility grouping on.  Total pages: 65536
[    0.000000] mem auto-init: stack:all(zero), heap alloc:off, heap free:off
[    0.000000] SLUB: HWalign=128, Order=0-3, MinObjects=0, CPUs=2, Nodes=1
[    0.000000] ftrace: allocating 38592 entries in 76 pages
[    0.000000] ftrace: allocated 76 pages with 3 groups
[    0.000000] rcu: Hierarchical RCU implementation.
[    0.000000] rcu:     RCU event tracing is enabled.
[    0.000000] rcu:     RCU restricting CPUs from NR_CPUS=4 to nr_cpu_ids=2.
[    0.000000]     Rude variant of Tasks RCU enabled.
[    0.000000]     Tracing variant of Tasks RCU enabled.
[    0.000000] rcu: RCU calculated value of scheduler-enlistment delay is 25 jiffies.
[    0.000000] rcu: Adjusting geometry for rcu_fanout_leaf=16, nr_cpu_ids=2
[    0.000000] RCU Tasks Rude: Setting shift to 1 and lim to 1 rcu_task_cb_adjust=1 rcu_task_cpu_ids=2.
[    0.000000] NR_IRQS: 256
[    0.000000] rcu: srcu_init: Setting srcu_struct sizes based on contention.
[    0.000000] clocksource: jiffies: mask: 0xffffffff max_cycles: 0xffffffff, max_idle_ns: 7645041785100000 ns
[    0.000000] clocksource: MIPS: mask: 0xffffffff max_cycles: 0xffffffff, max_idle_ns: 5148176286 ns
[    0.000000] Console: colour dummy device 80x25
[    0.000000] sched_clock: 32 bits at 250 Hz, resolution 4000000ns, wraps every 8589934590000000ns
[    0.004000] Calibrating delay loop... 740.35 BogoMIPS (lpj=1480704)
[    0.040000] pid_max: default: 32768 minimum: 301
[    0.044000] Mount-cache hash table entries: 1024 (order: 0, 4096 bytes, linear)
[    0.048000] Mountpoint-cache hash table entries: 1024 (order: 0, 4096 bytes, linear)
[    0.052000] VFS: Finished mounting rootfs on nullfs
[    0.056000] rcu: Hierarchical SRCU implementation.
[    0.060000] rcu:     Max phase no-delay instances is 1000.
[    0.064000] Timer migration: 1 hierarchy levels; 8 children per group; 1 crossnode level
[    0.068000] smp: Bringing up secondary CPUs ...
[    0.072000] SMP: Booting CPU1...
[    0.080000] Primary instruction cache 32kB, VIPT, 2-way, linesize 64 bytes.
[    0.080000] Primary data cache 64kB, 4-way, VIPT, cache aliases, linesize 64 bytes
[    0.080000] CPU1 revision is: 0002a064 (Broadcom BMIPS4380)
[    0.080000] FPU revision is: 00130001
[    0.108000] Counter synchronization [CPU#0 -> CPU#1]: passed
[    0.108000] SMP: CPU1 is running
[    0.112000] smp: Brought up 1 node, 2 CPUs
[    0.116000] Memory: 232044K/262144K available (14492K kernel code, 1789K rwdata, 3132K rodata, 1312K init, 298K bss, 27580K reserved, 0K cma-reserved, 0K highmem)
[    0.120000] devtmpfs: initialized
[    0.124000] posixtimers hash table entries: 1024 (order: 1, 8192 bytes, linear)
[    0.128000] futex hash table entries: 512 (65536 bytes on 1 NUMA nodes, total 64 KiB, linear).
[    0.132000] NET: Registered PF_NETLINK/PF_ROUTE protocol family
[    0.136000] error mapping AON_CTRL
[    0.152000] SCSI subsystem initialized
[    0.160000] usbcore: registered new interface driver usbfs
[    0.164000] usbcore: registered new interface driver hub
[    0.172000] usbcore: registered new device driver usb
[    0.176000] pps_core: LinuxPPS API ver. 1 registered
[    0.180000] pps_core: Software ver. 5.3.6 - Copyright 2005-2007 Rodolfo Giometti <giometti@linux.it>
[    0.192000] PTP clock support registered
[    0.200000] vgaarb: loaded
[    0.200000] clocksource: Switched to clocksource MIPS
[    0.220000] NET: Registered PF_INET protocol family
[    0.224000] IP idents hash table entries: 4096 (order: 3, 32768 bytes, linear)
[    0.236000] tcp_listen_portaddr_hash hash table entries: 512 (order: 0, 4096 bytes, linear)
[    0.244000] Table-perturb hash table entries: 65536 (order: 6, 262144 bytes, linear)
[    0.252000] TCP established hash table entries: 2048 (order: 1, 8192 bytes, linear)
[    0.260000] TCP bind hash table entries: 2048 (order: 3, 32768 bytes, linear)
[    0.268000] TCP: Hash tables configured (established 2048 bind 2048)
[    0.276000] UDP hash table entries: 256 (order: 2, 14336 bytes, linear)
[    0.284000] NET: Registered PF_UNIX/PF_LOCAL protocol family
[    0.292000] RPC: Registered named UNIX socket transport module.
[    0.296000] RPC: Registered udp transport module.
[    0.304000] RPC: Registered tcp transport module.
[    0.308000] RPC: Registered tcp-with-tls transport module.
[    0.312000] RPC: Registered tcp NFSv4.1 backchannel transport module.
[    0.324000] PCI: CLS 0 bytes, default 64
[    0.328000] Initialise system trusted keyrings
[    0.340000] workingset: timestamp_bits=30 (anon: 25) max_order=16 bucket_order=0 (anon: 0)
[    0.356000] squashfs: version 4.0 (2009/01/31) Phillip Lougher
[    0.368000] NFS: Registering the id_resolver key type
[    0.372000] Key type id_resolver registered
[    0.380000] Key type id_legacy registered
[    0.388000] nfs4filelayout_init: NFSv4 File Layout Driver Registering...
[    0.396000] nfs4flexfilelayout_init: NFSv4 Flexfile Layout Driver Registering...
[    0.468000] Key type cifs.idmap registered
[    0.472000] jffs2: version 2.2. (NAND) © 2001-2006 Red Hat, Inc.
[    0.488000] fuse: init (API version 7.46)
[    0.496000] Key type asymmetric registered
[    0.504000] Asymmetric key parser 'x509' registered
[    0.512000] io scheduler mq-deadline registered
[    0.516000] io scheduler kyber registered
[    0.540000] io scheduler bfq registered
[    0.556000] irq_bcm7038_l1: registered BCM7038 L1 intc (/rdb/interrupt-controller@411400, IRQs: 96)
[    0.992000] Serial: 8250/16550 driver, 4 ports, IRQ sharing disabled
[    1.016000] 10406900.serial: ttyS0 MMIO32:0x10406900 (irq = 65, base_baud = 5062500) is a 16550A
[    1.044000] 10406940.serial: ttyS1 MMIO32:0x10406940 (irq = 66, base_baud = 5062500) is a 16550A
[    1.060000] 10406980.serial: ttyS2 MMIO32:0x10406980 (irq = 67, base_baud = 5062500) is a 16550A
[    1.068000] printk: console [ttyS2] enabled
[    1.068000] printk: console [ttyS2] enabled
[    1.080000] printk: legacy bootconsole [ns16550a0] disabled
[    1.080000] printk: legacy bootconsole [ns16550a0] disabled
[    1.128000] bcmgenet 10430000.ethernet: GENET 2.9 EPHY: 0x00b0
[    1.128000] bcmgenet 10430000.ethernet: using random Ethernet MAC
[    1.172000] unimac-mdio unimac-mdio.-19: Broadcom UniMAC MDIO bus
[    1.172000] usbcore: registered new interface driver asix
[    1.172000] usbcore: registered new interface driver ax88179_178a
[    1.172000] usbcore: registered new interface driver cdc_ether
[    1.172000] usbcore: registered new interface driver net1080
[    1.172000] usbcore: registered new interface driver cdc_subset
[    1.172000] usbcore: registered new interface driver zaurus
[    1.172000] usbcore: registered new interface driver cdc_ncm
[    1.172000] usbcore: registered new interface driver r8153_ecm
[    1.172000] usbcore: registered new interface driver usb-storage
[    1.172000] ehci-platform 10480500.usb: EHCI Host Controller
[    1.172000] ehci-platform 10480500.usb: new USB bus registered, assigned bus number 1
[    1.188000] ehci-platform 10480300.usb: EHCI Host Controller
[    1.188000] ehci-platform 10480300.usb: new USB bus registered, assigned bus number 2
[    1.188000] usbcore: registered new interface driver usbhid
[    1.188000] usbhid: USB HID core driver
[    1.192000] NET: Registered PF_PACKET protocol family
[    1.192000] bridge: filtering via arp/ip/ip6tables is no longer available by default. Update your scripts to load br_netfilter if you need this.
[    1.192000] 8021q: 802.1Q VLAN Support v1.8
[    1.192000] Key type dns_resolver registered
[    1.192000] ohci-platform 10480400.usb: Generic Platform OHCI controller
[    1.192000] ehci-platform 10480500.usb: irq 70, io mem 0x10480500
[    1.192000] ohci-platform 10480400.usb: new USB bus registered, assigned bus number 3
[    1.192000] ohci-platform 10480400.usb: irq 71, io mem 0x10480400
[    1.204000] ehci-platform 10480500.usb: USB 2.0 started, EHCI 1.00
[    1.224000] ehci-platform 10480300.usb: irq 69, io mem 0x10480300
[    1.236000] ohci-platform 10480600.usb: Generic Platform OHCI controller
[    1.236000] ohci-platform 10480600.usb: new USB bus registered, assigned bus number 4
[    1.236000] ohci-platform 10480600.usb: irq 72, io mem 0x10480600
[    1.236000] hub 1-0:1.0: USB hub found
[    1.236000] hub 1-0:1.0: 1 port detected
[    1.252000] ehci-platform 10480300.usb: USB 2.0 started, EHCI 1.00
[    1.256000] Loading compiled-in X.509 certificates
[    1.264000] hub 2-0:1.0: USB hub found
[    1.264000] hub 2-0:1.0: 1 port detected
[    1.280000] mmc0: Hardware doesn't report any support voltages.
[    1.280000] cfg80211: Loading compiled-in X.509 certificates for regulatory database
[    1.368000] Loaded X.509 cert 'sforshee: 00b28ddf47aef9cea7'
[    1.372000] Loaded X.509 cert 'wens: 61c038651aabdcf94bd0ac7ff06c7248db18c600'
[    1.372000] faux_driver regulatory: Direct firmware load for regulatory.db failed with error -2
[    1.372000] cfg80211: failed to load regulatory.db
[    1.440000] hub 4-0:1.0: USB hub found
[    1.440000] hub 4-0:1.0: 1 port detected
[    1.440000] hub 3-0:1.0: USB hub found
[    1.440000] hub 3-0:1.0: 1 port detected
[    1.688000] usb 2-1: new high-speed USB device number 2 using ehci-platform
[    2.768000] usb-storage 2-1:1.0: USB Mass Storage device detected
[    2.768000] scsi host0: usb-storage 2-1:1.0
[    2.768000] clk: Disabling unused clocks
[    2.828000] Freeing unused kernel image (initmem) memory: 1312K
[    2.828000] This architecture does not have kernel memory protection.
[    2.828000] Run /init as init process
================================[    4.204000] scsi 0:0:0:0: Direct-Access     General  UDisk            5.00 PQ: 0 ANSI: 2
[    4.204000] sd 0:0:0:0: Attached scsi generic sg0 type 0
==================
 SML-482 HD Base - mainline Linux 7.3.1 init[    4.908000] sd 0:0:0:0: [sda] 15728640 512-byte logical blocks: (8.05 GB/7.50 GiB)
ramfs
=========================================[    5.112000] sd 0:0:0:0: [sda] Write Protect is off
=========
[    5.312000] sd 0:0:0:0: [sda] No Caching mode page found
[    5.312000] sd 0:0:0:0: [sda] Assuming drive cache: write through
[    7.436000]  sda: sda1
[    7.436000] sd 0:0:0:0: [sda] Attached SCSI removable disk
[    9.356000] FAT-fs (sda1): Volume was not properly unmounted. Some data may be corrupt. Please run fsck.
[init] stick mounted on /mnt1
[init] found Gentoo stage3, setting up loop ...
[init] creating 3G gentoo.img ...
[   32.992000] random: crng init done
```

</details>

## Mainline Kernel loading (or anything else)
To interrupt the default boot sequence and access the CFE bootloader prompt, connect to the onboard UART (`115200 8N1`) and spam `Ctrl+C` right after powering on the STB:

```text
BCM72300010
CFE initialized.
...
*** Automatic startup canceled via Ctrl-C ***
CFE>
```

From the `CFE>` prompt, you can boot a custom kernel over TFTP or from a USB flash drive:

```text
# Booting from USB (FAT32)
CFE> boot -elf -z usbdisk0:vmlinux.gz

# Or booting over TFTP
CFE> ifconfig eth0 -auto
CFE> boot -elf -z 192.168.X.XXX:vmlinux.gz
```

## After kernel boot
Currently, the mainline kernel boots from USB and initializes a basic Gentoo stage3 rootfs. Next steps and ongoing tasks:

- **Reverse-Engineering (Stock Linux 3.10 & Broadcom Nexus API):** ~5% done. Nexus API revealed details about hardware blocks in this STB, such as hardware DRM, HDMI CEC, and a 3D accelerator (VideoCore IV — the same architecture as in the early Raspberry Pi, so 3D acceleration might work in the future).

The main problem is the Nexus API itself, not booting the mainline kernel. It has too many abstraction layers and spaghetti code.. 

## Known Issues

- **Second RAM bank ignored (`256 MiB` of `512 MiB` usable):** The upper memory bank (`0x20000000`–`0x2fffffff`, 256 MiB) is currently ignored because `HIGHMEM` is not supported on this BMIPS4380 configuration (`This processor doesn't support highmem. 262144k highmem ignored`).
- **Missing `reserved-memory` node:** The Device Tree does not yet define a `reserved-memory` region (`No reserved-memory node in the DT`).
- **`AON_CTRL` mapping error:** Early boot logs show `error mapping AON_CTRL` during platform initialization.
- **`irqpoll` workaround in cmdline:** Currently booting with `irqpoll` in `bootargs` (`Misrouted IRQ fixup and polling support enabled`), which impacts interrupt performance until IRQ routing is finalized.
- **Random Ethernet MAC address:** `bcmgenet` currently assigns a random MAC address on boot instead of reading the factory MAC from CFE / NVMEM.

