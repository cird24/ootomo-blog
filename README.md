# Blog ootomo.ca

Chaque fichier `posts/*.md` devient un article sur https://www.ootomo.ca/blog.
Le site relit ce dépôt toutes les 5 minutes : aucun déploiement du site n'est nécessaire.

## Le plus simple (agents du vault, dont Grok)

Écrire le fichier dans le vault : `Projets/Ootomo/Blog/posts/<slug>.md`. Le Lenovo le publie ici toutes les 10 minutes (aucun jeton). Mode d'emploi : `Projets/Ootomo/Blog/README.md`. Le dossier du vault fait foi : un article modifié ou supprimé directement ici sera écrasé ou remis.

## Publier un article

1. Créer `posts/<slug>.md` (slug = minuscules, chiffres, tirets ; ex. `facturer-plus-vite.md`).
   L'adresse sera `https://www.ootomo.ca/blog/<slug>`.
2. Commencer le fichier par cet en-tête, puis le texte en Markdown :

```markdown
---
title: Facturer plus vite sans logiciel compliqué
date: 2026-11-03
description: Une phrase qui résume l'article (aperçu et Google).
draft: false
---

Le texte de l'article. **Gras**, listes, liens, intertitres `##`.
```

- `title`, `date` (AAAA-MM-JJ) et `description` sont obligatoires ; sans eux l'article est ignoré.
- `draft: true` garde l'article hors ligne.
- Le HTML brut est retiré à l'affichage : Markdown seulement.
- Pour modifier ou retirer un article : modifier ou supprimer le fichier.

## Pour un agent (API GitHub)

Un seul appel crée ou met à jour un article :

```
PUT https://api.github.com/repos/cird24/ootomo-blog/contents/posts/<slug>.md
Authorization: Bearer <jeton avec droit Contents: write sur ce dépôt>
{ "message": "post: <slug>", "content": "<fichier en base64>", "sha": "<sha actuel, seulement pour une mise à jour>" }
```

Ton du site : simple, rassurant, sans jargon (pas de « n8n » ni « LLM »), pas de promesse chiffrée, pas d'abonnement obligatoire.
