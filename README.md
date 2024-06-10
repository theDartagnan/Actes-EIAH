# Actes Latex EIAH / RJC-EIAH

Ce projet fourni un modèle complet d'actes de conférences francophones fondés sur le format LNCS, initialement prévu pour les conférences EIAH et RJC-EIAH.

## Prerequis

- Connaissances de base de LateX
- Editeur et compilateur LateX
- package LateX requis

## Principe général

- Chaque article de la conférence doit être au préalable produit au format __pdf__, sans en-tête ni pied de page (donc pas de mention d'auteur ou de titre en en-tête ni numérotion de page en pied de page), et doit respecter une mise en page au format exigé par la conférence (ce modèle ne permet pas la vérification automatique du respect du format).
- le fichier principal des actes __actes.tex__ est à adapter pour les actes (ex.: édtieurs, couleur principale du document, liste des articles à intégrer). Les sections ci-dessous présente comment réaliser cette adaptation.
- d'autres fichiers .tex peuvent être fourni pour les autres sections des actes (ex.: introduction, comité de programme). Des exemples sont fournis ici.
- les actes sont prévues pour une publication de type livre (lecture sur 2 pages).

## Structure du projet

- __actes.tex__ : point d'entrée Latex. Contient la structure de l'ensemble du manuscrit et la définition des commandes principales.
- __VendorPDF/__ : dossier des fichiers pdf de chaque article des actes.
- __Content/__ : contient les fichiers Latex des autres sections (ex.: comité, conférenciers invité, pages de garde et de fin...) ansi que le dossier des illustrations des actes __figures__ (logo des partenaires, de la conférence...)

## Préparation des actes

La préparation se fait au sein du fichier __actes.tex__.

### Informations générales

- _ligne 36_ : couleur principale des titres principaux : peut-être par exemple en accord avec la charte graphique de l'hôte de la conférence.
- _lignes 39-41_ : en-têtes des pages hors articles : Auteurs des actes en pages paires, titre des actes en pages impaires.
- _lignes 44-48_ : logo de la conférence : lien vers le logo de la conférence (utilisé à plusieurs reprise : page de garde, pages de titre de session, page de fin).
- _ligne 135_ : titre de la conférence.
- _lignes 138 et 139_ : auteurs des actes.

### contenu avant articles

Plusieurs pages particulières et sections peuvent être ajoutées en amont des articles des actes. Ce projet propose la structure suivante entre les lignes 142 à 171 : 
- page de garde ;
- Table des matière ;
- Comités de programme, d'organisation... ;
- Introduction aux actes ;
- Présentation des conférenciers invités.

Pour chaque section après la table des matières, le contenu est situé dans un fichier .tex dédié du dossier _Content_. Après une section, la commande \newpage permet de forcer le passage à la page suivante. 

Si une page débute par le logo de la conférence (ex.: Introduction) par la commande __\logoConf__, il peut être souhaitable d'aligner verticalement les titres des autres section pour garantir d'une homogénéité visuelle. Dans ce cas, les sections sans le logo seront précédées par un espace blanc __\vspace*{2em}__.

Les commandes __\startOnOddPage__ (exemple _ligne 145_)permettent d'assurer que le contenu suivant la commande soit affiché sur une page impaire.

### Articles de conférence

Le manuscrit présente ici les articles de la conférence organisés par les sessions de présentation. Pour chaque session une page de titre est générée mentionnant le nom de la session et son animateur. Viennent ensuite les différents articles de la session. Chaque nouvelle session commence sur une page impaire (droite). Pour chaque article, les en-têtes sont adaptés pour afficher les auteurs et le titre de l'article et non pas les auteurs et titre des actes.

#### Rappel

Chaque article des actes doit être un fichier __pdf__, situé dans le dossier VendorPDF, respectant les règles suivantes :
- sans en-têtes ni pied de page (donc pas de mention d'auteur ou de titre en en-tête ni numérotion de page en pied de page), et respecter la mise en page au format LLNCS (marges etc.).
- respect de la mise en page exigé par la conférence (la vérification n'est pas prise en charge par ce projet).

#### Page de titre de la session

La page de titre de la session est inclue par la commande __\pageTitreSession__ (ex.: ligne 174). Le paramètre de la commande est le sous-titre de la page (ex.: "Animateur de session : ...") ; le contenu suivant est le titre de la page (ex.: "Session de communication : Conception pour les jeux sérieux").

Exemple :
```
\pageTitreSession[Animateur de session : Sébastien Jolivet]{Session de communications 1 : Conception pour les jeux sérieux}
```

#### Insertion des articles

les articles sont positionnés avec la structure suivante (ex. d'une session d'articles des lignes 177 à 183).

Un nouvel article est ajouté à l'aide de la commande __\addpaper__ (ex.: ligne 189). Cette commande accepte 5 paramètres :
1. le nom de l'auteur ;
2. le titre court de l'article ;
3. le titre long de l'article ;
4. l'identifiant unique de l'article (choix arbitraire mais l'identifiant doit être unique pour chaque article des actes) ;
5. le chemin vers le pdf de l'article.

Chaque nouvel article sera ajouté de manière à ce qu'il commence sur une page paire (gauche).

Exemple :
```
\addpaper{Sophie Chane-Lune}{Un référentiel de compétences en programmation}{Un référentiel de compétences en programmation pour construire des ressources et des évaluations}{ART20}{VendorPDF/RJC-EIAH_2024_Sources_20.pdf}
```

Après avoir inséré toutes les sessions de présentation et article la comande __\resetHeadings__ permet de remettre les en-têtes généraux des actes (auteurs et titre des actes). Elle est automatiquement invoquée par la commande __\pageTitreSession__ (pour avoir les en-têtes généraux sur la page de titre de session), mais est à appeler après l'article de la dernière session pour retrouver les en-têtes généraux sur les pages suivantes.

#### Détails de la commande \includepdf

Exemple : 

```
\includepdf[pages={-}, pagecommand={\markboth{Estelle Prior}{Partage des savoirs dans une réunion de co-conception de jeux épistémiques numériques...}}, fitpaper=false, addtotoc={1, subsection, 2, Partage des savoirs dans une réunion de co-conception de jeux épistémiques numériques en recherche orientée par la conception\newline\textit{Estelle Prior}, ART10}]{VendorPDF/10.pdf}
```

### Contenu après articles de fin

Plusieurs pages particulière, ou sections peuvent être ajoutées en aval des articles des actes. Ce projet propose la structure suivante :
- présentation les ateliers et Symposia ;
- partenaires ;
- page de fin.

Comme pour les sections avant articles, le contenu de ces sections est situé dans un fichier .tex dédié du dossier _Content_. Après une section, la commande \newpage permet de forcer le passage à la page suivante.

## Compilation

La compilation Latex peut être faite à la main en ligne de commande ou automatisé par un IDE comme TexStudio.

Il est recommandé d'utiliser un éditeur Tex intégré comme TexStudio.

À la main, la commande `pdflatex actes.tex` permet de compiler et générer un fichier pdf, mais doit être exécutée au moins 2 fois de suite pour générer un fichier pdf complet (incluant la table des matières notamment).
