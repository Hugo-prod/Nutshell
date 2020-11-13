+++
title = "SSH autocompletion"
description = "Ajouter \"l'autocompletion\" pour SSH"
author = "Hugo Grosot"
date = "2020-11-09"
tags = ["ssh", "bash", "tips"]
categories = ["ssh"]
[[images]]
  src = "/img/2020/11/ssh_autocompletion/connexion_ssh.png"
  alt = "Connexion ssh"
  stretch = "stretchH"
+++


Vous savez tout comme moi qu'il peut-être épuisant de devoir retaper l'adresse **IP** ou le **Host** de votre serveur

**La solution:** ajouter l'autocomplete de Hostname pour **SSH** ! 

- Voici ce que ça donne:

![ssh_autocomplete.gif](/img/2020/11/ssh_autocompletion/ssh_autocomplete.gif)

- Pour ce faire il nous faut déjà remplir le fichier `~/.ssh/config` avec nos serveurs, voici un exemple:

```  
########################################
######## Serveur de production #########
########################################

Host ServeurDeProduction
        Hostname 127.0.0.1
        User root
        IdentityFile ~/.ssh/prod

########################################
######## Serveur de qualif #############
########################################

Host ServeurDeQualif
        Hostname 127.0.0.1
        User root
        IdentityFile ~/.ssh/qualif
        
#########################################
######## Serveur de tata odette #########
#########################################

Host tata_odette
        Hostname 127.0.0.1
        User root
        IdentityFile ~/.ssh/tata_odette

```

Ajoutez le script d'autocompletion dans ce nouveau fichier:

`$ vim /etc/bash_autocompletion.d/ssh`

```bash  
_ssh(){
        local cur prev opts
        COMPREPLY=()
        cur="${COMP_WORDS[COMP_CWORD]}"
        prev="${COMP_WORDS[COMP_CWORD-1]}"
        opts=$(grep '^Host' ~/.ssh/config ~/.ssh/config.d/* 2>/dev/null | grep -v '[?*]' | cut -d ' ' -f 2-)
        COMPREPLY=( $(compgen -W "$opts" -- ${cur}) )
        return 0
}
complete -F _ssh ssh
```

- Il faut ensuite indiquer au `~/.bashrc` de charger cette fonction

`$ vim ~/.bashrc`

- Ajouter tout à la fin du fichier cette ligne:

```bash  
. /etc/bash_completion.d/ssh
```

- Voilà, vous pouvez maintenant redémarrer votre terminal ou recharger votre configuration avec:

`. ~/.bashrc`
