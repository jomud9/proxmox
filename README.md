Some Footnotes for proxmox setup.

1. Config Serial Terminal under Proxmox 8 for Debian 12
   https://pve.proxmox.com/wiki/Serial_Terminal

1. At "Proxmox Node Shell", add serial 
qm set <vmid> -serial0 socket

or from GUI, Hardware > Add > Serial Port > "0"

2. Under VM Console

a. check /dev/ttyS0 exists
b. update grub
   cmd>: vi /etc/default/grub
     
   GRUB_CMDLINE_LINUX="quiet console=tty0 console=ttyS0,115200" 

   cmd> update-grub
