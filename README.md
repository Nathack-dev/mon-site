## 🌠 Terminal Web

Il s'agit d'un terminal web basique basé sur Ubuntu qui me sert de portfolio interactif.

Il comporte un système de commandes, ainsi qu'un "tapeur automatique" qui tape et saisit automatiquement les commandes à partir du code.
Ceci est utile pour les visiteurs qui ne sont pas familiers avec les CLI et élargit le nombre de personnes qui peuvent y naviguer.
Pour augmenter encore plus la praticité, il est possible de cliquer sur les fichiers répertoriés avec "ls" et à d'autres endroits pour exécuter automatiquement des commandes comme cat

## ⚙️ How-To setup 

Si vous souhaitez le configurer pour vos propres besoins, tous les fichiers du dossier terminalfiles sont automatiquement disponibles pour que le terminal les utilise.
Par défaut, les commandes `cat welcome.txt` et `ls` sont automatiquement lancées au démarrage du terminal. Vous pouvez modifier welcome.txt pour changer le message de bienvenue ou modifier les commandes elles-mêmes dans terminal.js, ligne 27 :

```js
autowriteQueue.push("Command here with arguments");
```

En plaçant un élément dans la file d'attente, la commande sera tapée et l'entrée de l'utilisateur sera verrouillée dès que l'entrée sera prête.

Si vous souhaitez le configurer pour vos propres besoins, tous les fichiers du dossier terminalfiles sont automatiquement disponibles pour que le terminal les utilise. Je recommande de créer un nouveau fichier et d'y ajouter les commandes personnalisées au lieu de defaultcommands.js pour faciliter les fusions git.
Vous pouvez regarder n'importe quelle commande dans defaultcommands.js pour plus d'exemples ou vous référer à l'exemple ci-dessous :

```js
function myCommand(args) {
  terminalPrint("Message here");
  cmdDone(); // Required after finishing function. Useful for any asynchronous functions. (ie. AJAX)
}

function ready() {
  addCmd("mycommand", myCommand);
}

$(document).ready(ready);
```

le premier argument passé à toute fonction de commande est une liste d'arguments donnée par l'utilisateur. Elle est séparée par des espaces mais ignore les guillemets.
Par exemple : `mycommand there are "some arguments" 'to pass'` donnerait `there, are, some arguments, to pass`.

## 📚 Fonctions utiles 

▶️ `terminalPrint` est une fonction d'impression simple. Le premier argument est le message à imprimer, et le deuxième argument facultatif est un booléen qui, s'il est vrai, ajoute un saut de ligne à la fin. Par défaut, cette valeur est vraie.

▶️ `cmdDone` réinitialise l'entrée de l'utilisateur, et doit être appelé après la fin de l'exécution d'une commande. Ceci est nécessaire pour supporter les fonctions asynchrones comme AJAX.

▶️ `toggleInput` désactive ou active la saisie de l'utilisateur. `true` bloquera la saisie et `false` l'activera. Aucun argument ne permettra de basculer en fonction de l'état de verrouillage actuel.

▶️ `addCmd` ajoute la commande au terminal. Le premier argument est une chaîne de caractères et constitue le mot clé permettant à l'utilisateur d'exécuter la commande. Le second est une fonction qui est appelée avec un tableau d'arguments que l'utilisateur a passés avec la commande.
