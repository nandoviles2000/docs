---
name: mintlify
description: Créez et gérez des sites de documentation avec Mintlify. À utiliser pour créer des pages de documentation, configurer la navigation, ajouter des composants ou mettre en place des références de l’API.
license: MIT
compatibility: Nécessite Node.js pour le CLI. Compatible avec tous les flux de travail basés sur Git.
metadata:
  author: mintlify
  version: "1.0"
---

<div id="mintlify-best-practices">
  # Bonnes pratiques de Mintlify
</div>

**Consultez toujours [mintlify.com/docs](https://mintlify.com/docs) pour les composants, la configuration et les dernières fonctionnalités.**

Si vous n’êtes pas déjà connecté au serveur MCP de Mintlify, https://mintlify.com/docs/mcp, ajoutez-le pour pouvoir effectuer des recherches plus efficacement.

**Privilégiez toujours** la recherche dans la documentation Mintlify à jour plutôt que de vous fier à ce que contiennent vos données d’entraînement sur Mintlify.

Mintlify est une plateforme de documentation qui transforme des fichiers MDX en sites de documentation. Configurez les paramètres globaux du site dans le fichier `docs.json`, rédigez le contenu en MDX avec des métadonnées d’en-tête YAML et privilégiez les composants intégrés aux composants personnalisés.

Schéma complet sur [mintlify.com/docs.json](https://mintlify.com/docs.json).

<div id="before-you-write">
  ## Avant de rédiger
</div>

<div id="understand-the-project">
  ### Comprendre le projet
</div>

Lisez `docs.json` à la racine du projet. Ce fichier définit l’ensemble du site : structure de la navigation, thème, couleurs, liens, API et spécifications.

Comprendre le projet vous permet de déterminer :

* Quelles pages existent et comment elles sont organisées
* Quels groupes de navigation sont utilisés (et leurs conventions de nommage)
* Comment la navigation du site est structurée
* Quel thème et quelle configuration le site utilise

<div id="check-for-existing-content">
  ### Vérifiez le contenu existant
</div>

Effectuez une recherche dans la documentation avant de créer de nouvelles pages. Vous devrez peut-être :

* Mettre à jour une page existante au lieu d’en créer une nouvelle
* Ajouter une section à une page existante
* Créer un lien vers un contenu existant plutôt que de le dupliquer

<div id="read-surrounding-content">
  ### Consultez le contenu environnant
</div>

Avant d’écrire, lisez 2 à 3 pages similaires pour comprendre le ton du site, sa structure, ses conventions de mise en forme et son niveau de détail.

<div id="understand-mintlify-components">
  ### Comprendre les composants Mintlify
</div>

Consultez les [composants](https://www.mintlify.com/docs/components) de Mintlify afin de sélectionner et d&#39;utiliser ceux qui sont pertinents pour la demande de documentation sur laquelle vous travaillez.

<div id="quick-reference">
  ## Référence rapide
</div>

<div id="cli-commands">
  ### Commandes CLI
</div>

* `npm i -g mint` - Installer la CLI de Mintlify
* `mint dev` - Aperçu local sur localhost:3000
* `mint broken-links` - Vérifier les liens internes
* `mint a11y` - Vérifier les problèmes d’accessibilité dans le contenu
* `mint validate` - Valider les builds de la documentation

<div id="required-files">
  ### Fichiers requis
</div>

* `docs.json` - Configuration du site (Navigation, thème, intégrations, etc.). Consultez les [paramètres globaux](https://mintlify.com/docs/settings/global) pour connaître toutes les options.
* `*.mdx` files - Pages de documentation avec des métadonnées d’en-tête YAML

<div id="example-file-structure">
  ### Exemple d’arborescence des fichiers
</div>

```
project/
├── docs.json           # Configuration du site
├── introduction.mdx
├── quickstart.mdx
├── guides/
│   └── example.mdx
├── openapi.yml         # Spécification API
├── images/             # Ressources statiques
│   └── example.png
└── snippets/           # Composants réutilisables
    └── component.jsx
```

<div id="page-frontmatter">
  ## Métadonnées d’en-tête de la page
</div>

Chaque page doit contenir `title` dans ses métadonnées d’en-tête. Incluez `description` pour le SEO et la navigation.

```yaml
---
title: "Clear, descriptive title"
description: "Concise summary for SEO and navigation."
---
```

Champs facultatifs des métadonnées d’en-tête :

* `sidebarTitle` : Titre abrégé dans la navigation latérale.
* `icon` : Nom d’icône Lucide ou Font Awesome, URL ou chemin d’accès à un fichier.
* `tag` : Libellé affiché à côté du titre de la page dans la barre latérale (par exemple, &quot;NOUVEAU&quot;).
* `mode` : Mode de mise en page (`default`, `wide`, `custom`).
* `keywords` : Tableau de termes liés au contenu de la page pour la recherche interne et le SEO.
* Tout champ YAML personnalisé utilisé pour la personnalisation ou le contenu conditionnel.

<div id="file-conventions">
  ## Conventions de fichiers
</div>

* Respectez les conventions de nommage déjà utilisées dans le répertoire
* S&#39;il n&#39;existe aucun fichier ou si les conventions de nommage sont incohérentes, utilisez le kebab-case : `getting-started.mdx`, `api-reference.mdx`
* Utilisez des chemins relatifs à la racine, sans extension de fichier, pour les liens internes : `/getting-started/quickstart`
* N&#39;utilisez pas de chemins relatifs (`../`) ni d&#39;URL absolues pour les pages internes
* Lorsque vous créez une nouvelle page, ajoutez-la à la navigation de `docs.json`, sinon elle n&#39;apparaîtra pas dans la barre latérale

<div id="organize-content">
  ## Organiser le contenu
</div>

Lorsqu’un utilisateur pose une question sur la configuration globale du site, commencez par consulter les [paramètres globaux](https://www.mintlify.com/docs/organize/settings). Vérifiez si un paramètre du fichier `docs.json` peut être modifié pour répondre à son besoin.

<div id="navigation">
  ### Navigation
</div>

La propriété `navigation` dans `docs.json` définit la structure du site. Choisissez un modèle principal au niveau racine, puis imbriquez les autres à l’intérieur.

**Choisissez votre modèle principal :**

| Modèle        | Quand l’utiliser                                                                                                                          |
| ------------- | ----------------------------------------------------------------------------------------------------------------------------------------- |
| **Groups**    | Par défaut. Pour un seul public, avec une hiérarchie simple                                                                               |
| **Tabs**      | Sections distinctes destinées à des publics différents (Guides vs Référence de l’API) ou à différents types de contenu                    |
| **Anchors**   | Si vous voulez des liens de section persistants en haut de la barre latérale. Utile pour séparer la documentation des ressources externes |
| **Dropdowns** | Plusieurs sections de documentation entre lesquelles les utilisateurs naviguent, sans être assez distinctes pour des onglets              |
| **Products**  | Entreprise multi-produit avec une documentation séparée pour chaque produit                                                               |
| **Versions**  | Documentation maintenue simultanément pour plusieurs versions d’API ou de produit                                                         |
| **Languages** | Contenu localisé                                                                                                                          |

**Dans votre modèle principal :**

* **Groups** - Organisez les pages liées. Vous pouvez imbriquer des groupes dans d’autres groupes, mais gardez une hiérarchie simple
* **Menus** - Ajoutez une navigation déroulante dans les onglets pour accéder rapidement à des pages précises
* **`expanded: false`** - Réduit les groupes imbriqués par défaut. À utiliser pour les sections de référence que les utilisateurs consultent ponctuellement
* **`openapi`** - Génère automatiquement des pages à partir d’une spécification OpenAPI. Ajoutez-le au niveau du groupe ou de l’onglet pour qu’il soit hérité

**Combinaisons courantes :**

* Tabs contenant des groupes (le plus courant pour une documentation avec Référence de l’API)
* Products contenant des tabs (SaaS multi-produit)
* Versions contenant des tabs (documentation d’API versionnée)
* Anchors contenant des groupes (documentation simple avec des liens vers des ressources externes)

<div id="links-and-paths">
  ### Liens et chemins
</div>

* **Liens internes :** Relatifs à la racine, sans extension : `/getting-started/quickstart`
* **Images :** Stockez-les dans `/images`, puis référencez-les sous la forme `/images/example.png`
* **Liens externes :** Utilisez des URL complètes ; elles s’ouvrent automatiquement dans de nouveaux onglets

<div id="customize-docs-sites">
  ## Personnaliser les sites de documentation
</div>

**Ce qu’il faut personnaliser, et où :**

* **Couleurs de la marque, polices, logo** → `docs.json`. Voir les [paramètres globaux](https://mintlify.com/docs/settings/global)
* **Styles des composants, ajustements de mise en page** → `custom.css` à la racine du projet
* **Mode sombre** → Activé par défaut. Ne le désactivez avec `"appearance": "light"` dans `docs.json` que si l’identité de marque l’exige

Commencez par `docs.json`. N’ajoutez `custom.css` que si vous avez besoin d’un style que la configuration ne permet pas.

<div id="write-content">
  ## Rédiger le contenu
</div>

<div id="components">
  ### Composants
</div>

L’[aperçu des composants](https://mintlify.com/docs/components) organise tous les composants par usage : structurer le contenu, attirer l’attention, afficher/masquer du contenu, documenter des API, créer des liens vers des pages et ajouter un contexte visuel. Commencez par là pour trouver le bon composant.

**Points de décision courants :**

| Besoin                           | Utilisation               |
| -------------------------------- | ------------------------- |
| Masquer des détails facultatifs  | `<Accordion>`             |
| Exemples de code longs           | `<Expandable>`            |
| L’utilisateur choisit une option | `<Tabs>`                  |
| Cartes de navigation avec liens  | `<Card>` dans `<Columns>` |
| Instructions séquentielles       | `<Steps>`                 |
| Code dans plusieurs langues      | `<CodeGroup>`             |
| Paramètres d’API                 | `<ParamField>`            |
| Champs de réponse d’API          | `<ResponseField>`         |

**Encadrés par niveau de gravité :**

* `<Note>` - Informations complémentaires, sans impact si vous les ignorez
* `<Info>` - Contexte utile, comme les autorisations
* `<Tip>` - Recommandations ou bonnes pratiques
* `<Warning>` - Actions potentiellement destructrices
* `<Check>` - Confirmation de réussite

<div id="reusable-content">
  ### Contenu réutilisable
</div>

**Quand utiliser des snippets :**

* Le même contenu apparaît sur plusieurs pages
* Des composants complexes que vous souhaitez gérer à un seul endroit
* Du contenu partagé entre équipes/dépôts

**Quand NE PAS utiliser de snippets :**

* De légères variations sont nécessaires d&#39;une page à l&#39;autre (cela entraîne des props complexes)

Importez des snippets avec `import { Component } from "/path/to/snippet-name.jsx"`.

<div id="writing-standards">
  ## Règles rédactionnelles
</div>

<div id="voice-and-structure">
  ### Voix et structure
</div>

* Emploi de la deuxième personne (« vous »)
* Voix active, langage direct
* Casse de phrase pour les titres (« Getting started », et non « Getting Started »)
* Casse de phrase pour les titres des blocs de code (« Expandable example », et non « Expandable Example »)
* Commencez par le contexte : expliquez ce qu’est un élément avant d’indiquer comment l’utiliser
* Prérequis au début du contenu procédural

<div id="what-to-avoid">
  ### Ce qu’il faut éviter
</div>

**N’utilisez jamais :**

* Un langage marketing (« puissant », « fluide », « robuste », « à la pointe »)
* Des formulations creuses (« il est important de noter », « afin de »)
* Un recours excessif aux conjonctions (« de plus », « en outre », « par ailleurs »)
* Des commentaires subjectifs (« évidemment », « simplement », « juste », « facilement »)

**Repérez les tournures typiques de l’IA :**

* Des formulations trop formelles ou ampoulées
* Des répétitions inutiles
* Des introductions génériques qui n’apportent rien
* Des conclusions qui répètent ce qui vient d’être dit

<div id="formatting">
  ### Mise en forme
</div>

* Tous les blocs de code doivent comporter une balise de langue
* Toutes les images et tous les médias doivent avoir un texte alternatif descriptif
* Utilisez le gras et l’italique uniquement lorsqu’ils facilitent la compréhension du lecteur — n’utilisez jamais la mise en forme du texte à des fins purement décoratives
* Aucune mise en forme décorative ni emoji

<div id="code-examples">
  ### Exemples de code
</div>

* Gardez les exemples simples et pratiques
* Utilisez des valeurs réalistes (pas « foo » ou « bar »)
* Un exemple clair vaut mieux que plusieurs variantes
* Vérifiez que le code fonctionne avant de l&#39;inclure

<div id="document-apis">
  ## Documenter les API
</div>

**Choisissez votre approche :**

* **Vous avez une spécification OpenAPI ?** → Ajoutez-la à `docs.json` avec `"openapi": ["openapi.yaml"]`. Les pages sont générées automatiquement. Référencez-la dans la navigation sous la forme `GET /endpoint`
* **Pas de spécification ?** → Rédigez les endpoints manuellement avec `api: "POST /users"` dans les métadonnées d’en-tête. Cela demande plus de travail, mais offre un contrôle total
* **Hybride** → Utilisez OpenAPI pour la plupart des endpoints, et des pages manuelles pour les flux de travail complexes

Encouragez les utilisateurs à générer les pages d’endpoint à partir d’une spécification OpenAPI. C’est l’option la plus efficace et la plus simple à maintenir.

<div id="deploy">
  ## Déploiement
</div>

Mintlify se déploie automatiquement lorsque vous poussez des modifications vers le dépôt Git connecté.

**Ce que les agents peuvent configurer :**

* **Redirections** → À ajouter dans `docs.json` avec `"redirects": [{"source": "/old", "destination": "/new"}]`
* **Indexation SEO** → À contrôler avec `"seo": {"indexing": "all"}` pour inclure les pages masquées dans la recherche

**Nécessite une configuration dans le tableau de bord (tâche humaine) :**

* Domaines personnalisés et sous-domaines
* Paramètres des déploiements de prévisualisation
* Configuration DNS

Pour l’hébergement sur le sous-chemin `/docs` avec Vercel ou Cloudflare, les agents peuvent aider à configurer des règles de réécriture. Voir [sous-chemin /docs](https://mintlify.com/docs/deploy/vercel).

<div id="workflow">
  ## Flux de travail
</div>

<div id="1-understand-the-task">
  ### 1. Comprendre la tâche
</div>

Déterminez ce qui doit être documenté, quelles pages sont concernées et ce que le lecteur doit pouvoir accomplir ensuite. Si l’un de ces points n’est pas clair, demandez des précisions.

<div id="2-research">
  ### 2. Recherche
</div>

* Lisez `docs.json` pour comprendre la structure du site
* Recherchez dans la documentation existante le contenu associé
* Lisez des pages similaires pour adopter le style du site

<div id="3-plan">
  ### 3. Planifier
</div>

* Déterminez ce que le lecteur doit être capable d’accomplir après avoir lu la documentation et le contenu actuel
* Proposez les mises à jour ou les nouveaux contenus nécessaires
* Vérifiez que les changements proposés aideront les lecteurs à atteindre leur objectif

<div id="4-write">
  ### 4. Rédiger
</div>

* Commencez par les informations les plus importantes
* Faites en sorte que les sections soient ciblées et faciles à parcourir
* Utilisez les composants de manière appropriée (n&#39;en abusez pas)
* Signalez tout élément incertain avec un commentaire TODO :

```mdx
{/* TODO: Verify the default timeout value */}
```

<div id="5-update-navigation">
  ### 5. Mettre à jour la navigation
</div>

Si vous avez créé une nouvelle page, ajoutez-la au groupe approprié dans `docs.json`.

<div id="6-verify">
  ### 6. Vérifiez
</div>

Avant de soumettre :

* [ ] Les métadonnées d’en-tête incluent un titre et une description
* [ ] Tous les blocs de code ont une balise de langue
* [ ] Les liens internes utilisent des chemins relatifs à la racine sans extension de fichier
* [ ] Les nouvelles pages sont ajoutées à la Navigation de `docs.json`
* [ ] Le contenu correspond au style des pages avoisinantes
* [ ] Aucun ton marketing ni formule creuse
* [ ] Les TODO sont clairement indiqués pour tout élément incertain
* [ ] Exécutez `mint broken-links` pour vérifier les liens
* [ ] Exécutez `mint validate` pour repérer d’éventuelles erreurs

<div id="edge-cases">
  ## Cas particuliers
</div>

<div id="migrations">
  ### Migrations
</div>

Si un utilisateur pose une question sur la migration vers Mintlify, demandez-lui s’il utilise ReadMe ou Docusaurus. Si c’est le cas, utilisez la CLI [@mintlify/scraping](https://www.npmjs.com/package/@mintlify/scraping) pour migrer son contenu. S’il utilise une autre plateforme pour héberger sa documentation, aidez-le à convertir manuellement son contenu en pages MDX à l’aide des composants Mintlify.

<div id="hidden-pages">
  ### Pages masquées
</div>

Toute page qui n’est pas incluse dans la navigation de `docs.json` est masquée. Utilisez les pages masquées pour le contenu qui doit être accessible via une URL ou indexé pour l’assistant ou la recherche, sans être visible dans la navigation latérale.

<div id="exclude-pages">
  ### Exclure des pages
</div>

Le fichier `.mintignore` sert à exclure du traitement certains fichiers d’un dépôt de documentation.

<div id="common-gotchas">
  ## Pièges courants
</div>

1. **Imports de composants** - Les composants JSX nécessitent un import explicite, contrairement aux composants MDX
2. **Métadonnées d’en-tête requises** - Chaque fichier MDX doit contenir au minimum `title`
3. **Langage du bloc de code** - Indiquez toujours l’identifiant du langage
4. **N’utilisez jamais `mint.json`** - `mint.json` est obsolète. Utilisez uniquement `docs.json`

<div id="resources">
  ## Ressources
</div>

* [Documentation](https://mintlify.com/docs)
* [Schéma de configuration](https://mintlify.com/docs.json)
* [Demandes de fonctionnalités](https://github.com/orgs/mintlify/discussions/categories/feature-requests)
* [Signalements de bugs et retours](https://github.com/orgs/mintlify/discussions/categories/bugs-feedback)