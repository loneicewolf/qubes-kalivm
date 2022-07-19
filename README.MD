# kali vm on qubes
- overview of the non-vm: (Qubes with UEFI, encryption+nuke key)
- overview of the VM BIOS, not encryption/nuke, Install -> Manual disk part{`LVM.`}

- todo: :warning: check and verify correctness.




- ☢️ NOTE - this might Be out of date, inaccurate, wrong, questionable, and so on. this is because, again - this is intended for myself.





### In VMWARE:

1. File 
2. create a new virtual machine
3. I will install the Operating System later
4. Linux
5. Version: Custom debian 11.x 64bit
6. Name`[v3]` and Location`[/VMS_PART/v3]`
7. Disk: `108.000 GB`, `SINGLE FILE`
8. Customize
9. 4GB RAM
10. 2 CPUS
11. CD/ISO: use iso `kali-linux-2022.2-installer-amd64.iso`
12. REMOVE: `sound` and `printer`
13. USB: `harden and tweak it`
14. CLOSE & FINISH
15. Go to the VM settings -> `defrag it and compact it` then POWER ON.
16. `-----` First Boot `-----`
17. `bios` ->  Install. (Not gui)
18. ENGLISH
19. UNITED STATES
20. AMERICAN ENGLISH
21. `-----` Network `-----`
22. hostname  : SOMEHOSTNAME
23. domainname: SOMEDOMAINNAME
24. `-----` user, pasword, groups `-----`
25. full name: SOME FULL NAME
26. username:  SOME USERNAME
27. password:  SOME LONG PASSWORD
28. timezone:  SOME TIMEZONE
29. `-----` Disk Partitioning `-----`
30. LAYOUT: not uefi, not crypto, we will have 2 partitions in total:
31. p1: `1G boot /boot, bootflag on.`
32. p2: `remaining space /`
33. we will on p2 setup LVM and make 3 LV's as: (1,2,3 in not in any particular order): `1swap:8GB` , `2root:remain space After LVS:{swap,home} has been made` , `3:home ~39GB.`
34. (...)
37. Finish & Continue
38. back to the partitions and disks view, one by one, set 'use as', and set mount points; options and such.
39. Complete, Write it, `Y`
40. When it comes to asking about APT, PROXY and maybe MEDIA/CDROMS:
41. choose **`absolutely NOTHING`**. This is VERY Important. choose NOTHING. no tools,no GUI, nothing. We don't want a bloated system.
42. Okay, choose the GRUB manually, and we're done.
43. `-----` **First Boot** `-----`

```sh
# as USER, in the Terminal (no gui)
# this is only done in the FIRST BOOT; dont copy these to a startup file. we e.g dont want to 
# remove ssh(might have apps that dep. on it) and install lxde(we already have it afterwards) reboot:(`..`) 
# this is why I comment these out. do them 1 time, manually.
#-heads up-# LATER IN THE FUTURE WE WILL KEEP OPENSSH NETCAT ETC. since TOOLS MIGHT DEPEND ON THEM

kali-tweaks (user)
-   terminal,harden,no packages,VM

then

##  sudo apt clean && sudo apt autoclean && sudo apt autoremove && sudo apt autopurge
### some of the below will Kinda fail because we haven't installed lxde yet. 
### sudo apt update && sudo apt remove firefox-esr  && sudo apt autoremove 
##  sudo apt autoremove
##  sudo apt update && sudo apt remove  netcat* openssh-*  audacious* mpv smplayer* parcellite
##  sudo apt autoremove
### reboot
##  sudo apt update && sudo apt-get install upgrade-system && sudo apt upgrade && sudo apt full-upgrade && sudo apt-get dist-upgrade && sudo apt autoremove
### reboot
## sudo apt update && sudo apt install kali-desktop-lxde
### reboot
##  sudo apt remove audacious* mpv smplayer* parcellite firefox-esr  
### reboot 1 last time to be sure
```

## GUI POST INSTALL

```sh

## make a file called FULL_APT.sh
# note: (no sudo (...))

apt update
apt dist-upgrade
apt full-upgrade
apt upgrade
apt-get install upgrade-system

## Then go to DOTFILES
# https://github.com/loneicewolf/DotFiles
## and set that up.

```


- :warning: todo:  `v2` -> `v3`








