Loïs CHABRIER

# _TP 2 - Bash_

## Exercice 1. Variables d’environnement

<br>
<span style='color:red'>1.</span> Dans quels dossiers bash trouve-t-il les commandes tapées par l’utilisateur ?
</span>

Pour savoir quels sont les dossiers où bash trouve-t-il les commandes, il faut executer la commande  `echo $PATH`, qui va parcourir tout les dossiers où figurent des commandes bash.
La commande nous retourne les chemins des dossiers comme ceci : `/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/snap/bin`

<span style='color:red'>2.</span> Quelle variable d’environnement permet à la commande cd tapée sans argument de vous ramener dans votre répertoire personnel ?

C'est la variable d'environnement `$HOME` qui permet à la commande `cd` passée sans argument de retourner au répertoire personnel : `cd $HOME`. 

<span style='color:red'>3.</span> Explicitez le rôle des variables LANG, PWD, OLDPWD, SHELL et _.

  - La variable `$LANG` est utilisée pour déterminer la langue des messages à afficher.
  - La variable `$PWD` permet de savoir où l'on se trouve dans l'arborescence. Elle retourne le chemin absolu vers le répertoire courant.
  - La variable `$OLDPWD` permet de savoir d'où l'on vient, c'est-à-dire qu'elle retourne le chemin absolu vers le répertoire courant précédent.
  - La variable `$SHELL` retourne le chemin vers l'interpréteur SHELL utilisé par défaut.


<span style='color:red'>4.</span> Créez une variable locale MY_VAR (le contenu n’a pas d’importance). Vérifiez que la variable existe.

Pour créer la variable, entrer `MY_VAR=toto` ce qui signifie qu'on entre `toto` dans la variable `MY_VAR`.
Pour vérifier qu'elle est existante, il suffit de vérifier s'il est possible d'afficher son contenu. Pour se faire, entrer `echo $MY_VAR`. La commande devrait retourner `toto`.

<span style='color:red'>5.</span> Tapez ensuite la commande bash. Que fait-elle ? La variable MY_VAR existe-t-elle ? Expliquez. A la fin de cette question, tapez la commande exit pour revenir dans votre session initiale.

Lorsque l'on tape `bash`, on ouvre un nouveau Shell. C'est comme si on ouvrait une nouvelle console ou une nouvelle fenêtre. Lorsqu'on fait un `echo $MY_VAR`, on peut voir que la commande ne retourne rien et c'est normal. Comme nous avons créé la variable locale `MY_VAR` dans le Shell de niveau 1, on ne peut pas l'utiliser dans les autres niveau, et en l'occurence ici nous sommes passé au niveau 2 en tapant la commande `bash` (pour vérifier le niveau dans lequel nous sommes, entrer `echo $SHLVL`), de ce fait, nous ne pouvons pas utiliser la variable locale au niveau 1.

<span style='color:red'>6.</span> Transformez MY_VAR en une variable d’environnement et recommencez la question précédente. Expliquez.

$MY_VAR est une variable locale. Pour la transformer en variable d'environnement, il suffit de taper `export MY_VAR="le texte à entrer dedans"`. Désormais, effectuer un `echo $MY_VAR` pour vérifier qu'on a bien la variable créée avec le texte passé dedans. 
Maintenant, ouvrir un nouveau bash avec `bash` et afficher le contenu de la variable avec `echo $MY_VAR`. On peut désormais voir que la variable d'environnement MY_VAR est fonctionnelle puisqu'elle est utilisable peut importe le niveau de Shell où l'on se trouve.

<span style='color:red'>7.</span> Créer la variable d’environnement NOMS ayant pour contenu vos noms de binômes séparés par un espace.
Afficher la valeur de NOMS pour vérifier que l’affectation est correcte.

Entrer `export NOMS="COTET CHABRIER"` puis `echo $NOMS`. Si l'affectation est correcte, la commande devrait retourner "COTET CHABRIER".

<span style='color:red'>8.</span> Ecrivez une commande qui affiche ”Bonjour à vous deux, binôme1 binôme2 !” (où binôme1 et binôme2 sont vos deux noms) en utilisant la variable NOMS.

Entrer simplement `echo "Bonjour à vous deux," $NOMS`

<span style='color:red'>9.</span> Quelle différence y a-t-il entre donner une valeur vide à une variable et l’utilisation de la commande unset ?

La différence est qu'une variable vide ne possède pas de contenu mais existe quand même, alors qu'en utilisant la commande `unset`, on supprime carrément la variable et son contenu.

<span style='color:red'>10.</span> Utilisez la commande echo pour écrire exactement la phrase : $HOME = chemin (où chemin est votre dossier personnel d’après bash)

Il y a 2 manières de le faire : `echo "\$HOME = $HOME"` ou alors `echo '$HOME'" = $HOME"`.

### Programmation Bash

Vous enregistrerez vos scripts dans un dossier script que vous créerez dans votre répertoire personnel.
Tous les scripts sont bien entendu à tester.
Ajoutez le chemin vers script à votre PATH de manière permanente.

Pour se faire, dans le répertoire personnel, entrer `mkdir script` puis `nano .bashrc` pour rajouter la ligne `PATH=$PATH:~/script` à la fin du fichier. Pour vérifier, entrer `echo $PATH` pour vérifier que notre chemin apparaît dans le retour de la commande.

## Exercice 2. Contrôle de mot de passe

<br>
Écrivez un script testpwd.sh qui demande de saisir un mot de passe et vérifie s’il correspond ou non au
contenu d’une variable PASSWORD dont le contenu est codé en dur dans le script. Le mot de passe saisi par l’utilisateur ne doit pas s’afficher.

Dans le dossier "script" créé précedemment, créer un fichier "testpwd.sh" avec `touch testpwd.sh`. 
Une fois créé, entrer dans la configuration du fichier avec `nano testpwd.sh` pour y écrire le script suivant :

       #!/bin/sh
       
       PASSWORD=11;

        echo 'entrer un mot de passe'
        read pass

        if [ $pass = $PASSWORD ]; then
              echo "Bon mot de passe"
        else
              echo "Mauvais mot de passe"
        fi

Normalement, en faisant un `./testpwd.sh`, il n'est pas possible d'exécuter le script car nous n'avons pas les permissions. 
Pour corriger le problème, entrer `chmod u+x testpwd.sh`. Désormais, il est possible de tester le script et il doit être fonctionnel.

## Exercice 3. Expressions rationnelles

<br>
Ecrivez un script qui prend un paramètre et utilise la fonction suivante pour vérifier que ce paramètre
est un nombre réel :

<br>
Il faut tout d'abord créer un nouveau fichier dans le dossier script que l'on appelera "ScriptEX3" : `touch ScriptEX3.sh`.
Il ne faut pas oublié de lui donner les bons droits avant de l'exécuter : `chmod u+x ScriptEX3.sh`.
Enfin, il n'y a plus qu'à écrire le script : 
<br>

        #!/bin/sh

        function is_number()
        {
                re='^[+-]?[0-9]+([.][0-9]+)?$' 
                        if ! [[ $1 =~ $re ]] ; then
                                return 1 
                        else
                                return 0
                        fi
        }

        is_number $1 
        if [ $? = 0 ]; then
                echo "C'est un nombre réel"
                        else
                echo "C'est un nombre non réel"
        fi

## Exercice 4. Contrôle d’utilisateur

<br>
Écrivez un script qui vérifie l’existence d’un utilisateur dont le nom est donné en paramètre du script. Si le
script est appelé sans nom d’utilisateur, il affiche le message : ”Utilisation : nom_du_script nom_utilisateur”,
où nom_du_script est le nom de votre script récupéré automatiquement (si vous changez le nom de votre
script, le message doit changer automatiquement)

<br>
Comme d'habitude, on créé un nouveau fichier dans le dossier script : `touch ScriptEX4.sh` en lui affectant les bons droits.
Ensuite, passons à l'écriture du script : 
<br>

        #!/bin/sh 
         
        function utilisateur()
        {

        grep -w ^$1 /etc/passwd;

        }

        if [ -z "$1" ]; then
                echo "Utilisation : $(basename "$0") nom_utilisateur"
        else

                utilisateur $1
                if [ $? = 0 ]; then
                    echo "L'utilisateur existe"
                else
                    echo "L'utilisateur n'existe pas"
                fi
         fi
        
## Exercice 5. Factorielle

<br>
Écrivez un programme qui calcule la factorielle d’un entier naturel passé en paramètre (on supposera que l’utilisateur saisit toujours un entier naturel).

<br>
Comme d'habitude, on créé un nouveau fichier dans le dossier script : `touch ScriptEX5.sh` en lui affectant les bons droits.
Ensuite, passons à l'écriture du script : 
<br>

        #!/bin/sh 
        
        function factorielle() {
              n=$1
              if [ $n -eq 0 ]; then
                     echo "Entrer autre chose que 0 svp"
              else
                     echo $(( n * `factorielle $(( n - 1 ))` ))
               fi
        }

        echo "Resultat : $(factorielle $1)"

## Exercice 6. Le juste prix

<br>
Écrivez un script qui génère un nombre aléatoire entre 1 et 1000 et demande à l’utilisateur de le deviner. Le programme écrira ”C’est plus!”, ”C’est moins!” ou ”Gagné!” selon les cas (vous utiliserez $RANDOM).

<br>
Comme d'habitude, on créé un nouveau fichier dans le dossier script : `touch ScriptEX6.sh` en lui affectant les bons droits.
Ensuite, passons à l'écriture du script : 
<br>

        #!/bin/sh 
        
        NBALEATOIRE=$(( ( RANDOM % 1000 )  + 1 ))
        NB_WHILE=-24
        echo "Essaye de trouver un nombre entre 1 et 1000 !"
        while [ $NBALEATOIRE != $NB_WHILE ]
            do
                echo "Allé je t'aide un peu... Le nombre à trouver est" $NBALEATOIRE
                read NB_WHILE
                if [ $NBALEATOIRE -lt $NB_WHILE ]; then
                      echo "Le nombre à trouver est plus petit"
                elif [ $NBALEATOIRE -gt $NB_WHILE ]; then
                      echo "T'es pas très bon.. C'est plus grand"
                fi
            done
        echo "Quel homme (ou femme), t'es tombé pleins dans le mille!!"

## Exercice 7. Statistiques

<br>
Écrivez un script qui prend en paramètres trois entiers (entre -100 et +100) et affiche le min, le max et la moyenne. Vous pouvez réutiliser la fonction de l’exercice 3 pour vous assurer que les paramètres sont bien des entiers. 
<br>
Comme d'habitude, on créé un nouveau fichier dans le dossier script : `touch ScriptEX7.sh` en lui affectant les bons droits.
Ensuite, passons à l'écriture du script : 
<br>
    
    #!/bin/sh
    
    function reelounon()
    {
            re='^[+-]?[0-9]+([.][0-9]+)?$'
            if ! [[ $nb =~ $re ]] ; then
                    return 1
            else
                    return 0
            fi
    }

    keep=1
    nb=0
    i=0
    marks=()

    while [ $keep != 0 ]
    do
            echo "entrez une note"
            read nb

            reelounon $nb
            if [ "$?" != "0" ]; then
                    echo "merci d'entrer que des réels"
            else
                    marks[$i]=$nb
            fi

            echo "continuer ? o / n"
            read answer
            if [ "$answer" = "n" ]; then
                    keep=0;
            fi

            ((i++))
    done

    mini=${marks[0]}
    maxi=${marks[0]}
    moy=0
    longueurtableau=${#marks[@]}
    for mark in "${marks[@]}"
    do
            if [[ $mark < $mini ]]; then
                    mini=$mark
            fi
            if [[ $mark > $maxi ]]; then
                    maxi=$mark
            fi
            ((moy=moy+mark))
    done
    moy=$((moy / longueurtableau))
    echo "le max est $maxi, le min est $mini et la moyenne est de $moy"
