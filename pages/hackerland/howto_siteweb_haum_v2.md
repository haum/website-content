---
title: Comment modifier le contenu du site web
slug: comment-modifier-le-contenu-du-site-web
summary: Écrire un article, corriger une page, ajouter un évènement à l'agenda.
---

Le site du **HAUM** est un espace collaboratif que chaque membre peut enrichir. Tout le contenu est écrit en [Markdown](https://www.markdownguide.org/basic-syntax/) dans le dépôt [website-content](https://github.com/haum/website-content/) : pas besoin d'installer quoi que ce soit pour écrire.

## Écrire un article

1. Sur la page [Articles](/articles/), cliquez sur **Proposer un article**. GitHub ouvre un nouveau fichier `articles/mon-article/index.md` avec un modèle déjà rempli.
2. Renommez le dossier `mon-article` (dans le champ du nom de fichier) et complétez l'en-tête ; c'est le `slug` qui donne l'adresse de la page :

   ```yaml
   ---
   title: Ma lampe connectée
   slug: ma-lampe-connectee   # → haum.org/ma-lampe-connectee.html
   date: 2026-10-13T20:00:00
   authors: [Pseudo]
   categories: [hack]         # news, hack, tuto, projets…
   tags: [esp32, led]
   summary: Une phrase qui donne envie de lire la suite.
   ---
   ```

3. Écrivez votre texte en dessous, puis **Commit changes**.

Sans droits d'écriture sur le dépôt, GitHub vous propose automatiquement d'en faire une *pull request* : un membre la relira et la fusionnera.

### Ajouter des photos

Une fois l'article créé, ouvrez son dossier sur GitHub, puis **Add file → Upload files** et déposez vos photos. Dans le texte :

```markdown
![Le prototype sur l'établi](prototype.jpg)

![Avec une légende](montage.jpg "Montage final au local")
```

Inutile de redimensionner les photos de téléphone : le site les réduit automatiquement.

## Corriger ou compléter une page

Chaque page du site a un lien **Modifier cette page** en bas : il ouvre directement le bon fichier dans l'éditeur de GitHub. Corrigez, décrivez votre modification en une phrase (par exemple « Ajout des horaires dans Nous rejoindre »), puis **Commit changes**.

Les pages de projets se trouvent dans `pages/projets/`. En plus du titre, leur en-tête accepte une bannière et deux badges :

```yaml
banner: /images/bannieres_projets/mon-projet.1.jpg
# couleurs : brightgreen, yellow, red, lightgrey
realisation: { label: en cours, color: yellow }
etat: { label: fonctionnel, color: brightgreen }
```

## Photos de la page d'accueil

La page d'accueil affiche une photo au hasard parmi celles du dossier [`images/accueil/`](https://github.com/haum/website-content/tree/master/images/accueil) : déposez-y vos plus belles photos de la vie du local (« Add file → Upload files »). Le nom du fichier sert de légende : `atelier-soudure.jpg` devient « Atelier soudure ». Évitez les photos avec du texte incrusté et celles où des personnes reconnaissables n'ont pas donné leur accord.

## Mettre le site en ligne

Les modifications apparaissent sur le site après une mise à jour lancée depuis le {{< matrix >}} par une personne habilitée :

```
!updatesite
```

## L'agenda

L'agenda se gère aussi depuis le {{< matrix >}} :

```
!agenda list
!agenda add 2026-10-20 20:30 | Session bidouille | Local du HAUM | Venez avec vos projets !
!agenda del 42
```

Lancez ensuite `!updatesite` pour publier. Les évènements passés disparaissent d'eux-mêmes du site, même sans nouvelle mise à jour.

## Indiquer que le local est ouvert

En arrivant au local, et en partant, dites-le au {{< matrix >}} :

```
!local ouvert
!local fermé
!local
```

Le badge « Local ouvert / fermé » du site change aussitôt, sans `!updatesite`. `!local` seul affiche le statut et depuis quand il est indiqué.

## Travailler sur sa machine (facultatif)

Pour prévisualiser vos changements ou modifier l'apparence du site, il vous faut [git](https://git-scm.com/) et [Hugo](https://gohugo.io/installation/) (un seul exécutable, version 0.156 ou plus récente) :

```sh
git clone git@github.com:haum/website.git
cd website
git clone git@github.com:haum/website-content.git content
make serve        # http://localhost:1313, mise à jour à chaque enregistrement
```

Pour un nouvel article : `hugo new articles/ma-lampe/index.md`. L'apparence du site se trouve dans `layouts/` (gabarits) et `assets/css/main.css` (styles).

Une fois satisfait, depuis le dossier `content` : `git add`, `git commit -m "…"`, `git push`.

### Des liens qui peuvent servir

- [Mémo de la syntaxe Markdown](https://www.markdownguide.org/cheat-sheet/)
- [Documentation de Hugo](https://gohugo.io/documentation/)
- [Ce que j’aurais aimé savoir quand j’ai commencé Git](https://lilobase.wordpress.com/2014/05/12/a-la-decouverte-de-git/)
