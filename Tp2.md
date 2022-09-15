# TP 2

## Exercice 1

#### 1
Les commandes tapées par l'utilisateur sont dans le fichier ``.bash_history``

#### 2
La commande `cd` permet de revenir dans le répertoire personnel grâce à la variable d'environnement `$HOME`. Tout d'abord, on peut voir le contenu des variables avec la commande `printenv [$VAR]`. 

#### 3
**LANG** affiche la langue utilisée par le terminal (en_US) et le language utilisé (UTF-8).
**PWD** contient le répertoire courant.
**OLDPWD** contient le répertoire courant précédent.
**SHELL** retourne le répertoire du dossier 'bash'.

#### 4
``MY_VAR="ru"``
``printenv MY_VAR``

#### 5
La commande ``bash`` permet d'ouvrir une nouvelle session ainsi la variable locale crée n'est plus trouvable après l'ouverture du bash.

#### 6
``export MY_VAR="ru"``
``printenv MY_VAR``
La variable d'environnement est une variable global.

#### 7
``export MY_VAR="Célian Jounin"``
``printenv NOM``

#### 8
``echo "Bonjour à vous" $NOM "!"``

#### 9
Une valeur vide ne supprime pas la variable mais lui assigne juste une valeur nulle alors que ``unset`` lui supprime la variable

#### 10
``echo $HOME=/home/user``

## Exercice 2

```bash
#!/bin/bash
 PASSWORD="123456"
 read -s -p "Mot de passe : "  pwd  
 if [ "$pwd" = "$PASSWORD" ]; then  
 echo  "Mot de passe bon"  
 else  
 echo  "Mot de passe erroné"  
 fi
```
on créer un fichier avec la commande
``nano testpwd.sh``
puis on le rend exécutable grâce a la commande
``chmod u+x testpwd.sh``

## Exercice 3
```bash
#!/bin/bash
function is_number()
 { 
 re='^[+-]?[0-9]+([.][0-9]+)?$' 
 if ! [[ $1 =~ $re ]] ; then 
 return 1 
 else 
 return 0 
 fi 
 }
if is_number ; then
echo "nice"
else
echo "nope"
```

## Exercice 4
```bash
#!/bin/bash 
if [ $# -eq 0 ] ; then 
echo "Utilisation : $0 nom_utilisateur" 
else 
if [ -z $(getent passwd $1) ] ; then
echo "L'utilisateur $1 n'existe pas" 
else 
echo "L'utilisateur $1 existe" 
fi 
fi
```

## Exercice 5
```bash
#!/bin/bash

read -p "Entrez nombre : " n 
FACT=1 
for i in $(seq 1 $n) 
do 
FACT=$((FACT*i)) 
done 
echo "$FACT"
```

## Exercice 6
```bash
#!/bin/bash 
nombre=$(($RANDOM % 1000 + 1)) 
echo "Devinez le nombre entre 1 et 1000" 
read reponse 
while [ $reponse -ne $nombre ] 
do 
if [ $reponse -lt $nombre ] ; then 
echo "C'est plus !" 
else 
echo "C'est moins !" 
fi 
read reponse 
done 
echo "Gagné !"
```

## Exercice 7

```bash
#!/bin/bash  
if [ $# -ne 3 ]; then  
  echo  "Guide: $0 n1 n2 n3"  
  exit 1 
fi  
for i in  $@; do  
  if [ $i -lt -100 -o $i -gt 100 ]; then 
    echo  "Erreur: $i n'est pas entre -100 et +100"  
    exit 1 
  fi  
done 
min=$1 
max=$1 
sum=0 
for i in  $@; do  
  if [ $i -lt $min ]; then 
    min=$i  
  fi  
  if [ $i -gt $max ]; then 
    max=$i  
  fi 
  sum=$((sum + i)) 
done  
echo  "Mini: $min"  
echo  "Maxi: $max"  
echo  "Moyenne: $((sum / 3))"
``` 

Pour avoir n quelconque de paramètres, on met en commentaire le premier `if` avec `##` :

```bash 
##if [ $# -ne 6 ]; 
##then
##      echo "Guide: $0 n1 n2 n3 n4 n5"
##      exit 1
##fi
```
```bash
#!/bin/bash  
# Initialisation des variables  
declare -a notes 
declare -i i=0 
declare -i min=100 
declare -i max=-100 
declare -i moyenne=0 
declare -i somme=0 
# Saisie des notes  
while  true  do  
  read -p "Saisir note : " input 
  if [ $input -ge -100 ] && [ $input -le 100 ] && [[ $input == ?     (-)+([0-9]) ]]; then 
    notes[$i]=$input 
    i=$i+1 
  elif [[ $input = "q" ]] || [[ $input = "Q" ]]; then  
    break  
  else  
    echo  "La note doit être comprise entre -100 et 100 / Entrer sur q/Q pour quitter"  
  fi  
done  
# Calcul des notes  
for note in  ${notes[*]} ; do  
  if [ $note -lt $min ] ; then 
    min=$note  
  fi  
  if [ $note -gt $max ] ; then 
    max=$note  
  fi 
  somme=$somme+$note  
done 
moyenne=$somme/10 
# Affichage des résultats  
echo  "La note minimale est $min"  
echo  "La note maximale est $max"  
echo  "La moyenne est $moyenne"
```
