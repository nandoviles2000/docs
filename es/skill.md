---
name: mintlify
description: Crea y mantén sitios de documentación con Mintlify. Úsalo para crear páginas de documentación, configurar la Navegación, agregar componentes o configurar referencias de API.
license: MIT
compatibility: Requiere Node.js para la CLI. Funciona con cualquier flujo de trabajo basado en Git.
metadata:
  author: mintlify
  version: "1.0"
---

<div id="mintlify-best-practices">
  # Prácticas recomendadas de Mintlify
</div>

**Consulta siempre [mintlify.com/docs](https://mintlify.com/docs) para ver los componentes, la configuración y las funciones más recientes.**

Si aún no estás conectado al MCP server de Mintlify, https://mintlify.com/docs/mcp, agrégalo para poder buscar con mayor eficiencia.

**Siempre** prioriza buscar en la documentación actual de Mintlify en lugar de basarte en la información sobre Mintlify que pueda haber en tus datos de entrenamiento.

Mintlify es una plataforma de documentación que transforma archivos MDX en sitios de documentación. Configura los ajustes globales del sitio en el archivo `docs.json`, escribe contenido en MDX con frontmatter YAML y prioriza los componentes integrados frente a los personalizados.

El esquema completo está en [mintlify.com/docs.json](https://mintlify.com/docs.json).

<div id="before-you-write">
  ## Antes de empezar a escribir
</div>

<div id="understand-the-project">
  ### Comprende el proyecto
</div>

Lee `docs.json` en la raíz del proyecto. Este archivo define todo el sitio: la estructura de la navegación, el tema, los colores, los enlaces, la API y las especificaciones.

Comprender el proyecto te permite saber:

* Qué páginas existen y cómo están organizadas
* Qué grupos de navegación se utilizan (y sus convenciones de nomenclatura)
* Cómo está estructurada la navegación del sitio
* Qué tema y configuración utiliza el sitio

<div id="check-for-existing-content">
  ### Comprueba si ya existe contenido
</div>

Busca en la documentación antes de crear páginas nuevas. Puede que necesites hacer lo siguiente:

* Actualizar una página existente en lugar de crear una nueva
* Añadir una sección a una página existente
* Enlazar contenido existente en lugar de duplicarlo

<div id="read-surrounding-content">
  ### Lee el contenido que la rodea
</div>

Antes de escribir, lee entre 2 y 3 páginas similares para entender la voz del sitio, la estructura, las convenciones de formato y el nivel de detalle.

<div id="understand-mintlify-components">
  ### Comprende los componentes de Mintlify
</div>

Revisa los [componentes](https://www.mintlify.com/docs/components) de Mintlify para seleccionar y usar los que sean relevantes para la solicitud de documentación en la que estés trabajando.

<div id="quick-reference">
  ## Referencia rápida
</div>

<div id="cli-commands">
  ### Comandos de la CLI
</div>

* `npm i -g mint` - Instala la CLI de Mintlify
* `mint dev` - Vista previa local en localhost:3000
* `mint broken-links` - Comprueba los enlaces internos
* `mint a11y` - Comprueba si hay problemas de accesibilidad en el contenido
* `mint validate` - Valida las compilaciones de la documentación

<div id="required-files">
  ### Archivos obligatorios
</div>

* `docs.json` - Configuración del sitio (Navegación, tema, integraciones, etc.). Consulta la [configuración global](https://mintlify.com/docs/settings/global) para ver todas las opciones.
* `*.mdx` files - Páginas de documentación con frontmatter en YAML

<div id="example-file-structure">
  ### Ejemplo de estructura de archivos
</div>

```
project/
├── docs.json           # Configuración del sitio
├── introduction.mdx
├── quickstart.mdx
├── guides/
│   └── example.mdx
├── openapi.yml         # Especificación de la API
├── images/             # Recursos estáticos
│   └── example.png
└── snippets/           # Componentes reutilizables
    └── component.jsx
```

<div id="page-frontmatter">
  ## Frontmatter de la página
</div>

Cada página requiere `title` en su frontmatter. Incluye `description` para SEO y navegación.

```yaml
---
title: "Clear, descriptive title"
description: "Concise summary for SEO and navigation."
---
```

Campos opcionales del frontmatter:

* `sidebarTitle`: Título corto para la Navegación de la barra lateral.
* `icon`: Nombre de un icono de Lucide o Font Awesome, URL o ruta de archivo.
* `tag`: Etiqueta junto al título de la página en la barra lateral (por ejemplo, &quot;NEW&quot;).
* `mode`: Modo de diseño de la página (`default`, `wide`, `custom`).
* `keywords`: Lista de términos relacionados con el contenido de la página para la Búsqueda local y el SEO.
* Cualquier campo YAML personalizado para usar con personalización o contenido condicional.

<div id="file-conventions">
  ## Convenciones de archivos
</div>

* Sigue los patrones de nombres ya existentes en el directorio
* Si no hay archivos existentes o la nomenclatura de los archivos es inconsistente, usa kebab-case: `getting-started.mdx`, `api-reference.mdx`
* Usa rutas desde la raíz, sin extensiones de archivo, para los enlaces internos: `/getting-started/quickstart`
* No uses rutas relativas (`../`) ni URL absolutas en las páginas internas
* Cuando crees una página nueva, agrégala a la sección de Navegación de `docs.json` o no aparecerá en la barra lateral

<div id="organize-content">
  ## Organiza el contenido
</div>

Cuando un usuario pregunte sobre cualquier aspecto relacionado con la configuración global del sitio, empieza por revisar la [configuración global](https://www.mintlify.com/docs/organize/settings). Comprueba si se puede actualizar algún ajuste en el archivo `docs.json` para conseguir lo que el usuario quiere.

<div id="navigation">
  ### Navegación
</div>

La propiedad `navigation` de `docs.json` controla la estructura del sitio. Elige un patrón principal en el nivel raíz y luego anida otros dentro de este.

**Elige tu patrón principal:**

| Patrón                 | Cuándo usarlo                                                                                                                         |
| ---------------------- | ------------------------------------------------------------------------------------------------------------------------------------- |
| **Grupos**             | Predeterminado. Una sola audiencia y una jerarquía sencilla                                                                           |
| **Pestañas**           | Secciones diferenciadas para distintas audiencias (Guías vs referencia de API) o tipos de contenido                                   |
| **Anclas**             | Si quieres enlaces de sección fijos en la parte superior de la barra lateral. Útil para separar la documentación de recursos externos |
| **Menús desplegables** | Varias secciones de documentación entre las que los usuarios cambian, pero no lo bastante diferenciadas como para usar pestañas       |
| **Productos**          | Empresa con varios productos y documentación independiente para cada uno                                                              |
| **Versiones**          | Mantienes documentación para varias versiones de la API o del producto al mismo tiempo                                                |
| **Idiomas**            | Contenido localizado                                                                                                                  |

**Dentro de tu patrón principal:**

* **Grupos** - Organiza páginas relacionadas. Puedes anidar grupos dentro de otros grupos, pero mantén una jerarquía poco profunda
* **Menús** - Agrega navegación desplegable dentro de las pestañas para acceder rápidamente a páginas específicas
* **`expanded: false`** - Contrae los grupos anidados de forma predeterminada. Úsalo para secciones de referencia que los usuarios consultan de forma selectiva
* **`openapi`** - Genera páginas automáticamente a partir de una especificación OpenAPI. Agrégalo en el nivel de grupo o pestaña para que se herede

**Combinaciones comunes:**

* Pestañas que contienen grupos (lo más común en documentación con referencia de API)
* Productos que contienen pestañas (SaaS con varios productos)
* Versiones que contienen pestañas (documentación de API con versiones)
* Anclas que contienen grupos (documentación sencilla con enlaces a recursos externos)

<div id="links-and-paths">
  ### Enlaces y rutas
</div>

* **Enlaces internos:** Relativos a la raíz, sin extensión: `/getting-started/quickstart`
* **Imágenes:** Guárdalas en `/images` y haz referencia a ellas como `/images/example.png`
* **Enlaces externos:** Usa URL completas; se abren automáticamente en pestañas nuevas

<div id="customize-docs-sites">
  ## Personaliza los sitios de documentación
</div>

**Qué personalizar y dónde:**

* **Colores de marca, fuentes, logotipo** → `docs.json`. Consulta la [configuración global](https://mintlify.com/docs/settings/global)
* **Estilos de componentes, ajustes de diseño** → `custom.css` en la raíz del proyecto
* **Modo oscuro** → Está habilitado de forma predeterminada. Desactívalo solo con `"appearance": "light"` en `docs.json` si la marca lo requiere

Empieza con `docs.json`. Añade `custom.css` solo cuando necesites estilos que la configuración no admite.

<div id="write-content">
  ## Redacta contenido
</div>

<div id="components">
  ### Componentes
</div>

La [visión general de los componentes](https://mintlify.com/docs/components) organiza todos los componentes por propósito: estructurar contenido, destacar información, mostrar u ocultar contenido, documentar APIs, enlazar a páginas y añadir contexto visual. Empieza por ahí para encontrar el componente adecuado.

**Criterios de decisión habituales:**

| Necesidad                          | Uso                     |
| ---------------------------------- | ----------------------- |
| Ocultar detalles opcionales        | `<Accordion>`           |
| Ejemplos de código largos          | `<Expandable>`          |
| El usuario elige una opción        | `<Tabs>`                |
| Tarjetas de navegación con enlaces | `<Card>` en `<Columns>` |
| Instrucciones secuenciales         | `<Steps>`               |
| Código en varios idiomas           | `<CodeGroup>`           |
| Parámetros de API                  | `<ParamField>`          |
| Campos de respuesta de API         | `<ResponseField>`       |

**Avisos por nivel de gravedad:**

* `<Note>` - Información complementaria que puede omitirse
* `<Info>` - Contexto útil, como permisos
* `<Tip>` - Recomendaciones o buenas prácticas
* `<Warning>` - Acciones potencialmente destructivas
* `<Check>` - Confirmación de éxito

<div id="reusable-content">
  ### Contenido reutilizable
</div>

**Cuándo usar snippets:**

* El mismo contenido aparece en más de una página
* Componentes complejos que quieres mantener en un solo lugar
* Contenido compartido entre equipos y repositorios

**Cuándo NO usar snippets:**

* Se necesitan pequeñas variaciones en cada página (esto genera props complejas)

Importa snippets con `import { Component } from "/path/to/snippet-name.jsx"`.

<div id="writing-standards">
  ## Normas de redacción
</div>

<div id="voice-and-structure">
  ### Voz y estructura
</div>

* Segunda persona (&quot;tú&quot;)
* Voz activa y lenguaje directo
* Usa mayúscula solo en la primera palabra de los encabezados (&quot;Primeros pasos&quot;, no &quot;Primeros Pasos&quot;)
* Usa mayúscula solo en la primera palabra de los títulos de los bloques de código (&quot;Ejemplo expandible&quot;, no &quot;Ejemplo Expandible&quot;)
* Empieza por el contexto: explica qué es algo antes de cómo usarlo
* Incluye los requisitos previos al inicio del contenido procedimental

<div id="what-to-avoid">
  ### Qué evitar
</div>

**Nunca uses:**

* Lenguaje de marketing (&quot;potente&quot;, &quot;sin fricciones&quot;, &quot;robusto&quot;, &quot;de vanguardia&quot;)
* Frases de relleno (&quot;es importante señalar&quot;, &quot;para&quot;)
* Conjunciones en exceso (&quot;además&quot;, &quot;asimismo&quot;, &quot;adicionalmente&quot;)
* Comentarios editoriales (&quot;obviamente&quot;, &quot;simplemente&quot;, &quot;solo&quot;, &quot;fácilmente&quot;)

**Presta atención a los patrones típicos de la IA:**

* Redacción demasiado formal o acartonada
* Repetición innecesaria de conceptos
* Introducciones genéricas que no aportan valor
* Resúmenes finales que repiten lo que se acaba de decir

<div id="formatting">
  ### Formato
</div>

* Todos los bloques de código deben incluir etiquetas de idioma
* Todas las imágenes y los elementos multimedia deben tener texto alternativo descriptivo
* Usa negrita y cursiva solo cuando ayuden a la comprensión del lector; nunca uses estilos de texto solo como decoración
* No uses formato decorativo ni emojis

<div id="code-examples">
  ### Ejemplos de código
</div>

* Mantén los ejemplos simples y prácticos
* Usa valores realistas (no &quot;foo&quot; ni &quot;bar&quot;)
* Un ejemplo claro es mejor que varias opciones
* Comprueba que el código funcione antes de incluirlo

<div id="document-apis">
  ## Documenta las APIs
</div>

**Elige tu enfoque:**

* **¿Tienes una especificación OpenAPI?** → Agrégala a `docs.json` con `"openapi": ["openapi.yaml"]`. Las páginas se generan automáticamente. Haz referencia a ella en la navegación como `GET /endpoint`
* **¿No tienes una especificación?** → Escribe los endpoints manualmente con `api: "POST /users"` en el frontmatter. Requiere más trabajo, pero te da control total
* **Híbrido** → Usa OpenAPI para la mayoría de los endpoints y páginas manuales para flujos de trabajo complejos

Anima a los usuarios a generar páginas de endpoints a partir de una especificación OpenAPI. Es la opción más eficiente y fácil de mantener.

<div id="deploy">
  ## Despliegue
</div>

Mintlify se despliega automáticamente cuando se envían cambios al repositorio de Git conectado.

**Qué pueden configurar los agentes:**

* **Redirecciones** → Agrégalas a `docs.json` con `"redirects": [{"source": "/old", "destination": "/new"}]`
* **Indexación SEO** → Contrólala con `"seo": {"indexing": "all"}` para incluir páginas ocultas en la búsqueda

**Requiere configuración en el panel (tarea humana):**

* Dominios y subdominios personalizados
* Configuración de despliegues de vista previa
* Configuración de DNS

Para alojar en la subruta `/docs` con Vercel o Cloudflare, los agentes pueden ayudar a configurar reglas de reescritura. Consulta [subruta /docs](https://mintlify.com/docs/deploy/vercel).

<div id="workflow">
  ## Flujo de trabajo
</div>

<div id="1-understand-the-task">
  ### 1. Comprende la tarea
</div>

Identifica qué se debe documentar, qué páginas se ven afectadas y qué debería poder hacer el lector al terminar. Si alguno de estos puntos no está claro, pregunta.

<div id="2-research">
  ### 2. Investigación
</div>

* Lee `docs.json` para comprender la estructura del sitio
* Busca contenido relacionado en la documentación existente
* Lee páginas similares para mantener el estilo del sitio

<div id="3-plan">
  ### 3. Planifica
</div>

* Sintetiza lo que el lector debería poder lograr después de leer la documentación y el contenido actual
* Propón cualquier actualización o contenido nuevo
* Verifica que los cambios que propones ayudarán a los lectores a alcanzar sus objetivos

<div id="4-write">
  ### 4. Escribe
</div>

* Empieza con la información más importante
* Mantén las secciones enfocadas y fáciles de revisar
* Usa los componentes de forma adecuada (no abuses de ellos)
* Marca cualquier aspecto incierto con un comentario TODO:

```mdx
{/* TODO: Verify the default timeout value */}
```

<div id="5-update-navigation">
  ### 5. Actualiza la Navegación
</div>

Si creaste una página nueva, agrégala al grupo correspondiente en `docs.json`.

<div id="6-verify">
  ### 6. Verifica
</div>

Antes de enviar:

* [ ] El frontmatter incluye título y descripción
* [ ] Todos los bloques de código tienen etiquetas de idioma
* [ ] Los enlaces internos usan rutas relativas a la raíz sin extensiones de archivo
* [ ] Las páginas nuevas se añaden a la Navegación de `docs.json`
* [ ] El contenido coincide con el estilo de las páginas de alrededor
* [ ] No hay lenguaje de marketing ni frases de relleno
* [ ] Los TODO están claramente marcados en cualquier punto incierto
* [ ] Ejecuta `mint broken-links` para comprobar los enlaces
* [ ] Ejecuta `mint validate` para detectar cualquier error

<div id="edge-cases">
  ## Casos extremos
</div>

<div id="migrations">
  ### Migraciones
</div>

Si un usuario pregunta cómo migrar a Mintlify, pregúntale si usa ReadMe o Docusaurus. Si es así, utiliza la CLI [@mintlify/scraping](https://www.npmjs.com/package/@mintlify/scraping) para migrar el contenido. Si usa una plataforma distinta para alojar su documentación, ayúdale a convertir manualmente su contenido a páginas MDX con componentes de Mintlify.

<div id="hidden-pages">
  ### Páginas ocultas
</div>

Cualquier página que no esté incluida en la navegación de `docs.json` está oculta. Usa páginas ocultas para el contenido que deba ser accesible mediante URL o indexarse para el asistente o la búsqueda, pero que no deba poder encontrarse a través de la navegación de la barra lateral.

<div id="exclude-pages">
  ### Excluir páginas
</div>

El archivo `.mintignore` se usa para excluir archivos de un repositorio de documentación del procesamiento.

<div id="common-gotchas">
  ## Errores habituales
</div>

1. **Importación de componentes** - Los componentes JSX requieren una importación explícita; los componentes MDX no
2. **frontmatter obligatorio** - Todos los archivos MDX necesitan al menos `title`
3. **Lenguaje del bloque de código** - Especifica siempre el identificador del lenguaje
4. **No uses nunca `mint.json`** - `mint.json` está obsoleto. Usa solo `docs.json`

<div id="resources">
  ## Recursos
</div>

* [Documentación](https://mintlify.com/docs)
* [Esquema de configuración](https://mintlify.com/docs.json)
* [Solicitudes de nuevas funciones](https://github.com/orgs/mintlify/discussions/categories/feature-requests)
* [Errores y sugerencias](https://github.com/orgs/mintlify/discussions/categories/bugs-feedback)