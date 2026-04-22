---
name: mintlify
description: Créez et maintenez des sites de documentation avec Mintlify. À utiliser pour créer des pages de documentation, configurer la navigation, ajouter des composants ou mettre en place des références de l’API.
license: MIT
compatibility: Nécessite Node.js pour la CLI. Fonctionne avec n’importe quel flux de travail basé sur Git.
metadata:
  author: mintlify
  version: "1.0"
---

<div id="mintlify-best-practices">
  # Bonnes pratiques de Mintlify
</div>

**Consultez toujours [mintlify.com/docs](https://mintlify.com/docs) pour les composants, la configuration et les dernières fonctionnalités.**

Si vous n’êtes pas déjà connecté au serveur MCP de Mintlify, https://mintlify.com/docs/mcp, ajoutez-le pour effectuer vos recherches plus efficacement.

**Privilégiez toujours** la recherche dans la documentation Mintlify à jour plutôt que de vous fier à ce que contiennent vos données d’entraînement sur Mintlify.

Mintlify est une plateforme de documentation qui transforme les fichiers MDX en sites de documentation. Configurez les paramètres du site dans le fichier `docs.json`, rédigez le contenu en MDX avec des métadonnées d’en-tête YAML, et privilégiez les composants intégrés aux composants personnalisés.

Schéma complet sur [mintlify.com/docs.json](https://mintlify.com/docs.json).

<div id="before-you-write">
  ## Avant de rédiger
</div>

<div id="understand-the-project">
  ### Comprendre le projet
</div>

Lisez `docs.json` à la racine du projet. Ce fichier définit l’ensemble du site : structure de la navigation, thème, couleurs, liens, API et spécifications.

Comprendre le projet vous permet de savoir :

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
* Créer un lien vers du contenu existant plutôt que de le dupliquer

<div id="read-surrounding-content">
  ### Consultez le contenu connexe
</div>

Avant d’écrire, lisez 2 à 3 pages similaires pour comprendre le ton du site, sa structure, ses conventions de mise en forme et son niveau de détail.

<div id="understand-mintlify-components">
  ### Comprendre les composants Mintlify
</div>

Consultez les [composants](https://www.mintlify.com/docs/components) Mintlify afin de sélectionner et d’utiliser les composants pertinents pour la demande de documentation sur laquelle vous travaillez.

<div id="quick-reference">
  ## Aide-mémoire
</div>

<div id="cli-commands">
  ### Commandes CLI
</div>

* `npm i -g mint` - Installez la CLI Mintlify
* `mint dev` - Aperçu local sur localhost:3000
* `mint broken-links` - Vérifiez les liens internes
* `mint a11y` - Vérifiez les problèmes d’accessibilité du contenu
* `mint validate` - Validez les builds de la documentation

<div id="required-files">
  ### Fichiers requis
</div>

* `docs.json` - Configuration du site (Navigation, thème, intégrations, etc.). Consultez les [paramètres globaux](https://mintlify.com/docs/settings/global) pour connaître toutes les options.
* Fichiers `*.mdx` - Pages de documentation avec des métadonnées d’en-tête YAML

<div id="example-file-structure">
  ### Exemple de structure de fichier
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

Chaque page doit inclure `title` dans ses métadonnées d’en-tête. Incluez `description` pour le SEO et la navigation.

```yaml
---
title: "Clear, descriptive title"
description: "Concise summary for SEO and navigation."
---
```

Champs facultatifs des métadonnées d’en-tête :

* `sidebarTitle` : Titre court dans la barre latérale.
* `icon` : Nom d’icône Lucide ou Font Awesome, URL ou chemin d’accès au fichier.
* `tag` : Libellé affiché à côté du titre de la page dans la barre latérale (par exemple, &quot;NOUVEAU&quot;).
* `mode` : Mode de mise en page (`default`, `wide`, `custom`).
* `keywords` : Liste de termes liés au contenu de la page pour la recherche locale et le SEO.
* Tout champ YAML personnalisé à utiliser pour la personnalisation ou le contenu conditionnel.

<div id="file-conventions">
  ## Conventions de fichiers
</div>

* Respectez les conventions de nommage déjà utilisées dans le répertoire
* S&#39;il n&#39;existe aucun fichier ou si les conventions de nommage sont incohérentes, utilisez le format kebab-case : `getting-started.mdx`, `api-reference.mdx`
* Utilisez des chemins relatifs à la racine, sans extension de fichier, pour les liens internes : `/getting-started/quickstart`
* N&#39;utilisez pas de chemins relatifs (`../`) ni d&#39;URL absolues pour les pages internes
* Lorsque vous créez une page, ajoutez-la à la navigation de `docs.json`, sinon elle n&#39;apparaîtra pas dans la barre latérale

<div id="organize-content">
  ## Organiser le contenu
</div>

Lorsqu’un utilisateur pose une question sur une configuration à l’échelle du site, commencez par consulter les [paramètres globaux](https://www.mintlify.com/docs/organize/settings). Vérifiez si un paramètre du fichier `docs.json` peut être modifié pour obtenir le résultat souhaité par l’utilisateur.

<div id="navigation">
  ### Navigation
</div>

La propriété `navigation` dans `docs.json` détermine la structure du site. Choisissez un schéma principal au niveau racine, puis imbriquez les autres en son sein.

**Choisissez votre schéma principal :**

| Pattern       | Quand l’utiliser                                                                                                                             |
| ------------- | -------------------------------------------------------------------------------------------------------------------------------------------- |
| **Groups**    | Par défaut. Un seul public, hiérarchie simple                                                                                                |
| **Tabs**      | Sections distinctes pour différents publics (Guides vs Référence de l’API) ou différents types de contenu                                    |
| **Anchors**   | Si vous voulez des liens de section persistants en haut de la barre latérale. Pratique pour séparer la documentation des ressources externes |
| **Dropdowns** | Plusieurs sections de documentation entre lesquelles les utilisateurs naviguent, mais pas assez distinctes pour justifier des onglets        |
| **Products**  | Entreprise multi-produit avec une documentation distincte pour chaque produit                                                                |
| **Versions**  | Documentation maintenue simultanément pour plusieurs versions d’API ou de produit                                                            |
| **Languages** | Contenu localisé                                                                                                                             |

**Dans votre schéma principal :**

* **Groups** - Organisez les pages connexes. Vous pouvez imbriquer des groupes dans des groupes, mais gardez une hiérarchie peu profonde
* **Menus** - Ajoutez une navigation déroulante dans les onglets pour accéder rapidement à des pages précises
* **`expanded: false`** - Réduit les groupes imbriqués par défaut. À utiliser pour les sections de référence que les utilisateurs consultent ponctuellement
* **`openapi`** - Génère automatiquement des pages à partir d’une spécification OpenAPI. Ajoutez-le au niveau du groupe ou de l’onglet pour qu’il soit hérité

**Combinaisons courantes :**

* Des onglets contenant des groupes (le plus courant pour une documentation avec référence d’API)
* Des produits contenant des onglets (SaaS multi-produit)
* Des versions contenant des onglets (documentation d’API versionnée)
* Des ancres contenant des groupes (documentation simple avec des liens vers des ressources externes)

<div id="links-and-paths">
  ### Liens et chemins
</div>

* **Liens internes :** Relatifs à la racine, sans extension : `/getting-started/quickstart`
* **Images :** Stockez-les dans `/images` et référencez-les sous la forme `/images/example.png`
* **Liens externes :** Utilisez des URL complètes ; elles s’ouvrent automatiquement dans de nouveaux onglets

<div id="customize-docs-sites">
  ## Personnaliser les sites de documentation
</div>

**Que personnaliser, et où :**

* **Couleurs de la marque, polices, logo** → `docs.json`. Voir les [paramètres globaux](https://mintlify.com/docs/settings/global)
* **Style des composants, ajustements de mise en page** → `custom.css` à la racine du projet
* **Mode sombre** → Activé par défaut. Désactivez-le uniquement avec `"appearance": "light"` dans `docs.json` si la marque l’exige

Commencez par `docs.json`. N’ajoutez `custom.css` que si vous avez besoin d’une personnalisation du style que la configuration ne permet pas.

<div id="write-content">
  ## Rédiger du contenu
</div>

<div id="components">
  ### Composants
</div>

La [vue d’ensemble des composants](https://mintlify.com/docs/components) classe tous les composants par usage : structurer le contenu, attirer l’attention, afficher ou masquer du contenu, documenter des API, créer des liens vers des pages et ajouter un contexte visuel. Commencez par là pour trouver le composant adapté.

**Cas d’usage courants :**

| Besoin                           | Utiliser                  |
| -------------------------------- | ------------------------- |
| Masquer des détails facultatifs  | `<Accordion>`             |
| Exemples de code longs           | `<Expandable>`            |
| L’utilisateur choisit une option | `<Tabs>`                  |
| Cartes de navigation avec liens  | `<Card>` dans `<Columns>` |
| Instructions séquentielles       | `<Steps>`                 |
| Code en plusieurs langues        | `<CodeGroup>`             |
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
* Du contenu partagé entre plusieurs équipes/dépôts

**Quand NE PAS utiliser de snippets :**

* De légères variations sont nécessaires selon la page (ce qui entraîne des props complexes)

Importez des snippets avec `import { Component } from "/path/to/snippet-name.jsx"`.

<div id="writing-standards">
  ## Règles de rédaction
</div>

<div id="voice-and-structure">
  ### Voix et structure
</div>

* Adresse directe à la deuxième personne (« vous »)
* Voix active, langage direct
* Casse de phrase pour les titres (« Premiers pas », et non « Premiers Pas »)
* Casse de phrase pour les titres des blocs de code (« Exemple déroulant », et non « Exemple Déroulant »)
* Commencez par le contexte : expliquez ce qu’est un élément avant d’expliquer comment l’utiliser
* Prérequis au début des procédures

<div id="what-to-avoid">
  ### Ce qu’il faut éviter
</div>

**N’utilisez jamais :**

* Un langage marketing (&quot;puissant&quot;, &quot;fluide&quot;, &quot;robuste&quot;, &quot;de pointe&quot;)
* Des formules creuses (&quot;il est important de noter&quot;, &quot;afin de&quot;)
* Un usage excessif des conjonctions (&quot;de plus&quot;, &quot;en outre&quot;, &quot;par ailleurs&quot;)
* Des commentaires éditoriaux (&quot;évidemment&quot;, &quot;simplement&quot;, &quot;juste&quot;, &quot;facilement&quot;)

**Soyez attentif aux tournures typiques de l’IA :**

* Des formulations trop formelles ou guindées
* Des répétitions inutiles
* Des introductions génériques qui n’apportent rien
* Des résumés de conclusion qui répètent ce qui vient d’être dit

<div id="formatting">
  ### Mise en forme
</div>

* Tous les blocs de code doivent comporter des balises de langue
* Toutes les images et tous les médias doivent avoir un texte alternatif descriptif
* Utilisez le gras et l’italique uniquement lorsqu’ils facilitent la compréhension du lecteur — n’utilisez jamais la mise en forme du texte à des fins purement décoratives
* Aucune mise en forme décorative ni aucun emoji

<div id="code-examples">
  ### Exemples de code
</div>

* Gardez les exemples simples et pratiques
* Utilisez des valeurs réalistes (pas « foo » ni « bar »)
* Un exemple clair vaut mieux que plusieurs variantes
* Vérifiez que le code fonctionne avant de l’inclure

<div id="document-apis">
  ## Documenter les API
</div>

**Choisissez votre approche :**

* **Vous avez une spécification OpenAPI ?** → Ajoutez-la à `docs.json` avec `"openapi": ["openapi.yaml"]`. Les pages sont générées automatiquement. Référencez-les dans la navigation sous la forme `GET /endpoint`
* **Pas de spécification ?** → Rédigez les endpoints manuellement avec `api: "POST /users"` dans les métadonnées d’en-tête. Cela demande plus de travail, mais vous donne un contrôle total
* **Hybride** → Utilisez OpenAPI pour la plupart des endpoints, et des pages manuelles pour les flux de travail complexes

Encouragez les utilisateurs à générer les pages d’endpoint à partir d’une spécification OpenAPI. C’est l’option la plus efficace et la plus simple à maintenir.

<div id="deploy">
  ## Déploiement
</div>

Mintlify se déploie automatiquement lorsque des modifications sont poussées vers le dépôt Git connecté.

**Ce que les agents peuvent configurer :**

* **Redirections** → Ajoutez-les à `docs.json` avec `"redirects": [{"source": "/old", "destination": "/new"}]`
* **Indexation SEO** → Contrôlez-la avec `"seo": {"indexing": "all"}` pour inclure les pages masquées dans les résultats de recherche

**Nécessite une configuration dans le tableau de bord (tâche humaine) :**

* Domaines personnalisés et sous-domaines
* Paramètres de déploiement de prévisualisation
* Configuration DNS

Pour l’hébergement sur le sous-chemin `/docs` avec Vercel ou Cloudflare, les agents peuvent aider à configurer les règles de réécriture. Voir [/docs en sous-chemin](https://mintlify.com/docs/deploy/vercel).

<div id="workflow">
  ## Flux de travail
</div>

<div id="1-understand-the-task">
  ### 1. Comprendre la tâche
</div>

Déterminez ce qui doit être documenté, quelles pages sont concernées et ce que le lecteur doit pouvoir accomplir ensuite. Si l’un de ces éléments n’est pas clair, posez la question.

<div id="2-research">
  ### 2. Recherche
</div>

* Lisez `docs.json` pour comprendre la structure du site
* Recherchez dans la documentation existante du contenu connexe
* Lisez des pages similaires pour vous aligner sur le style du site

<div id="3-plan">
  ### 3. Planification
</div>

* Déterminez ce que le lecteur doit pouvoir accomplir après avoir lu la documentation et le contenu actuel
* Proposez les mises à jour ou les nouveaux contenus nécessaires
* Vérifiez que les modifications proposées aideront les lecteurs à atteindre leur objectif

<div id="4-write">
  ### 4. Rédiger
</div>

* Commencez par les informations les plus importantes
* Veillez à ce que les sections restent ciblées et faciles à parcourir
* Utilisez les composants à bon escient (n&#39;en abusez pas)
* Signalez tout élément incertain avec un commentaire TODO :

```mdx
{/* TODO: Verify the default timeout value */}
```

<div id="5-update-navigation">
  ### 5. Mettez à jour la navigation
</div>

Si vous avez créé une nouvelle page, ajoutez-la au groupe approprié dans `docs.json`.

<div id="6-verify">
  ### 6. Vérifiez
</div>

Avant de soumettre :

* [ ] Les métadonnées d’en-tête incluent le titre et la description
* [ ] Tous les blocs de code comportent une balise de langage
* [ ] Les liens internes utilisent des chemins relatifs à la racine, sans extension de fichier
* [ ] Les nouvelles pages sont ajoutées à la navigation de `docs.json`
* [ ] Le contenu correspond au style des pages voisines
* [ ] Aucune formulation marketing ni aucun remplissage
* [ ] Les TODO sont clairement marqués pour tout point incertain
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

Toute page qui n&#39;est pas incluse dans la Navigation de `docs.json` est masquée. Utilisez les pages masquées pour les contenus qui doivent être accessibles par URL ou indexés pour l&#39;assistant ou la recherche, sans être visibles dans la navigation latérale.

<div id="exclude-pages">
  ### Exclure des pages
</div>

Le fichier `.mintignore` permet d’exclure du traitement les fichiers d’un dépôt de documentation.

<div id="common-gotchas">
  ## Pièges courants
</div>

1. **Imports de composants** - Les composants JSX nécessitent un import explicite, contrairement aux composants MDX
2. **Métadonnées d’en-tête requises** - Chaque fichier MDX doit contenir au minimum un `title`
3. **Langue du bloc de code** - Spécifiez toujours un identifiant de langue
4. **N’utilisez jamais `mint.json`** - `mint.json` est obsolète. Utilisez uniquement `docs.json`

<div id="resources">
  ## Ressources
</div>

* [Documentation](https://mintlify.com/docs)
* [Schéma de configuration](https://mintlify.com/docs.json)
* [Demandes de fonctionnalités](https://github.com/orgs/mintlify/discussions/categories/feature-requests)
* [Signalements de bugs et retours](https://github.com/orgs/mintlify/discussions/categories/bugs-feedback)