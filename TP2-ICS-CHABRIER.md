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

**PASSWORD=11;**

**echo 'entrer un mot de passe'<br>
read pass<br>**

**if [ $pass = $PASSWORD ]; then<br>
  echo "Bon mot de passe"<br>
else <br>
  echo "Mauvais mot de passe"<br>
fi**

Normalement, en faisant un `./testpwd.sh`, il n'est pas possible d'exécuter le script car nous n'avons pas les permissions. 
Pour corriger le problème, entrer `chmod u+x testpwd.sh`. Désormais, il est possible de tester le script et il doit être fonctionnel.
