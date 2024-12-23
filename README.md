# Some Footnotes for Proxmox setup.

### Config Serial Terminal under Proxmox 8 for Debian 12
Ref:  https://pve.proxmox.com/wiki/Serial_Terminal

1. At "Proxmox Node Shell", add serial 
`$ qm set <vmid> -serial0 socket`

or from GUI, 
`Hardware > Add > Serial Port > "0"`

2. Under VM Console

- check /dev/ttyS0 exists
- update grub
    $ vi /etc/default/grub

    add:
      GRUB_TERMINAL="console serial" <br/>
      GRUB_SERIAL_COMMAND="serial --speed=115200"

    update this line  
      # GRUB_CMDLINE_LINUX="" <br/>
      GRUB_CMDLINE_LINUX="quiet console=tty0 console=ttyS0,115200"

    After that, update grub setting
      $ update-grub


`$ npm install marked`


### Workaround for installer hang with newer hardward
Ref:  
[Proxmox Kernel 6.8.12-2 Freezes (again)](https://forum.proxmox.com/threads/proxmox-kernel-6-8-12-2-freezes-again.154875/) 
https://www.thomas-krenn.com/de/wiki/Known_Issues_Proxmox_VE_8.2#

0. Update CPU Microcode 
https://tteck.github.io/Proxmox/#proxmox-ve-processor-microcode

1. Add nomodeset at kernel /etc/kernel/cmdline 
root=ZFS=rpool/ROOT/pve-1 boot=zfs nomodeset intel_iommu=on iommu=pt pcie_acs_override=downstream,multifunction pcie_port_pm=off libata.force=noncq consoleblank=0 nox2apic

2. Refresh the boot tool

After editing the /etc/kernel/cmdline file, refresh the boot tool by running:

proxmox-boot-tool refresh
update-initramfs -k all -u

### Workaround for installer hang with newer hardward
Ref: 
https://forum.proxmox.com/threads/simple-working-gpu-passthrough-on-uptodate-pve-and-amd-hardware.145462/


### Thunderbolt Networking for Proxmox
Reference: 
ProxMox Cluster - Soup-to-Nutz
https://gist.github.com/scyto/76e94832927a89d977ea989da157e9dc


Networking over Thunderbolt cable
https://docs.kernel.org/admin-guide/thunderbolt.html
It is possible to tunnel any kind of traffic over a Thunderbolt link but currently we only support Apple ThunderboltIP protocol.

If the other host is running Windows or macOS, the only thing you need to do is to connect a Thunderbolt cable between the two hosts; the thunderbolt-net driver is loaded automatically. If the other host is also Linux you should load thunderbolt-net manually on one host (it does not matter which one):

# modprobe thunderbolt-net
This triggers module load on the other host automatically. If the driver is built-in to the kernel image, there is no need to do anything.

The driver will create one virtual ethernet interface per Thunderbolt port which are named like thunderbolt0 and so on. From this point you can either use standard userspace tools like ifconfig to configure the interface or let your GUI handle it automatically.




Rename Thunderbolt port
https://gist.github.com/scyto/67fdc9a517faefa68f730f82d7fa3570


https://forum.proxmox.com/threads/networking-via-thunderbolt.141027/

