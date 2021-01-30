![Gautoz logo](assets/social.jpg)

# Gautoz

Ce repo contient les sources et le contenu du site de [Gautoz](https://twitter.com/gautoz). 

## Comment ajouter des pages dans une sous-section (exemple : matinales)

1. Aller dans le dossier désiré, par exemple `/matinales`
2. Cliquer sur `add file` ou `ajouter un fichier`
3. Nommer le fichier à la date voulue auf format `jour-mois-année`
4. Ne pas oublier de lui donner une extension `.md`
5. Remplir le fichier avec le contenu voulu
6. Enregistrer

Le nouveau fichier déclenchera la reconstruction du site et sous quelques minutes, la nouvelle page apparaîtra. Le fichier RSS disponible via l'url `/feed.xml` sera aussi mis à jour.

## Customiser la page d'accueil et les pages intermédiaires

- Le contenu de la page d'accueil se trouve dans le fichier `home.md`. Il peut être rédigé comme n'importe quel fichier markdown.
- Le contenu de la page matinales se trouve dans `matinales/index.md`. Comme la page d'accueil, il peut être rédigé comme n'importe quelle autre page.

La seule différence avec une page classique est que **la page d'accueil et les pages intermédiaires listent automatiquement le contenu des sous-dossiers par ordre chronologique inversé**.

La page d'accueil ne liste que les 5 dernières entrées, tandis que la page intermédiaire liste toutes les entrées.

En modifiant le fichier `src/config.py` il est possible de changer :

- Le nom du site via `siteName`
- La meta description du site via `siteMetaDescription`
- Le compte twitter utilisé lors des embeds twitter via `twitterName`

## Comment ajouter une nouvelle section 

Le site est prévu pour accueillir autant de sous-sections que nécessaire. Pour en ajouter une :

1. Ajouter un dossier à la racine du projet, par exemple `blog/`
2. Dans `/blog`, ajouter `index.md` afin de créer la page intermédiaire.
3. Dans le fichier `src/config.py`, ajouter le nom de cette nouvelle sous-section dans la variable `contentFolder`. Par exemple : `['matinales', 'blog']`

La nouvelle section `blog` est prête, il suffit maintenant d'ajouter des pages. Le contenu de cette nouvelle sous-section sera automatiquement listé sur la page d'accueil.

## Détails techniques

Les fichiers utilisés pour construire le site sont :

- `src/config.py` contient la configuration pour certaines étapes de la construction du site comme les url, le nom des fichiers, etc
- `src/build.py` est le fichier créant le site en lui-même.
- `src/mistune.py` est le parser markdown utilisé pour générer le contenu en HTML.
- `assets/` contient les images et le fichier de style du site.
- `partials/` content le fichier de templating du site.
- `docs/` contient la version buildée du site.
- `kantan.sh` est un script pour créer un environnement de développement.

Lors du build, le script génère les pages HTML à partir des fichiers markdown, puis génère les pages intermédiaires et la page d'accueil. Enfin, il copie le contenu du dossier assets dans un dossier du même nom.

Il existe deux méthodes pour construire le site:

- `python3 src/build.py` construit le site avec une URL _relative_, à savoir `/`.
- `python 3 src/build.py --prod` construit le site avec une URL _absolue_, par exemple `gautoz.com`.

L'url absolue est à renseigner dans le fichier `src/config.py`.

## Automatisation de la mise en ligne via la branche `github-pages`

Le site est automatiquement reconstruit à chaque changement via une github action nommée `build and deploy`. Celle-ci crée un environnement permettant l'execution de `build.py`, puis copie le site généré dans la branche `github-pages`. Celle-ci est ensuite utilisée par github pour afficher le site.
