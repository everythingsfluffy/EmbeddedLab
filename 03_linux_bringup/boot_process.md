### Log part

### What happened

### What component produced message

### Why it happened

### What if it fails 

### Log part
[    0.000000] Booting Linux on physical CPU 0x0
[    0.000000] Linux version 6.18.34+rpt-rpi-v6 (serge@raspberrypi.com) (arm-linux-gnueabihf-gcc-14 (Raspbian 14.2.0-19+rpi1) 14.2.0, GNU ld (GNU Binutils for Raspbian) 2.44) #1 Raspbian 1:6.18.34-1+rpt1 (2026-06-09)
[    0.000000] CPU: ARMv6-compatible processor [410fb767] revision 7 (ARMv7), cr=00c5387d
[    0.000000] CPU: PIPT / VIPT nonaliasing data cache, VIPT nonaliasing instruction cache
[    0.000000] OF: fdt: Machine model: Raspberry Pi Zero W Rev 1.1
[    0.000000] random: crng init done
[    0.000000] Memory policy: Data cache writeback
[    0.000000] Reserved memory: created CMA memory pool at 0x0b000000, size 256 MiB
[    0.000000] OF: reserved mem: initialized node linux,cma, compatible id shared-dma-pool
[    0.000000] OF: reserved mem: 0x0b000000..0x1affffff (262144 KiB) map reusable linux,cma


### What happened?
Started booting  (kernel version 6.18.34) at physical CPU 0x0 
Detected CPU (ARMv6 compatibl)
TODO: understand CPU cache PIPT/VIPT later
Detected RPI model (Zero W)
TODO: Device Tree / FDT
random: crng init done - Kernel cryptographic random number generator 
Reserved memory part for CMA
TODO: CMA 
### What component produced message
Kernel

### Why it happened
Linux Kernel found the hardware and starting initialization of CPU memory etc 

### What if it fails?
No boot, may show kernel panic


### Log Part
[    0.000000] Zone ranges:
[    0.000000]   Normal   [mem 0x0000000000000000-0x000000001bffffff]
[    0.000000] Movable zone start for each node
[    0.000000] Early memory node ranges
[    0.000000]   node   0: [mem 0x0000000000000000-0x000000001bffffff]
[    0.000000] Initmem setup node 0 [mem 0x0000000000000000-0x000000001bffffff]
[    0.000000] Kernel command line: coherent_pool=1M 8250.nr_uarts=1 snd_bcm2835.enable_headphones=0 cgroup_disable=memory snd_bcm2835.enable_hdmi=1 snd_bcm2835.enable_hdmi=0  smsc95xx.macaddr=B8:
vc_mem.mem_base=0x1ec00000 vc_mem.mem_size=0x20000000  console=ttyS0,115200 console=tty1 root=PARTUUID=25b814e8-02 rootfstype=ext4 fsck.repair=yes rootwait modules-load=dwc2,g_ether console=ttyS0,115200 ds=nocloud;i=rpi-imager-1784572696173 cfg80211.ieee80211_regdom=PL
[    0.000000] cgroup: Disabling memory control group subsystem
[    0.000000] Unknown kernel command line parameters "modules-load=dwc2,g_ether ds=nocloud;i=rpi-imager-1784572696173", will be passed to user space.
[    0.000000] printk: log buffer data + meta data: 131072 + 409600 = 540672 bytes
[    0.000000] Dentry cache hash table entries: 32768 (order: 5, 131072 bytes, linear)
[    0.000000] Inode-cache hash table entries: 16384 (order: 4, 65536 bytes, linear)
[    0.000000] Built 1 zonelists, mobility grouping on.  Total pages: 114688

### What happened

Kernel initialized initial memory ranges 

TODO:
- Linux memory zones
- NUMA nodes

Kernel received and parsed its command line.
coherent_pool - set for 1MiB 
Sets the initial coherent DMA memory pool size to 1 MiB.
TODO: DMA / coherent DMA

Configured the 8250/16550 serial driver for one UART.

Disabled headphones on snd_bcm2835
cgroup_disable=memory (?)
enabled hdmi
disabled hdmi (second one or previously enabled?)
TODO:
- Why is snd_bcm2835.enable_hdmi specified twice with different values?
- Which value is actually used?

set  mac address

Disabled memory control group subsystem (from cgroup_disable command)
TODO:
- cgroups
Not recognized parameters modules-load, g_ether and i= rpi imager
NOTE:
KERNEL SPACE = Kernel level operations and components
USERSPACE = Processes "over" kernel  
TODO: printk / kernel ring buffer / dmesg
Kernel initializes filesystem-related caches.

TODO:
- inode
- dentry
### What component produced message
Kernel
### Why it happened
Memory needs to be initialized , then reads initial boot commands (like hardwarer setup or uart enable)
### What if it fails 
Failure of critical early memory initialization may prevent the kernel from continuing boot and can result in a kernel panic.
Commands - sent to user space 


### Log part
 0.000793] Console: colour dummy device 80x30
[    0.000828] printk: legacy console [tty1] enabled
[    0.001439] Calibrating delay loop... 996.14 BogoMIPS (lpj=4980736)
[    0.040236] CPU: Testing write buffer coherency: ok
[    0.040332] pid_max: default: 32768 minimum: 301
[    0.040519] LSM: initializing lsm=capability
[    0.040835] Mount-cache hash table entries: 1024 (order: 0, 4096 bytes, linear)
[    0.040899] Mountpoint-cache hash table entries: 1024 (order: 0, 4096 bytes, linear)
[    0.044510] Setting up static identity map for 0x8240 - 0x8278
[    0.045323] Memory: 158864K/458752K available (10900K kernel code, 1617K rwdata, 3540K rodata, 492K init, 329K bss, 35984K reserved, 262144K cma-reserved)
[    0.046203] devtmpfs: initialized
[    0.056331] VFP support v0.3: implementor 41 architecture 1 part 20 variant b rev 5
[    0.057199] clocksource: jiffies: mask: 0xffffffff max_cycles: 0xffffffff, max_idle_ns: 19112604462750000 ns
[    0.057380] posixtimers hash table entries: 512 (order: 0, 2048 bytes, linear)
[    0.057452] futex hash table entries: 256 (4096 bytes on 1 NUMA nodes, total 4 KiB, linear).
[    0.074426] pinctrl core: initialized pinctrl subsystem
[    0.076157] NET: Registered PF_NETLINK/PF_ROUTE protocol family
[    0.078389] DMA: preallocated 1024 KiB pool for atomic coherent allocations
[    0.082980] audit: initializing netlink subsys (disabled)
[    0.084309] thermal_sys: Registered thermal governor 'step_wise'
[    0.084667] hw-breakpoint: found 6 breakpoint and 1 watchpoint registers.
[    0.084751] hw-breakpoint: maximum watchpoint size is 4 bytes.
[    0.085111] Serial: AMBA PL011 UART driver
[    0.090569] audit: type=2000 audit(0.080:1): state=initialized audit_enabled=0 res=1
[    0.093076] bcm2835-mbox 2000b880.mailbox: mailbox enabled
[    0.110608] raspberrypi-firmware soc:firmware: Attached to firmware from 2026-05-21T11:21:57, variant start
[    0.120636] raspberrypi-firmware soc:firmware: Firmware hash is 288930ab4712b99596f32732664aaaeb881ef1e0
[    0.135332] kprobes: kprobe jump-optimization is enabled. All kprobes are optimized if possible.
[    0.151908] bcm2835-dma 20007000.dma-controller: DMA legacy API manager, dmachans=0x1
### What happened
Enabled virtual console (tty1 old ass simple full screen console)
TODO:
- Linux console vs TTY
- virtual console
CPU tested
TODO: BogoMIPS / delay loop
Cheked available memory
NOTE:
256 MiB is reserved for CMA, which matches the earlier CMA initialization.
TODO: why is CMA reservation so large?
ran devtmpfs (dev temporary file system?)
TODO:
- devtmpfs
- device nodes
- relationship between devtmpfs and udev
thermal_sys - handling thermal protection? 
Serial - UART driver enabled
bcm2835 mailbox - Communication between ARM and GPU VideoCore
TODO:
-BCM2835 Mailbox

 firmware attached
 DMA subsystem allocated memory and the BCM2835 DMA controller
driver was initialized.

TODO:
- DMA
- DMA controller
- coherent DMA
### What component produced message
Kernel
### Why it happened
kernel enables it's subsystems and hardware drivers
### What if it fails 
No correct boot (may), some devices/elements may not work


### Log part
[    0.154012] SCSI subsystem initialized
[    0.154445] usbcore: registered new interface driver usbfs
[    0.154576] usbcore: registered new interface driver hub
[    0.154688] usbcore: registered new device driver usb
[    0.155342] pps_core: LinuxPPS API ver. 1 registered
[    0.155401] pps_core: Software ver. 5.3.6 - Copyright 2005-2007 Rodolfo Giometti <giometti@linux.it>
[    0.155468] PTP clock support registered
[    0.157848] clocksource: Switched to clocksource timer
[    0.158963] VFS: Disk quotas dquot_6.6.0
[    0.159095] VFS: Dquot-cache hash table entries: 1024 (order 0, 4096 bytes)
[    0.198217] NET: Registered PF_INET protocol family
[    0.198560] IP idents hash table entries: 4096 (order: 3, 32768 bytes, linear)
[    0.199888] tcp_listen_portaddr_hash hash table entries: 1024 (order: 0, 4096 bytes, linear)
[    0.199984] Table-perturb hash table entries: 65536 (order: 6, 262144 bytes, linear)
[    0.200039] TCP established hash table entries: 2048 (order: 1, 8192 bytes, linear)
[    0.200107] TCP bind hash table entries: 2048 (order: 2, 16384 bytes, linear)
[    0.200182] TCP: Hash tables configured (established 2048 bind 2048)
[    0.200331] UDP hash table entries: 256 (order: 1, 8192 bytes, linear)
[    0.200407] UDP-Lite hash table entries: 256 (order: 1, 8192 bytes, linear)
[    0.200751] NET: Registered PF_UNIX/PF_LOCAL protocol family
[    0.208937] RPC: Registered named UNIX socket transport module.
[    0.209016] RPC: Registered udp transport module.
[    0.209045] RPC: Registered tcp transport module.
[    0.209070] RPC: Registered tcp-with-tls transport module.
[    0.209095] RPC: Registered tcp NFSv4.1 backchannel transport module.
[    0.212624] Trying to unpack rootfs image as initramfs...
[    3.542726] Initialise system trusted keyrings
[    3.544252] workingset: timestamp_bits=14 max_order=17 bucket_order=3
[    3.545818] NFS: Registering the id_resolver key type
[    3.545923] Key type id_resolver registered
[    3.545956] Key type id_legacy registered[    0.154012] SCSI subsystem initialized
[    0.154445] usbcore: registered new interface driver usbfs
[    0.154576] usbcore: registered new interface driver hub
[    0.154688] usbcore: registered new device driver usb
[    0.155342] pps_core: LinuxPPS API ver. 1 registered
[    0.155401] pps_core: Software ver. 5.3.6 - Copyright 2005-2007 Rodolfo Giometti <giometti@linux.it>
[    0.155468] PTP clock support registered
[    0.157848] clocksource: Switched to clocksource timer
[    0.158963] VFS: Disk quotas dquot_6.6.0
[    0.159095] VFS: Dquot-cache hash table entries: 1024 (order 0, 4096 bytes)
[    0.198217] NET: Registered PF_INET protocol family
[    0.198560] IP idents hash table entries: 4096 (order: 3, 32768 bytes, linear)
[    0.199888] tcp_listen_portaddr_hash hash table entries: 1024 (order: 0, 4096 bytes, linear)
[    0.199984] Table-perturb hash table entries: 65536 (order: 6, 262144 bytes, linear)
[    0.200039] TCP established hash table entries: 2048 (order: 1, 8192 bytes, linear)
[    0.200107] TCP bind hash table entries: 2048 (order: 2, 16384 bytes, linear)
[    0.200182] TCP: Hash tables configured (established 2048 bind 2048)
[    0.200331] UDP hash table entries: 256 (order: 1, 8192 bytes, linear)
[    0.200407] UDP-Lite hash table entries: 256 (order: 1, 8192 bytes, linear)
[    0.200751] NET: Registered PF_UNIX/PF_LOCAL protocol family
[    0.208937] RPC: Registered named UNIX socket transport module.
[    0.209016] RPC: Registered udp transport module.
[    0.209045] RPC: Registered tcp transport module.
[    0.209070] RPC: Registered tcp-with-tls transport module.
[    0.209095] RPC: Registered tcp NFSv4.1 backchannel transport module.
[    0.212624] Trying to unpack rootfs image as initramfs...
[    3.542726] Initialise system trusted keyrings
[    3.544252] workingset: timestamp_bits=14 max_order=17 bucket_order=3
[    3.545818] NFS: Registering the id_resolver key type
[    3.545923] Key type id_resolver registered
[    3.545956] Key type id_legacy registered
[    3.546043] nfs4filelayout_init: NFSv4 File Layout Driver Registering...
[    3.546086] nfs4flexfilelayout_init: NFSv4 Flexfile Layout Driver Registering...
[    3.547493] Key type asymmetric registered
[    3.547572] Asymmetric key parser 'x509' registered
[    3.546043] nfs4filelayout_init: NFSv4 File Layout Driver Registering...
[    3.546086] nfs4flexfilelayout_init: NFSv4 Flexfile Layout Driver Registering...
[    3.547493] Key type asymmetric registered
[    3.547572] Asymmetric key parser 'x509' registered
### What happened
SCSI initialized 
TODO:
- SCSI subsystem
- why Linux uses SCSI layer for many storage devices
USBFS - virtual filesystem driver for usb devices initialized
driver hub - many usb devices into one port
TODO:
- usbcore
- usbfs
- USB hub driver
Old Italian Pulse System initialized xD

TODO:
- PPS
- PTP
Network stack initialized (UDP TCP ETC)
TODO:
- protocol families
- PF_INET
- PF_UNIX
- sockets
- RPC
- NFS
rootfs image into ram before it's fully initialized
keyrings (secure boot?) passwords, certificates? 
TODO:
- kernel keyrings
- X.509 certificates
- what uses kernel trusted keys?
### What component produced message
Kernel
### Why it happened
Further initialization, prepairing for initial actual system boot (prepairing network stash, root file system)
### What if it fails 
Boot issues, network errors , usb issues - for initramfs potential oreo