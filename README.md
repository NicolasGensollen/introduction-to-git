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

todo...

## VI. Partager son projet

todo...

## VII. Contribuer

todo...
