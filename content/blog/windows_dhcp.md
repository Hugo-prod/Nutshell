+++
title = "Faire un serveur DHCP avec Windows server 16"
#description = "Voici un tutoriel pour réaliser étape par étape un serveur DHCP avec Windows server 16"
author = "Hugo Grosot"
date = "2020-11-10"
tags = ["windows", "serveur", "dhcp"]
categories = ["windows"]
[[images]]
  src = "/img/2020/11/windows_dhcp/Windows-server.jpg"
  alt = "cheatsheet bash"
  stretch = "stretchH"
+++

Voici un tutoriel pour réaliser étape par étape un serveur DHCP avec Windows server 16

- Cliquez sur **Gérer**, puis sur **Ajouter des rôles et fonctionnalités**:  
![01](/img/2020/11/windows_dhcp/01.PNG)

---  

- **Suivant**:
![02](/img/2020/11/windows_dhcp/02.PNG)

---

- Sélectionner le type d’installation **Installation basée sur un rôle ou une fonctionnalité**:
![03](/img/2020/11/windows_dhcp/03.PNG)

---

- Selectionner le serveur puis **suivant**:
![04](/img/2020/11/windows_dhcp/04.PNG)

---

- Sélectionner le rôle **Serveur DHCP**:
![05](/img/2020/11/windows_dhcp/05.PNG)

---

- Valider avec **Suivant**:
![06](/img/2020/11/windows_dhcp/06.PNG)

---

- Ici vous pouvez constater toutes les fonctionnalités disponnible, dans notre cas nous n'en avons besoin d'aucune, cliquez sur **Suivant**:
![07](/img/2020/11/windows_dhcp/07.PNG)

---

- :warning: Rappel: votre serveur doit avoir une **IP fixée** ! :warning:  
- Cliquez sur **suivant**: 
![08](/img/2020/11/windows_dhcp/08.PNG)

---

- Vous pouvez maintenant **l'installer**:
![09](/img/2020/11/windows_dhcp/09.PNG)

---

- Patienter pendant l'installation:
![10](/img/2020/11/windows_dhcp/10.PNG)

---

- L'installation est maintenant finit, cliquez sur **Fermer**:
![11](/img/2020/11/windows_dhcp/11.PNG)

---

On peut maintenant aperçevoir un petit drapeau avec un :warning: car le serveur **DHCP** nécessite encore quelques manipulations
- Cliquez **Terminer la configuration DHCP**:
![12](/img/2020/11/windows_dhcp/12.PNG)

---

- **Valider**:
![13](/img/2020/11/windows_dhcp/13.PNG)

---

- **Fermer**:
![14](/img/2020/11/windows_dhcp/14.PNG)

---

Maintenant que le serveur DHCP est installé, il nous reste plus qu'à le configurer, pour ce faire
- Ouvrez le pannel de configuration du serveur DHCP, depuis le menu **Outils**, puis sélectionnez **DHCP**:
![16](/img/2020/11/windows_dhcp/16.PNG)

---

Nous allons créer une **Nouvelle étendue** qui aura pour effet de paramétrer une plage d'adresse IP disponible aux clients 
- Clique droit sur **IPv4**
- Clique gauche **Nouvelle étendue**  
![17](/img/2020/11/windows_dhcp/17.PNG)

---

- **Suivant**:  
![18](/img/2020/11/windows_dhcp/18.PNG)

---

- Nommez la nouvelle étendu:  
![19](/img/2020/11/windows_dhcp/19.PNG)

---

- Saisissez une plage d'adresse IP:  
![20](/img/2020/11/windows_dhcp/20.PNG)

---

- Vous pouvez sélectionner des adresses IP à exclure et même attribuer un retard pour transmettre un message **DHCPOFFER**:  
![21](/img/2020/11/windows_dhcp/21.PNG)

---

- Voici la durée du bail, vous pouvez également le modifier:  
![22](/img/2020/11/windows_dhcp/22.PNG)

---

- Sélectionner **Oui** dans le cas où vous avez une **passerelle par défaut** et/ou un **DNS**:  
![23](/img/2020/11/windows_dhcp/23.PNG)

---

- Saisir votre **Passerelle par défaut**:  
![24](/img/2020/11/windows_dhcp/24.PNG)

---

- Saisir votre **DNS**:  
![25](/img/2020/11/windows_dhcp/25.PNG)

---

- Activer l'étendue:  
![27](/img/2020/11/windows_dhcp/27.PNG)

---

- Terminer:  
![28](/img/2020/11/windows_dhcp/28.PNG)

---

- Nous pouvons constater que l'étendue a bien été créée:  
![29](/img/2020/11/windows_dhcp/29.PNG)

---

- On peut consulter les baux attribués:
![30](/img/2020/11/windows_dhcp/30.PNG)

---

- Et voici la preuve que le serveur **DHCP** fonctionne, car il a attribué deux baux:  
![31](/img/2020/11/windows_dhcp/31.PNG)

> Note: on peut constater le `BAD_ADDRESS` pour l'adresse IP: `192.168.1.10`
> Pour la simple est bonne raison qu'un service **DHCP** était déjà actif sur un switch, et a donc provoqué un conflit !

---

Voilà :) 