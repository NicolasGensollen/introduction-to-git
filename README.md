# Introduction à Git et GitHub

## I. Différence entre Git et GitHub

Le but de cette section est d'expliquer en quelques mots la différence fondamentale entre **Git** et **GitHub** qui sont souvent confondu.

### Git

**Git** est un *système de contrôle de version* (*version control system* en anglais) qui permet d'organiser le dévelopement de ses projets. Autrement dit, **Git** est un programme permettant aux developpeurs d'améliorer leur productivité en automatisant certaines taches rébarbatives. 

### A quoi ça sert?

Qui n'a jamais voulu tester un bout de code sans être certain de son fonctionnement? 

Sans système de contrôle de version, il faudrait passer par tout un processsus de copies de fichiers et de suppressions en cas d'échec. C'est gérable pour des projets très très simples mais impensable dans la "*vraie vie*".  

**Git** permet ainsi de tester diverses implémentation en parrallèle, de combiner diverses solutions trouvées, ou de revenir en arrière dans l'historique si besoin. Autrement dit, on peut très bien utiliser **Git** tout seul sur une machine non connectée à Internet.

### Comment ça marche?

On expliquera plus en détails le fonctionnement de **Git** dans les sections suivantes avec de exemples. En deux mots, **Git** permet de prendre des snapshots de son projet à divers moments. On nomme ces snapshots des `commits` dans le jargon **Git**. Ces snapshots (ou commits) sont organisés en un arbre dont la racine est le premier commit, en d'autres termes l'état initial du projet. Chaque nouveau commit que l'on réalise ensuite pointe vers son parent, et **Git** traque les changements requis pour passer d'un commit à un autre. Une des forces de cette approche est que l'on peut naviguer facilement dans l'historique de son projet sans stocker trop de données et avec une grande rapidité.

### GitHub

L'un des principaux intérêts de **Git** réside dans le fait de pouvoir stocker ses données et son historique  de travail sur des serveurs externes. Autrement dit, sauvegarder l'état actuel de son travail, mais aussi l'ensemble des étapes qui ont permit d'arriver à cet état. 

**GitHub** est ainsi une plateforme permettant le stockage des données d'utilisateurs sur le Cloud. On peut donc voir **GitHub** comme une application basée sur **Git** et offrant un certain nombre de services à ses utilisateurs. Bien entendu elle n'est pas la seule plateforme disponible, d'autres existent depuis longtemps comme **BitBucket** tandis que d'autres sont apparues plus récemment comme **GitLab**. Toutes ces plateformes ont de grandes similitudes et permettent de faire plus ou moins de choses. Dans ce tutoriel, on se focalisera sur **GitHub** qui est de loin la plus populaire de ces plateformes et celle qui offre, pour le moment, le plus grand éventail de services (*Issue tracking*, *Travis*, *CodeCov*...).

### Le réseau social des dévelopeurs

Il est assez réducteur de considérer **GitHub** uniquement comme une simple plateforme de stockage puisqu'elle permet en réalité de faire beaucoup plus. N'importe qui peut y créer un profile gratuitement et y stocker son code également gratuitement. En faisant cela, le code qu'un individu produit et "*pousse*" sur **GitHub** est exposé à l'ensemble de la communauté qui, en plus de pouvoir le lire, peut choisir d'y contribuer. C'est la base de *l'open source*, i.e. la pratique qui consiste à rendre le code source publique. La puissance de l'open source réside dans le fait que n'importe qui peut proposer une amélioration sur n'importe quel projet. **GitHub** facilite et clarifie ce processus de sorte que quelques clicks suffisent pour *forker* un projet existant, y apporter ses propres modifications, et les soumettre aux administrateurs du projet pour qu'elles y soient intégrées. 

**GitHub** a ainsi évolué pour devenir le plus grand réseau social de dévelopeurs au monde. Comme dans tout réseau social, il est possible de suivre d'autres dévelopeurs, de s'organiser en groupe collaboratifs (appelés *organisations*), de mettre des étoiles à certains projets (l'équivalent du fameux *Like*), ou de discuter avec ses collaborateurs.

Cette plateforme a pris tellement d'ampleur que certaines entreprises demande aux candidats qu'elles évaluent d'inclure leur profile **GitHub** dans leur CV. Cela permet en effet de voir comment un individu contribue à l'open source, et d'évaluer la qualité du code qu'il produit.

### Résumons...

Comme expliqué plus haut, il est possible d'utiliser **Git** sans utiliser **GitHub**, et il est également possible d'utiliser **GitHub** sans utiliser **Git**. Dans les deux cas l'utilisation est très limitée et ne présente pas beaucoup d'intérêt par rapport à d'autres services comme *Dropbox*. Néanmoins, lorsque l'on combine l'utilisation des deux, on obtient un outil extrêmement puissant. La suite de ce tutoriel introduit les bases de **Git** et explique comment créer son propre projet et comment le *pousser* sur **GitHub**.

## II. Vérifier si Git est installé

Pour vérifier que Git est bien installé, ouvrir un terminal et taper la commande suivante:

```bash
$ git --version
```

Qui devrait retourner quelque chose comme

```bash
git version 2.7.4
```
si Git est bien installé.

## III. Demander de l'aide à Git

Pour afficher la documentation:

```bash
$ git --help
```

En règle général Git s'évertue à donner un maximum d'information pour aider l'utilisateur. Ainsi en cas de faute de frappe dans une commande, Git propose souvent des corrections possibles:

```bash
$ git comit
git: 'comit' is not a git command. See 'git --help'.

Did you mean this?
    commit
```

## IV. Créer un projet

Il existe deux façons principales de créer un nouveau projet:

- Depuis un répertoire sur sa propre machine
- Depuis un répertoire initialisé sur GitHub

La seconde méthode nécessite d'avoir un compte GitHub, nous y reviendrons plus tard. Pour le moment, concentrons nous sur la première méthode.

### Créer le dossier qui va contenir le projet

On va donc créer un nouveau dossier qui contiendra notre nouveau projet. Ouvrez un terminal, et déplacez vous à un endroit de votre choix. Mon organisation personnelle consiste à créer un dossier *GitRepos* dans *home* et d'y mettre tout les dossier Git. En guise d'exemple, je vais créer ce dossier *GitRepos* et y créer un dossier *projet-test* qui contiendra notre nouveau projet:

```bash
$ cd ~
$ mkdir GitRepos
$ cd GitRepos
$ mkdir projet-test
$ cd projet-test
```

### Transformer le dossier en répertoire git

Pour le moment, *projet-test* est un répertoire comme un autre. Transformons le en répertoire Git:

```bash
$ git init
```

Et voilà! C'est pas plus compliqué que ça. Notre répertoire *projet-test* est maintenant un répertoire git. Pour s'en convaincre:

```bash
$ ls -a
. .. .git
```

La commande `git init` a donc créé un répertoire caché nommé `.git`. Quelque soit le projet, ce répertoire sera toujours présent à la racine et se nomera toujours pareil. Ce répertoire contient les informations dont Git a besoin et nous y reviendrons plus tard. 

### Ajouter du contenu

Pour le moment, nous allons commencer notre projet en créant un fichier Markdown nommé `README.md`. Comme vous le verrez en naviguant sur GitHub, c'est une convention de base d'avoir un readme qui décrit le projet. Ouvrez un éditeur de texte comme *vim*, *gedit*, ou *emacs* et écrivez un petit descriptif du projet, par exemple:

```
# Projet test
Ce répertoire contient le code source de mon projet test dans le cadre du module ARE dynamics 2019.
```

**Markdown** permet de mettre en forme du texte de manière assez simple. C'est un language particulièrement utilisé et très facile à apprendre. Quelques notions de base sont disponibles sur [link](https://markdown-guide.readthedocs.io/en/latest/basics.html) par exemple.

### Vérifier l'état de son projet

En l'état actuel des choses, on devrait avoir un unique fichier dans notre répertoire:

```bash
$ ls
README.md
```

Nous allons maintenant demander à Git quel est l'état de notre projet avec la commande:

```bash
$ git status
On branch master

Initial commit

Untracked files:
  (use "git add <file>..." to include in what will be committed)

    README.md

nothing added to commit but untracked files present (use "git add" to track)
```

Comme souvent, Git est assez verbeux mais il n'y a rien de bien compliqué ici. La première ligne nous dit simplement que nous sommes actuellement sur la branche `master`. Nous reviendrons la dessus lorsque nous parlerons des branches, pour le moment ignorons cette information. La suite nous dit qu'il y a actuellement un fichier non répertorié par git dans le projet, et que ce fichier s'appelle `README.md`. Jusque là, pas de surprise, on vient effectivement juste de  créer ce fichier et, même si git le voit, il ne fait rien avec pour le moment. 

### Ajouter des modifications au commit en cours

Pour que git commence à traquer ce fichier, nous allons devoir lui dire de le faire. C'est exactement ce que dit la dernière ligne de `git status` et nous allons suivre son conseil:

```bash
$ git add README.md
```

Et voilà, git traque dorénavant notre README. Vérifions ce qu'il s'est passé dans le statut de notre projet:

```bash
$ git statusOn branch master

Initial commit

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)

    new file:   README.md
```

Notre README est donc passé du status de fichier non traqué à celui de nouveau fichier. 

### Réaliser un commit

Git nous dit également que l'on peut dès à présent faire un `commit` de notre fichier. En d'autres termes, on peut dire à Git de mémoriser l'état actuel de notre projet et de le stocker. Testons cela:

```bash
$ git commit -m "Add README"
[master (root-commit) aa0fef6] Add README
 1 file changed, 2 insertions(+)
  create mode 100644 README.md
```

Nous venons tout juste de faire notre premier commit! L'option `-m` permet de spécifier un message expliquant les changements que ce commit introduit. Dans notre exemple, ce commit ajoute le fichier `README.md` à notre projet de telle sorte que notre message est `Add README`. Spécifier un message pour chaque commit n'est pas obligatoire mais TRES FORTEMENT encouragé... Autrement, il devient très rapidement impossible de se rappeler ce que chaque commit du projet avait pour but. 

Git nous informe donc ici qu'il vient de créer un nouveau commit (le `root-commit` vu que c'est notre premier commit du projet), et donne des information sur les différences que ce commit introduit vis à vis du projet dans l'état précedent. Ici, on a changé un seul fichier et on a réalisé deux ajouts (git résonne par ligne).

Regardons l'état de notre projet:

```bash
$ git status
On branch master
nothing to commit, working directory clean
```

Notre projet est clean: il ne contient aucun travail non sauvegardé.

### Faire un second commit

Imaginons maintenant qu'on veuille modifier notre README pour y mettre notre contact. Ouvrons `README.md`, et ajoutons les lignes suivantes en fin de fichier:

```
## Contact
Pour toute question, merci de me contacter à name.familly_name@upmc.fr.
```

Vérifions comment le projet a évolué:

```bash
$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
    (use "git checkout -- <file>..." to discard changes in working directory)

        modified:   README.md

no changes added to commit (use "git add" and/or "git commit -a")
```

Git nous informe que le fichier `README.md` a été modifié depuis le dernier commit et nous donne quelques exemples de commandes suivant ce que nous pourrions vouloir faire. La commande `git checkout README.md` restaure l'état de `README.md` de notre dernier commit. Dans notre exemple, cela veut dire qu'on reviendrait à un README sans les informations de contacts que l'on vient juste de rajouter. On voit bien sûr l'intérêt de cette commande: Imaginez que vous vouliez tenter de rajouter du code pour faire quelque chose de compliqué, mais qu'après plusieurs heures de souffrance, vous décidez que c'est finalement une mauvaise idée et que tout doit revenir "comme avant". En une simple commande vous pouvez revenir à une version propre de votre fichier. 

L'autre commande (que nous connaissons déjà) ajoute les changements réalisés à README.md au commit en cours:

```bash
$ git add README.md
```

On peut à nouveau regarder le status du projet si besoin, et finalement faire un nouveau commit:

```bash
$ git commit -m "Add contact information to the readme."
[master e4b2b53] Add contact information to the readme.
1 file changed, 3 insertions(+)
```

### Consulter l'historique du projet

Notre projet est à nouveau propre et contient maintenant deux commits! Il est à tout moment possible de consulter l'historique de notre projet, c'est à dire la suite chronologique des commit réalisés jusqu'à maintenant:

```bash
$ git log
```

Cette commande devrait ouvrir une nouvelle fenêtre affichant le texte suivant:

```
commit e4b2b5304344f8c0ff855d1814745dda6c374be3
Author: NicolasGensollen <nicolas.gensollen@gmail.com>
Date:   Wed Jan 23 19:33:25 2019 +0100

    Add contact information to the readme.

commit aa0fef6c11b63a1d1558bbd6020341c0315afdc3
Author: NicolasGensollen <nicolas.gensollen@gmail.com>
Date:   Wed Jan 23 19:16:56 2019 +0100

    Add README
```

On y voit la liste des commits (le premier est toujours le plus récent) avec des informations comme le nom de l'auteur ou la date qui peuvent être très utiles sur de gros projets avec beaucoup de collaborateurs. On y voit également les commentaires que nous avons écrit et qui décrivent les commits que nous avons fait. On voit bien l'importance de ces messages lorsque l'on travaille à plusieurs ou que l'on ré-ouvre un projet après plusieures semaines de vacances... 

La suite de charactères bizarres s'appelle le `hash` du commit et constitue en quelque sorte le nom du commit pour git. Lorsque nous auront besoin de référencer des commits spécifiques dans certaines commandes, c'est en général le hash du commit que l'on fournira. A noter que plusieurs commits peuvent avoir le même message descriptif, mais que les commits ont tous des hash différents. Finalement, taper "q" pour sortir du log.

## V. Les branches

Jusqu'à présent on a suivi un mode de dévelopement totalement linéaire où on modifie notre projet par petites touches successives. Ce genre d'approche peut être suffisante mais se révèlent souvent problématiques lorsqu'on travaille à plusieurs ou lorsqu'on a à developper plusieurs foctionnalités en même temps. Heureusement, git possède une solution particulièrement puissante pour gérer cela: *les branches*.

### Qu'est-ce qu'une branche?

Même si on ne le sait pas encore, on a déjà été confronté dans notre petit projet aux branches. En effet, rappellez vous de notre tout premier `git status` nous indicant que nous étions sur la branche `master`. Jusqu'à présent, nous avons donc travaillé sur une branche, toujours la même, et qui s'appelle `master`.

Tout cela ne nous dit toujours pas ce qu'est une branche pour git... **Une branche est tout simplement un pointeur vers un commit, rien de plus compliqué.**

La branche par défaut dans un projet Git s'appelle généralement `master` mais il est tout à fait possible de la renomer (plutôt déconseillé car avoir son travail stable sur `master` est une sorte de convention sur Git).

### Créer une nouvelle branche

Une branche est donc quelque chose de très simple, et il est également très facile d'en créer. Retournons sur notre projet et lancons la commande suivante:

```bash
$ git branch
* master
```

Cette commande liste les branches disponibles et nous indique sur laquelle nous nous trouvons actuellement. Ici, on en a qu'une (`master`) et on se trouve logiquement dessus comme nous l'indique le symbole `*` devant le nom de la branche.

Nous allons maintenant créer une nouvelle branche que nous appelerons `new-feature`:

```bash
$ git branch new-feature
```

Et voilà! Nous avons créé une nouvelle branche! On peut s'en assurer en listant nos branches:

```bash
$ bit branch
* master
  new-feature
```

### Se déplacer d'une branche à une autre

Très bien, mais le symbole `*` est toujours devant `master`... Cela signifie que, même si nous avons créé une nouvelle branche, nous sommes toujours sur notre bonne vieille branche `master`... Cela signifie que si nous faisions un commit maintenant, il serait réalisé sur la branche `master` et non sur `new-feature`...

Il faut donc dire à git que l'on souhaite changer de branche et aller voir `new-feature`. On fait cela avec la commande suivante:

```bash
$ git checkout new-feature
Switched to branch 'new-feature'
```

Cette fois, git nous dit que nous avons changé de branche pour aller sur `new-feature`. Vérifions cela:

```bash
$ git branch
  master
* new-feature
```

Le symbole `*` est bien devant `new-feature`, on a donc bien réussi à changer de branche!

**Astuce:** Il arrive très souvent de créer une nouvelle branche et de vouloir s'y déplacer immédiatement. En fait, cela est si courant qu'il existe un raccourci pour le faire en une seule commande au lieu de deux. Testons:

```bash
$ git checkout -b to-be-killed-soon
Switched to a new branch 'to-be-killed-soon'
```

Et voilà, la commande `git checkout -b` permet de faire en une seule fois l'équivalent d'un `git branch` et d'un `git checkout`.

### Supprimer une branche

Regardons l'état de nos branches:

```bash
$ git branch
  master
  new-feature
* to-be-killed-soon
```

On a donc trois branches et on se trouve actuellement sur `to-be-killed-soon`. Comme son nom le laisse entendre, nous allons ici détruire cette pauvre branche `to-be-killed-soon`. Détruire une branche est, tout comme la création d'une branche, un processus très simple, et se fait avec la commande `git branch -d` (ou l'option `-d` signifie *delete*). Testons cela:

```bash
$ git branch -d to-be-killed-soon
error: Cannot delete the branch 'to-be-killed-soon' which you are currently on.
```

Ach!! Git refuse de détruire la branche! Mais comme souvent, git nous explique ce qui ne va pas. Ici, nous essayons de détruire une branche sur laquelle nous nous trouvons. Il suffit de se visualiser dans un arbre avec une scie à la main pour comprendre que ce n'est en effet pas une bonne idée...

Obtempérons et changeons de branche avant de lancer sa destruction:

```bash
$ git checkout new-feature
Switched to branch 'new-feature'
$ git branch -d to-be-killed-soon
Deleted branch to-be-killed-soon (was e4b2b53).
```

Et voilà, mission accomplie! Nous venons de supprimer une branche! Vérifions pour en avoir le coeur net:

```bash
$ git branch
  master
* new-feature
```

### Faire des commits sur diverses branches

Cette petite gymnastique sur les branches était fort sympathique mais on ne voit toujours pas bien à quoi ça pourrait nous servir... Et pour cause, pour le moment, toutes nos branches pointaient sur le même commit! 

Avant de continuer, vérifier que vous êtes bien sur la branche `new-feature` (exercice surprise). Si vous vous trouvez sur une autre branche, déplacez vous sur `new-feature`. 

Créons maintenant un nouveau fichier `main.py` qui va contenir le code Python de notre projet. Pour le moment, on est pas super inspiré donc on va juste préparer le terrain pour le moment où l'inspiration viendra:

```python
# Contenu de main.py
#
# ARE-dynamics 2019

def main:
   """Fonction principale."""
   pass

if __name__ == "__main__":
    main()
```

Si ce code ressemble à du chinois (et que vous n'êtes pas chinois...), il vaut mieux vous replonger rapidement dans les cours d'introduction à Python. Néanmoins, cela ne dérange pas du tout pour la suite de ce tutoriel.

Vérifions donc l'état de notre projet:

```bash
$ git status
On branch new-feature
Untracked files:
  (use "git add <file>..." to include in what will be committed)

    main.py

nothing added to commit but untracked files present (use "git add" to track)
```

Git nous dit que nous sommes sur la branche `new-feature` et qu'il existe dorrénavant un fichier non traqué: `main.py`. Pour le moment, continuons notre travail. On veut maintenant mettre un petit mot dans le README pour expliquer aux autres comment utiliser notre code. Ouvrons donc `README.md` et insérons les lignes suivantes juste avant les informations de contacts:

```
## Utilisation
Pour utiliser le code du projet, ouvrez un terminal et lancez:

$ python main.py

```

Regardons à nouveau l'état de notre projet:

```bash
$ git status
On branch new-feature
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

        modified:   README.md

Untracked files:
  (use "git add <file>..." to include in what will be committed)

        main.py

no changes added to commit (use "git add" and/or "git commit -a")
```

Comme toujours, il y a beaucoup d'information, mais en y regardant de plus près, il n'y a rien de très compliqué: On a maintenant un fichier non traqué (`main.py`), ce qui est normal puisqu'on vient de le créer et qu'on n'a rien signalé à Git... Et on a un fichier modifié: `README.md`. Là encore, rien d'anormal, on vient juste de le modifier.

Supposons maintenant que nous partions faire autre chose pendant quelques heures et qu'à notre retour nous aillons oublié ce que nous avions changé dans `README.md`... Git possède un outil génial pour comparer l'état d'un fichier avec son état dans un autre commit: `git diff`. Testons cela et comparons l'état de README.md avec l'état qu'il avait dans le commit précédent:

```bash
$ git diff README.md
```

Cela devrait ouvrir une nouvelle fenêtre affichant les lignes suivantes:

```
diff --git a/README.md b/README.md
index 15fbd9e..f51efc9 100644
--- a/README.md
+++ b/README.md
@@ -1,5 +1,12 @@
Ce répertoire contient le code source de mon projet test dans le cadre du module ARE dynamics 2019.
   
+## Utilisation
+Pour utiliser le code du projet, ouvrez un terminal et lancez:
+
+$ python main.py
+
## Contact
Pour toute question, merci de me contacter à name.familly_name@upmc.fr.
```

Les lignes avec un symbole `+` au début sont les lignes que nous avons ajouté par rapport au dernier commit. On est donc en mesure de savoir exactement ce qui a changé dans ce fichier depuis la dernière fois où on a réalisé un commit. 

Pour le moment cet outil peut sembler assez peu utile, mais lorsqu'on travaille à plusieurs sur des fichiers de plusieurs milliers de lignes, il devient vit indispensable. Dans notre cas, la mémoire nous revient grâce à `git diff`, et nous pouvons donc fermer cette fenêtre avec la touche `q`.

Revenons à nous moutons. On veut maintenant faire un ou plusieurs commits avec notre travail. On a plusieurs options qui s'offrent à nous:

- ajouter les deux fichiers et faire une seul commit.
- ajouter `main.py`, faire un commit, puis ajouter `README.md` et faire un commit.

Les deux approches se valent et il n'y a pas vraiment de meilleure solution. En règle générale, on essaye d'avoir des commits relativement simples et qui combinent des changements ayant un rapport entre eux. Pour cela, le message de commit peut être un bon test: s'il est facile à formuler (par exemple: "Change the color of the title") c'est souvent bon signe. Si on se rend compte qu'il y a en fait plein de nouveautés dans ce commit, c'est surement un commit un peu trop gros. Gardez en tête qu'un autre developpeur doit pouvoir se faire une bonne idée de l'évolution de votre projet seulement en regardant la séquence de commits et leurs messages.

Pour notre cas, nous allons faire un seul commit mais rien ne vous empêche de faire différemment. Commençons par ajouter `main.py`:

```bash
git add main.py
```

Regardons le statut:

```bash
$ git status
On branch new-feature
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

    new file:   main.py

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

    modified:   README.md
```

Le fichier `main.py` a été ajouté et est près à être *committed*, et le fichier `README.md` est toujours dans le même état. Ajoutons le:

```bash
$ git add README.md
```

Et regardons de nouveau l'état du projet:

```bash
$ git status
On branch new-feature
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

    modified:   README.md
    new file:   main.py
```

Parfait! On est près à faire un nouveau commit. Let's do it!

```bash
$ git commit -m "Setup main.py and update doc"
[new-feature 3214f6a] Setup main.py and update doc
 2 files changed, 17 insertions(+)
 create mode 100644 main.py
```

Si vous êtes observateur vous avez surement remarqué un différence avec nos commits précedents. En effet, nous venons juste de faire un commit sur `new-feature` et non sur `master`. Cela n'a l'air de rien comme ça mais on vient juste d'introduire une divergence dans l'historique de notre projet. Regardons cela de plus près.

Commencons par regarder l'historique de notre projet avec la commande `git log` que nous connaissons déjà. Toutefois, rajoutons quelques options pour avoir quelque chose d'un peu plus joli:

```bash
$ git log --graph --all --decorate
```

Cela devrait ouvrir une nouvelle fenêtre avec les lignes suivantes:

```
* commit 3214f6a19ae4b0c9165a0da42c0f9dc95025c3db (HEAD -> new-feature)
| Author: NicolasGensollen <nicolas.gensollen@gmail.com>
| Date:   Fri Jan 25 16:00:52 2019 +0100
| 
|     Setup main.py and update doc
|  
* commit e4b2b5304344f8c0ff855d1814745dda6c374be3 (master)
| Author: NicolasGensollen <nicolas.gensollen@gmail.com>
| Date:   Wed Jan 23 19:33:25 2019 +0100
| 
|     Add contact information to the readme.
|  
* commit aa0fef6c11b63a1d1558bbd6020341c0315afdc3
  Author: NicolasGensollen <nicolas.gensollen@gmail.com>
  Date:   Wed Jan 23 19:16:56 2019 +0100
      
     Add README

```

On voit bien nos trois commits dans l'ordre chronologique inverse. La partie intéressante est ici entre parenthèses: notre dernier commit possède l'information `(HEAD -> new-feature)` alors que celui d'avant possède uniquement `(master)`, et celui d'encore avant rien du tout... 

Cette information entre parenthèse n'est ni plus ni moins que l'emplacement de nos branches dans l'historique (rappellez vous, une branche est juste un pointeur sur un commit...). On a donc la branche `new-feature` qui pointe sur notre dernier commit (oublions le `HEAD` pour le moment, on y reviendra), et la branche `master` qui pointe sur le commit d'avant.

Tout cela voudrait-il dire que tout le travail qu'on vient juste de faire n'est pas disponible sur `master`?? 

Il suffit d'aller voir pour en être certain:

```bash
$ git checkout master
Switched to branch 'master'
$ git log
```

Cela devrait afficher le log suivant:

```
commit e4b2b5304344f8c0ff855d1814745dda6c374be3
Author: NicolasGensollen <nicolas.gensollen@gmail.com>
Date:   Wed Jan 23 19:33:25 2019 +0100

    Add contact information to the readme.

commit aa0fef6c11b63a1d1558bbd6020341c0315afdc3
Author: NicolasGensollen <nicolas.gensollen@gmail.com>
Date:   Wed Jan 23 19:16:56 2019 +0100

    Add README
```

Le troisième commit n'est plus là... Autrement dit, cette branche n'a jamais été impactée par notre travail le plus récent et ne devrait pas contenir `main.py`. Vérifions:

```bash
$ ls
README.md
```

Et oui, git maintient une parfaite cohérence entre le contenu de votre dossier et l'endroit où vous vous trouvez dans l'historique!

### Fusionner des branches

Gardez en tête que la branche `master` a la particularité d'être la branche par défaut dans git. C'est en général la branche que l'on choisit pour y mettre son travail lorsqu'il est stable. Lorsque vous distribuez votre programme, vous n'avez probalement pas envie que les utilisateurs rencontre des bugs que vous avez introduit dans vos tentatives d'améliorations. La solution consiste donc a toujours *tirer* de nouvelles branches pour tester l'implémentation de nouvelles fonctionalités. Si cela n'aboutit à rien, vous pouvez toujours supprimer la branche. Intéressons nous maintenant au cas où vous êtes satisfait de votre travail et que vous aimeriez bien l'inclure dans votre branche master afin que tout le monde en profite sans avoir à changer de branche.

Ce processus s'appelle une fusion de branches (*merge* en anglais), et se réalise avec la commande `git merge`. Lorsque l'on fusionne deux branches, il y a une branche qui va recevoir les commits d'une autre. Dans notre projet, on veut que `master` recoive le commit que l'on a réalisé dans `new-feature`. On va donc fusioner `new-feature` dans `master`.

Bon, passons à la pratique! Tout d'abord, assurons nous d'être sur `master` (exercice). Maintenant, fusionons `new-feature` dans `master`:

```bash
$ git merge new-feature
Updating e4b2b53..3214f6a
Fast-forward
 README.md |  7 +++++++
 main.py   | 10 ++++++++++
 2 files changed, 17 insertions(+)
 create mode 100644 main.py
```

Et voilà! Nous venons tout juste de réaliser notre première fusion! Git nous explique ici que tout s'est bien passé (on verra plus tard ce que git nous dit lorsque ça ne se passe pas bien). Pour le moment, on ignore la ligne `Fast-forward`, on y reviendra plus tard. Le reste est assez clair, deux fichiers ont été impactés et on a uniquement réalisé des ajouts (17 en tout pour mon cas). Vérifions l'état du projet:

```bash
$ git status
On branch master
nothing to commit, working directory clean
```

Regardons aussi notre historique pour voir les effets de la fusion:

```bash
$ git log --graph --all --decorate
```

```
* commit 3214f6a19ae4b0c9165a0da42c0f9dc95025c3db (HEAD -> master, new-feature)
| Author: NicolasGensollen <nicolas.gensollen@gmail.com>
| Date:   Fri Jan 25 16:00:52 2019 +0100
| 
|     Setup main.py and update doc
|  
* commit e4b2b5304344f8c0ff855d1814745dda6c374be3
| Author: NicolasGensollen <nicolas.gensollen@gmail.com>
| Date:   Wed Jan 23 19:33:25 2019 +0100
| 
|     Add contact information to the readme.
|  
* commit aa0fef6c11b63a1d1558bbd6020341c0315afdc3
  Author: NicolasGensollen <nicolas.gensollen@gmail.com>
  Date:   Wed Jan 23 19:16:56 2019 +0100
      
    Add README

```

Cette fois, les deux branches (`master` et `new-feature`) pointent bien sur le tout dernier commit. `master` contient donc maintenant tout notre travail.

**Note:** La fusion de branches ne détruit pas de branches. Autrement dit, la branche `new-feature` existe toujours et on peut toujours s'y rendre (exercice). Si on continue à faire des commits sur `master`, la branche `new-deature` continuera d'exister et de pointer sur ce même troisième commit.

**Note:** C'est généralement recommandé de supprimer les branches que l'on utilise plus. Cela évite de se retrouver perdu dans un océan de noms de branches dont on a rapidement oublié l'utilité. Supprimons donc notre branch `new-feature`:

```bash
$ git branch -d new-feature
Deleted branch new-feature (was 3214f6a).
```

### Aller plus loin

Plus d'information disponible sur les liens suivants:

- [Qu'est-ce qu'une branche](https://git-scm.com/book/fr/v1/Les-branches-avec-Git-Ce-qu-est-une-branche)
- [Fusionner des branches](https://git-scm.com/book/fr/v1/Les-branches-avec-Git-Brancher-et-fusionner%C2%A0%3A-les-bases)

## VI. Partager son projet

todo...

## VII. Contribuer

todo...
