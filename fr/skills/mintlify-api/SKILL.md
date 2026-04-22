---
name: mintlify-api
description: Interagissez avec l’API REST de Mintlify pour gérer les déploiements, déclencher des builds et interroger les métadonnées du site de documentation de façon programmatique.
license: MIT
compatibility: N’importe quel client HTTP. Authentification via une clé API.
metadata:
  author: mintlify
  version: "1.0"
---

<div id="mintlify-api">
  # API de Mintlify
</div>

Utilisez l’API de Mintlify pour gérer vos sites de documentation de manière programmatique. Cette compétence couvre la gestion des déploiements, les déclencheurs de build et les requêtes de métadonnées du site.

<div id="authentication">
  ## Authentification
</div>

Toutes les requêtes API nécessitent une clé API transmise dans l’en-tête `Authorization` :

```
Authorization: Bearer <your-api-key>
```

Générez des clés API depuis le [tableau de bord Mintlify](https://dashboard.mintlify.com), sous Settings &gt; API Keys.

<div id="core-capabilities">
  ## Fonctionnalités clés
</div>

<div id="trigger-deployments">
  ### Déclencher des déploiements
</div>

Déclenchez par programmation une reconstruction de la documentation lorsque votre base de code est modifiée autrement que par un push Git.

<div id="query-site-metadata">
  ### Consulter les métadonnées du site
</div>

Récupérez des informations sur votre site de documentation, notamment son statut de déploiement, les domaines configurés et la structure de navigation.

<div id="manage-preview-deployments">
  ### Gérer les déploiements d’aperçu
</div>

Créez et gérez des déploiements d’aperçu pour les pull requests (PR) et les branches afin d’examiner les modifications de la documentation avant leur mise en ligne.

<div id="resources">
  ## Ressources
</div>

* [Référence de l’API](https://mintlify.com/docs/api)
* [Tableau de bord](https://dashboard.mintlify.com)
* [Guide de déploiement](https://mintlify.com/docs/deploy)