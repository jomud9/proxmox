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



