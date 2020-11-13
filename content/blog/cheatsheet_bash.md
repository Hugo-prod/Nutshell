+++
title = "Cheatsheet Bash"
description = "Petit carnet de note pour Bash"
author = "Hugo Grosot"
date = "2020-11-09"
tags = ["bash", "tips"]
categories = ["bash"]
[[images]]
  src = "/img/2020/11/cheatsheet_bash/cheatsheet_bash.png"
  alt = "cheatsheet bash"
  stretch = "stretchH"
+++


> Cette cheatsheet est juste une réécriture partielle de cette cheatsheet: [Source: devhints.io/bash](https://devhints.io/bash)


#### Liste des variables définies dans un shell:  
```Bash  
$ set # Afficher les variables définie dans un shell
$ unset MAVAR # Effacer une variable du shell
```

#### Variable:

**Convention de nommage:** écrire les variables en majuscule

```bash  
NAME="John"
echo $NAME
echo "$NAME"
echo "${NAME}!"
```
---  

#### Variable portée:  

```Bash  
readonly LECTURESEULE="ceci est une constante" # Constante
```
---  

#### Variable ` ' " tick `:

```Bash
DATE=date
echo $DATE    # date (affiche - "string")
----------
DATE="La date:"date
echo $DATE    # la date:date (affiche - "string"string)
----------
DATE='La date:'date
echo $DATE    # La date:date (affiche - "string"string)
----------
DATE="La date:"`date`
echo $DATE    # La date: samedi 22... (affiche - "string"`cmd`)
----------
DATE="La date:`date`"
echo $DATE    # La date: samedi 22... (affiche - "string`cmd`")
----------
```

---

#### Variable manipulation:

```Bash 
STR="HELLO WORLD!"
echo ${STR,}   #=> "hELLO WORLD!" (lowercase 1st letter)
echo ${STR,,}  #=> "hello world!" (all lowercase)

STR="hello world!"
echo ${STR^}   #=> "Hello world!" (uppercase 1st letter)
echo ${STR^^}  #=> "HELLO WORLD!" (all uppercase)
```

---  

#### Variables traitment:  

```Bash
name="John"
echo ${name}
echo ${name/J/j}    #=> "john" (substitution)
echo ${name:0:2}    #=> "Jo" (slicing)
echo ${name::2}     #=> "Jo" (slicing)
echo ${name::-1}    #=> "Joh" (slicing)
echo ${name: -1}   #=> "n" (slicing from right) -> ${$PATH_TO_FOLDER: -1}
echo ${name:(-2):1} #=> "h" (slicing from right)
echo ${food:-Cake}  #=> $food or "Cake"

length=2
echo ${name:0:length}  #=> "Jo"

echo ${#name}       # 4 (size)
STR="/path/to/foo.cpp"
echo ${STR%.cpp}    # /path/to/foo
echo ${STR%.cpp}.o  # /path/to/foo.o

echo ${STR##*.}     # cpp (extension)
echo ${STR##*/}     # foo.cpp (basepath)

echo ${STR#*/}      # path/to/foo.cpp
echo ${STR##*/}     # foo.cpp

echo ${STR/foo/bar} # /path/to/bar.cpp

STR="Hello world"
echo ${STR:6:5}   # "world"
echo ${STR:-5:5}  # "world"

SRC="/path/to/foo.cpp"
BASE=${SRC##*/}   #=> "foo.cpp" (basepath)
DIR=${SRC%$BASE}  #=> "/path/to/" (dirpath)
```

---  

#### Variable math:  
```Bash  
echo $((5*5))
```

---  

#### String quote:

```bash  
NAME="John"
echo "Hi $NAME"  #=> Hi John
echo 'Hi $NAME'  #=> Hi $NAME
```

--- 

#### Conditionals:

```Bash  
if [[ -z "$string" ]]; then
  echo "String is empty"
elif [[ -n "$string" ]]; then
  echo "String is not empty"
fi
```  

[See Conditionals](https://devhints.io/bash#conditionals)

---  

#### Conditional execution:

```Bash  
git commit && git push
git commit || echo "Commit failed"
```

---  

#### Condition négation:
```Bash
if [! -d /etc/fstab ]   # Si '/etc/fstab' n'est pas un dossier
```
---

#### Condition (number):

> Note that \[\[ is actually a command/program that returns either 0 (true) or 1 (false). Any program that obeys the same logic (like all base utils, such as grep(1) or ping(1)) can be used as condition, see examples.
> 
```Bash
[[ -z STRING ]] 	# Empty string
[[ -n STRING ]] 	# Not empty string
[[ STRING == STRING ]] 	# Equal
[[ STRING != STRING ]] 	# Not Equal
[[ NUM -eq NUM ]] 	# == : Equal
[[ NUM -ne NUM ]] 	# != : Not equal
[[ NUM -lt NUM ]] 	# <  : Less than
[[ NUM -le NUM ]] 	# <= : Less than or equal
[[ NUM -gt NUM ]] 	# >  : Greater than
[[ NUM -ge NUM ]] 	# >= : Greater than or equal
[[ STRING =~ STRING ]] 	# Regexp
(( NUM < NUM )) 	# Numeric conditions
[[ -o noclobber ]] 	# If OPTIONNAME is 
```

---  

#### File condition:
```Bash
[[ -e FILE ]] 	# Exists: Le fichier existe
[[ -r FILE ]] 	# Readable: Le fichier est lisible
[[ -h FILE ]] 	# Symlink: ???
[[ -L FILE ]]   # link: Le fichier est un lien
[[ -d FILE ]] 	# Directory: Le fichier est un répertoire
[[ -w FILE ]] 	# Writable: Le fichier est modifiable
[[ -s FILE ]] 	# Size is > 0 bytes: ???
[[ -f FILE ]] 	# File: Le fichier est un fichier (PDV: unix)
[[ -x FILE ]] 	# Executable: Le fichier est exécutable
[[ FILE1 -nt FILE2 ]] 	# 1 is more recent than 2: FICHIER1 (+) récent que FICHIER2
[[ FILE1 -ot FILE2 ]] 	# 2 is more recent than 1: FICHIER1 (-) récent que FICHIER2
[[ FILE1 -ef FILE2 ]] 	# Same files: FICHIER1 == FICHIER2
```

---  

#### Functions:  

```bash  
get_name() {
  echo "John"
}

echo "You are $(get_name)"
```
[See more](https://devhints.io/bash#functions)

---  

#### Shell execution

```Bash  
echo "I'm in $(pwd)"
echo "I'm in `pwd`"
```

[See more](http://wiki.bash-hackers.org/syntax/expansion/cmdsubst)

---  

#### Work with arrays:  

```Bash  
echo ${Fruits[0]}           # Element #0
echo ${Fruits[@]}           # All elements, space-separated
echo ${#Fruits[@]}          # Number of elements
echo ${#Fruits}             # String length of the 1st element
echo ${#Fruits[3]}          # String length of the Nth element
echo ${Fruits[@]:3:2}       # Range (from position 3, length 2)
```  
```Bash  
Fruits=("${Fruits[@]}" "Watermelon")    # Push
Fruits+=('Watermelon')                  # Also Push
Fruits=( ${Fruits[@]/Ap*/} )            # Remove by regex match
unset Fruits[2]                         # Remove one item
Fruits=("${Fruits[@]}")                 # Duplicate
Fruits=("${Fruits[@]}" "${Veggies[@]}") # Concatenate
lines=(`cat "logfile"`)                 # Read from file
```
---  

#### Return values:

```Bash  
./monscript.sh var1 test2 valeur3
$0 # Nom du script "./monscript"
$* # Tous les paramètres sous formes d'un seul arguments: "var1 test2 valeur3"
$@ # Tous les paramètres sous formes d'un argument par paramètres "var1" "test2" "valeur3"
$# # Nombre de paramètres dans l'exemple : 3
$? # Code de retour (0: OK, 1 à 128: Erreur)
$$ # PID du shell qui execute le script
$! # PId du dernier processus lancé en arrière-plan
```

---  

#### Moulinette - Check syntaxe:
```Bash  
bash -n monscript.sh
```