---
name: mintlify-api
description: Interactúa con la API REST de Mintlify para gestionar despliegues, iniciar compilaciones y consultar programáticamente los metadatos del sitio de documentación.
license: MIT
compatibility: Cualquier cliente HTTP. Autenticación mediante clave de API.
metadata:
  author: mintlify
  version: "1.0"
---

<div id="mintlify-api">
  # API de Mintlify
</div>

Usa la API de Mintlify para gestionar sitios de documentación mediante programación. Esta sección abarca la gestión de despliegues, los activadores de compilación y las consultas de metadatos del sitio.

<div id="authentication">
  ## Autenticación
</div>

Todas las solicitudes a la API requieren una clave de API que se envía en el encabezado `Authorization`:

```
Authorization: Bearer <your-api-key>
```

Genera claves de API en el [panel de Mintlify](https://dashboard.mintlify.com), en Settings &gt; API Keys.

<div id="core-capabilities">
  ## Capacidades principales
</div>

<div id="trigger-deployments">
  ### Activar despliegues
</div>

Activa mediante programación una nueva compilación de la documentación cuando haya cambios en tu base de código fuera de los eventos de `git push`.

<div id="query-site-metadata">
  ### Consultar los metadatos del sitio
</div>

Obtén información sobre tu sitio de documentación, incluido el estado de despliegue, los dominios configurados y la estructura de navegación.

<div id="manage-preview-deployments">
  ### Gestionar despliegues de vista previa
</div>

Crea y gestiona despliegues de vista previa para solicitudes de extracción (pull request, PR) y ramas, a fin de revisar los cambios en la documentación antes de que se publiquen.

<div id="resources">
  ## Recursos
</div>

* [Referencia de API](https://mintlify.com/docs/api)
* [Panel](https://dashboard.mintlify.com)
* [Guía de despliegue](https://mintlify.com/docs/deploy)