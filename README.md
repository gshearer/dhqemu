# dhqemu

<pre>
·▄▄▄▄         ▄▄·  ▄ .▄ ▄▄▄· ▄▄▄▄▄
██▪ ██ ▪     ▐█ ▌▪██▪▐█▐█ ▀█ •██  
▐█· ▐█▌ ▄█▀▄ ██ ▄▄██▀▐█▄█▀▀█  ▐█.▪
██. ██ ▐█▌.▐▌▐███▌██▌▐▀▐█ ▪▐▌ ▐█▌·
▀▀▀▀▀•  ▀█▄▀▪·▀▀▀ ▀▀▀ · ▀  ▀  ▀▀▀ 

   DHQEMU Version: 2026010201

    Written by George Shearer
       george@shearer.tech
</pre>

## About

This is a thin "hypervisor" written in bash. It directly invokes QEMU with KVM features.

Features:

* simple command line
* supports XDG pathing ($XDG_CONFIG_HOME, etc)
* implementd completely in bash
* global and per-guest config
* automated adjustment of kernel hugepages
* automated start/stop of TPM emulater daemon
* automated creation of base vdisks and snapshot files
* automated creation of network device taps and bridge mapping
* Uses io_uring for vdisk I/O
* delayed commits of changes
* snapshot reverting
* hotplug host usb devices and local file mapping
* systemd integration for stopping or starting vms with system
* simple one file backups of all necessary files for each VM

## Usage

<pre>
Where command is one of:

  boot      :: power on guest
  bootall   :: boot all dhqemu guests with bootall=true
  iceboot   :: power on guest but in cpu suspend mode
  reset     :: issue qemu 'system_reset'
  wake      :: issue qemu 'system_wakeup'
  shut      :: attempt graceful shutdown
  shutall   :: attempt graceful shutdown for all dhqemu guests
  kill      :: immediately power off guest
  killall   :: immediately power off all dhqemu guests
  freeze    :: suspend execution
  thaw      :: continue execution
  mon       :: connect to qemu monitor
  list      :: list of dhqemu guests
  dir       :: show folder of guest
  pid       :: shows list of running qemu instances
  show      :: shows the qemu command line used to boot VM
  backup    :: create backup archive of guest directory
  delete    :: delete the guest folder, next boot will generate files
  unmap     :: unmap file to usb-disk
  unplug    :: unplug virtual usb device created with 'plug'

commands with args:
  clone   guestname newname    :: create new vm
  commit  guestname [disknum]  :: commit change disk
  revert  guestname [disknum]  :: erase change disk and recreate
  erase   guestname [disknum]  :: erase base disk and recreate
  map     guestname /path/to/example.iso    :: map a local file to vm usb disk
  plug    guestname hostbus hostdev [vmbus] :: 'plug' a local usb dev to vm usb bus

Note: Use the 'lsusb' command to find hostbus and hostdev for use with the plug command. Don't include the 0 padding. The third argument (vmbus) is defined in your guest's configuration. This defaults to usb.0 if not specified.
</pre>
