+++
title = "Créer une clef SSH"
description = "Voici comment créer une clef SSH sous Linux"
author = "Hugo Grosot"
date = "2020-11-13"
tags = ["linux", "ssh", "tips"]
categories = ["ssh"]
[[images]]
  src = "/img/2020/11/creer_clef_ssh/key.png"
  alt = "clef"
  stretch = "stretchH"
+++

Nous allons voir comment générer une clef SSH sous Linux et c'est très simple !

- Tout d'abord il faut lancer l'utilitaire: `ssh-keygen`
- Il faut choisir un nom pour cette clef, dans mon cas c'est pour un accès à Github, je l'ai donc nommée `github_hugo`
![ssh_keygen.png](/img/2020/11/creer_clef_ssh/ssh_keygen.png)
- Et voilà nous avons une clef

---

**Note:**
On pourra noter que j'ai quand même spécifié le chemin absolu du lieu de son stockage, en l'occurence dans le dossier **.ssh** de mon compte **root**, mais dans votre cas, vous voudrez certainement la stocker directement dans le dossier de votre session donc compléter avec votre chemin `/home/{VOTRE_USERNAME}/.ssh/{LE_NOM_DE_VOTRE_CLEF}`

---

#### Nous pouvons vérifier l'existence de cette clef:

- Rendons nous dans notre dossier de configuration **ssh** respectif: `cd /home/.ssh/`
- Puis, listons les fichiers avec: `ls -l`
![ls_l_ssh.png](/img/2020/11/creer_clef_ssh/ls_l_ssh.PNG)

Nous pouvons constater 2 fichiers portant le nom `github_hugo`:
- `github_hugo`: La clef privée ! :warning: Cette clef doit être confidentielle ! :warning:
- `github_hugo.pub`: La clef publique, c'est celle que vous pouvez distribuer sur la machine distante !

---

#### Déployer la clef 

---

#### Vérifier que la clef est bien configurée:

ssh -T git@github.com -i .ssh/github_hugo