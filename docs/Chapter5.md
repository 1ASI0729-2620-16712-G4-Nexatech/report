# Capítulo V: Product Implementation, Validation & Deployment

## 5.1. Software Configuration Management
 
Esta sección establece las herramientas, convenciones y configuraciones que el equipo utiliza para mantener la consistencia del proyecto VitalTrek a lo largo de su ciclo de vida. Se documentan el entorno de desarrollo, el esquema de control de versiones con GitFlow, las convenciones de codificación y la configuración de despliegue de cada producto. Estas decisiones permiten coordinar el trabajo de los cinco integrantes, mantener trazabilidad sobre cada cambio y reproducir el entorno en cualquier equipo.
 
### 5.1.1. Software Development Environment Configuration
 
La siguiente tabla especifica los productos de software que el equipo utiliza, agrupados por tipo de actividad del ciclo de vida. Para los productos basados en modelos SaaS se indica la ruta de referencia; para los que se ejecutan en el computador de cada integrante se indica la ruta de descarga.
 
| Actividad | Producto | Propósito de uso en el proyecto | Tipo | Ruta de referencia o descarga |
| --- | --- | --- | --- | --- |
| Project Management | Jira Software | Gestionar el Product Backlog, los Sprint Backlogs, las Engineering Tasks y las estimaciones en Story Points y horas. | SaaS | https://www.atlassian.com/software/jira |
| Project Management | Discord | Coordinar las ceremonias del Sprint y la comunicación diaria del equipo. | SaaS / aplicación de escritorio | https://discord.com/download |
| Requirements Management | UXPressia | Elaborar las fichas de User Persona, los Journey Maps, los Empathy Maps y el Impact Map. | SaaS | https://uxpressia.com/ |
| Requirements Management | Miro | Elaborar el Big Picture EventStorming y el Design-Level EventStorming. | SaaS | https://miro.com/ |
| Product UX/UI Design | Figma | Elaborar los wireframes, mock-ups y prototipos del Landing Page y de las Web Applications. | SaaS | https://www.figma.com/ |
| Software Development | Git | Controlar las versiones del código fuente en el computador de cada integrante y aplicar el flujo de ramas de GitFlow. | Instalación local | https://git-scm.com/downloads |
| Software Development | GitHub | Alojar los repositorios de la organización del equipo, gestionar los Pull Requests y registrar la colaboración. | SaaS | https://github.com/ |
| Software Development | Visual Studio Code | Editar el código del Landing Page, de las Web Applications y la documentación en Markdown. | Instalación local | https://code.visualstudio.com/download |
| Software Development | Google Chrome | Verificar la navegación, el comportamiento responsive y la accesibilidad del Landing Page y de las Web Applications mediante sus herramientas de desarrollo. | Instalación local | https://www.google.com/chrome/ |
| Software Development | Vue.js | Construir las Frontend Web Applications con Vue 3 y Vite, junto con Pinia, Vue Router, Axios, PrimeVue y vue-i18n. Implementado en el Sprint 2 (TB1). | Instalación local (vía npm) | https://vuejs.org/ |
| Software Development | json-server | Ejecutar la Fake API con recursos JSON de prueba que consumen las Web Applications. Implementado en el Sprint 2 (TB1). | Instalación local (vía npm) | https://github.com/typicode/json-server |
| Software Development | JetBrains Rider | Editar, compilar y depurar el RESTful Web Services en C#. Utilizado desde el Sprint 3 (AV2). | Instalación local | https://www.jetbrains.com/rider/download/ |
| Software Development | .NET SDK 10 y C# | Construir el RESTful Web Services con ASP.NET Core y Entity Framework Core. Implementado en el Sprint 3 (AV2). | Instalación local | https://dotnet.microsoft.com/download |
| Software Development | MySQL Server y MySQL Workbench | Persistir localmente la información del RESTful Web Services y revisar las tablas generadas por las migraciones de Entity Framework Core. Implementado en el Sprint 3 (AV2). | Instalación local | https://dev.mysql.com/downloads/ |
| Software Deployment | Vercel | Desplegar y publicar el Landing Page y las Web Applications a partir de sus repositorios de GitHub. | SaaS | https://vercel.com/ |
| Software Deployment | Docker | Empaquetar el RESTful Web Services en una imagen de contenedor a partir del `Dockerfile` del repositorio. La imagen se construye en Render. | Archivo de configuración en el repositorio | https://www.docker.com/ |
| Software Deployment | Render | Desplegar el RESTful Web Services como Web Service basado en Docker a partir de la rama `main`. | SaaS | https://render.com/ |
| Software Deployment | Railway MySQL | Alojar la base de datos MySQL administrada que utiliza el RESTful Web Services desplegado. | SaaS | https://railway.app/ |
| Software Documentation | Scalar (OpenAPI) | Publicar y probar la documentación OpenAPI de los endpoints del RESTful Web Services. Implementado en el Sprint 3 (AV2). | Paquete NuGet del proyecto | https://scalar.com/ |
| Software Documentation | Markdown | Redactar el informe del proyecto y los archivos README de cada repositorio. | Formato abierto | https://www.markdownguide.org/ |
| Software Documentation | dbdiagram.io | Elaborar el Database Diagram de la sección 4.8. | SaaS | https://dbdiagram.io/ |
| Software Documentation | PlantUML | Elaborar los Class Diagrams de la sección 4.7. | Instalación local / SaaS | https://plantuml.com/download |
| Software Documentation | Microsoft PowerPoint | Elaborar la presentación de exposición de cada entrega. | Instalación local | https://www.microsoft.com/microsoft-365/powerpoint |
| Software Documentation | Microsoft Stream | Publicar los videos de exposición y de navegación del producto. | SaaS | https://www.microsoft.com/microsoft-365/microsoft-stream |
 
### 5.1.2. Source Code Management
 
El código fuente de VitalTrek se administra con **Git** como sistema de control de versiones y **GitHub** como plataforma de alojamiento y colaboración. Cada producto de la solución mantiene su propio repositorio dentro de la organización del equipo, de modo que sus ciclos de vida y despliegues sean independientes.
 
| Producto | Repositorio | Rama por defecto | Estado en AV2 |
| --- | --- | --- | --- |
| Project Report | https://github.com/1ASI0729-2620-16712-G4-Nexatech/report | `develop` | En elaboración |
| Landing Page | https://github.com/1ASI0729-2620-16712-G4-Nexatech/landing-page | `main` | Implementado y desplegado |
| Frontend Web Applications | https://github.com/1ASI0729-2620-16712-G4-Nexatech/web-applications | `develop` | Implementado y desplegado (`v1.1.0`); consume el RESTful Web Services en IAM y Expedition Setup |
| RESTful Web Services | https://github.com/1ASI0729-2620-16712-G4-Nexatech/vitaltrek-backend | `develop` | Implementado y desplegado (`v1.0.0`) |
 
En el caso del RESTful Web Services, el repositorio contiene la solución `VitalTrek.Platform.sln` con el proyecto `VitalTrek.API`, organizado por bounded contexts, junto con sus migraciones de base de datos y el `Dockerfile` utilizado para el despliegue.
 
#### GitFlow como Workflow de branching y colaboración
 
El equipo aplica **GitFlow**, según el modelo descrito por Vincent Driessen en *A successful Git branching model*. El repositorio mantiene dos ramas de larga duración y tres tipos de ramas de apoyo.
 
**Ramas de larga duración**
 
| Rama | Propósito | Quién integra en ella |
| --- | --- | --- |
| `main` | Contiene únicamente versiones estables y publicadas. Cada integración en esta rama corresponde a una Release etiquetada. | Solo mediante Pull Request desde `release/*` o `hotfix/*`. |
| `develop` | Integra el trabajo aprobado de todas las funcionalidades en curso. Es la base desde la que nacen las ramas de funcionalidad. | Solo mediante Pull Request desde `feature/*`. |
 
**Ramas de apoyo y sus convenciones de nombre**
 
| Tipo | Convención de nombre | Nace de | Se integra en | Ejemplo real del proyecto |
| --- | --- | --- | --- | --- |
| Feature | `feature/<ámbito>-<descripción-breve>` en inglés y `kebab-case` | `develop` | `develop` | `feature/landing-seo-a11y` |
| Release | `release/vMAJOR.MINOR.PATCH` | `develop` | `main` y `develop` | `release/v1.0.0` |
| Hotfix | `hotfix/vMAJOR.MINOR.PATCH-<descripción-breve>` | `main` | `main` y `develop` | `hotfix/v1.0.1-contact-form-validation` |
 
Reglas aplicables a los nombres de rama:
 
1. Se escriben íntegramente en inglés y en minúsculas, con palabras separadas por guion.
2. El ámbito identifica el producto o el capítulo afectado: `landing`, `webapp`, `api`, `chapter-3`.
3. No se usan espacios, caracteres acentuados ni mayúsculas.
4. Una rama de funcionalidad corresponde a una sola User Story o Technical Story, y se elimina una vez integrada.

**Flujo de trabajo**
 
![Gitflow_AV01](../assets/images/chapter-5/gitflow_av01.png)
 
*Figura 5.0. Flujo de ramas aplicado en los repositorios de VitalTrek.*
 
**Política de Pull Requests**
 
1. Toda integración a `develop` y a `main` se realiza mediante Pull Request; no se permite empujar directamente a ninguna de las dos.
2. Cada Pull Request indica en su descripción la User Story o Technical Story que resuelve y los criterios de aceptación cubiertos.
3. Un Pull Request requiere la revisión y aprobación de al menos un integrante distinto de su autor.
4. La rama de funcionalidad se elimina después de la integración.
#### Semantic Versioning
 
Las Releases se nombran según **Semantic Versioning 2.0.0**, con el formato `vMAJOR.MINOR.PATCH`:
 
| Componente | Se incrementa cuando | Ejemplo |
| --- | --- | --- |
| `MAJOR` | Se introduce un cambio incompatible con la versión anterior. | `v2.0.0` |
| `MINOR` | Se agrega funcionalidad manteniendo la compatibilidad. | `v1.1.0` |
| `PATCH` | Se corrige un defecto sin agregar funcionalidad. | `v1.0.1` |
 
La versión publicada al cierre del Sprint 1 es **`v1.0.0`**, correspondiente a la primera versión funcional y desplegada del Landing Page. Cada Release se etiqueta en `main` con su número de versión.
 
#### Conventional Commits
 
Los mensajes de commit siguen la especificación **Conventional Commits 1.0.0**, con la estructura:
 
```
<tipo>(<alcance>): <descripción en imperativo y en inglés>
 
[cuerpo opcional]
```
 
| Tipo | Se usa para |
| --- | --- |
| `feat` | Agregar una funcionalidad nueva. |
| `fix` | Corregir un defecto. |
| `docs` | Cambios que solo afectan documentación. |
| `style` | Cambios de formato que no alteran el comportamiento. |
| `refactor` | Reestructurar código sin cambiar su comportamiento externo. |
| `test` | Agregar o corregir pruebas. |
| `chore` | Tareas de mantenimiento, configuración o dependencias. |
 
Ejemplos tomados del repositorio del proyecto:
 
```
feat(a11y): add skip to main content link
feat(seo): complete meta tags defined in report 4.2.3
docs(chapter5): add Jorge Mateo Leon commits to development evidence
style(a11y): add skip link styles
```
 
> **Nota sobre la adopción de las convenciones.** El equipo adoptó formalmente Conventional Commits y la convención de nombres de rama a partir del 7 de septiembre de 2026. Los commits y ramas anteriores a esa fecha, registrados en la sección 5.2.1.4, no siguen la convención, dado que corresponden al período de configuración inicial del repositorio. No se reescribió el historial para preservar la trazabilidad de los aportes individuales. A partir de esa fecha, la convención se verifica durante la revisión de cada Pull Request.
 
### 5.1.3. Source Code Style Guide & Conventions
 
El equipo adopta guías de estilo estándar para cada lenguaje de la solución. Todos los identificadores, nombres de archivo, clases, funciones y comentarios se redactan en inglés, conforme a lo indicado en el enunciado del trabajo final.
 
| Tecnología | Convenciones adoptadas | Referencia |
| --- | --- | --- |
| HTML5 | Elementos semánticos, etiquetas y atributos en minúscula, atributos entre comillas dobles, texto alternativo en toda imagen informativa, indentación de dos espacios. | [Google HTML/CSS Style Guide](https://google.github.io/styleguide/htmlcssguide.html) · [W3Schools HTML Style Guide](https://www.w3schools.com/html/html5_syntax.asp) |
| CSS3 | Clases e identificadores en `kebab-case`, variables centralizadas en `tokens.css`, enfoque mobile-first, una declaración por línea. | [Google HTML/CSS Style Guide](https://google.github.io/styleguide/htmlcssguide.html) |
| JavaScript | Variables y funciones en `camelCase`, constantes en `UPPER_SNAKE_CASE`, uso de `const` y `let` en lugar de `var`, funciones con una sola responsabilidad, punto y coma obligatorio. | [Google JavaScript Style Guide](https://google.github.io/styleguide/jsguide.html) · [MDN JavaScript Guidelines](https://developer.mozilla.org/en-US/docs/MDN/Writing_guidelines/Code_style_guide/JavaScript) |
| Vue.js | Componentes en `PascalCase` con nombre de varias palabras, props en `camelCase` dentro del script y en `kebab-case` en la plantilla, un componente por archivo. | [Vue Style Guide](https://vuejs.org/style-guide/) |
| C# | Clases, métodos y propiedades en `PascalCase`; parámetros y variables locales en `camelCase`; interfaces con prefijo `I`. Planificado para el RESTful Web Services. | [C# Coding Conventions](https://learn.microsoft.com/en-us/dotnet/csharp/fundamentals/coding-style/coding-conventions) · [ASP.NET Core Engineering Guidelines](https://github.com/dotnet/aspnetcore/wiki/Engineering-guidelines) |
| Gherkin | Un escenario por comportamiento, redacción en tiempo presente y tercera persona, sin referencias a elementos de interfaz. | [Gherkin Reference](https://cucumber.io/docs/gherkin/reference/) |
| Markdown | Encabezados jerárquicos sin saltar niveles, enlaces relativos entre capítulos, imágenes con texto alternativo, tablas con formato consistente. | [Markdown Guide](https://www.markdownguide.org/basic-syntax/) |
 
Ejemplos aplicados en el Landing Page:
 
```html
<section class="safety-features" aria-labelledby="safety-title">
  <h2 id="safety-title" data-i18n="safetyTitle">Checkpoint synchronization</h2>
</section>
```
 
```css
:root {
  --forest-green: #0f3d2e;
  --safety-amber: #f2a93b;
}
 
.request-demo-button {
  background-color: var(--safety-amber);
}
```
 
```javascript
const DEFAULT_LOCALE = 'en-US';
 
function setLanguage(selectedLocale) {
  document.documentElement.lang = selectedLocale;
  localStorage.setItem('vitaltrek-language', selectedLocale);
}
```
 
### 5.1.4. Software Deployment Configuration
 
El despliegue de cada producto parte de su repositorio de código fuente. En AV1 se desplegó el Landing Page y en TB1 se desplegaron las Web Applications, ambos en Vercel a partir de sus repositorios de GitHub. En AV2 se desplegó el RESTful Web Services en Render como contenedor Docker, conectado a una base de datos MySQL administrada en Railway.
 
| Producto | Plataforma | Rama de despliegue | Estado |
| --- | --- | --- | --- |
| Landing Page | Vercel | `main` | Desplegado (`v1.1.0`) |
| Frontend Web Applications | Vercel | `main` | Desplegado (`v1.1.0`) |
| RESTful Web Services | Render (Docker) y Railway MySQL | `main` | Desplegado (`v1.0.0`) |
 
#### Configuración del Landing Page
 
| Parámetro | Valor |
| --- | --- |
| Repositorio | https://github.com/1ASI0729-2620-16712-G4-Nexatech/landing-page |
| Plataforma | Vercel |
| Production Branch | `main` |
| Framework preset | Other (HTML, CSS y JavaScript estáticos) |
| Build command | No aplica |
| Output directory | Directorio raíz del repositorio |
| Variables de entorno | No requeridas |
| URL pública de producción | https://landing-page-mrca1.vercel.app/ |
| Versión desplegada | `v1.1.0` (Sprint 3); `v1.0.0` en el Sprint 1 |
 
#### Pasos para lograr el despliegue desde el repositorio
 
1. El integrante desarrolla la funcionalidad en su rama `feature/*` y abre un Pull Request hacia `develop`.
2. Otro integrante revisa el Pull Request y verifica que se cumplan los criterios de aceptación de la historia correspondiente.
3. Aprobado el Pull Request, la rama se integra en `develop` y se elimina.
4. Al cerrar el Sprint se crea la rama `release/vX.Y.Z` desde `develop`, donde se ejecutan las validaciones finales: marcado W3C, enlaces internos, comportamiento responsive, cambio de idioma y accesibilidad por teclado.
5. La rama de Release se integra en `main` mediante Pull Request y se etiqueta con su número de versión.
6. Vercel detecta el cambio en la Production Branch y ejecuta el despliegue automático.
7. Se verifica la URL pública de producción y se registra la evidencia en la sección 5.2.X.7 del Sprint correspondiente.

#### Configuración de las Web Applications

| Parámetro | Valor |
| --- | --- |
| Repositorio | https://github.com/1ASI0729-2620-16712-G4-Nexatech/web-applications |
| Plataforma | Vercel |
| Production Branch | `main` |
| Framework preset | Vite |
| Build command | `npm run build` |
| Output directory | `dist` |
| Rewrites | `vercel.json` redirige todas las rutas a `index.html` para la navegación de la SPA |
| Variable `VITE_VITALTREK_API_URL` | `https://vitaltrek-backend.onrender.com/api/v1`, URL base del RESTful Web Services |
| Variable `VITE_SIMULATED_OPERATIONS` | `false` (definida en `.env.production`); los contextos aún no implementados en el API muestran que estarán disponibles en un próximo sprint |
| URL pública de producción | https://web-applications-vert.vercel.app/ |
| Versión desplegada | `v1.1.0` |

#### Configuración del RESTful Web Services

| Parámetro | Valor |
| --- | --- |
| Repositorio | https://github.com/1ASI0729-2620-16712-G4-Nexatech/vitaltrek-backend |
| Plataforma del servicio | Render, Web Service en plan Free |
| Runtime | Docker: `Dockerfile` en la raíz del repositorio, con imágenes oficiales del SDK y del runtime de ASP.NET Core 10 |
| Production Branch | `main` |
| Región | Singapore (Southeast Asia) |
| Puerto | Variable `PORT` inyectada por Render; 8080 por defecto |
| Base de datos | Railway MySQL, plan Starter, conexión cifrada (`SslMode=Required`) |
| Configuración de producción | `appsettings.Production.json`, cuya cadena de conexión y clave de firma se completan con variables de entorno al iniciar la aplicación |
| Migraciones | Se aplican automáticamente al iniciar la aplicación mediante Entity Framework Core |
| Documentación | Scalar en `/scalar` y especificación OpenAPI en `/openapi/v1.json` |
| URL pública de producción | https://vitaltrek-backend.onrender.com |
| Versión desplegada | `v1.0.0` |

Las variables de entorno se registran únicamente en Render y no se versionan en el repositorio:

| Variable | Propósito |
| --- | --- |
| `ASPNETCORE_ENVIRONMENT` | Valor `Production`; carga `appsettings.Production.json`. |
| `ASPNETCORE_FORWARDEDHEADERS_ENABLED` | Valor `true`; permite reconocer el esquema HTTPS detrás del proxy de Render. |
| `DATABASE_URL` | Host del servicio MySQL en Railway. |
| `DATABASE_PORT` | Puerto del servicio MySQL en Railway. |
| `DATABASE_USER` | Usuario de la base de datos. |
| `DATABASE_PASSWORD` | Contraseña de la base de datos. |
| `DATABASE_SCHEMA` | Base de datos utilizada (`defaultdb`). |
| `TOKEN_SECRET` | Clave de firma de los tokens JWT (HS256). |

#### Pasos para lograr el despliegue del RESTful Web Services desde el repositorio

1. El integrante desarrolla la funcionalidad en su rama `feature/*` y abre un Pull Request hacia `develop`.
2. Al cerrar el Sprint se crea la rama `release/vX.Y.Z` desde `develop`, donde se incorporan los ajustes de configuración de producción.
3. La rama de Release se integra en `main` y en `develop` mediante Pull Requests, y `main` se etiqueta con su número de versión.
4. Render detecta el cambio en la Production Branch, construye la imagen Docker y reinicia el servicio.
5. Al iniciar, la aplicación aplica las migraciones pendientes sobre la base de datos de Railway y carga los datos de demostración si la base de datos está vacía.
6. Se verifica la documentación en `/scalar` ejecutando el inicio de sesión y una consulta autenticada, y se registra la evidencia en la sección 5.2.X.7 del Sprint correspondiente.

## 5.2. Landing Page, Services & Applications Implementation

Esta sección documenta la implementación, validación y despliegue de los productos incluidos en la solución VitalTrek. Para AV1, el alcance se concentra en la primera versión funcional y desplegada del Landing Page, desarrollado con HTML5, CSS3 y JavaScript. En TB1, el Sprint 2 amplía el producto con las Web Applications frontend para configurar expediciones y consultar su progreso mediante una Fake API y datos simulados. El RESTful Web Services productivo, la persistencia real y la integración con dispositivos permanecen fuera del alcance de esta entrega.

### 5.2.1. Sprint 1

El Sprint 1 tiene como objetivo implementar y publicar la primera versión del Landing Page de VitalTrek. El alcance comprende las User Stories US01 a US06 y US33, relacionadas con la navegación, la propuesta de valor, los planes, la información del equipo, la solicitud de información, el cambio de idioma y la publicación de los términos de servicio y la política de privacidad; y las Technical Stories TS01 a TS04, que habilitan la estructura técnica, la adaptación a distintos dispositivos, la internacionalización con accesibilidad y el despliegue. La estimación total del Sprint es de 30 Story Points.

| Campo | Valor |
| --- | --- |
| Sprint Velocity | 30 Story Points |
| Total de Story Points | 30 |

#### 5.2.1.1. Sprint Planning 1

La reunión de planificación permitió definir el objetivo, alcance, responsabilidades y tareas del primer Sprint. El trabajo se enfocó en entregar un Landing Page responsive, accesible y coherente con los wireframes, mock-ups, Style Guidelines e Information Architecture definidos en el capítulo IV.

| **Sprint #** | **Sprint 1** |
| --- | --- |
| **Sprint Planning Background**  |
| Date | 2026-09-05 |
| Time | 08:00 PM |
| Location | Reunión virtual en Discord |
| Prepared By | Rodriguez Rojas, Miler Alexander |
| Attendees (to planning meeting) | Cayanchi Avila, Milenko Rubén / Herrera Enriquez, Diego Fernando / León Naupari, Jorge Mateo / Mendoza Blanco, Ariel Roberto / Rodriguez Rojas, Miler Alexander |
| Sprint 0 Review Summary | No aplica. El Sprint 1 es el primer Sprint del proyecto; no existe un incremento previo que revisar. |
| Sprint 0 Retrospective Summary | No aplica. El Sprint 1 es el primer Sprint del proyecto; no existe un Sprint previo sobre el cual realizar una retrospectiva. |
| **Sprint Goal & User Stories**  |
| Sprint 1 Goal | **Our focus is on** publishing a bilingual and responsive Landing Page that presents the VitalTrek value proposition to adventure tourism agencies and adventure tourists.<br>**We believe it delivers** a clear understanding of the solution and a direct channel to request information or a demo **to** visitors from both target segments.<br>**This will be confirmed when** the Landing Page is deployed on a public URL and visitors can browse all its sections in Spanish and English, and submit an information request from desktop and mobile web browsers. |
| Sprint 1 Velocity | 30 Story Points |
| Sum of Story Points | 30 Story Points (US01, US02, US03, US04, US05, US06, US33, TS01, TS02, TS03 y TS04) |


#### 5.2.1.2. Aspect Leaders and Collaborators

La siguiente matriz organiza el liderazgo y la colaboración del equipo durante el Sprint 1, en correspondencia con las tareas registradas en el Sprint Backlog.

| Integrante                       | Usuario de GitHub | Landing Page structure | Responsive UI | i18n y a11y | QA y deployment | Documentación |
| -------------------------------- | ----------------- | ---------------------- | ------------- | ----------- | --------------- | ------------- |
| Cayanchi Avila, Milenko Rubén    | `MaxghZZ`         | L                      | C             | C           | C               | L             |
| León Naupari, Jorge Mateo        | `mateool10`       | C                      | L             | C           | C               | C             |
| Mendoza Blanco, Ariel Roberto    | `Trepequiper`     | C                      | C             | L           | C               | C             |
| Rodriguez Rojas, Miler Alexander | `Miler2003`       | C                      | C             | C           | L               | L             |
| Herrera Enriquez, Diego Fernando | `DerDFHE`         | C                      | C             | C           | C               | C             |

**Leyenda:** L = Leader; C = Collaborator.

#### 5.2.1.3. Sprint Backlog 1

El Sprint Backlog 1 agrupa las siete User Stories de la Landing Page y las cuatro Technical Stories que la habilitan, seleccionadas desde el Product Backlog de la sección 3.3. La descomposición produjo veintiún Work-items, estimados individualmente entre 4 y 8 horas, con un total de 105 horas. Las tareas se repartieron según la matriz de líderes y colaboradores de la sección 5.2.1.2: cada integrante asume las tareas del aspecto que lidera y colabora en los aspectos restantes.
 
**Evidencia del Board del Sprint**

![Product Backlog de VitalTrek en Jira](../assets/images/chapter-3/product-backlog-jira.png)
 
*Figura 5.1. Board del Sprint 1 en Jira.*
 
**Enlace público del board Jira:** [Ver Product Backlog](https://milenkorvu.atlassian.net/jira/software/projects/SCRUM/boards/1/backlog)
 
| Sprint # | Story Id | Story Title | Task Id | Task Title | Task Description | Estimation (Hours) | Assigned To | Status |
| --- | --- | --- | --- | --- | --- | ---: | --- | --- |
| Sprint 1 | US01 | Navegación principal | T-01 | Estructura del header y de las secciones principales | Construir el encabezado y el esqueleto de las secciones del sitio con elementos semánticos, de modo que cada sección sea alcanzable desde la navegación. | 5 | Cayanchi Avila, Milenko Rubén | Done |
| Sprint 1 | US01 | Navegación principal | T-02 | Navegación para pantallas reducidas | Implementar el comportamiento de la navegación por debajo de 768 px conservando las mismas opciones que la vista de escritorio. | 4 | Herrera Enriquez, Diego Fernando | Done |
| Sprint 1 | US02 | Propuesta de valor | T-03 | Sección inicial con problema, solución y beneficios | Maquetar la sección inicial que presenta el problema de las zonas sin cobertura, la solución por checkpoints y los beneficios principales. | 6 | Cayanchi Avila, Milenko Rubén | Done |
| Sprint 1 | US02 | Propuesta de valor | T-04 | Contenido de beneficios por segmento | Redactar e integrar el contenido que diferencia los beneficios para agencias y para turistas, a partir de los insights del capítulo II. | 4 | Mendoza Blanco, Ariel Roberto | Done |
| Sprint 1 | US03 | Consulta de planes y precios | T-05 | Sección comparativa de planes | Construir la presentación de los planes con su precio, alcance y características, de forma que puedan compararse entre sí. | 5 | Rodriguez Rojas, Miler Alexander | Done |
| Sprint 1 | US03 | Consulta de planes y precios | T-06 | Continuidad desde el plan hacia el contacto | Enlazar cada plan con el formulario de contacto de modo que el plan de interés quede identificado en la solicitud. | 4 | Rodriguez Rojas, Miler Alexander | Done |
| Sprint 1 | US04 | Información del equipo | T-07 | Sección de equipo con los perfiles de NexaTech | Construir la sección de equipo con el nombre, el rol y la descripción de cada integrante, y sus fotografías. | 5 | Mendoza Blanco, Ariel Roberto | Done |
| Sprint 1 | US05 | Solicitud de información o demostración | T-08 | Formulario de contacto y estructura de campos | Construir el formulario con los campos requeridos para registrar una solicitud de información o demostración. | 5 | Mendoza Blanco, Ariel Roberto | Done |
| Sprint 1 | US05 | Solicitud de información o demostración | T-09 | Validación de campos obligatorios y formato de correo | Implementar la validación que impide el envío con campos obligatorios vacíos o con correo de formato inválido, e informa qué corregir. | 4 | Herrera Enriquez, Diego Fernando | Done |
| Sprint 1 | US06 | Consulta del contenido en el idioma del visitante | T-10 | Mecanismo de cambio de idioma y diccionario de claves | Implementar la función que recorre las cadenas marcadas y las sustituye por el bloque de idioma seleccionado. | 6 | León Naupari, Jorge Mateo | Done |
| Sprint 1 | US06 | Consulta del contenido en el idioma del visitante | T-11 | Persistencia de la preferencia de idioma | Conservar el idioma seleccionado entre visitas y actualizar el idioma declarado del documento al cambiarlo. | 4 | Mendoza Blanco, Ariel Roberto | Done |
| Sprint 1 | US33 | Consulta del tratamiento de datos personales | T-12 | Páginas de términos de servicio y política de privacidad | Construir ambas páginas con las categorías de datos registrados, su finalidad, el plazo de conservación y los derechos del titular. | 6 | León Naupari, Jorge Mateo | Done |
| Sprint 1 | US33 | Consulta del tratamiento de datos personales | T-13 | Contenido legal bilingüe y acceso desde el pie de página | Traducir el contenido legal a ambos idiomas y habilitar su acceso desde el pie de página de todas las vistas. | 5 | León Naupari, Jorge Mateo | Done |
| Sprint 1 | TS01 | Estructura técnica del Landing Page | T-14 | Estructura de directorios, tokens de estilo y README | Separar marcado, estilos y scripts en directorios propios, centralizar color y tipografía como variables, y documentar la estructura y la ejecución local. | 6 | Cayanchi Avila, Milenko Rubén | Done |
| Sprint 1 | TS02 | Adaptación del Landing Page a distintos dispositivos | T-15 | Adaptación a los anchos de referencia | Ajustar la presentación en 360, 768, 1024 y 1440 px verificando que no se produzca desplazamiento horizontal ni recorte de texto. | 8 | Herrera Enriquez, Diego Fernando | Done |
| Sprint 1 | TS02 | Adaptación del Landing Page a distintos dispositivos | T-16 | Áreas táctiles y escala tipográfica móvil | Verificar el área mínima de los controles interactivos y aplicar la escala tipográfica móvil por debajo de 768 px. | 4 | Herrera Enriquez, Diego Fernando | Done |
| Sprint 1 | TS03 | Internacionalización y accesibilidad del Landing Page | T-17 | Acceso al contenido principal, elementos semánticos y orden de tabulación | Incorporar el acceso directo al contenido principal como primer elemento enfocable, aplicar los elementos semánticos de referencia y verificar el orden de tabulación. | 6 | León Naupari, Jorge Mateo | Done |
| Sprint 1 | TS03 | Internacionalización y accesibilidad del Landing Page | T-18 | Verificación de contraste y textos alternativos | Comprobar que el contraste cumple WCAG 2.1 AA y que las imágenes informativas declaran texto alternativo descriptivo. | 5 | Rodriguez Rojas, Miler Alexander | Done |
| Sprint 1 | TS03 | Internacionalización y accesibilidad del Landing Page | T-19 | Paridad de claves entre los bloques de idioma | Verificar que ambos bloques de idioma contienen el mismo conjunto de claves y corregir las ausencias detectadas. | 4 | Mendoza Blanco, Ariel Roberto | Done |
| Sprint 1 | TS04 | Validación y despliegue del Landing Page | T-20 | Metadatos de identificación e indexación | Declarar en cada página el título, la descripción, la URL canónica, las alternativas de idioma y los metadatos de previsualización social. | 5 | León Naupari, Jorge Mateo | Done |
| Sprint 1 | TS04 | Validación y despliegue del Landing Page | T-21 | Validación del marcado, de los enlaces y despliegue | Ejecutar la validación del W3C, comprobar que ningún enlace interno responde 404 y publicar la versión aprobada desde la rama estable. | 4 | Rodriguez Rojas, Miler Alexander | Done |
 
**Resumen del Sprint Backlog 1**
 
| Concepto | Valor |
| --- | ---: |
| User Stories y Technical Stories asignadas | 11 |
| Work-items resultantes de la descomposición | 21 |
| Estimación mínima de una task | 4 horas |
| Estimación máxima de una task | 8 horas |
| Total de horas estimadas | 105 |
| Sum of Story Points | 30 |
 
**Distribución de la carga por integrante**
 
| Integrante | Tasks | Horas |
| --- | ---: | ---: |
| León Naupari, Jorge Mateo | 5 | 28 |
| Mendoza Blanco, Ariel Roberto | 5 | 22 |
| Herrera Enriquez, Diego Fernando | 4 | 20 |
| Rodriguez Rojas, Miler Alexander | 4 | 18 |
| Cayanchi Avila, Milenko Rubén | 3 | 17 |
| **Total** | **21** | **105** |
 
---

#### 5.2.1.4. Development Evidence for Sprint Review

##### Report Development Evidence
Durante el Sprint 1 se implementaron los componentes correspondientes al Report. La siguiente tabla relaciona cada cambio con su repositorio, rama, commit y fecha de realización.

| Repositorio                                                          | Rama                                           | Commit ID | Mensaje del commit                                                                                                            | Fecha      | Sección / Capítulo relacionada |
| -------------------------------------------------------------------- | ---------------------------------------------- | --------- | ----------------------------------------------------------------------------------------------------------------------------- | ---------- | ------------------------------ |
| [Reporte](https://github.com/1ASI0729-2620-16712-G4-Nexatech/report) | `develop`                                      | `dd2827f` | `Merge pull request #29 from 1ASI0729-2620-16712-G4-Nexatech/feature/chapter-5-development-evidence`                          | 2026-09-17 | Capítulo 5                     |
| [Reporte](https://github.com/1ASI0729-2620-16712-G4-Nexatech/report) | `feature/chapter-5-development-evidence`       | `f410575` | `docs(chapter5): add Jorge Mateo Leon commits to 5.2.1.4 development evidence`                                                | 2026-09-17 | Capítulo 5                     |
| [Reporte](https://github.com/1ASI0729-2620-16712-G4-Nexatech/report) | `develop`                                      | `842b4a3` | `Merge pull request #28 from 1ASI0729-2620-16712-G4-Nexatech/feature/chapter-5-collaboration-insights`                        | 2026-09-17 | Capítulo 5                     |
| [Reporte](https://github.com/1ASI0729-2620-16712-G4-Nexatech/report) | `feature/chapter-5-collaboration-insights`     | `e9ae4cc` | `docs(chapter5): complete 5.2.1.8 collaboration insights for Jorge Mateo Leon`                                                | 2026-09-17 | Capítulo 5                     |
| [Reporte](https://github.com/1ASI0729-2620-16712-G4-Nexatech/report) | `feature/chapter-5-collaboration-insights`     | `410f207` | `docs(chapter5): add collaboration evidence screenshots`                                                                      | 2026-09-17 | Capítulo 5                     |
| [Reporte](https://github.com/1ASI0729-2620-16712-G4-Nexatech/report) | `develop`                                      | `398d3e2` | `docs(chapter3): add epics table.`                                                                                            | 2026-09-17 | Capítulo 3                     |
| [Reporte](https://github.com/1ASI0729-2620-16712-G4-Nexatech/report) | `develop`                                      | `ed4bec2` | `docs(chapter3): update user stories:`                                                                                        | 2026-09-17 | Capítulo 3                     |
| [Reporte](https://github.com/1ASI0729-2620-16712-G4-Nexatech/report) | `main`                                         | `374dd07` | `chore: update readme.`                                                                                                       | 2026-09-17 | Documentación                  |
| [Reporte](https://github.com/1ASI0729-2620-16712-G4-Nexatech/report) | `main`                                         | `bfee799` | `chore: update readme.`                                                                                                       | 2026-09-17 | Documentación                  |
| [Reporte](https://github.com/1ASI0729-2620-16712-G4-Nexatech/report) | `feature/chapter-5`                            | `8b648e3` | `docs(chapter5): add chapter 5.`                                                                                              | 2026-09-17 | Capítulo 5                     |
| [Reporte](https://github.com/1ASI0729-2620-16712-G4-Nexatech/report) | `feature/chapter-5`                            | `abfcbf3` | `docs(chapter5): add chapter 5.`                                                                                              | 2026-09-17 | Capítulo 5                     |
| [Reporte](https://github.com/1ASI0729-2620-16712-G4-Nexatech/report) | `develop`                                      | `a5a3931` | `Merge branch 'feature/documentation-profile' into develop`                                                                   | 2026-09-16 | Documentación                  |
| [Reporte](https://github.com/1ASI0729-2620-16712-G4-Nexatech/report) | `feature/documentation-profile`                | `8519f14` | `docs: add Student Outcome section with communication criteria and actions`                                                   | 2026-09-16 | Documentación                  |
| [Reporte](https://github.com/1ASI0729-2620-16712-G4-Nexatech/report) | `feature/documentation-profile`                | `2856a3e` | `docs: add collaboration insights for project report`                                                                         | 2026-09-16 | Documentación                  |
| [Reporte](https://github.com/1ASI0729-2620-16712-G4-Nexatech/report) | `feature/documentation-profile`                | `7a1cc16` | `docs: add version history for project report`                                                                                | 2026-09-16 | Documentación                  |
| [Reporte](https://github.com/1ASI0729-2620-16712-G4-Nexatech/report) | `develop`                                      | `2196ad8` | `docs(chapter4): update section headings for consistency and clarity`                                                         | 2026-09-16 | Capítulo 4                     |
| [Reporte](https://github.com/1ASI0729-2620-16712-G4-Nexatech/report) | `feature/documentation-profile`                | `a460900` | `docs: add cover page for final project report`                                                                               | 2026-09-16 | Documentación                  |
| [Reporte](https://github.com/1ASI0729-2620-16712-G4-Nexatech/report) | `feature/chapter-4-wireframes`                 | `027a2a1` | `docs(chapter4): add login wireframes and mockups.`                                                                           | 2026-09-15 | Capítulo 4                     |
| [Reporte](https://github.com/1ASI0729-2620-16712-G4-Nexatech/report) | `feature/chapter-4-wireframes`                 | `737470f` | `docs(chapter4): add wireframes and mockups descriptions.`                                                                    | 2026-09-15 | Capítulo 4                     |
| [Reporte](https://github.com/1ASI0729-2620-16712-G4-Nexatech/report) | `feature/chapter-4-wireframes`                 | `0f63dd3` | `docs(chapter4): add wireframes and mockups web.`                                                                             | 2026-09-15 | Capítulo 4                     |
| [Reporte](https://github.com/1ASI0729-2620-16712-G4-Nexatech/report) | `feature/chapter-4-wireframes`                 | `0bd53a1` | `docs(chapter4): add assets`                                                                                                  | 2026-09-15 | Capítulo 4                     |
| [Reporte](https://github.com/1ASI0729-2620-16712-G4-Nexatech/report) | `feature/chapter-4-wireframes`                 | `f7a00a6` | `docs(chapter4): add wireframes and mockups web.`                                                                             | 2026-09-14 | Capítulo 4                     |
| [Reporte](https://github.com/1ASI0729-2620-16712-G4-Nexatech/report) | `feature/chapter-4-wireframes`                 | `4f39ddb` | `docs(chapter4): add wireframes and mockups web.`                                                                             | 2026-09-14 | Capítulo 4                     |
| [Reporte](https://github.com/1ASI0729-2620-16712-G4-Nexatech/report) | `feature/chapter4-architecture`                | `b5ec32a` | `docs(chapter4): add class diagrams.`                                                                                         | 2026-09-13 | Capítulo 4                     |
| [Reporte](https://github.com/1ASI0729-2620-16712-G4-Nexatech/report) | `develop`                                      | `06a7842` | `Merge pull request #24 from 1ASI0729-2620-16712-G4-Nexatech/feature/chapter-4-event-storming`                                | 2026-09-13 | Capítulo 4                     |
| [Reporte](https://github.com/1ASI0729-2620-16712-G4-Nexatech/report) | `feature/chapter-4-event-storming`             | `5525c8b` | `docs(chapter4): add 4.6.1 design-level event storming`                                                                       | 2026-09-13 | Capítulo 4                     |
| [Reporte](https://github.com/1ASI0729-2620-16712-G4-Nexatech/report) | `feature/chapter-4-event-storming`             | `cdf9343` | `docs(chapter4): add event storming board screenshots`                                                                        | 2026-09-13 | Capítulo 4                     |
| [Reporte](https://github.com/1ASI0729-2620-16712-G4-Nexatech/report) | `develop`                                      | `a114277` | `Merge remote-tracking branch 'origin/develop' into develop`                                                                  | 2026-09-13 | Documentación                  |
| [Reporte](https://github.com/1ASI0729-2620-16712-G4-Nexatech/report) | `feature/chapter-4-database`                   | `ba5ba04` | `docs(chapter4): add database diagram`                                                                                        | 2026-09-13 | Capítulo 4                     |
| [Reporte](https://github.com/1ASI0729-2620-16712-G4-Nexatech/report) | `feature/chapter-4-database`                   | `50d57b4` | `docs(chapter4): add database diagram`                                                                                        | 2026-09-13 | Capítulo 4                     |
| [Reporte](https://github.com/1ASI0729-2620-16712-G4-Nexatech/report) | `feature/chapter4-architecture`                | `dabdd80` | `docs(chapter4): add software achitecture diagrams.`                                                                          | 2026-09-13 | Capítulo 4                     |
| [Reporte](https://github.com/1ASI0729-2620-16712-G4-Nexatech/report) | `feature/chapter4-architecture`                | `2384479` | `docs(chapter4): add software achitecture diagrams.`                                                                          | 2026-09-13 | Capítulo 4                     |
| [Reporte](https://github.com/1ASI0729-2620-16712-G4-Nexatech/report) | `develop`                                      | `df04fcb` | `Merge pull request #20 from 1ASI0729-2620-16712-G4-Nexatech/feature/chapter4-architecture`                                   | 2026-09-12 | Capítulo 4                     |
| [Reporte](https://github.com/1ASI0729-2620-16712-G4-Nexatech/report) | `feature/chapter4-architecture`                | `792c63c` | `docs(chapter4): add sections 4.6.2 context and 4.6.3 container diagrams`                                                     | 2026-09-12 | Capítulo 4                     |
| [Reporte](https://github.com/1ASI0729-2620-16712-G4-Nexatech/report) | `develop`                                      | `727277d` | `Merge branch 'feature/chapter-4-information-architecture' into develop`                                                      | 2026-09-10 | Capítulo 4                     |
| [Reporte](https://github.com/1ASI0729-2620-16712-G4-Nexatech/report) | `feature/chapter-4-information-architecture`   | `d798a57` | `docs(chapter4): add section on information architecture and organization systems`                                            | 2026-09-10 | Capítulo 4                     |
| [Reporte](https://github.com/1ASI0729-2620-16712-G4-Nexatech/report) | `feature/chapter-4-style-guidelines`           | `ba24361` | `Feature/chapter 4 style guidelines`                                                                                          | 2026-09-10 | Capítulo 4                     |
| [Reporte](https://github.com/1ASI0729-2620-16712-G4-Nexatech/report) | `feature/chapter-4-style-guidelines`           | `708d7cc` | `docs(chapter4): add chapter 4.1 Style Guidelines`                                                                            | 2026-09-10 | Capítulo 4                     |
| [Reporte](https://github.com/1ASI0729-2620-16712-G4-Nexatech/report) | `feature/chapter-4-style-guidelines`           | `4f0a81d` | `docs(chapter4): add chapter 4`                                                                                               | 2026-09-10 | Capítulo 4                     |
| [Reporte](https://github.com/1ASI0729-2620-16712-G4-Nexatech/report) | `feature/chapter-3-product-backlog`            | `14fc8b5` | `docs: add point 3.3 product backlog`                                                                                         | 2026-09-09 | Capítulo 3                     |
| [Reporte](https://github.com/1ASI0729-2620-16712-G4-Nexatech/report) | `feature/chapter-3-product-backlog`            | `de00def` | `docs: add point 3.3 product backlog`                                                                                         | 2026-09-09 | Capítulo 3                     |
| [Reporte](https://github.com/1ASI0729-2620-16712-G4-Nexatech/report) | `develop`                                      | `3f61ff8` | `Merge branch 'feature/chapter3-impact-mapping' into develop`                                                                 | 2026-09-09 | Capítulo 3                     |
| [Reporte](https://github.com/1ASI0729-2620-16712-G4-Nexatech/report) | `feature/chapter3-impact-mapping`              | `4744c54` | `docs(chapter3): add impact mapping diagram`                                                                                  | 2026-09-09 | Capítulo 3                     |
| [Reporte](https://github.com/1ASI0729-2620-16712-G4-Nexatech/report) | `feature/chapter3-impact-mapping`              | `9610c3d` | `docs(chapter3): add impact mapping section with user personas and business goals`                                            | 2026-09-09 | Capítulo 3                     |
| [Reporte](https://github.com/1ASI0729-2620-16712-G4-Nexatech/report) | `develop`                                      | `256b027` | `docs(chapter2): update section headings and improve structure for clarity`                                                   | 2026-09-09 | Capítulo 2                     |
| [Reporte](https://github.com/1ASI0729-2620-16712-G4-Nexatech/report) | `feature/chapter-3-user-stories`               | `82de5d3` | `docs: add chapter 3.1 user stories`                                                                                          | 2026-09-08 | Capítulo 3                     |
| [Reporte](https://github.com/1ASI0729-2620-16712-G4-Nexatech/report) | `feature/chapter-3-user-stories`               | `85f00c5` | `docs: add chapter 3.1 user stories`                                                                                          | 2026-09-08 | Capítulo 3                     |
| [Reporte](https://github.com/1ASI0729-2620-16712-G4-Nexatech/report) | `feature/chapter-3-event-storming`             | `d5e5cc2` | `docs: update event storming`                                                                                                 | 2026-09-08 | Capítulo 3                     |
| [Reporte](https://github.com/1ASI0729-2620-16712-G4-Nexatech/report) | `feature/chapter-3-user-journey`               | `fa74dfa` | `docs: add user journey maping`                                                                                               | 2026-09-08 | Capítulo 3                     |
| [Reporte](https://github.com/1ASI0729-2620-16712-G4-Nexatech/report) | `feature/chapter-3-event-storming`             | `796d8a7` | `docs: add event storming point`                                                                                              | 2026-09-08 | Capítulo 3                     |
| [Reporte](https://github.com/1ASI0729-2620-16712-G4-Nexatech/report) | `feature/chapter-3-event-storming`             | `4c1ac88` | `docs: add event storming point`                                                                                              | 2026-09-08 | Capítulo 3                     |
| [Reporte](https://github.com/1ASI0729-2620-16712-G4-Nexatech/report) | `feature/chapter-3-event-storming`             | `c4e1e45` | `docs: add event storming image`                                                                                              | 2026-09-08 | Capítulo 3                     |
| [Reporte](https://github.com/1ASI0729-2620-16712-G4-Nexatech/report) | `develop`                                      | `d335beb` | `Merge branch 'feature/chapter-2-graficos-entrevistas' into develop`                                                          | 2026-09-08 | Capítulo 2                     |
| [Reporte](https://github.com/1ASI0729-2620-16712-G4-Nexatech/report) | `feature/chapter-2-graficos-entrevistas`       | `7cf074a` | `docs(chapter2): add graphical representations for agency and tourist data`                                                   | 2026-09-08 | Capítulo 2                     |
| [Reporte](https://github.com/1ASI0729-2620-16712-G4-Nexatech/report) | `feature/chapter-2-graficos-entrevistas`       | `2b36dfb` | `docs(chapter2): update interview analysis and add visual data representation`                                                | 2026-09-08 | Capítulo 2                     |
| [Reporte](https://github.com/1ASI0729-2620-16712-G4-Nexatech/report) | `develop`                                      | `2ff9f6e` | `Merge pull request #15 from Vitalrek-Project/feature/chapter2-user-task-matrix`                                              | 2026-09-07 | Capítulo 2                     |
| [Reporte](https://github.com/1ASI0729-2620-16712-G4-Nexatech/report) | `feature/chapter2-user-task-matrix`            | `fd23036` | `docs(chapter2): agregar seccion 2.3.2 User Task Matrix`                                                                      | 2026-09-07 | Capítulo 2                     |
| [Reporte](https://github.com/1ASI0729-2620-16712-G4-Nexatech/report) | `feature/chapter-2-user-segments`              | `bde7426` | `docs: add users by object segment`                                                                                           | 2026-09-07 | Capítulo 2                     |
| [Reporte](https://github.com/1ASI0729-2620-16712-G4-Nexatech/report) | `feature/chapter-2-user-segments`              | `0681347` | `docs: add users by object segment`                                                                                           | 2026-09-07 | Capítulo 2                     |
| [Reporte](https://github.com/1ASI0729-2620-16712-G4-Nexatech/report) | `develop`                                      | `495d242` | `docs: update document points`                                                                                                | 2026-09-07 | Documentación                  |
| [Reporte](https://github.com/1ASI0729-2620-16712-G4-Nexatech/report) | `develop`                                      | `ae2b8db` | `Merge pull request #13 from Vitalrek-Project/feature/chapter2-ubiquitous-language-v2`                                        | 2026-09-07 | Capítulo 2                     |
| [Reporte](https://github.com/1ASI0729-2620-16712-G4-Nexatech/report) | `feature/chapter2-ubiquitous-language-v2`      | `50ff348` | `docs(chapter2): agregar seccion 2.5 Ubiquitous Language`                                                                     | 2026-09-07 | Capítulo 2                     |
| [Reporte](https://github.com/1ASI0729-2620-16712-G4-Nexatech/report) | `feature/chapter-1`                            | `66a2a15` | `docs(chapter1): add member photo and description`                                                                            | 2026-09-07 | Capítulo 1                     |
| [Reporte](https://github.com/1ASI0729-2620-16712-G4-Nexatech/report) | `main`                                         | `beb1ee5` | `docs(readme): fix team`                                                                                                      | 2026-09-07 | Documentación                  |
| [Reporte](https://github.com/1ASI0729-2620-16712-G4-Nexatech/report) | `develop`                                      | `9896b41` | `Merge branch 'feature/chapter-2-analissi-entrevistas' into develop`                                                          | 2026-09-07 | Capítulo 2                     |
| [Reporte](https://github.com/1ASI0729-2620-16712-G4-Nexatech/report) | `feature/chapter-2-analissi-entrevistas`       | `d192aa5` | `docs(chapter2): refine interview analysis for adventure tourism stakeholders`                                                | 2026-09-07 | Capítulo 2                     |
| [Reporte](https://github.com/1ASI0729-2620-16712-G4-Nexatech/report) | `feature/chapter-2-analissi-entrevistas`       | `37ad77b` | `docs(chapter2): add interview analysis for adventure tourism stakeholders`                                                   | 2026-09-07 | Capítulo 2                     |
| [Reporte](https://github.com/1ASI0729-2620-16712-G4-Nexatech/report) | `develop`                                      | `56c6462` | `Merge branch 'feature/chapter2-entrevistas' into develop`                                                                    | 2026-09-07 | Capítulo 2                     |
| [Reporte](https://github.com/1ASI0729-2620-16712-G4-Nexatech/report) | `feature/chapter2-entrevistas`                 | `22767b7` | `Merge branch 'develop' of https://github.com/Vitalrek-Project/VitalRek-Documents into feature/chapter2-entrevistas`          | 2026-09-07 | Capítulo 2                     |
| [Reporte](https://github.com/1ASI0729-2620-16712-G4-Nexatech/report) | `feature/chapter2-entrevistas`                 | `0f7cf2c` | `docs(chapter2): add interview segment images to assets`                                                                      | 2026-09-07 | Capítulo 2                     |
| [Reporte](https://github.com/1ASI0729-2620-16712-G4-Nexatech/report) | `feature/chapter2-entrevista-segmento1`        | `f237d53` | `docs(chapter2): update interview details with extended summaries and additional records`                                     | 2026-09-07 | Capítulo 2                     |
| [Reporte](https://github.com/1ASI0729-2620-16712-G4-Nexatech/report) | `develop`                                      | `296689b` | `Merge branch 'feature/chapter2-entrevista-segmento1' into develop`                                                           | 2026-09-07 | Capítulo 2                     |
| [Reporte](https://github.com/1ASI0729-2620-16712-G4-Nexatech/report) | `feature/chapter2-entrevista-segmento1`        | `30aa8c0` | `Merge branch 'develop' of https://github.com/Vitalrek-Project/VitalRek-Documents into feature/chapter2-entrevista-segmento1` | 2026-09-07 | Capítulo 2                     |
| [Reporte](https://github.com/1ASI0729-2620-16712-G4-Nexatech/report) | `feature/chapter2-entrevista-segmento1`        | `7d17d15` | `docs(chapter2): update interview records and add project configuration files`                                                | 2026-09-07 | Capítulo 2                     |
| [Reporte](https://github.com/1ASI0729-2620-16712-G4-Nexatech/report) | `develop`                                      | `56474a5` | `Merge branch 'feature/chapter-2-analisis-entrevistas' into develop`                                                          | 2026-09-07 | Capítulo 2                     |
| [Reporte](https://github.com/1ASI0729-2620-16712-G4-Nexatech/report) | `feature/chapter-2-analisis-entrevistas`       | `98bda71` | `docs(chapter2): add analysis of interviews with adventure tourism stakeholders`                                              | 2026-09-07 | Capítulo 2                     |
| [Reporte](https://github.com/1ASI0729-2620-16712-G4-Nexatech/report) | `feature/chapter-2-entrevista-miler-rodriguez` | `cf441d0` | `docs: add second interview`                                                                                                  | 2026-09-06 | Capítulo 2                     |
| [Reporte](https://github.com/1ASI0729-2620-16712-G4-Nexatech/report) | `feature/chapter-2-entrevista-miler-rodriguez` | `64c6608` | `docs: add second interview`                                                                                                  | 2026-09-06 | Capítulo 2                     |
| [Reporte](https://github.com/1ASI0729-2620-16712-G4-Nexatech/report) | `develop`                                      | `a3efb26` | `Merge branch 'feature/chapter-2-entrevista-miler-rodriguez' into develop`                                                    | 2026-09-06 | Capítulo 2                     |
| [Reporte](https://github.com/1ASI0729-2620-16712-G4-Nexatech/report) | `feature/chapter-2-entrevista-miler-rodriguez` | `fbc3b37` | `docs(chapter2): add details for second interview with Celeste Rodriguez`                                                     | 2026-09-06 | Capítulo 2                     |
| [Reporte](https://github.com/1ASI0729-2620-16712-G4-Nexatech/report) | `feature/chapter-2-entrevista-miler-rodriguez` | `cbbcf3e` | `docs: add image for third interview segment 1 into assets file`                                                              | 2026-09-06 | Capítulo 2                     |
| [Reporte](https://github.com/1ASI0729-2620-16712-G4-Nexatech/report) | `feature/chapter-2-entrevista-miler-rodriguez` | `7ca0097` | `docs(chapter2): add evidence for third interview with Miler Rodriguez`                                                       | 2026-09-06 | Capítulo 2                     |
| [Reporte](https://github.com/1ASI0729-2620-16712-G4-Nexatech/report) | `feature/chapter-2-entrevista-miler-rodriguez` | `c8f57f4` | `docs(chapter2): add second interview details for Celeste Rodriguez`                                                          | 2026-09-06 | Capítulo 2                     |
| [Reporte](https://github.com/1ASI0729-2620-16712-G4-Nexatech/report) | `feature/chapter2-entrevista-segmento1`        | `defbc42` | `docs(chapter2): agregar registro entrevista 2 segmento 1`                                                                    | 2026-09-06 | Capítulo 2                     |
| [Reporte](https://github.com/1ASI0729-2620-16712-G4-Nexatech/report) | `feature/chapter2-entrevista-segmento1`        | `f959752` | `docs(chapter2): agregar registro entrevista 2 segmento 1`                                                                    | 2026-09-06 | Capítulo 2                     |
| [Reporte](https://github.com/1ASI0729-2620-16712-G4-Nexatech/report) | `feature/chapter2-entrevista-segmento1`        | `193f12a` | `evidencia entrevista 2 segmento 1`                                                                                           | 2026-09-06 | Capítulo 2                     |
| [Reporte](https://github.com/1ASI0729-2620-16712-G4-Nexatech/report) | `develop`                                      | `d3ee05a` | `Merge branch 'feature/chapter2-entrevistas' into develop`                                                                    | 2026-09-06 | Capítulo 2                     |
| [Reporte](https://github.com/1ASI0729-2620-16712-G4-Nexatech/report) | `feature/chapter2-entrevistas`                 | `b413637` | `docs(chapter2): add interviews`                                                                                              | 2026-09-06 | Capítulo 2                     |
| [Reporte](https://github.com/1ASI0729-2620-16712-G4-Nexatech/report) | `feature/chapter2-entrevistas`                 | `0132a61` | `docs: add interviews`                                                                                                        | 2026-09-06 | Capítulo 2                     |
| [Reporte](https://github.com/1ASI0729-2620-16712-G4-Nexatech/report) | `feature/chapter2-entrevistas`                 | `30cbdac` | `docs: add interviews`                                                                                                        | 2026-09-06 | Capítulo 2                     |
| [Reporte](https://github.com/1ASI0729-2620-16712-G4-Nexatech/report) | `main`                                         | `cc46ed5` | `docs: update readme`                                                                                                         | 2026-09-04 | Documentación                  |
| [Reporte](https://github.com/1ASI0729-2620-16712-G4-Nexatech/report) | `feature/chapter-2-interview-design`           | `fe22b36` | `docs: add interview design section (2.2.1) to Chapter2.md`                                                                   | 2026-09-04 | Capítulo 2                     |
| [Reporte](https://github.com/1ASI0729-2620-16712-G4-Nexatech/report) | `feature/chapter-2-interview-design`           | `af48411` | `docs: add interview design section (2.2.1) to Chapter2.md`                                                                   | 2026-09-04 | Capítulo 2                     |
| [Reporte](https://github.com/1ASI0729-2620-16712-G4-Nexatech/report) | `feature/chapter-2-competitor-analysis`        | `686c807` | `docs: add competitor analysis section (2.1) to Chapter2.md`                                                                  | 2026-09-04 | Capítulo 2                     |
| [Reporte](https://github.com/1ASI0729-2620-16712-G4-Nexatech/report) | `feature/chapter-2-competitor-analysis`        | `d7620ad` | `docs: add competitor analysis section (2.1) to Chapter2.md`                                                                  | 2026-09-04 | Capítulo 2                     |
| [Reporte](https://github.com/1ASI0729-2620-16712-G4-Nexatech/report) | `feature/chapter1-solution-profile`            | `18f0e58` | `docs: update lean ux assumption.`                                                                                            | 2026-09-01 | Capítulo 1                     |
| [Reporte](https://github.com/1ASI0729-2620-16712-G4-Nexatech/report) | `feature/chapter1-solution-profile`            | `d4bca68` | `docs: update lean ux assumption.`                                                                                            | 2026-09-01 | Capítulo 1                     |
| [Reporte](https://github.com/1ASI0729-2620-16712-G4-Nexatech/report) | `feature/chapter1-solution-profile`            | `b3e69c0` | `docs: update problem statement.`                                                                                             | 2026-09-01 | Capítulo 1                     |
| [Reporte](https://github.com/1ASI0729-2620-16712-G4-Nexatech/report) | `feature/chapter1-solution-profile`            | `eb6ccb8` | `docs: update problem statement.`                                                                                             | 2026-09-01 | Capítulo 1                     |
| [Reporte](https://github.com/1ASI0729-2620-16712-G4-Nexatech/report) | `develop`                                      | `3620c5f` | `Merge branch 'feature/chapter1-solution-profile' into develop`                                                               | 2026-09-01 | Capítulo 1                     |
| [Reporte](https://github.com/1ASI0729-2620-16712-G4-Nexatech/report) | `feature/chapter1-solution-profile`            | `897a35a` | `docs(chapter1): fix 1.2.2.3 Lean UX Hypothesis Statement`                                                                    | 2026-09-01 | Capítulo 1                     |
| [Reporte](https://github.com/1ASI0729-2620-16712-G4-Nexatech/report) | `feature/chapter1-solution-profile`            | `7f28d62` | `docs: update Jorge's photo filename in Chapter1 and adjust image path`                                                       | 2026-09-01 | Capítulo 1                     |
| [Reporte](https://github.com/1ASI0729-2620-16712-G4-Nexatech/report) | `feature/chapter1-solution-profile`            | `3e34365` | `docs: update team profiles and add Lean UX Canvas details`                                                                   | 2026-09-01 | Capítulo 1                     |
| [Reporte](https://github.com/1ASI0729-2620-16712-G4-Nexatech/report) | `feature/chapter1-solution-profile`            | `4a20f6f` | `fix: resolve merge conflict in Chapter1`                                                                                     | 2026-09-01 | Capítulo 1                     |
| [Reporte](https://github.com/1ASI0729-2620-16712-G4-Nexatech/report) | `feature/chapter1-solution-profile`            | `1dedf24` | `docs: update team member profiles; add Ariel's photo and description`                                                        | 2026-09-01 | Capítulo 1                     |
| [Reporte](https://github.com/1ASI0729-2620-16712-G4-Nexatech/report) | `feature/chapter1-solution-profile`            | `37a9c73` | `docs: add Ariel's photo to assets`                                                                                           | 2026-09-01 | Capítulo 1                     |
| [Reporte](https://github.com/1ASI0729-2620-16712-G4-Nexatech/report) | `feature/chapter1-solution-profile`            | `7cd5d4a` | `docs: refine team member profiles; update Miler's photo and descriptions`                                                    | 2026-09-01 | Capítulo 1                     |
| [Reporte](https://github.com/1ASI0729-2620-16712-G4-Nexatech/report) | `feature/chapter1-solution-profile`            | `bed538d` | `docs: update team member profiles; include Lean UX Canvas image`                                                             | 2026-09-01 | Capítulo 1                     |
| [Reporte](https://github.com/1ASI0729-2620-16712-G4-Nexatech/report) | `feature/chapter1-solution-profile`            | `23a15be` | `docs: add Miler's photo to assets`                                                                                           | 2026-09-01 | Capítulo 1                     |
| [Reporte](https://github.com/1ASI0729-2620-16712-G4-Nexatech/report) | `feature/chapter1-solution-profile`            | `2476747` | `docs: add image of lean ux canvas into assets file`                                                                          | 2026-09-01 | Capítulo 1                     |
| [Reporte](https://github.com/1ASI0729-2620-16712-G4-Nexatech/report) | `feature/chapter1-solution-profile`            | `49fcc4d` | `docs: add Lean UX Canvas section with detailed descriptions and structured content`                                          | 2026-09-01 | Capítulo 1                     |
| [Reporte](https://github.com/1ASI0729-2620-16712-G4-Nexatech/report) | `feature/chapter1-solution-profile`            | `0be047c` | `docs: add team profile (Ariel) and Lean UX hypothesis statements (1.2.2.3. Lean UX Hypothesis Statement)`                    | 2026-08-30 | Capítulo 1                     |
| [Reporte](https://github.com/1ASI0729-2620-16712-G4-Nexatech/report) | `feature/chapter1-solution-profile`            | `23c2fdd` | `docs: add team profile (Ariel) and Lean UX hypothesis statements (1.2.2.3)`                                                  | 2026-08-30 | Capítulo 1                     |
| [Reporte](https://github.com/1ASI0729-2620-16712-G4-Nexatech/report) | `feature/chapter1-solution-profile`            | `a5d158f` | `Update Chapter1.md`                                                                                                          | 2026-08-30 | Capítulo 1                     |
| [Reporte](https://github.com/1ASI0729-2620-16712-G4-Nexatech/report) | `feature/chapter1-solution-profile`            | `790af9c` | `Add files via upload`                                                                                                        | 2026-08-30 | Capítulo 1                     |
| [Reporte](https://github.com/1ASI0729-2620-16712-G4-Nexatech/report) | `main`                                         | `9cfa9d6` | `Update README.md`                                                                                                            | 2026-08-30 | Documentación                  |
| [Reporte](https://github.com/1ASI0729-2620-16712-G4-Nexatech/report) | `main`                                         | `95b583a` | `Update README.md`                                                                                                            | 2026-08-30 | Documentación                  |
| [Reporte](https://github.com/1ASI0729-2620-16712-G4-Nexatech/report) | `main`                                         | `9ae61f6` | `docs: update the data in the README file.`                                                                                   | 2026-08-30 | Documentación                  |
| [Reporte](https://github.com/1ASI0729-2620-16712-G4-Nexatech/report) | `feature/chapter1-solution-profile`            | `86f8263` | `docs: update section 1.3 - align target segments with checkpoint-based monitoring language`                                  | 2026-08-30 | Capítulo 1                     |
| [Reporte](https://github.com/1ASI0729-2620-16712-G4-Nexatech/report) | `feature/chapter1-solution-profile`            | `58fbaee` | `docs: add section 1.3 - align target segments with checkpoint-based monitoring language.`                                    | 2026-08-30 | Capítulo 1                     |
| [Reporte](https://github.com/1ASI0729-2620-16712-G4-Nexatech/report) | `feature/chapter1-solution-profile`            | `d05545e` | `docs: add section 1.2.1 fix real time monitoring language to checkpoint-based alerts.`                                       | 2026-08-30 | Capítulo 1                     |
| [Reporte](https://github.com/1ASI0729-2620-16712-G4-Nexatech/report) | `feature/chapter1-solution-profile`            | `9ef7345` | `docs: add section 1.2.1 fix real time monitoring language to checkpoint-based alerts.`                                       | 2026-08-30 | Capítulo 1                     |
| [Reporte](https://github.com/1ASI0729-2620-16712-G4-Nexatech/report) | `main`                                         | `afe4cdb` | `add structure base od readme.`                                                                                               | 2026-08-30 | Documentación                  |
| [Reporte](https://github.com/1ASI0729-2620-16712-G4-Nexatech/report) | `main`                                         | `1d4261c` | `add structure base od readme.`                                                                                               | 2026-08-30 | Documentación                  |
| [Reporte](https://github.com/1ASI0729-2620-16712-G4-Nexatech/report) | `feature/chapter1-solution-profile`            | `87f7b69` | `feat: create first chapter file`                                                                                             | 2026-08-30 | Capítulo 1                     |
| [Reporte](https://github.com/1ASI0729-2620-16712-G4-Nexatech/report) | `feature/chapter1-solution-profile`            | `a10b6e0` | `feat: create first chapter file`                                                                                             | 2026-08-30 | Capítulo 1                     |
| [Reporte](https://github.com/1ASI0729-2620-16712-G4-Nexatech/report) | `main`                                         | `6b44ca3` | `Initial commit`                                                                                                              | 2026-08-29 | Configuración inicial          |


##### Landing Page Development Evidence
Durante el Sprint 1 se implementaron los componentes correspondientes al Landing Page. La siguiente tabla relaciona cada cambio con su repositorio, rama, commit y fecha de realización.

| Repositorio                                                                     | Rama                       | Commit ID | Mensaje del commit                                      | Fecha      | User Story relacionada |
| ------------------------------------------------------------------------------- | -------------------------- | --------- | ------------------------------------------------------- | ---------- | ---------------------- |
| [Landing Page](https://github.com/1ASI0729-2620-16712-G4-Nexatech/landing-page) | `feature/landing-seo-a11y` | `2cebb2f` | `docs(readme): fix brand asset file extensions`         | 2026-09-17 | US01–US06              |
| [Landing Page](https://github.com/1ASI0729-2620-16712-G4-Nexatech/landing-page) | `feature/landing-seo-a11y` | `d216d5e` | `feat(a11y): add skip to main content link`             | 2026-09-17 | US01–US06              |
| [Landing Page](https://github.com/1ASI0729-2620-16712-G4-Nexatech/landing-page) | `feature/landing-seo-a11y` | `9252476` | `feat(seo): complete meta tags defined in report 4.2.3` | 2026-09-17 | US01–US06              |
| [Landing Page](https://github.com/1ASI0729-2620-16712-G4-Nexatech/landing-page) | `feature/landing-seo-a11y` | `b296ddc` | `feat(i18n): add skip link translation keys`            | 2026-09-17 | US01–US06              |
| [Landing Page](https://github.com/1ASI0729-2620-16712-G4-Nexatech/landing-page) | `feature/landing-seo-a11y` | `36b333b` | `style(a11y): add skip link styles`                     | 2026-09-17 | US01–US06              |
| [Landing Page](https://github.com/1ASI0729-2620-16712-G4-Nexatech/landing-page) | `main`                     | `11ac9e2` | `chore(team): fix Team Member`                          | 2026-09-17 | US04                   |
| [Landing Page](https://github.com/1ASI0729-2620-16712-G4-Nexatech/landing-page) | `main`                     | `645afa1` | `chore(team): add Team Member`                          | 2026-09-17 | US04                   |
| [Landing Page](https://github.com/1ASI0729-2620-16712-G4-Nexatech/landing-page) | `main`                     | `9a91594` | `2da version landing page`                              | 2026-09-12 | US01–US06              |
| [Landing Page](https://github.com/1ASI0729-2620-16712-G4-Nexatech/landing-page) | `main`                     | `117ad46` | `docs: add project documentation`                       | 2026-09-08 | Documentación          |
| [Landing Page](https://github.com/1ASI0729-2620-16712-G4-Nexatech/landing-page) | `main`                     | `935e346` | `docs: add project documentation`                       | 2026-09-08 | Documentación          |
| [Landing Page](https://github.com/1ASI0729-2620-16712-G4-Nexatech/landing-page) | `main`                     | `869b9db` | `Initial commit`                                        | 2026-08-30 | Configuración inicial  |

![Commits del Sprint 1](../assets/images/chapter-5/development-commits.png)

*Figura 5.2. Commits relacionados con la implementación del Landing Page durante el Sprint 1.*

#### 5.2.1.5. Execution Evidence for Sprint Review

La ejecución del Sprint produjo una primera versión funcional del Landing Page. La página presenta la propuesta de valor de VitalTrek, explica el problema de monitoreo en rutas remotas, muestra el funcionamiento por checkpoints, diferencia los beneficios para operadores y turistas, presenta las funcionalidades, planes, equipo, preguntas frecuentes y formulario de contacto.

![Landing Page desktop](../assets/images/chapter-4/mockups/hero-metrics.png)

*Figura 5.3. Vista desktop del Landing Page implementado.*

![Secciones principales del Landing Page](../assets/images/chapter-5/landing-page-sections.png)

*Figura 5.4. Secciones principales implementadas en el Sprint 1.*

La validación visual comprende la navegación entre secciones, el comportamiento responsive, el cambio de idioma, los call-to-action, el formulario de contacto y la legibilidad del contenido.

#### 5.2.1.6. Services Documentation Evidence for Sprint Review

El alcance del Sprint 1 se limita al Landing Page estático desarrollado con HTML5, CSS3 y JavaScript. No se implementaron endpoints RESTful ni una API en este Sprint; por ello, la documentación OpenAPI y Swagger no aplican a esta entrega. La implementación de Web Services se planifica para una entrega posterior.

| Producto             | Endpoint              | Método HTTP | Estado      |
| -------------------- | --------------------- | ----------- | ----------- |
| RESTful Web Services | No aplica en Sprint 1 | No aplica   | Planificado |

#### 5.2.1.7. Software Deployment Evidence for Sprint Review

La primera versión del Landing Page se publica desde el repositorio de GitHub hacia la plataforma de despliegue configurada.

| Elemento             | Información                                                     |
| -------------------- | --------------------------------------------------------------- |
| Producto             | Landing Page                                                    |
| Plataforma           | Vercel                                                          |
| Repositorio          | https://github.com/1ASI0729-2620-16712-G4-Nexatech/landing-page |
| Rama desplegada      | main                                                            |
| Build command        | No aplica para HTML5, CSS3 y JavaScript estático                |
| Output directory     | Directorio raíz del repositorio                                 |
| Variables de entorno | No requeridas                                                   |
| URL pública          | https://landing-page-mrca1.vercel.app/                          |

![Configuración del despliegue](../assets/images/chapter-5/deployment-configuration.png)

*Figura 5.5. Configuración del proyecto en la plataforma de despliegue.*

![Despliegue exitoso](../assets/images/chapter-5/deployment-success.png)

*Figura 5.6. Despliegue exitoso de la primera versión del Landing Page.*

**Landing Page desplegado:** [https://landing-page-mrca1.vercel.app/](https://landing-page-mrca1.vercel.app/)

#### 5.2.1.8. Team Collaboration Insights during Sprint

El trabajo colaborativo del Sprint 1 se realizó mediante GitHub, Jira/Trello y herramientas de diseño. Cada integrante participó en actividades de planificación, diseño, implementación, validación o documentación.

![GitHub Insights del Sprint 1](../assets/images/chapter-5/github-insights.png)

*Figura 5.7. Analítica de colaboración del repositorio durante el Sprint 1.*

![Participación mediante commits](../assets/images/chapter-5/team-commits.png)

*Figura 5.8. Participación de los integrantes mediante commits.*

| Integrante                       | Actividad realizada                                                                                                                                                                                                   | Evidencia                                                                                                                    |
| -------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- |
| Cayanchi Avila, Milenko Rubén    | Especificación de User Stories y Product Backlog; diagramas de arquitectura y base de datos.                                                                                                                          | Commits `ed4bec2`, `398d3e2`, `dabdd80` y `ba5ba04`.                                                                         |
| León Naupari, Jorge Mateo        | Modelado del Ubiquitous Language, User Task Matrix, diagramas C4 de contexto y contenedores, Design-Level Event Storming (4.6.1) y, en el Landing Page, meta tags de SEO, skip link de accesibilidad e i18n asociado. | 16 commits en report y 6 en landing-page; PRs #13, #15, #20 y #24 (report) y PR #2 (landing-page). Figuras 5.9, 5.10 y 5.11. |
| Mendoza Blanco, Ariel Roberto    | Registro de entrevistas y User Journey Maps del Chapter II.                                                                                                                                                           | Commits `cf441d0` y `fa74dfa`.                                                                                               |
| Rodriguez Rojas, Miler Alexander | Impact Mapping, perfil de colaboración, Student Outcome e integración de Chapters IV y V.                                                                                                                             | Commits `9610c3d`, `8519f14`, `7a1cc16` y `98b172a`.                                                                         |
| Herrera Enriquez, Diego Fernando | Style Guidelines y wireframes/mock-ups de Landing Page y Web Applications.                                                                                                                                            | Commits `708d7cc`, `737470f` y `027a2a1`.                                                                                    |

**Evidencia individual - León Naupari, Jorge Mateo (mateool10)**

Los siguientes registros corresponden a la participación verificable del integrante en los repositorios del equipo durante el Sprint 1.

![Commits de mateool10 en el repositorio report](../assets/images/chapter-5/5218-commits-mateo-report.jpg)

*Figura 5.9. Historial de commits de mateool10 en el repositorio report.*

![Commits de mateool10 en el repositorio landing-page](../assets/images/chapter-5/5218-commits-mateo-landing.jpg)

*Figura 5.10. Historial de commits de mateool10 en el repositorio landing-page (rama main).*

![Pull requests creados por mateool10](../assets/images/chapter-5/5218-pull-requests-mateo.jpg)

*Figura 5.11. Pull requests creados y fusionados por mateool10 en el repositorio report.*

### 5.2.2. Sprint 2

El Sprint 2 entrega la primera versión de las **Web Applications frontend** de VitalTrek para TB1. El alcance combina la configuración de rutas y expediciones dentro del bounded context `expedition-setup` con la consulta del progreso simulado en `field-tracking`. Se completaron US07, US08, US09, US11, US13, US12 y US20, con un total de **28 Story Points**, conforme al Product Backlog de la sección 3.3.

La aplicación está construida con Vue 3 y Vite; utiliza Pinia, Vue Router, Axios, PrimeVue y vue-i18n para el estado, navegación, componentes, consumo HTTP e internacionalización. json-server@0.17.4 proporciona los datos de prueba. Las capas `domain`, `application`, `infrastructure` y `presentation` separan las entidades, casos de uso/estado, acceso y mapeo de datos, e interfaz. El alcance no incluye autenticación real, backend productivo, persistencia real, Bluetooth, GPS, wearables, telemetría ni alertas reales.

| Campo | Valor |
| --- | --- |
| Sprint Goal | Completar el flujo frontend de preparación de expediciones y consulta de progreso estimado para Operations Administrators y Field Guides. |
| Historias incluidas | US07, US08, US09, US11, US13, US12 y US20 |
| Total de historias | 7 User Stories |
| Sprint Velocity / Total de Story Points | 28 Story Points |
| Contextos de dominio | `expedition-setup` y `field-tracking` |
| Resultado | Web Application frontend implementada; Fake API y telemetría de prueba. |

#### 5.2.2.1. Sprint Planning 2

La planificación del Sprint 2 definió como objetivo completar el flujo de preparación de una expedición —desde la configuración de la Route hasta el registro del Tourist Manifest— y agregar la consulta del progreso estimado del grupo. Las historias se seleccionaron del Product Backlog y se ordenaron según sus dependencias: primero la configuración de rutas, checkpoints y ventanas; luego la creación del grupo, la asignación del guía y el manifiesto; finalmente, el dashboard de seguimiento.

| **Sprint #** | **Sprint 2** |
| --- | --- |
| **Sprint Planning Background** | |
| Date | 2026-10-04 |
| Time | 08:00 PM |
| Location | Reunión virtual en Discord |
| Prepared By | Cayanchi Avila, Milenko Rubén |
| Attendees (to planning meeting) | Cayanchi Avila, Milenko Rubén / Herrera Enriquez, Diego Fernando / León Naupari, Jorge Mateo / Mendoza Blanco, Ariel Roberto / Rodriguez Rojas, Miler Alexander |
| Sprint 1 Review Summary | • Se presentó la primera versión del Landing Page de VitalTrek, desplegada en Vercel y entregada en AV1.<br>• Se completaron las 11 historias comprometidas (US01–US06, US33 y TS01–TS04), equivalentes a 30 Story Points: navegación, propuesta de valor, planes, equipo, solicitud de información, cambio de idioma ES/EN y publicación de términos de servicio y política de privacidad.<br>• El Landing Page se adapta a dispositivos desktop y mobile e incorpora internacionalización y atributos de accesibilidad.<br>• A partir de la revisión de AV1, el equipo corrigió la consistencia, los enlaces, la estructura y las evidencias del informe, y ajustó los roles, el flujo del frontend y la priorización del backlog, dejando los pagos fuera del MVP (versiones 1.6 y 1.7 del Registro de Versiones). |
| Sprint 1 Retrospective Summary | • **Aciertos:** el Sprint se desarrolló según lo planificado; todos los integrantes cumplieron sus tareas dentro del plazo y el incremento se entregó completo.<br>• **Aciertos:** la comunicación por Discord y la división del trabajo por secciones del Landing Page permitieron avanzar en paralelo sin bloqueos.<br>• **Oportunidad de mejora:** la integración del trabajo se concentró al final del Sprint, lo que dificultó revisar los cambios con anticipación.<br>• **Acciones para el Sprint 2:** descomponer cada User Story en tasks de 4 a 8 horas registradas en Jira, desarrollar cada funcionalidad en su propia feature branch e integrarla en `develop` mediante Pull Requests revisados. |
| **Sprint Goal & User Stories** | |
| Sprint 2 Goal | **Our focus is on** enabling the preparation of a complete expedition (route, checkpoints, expected time windows, expedition group, field guide assignment and tourist manifest) and the consultation of the estimated progress of a group.<br>**We believe it delivers** faster and more organized tour preparation **to** Operations Administrators, and a reliable way to register participants and follow the group progress **to** Field Guides.<br>**This will be confirmed when** an Operations Administrator can configure a route with its checkpoints and expected time windows, create an expedition group and assign a field guide, a Field Guide can register the tourist manifest, and both can view the estimated progress of the group in the deployed Web Application, in Spanish and English. |
| Sprint 2 Velocity | 28 Story Points |
| Sum of Story Points | 28 Story Points (US07, US08, US09, US11, US13, US12 y US20) |


#### 5.2.2.2. Aspect Leaders and Collaborators

Milenko Rubén Cayanchi Avila coordinó el trabajo general del Sprint. La matriz resume el liderazgo por aspecto a partir de los cambios de código y Pull Requests consultados en GitHub al 2026-10-05.

| Integrante | Usuario de GitHub | Coordinación | Rutas, checkpoints y ventanas | Grupos, guías, manifiesto y progreso | Espacios de trabajo, navegación e idioma |
| --- | --- | --- | --- | --- | --- |
| Cayanchi Avila, Milenko Rubén | `MaxghZZ` | L | L | C | L |
| León Naupari, Jorge Mateo | `mateool10` | C | C | C | C |
| Mendoza Blanco, Ariel Roberto | `Trepequiper` | C | C | C | L |
| Rodriguez Rojas, Miler Alexander | `Miler2003` | C | C | L | C |
| Herrera Enriquez, Diego Fernando | `DerDFHE` | C | C | C | C |

**Leyenda:** L = líder del aspecto; C = colaborador.

La autoría de los commits y el estado de integración de cada cambio se detallan en la sección 5.2.2.4.

#### 5.2.2.3. Sprint Backlog 2

El Sprint Backlog 2 comprende las siete User Stories seleccionadas para TB1. La tabla conserva las estimaciones del Product Backlog de la sección 3.3 y presenta la descomposición de cada historia en tareas, horas estimadas y responsables.

| Sprint # | Story Id | Story Title | Task Id | Task Title | Task Description | Estimation (Hours) | Assigned To | Status |
| --- | --- | --- | --- | --- | --- | ---: | --- | --- |
| Sprint 2 | US07 | Configuración de rutas | T-22 | Definición del modelo de Route y estado inicial | Implementar la entidad Route con los atributos geográficos y operativos de la historia, e inicializar cada ruta nueva en estado `draft`. | 5 | Cayanchi Avila, Milenko Rubén | Done |
| Sprint 2 | US07 | Configuración de rutas | T-23 | Formulario y listado de rutas | Construir las vistas para consultar las rutas existentes y registrar nombre, origen, destino, distancia, desnivel, dificultad y duración. | 6 | Herrera Enriquez, Diego Fernando | Done |
| Sprint 2 | US07 | Configuración de rutas | T-24 | Persistencia y validación de rutas | Integrar assembler, Fake API y store para crear rutas; validar campos obligatorios y nombres duplicados, y presentar los mensajes de error localizados. | 5 | Cayanchi Avila, Milenko Rubén | Done |
| Sprint 2 | US08 | Definición de checkpoints | T-25 | Modelo y asociación de Checkpoint | Implementar la entidad Checkpoint y asociarla a una Route mediante su identificador, ubicación y posición en la secuencia. | 5 | Cayanchi Avila, Milenko Rubén | Done |
| Sprint 2 | US08 | Definición de checkpoints | T-26 | Vista de configuración de checkpoints | Construir la vista para consultar los checkpoints de una ruta seleccionada y registrar nuevos puntos con su ubicación y orden. | 6 | Herrera Enriquez, Diego Fernando | Done |
| Sprint 2 | US08 | Definición de checkpoints | T-27 | Validación de secuencia y habilitación de ruta | Integrar la persistencia y las reglas del store para rechazar órdenes repetidos e impedir que una ruta sin checkpoints pase de `draft` a `enabled`. | 5 | Cayanchi Avila, Milenko Rubén | Done |
| Sprint 2 | US09 | Ventanas de tiempo esperadas | T-28 | Modelo y mapeo de Expected Time Window | Implementar la entidad y el assembler de ExpectedTimeWindow con ruta, checkpoints de inicio y fin, y límites mínimo y máximo en minutos. | 5 | Mendoza Blanco, Ariel Roberto | Done |
| Sprint 2 | US09 | Ventanas de tiempo esperadas | T-29 | Identificación y configuración de tramos | Construir la vista para ordenar los checkpoints, generar los tramos consecutivos y permitir configurar la ventana esperada de cada uno. | 6 | Rodriguez Rojas, Miler Alexander | Done |
| Sprint 2 | US09 | Ventanas de tiempo esperadas | T-30 | Reglas de validación de ventanas | Integrar Fake API y store para rechazar máximos menores o iguales a los mínimos, evitar ventanas duplicadas e identificar tramos pendientes de configuración. | 5 | Cayanchi Avila, Milenko Rubén | Done |
| Sprint 2 | US11 | Creación del grupo de expedición | T-31 | Modelo y recursos de Expedition Group | Implementar la entidad del grupo y agregar a la Fake API los datos necesarios para relacionarlo con una ruta habilitada, fecha de salida y capacidad máxima. | 6 | Rodriguez Rojas, Miler Alexander | Done |
| Sprint 2 | US11 | Creación del grupo de expedición | T-32 | Vista de creación y consulta de grupos | Construir el flujo para consultar grupos asociados a una ruta y registrar un nuevo grupo desde la gestión de rutas. | 6 | Herrera Enriquez, Diego Fernando | Done |
| Sprint 2 | US11 | Creación del grupo de expedición | T-33 | Validaciones y localización de grupos | Integrar la creación en el store y validar la ruta habilitada, la fecha no pasada y los datos obligatorios; agregar mensajes en español e inglés. | 5 | Mendoza Blanco, Ariel Roberto | Done |
| Sprint 2 | US13 | Asignación del guía | T-34 | Recurso y consulta de Field Guides | Incorporar guías de prueba a la Fake API y mapearlos a entidades de dominio consultables desde el contexto de configuración de expediciones. | 5 | León Naupari, Jorge Mateo | Done |
| Sprint 2 | US13 | Asignación del guía | T-35 | Asignación y control de cruce de fechas | Implementar la asignación de un guía al grupo, informar si ya tiene otro tour en la misma fecha y solicitar confirmación explícita ante el cruce. | 6 | Rodriguez Rojas, Miler Alexander | Done |
| Sprint 2 | US12 | Registro del manifiesto | T-36 | Modelo y endpoint de Manifest Entries | Implementar el modelo de entrada del manifiesto y conectar su consulta y registro con el recurso de prueba asociado al Expedition Group. | 5 | Mendoza Blanco, Ariel Roberto | Done |
| Sprint 2 | US12 | Registro del manifiesto | T-37 | Vista de registro del Tourist Manifest | Construir la vista del Field Guide para consultar los participantes del grupo y registrar turistas con los datos requeridos. | 6 | Herrera Enriquez, Diego Fernando | Done |
| Sprint 2 | US12 | Registro del manifiesto | T-38 | Validación de identidad y capacidad del grupo | Rechazar documentos de identidad duplicados y nuevos participantes que excedan la capacidad máxima; mostrar errores localizados. | 5 | León Naupari, Jorge Mateo | Done |
| Sprint 2 | US20 | Seguimiento del progreso | T-39 | Modelo y fuente de datos de seguimiento | Crear la estructura del bounded context `field-tracking` y mapear datos simulados de grupo, checkpoint, tramo, progreso, estado y sincronización. | 6 | León Naupari, Jorge Mateo | Done |
| Sprint 2 | US20 | Seguimiento del progreso | T-40 | Dashboard de progreso del grupo | Construir la vista para presentar el tramo actual, último checkpoint confirmado y porcentaje de progreso estimado del grupo. | 6 | Rodriguez Rojas, Miler Alexander | Done |
| Sprint 2 | US20 | Seguimiento del progreso | T-41 | Estados de seguimiento y mensajes bilingües | Presentar la antigüedad de la última sincronización y aclarar que el progreso es estimado; informar cuando el tour todavía no está activo. | 5 | Mendoza Blanco, Ariel Roberto | Done |

**Resumen del Sprint Backlog 2**

| Concepto | Valor |
| --- | ---: |
| User Stories asignadas | 7 |
| Work-items resultantes de la descomposición | 20 |
| Estimación mínima de una task | 5 horas |
| Estimación máxima de una task | 6 horas |
| Total de horas estimadas | 109 |
| Sum of Story Points | 28 |

**Distribución de la carga por integrante**

| Integrante | Tasks | Horas |
| --- | ---: | ---: |
| Cayanchi Avila, Milenko Rubén | 5 | 25 |
| León Naupari, Jorge Mateo | 3 | 16 |
| Mendoza Blanco, Ariel Roberto | 4 | 20 |
| Rodriguez Rojas, Miler Alexander | 4 | 24 |
| Herrera Enriquez, Diego Fernando | 4 | 24 |
| **Total** | **20** | **109** |

El Sprint se planificó con el orden de dependencias **US07 → US08 → US09 → US11 → US13 → US12 → US20**.

#### 5.2.2.4. Development Evidence for Sprint Review

La evidencia de desarrollo del Sprint 2 se encuentra en el repositorio [web-applications](https://github.com/1ASI0729-2620-16712-G4-Nexatech/web-applications). Los cambios de US07, US08 y US09 se integraron en `develop` mediante los PR #4, #5 y #6, y los de US11, US13, US12 y US20 mediante el PR #7.

| User Story | Rama | Commit de referencia | Evidencia de integración |
| --- | --- | --- | --- |
| US07 — Configuración de rutas | `feature/webapp-route-configuration` | [`77e6fda`](https://github.com/1ASI0729-2620-16712-G4-Nexatech/web-applications/commit/77e6fda005b45ac9347db60c9d6781675cb9313a) | [PR #4](https://github.com/1ASI0729-2620-16712-G4-Nexatech/web-applications/pull/4), integrado en `develop`. |
| US08 — Definición de checkpoints | `feature/webapp-checkpoints` | [`29b84cc`](https://github.com/1ASI0729-2620-16712-G4-Nexatech/web-applications/commit/29b84cca5935d0fcf8f9f20fc999c770368a6541) | [PR #5](https://github.com/1ASI0729-2620-16712-G4-Nexatech/web-applications/pull/5), integrado en `develop`. |
| US09 — Ventanas de tiempo esperadas | `feature/webapp-expected-time-windows` | [`f0af953`](https://github.com/1ASI0729-2620-16712-G4-Nexatech/web-applications/commit/f0af953046fc8ceefbca4bd305598fedea35648c) | [PR #6](https://github.com/1ASI0729-2620-16712-G4-Nexatech/web-applications/pull/6), integrado en `develop`. |
| US11 — Creación del grupo de expedición | `feature/webapp-expedition-group-creation` | [`e1cb43a`](https://github.com/1ASI0729-2620-16712-G4-Nexatech/web-applications/commit/e1cb43a792ddb626779e2d27d33acc15ed81cdea) | [PR #7](https://github.com/1ASI0729-2620-16712-G4-Nexatech/web-applications/pull/7), integrado en `develop`. |
| US13 — Asignación del guía | `feature/webapp-field-guide-assignment` | [`21aedcd`](https://github.com/1ASI0729-2620-16712-G4-Nexatech/web-applications/commit/21aedcd63b2b18f91487b86a2fce768c38644c8a) | [PR #7](https://github.com/1ASI0729-2620-16712-G4-Nexatech/web-applications/pull/7), integrado en `develop`. |
| US12 — Registro del manifiesto | `feature/webapp-tourist-manifest` | [`71bbcaca`](https://github.com/1ASI0729-2620-16712-G4-Nexatech/web-applications/commit/71bbcaca4648445471ce6b81c3f0431925fac282) | [PR #7](https://github.com/1ASI0729-2620-16712-G4-Nexatech/web-applications/pull/7), integrado en `develop`. |
| US20 — Seguimiento del progreso | `feature/webapp-group-progress-dashboard` | [`cef703d`](https://github.com/1ASI0729-2620-16712-G4-Nexatech/web-applications/commit/cef703d1c403cd0ff50717a9f5bebd45b2bfdad1) | [PR #7](https://github.com/1ASI0729-2620-16712-G4-Nexatech/web-applications/pull/7), integrado en `develop`. |

El PR #7 agrupó la creación de Expedition Groups, la asignación de Field Guides, el Tourist Manifest y el Group Progress Dashboard. Fue integrado en `develop` el 2026-10-05 y contiene 37 commits con cambios en 22 archivos. Sus commits de funcionalidad fueron realizados principalmente por `Miler2003`; el PR fue creado e integrado por `MaxghZZ`.

**Cambios colaborativos complementarios del frontend**

| Cambio | Autor / rama | Commit | Estado en GitHub |
| --- | --- | --- | --- |
| Espacios de trabajo por rol y vistas de Operations Administrator y Field Guide | `MaxghZZ` / `field-guide-views` | [`207f528`](https://github.com/1ASI0729-2620-16712-G4-Nexatech/web-applications/commit/207f52815862f5dc284f9400c26e97d9fed70025) | Integrado en `develop` mediante commit directo. |
| Corrección de visualización del selector de rol | `DerDFHE` / `develop` | [`2c66861`](https://github.com/1ASI0729-2620-16712-G4-Nexatech/web-applications/commit/2c66861a26154775d1e1336fd3e13b7ef9bedf82) | Integrado en `develop` el 2026-10-05. |
| Cambio del selector de idioma a botones ES/EN con etiquetas accesibles y documentación | `Trepequiper` / `feature/button-update` | [`bc74c80`](https://github.com/1ASI0729-2620-16712-G4-Nexatech/web-applications/commit/bc74c80b990714031109cd7c9c01a537a6f39083) | [PR #9](https://github.com/1ASI0729-2620-16712-G4-Nexatech/web-applications/pull/9), 5 commits integrados en `develop` el 2026-10-05. |
| Ajuste de marca en la barra lateral del espacio de trabajo | `mateool10` / `feature/webapp-sidebar-brand` | [`91ebc19`](https://github.com/1ASI0729-2620-16712-G4-Nexatech/web-applications/commit/91ebc19b067eeb642804865f893534a555ed8016) | [PR #8](https://github.com/1ASI0729-2620-16712-G4-Nexatech/web-applications/pull/8), integrado en `develop`. |
| Ajuste de layout para pasar el espacio de trabajo desde la metadata de ruta | `mateool10` / `feature/webapp-workspace-layout-fix` | [`c3a1ae6`](https://github.com/1ASI0729-2620-16712-G4-Nexatech/web-applications/commit/c3a1ae61e7e53875dd213ec8b020cfd5d4ea47b0) | Disponible en la rama `feature/webapp-workspace-layout-fix`. |

#### 5.2.2.5. Execution Evidence for Sprint Review

La validación funcional del Sprint 2 cubre los escenarios principales de las User Stories implementadas. La telemetría y los datos de seguimiento utilizados en US20 son simulados; la aplicación no sustituye sistemas de comunicación o respuesta de emergencia.

| User Story | Escenario de validación | Resultado esperado |
| --- | --- | --- |
| US07 | Registrar una Route válida y probar un nombre duplicado o campos obligatorios incompletos. | La ruta se crea en estado `draft`; los datos inválidos o duplicados se rechazan y se informa el problema. |
| US08 | Registrar checkpoints con órdenes únicos; intentar duplicar un orden y habilitar una ruta sin checkpoints. | Se asocian los checkpoints a la ruta; se rechaza el orden duplicado y no se habilita la ruta vacía. Con al menos un checkpoint, la ruta puede habilitarse. |
| US09 | Guardar una ventana válida, invertir los límites mínimo/máximo y consultar tramos sin configuración. | Se guarda la ventana válida, se rechazan límites inconsistentes y se identifican los tramos pendientes. |
| US11 | Crear un Expedition Group para una ruta habilitada y probar una fecha anterior a la actual. | El grupo se asocia a la ruta; una fecha pasada se rechaza. |
| US13 | Asignar un guía disponible, seleccionar uno con cruce de fecha y comprobar el requisito de responsable. | La asignación se registra; el cruce requiere confirmación y el sistema identifica un grupo sin guía. |
| US12 | Registrar participantes, repetir un documento de identidad y superar la capacidad del grupo. | El manifiesto se actualiza; el documento duplicado y el participante que excede la capacidad se rechazan. |
| US20 | Consultar un tour activo con datos de seguimiento, uno sin sincronización reciente y uno no iniciado. | Se muestran último checkpoint, tramo y progreso estimado; se indica la antigüedad de la información y que es una estimación; un tour no iniciado informa que el seguimiento se habilita al comenzar. |

**Capturas de ejecución**

Las siguientes capturas documentan las vistas de la aplicación observadas durante la ejecución. Exec1 muestra la vista de seguimiento de progreso durante la carga de rutas; Exec2, el listado de rutas en estado de carga con un mensaje de error de creación; Exec3 y Exec5, la selección de espacio de trabajo y rol en español y en inglés; y Exec4, el formulario de registro de una nueva Route.

![Exec1: vista de seguimiento de progreso mientras se cargan las rutas](../assets/images/chapter-5/Exec1.png)

*Figura 5.12. Vista de seguimiento de progreso durante la carga de rutas.*

![Exec2: listado de rutas durante la carga, con mensaje de error visible](../assets/images/chapter-5/Exec2.png)

*Figura 5.13. Listado de rutas en estado de carga y mensaje de error de creación.*

![Exec3: selección de espacio de trabajo y rol en español](../assets/images/chapter-5/Exec3.png)

*Figura 5.14. Selección de espacio de trabajo para Operations Administrator o Field Guide.*

![Exec4: formulario para registrar una nueva ruta](../assets/images/chapter-5/Exec4.png)

*Figura 5.15. Formulario de configuración de una nueva Route.*

![Exec5: selección de espacio de trabajo y rol en inglés](../assets/images/chapter-5/Exec5.png)

*Figura 5.16. Selector de espacio de trabajo en inglés.*


#### 5.2.2.6. Services Documentation Evidence for Sprint Review

El Sprint 2 no implementa el RESTful Web Services productivo. Para habilitar el frontend se utiliza una **Fake API** ejecutada con json-server@0.17.4 y recursos JSON de prueba. Los datos de US20 se simulan para presentar el estado de seguimiento. Por ello, no se genera una especificación OpenAPI/Swagger de servicios productivos en esta entrega.

| Recurso de prueba | Endpoint local | Métodos utilizados | Propósito |
| --- | --- | --- | --- |
| Routes | `/api/v1/routes` | GET, POST y actualización de estado | Consultar y registrar rutas; habilitar una ruta después de agregar checkpoints. |
| Checkpoints | `/api/v1/checkpoints` | GET, POST | Consultar y registrar puntos de control asociados a una ruta. |
| Expected Time Windows | `/api/v1/expected-time-windows` | GET, POST | Consultar y registrar ventanas esperadas entre checkpoints. |
| Expedition Groups | `/api/v1/expedition-groups` | GET, POST y actualización | Consultar y crear grupos vinculados a una ruta; actualizar su guía asignado. |
| Field Guides | `/api/v1/field-guides` | GET | Consultar guías de prueba disponibles para la asignación. |
| Manifest Entries | `/api/v1/manifest-entries` | GET, POST | Consultar y registrar participantes asociados a un Expedition Group. |
| Group Progress | `/api/v1/group-progress` | GET | Leer registros simulados de último checkpoint, tramo, progreso, estado y antigüedad de sincronización. |

La ruta `/api/v1/*` se resuelve mediante `server/routes.json`. La URL configurada en `.env.development` (`http://localhost:3000/api/v1`) corresponde al entorno de desarrollo local. Los manifiestos y el progreso se persisten en el archivo JSON atendido por json-server.

#### 5.2.2.7. Software Deployment Evidence for Sprint Review

La Web Application del Sprint 2 se encuentra desplegada para su revisión. El despliegue corresponde al frontend de TB1. La aplicación consume una Fake API con datos simulados.

| Elemento | Información |
| --- | --- |
| Producto | VitalTrek Web Applications — frontend TB1 |
| Plataforma de despliegue | Vercel |
| Repositorio | https://github.com/1ASI0729-2620-16712-G4-Nexatech/web-applications |
| Build command | `npm run build` |
| Output directory | `dist` |
| Variable de entorno de producción | `VITE_VITALTREK_API_URL`: URL de la Fake API consumida por el despliegue; la URL `localhost` corresponde al entorno de desarrollo local. |

#### 5.2.2.8. Team Collaboration Insights during Sprint

El equipo colaboró sobre el repositorio [web-applications](https://github.com/1ASI0729-2620-16712-G4-Nexatech/web-applications), utilizando `develop` como rama de integración, ramas de funcionalidad y Pull Requests. Los PR #4, #5 y #6 integraron US07, US08 y US09; el PR #7 integró US11, US13, US12 y US20. Después se incorporaron mejoras transversales de selección de espacio de trabajo y cambio de idioma mediante cambios de varios integrantes. El estado de cada contribución se reporta según la rama y el PR visibles en GitHub al 2026-10-05.

| Integrante | Contribución comprobable en TB1 | Evidencia de GitHub |
| --- | --- | --- |
| Cayanchi Avila, Milenko Rubén (`MaxghZZ`) | Liderazgo general; configuración de rutas, checkpoints y ventanas de tiempo; incorporación de los espacios de trabajo según rol y de las vistas para Operations Administrator y Field Guide. | PR #4, #5 y #6; commit [`207f528`](https://github.com/1ASI0729-2620-16712-G4-Nexatech/web-applications/commit/207f52815862f5dc284f9400c26e97d9fed70025). |
| León Naupari, Jorge Mateo (`mateool10`) | Ajustes de marca y layout para la selección de espacio de trabajo y la barra lateral. | Commit [`c3a1ae6`](https://github.com/1ASI0729-2620-16712-G4-Nexatech/web-applications/commit/c3a1ae61e7e53875dd213ec8b020cfd5d4ea47b0) en `feature/webapp-workspace-layout-fix`; [PR #8](https://github.com/1ASI0729-2620-16712-G4-Nexatech/web-applications/pull/8) con commit [`91ebc19`](https://github.com/1ASI0729-2620-16712-G4-Nexatech/web-applications/commit/91ebc19b067eeb642804865f893534a555ed8016), integrado en `develop`. |
| Mendoza Blanco, Ariel Roberto (`Trepequiper`) | Actualización del selector de idioma ES/EN a botones, incluyendo etiquetas accesibles y documentación del componente. | [PR #9](https://github.com/1ASI0729-2620-16712-G4-Nexatech/web-applications/pull/9), 5 commits; [`bc74c80`](https://github.com/1ASI0729-2620-16712-G4-Nexatech/web-applications/commit/bc74c80b990714031109cd7c9c01a537a6f39083). |
| Rodriguez Rojas, Miler Alexander (`Miler2003`) | Implementación de la creación de grupos, asignación de guías, registro del manifiesto y dashboard de progreso estimado mediante Fake API y datos simulados. | 37 commits integrados mediante [PR #7](https://github.com/1ASI0729-2620-16712-G4-Nexatech/web-applications/pull/7); commits representativos [`e1cb43a`](https://github.com/1ASI0729-2620-16712-G4-Nexatech/web-applications/commit/e1cb43a792ddb626779e2d27d33acc15ed81cdea), [`21aedcd`](https://github.com/1ASI0729-2620-16712-G4-Nexatech/web-applications/commit/21aedcd63b2b18f91487b86a2fce768c38644c8a), [`71bbcaca`](https://github.com/1ASI0729-2620-16712-G4-Nexatech/web-applications/commit/71bbcaca4648445471ce6b81c3f0431925fac282) y [`cef703d`](https://github.com/1ASI0729-2620-16712-G4-Nexatech/web-applications/commit/cef703d1c403cd0ff50717a9f5bebd45b2bfdad1). |
| Herrera Enriquez, Diego Fernando (`DerDFHE`) | Corrección de la vista de selección de rol para mejorar su visualización. | Commit [`2c66861`](https://github.com/1ASI0729-2620-16712-G4-Nexatech/web-applications/commit/2c66861a26154775d1e1336fd3e13b7ef9bedf82), integrado en `develop`. |

Al 2026-10-05, el historial mostraba `develop` actualizado hasta el commit `2c66861`. Posteriormente, el PR #8 fue integrado en `develop`.

![Commits de colaboración en web-applications durante TB1](../assets/images/chapter-5/ColabInsights21.png)

*Figura 5.17. Historial de commits del repositorio web-applications durante TB1.*

![GitHub Insights de web-applications durante TB1](../assets/images/chapter-5/ColabInsights22.png)

*Figura 5.18. GitHub Insights del repositorio web-applications para el período del 28 de septiembre al 5 de octubre de 2026.*

### 5.2.3. Sprint 3

El Sprint 3 tiene como objetivo implementar y desplegar la primera versión del RESTful Web Services de VitalTrek e integrarlo con las Web Applications. El alcance comprende las Technical Stories TS06, TS07 y TS09 y las User Stories US07 a US16, que habilitan la infraestructura de persistencia, la documentación OpenAPI, la seguridad con JWT y los endpoints de Expedition Setup. La estimación total del Sprint es de 57 Story Points.

| Campo | Valor |
| --- | --- |
| Sprint Velocity | 57 Story Points |
| Total de Story Points | 57 |

#### 5.2.3.1. Sprint Planning 3

La reunión de planificación permitió definir el objetivo, alcance, responsabilidades y tareas del tercer Sprint. El trabajo se enfocó en entregar el backend productivo del bounded context Expedition Setup con persistencia en MySQL, integrado con las Web Applications ya desplegadas en Vercel.

| **Sprint #** | **Sprint 3** |
| --- | --- |
| **Sprint Planning Background** |  |
| Date | <!-- COMPLETAR --> |
| Time | <!-- COMPLETAR --> |
| Location | Reunión virtual en Discord |
| Prepared By | <!-- COMPLETAR: Apellidos, Nombres --> |
| Attendees (to planning meeting) | Cayanchi Avila, Milenko Rubén / Herrera Enriquez, Diego Fernando / León Naupari, Jorge Mateo / Mendoza Blanco, Ariel Roberto / Rodriguez Rojas, Miler Alexander |
| Sprint 2 Review Summary | • Se presentó la primera versión de las Web Applications frontend de VitalTrek, desarrolladas con Vue 3, PrimeVue, Pinia, Vue Router y vue-i18n, desplegadas en Vercel e integradas con una Fake API.<br>• Se completaron las 7 User Stories comprometidas (US07, US08, US09, US11, US13, US12 y US20), equivalentes a 28 Story Points, correspondientes a los bounded contexts `expedition-setup` y `field-tracking`.<br>• La retroalimentación de TB1 señaló como oportunidades de mejora la aplicación parcial de Responsive Web Design en el Landing Page y la ausencia de algunas de sus secciones, la necesidad de evidenciar la participación de todos los integrantes en la implementación, la evidencia de mejora continua entre entregas y la calidad de la comunicación escrita del informe.<br>• En respuesta, el equipo corrigió el informe (versión 1.9 del Registro de Versiones) e incorporó al Sprint 3 las mejoras pendientes del Landing Page. |
| Sprint 2 Retrospective Summary | <!-- COMPLETAR --> |
| **Sprint Goal & User Stories** |  |
| Sprint 3 Goal | **Our focus is on** implementing and deploying the first version of VitalTrek's RESTful Web Services, covering authentication with JWT, the Expedition Setup bounded context and MySQL persistence via Entity Framework Core, integrated with the already-deployed Web Applications.<br>**We believe it delivers** a functional, documented and publicly accessible backend that enables agencies to configure routes, checkpoints, time windows, expedition groups and manifests through a real API **to** Operations Administrators, Field Guides and Adventure Tourists using the platform.<br>**This will be confirmed when** the Web Services are deployed on a public URL in Render, the OpenAPI documentation is accessible at `/scalar`, and the Web Applications consume the real API for authentication and expedition setup flows without errors. |
| Sprint 3 Velocity | 57 Story Points |
| Sum of Story Points | 57 Story Points (TS06, TS07, TS09, US07, US08, US09, US10, US11, US12, US13, US14, US15, US16) |


#### 5.2.3.2. Aspect Leaders and Collaborators

La siguiente matriz organiza el liderazgo y la colaboración del equipo durante el Sprint 3, en correspondencia con las tareas registradas en el Sprint Backlog.

| Integrante | Usuario de GitHub | IAM y seguridad | Expedition Setup API | Persistencia y OpenAPI | Integración de Web Applications | Landing Page y despliegue |
| --- | --- | --- | --- | --- | --- | --- |
| Cayanchi Avila, Milenko Rubén | `MaxghZZ` | L | C | C | C | C |
| León Naupari, Jorge Mateo | `mateool10` | C | L | C | C | C |
| Rodriguez Rojas, Miler Alexander | `Miler2003` | C | C | L | C | C |
| Mendoza Blanco, Ariel Roberto | `Trepequiper` | C | C | C | L | C |
| Herrera Enriquez, Diego Fernando | `DerDFHE` | C | C | C | C | L |

**Leyenda:** L = Leader; C = Collaborator.

#### 5.2.3.3. Sprint Backlog 3

El Sprint Backlog 3 se enfoca en la primera versión del RESTful Web Services de VitalTrek y en su integración con las Web Applications. Las User Stories y Technical Stories seleccionadas se descompusieron en tasks estimadas entre 4 y 8 horas, cuyo avance se registró en Jira Software con los estados To-do, In-Process, To-Review y Done.

![Board del Sprint 3 en Jira](../assets/images/chapter-5/sprint3-board-jira.png)

*Figura 5.X. Board del Sprint 3 en Jira Software con las 13 historias (57 Story Points) en estado Finalizado.*

**Enlace público del board:** [Jira — VitalTrek](https://milenkorvu.atlassian.net/jira/software/projects/SCRUM/boards/1/backlog)

| **Sprint #** | **Sprint 3** | | | | | | |
| --- | --- | --- | --- | --- | --- | --- | --- |
| **User Story Id** | **User Story Title** | **Work-Item / Task Id** | **Title** | **Description** | **Estimation (Hours)** | **Assigned To** | **Status (To-do / In-Process / To-Review / Done)** |
| TS07 | Persistencia y migraciones | T-42 | Infraestructura compartida y contexto de datos | Configurar el Shared kernel, el DbContext con MySQL, la convención snake_case y el acortamiento de nombres largos de claves e índices. | 6 | Cayanchi Avila, Milenko Rubén | Done |
| TS06 | Contratos del RESTful API | T-43 | OpenAPI, Scalar y localización | Configurar la generación de OpenAPI, la documentación con Scalar, las rutas kebab-case y los mensajes localizados en inglés y español. | 5 | Rodriguez Rojas, Miler Alexander | Done |
| TS07 | Persistencia y migraciones | T-44 | Migraciones y datos de demostración | Generar las migraciones de cada bounded context y cargar los datos de demostración de agencias, usuarios, rutas y grupos. | 5 | León Naupari, Jorge Mateo | Done |
| TS09 | Seguridad, autenticación y privacidad | T-45 | Registro de agencias e inicio de sesión con JWT | Implementar sign-up y sign-in con contraseñas cifradas mediante BCrypt y emisión de tokens JWT firmados con HS256. | 8 | Cayanchi Avila, Milenko Rubén | Done |
| TS09 | Seguridad, autenticación y privacidad | T-46 | Autorización por roles y gestión de usuarios | Implementar el middleware de autorización por rol y agencia, y los endpoints de consulta y creación de usuarios. | 6 | Mendoza Blanco, Ariel Roberto | Done |
| TS09 | Seguridad, autenticación y privacidad | T-47 | Sesión JWT en las Web Applications | Consumir el inicio de sesión del API, guardar el token con su expiración y enviarlo mediante un interceptor HTTP. | 6 | Herrera Enriquez, Diego Fernando | Done |
| US07 | Configuración de rutas | T-48 | Agregado Route y endpoints de rutas | Implementar el agregado Route y los endpoints de consulta, registro en `draft` y cambio de estado de rutas. | 6 | León Naupari, Jorge Mateo | Done |
| US08 | Definición de checkpoints | T-49 | Endpoints de checkpoints | Implementar el registro y la consulta de checkpoints con validación de orden, coordenadas e identificador Bluetooth únicos. | 5 | Mendoza Blanco, Ariel Roberto | Done |
| US09 | Ventanas de tiempo esperadas | T-50 | Endpoints de ventanas de tiempo | Implementar el registro y la consulta de ventanas esperadas por tramo con límites mínimo y máximo válidos. | 5 | Rodriguez Rojas, Miler Alexander | Done |
| US10 | Protocolo de seguridad | T-51 | Protocolos de seguridad y notas de ruta | Implementar los endpoints de protocolos de seguridad y notas de ruta, e integrarlos en la preparación del grupo. | 5 | Herrera Enriquez, Diego Fernando | Done |
| US11 | Creación del grupo de expedición | T-52 | Endpoints de grupos de expedición | Implementar la creación de grupos para rutas habilitadas con fecha de salida no pasada y capacidad máxima. | 5 | Rodriguez Rojas, Miler Alexander | Done |
| US13 | Asignación del guía | T-53 | Guías de campo y asignación con control de fechas | Implementar el registro de guías y la asignación al grupo con confirmación explícita ante cruces de fecha. | 5 | León Naupari, Jorge Mateo | Done |
| US12 | Registro del manifiesto | T-54 | Endpoints del manifiesto de turistas | Implementar el registro de participantes con validación de documento único, cruce de fechas y capacidad del grupo. | 5 | Mendoza Blanco, Ariel Roberto | Done |
| US15 | Asignación del wearable | T-55 | Inventario y asignación de wearables | Implementar el inventario de wearables y su asignación a la preparación de cada participante. | 6 | Cayanchi Avila, Milenko Rubén | Done |
| US14 | Registro de contacto de emergencia | T-56 | Endpoint de contacto de emergencia | Implementar el registro del contacto de emergencia por el propio Adventure Tourist. | 4 | Herrera Enriquez, Diego Fernando | Done |
| US16 | Activación del wearable | T-57 | Consentimiento y activación del wearable | Implementar el otorgamiento y la revocación del consentimiento de monitoreo, que activa o desactiva el wearable asignado. | 4 | Rodriguez Rojas, Miler Alexander | Done |
| US07 | Configuración de rutas | T-58 | Integración de Expedition Setup en las Web Applications | Adaptar los stores de rutas, checkpoints, ventanas, grupos, guías y manifiesto a los endpoints del API. | 6 | León Naupari, Jorge Mateo | Done |
| US15 | Asignación del wearable | T-59 | Integración de la preparación del participante | Adaptar la asignación de wearables, el contacto de emergencia y el consentimiento a los endpoints del API. | 5 | Mendoza Blanco, Ariel Roberto | Done |
| TS06 | Contratos del RESTful API | T-60 | Despliegue del API en Render y Railway | Configurar la base de datos MySQL en Railway, el Web Service con Docker en Render y sus variables de entorno. | 6 | Cayanchi Avila, Milenko Rubén | Done |
| TS06 | Contratos del RESTful API | T-61 | Despliegue de las Web Applications y del Landing Page | Publicar las versiones `v1.1.0` en Vercel y configurar la URL del API desplegado. | 4 | Herrera Enriquez, Diego Fernando | Done |
| — | Mejoras del Landing Page (feedback TB1) | T-62 | Responsive y contenido del hero | Corregir la grilla de características en móvil y el texto duplicado del hero. | 4 | Herrera Enriquez, Diego Fernando | Done |
| — | Mejoras del Landing Page (feedback TB1) | T-63 | Enlaces a la app y redes sociales | Centralizar la URL de las Web Applications en los CTA y agregar redes sociales y ubicación. | 4 | Rodriguez Rojas, Miler Alexander | Done |


**Resumen del Sprint Backlog 3**

| Concepto | Valor |
| --- | ---: |
| User Stories y Technical Stories asignadas | 13 |
| Work-items resultantes de la descomposición | 22 |
| Estimación mínima de una task | 4 horas |
| Estimación máxima de una task | 8 horas |
| Total de horas estimadas | 115 |
| Sum of Story Points | 57 |

**Distribución de la carga por integrante**

| Integrante | Tasks | Horas |
| --- | ---: | ---: |
| Cayanchi Avila, Milenko Rubén | 4 | 26 |
| León Naupari, Jorge Mateo | 4 | 22 |
| Mendoza Blanco, Ariel Roberto | 4 | 21 |
| Rodriguez Rojas, Miler Alexander | 5 | 23 |
| Herrera Enriquez, Diego Fernando | 5 | 23 |
| **Total** | **22** | **115** |

Las dos tasks de mejora del Landing Page responden a la retroalimentación de TB1 y no suman Story Points.

#### 5.2.3.4. Development Evidence for Sprint Review

En el Sprint 3 se implementó la primera versión del RESTful Web Services de VitalTrek en el repositorio [vitaltrek-backend](https://github.com/1ASI0729-2620-16712-G4-Nexatech/vitaltrek-backend), desarrollado con ASP.NET Core 10 y C# en JetBrains Rider. El proyecto se organiza en los módulos Shared, IAM y Expedition Setup, aplica las capas de dominio, aplicación, infraestructura e interfaces, implementa la persistencia en MySQL mediante Entity Framework Core con migraciones versionadas y documenta sus endpoints con OpenAPI. La versión `v1.0.0` se preparó en la rama `release/v1.0.0`, se integró en `main` y `develop` mediante Pull Requests y se etiquetó en `main`. Asimismo, se registran los cambios realizados en el Landing Page y en las Web Applications durante el Sprint. Todas las contribuciones siguieron GitFlow y Conventional Commits.

| Repository | Branch | Commit Id | Commit Message | Commit Message Body | Committed on (Date) |
| --- | --- | --- | --- | --- | --- |
| 1ASI0729-2620-16712-G4-Nexatech/vitaltrek-backend | `main` | `ee3c556` | chore: initial scaffold | — | 2026-10-28 |
| 1ASI0729-2620-16712-G4-Nexatech/vitaltrek-backend | `main` | `9345935` | fix: remove corrupted VitalRek.Apí folder | — | 2026-10-28 |
| 1ASI0729-2620-16712-G4-Nexatech/vitaltrek-backend | `feature/shared-infrastructure` | `def4ee0` | chore: rename solution to VitalTrek and add shared infrastructure | Add Shared kernel (Result, repositories, unit of work, DbContext, kebab-case routes), i18n resources, MySQL configuration, CORS, Scalar and Dockerfile. | 2026-10-28 |
| 1ASI0729-2620-16712-G4-Nexatech/vitaltrek-backend | `feature/iam-bounded-context` | `3a5c3f6` | feat(iam): add IAM bounded context with JWT authentication | Add agencies and users, sign-up and sign-in, role-based authorization middleware, users endpoints, localized OpenAPI metadata, demo data seeding and initial migration. | 2026-10-29 |
| 1ASI0729-2620-16712-G4-Nexatech/vitaltrek-backend | `feature/iam-bounded-context` | `cd32c5f` | feat(iam): add initial database migration | — | 2026-10-29 |
| 1ASI0729-2620-16712-G4-Nexatech/vitaltrek-backend | `feature/expedition-setup-routes` | `4514175` | feat(expedition-setup): add routes, checkpoints, expected time windows, route notes and safety protocols | — | 2026-10-29 |
| 1ASI0729-2620-16712-G4-Nexatech/vitaltrek-backend | `feature/expedition-setup-routes` | `d62e131` | fix(expedition-setup): shorten segment index name and add database migration | — | 2026-10-29 |
| 1ASI0729-2620-16712-G4-Nexatech/vitaltrek-backend | `feature/expedition-setup-groups` | `ebe5c10` | feat(expedition-setup): add expedition groups, field guides, tourist manifest, wearables and participant preparation | — | 2026-10-29 |
| 1ASI0729-2620-16712-G4-Nexatech/vitaltrek-backend | `release/v1.0.0` | `3df83d0` | chore(deploy): configure production database connection and container port | — | 2026-10-29 |
| 1ASI0729-2620-16712-G4-Nexatech/vitaltrek-backend | `main` | `8886380` | Release/v1.0.0 | Pull Request de `release/v1.0.0` hacia `main`; etiqueta `v1.0.0`. | 2026-10-31 |
| 1ASI0729-2620-16712-G4-Nexatech/web-applications | `feature/backend-integration` | `9e824d8` | feat(webapp): consume VitalTrek RESTful API for IAM and expedition setup | — | 2026-10-31 |
| 1ASI0729-2620-16712-G4-Nexatech/web-applications | `develop` | `9585e7b` | feat(webapp): consume VitalTrek RESTful API for IAM and expedition setup | Pull Request de `feature/backend-integration` hacia `develop`. | 2026-10-31 |
| 1ASI0729-2620-16712-G4-Nexatech/web-applications | `main` | `4166921` | Release/v1.1.0 | Pull Request de `release/v1.1.0` hacia `main`; etiqueta `v1.1.0`. | 2026-10-31 |
| 1ASI0729-2620-16712-G4-Nexatech/landing-page | `main` | `5b1d52c` | feat: redirige botones Get Started y Go to VitalTrek a la app | — | 2026-10-06 |
| 1ASI0729-2620-16712-G4-Nexatech/landing-page | `develop` | `69cf64e` | fix(responsive): use single-column features grid on mobile to remove horizontal scroll | — | 2026-10-28 |
| 1ASI0729-2620-16712-G4-Nexatech/landing-page | `develop` | `1ce678c` | feat(links): centralize Web App URL with data-app-path and point segment CTAs to the app | — | 2026-10-28 |
| 1ASI0729-2620-16712-G4-Nexatech/landing-page | `develop` | `4e88070` | feat(social): add social media links and location to contact and footer | — | 2026-10-28 |
| 1ASI0729-2620-16712-G4-Nexatech/landing-page | `develop` | `c96a3c3` | fix: remove duplicated hero text, dev comments and fix login placeholder i18n | — | 2026-10-28 |
| 1ASI0729-2620-16712-G4-Nexatech/landing-page | `main` | `4649e05` | Release/v1.1.0 | Pull Request de `release/v1.1.0` hacia `main`; etiqueta `v1.1.0`. | 2026-10-31 |

#### 5.2.3.5. Execution Evidence for Sprint Review

Al cierre del Sprint 3, las Web Applications de VitalTrek consumen el RESTful Web Services desplegado en Render para la autenticación y la gestión de cuentas (IAM) y para la configuración de expediciones (Expedition Setup). El inicio de sesión obtiene un token JWT que se envía en cada solicitud, y el API restringe cada operación según el rol y la agencia del usuario. Las funcionalidades de Field Tracking, Checkpoint Sync, Safety Monitoring, Incident Response y Tour Closure se muestran como disponibles en un próximo sprint, a la espera de su implementación en el backend. A continuación se presentan capturas del recorrido realizado con las cuentas de demostración de Operations Administrator, Field Guide y Adventure Tourist.

![Listado de rutas cargado desde el RESTful API](../assets/images/chapter-5/sprint3-exec-01.png)

*Figura 5.X. Listado de rutas de la agencia obtenido con `GET /api/v1/routes`.*

![Formulario de registro de una nueva ruta](../assets/images/chapter-5/sprint3-exec-02.png)

*Figura 5.X. Registro de la ruta `Laguna 69 Demo` (US07), enviado con `POST /api/v1/routes`.*

![Checkpoint registrado en la nueva ruta](../assets/images/chapter-5/sprint3-exec-03.png)

*Figura 5.X. Registro del checkpoint `Cebollapampa` con coordenadas e identificador Bluetooth (US08).*

![Ruta habilitada para la planificación de tours](../assets/images/chapter-5/sprint3-exec-04.png)

*Figura 5.X. Habilitación de la ruta mediante `PATCH /api/v1/routes/{id}/status`.*

![Grupo de expedición con guía asignado](../assets/images/chapter-5/sprint3-exec-05.png)

*Figura 5.X. Creación del grupo `Laguna 69 Grupo Demo` y asignación de la guía Lucía Paredes (US11 y US13).*

![Cuentas de la agencia](../assets/images/chapter-5/sprint3-exec-06.png)

*Figura 5.X. Creación de la cuenta del Field Guide `lucia@vitaltrek.demo` mediante `POST /api/v1/users`.*

![Notas de ruta y protocolo de seguridad](../assets/images/chapter-5/sprint3-exec-07.png)

*Figura 5.X. Registro de las notas de ruta y del protocolo de seguridad del grupo (US10).*

![Funcionalidad pendiente para el próximo sprint](../assets/images/chapter-5/sprint3-exec-08.png)

*Figura 5.X. Pestaña de seguimiento en campo, cuya integración con el RESTful API se realizará en un próximo sprint.*

![Manifiesto de turistas actualizado](../assets/images/chapter-5/sprint3-exec-09.png)

*Figura 5.X. Registro del participante `Lucas Prado` en el manifiesto por la guía asignada (US12).*

![Asignación de wearable al participante](../assets/images/chapter-5/sprint3-exec-10.png)

*Figura 5.X. Asignación del wearable `VT-W-010` mediante `PUT /api/v1/participant-preparations/{id}/wearable-assignment` (US15).*

![Preparación del turista](../assets/images/chapter-5/sprint3-exec-11.png)

*Figura 5.X. Registro del contacto de emergencia y del consentimiento del turista; el wearable queda activado (US14 y US16).*

**Video de navegación del Sprint 3:** [upc-pre-202620-1asi0730-16712-nexatech-productnavigation-sprint-3](https://upcedupe-my.sharepoint.com/:v:/g/personal/u202312566_upc_edu_pe/IQDKeKk3TNpkTYYaH-CaM33lARxSFJg5juS51cXSIAO2Wlk?nav=eyJyZWZlcnJhbEluZm8iOnsicmVmZXJyYWxBcHAiOiJPbmVEcml2ZUZvckJ1c2luZXNzIiwicmVmZXJyYWxBcHBQbGF0Zm9ybSI6IldlYiIsInJlZmVycmFsTW9kZSI6InZpZXciLCJyZWZlcnJhbFZpZXciOiJNeUZpbGVzTGlua0NvcHkifX0&e=m6od4Y)

#### 5.2.3.6. Services Documentation Evidence for Sprint Review

En el Sprint 3 se documentaron con OpenAPI Specification los 41 endpoints implementados en el RESTful Web Services. La especificación se genera a partir del proyecto ASP.NET Core con `Microsoft.AspNetCore.OpenApi` y se publica mediante **Scalar**, que permite explorar y ejecutar cada operación desde el navegador. Para cada endpoint se describen el verbo HTTP, la ruta, los parámetros, el cuerpo de la solicitud y los posibles responses; las descripciones de las operaciones se muestran en español mediante recursos localizados. Todos los endpoints, excepto los de autenticación, requieren el header `Authorization: Bearer <token>` con el token obtenido en el inicio de sesión, y cada operación se limita a los datos de la agencia del usuario autenticado.

**Repositorio:** [vitaltrek-backend](https://github.com/1ASI0729-2620-16712-G4-Nexatech/vitaltrek-backend)<br>
**Documentación desplegada (Scalar):** [https://vitaltrek-backend.onrender.com/scalar](https://vitaltrek-backend.onrender.com/scalar)<br>
**Especificación OpenAPI:** [https://vitaltrek-backend.onrender.com/openapi/v1.json](https://vitaltrek-backend.onrender.com/openapi/v1.json)

| Endpoint | HTTP Verb | Call Syntax | Parameters | Response Example | Response Explanation |
| --- | --- | --- | --- | --- | --- |
| `/api/v1/authentication/sign-up` | POST | `POST /api/v1/authentication/sign-up` | Body: `agencyName`, `name`, `username`, `password` | `201 Created` — `{ "id": 3, "username": "owner@agency.pe", "role": "operations_administrator", "agencyId": 2 }` | Registra una agencia y su Operations Administrator. 400 si los datos son inválidos y 409 si el usuario ya existe. No requiere token. |
| `/api/v1/authentication/sign-in` | POST | `POST /api/v1/authentication/sign-in` | Body: `username`, `password` | `200 OK` — `{ "id": 1, "username": "admin@vitaltrek.demo", "role": "operations_administrator", "agencyId": 1, "token": "eyJ..." }` | Autentica al usuario y devuelve un token bearer válido por 12 horas. 401 si las credenciales son inválidas. No requiere token. |
| `/api/v1/users` | GET | `GET /api/v1/users` | Header: `Authorization: Bearer <token>` | `200 OK` — lista de usuarios de la agencia | Lista los usuarios de la agencia. Solo Operations Administrator (403 para otros roles). |
| `/api/v1/users/{id}` | GET | `GET /api/v1/users/{id}` | Path: `id` | `200 OK` — usuario | Obtiene un usuario de la agencia. 404 si no existe. |
| `/api/v1/users` | POST | `POST /api/v1/users` | Body: `name`, `username`, `password`, `role`, `fieldGuideId`, `identityDocument` | `201 Created` — usuario creado | Crea un usuario Field Guide o Adventure Tourist en la agencia. Solo Operations Administrator; 409 si el usuario ya existe. |
| `/api/v1/routes` | GET | `GET /api/v1/routes` | — | `200 OK` — `[{ "id": 1, "name": "Cordillera Huayhuash Circuit", "difficulty": "Advanced", "status": "enabled" }]` | Lista las rutas de la agencia (US07). |
| `/api/v1/routes/{id}` | GET | `GET /api/v1/routes/{id}` | Path: `id` | `200 OK` — ruta | Obtiene una ruta de la agencia. 404 si no existe. |
| `/api/v1/routes` | POST | `POST /api/v1/routes` | Body: `name`, `origin`, `destination`, `distanceKm`, `elevationGainMeters`, `difficulty`, `estimatedDurationMinutes` | `201 Created` — ruta en estado `draft` | Registra una ruta en borrador (US07). Solo Operations Administrator. |
| `/api/v1/routes/{id}/status` | PATCH | `PATCH /api/v1/routes/{id}/status` | Path: `id`; Body: `status` | `200 OK` — ruta con el nuevo estado | Habilita o deshabilita una ruta. 409 si se intenta habilitar sin checkpoints. |
| `/api/v1/checkpoints` | GET | `GET /api/v1/checkpoints` | Query opcional: `routeId` | `200 OK` — lista de checkpoints | Lista los checkpoints de la agencia, opcionalmente por ruta (US08). |
| `/api/v1/checkpoints/{id}` | GET | `GET /api/v1/checkpoints/{id}` | Path: `id` | `200 OK` — checkpoint | Obtiene un checkpoint. 404 si no existe. |
| `/api/v1/checkpoints` | POST | `POST /api/v1/checkpoints` | Body: `routeId`, `location`, `sequenceOrder`, `bluetoothId`, `latitude`, `longitude` | `201 Created` — checkpoint creado | Registra un checkpoint Bluetooth en una ruta (US08). 409 ante orden o identificador duplicado. |
| `/api/v1/expected-time-windows` | GET | `GET /api/v1/expected-time-windows` | Query opcional: `routeId` | `200 OK` — lista de ventanas | Lista las ventanas de tiempo esperadas (US09). |
| `/api/v1/expected-time-windows/{id}` | GET | `GET /api/v1/expected-time-windows/{id}` | Path: `id` | `200 OK` — ventana | Obtiene una ventana de tiempo. 404 si no existe. |
| `/api/v1/expected-time-windows` | POST | `POST /api/v1/expected-time-windows` | Body: `routeId`, `fromCheckpointId`, `toCheckpointId`, `minimumMinutes`, `maximumMinutes` | `201 Created` — ventana creada | Registra el tiempo mínimo y máximo entre dos checkpoints (US09). |
| `/api/v1/route-notes` | GET | `GET /api/v1/route-notes` | Query opcional: `routeId` | `200 OK` — lista de notas | Lista las notas de ruta de la agencia. |
| `/api/v1/route-notes/{id}` | GET | `GET /api/v1/route-notes/{id}` | Path: `id` | `200 OK` — nota | Obtiene una nota de ruta. 404 si no existe. |
| `/api/v1/route-notes` | POST | `POST /api/v1/route-notes` | Body: `routeId`, `title`, `content`, `displayOrder` | `201 Created` — nota creada | Registra una nota de ruta consultable en campo. Solo Operations Administrator. |
| `/api/v1/route-notes/{id}` | PUT | `PUT /api/v1/route-notes/{id}` | Path: `id`; Body: `title`, `content`, `displayOrder` | `200 OK` — nota actualizada | Actualiza una nota de ruta. |
| `/api/v1/safety-protocols` | GET | `GET /api/v1/safety-protocols` | Query opcional: `routeId` | `200 OK` — lista de protocolos | Lista los protocolos de seguridad (US10). |
| `/api/v1/safety-protocols/{id}` | GET | `GET /api/v1/safety-protocols/{id}` | Path: `id` | `200 OK` — protocolo | Obtiene un protocolo. 404 si no existe. |
| `/api/v1/safety-protocols` | POST | `POST /api/v1/safety-protocols` | Body: `routeId`, `instructions` | `201 Created` — protocolo creado | Registra el protocolo de seguridad de una ruta (US10). |
| `/api/v1/safety-protocols/{id}` | PUT | `PUT /api/v1/safety-protocols/{id}` | Path: `id`; Body: `instructions`, `status` | `200 OK` — protocolo actualizado | Actualiza las instrucciones o el estado de un protocolo. |
| `/api/v1/field-guides` | GET | `GET /api/v1/field-guides` | — | `200 OK` — lista de guías | Lista los guías de la agencia. Solo Operations Administrator. |
| `/api/v1/field-guides/{id}` | GET | `GET /api/v1/field-guides/{id}` | Path: `id` | `200 OK` — guía | Obtiene un guía. 404 si no existe. |
| `/api/v1/field-guides` | POST | `POST /api/v1/field-guides` | Body: `name` | `201 Created` — guía creado | Registra un guía en la agencia. |
| `/api/v1/expedition-groups` | GET | `GET /api/v1/expedition-groups` | Query opcional: `routeId` | `200 OK` — lista de grupos | El administrador ve todos los grupos de la agencia; el guía, solo los asignados (US11). |
| `/api/v1/expedition-groups/{id}` | GET | `GET /api/v1/expedition-groups/{id}` | Path: `id` | `200 OK` — grupo | Obtiene un grupo visible para el usuario. 404 si no existe. |
| `/api/v1/expedition-groups` | POST | `POST /api/v1/expedition-groups` | Body: `routeId`, `name`, `departureDate`, `maximumCapacity` | `201 Created` — grupo en estado `scheduled` | Crea un grupo para una ruta habilitada (US11). Solo Operations Administrator. |
| `/api/v1/expedition-groups/{id}/field-guide` | PUT | `PUT /api/v1/expedition-groups/{id}/field-guide` | Path: `id`; Body: `fieldGuideId`, `confirmScheduleConflict` | `200 OK` — grupo con guía asignado | Asigna el guía responsable (US13). 409 si el guía tiene otro grupo en la misma fecha y no se confirmó el conflicto. |
| `/api/v1/manifest-entries` | GET | `GET /api/v1/manifest-entries` | Query opcional: `expeditionGroupId` | `200 OK` — lista de participantes | Lista los participantes visibles para el usuario (US12). |
| `/api/v1/manifest-entries/{id}` | GET | `GET /api/v1/manifest-entries/{id}` | Path: `id` | `200 OK` — participante | Obtiene un participante del manifiesto. 404 si no existe. |
| `/api/v1/manifest-entries` | POST | `POST /api/v1/manifest-entries` | Body: `expeditionGroupId`, `fullName`, `identityDocument` | `201 Created` — participante registrado | Registra un turista en el manifiesto y crea su preparación (US12). 409 si el grupo está lleno o el documento ya existe. |
| `/api/v1/wearable-devices` | GET | `GET /api/v1/wearable-devices` | — | `200 OK` — lista de wearables | Lista los wearables de la agencia. Solo Operations Administrator. |
| `/api/v1/wearable-devices/{id}` | GET | `GET /api/v1/wearable-devices/{id}` | Path: `id` | `200 OK` — wearable | Obtiene un wearable. 404 si no existe. |
| `/api/v1/wearable-devices` | POST | `POST /api/v1/wearable-devices` | Body: `code` | `201 Created` — wearable registrado | Registra un wearable disponible en la agencia. |
| `/api/v1/participant-preparations` | GET | `GET /api/v1/participant-preparations` | Query opcional: `expeditionGroupId` | `200 OK` — lista de preparaciones | Lista las preparaciones visibles para el usuario; el turista solo ve la suya. |
| `/api/v1/participant-preparations/{id}` | GET | `GET /api/v1/participant-preparations/{id}` | Path: `id` | `200 OK` — preparación | Obtiene una preparación. 404 si no existe. |
| `/api/v1/participant-preparations/{id}/wearable-assignment` | PUT | `PUT /api/v1/participant-preparations/{id}/wearable-assignment` | Path: `id`; Body: `wearableDeviceId` | `200 OK` — preparación con wearable asignado | Asigna un wearable a un participante (US15). 409 si el wearable no está disponible. |
| `/api/v1/participant-preparations/{id}/emergency-contact` | PUT | `PUT /api/v1/participant-preparations/{id}/emergency-contact` | Path: `id`; Body: `name`, `phone`, `relationship` | `200 OK` — preparación con contacto registrado | El turista registra su contacto de emergencia (US14). Solo Adventure Tourist. |
| `/api/v1/participant-preparations/{id}/consent` | PUT | `PUT /api/v1/participant-preparations/{id}/consent` | Path: `id`; Body: `granted` | `200 OK` — preparación con consentimiento y activación | El turista otorga o revoca el consentimiento de monitoreo; al otorgarlo se activa el wearable (US16). Solo Adventure Tourist. |

Los endpoints de creación responden `201 Created` y los de actualización `200 OK`. Ante datos inválidos responden `400 Bad Request`; sin token, `401 Unauthorized`; con un rol no autorizado, `403 Forbidden`; si el recurso no existe en la agencia, `404 Not Found`; y si se incumple una regla de negocio, `409 Conflict`.

A continuación se muestran capturas de la interacción con la documentación desplegada en Scalar usando los datos de demostración.

![Portada de la documentación del VitalTrek Platform API en Scalar](../assets/images/chapter-5/sprint3-scalar-home.png)

*Figura 5.X. Documentación del VitalTrek Platform API publicada con Scalar en Render.*

![Inicio de sesión ejecutado desde Scalar](../assets/images/chapter-5/sprint3-scalar-sign-in.png)

*Figura 5.X. Ejecución de `POST /api/v1/authentication/sign-in` con el usuario `admin@vitaltrek.demo`: respuesta `200 OK` con el token bearer.*

![Consulta de rutas ejecutada desde Scalar](../assets/images/chapter-5/sprint3-scalar-routes.png)

*Figura 5.X. Ejecución de `GET /api/v1/routes` con token bearer: respuesta `200 OK` con las cuatro rutas de la agencia.*

**Commits relacionados con la documentación de servicios:**

| Commit Id | Commit Message | Committed on (Date) |
| --- | --- | --- |
| `def4ee0` | chore: rename solution to VitalTrek and add shared infrastructure (configuración de OpenAPI y Scalar) | 2026-10-28 |
| `3a5c3f6` | feat(iam): add IAM bounded context with JWT authentication (metadatos OpenAPI localizados) | 2026-10-29 |
| `4514175` | feat(expedition-setup): add routes, checkpoints, expected time windows, route notes and safety protocols | 2026-10-29 |
| `ebe5c10` | feat(expedition-setup): add expedition groups, field guides, tourist manifest, wearables and participant preparation | 2026-10-29 |

#### 5.2.3.7. Software Deployment Evidence for Sprint Review

En el Sprint 3 se realizó el primer despliegue del RESTful Web Services de VitalTrek y se publicaron las versiones `v1.1.0` de las Web Applications, que consume dicho servicio, y del Landing Page. Las actividades comprendieron la creación de los servicios en Railway y Render, el aprovisionamiento de la base de datos MySQL administrada, la configuración del Web Service basado en Docker con sus variables de entorno, la publicación de la versión `v1.0.0` mediante GitFlow y la verificación del servicio desplegado a través de Scalar. La configuración detallada se describe en la sección 5.1.4. Para las Web Applications se actualizó en Vercel la variable `VITE_VITALTREK_API_URL` con la URL del API desplegado. La versión se numeró `v1.1.0` según Semantic Versioning, porque agrega funcionalidad compatible sobre la versión publicada en TB1.

| Producto | Plataforma | Repositorio | URL pública |
| --- | --- | --- | --- |
| Landing Page | Vercel | [landing-page](https://github.com/1ASI0729-2620-16712-G4-Nexatech/landing-page) | https://landing-page-mrca1.vercel.app/ |
| Web Applications | Vercel | [web-applications](https://github.com/1ASI0729-2620-16712-G4-Nexatech/web-applications) | https://web-applications-vert.vercel.app/ |
| RESTful Web Services | Render (Web Service con Docker) | [vitaltrek-backend](https://github.com/1ASI0729-2620-16712-G4-Nexatech/vitaltrek-backend) | https://vitaltrek-backend.onrender.com/scalar |
| Base de datos | Railway MySQL (plan Starter) | — | Acceso privado mediante credenciales |

**Pasos del despliegue del RESTful Web Services**

1. Creación del servicio MySQL en Railway con Public Networking habilitado, y obtención de los datos de conexión: host público (`centerbeam.proxy.rlwy.net`), puerto, usuario, nombre de base de datos y modo SSL `REQUIRED`.

![Servicio MySQL en Railway](../assets/images/chapter-5/sprint3-deploy-aiven.png)

*Figura 5.X. Servicio MySQL en estado Online en Railway, con Public Networking habilitado y los datos de conexión.*

2. Preparación de la versión en la rama `release/v1.0.0`: cadena de conexión de producción con puerto y SSL, `Dockerfile` que escucha en el puerto asignado por la plataforma y `.dockerignore`. La rama se integró en `main` y `develop` mediante Pull Requests y `main` se etiquetó como `v1.0.0`.
3. Creación del Web Service `vitaltrek-api` en Render conectado al repositorio `vitaltrek-backend`, con runtime Docker, rama `main` y plan Free, y registro de las variables de entorno de la base de datos y de la clave de firma JWT.

![Variables de entorno del servicio en Render](../assets/images/chapter-5/sprint3-deploy-render-env.png)

*Figura 5.X. Variables de entorno del Web Service `vitaltrek-api` en Render, con los valores ocultos.*

4. Construcción de la imagen Docker e inicio del contenedor: la aplicación leyó las variables de entorno de Railway, aplicó las migraciones sobre la base de datos, cargó los datos de demostración y quedó publicada en https://vitaltrek-backend.onrender.com.

![Despliegue exitoso del servicio en Render](../assets/images/chapter-5/sprint3-deploy-render-live.png)

*Figura 5.X. Despliegue en estado Live en Render.*

5. Verificación del servicio en https://vitaltrek-backend.onrender.com/scalar: el inicio de sesión con `admin@vitaltrek.demo` respondió `200 OK` con el token bearer y `GET /api/v1/routes` respondió `200 OK` con las rutas de la agencia (sección 5.2.3.6).

**Pasos del despliegue de las Web Applications**

1. Integración de `feature/backend-integration` en `develop` mediante Pull Request, creación de la rama `release/v1.1.0` e integración en `main` y `develop`, con la etiqueta `v1.1.0` en `main`.
2. Actualización de la variable de entorno `VITE_VITALTREK_API_URL` en Vercel con la URL base del RESTful Web Services, para los entornos Production y Preview.

![Variable de entorno de las Web Applications en Vercel](../assets/images/chapter-5/sprint3-deploy-vercel-env.png)

*Figura 5.X. Variable `VITE_VITALTREK_API_URL` configurada en Vercel con la URL del API desplegado.*

3. Verificación de `main` como Production Branch del proyecto en Vercel.

![Production Branch del proyecto en Vercel](../assets/images/chapter-5/sprint3-deploy-vercel-branch.png)

*Figura 5.X. Configuración de `main` como Production Branch y dominio `web-applications-vert.vercel.app`.*

4. Nuevo despliegue de producción a partir del commit `4166921` (`Release/v1.1.0`) de la rama `main`, en estado Ready.

![Despliegue de las Web Applications en Vercel](../assets/images/chapter-5/sprint3-deploy-vercel-ready.png)

*Figura 5.X. Despliegue de producción de las Web Applications `v1.1.0` en Vercel.*

5. Verificación en https://web-applications-vert.vercel.app/: el inicio de sesión del Operations Administrator y el listado de rutas responden con datos del RESTful Web Services.

![Listado de rutas en las Web Applications desplegadas](../assets/images/chapter-5/sprint3-deploy-webapp-routes.png)

*Figura 5.X. Listado de rutas obtenido del RESTful Web Services desde las Web Applications desplegadas.*

**Pasos del despliegue del Landing Page**

1. Creación de la rama `release/v1.1.0` desde `develop` con los cambios del Sprint 3: enlaces a las Web Applications, grilla de una columna en móvil, redes sociales y ubicación en contacto y footer, y corrección del texto del hero y del i18n del login. La rama se integró en `main` mediante Pull Request y `main` se etiquetó como `v1.1.0`.
2. Despliegue automático de producción en Vercel a partir del commit `4649e05` (`Release/v1.1.0`) de la rama `main`.

![Despliegue del Landing Page en Vercel](../assets/images/chapter-5/sprint3-deploy-landing-ready.png)

*Figura 5.X. Despliegue de producción del Landing Page `v1.1.0` en estado Ready en Vercel.*

3. Verificación del Landing Page publicado, con los enlaces a redes sociales incorporados en el footer.

![Footer del Landing Page con redes sociales](../assets/images/chapter-5/sprint3-deploy-landing-footer.png)

*Figura 5.X. Footer del Landing Page `v1.1.0` con los enlaces a redes sociales.*

#### 5.2.3.8. Team Collaboration Insights during Sprint

Durante el Sprint 3, el equipo trabajó sobre los repositorios [vitaltrek-backend](https://github.com/1ASI0729-2620-16712-G4-Nexatech/vitaltrek-backend), [web-applications](https://github.com/1ASI0729-2620-16712-G4-Nexatech/web-applications) y [landing-page](https://github.com/1ASI0729-2620-16712-G4-Nexatech/landing-page), aplicando GitFlow: `develop` como rama de integración, feature branches por funcionalidad y Pull Requests revisados por otro integrante antes de su integración. Todos los integrantes participaron en la implementación del RESTful Web Services. A continuación se resume la contribución de cada integrante y se presentan los analíticos de colaboración de GitHub.

| Integrante | Contribución en el Sprint 3 | Evidencia de GitHub |
| --- | --- | --- |
| Cayanchi Avila, Milenko Rubén (`MaxghZZ`) | Implementó el bounded context IAM (autenticación JWT, registro y login), el bounded context Expedition Setup (rutas, checkpoints, grupos de expedición, guías de campo, manifiesto turístico, wearables y preparación de participantes) y el bounded context Field Tracking. Configuró el contenedor Docker, las variables de entorno de producción y el despliegue en Render. Integró el frontend con el RESTful Web Services (IAM y Expedition Setup) y publicó la Release `v1.1.0` del frontend. Revisó y aprobó los PRs de los demás bounded contexts. Commits representativos: `8759081`, `4514175`, `b5331de`, `a6241c8`, `8886380`, `cab65a3`. | [vitaltrek-backend](https://github.com/1ASI0729-2620-16712-G4-Nexatech/vitaltrek-backend) · [web-applications](https://github.com/1ASI0729-2620-16712-G4-Nexatech/web-applications) |
| Herrera Enriquez, Diego Fernando (`DerDFHE`) | Implementó el bounded context Safety Monitoring (modelo de dominio EarlyWarningAlert, servicios de aplicación, fachada ACL con ExpectedTimeWindow, persistencia con EF Core, endpoints REST y migración de base de datos). En las Web Applications, configuró el entorno de desarrollo para apuntar al backend local y agregó pruebas unitarias para los flujos de sesión IAM, pantalla de errores y preparación de participantes. Commits representativos: `b4afa03`, `95dda1d`, `ef1b583`, `6e30a3a`, `9d74e83`. | [vitaltrek-backend](https://github.com/1ASI0729-2620-16712-G4-Nexatech/vitaltrek-backend) · [web-applications](https://github.com/1ASI0729-2620-16712-G4-Nexatech/web-applications) |
| León Naupari, Jorge Mateo (`mateool10`) | Implementó el bounded context Incident Response (modelo de dominio Incident y Notification, servicios de aplicación con validación de sesión de expedición, fachada ACL para contar incidentes, persistencia con EF Core, endpoints REST y migración de base de datos). Colaboró en la integración de los bounded contexts de Expedition Setup mediante pruebas unitarias de reglas de rutas y checkpoints. Commits representativos: `843ef1c`, `b7a9cd7`, `2937cdb`, `3b99692`, `b7318fd`. | [vitaltrek-backend](https://github.com/1ASI0729-2620-16712-G4-Nexatech/vitaltrek-backend) |
| Mendoza Blanco, Ariel Roberto (`Trepequiper`) | Implementó el bounded context Tour Closure completo: modelo de dominio TourSummary, comandos y queries, interfaces de repositorio y servicios, implementaciones de servicios de comando y consulta, repositorio EF Core, configuración de entidad, DTOs de recursos y assembler, endpoints REST en TourSummariesController, registro DI en Program.cs y migración de base de datos. Colaboró en pruebas unitarias de Expedition Setup. Commits representativos: `dd7b0d9`, `268f33f`, `0421678`, `1527d2e`, `4cd43e6`, `5fb3b48`. | [vitaltrek-backend](https://github.com/1ASI0729-2620-16712-G4-Nexatech/vitaltrek-backend) |
| Rodriguez Rojas, Miler Alexander (`Miler2003`) | Implementó el bounded context Checkpoint Sync (modelo de dominio CheckpointPassage, servicios de aplicación, fachada ACL, persistencia EF Core, endpoints REST y migración de base de datos). Actualizó las pruebas unitarias de Expedition Setup al API de dominio actual y agregó pruebas de paso por checkpoint. Protegió la configuración de desarrollo removiendo credenciales de los archivos versionados y documentó el README inicial del repositorio. Commits representativos: `0265254`, `864b3b9`, `6067764`, `fc16027`, `41f4bfd`. | [vitaltrek-backend](https://github.com/1ASI0729-2620-16712-G4-Nexatech/vitaltrek-backend) |

![Commits del repositorio vitaltrek-backend durante el Sprint 3](../assets/images/chapter-5/sprint3-commits-vitaltrek-backend.png)

*Figura 5.X. Commits del repositorio vitaltrek-backend durante el Sprint 3.*

![GitHub Insights del repositorio vitaltrek-backend durante el Sprint 3](../assets/images/chapter-5/sprint3-insights-vitaltrek-backend.png)

*Figura 5.X. GitHub Insights (Contributors) del repositorio vitaltrek-backend para el periodo del Sprint 3.*

## 5.3. Validation Interviews

En esta sección se registran y explican las entrevistas de validación realizadas con representantes de los dos segmentos objetivo de VitalTrek: los **dueños o responsables de agencias de turismo de aventura** y los **turistas de aventura**. A diferencia de las entrevistas de las entrevistas anteriores, que tuvieron un enfoque de descubrimiento, estas sesiones tienen un enfoque de **validación**: los participantes interactúan con el Landing Page y con las Web Applications desplegadas, realizan tareas concretas y manifiestan sus observaciones. Los resultados se evalúan según heurísticas de usabilidad, diseño inclusivo y arquitectura de información, con el formato indicado para el proyecto.

### 5.3.1. Diseño de Entrevistas

Las sesiones de validación buscan comprobar si la solución implementada resuelve los problemas identificados en el Needfinding y si los usuarios pueden completar los flujos principales sin ayuda. Para ello, cada participante recibe un conjunto de tareas sobre los productos desplegados y el entrevistador observa su comportamiento, registra las dificultades y, al finalizar, recoge sus apreciaciones.

### Objetivos Generales del Proceso de Validación

1. Verificar que los visitantes de cada segmento comprendan la propuesta de valor de VitalTrek a partir del Landing Page y encuentren la información y los Call-To-Action dirigidos a su segmento.
2. Comprobar que los usuarios puedan completar los user flows principales de las Web Applications definidos en la sección 4.4.4, sin asistencia del entrevistador.
3. Identificar problemas de usabilidad, diseño inclusivo y arquitectura de información, y clasificarlos según su severidad.
4. Contrastar los Lean UX Hypothesis Statements y los assumptions de la sección 1.2.2 con el comportamiento real observado en los usuarios.
5. Recoger testimonios de los participantes que sustenten la propuesta de valor y que puedan incluirse en el Video About-the-Product.

### Principios aplicados a la conducción de las sesiones

- Se pide al participante **pensar en voz alta** (think-aloud) mientras realiza cada tarea.
- El entrevistador **no explica la interfaz ni indica dónde hacer clic**; solo lee la tarea y observa.
- Las tareas se formulan como **objetivos del usuario**, no como instrucciones de interfaz: "registre a los participantes de su grupo" en lugar de "haga clic en el botón Manifiesto".
- Ante una dificultad, se repregunta de forma neutra: "¿qué esperaba encontrar?", "¿qué haría ahora?".
- Las preguntas de opinión se realizan **al finalizar todas las tareas**, para no influir en el comportamiento observado.

---

### Segmento 1: Dueños o Responsables de Agencias de Turismo de Aventura

**Perfil del participante:** propietarios, jefes de operaciones o guías principales de agencias de turismo de aventura que operen rutas en zonas con conectividad limitada.

**Elementos incluidos en la sesión:** Landing Page y Web Application (espacios de trabajo de Operations Administrator y Field Guide).

**Tareas en el Landing Page**

1. Identifique qué problema resuelve VitalTrek para una agencia como la suya.
2. Encuentre los planes disponibles para agencias y su precio.
3. Cambie el idioma del sitio a inglés y luego regrese a español.
4. Solicite información o una demostración del producto.
5. Acceda a la aplicación desde la sección dirigida a agencias.

**Tareas en la Web Application (user flows de la sección 4.4.4)**

6. Inicia sesión con tu cuenta de administrador de operaciones.
7. Registra una nueva ruta con sus datos principales (nombre, origen, destino, distancia, dificultad y duración estimada).
8. Agrega los checkpoints de la ruta en el orden del recorrido y define los tiempos esperados entre cada tramo.
9. Crea un grupo de expedición para esa ruta y asígnale un guía de campo.
10. Con el rol de guía, registra a los participantes del grupo en el manifiesto.
11. Consulta el progreso en tiempo real de un grupo que se encuentra actualmente en ruta.

**Preguntas posteriores a las tareas**

1. ¿Qué tarea le resultó más difícil? ¿Por qué?
2. ¿Hubo algún momento en que no supo qué hacer a continuación?
3. ¿Qué información esperaba ver sobre sus grupos que no encontró?
4. ¿Cómo se compara esta forma de preparar un tour con la forma en que lo hace hoy?
5. ¿Qué cambiaría o agregaría para usarlo en su operación?
6. ¿Recomendaría VitalTrek a otra agencia? ¿Por qué?

---

### Segmento 2: Turistas de Aventura

**Perfil del participante:** personas que practican trekking, caminatas o rutas de montaña y que contratan agencias para recorridos de mayor dificultad, duración o riesgo, preferentemente en zonas sin cobertura móvil.

**Elementos incluidos en la sesión:** Landing Page y Web Application.

**Tareas en el Landing Page**

1. Identifique cómo VitalTrek protege a un turista durante un recorrido sin señal.
2. Encuentre qué beneficios ofrece VitalTrek a los turistas.
3. Consulte cómo se tratan sus datos personales y de salud.
4. Cambie el idioma del sitio a inglés y luego regrese a español.
5. Acceda a la aplicación desde la sección dirigida a turistas.

**Tareas en la Web Application**

6. Inicia sesión con tu cuenta de turista.
7. Busca el grupo de expedición al que estás inscrito.
8. Registra tu contacto de emergencia (nombre, teléfono y parentesco).
9. Da tu consentimiento para participar en el tour.
10. Descarga la información del tour para acceder sin señal.
11. Consulta la ruta y los checkpoints de tu expedición.

**Preguntas posteriores a las tareas**

1. ¿Qué tarea le resultó más difícil? ¿Por qué?
2. ¿Entendió qué datos suyos registra VitalTrek y para qué los usa?
3. ¿Se sentiría más tranquilo si la agencia con la que viaja utilizara VitalTrek? ¿Por qué?
4. ¿Qué información esperaba encontrar que no encontró?
5. ¿Recomendaría a una agencia que utilice VitalTrek?

---

### Consideraciones de las Sesiones de Validación

**Cantidad de entrevistas:** mínimo 3 y máximo 5 por segmento, conforme al enunciado del proyecto.

**Entorno:** las sesiones se realizan sobre las versiones desplegadas del Landing Page y de las Web Applications, en desktop o mobile web browser según el dispositivo habitual del participante. Se registra el dispositivo y el navegador utilizados.

**Registro:** las sesiones se graban en video con consentimiento previo del participante, incluyendo la pantalla y la voz. Las grabaciones se consolidan en un único video de validación.

**Evaluación:** los problemas observados se clasifican según la escala de severidad y las heurísticas de usabilidad, diseño inclusivo y arquitectura de información de la sección 5.3.3.

**Ética:** antes de cada sesión se informa al participante sobre el propósito de la validación, la confidencialidad de sus respuestas y su derecho a retirarse en cualquier momento. Los datos utilizados en las tareas son ficticios.

### 5.3.2. Registro de Entrevistas

En esta sección se presentan los registros de las entrevistas de validación realizadas para cada segmento objetivo. Todas las sesiones se consolidan en el video [upc-pre-202620-1asi0730-16712-nexatech-validation-sprint-3](<!-- COMPLETAR: URL de Microsoft Stream -->).

![Captura del video de validación](../assets/images/chapter-5/validation-video.png)
<!-- COMPLETAR: captura representativa del video -->

#### Segmento 1: Dueños o Responsables de Agencias de Turismo de Aventura

| **Entrevista #1** | |
| --- | --- |
| **Nombre** | <!-- COMPLETAR --> |
| **Apellidos** | <!-- COMPLETAR --> |
| **Edad** | <!-- COMPLETAR --> |
| **Distrito** | <!-- COMPLETAR --> |
| **Rol** | <!-- COMPLETAR --> |
| **Dispositivo y navegador** | <!-- COMPLETAR --> |
| **Evidencias** | ![Entrevista de validación 1 del segmento 1](../assets/images/chapter-5/validation/Validacion1Segmento1.png) |
| **Link** | [Ver Video](<!-- COMPLETAR -->) |
| **Timing donde inicia la entrevista** | <!-- COMPLETAR: mm:ss min --> |
| **Duración de la entrevista** | <!-- COMPLETAR: mm:ss min --> |
| **Resumen** | <!-- COMPLETAR: qué tareas completó sin ayuda, en cuáles tuvo dificultades y por qué, qué comentó al finalizar y cuál fue su apreciación general --> |

| **Entrevista #2** | |
| --- | --- |
| **Nombre** | Diego |
| **Apellidos** | Livimoro |
| **Edad** | 38 años |
| **Distrito** | Magdalena del Mar, Lima |
| **Rol** | Dueño / responsable de agencia de turismo de aventura |
| **Dispositivo y navegador** | Laptop con Windows, navegador Brave |
| **Evidencias** | ![Entrevista de validación 2 del segmento 1](../assets/images/chapter-5/validation/Validacion2Segmento1.png) |
| **Link** | [Ver Video](https://upcedupe-my.sharepoint.com/:v:/g/personal/u20241a827_upc_edu_pe/IQBtOnmgiHHkRqqiVnRZTWB6AXinsHZ_8DOSNfUrMwRdAlc?e=t7fDHG) |
| **Timing donde inicia la entrevista** | 00:00 min |
| **Duración de la entrevista** | 10:21 min |
| **Resumen** | Diego completó sin ayuda las once tareas propuestas. En el Landing Page identificó la propuesta de monitoreo por puntos de control en zonas sin cobertura y valoró que la solución no prometa cobertura continua sino evidencia periódica, ubicó la sección de planes, verificó el cambio de idioma entre español e inglés —señaló que sus mayoristas extranjeros se lo exigirían en inglés— y envió una solicitud de demostración. En las Web Applications ingresó con el rol de administrador de operaciones y ejecutó el flujo completo de configuración: registró la ruta Trekking Colca Sangalle, agregó sus tres puntos de control ordenados, habilitó la ruta, configuró las ventanas de tiempo esperadas de cada tramo y creó el grupo Grupo Colca Diciembre con fecha de salida 20/12/2026 y capacidad 12; con el rol de guía de campo registró al participante en el manifiesto y, de vuelta como administrador, consultó el progreso de un grupo en ruta. Observó dos limitaciones. Al asignar el guía, la lista muestra únicamente nombres sin un identificador que permita distinguir entre guías homónimos, lo que considera un riesgo en una operación con quince guías. Al revisar el seguimiento preguntó si el historial queda almacenado y puede descargarse para responder a una aseguradora o a una homologación de mayorista, y no encontró una opción de exportación. Sobre las ventanas de tiempo comentó que le parece correcto que se pida un rango y no un valor fijo, aunque los campos están en minutos y él maneja horas. En su apreciación general comparó la solución con su protocolo de seguridad en papel, que depende de que el guía recuerde reportar y encuentre señal, y valoró que aquí el registro se genere al paso por el punto de control. Como mejoras prioritarias pidió la exportación del historial por grupo con horas y códigos de identificación para los guías. Indicó que recomendaría el producto a agencias que operen rutas de varios días. |

| **Entrevista #3** | |
| --- | --- |
| **Nombre** | Luis |
| **Apellidos** | Mendoza |
| **Edad** | 41 años |
| **Distrito** | Santiago de Surco, Lima |
| **Rol** | Dueño de agencia de turismo de aventura |
| **Dispositivo y navegador** | Laptop con Windows, Opera GX |
| **Evidencias** | ![Entrevista de validación 3 del segmento 1](../assets/images/chapter-5/validation/Validacion3Segmento1.png) |
| **Link** | [Ver Video](https://upcedupe-my.sharepoint.com/:v:/g/personal/u20241a827_upc_edu_pe/IQB9Gu0sEsMgQ6Th3nnuzVWWAaE0ZuAxk0x4ddSl9EI7ajM?e=3Zd72p) |
| **Timing donde inicia la entrevista** | 00:00 min |
| **Duración de la entrevista** | 09:56 min |
| **Resumen** | Luis completó las quince tareas propuestas. En el Landing Page comprendió la propuesta de monitoreo por puntos de control en rutas sin cobertura y la relacionó con su propia operación, identificó en la sección de planes que una agencia con cinco grupos activos corresponde al plan Operator de S/ 199 por incluir hasta ocho grupos y las alertas tempranas, verificó el cambio de idioma entre español e inglés y consultó las preguntas frecuentes para confirmar que la solución no funciona como un rastreador GPS continuo sino por sincronización en checkpoints. En las Web Applications ingresó por el acceso de operaciones de la agencia, leyó el panel de operaciones para identificar cuántas rutas están registradas y cuántas habilitadas, y utilizó los filtros de dificultad y estado del listado de rutas. Registró la ruta Trekking Santa Cruz con sus datos geográficos y operativos, agregó sus tres puntos de control ordenados, habilitó la ruta, configuró las ventanas de tiempo esperadas de cada tramo y creó el grupo Grupo Santa Cruz Diciembre con fecha de salida 18/12/2026 y capacidad 12. Luego registró un guía de campo, le creó su cuenta de acceso vinculándola al guía y lo asignó al grupo; finalmente, con el rol de guía de campo, accedió al espacio de campo y registró a los participantes en el manifiesto. Señaló tres fricciones: el campo de duración de la ruta se expresa en horas mientras que él planifica en días, las ventanas de tiempo se piden en minutos cuando maneja horas, y dar de alta a un guía y crear su cuenta de acceso son dos acciones separadas que al inicio interpretó como una sola. También indicó que esperaba un formulario de contacto en el Landing Page y solo encontró una dirección de correo, y que echa en falta un campo para datos de salud o contacto de emergencia en el manifiesto. En su apreciación general valoró que la configuración se hace una sola vez y queda guardada, frente a su práctica actual de armar cada tour desde cero en una hoja de cálculo, y recomendaría el producto a agencias que operen rutas de varios días. |

<!-- COMPLETAR: repetir la tabla para las entrevistas #4 y #5 -->

#### Segmento 2: Turistas de Aventura

| **Entrevista #1** | |
| --- | --- |
| **Nombre** | Alejandro Manuel |
| **Apellidos** | Molina Vasquez |
| **Edad** | 25 años |
| **Distrito** | San Miguel, Lima |
| **Rol** | Turista de aventura |
| **Dispositivo y navegador** | Samsung S24, Google Chrome |
| **Evidencias** | ![Entrevista de validación 1 del segmento 2](../assets/images/chapter-5/validation/Validacion1Segmento2.png) |
| **Link** | [Ver Video](https://upcedupe-my.sharepoint.com/:v:/g/personal/u20241a827_upc_edu_pe/IQC3hudLgmLgQ6F1w5X9UWWAAe0BWKtMND8Eg8Zj-wCulDc?e=MsBi7v) |
| **Timing donde inicia la entrevista** | 00:00 min |
| **Duración de la entrevista** | 09:36 min |
| **Resumen** | Manuel Alejandro revisó la landing page, comprendió la propuesta de monitoreo sin conexión y verificó el funcionamiento del cambio de idioma. En la aplicación, ingresó con su cuenta de turista, registró un contacto de emergencia, otorgó su consentimiento y descargó la información de la ruta para uso offline; completó todas las tareas sin dificultades, en parte porque recibió indicaciones paso a paso del entrevistador, y describió la interfaz como intuitiva. Valoró especialmente el acceso offline, la sincronización de puntos de control y la visualización del mapa con sus checkpoints, aunque señaló como mejora prioritaria mostrar su ubicación exacta y el progreso por tramos ya recorridos. Indicó que recomendaría la aplicación a una agencia siempre que se incorporen esas mejoras de seguimiento. |

| **Entrevista #2** | |
| --- | --- |
| **Nombre** | Fernando |
| **Apellidos** | Flores Pinchi |
| **Edad** | 22 años |
| **Distrito** | Callao, Lima |
| **Rol** | Turista de aventura |
| **Dispositivo y navegador** | Google Chrome |
| **Evidencias** | ![Entrevista de validación 2 del segmento 2](../assets/images/chapter-5/Validacion2Segmento2.png) |
| **Link** | [Ver Video](https://upcedupe-my.sharepoint.com/personal/u20241a827_upc_edu_pe/_layouts/15/stream.aspx?id=%2Fpersonal%2Fu20241a827_upc_edu_pe%2FDocuments%2FEntrevistas%2FSegmento%202%2F2026-11-12%2000-02-06%2Emp4&referrer=StreamWebApp%2EWeb&referrerScenario=AddressBarCopied%2Eview%2E60f04891-a616-4409-bba7-4db012ed4cef) |
| **Timing donde inicia la entrevista** | 00:00 min |
| **Duración de la entrevista** | 06:06 min |
| **Resumen** | Fernando (22 años), quien cuenta con experiencia en rutas de trekking sin cobertura móvil, revisó la landing page de Vital Trek y la describió como visualmente atractiva, intuitiva y bien organizada por secciones, sin encontrar dificultades para navegarla; comprendió claramente la propuesta de expediciones sincronizadas y la generación de puntos de control (checkpoints) para resguardar su ubicación y evitar extravíos al perder la señal. En la aplicación, ingresó bajo el perfil de aventurero (con datos precargados de prueba), revisó el resumen del recorrido, la configuración del contacto de emergencia (nombre, teléfono y parentesco) y el mapa con las coordenadas exactas de parada y alojamiento, entendiendo qué información registra el sistema y con qué finalidad. Valoró especialmente la seguridad de conservar sus coordenadas exactas sin conexión y afirmó que viajaría más tranquilo si su agencia usara la plataforma, aunque señaló como mejora la posibilidad de ingresar manualmente sus propios datos personales (como nombre y edad) y registrar por sí mismo la ruta que va a recorrer. Finalmente, indicó que sí recomendaría a una agencia implementar la versión final de la aplicación para garantizar la seguridad de los turistas de aventura. |

<!-- COMPLETAR: repetir la tabla para las entrevistas #2 y #3 (hasta #5) -->

#### Resultados de las tareas por segmento

Para cada segmento se consolida cuántos participantes completaron cada tarea, según lo registrado en el resumen de cada entrevista.

*Nota: el Segmento 1 considera 2 de 3 entrevistas registradas (la entrevista #1 está pendiente) y el Segmento 2, 2 de 3 (la entrevista #3 está pendiente). En el Segmento 1, Diego Livimoro completó sus tareas sin ayuda; el resumen de Luis Mendoza no indica si requirió ayuda. En el Segmento 2, Alejandro Manuel Molina Vasquez completó las tareas siguiendo indicaciones paso a paso del entrevistador. El asterisco (\*) indica que el resumen de uno de los participantes no registra esa tarea. La tabla se actualizará al concluir todas las sesiones.*

| Tarea | Seg. 1 — Agencias (n = 2) | Seg. 2 — Turistas (n = 2) | Observación principal |
| --- | --- | --- | --- |
| Identificar la propuesta de valor en el Landing Page | 2 de 2 | 2 de 2 | Ambos segmentos comprendieron la propuesta de monitoreo por checkpoints en rutas sin cobertura móvil. |
| Localizar planes y precios (Seg. 1) / beneficios para turistas (Seg. 2) | 2 de 2 | 1 de 2\* | Seg. 1: un participante identificó que una agencia con cinco grupos activos corresponde al plan Operator. |
| Cambiar el idioma a inglés y volver a español | 2 de 2 | 1 de 2\* | Seg. 1: un participante señaló que sus mayoristas extranjeros se lo exigirían en inglés. |
| Solicitar información o demostración (Seg. 1) / acceder a la aplicación (Seg. 2) | 1 de 2\* | 2 de 2 | Seg. 1: un participante esperaba un formulario de contacto en el Landing Page y solo encontró una dirección de correo. |
| Iniciar sesión con la cuenta del rol asignado | 2 de 2 | 2 de 2 | — |
| Registrar ruta y checkpoints con tiempos esperados (Seg. 1) / registrar contacto de emergencia y dar consentimiento (Seg. 2) | 2 de 2 | 1 de 2\* | Seg. 1: los dos participantes señalaron que las ventanas de tiempo se piden en minutos, mientras ellos planifican en horas. Seg. 2: un participante pidió poder ingresar por sí mismo sus datos personales y la ruta que va a recorrer. |
| Crear grupo, asignar guía y registrar manifiesto (Seg. 1) / descargar información de la ruta offline (Seg. 2) | 2 de 2 | 1 de 2\* | Seg. 1: la lista de guías muestra solo nombres, sin un identificador para distinguir guías homónimos; un participante echó en falta un campo para datos de salud en el manifiesto. |
| Consultar el progreso de un grupo en ruta (Seg. 1) / consultar ruta y checkpoints de la expedición (Seg. 2) | 1 de 2\* | 2 de 2 | Seg. 1: un participante no encontró una opción para exportar el historial del grupo. Seg. 2: un participante pidió ver su ubicación exacta y el progreso por tramos ya recorridos. |

En las entrevistas registradas, los participantes de ambos segmentos completaron los flujos principales del Landing Page y de las Web Applications. En el Segmento 1, las fricciones se concentran en la unidad de las ventanas de tiempo (minutos en la interfaz, horas en la planificación de las agencias) y en la identificación de guías solo por nombre, problemas clasificados en la sección 5.3.3 con severidad 3 y 2 respectivamente. En el Segmento 2, un participante pidió ver su ubicación exacta y el progreso por tramos recorridos, y otro pidió poder registrar por sí mismo sus datos personales y su ruta.

> Los resultados corresponden a la muestra de participantes de las sesiones de validación y no representan a todas las agencias o turistas del Perú.

### 5.3.3. Evaluaciones según heurísticas

En esta sección se evalúan las sesiones de validación según heurísticas de usabilidad, diseño inclusivo y arquitectura de información, con el formato UX Heuristics & Principles Evaluation indicado para el proyecto. Cada problema se registra con su severidad, la heurística o principio que viola y una recomendación de corrección, que se incorpora al Product Backlog para los siguientes Sprints.

Las heurísticas aplicadas son:

- **Usability:** las 10 heurísticas de usabilidad de Jakob Nielsen.
- **Inclusive Design:** los Inclusive Design Principles (proporciona experiencias comparables, considera la situación, sé consistente, da el control, ofrece opciones, prioriza el contenido y agrega valor).
- **Information Architecture:** las heurísticas de arquitectura de información de Abby Covert (findable, accessible, clear, communicative, useful, credible, controllable, valuable, learnable y delightful).

**UX Heuristics & Principles Evaluation**
**Usability – Inclusive Design – Information Architecture**

| | |
| --- | --- |
| **CARRERA** | Ingeniería de Software |
| **CURSO** | Aplicaciones Web |
| **SECCIÓN** | 16712 |
| **PROFESORES** | Sánchez Seña, Alberto Wilmer |
| **AUDITOR** | NexaTech |
| **CLIENTE(S)** | Diego Livimoro, Luis Mendoza y Alejandro Manuel Molina Vasquez |

**SITE o APP A EVALUAR:** VitalTrek: Landing Page y Web Applications.

**TAREAS A EVALUAR:**

El alcance de esta evaluación incluye la revisión de la usabilidad de las siguientes tareas:

1. Consulta de la propuesta de valor y de los planes en el Landing Page.
2. Cambio de idioma en el Landing Page y en la Web Application.
3. Acceso a la Web Application desde los Call-To-Action de cada segmento.
4. Registro de una ruta con sus datos geográficos y operativos.
5. Definición de los checkpoints de una ruta y habilitación de la misma.
6. Configuración de las ventanas de tiempo esperadas por tramo.
7. Creación de un grupo de expedición y asignación de un guía de campo.
8. Registro de un guía de campo y creación de su cuenta de acceso.
9. Registro del manifiesto de turistas con el rol de guía de campo.
10. Registro del contacto de emergencia y del consentimiento con el rol de turista.

No están incluidas en esta versión de la evaluación las siguientes tareas:

1. Consulta del progreso estimado de un grupo de expedición.
2. Revisión y atención de alertas tempranas.
3. Captura offline y sincronización de telemetría en checkpoints.
4. Gestión de incidentes, emergencias y evacuaciones.
5. Cierre del tour y generación del Tour Summary.

Las dos primeras corresponden a funcionalidades cuya integración con el RESTful Web Services está planificada para el siguiente Sprint, por lo que en la versión desplegada presentan el aviso correspondiente y no fueron sometidas a evaluación.

**ESCALA DE SEVERIDAD:**

Los errores serán puntuados tomando en cuenta la siguiente escala de severidad:

| Nivel | Descripción |
| :---: | --- |
| 1 | Problema superficial: puede ser fácilmente superado por el usuario u ocurre con muy poca frecuencia. No necesita ser arreglado a no ser que exista disponibilidad de tiempo. |
| 2 | Problema menor: puede ocurrir un poco más frecuentemente o es un poco más difícil de superar para el usuario. Se le debería asignar una prioridad baja para resolverlo de cara al siguiente release. |
| 3 | Problema mayor: ocurre frecuentemente o los usuarios no son capaces de resolverlo. Es importante que sea corregido y se le debe asignar una prioridad alta. |
| 4 | Problema muy grave: un error de gran impacto que impide al usuario continuar con el uso de la herramienta. Es imperativo que sea corregido antes del lanzamiento. |

**TABLA RESUMEN:**

| # | Problema | Escala de severidad | Heurística/Principio violada(o) |
| :---: | --- | :---: | --- |
| 1 | Las ventanas de tiempo esperadas se solicitan en minutos | 3 | Usability: Coincidencia entre el sistema y el mundo real |
| 2 | El estado de borrador de una ruta no comunica la acción necesaria para habilitarla | 3 | Usability: Visibilidad del estado del sistema |
| 3 | El manifiesto de turistas no admite información de salud del participante | 3 | Inclusive Design: Considera la situación |
| 4 | La duración estimada de la ruta se solicita en horas | 2 | Usability: Coincidencia entre el sistema y el mundo real |
| 5 | La lista de guías de campo no permite distinguir entre guías homónimos | 2 | Usability: Reconocimiento antes que recuerdo |
| 6 | Registrar un guía de campo y crear su cuenta de acceso son dos acciones separadas | 2 | Usability: Consistencia y estándares |

**DESCRIPCIÓN DE PROBLEMAS:**

**PROBLEMA #1:** Las ventanas de tiempo esperadas se solicitan en minutos

**Severidad:** 3
**Heurística violada:** Usability: Coincidencia entre el sistema y el mundo real

**Problema:**

En la tarea de configuración de las ventanas de tiempo esperadas, la pantalla solicita los campos `Tiempo mínimo (minutos)` y `Tiempo máximo (minutos)` para cada tramo entre checkpoints. Dos de los tres participantes del Segmento 1 estimaron la duración de los tramos en horas, que es la unidad con la que planifican sus itinerarios, y tuvieron que realizar la conversión mentalmente antes de completar el formulario. Uno de ellos manifestó además que la magnitud resultante le resultaba poco natural para describir un tramo de caminata, y otro indicó que un administrador sin experiencia de campo difícilmente sabría qué valor ingresar. Ninguno de los dos cometió un error de conversión, pero ambos interrumpieron la tarea para calcular.

![Ventanas de tiempo esperadas de una ruta, con el rango de cada tramo expresado en minutos](../assets/images/chapter-5/validation/problema1.png)

**Recomendación:**

Expresar las ventanas de tiempo en horas y minutos mediante dos campos independientes, o permitir el ingreso en horas con conversión automática a minutos en la capa de persistencia, conservando el modelo actual del dominio. La corrección se registra en el Product Backlog como mejora de la User Story US09, Ventanas de tiempo esperadas.

**PROBLEMA #2:** El estado de borrador de una ruta no comunica la acción necesaria para habilitarla

**Severidad:** 3
**Heurística violada:** Usability: Visibilidad del estado del sistema

**Problema:**

Una ruta recién registrada permanece en estado `Borrador — Pendiente de puntos de control` y no puede utilizarse para crear grupos de expedición hasta que se pulse explícitamente el botón `Habilitar ruta`, ubicado en la pantalla de configuración de checkpoints. En la tarea de habilitación, un participante del Segmento 1 dio por terminada la configuración tras guardar los checkpoints y tuvo que releer la pantalla para localizar la acción pendiente. El sistema informa el estado, pero no señala con suficiente jerarquía cuál es el siguiente paso ni la consecuencia de omitirlo, que solo se descubre al intentar crear un grupo.

![Pantalla de puntos de control con la ruta en estado de borrador y el botón de habilitación](../assets/images/chapter-5/validation/problema2.png)

**Recomendación:**

Mostrar en el listado de rutas y en la pantalla de checkpoints un indicador de progreso con los requisitos pendientes de la ruta, y anticipar en la propia tarjeta de la ruta que los grupos de expedición no podrán crearse mientras no esté habilitada. La corrección se registra en el Product Backlog como mejora de las User Stories US07, Configuración de rutas, y US08, Definición de checkpoints.

**PROBLEMA #3:** El manifiesto de turistas no admite información de salud del participante

**Severidad:** 3
**Heurística violada:** Inclusive Design: Considera la situación

**Problema:**

En la tarea de registro del manifiesto, el guía de campo solo dispone de los campos `Nombre completo` y `Documento de identidad`, y la vista del manifiesto desde operaciones muestra únicamente el nombre, el dispositivo wearable asignado, el consentimiento y el estado de activación. Un participante del Segmento 1 buscó un campo donde consignar alergias o condiciones médicas, información que declaró recoger siempre antes de iniciar un recorrido, y manifestó que la registraría dentro del campo de nombre a falta de un espacio propio. El contacto de emergencia sí está contemplado, pero depende de que cada turista lo confirme desde su propia cuenta, de modo que el guía no tiene forma de completarlo cuando el participante no lo ha hecho. La omisión resulta especialmente relevante en el contexto de uso del producto, donde la atención de una emergencia en zona sin cobertura depende de la información que el guía lleve consigo.

![Manifiesto de turistas de un grupo de expedición, sin campos de información de salud](../assets/images/chapter-5/validation/problema3.png)

**Recomendación:**

Incorporar al manifiesto un campo opcional de condiciones médicas relevantes y permitir que el guía de campo registre el contacto de emergencia de un participante que no lo haya confirmado desde su cuenta, con el tratamiento de datos sensibles descrito en la sección de Safety & Privacy del Landing Page. La corrección se registra en el Product Backlog como mejora de las User Stories US12, Registro del manifiesto, y US14, Registro de contacto de emergencia.

**PROBLEMA #4:** La duración estimada de la ruta se solicita en horas

**Severidad:** 2
**Heurística violada:** Usability: Coincidencia entre el sistema y el mundo real

**Problema:**

En la tarea de registro de una ruta, el formulario solicita el campo `Duración estimada (horas)`. Un participante del Segmento 1 describió la duración de la ruta en días, que es la unidad con la que comercializa sus recorridos, y tuvo que convertirla a horas antes de continuar. El problema es de menor severidad que el anterior porque la conversión es directa y el campo se completa una sola vez por ruta, pero evidencia la misma distancia entre la unidad del sistema y la del dominio.

![Formulario de registro de ruta con el campo Duración estimada expresado en horas](../assets/images/chapter-5/validation/problema4.png)

**Recomendación:**

Permitir el ingreso de la duración en días y horas, o mostrar bajo el campo la equivalencia calculada en días a medida que se escribe. La corrección se registra en el Product Backlog como mejora de la User Story US07, Configuración de rutas.

**PROBLEMA #5:** La lista de guías de campo no permite distinguir entre guías homónimos

**Severidad:** 2
**Heurística violada:** Usability: Reconocimiento antes que recuerdo

**Problema:**

En la tarea de asignación de un guía a un grupo de expedición, el selector presenta únicamente el nombre de cada guía registrado. Un participante del Segmento 1, que declaró operar con quince guías, advirtió que no podría identificar con certeza a cuál está asignando si dos de ellos compartieran nombre, y señaló que en su propio sistema cada guía cuenta con un código. La tarea se completó sin error porque el conjunto de datos de la demostración es reducido, pero el riesgo se manifiesta al escalar la operación.

![Selector de asignación de guía de campo, que muestra únicamente el nombre](../assets/images/chapter-5/validation/problema5.png)

**Recomendación:**

Añadir al selector un identificador del guía, su documento de identidad parcialmente enmascarado o el número de grupos que ya tiene asignados en el periodo, de modo que la elección pueda verificarse sin salir de la pantalla. La corrección se registra en el Product Backlog como mejora de la User Story US13, Asignación del guía.

**PROBLEMA #6:** Registrar un guía de campo y crear su cuenta de acceso son dos acciones separadas

**Severidad:** 2
**Heurística violada:** Usability: Consistencia y estándares

**Problema:**

En la pantalla de cuentas y guías conviven dos formularios independientes: uno para registrar al guía de campo y otro para crear la cuenta de acceso que se vincula a ese guía. Un participante del Segmento 1 interpretó inicialmente que ambas acciones eran la misma y esperó que la creación de la cuenta diera de alta también al guía. Completó la tarea tras releer la pantalla, pero la relación entre las dos entidades no resulta evidente a primera vista.

![Pantalla de cuentas y guías con los formularios de creación de cuenta y de registro de guía separados](../assets/images/chapter-5/validation/problema6.png)

**Recomendación:**

Presentar ambos formularios como pasos consecutivos de un mismo flujo de alta de guía, o permitir crear la cuenta directamente desde el guía recién registrado mediante una acción contextual. La corrección se registra en el Product Backlog como mejora de la User Story US13, Asignación del guía.

## 5.4. Video About-the-Product

El Video About-the-Product presenta VitalTrek a los visitantes del Landing Page que desean conocer el modelo de negocio y las características principales de la solución, así como a los usuarios de las Web Applications que desean conocer cómo realizar las tareas soportadas por el producto. El video resume el problema de supervisión de grupos en zonas sin cobertura, la propuesta de valor de VitalTrek para agencias y turistas, y muestra escenas de interacción con el Landing Page y la Web Application. Incluye al menos una opinión de un participante de cada segmento objetivo obtenida en las entrevistas de validación. El tono es serio, cercano y sereno, consistente con el tono de comunicación definido en las Style Guidelines de la sección 4.1.1.

| Elemento | Información |
| --- | --- |
| Nombre del video | upc-pre-202620-1asi0730-16712-nexatech-about-the-product-sprint-3 |
| Duración | <!-- COMPLETAR: mm:ss --> |
| Microsoft Stream | [Ver video](https://upcedupe-my.sharepoint.com/:v:/g/personal/u202312566_upc_edu_pe/IQAjsBrslu3MR7By39Fu-BsFAfiB4yq24hk4wPA72_Q76yM?nav=eyJyZWZlcnJhbEluZm8iOnsicmVmZXJyYWxBcHAiOiJPbmVEcml2ZUZvckJ1c2luZXNzIiwicmVmZXJyYWxBcHBQbGF0Zm9ybSI6IldlYiIsInJlZmVycmFsTW9kZSI6InZpZXciLCJyZWZlcnJhbFZpZXciOiJNeUZpbGVzTGlua0NvcHkifX0&e=iGJMnP) |
| YouTube (incrustado en el Landing Page) | [Ver video](https://youtu.be/dLyAscgf9Uw) |

![Captura del Video About-the-Product](../assets/images/chapter-5/about-the-product.png)
<!-- COMPLETAR: captura representativa -->

*Figura 5.X. Video About-the-Product de VitalTrek.*

**Secuencia de contenido**

| Inicio (hh:mm:ss) | Sección | Contenido |
| --- | --- | --- |
| | Problema | Situación de las agencias y turistas cuando un grupo pierde la cobertura durante el recorrido. |
|  | Propuesta de valor | Presentación de VitalTrek: supervisión por checkpoints, telemetría offline y alertas. |
|  | Producto | Escenas de interacción con el Landing Page y la Web Application. |
|  | Testimonios | Opinión de un participante de cada segmento obtenida en las entrevistas de validación. |
|  | Call-To-Action | Invitación a solicitar una demostración o acceder a la aplicación. |
