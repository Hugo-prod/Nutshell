+++
title = "Comment réparer une clef USB"
description = "Guide de réparation d'une clef USB avec Windows"
author = "Hugo Grosot"
date = "2020-11-08"
tags = ["windows", "usb", "partition"]
categories = ["Réparation"]
[[images]]
  src = "img/2020/11/reparer_cle_usb_avec_windows/memory-stick-1267620_1280.jpg"
  alt = "Clefs usb"
  stretch = "stretchH"
+++


## Réparer une clef USB Windows:
---  

Il arrive des fois, qu'après avoir créée une clef USB bootable (Linux, Windows...) on se retrouve avec un espace de stockage perdu...

Dans mon cas, je voulais reformater ma clef USB de 8 Go sur laquelle j'avais monté un ISO Debian, sauf que l'outil de formatage Windows indiquait sa capacité totale à 390 Ko !

![USB_390Ko.PNG](/img/2020/11/reparer_cle_usb_avec_windows/USB_390Ko.PNG)

Alors que l'outil de Gestion des disques Windows indiquait bien 8Go:

![Gestion_des_disques.PNG](/img/2020/11/reparer_cle_usb_avec_windows/Gestion_des_disques.PNG)

---

#### comment faire pour récupérer ce volume perdu ?

- Dans le menu Démarrer, recherchez et lancez diskpart  
![diskpart.PNG](/img/2020/11/reparer_cle_usb_avec_windows/diskpart.png)


- Tapez list disk pour voir tous les volumes de disque actuels sur votre système
![List_disk_unplugged.PNG](/img/2020/11/reparer_cle_usb_avec_windows/List_disk_unplugged.PNG)


- Branchez votre clé USB et tapez à nouveau list disk. Notez le nouveau volume listé
![List_disk_plugged.PNG](/img/2020/11/reparer_cle_usb_avec_windows/List_disk_plugged.PNG)


- Une fois le volume identifié:
![Cmd.PNG](/img/2020/11/reparer_cle_usb_avec_windows/Cmd.PNG)


- Tapez le numéro de disque sélectionné # où # correspond au numéro de volume de votre clé USB
- Tapez clean pour effacer le volume de toutes les partitions.
- Tapez create partition primary pour créer une nouvelle partition avec tout l'espace non alloué.
- Tapez exit pour terminer.
- Vous pouvez maintenant aller dans l'explorateur de fichier Windows, double cliquer sur votre clef USB
- L'outil de formatage se lancera:  

![Format_disk.PNG](/img/2020/11/reparer_cle_usb_avec_windows/Format_disk.PNG)


- Procéder au formatage

![format_8go.PNG](/img/2020/11/reparer_cle_usb_avec_windows/format_8go.PNG)

- Et voici votre clef réparée: 

![success.PNG](/img/2020/11/reparer_cle_usb_avec_windows/success.PNG)