+++
title = "Comment mettre une IP fixe/dynamique sur Linux"
description = "IP statique ou IP DHCP ?"
author = "Hugo Grosot"
date = "2020-11-09"
tags = ["ip", "linux", "tips"]
categories = ["linux"]
[[images]]
  src = "/img/2020/11/linux_ip_static_dynamic/linux_ip_static_dynamic.png"
  alt = "cheatsheet bash"
  stretch = "stretchH"
+++

Voici les modèles à suivre pour mettre une adresse IP en statique/fixée ou dynamique/DHCP 

#### IP statique/fixe:  

```bash  
auto eth0
iface eth0 inet static
    address 192.168.1.101 # L'adresse IP
    netmask 255.255.255.0 # Le masque de réseau
    gateway 192.168.1.1   # La passerelle par défaut
```

---  

#### IP DHCP:  
```Bash  
auto eth0
  iface eth0 inet dhcp
```

---

- Ne pas oublier de redemarrer le service bien sur :
- Debian: 
	- `sudo /etc/init.d/networking restart`
	- `systemctl restart networking`
- Ubuntu: 
	- `service networking restart`

---

D'ailleurs si les termes vous intrigue et que vous aimeriez en savoir plus, il y a une doc complète [ici](http://manpages.ubuntu.com/manpages/trusty/man5/interfaces.5.html)