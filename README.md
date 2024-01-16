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
    
    update this line  
    GRUB_CMDLINE_LINUX="quiet console=tty0 console=ttyS0,115200"
    After that, update grub setting
    $ update-grub


`$ npm install marked`
