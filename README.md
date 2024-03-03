# dhqemu

    ▄▄▌ ▐ ▄▌ ▄ .▄▄▄▄ . ▐ ▄ • ▌ ▄ ·.              ▐ ▄ 
    ██· █▌▐███▪▐█▀▄.▀·•█▌▐█·██ ▐███▪▪     ▪     •█▌▐█
    ██▪▐█▐▐▌██▀▐█▐▀▀▪▄▐█▐▐▌▐█ ▌▐▌▐█· ▄█▀▄  ▄█▀▄ ▐█▐▐▌
    ▐█▌██▐█▌██▌▐▀▐█▄▄▌██▐█▌██ ██▌▐█▌▐█▌.▐▌▐█▌.▐▌██▐█▌
     ▀▀▀▀ ▀▪▀▀▀ · ▀▀▀ ▀▀ █▪▀▀  █▪▀▀▀ ▀█▄▀▪ ▀█▄▀▪▀▀ █▪

              Cryptocurrency Trading Bot
  ·▄▄▄▄         ▄▄·  ▄ .▄ ▄▄▄· ▄▄▄▄▄
  ██▪ ██ ▪     ▐█ ▌▪██▪▐█▐█ ▀█ •██
  ▐█· ▐█▌ ▄█▀▄ ██ ▄▄██▀▐█▄█▀▀█  ▐█.▪
  ██. ██ ▐█▌.▐▌▐███▌██▌▐▀▐█ ▪▐▌ ▐█▌·
  ▀▀▀▀▀•  ▀█▄▀▪·▀▀▀ ▀▀▀ · ▀  ▀  ▀▀▀

     Written by George Shearer (george@shearer.tech)
  ·▄▄▄▄         ▄▄·  ▄ .▄ ▄▄▄· ▄▄▄▄▄
  ██▪ ██ ▪     ▐█ ▌▪██▪▐█▐█ ▀█ •██
  ▐█· ▐█▌ ▄█▀▄ ██ ▄▄██▀▐█▄█▀▀█  ▐█.▪
  ██. ██ ▐█▌.▐▌▐███▌██▌▐▀▐█ ▪▐▌ ▐█▌·
  ▀▀▀▀▀•  ▀█▄▀▪·▀▀▀ ▀▀▀ · ▀  ▀  ▀▀▀
     Written by George Shearer (george@shearer.tech)

DHQEMU - Thin hypervisor implemented with #!/bin/bash


Hello!
------

This is a thin hypervisor written in bash. It directly invokes QEMU with KVM features.

Features:

* simple command line
* implementd completely in bash - nothing resident
* global and per-guest config
* automatic adjustment of kernel hugepages
* automatic start/stop of TPM emulater daemon
* automatic creation of base vdisks and snapshot files
* Uses io_uring for vdisk I/O
* delayed commits of changes
* snapshot reverting
* hotplug usb devices
* systemd integration for stopping or starting vms with system
* simple one file backups of all necessary files for each VM

·▄▄▄▄         ▄▄·  ▄ .▄ ▄▄▄· ▄▄▄▄▄
██▪ ██ ▪     ▐█ ▌▪██▪▐█▐█ ▀█ •██  
▐█· ▐█▌ ▄█▀▄ ██ ▄▄██▀▐█▄█▀▀█  ▐█.▪
██. ██ ▐█▌.▐▌▐███▌██▌▐▀▐█ ▪▐▌ ▐█▌·
▀▀▀▀▀•  ▀█▄▀▪·▀▀▀ ▀▀▀ · ▀  ▀  ▀▀▀ 

   DHQEMU Version: 2024030101

    Written by George Shearer
       george@shearer.tech


Usage: dhqemu command guestname [args]

Where command is one of:

  boot     :: power on guest
  bootall  :: boot all guests defined to auto-start
  iceboot  :: power on guest but in cpu suspend mode (see thaw below)
  reset    :: issue qemu 'system_reset'
  wake     :: issue qemu 'system_wakeup'
  shut     :: issue qemu 'system_powerdown'
  shutall  :: shutdown all guests managed by dhqemu
  kill     :: immediately power off guest
  killall  :: kill all guests managed by dhqemu
  freeze   :: stop execution
  thaw     :: continue execution
  mon      :: connect to qemu monitor
  list     :: list of dhqemu conf files
  dir      :: show folder of guest
  pid      :: shows list of running qemu instances
  show     :: shows the qemu command line used to boot VM
  backup   :: create backup archive of guest directory
  delete   :: delete the guest folder, next boot will generate files
  unplug   :: unplug device created with'plug' command

commands with args:
  clone  guestname newname             :: create new vm
  plug   guestname /path/to/cdrom.iso  :: hot-plug usb drive, map to file
  commit guestname [disknum]           :: commit change disk
  revert guestname [disknum]           :: erase change disk and recreate
  erase  guestname [disknum]           :: erase base disk and recreate

