# 5. Product Implementation, Validation & Deployment

### 5.1. Software Configuration Management

Esta sección establece las herramientas, configuraciones y convenciones utilizadas para mantener la consistencia del proyecto VitalTrek durante el Sprint 1. Se documentan el entorno de desarrollo, el control de versiones, las reglas de estilo y la configuración de despliegue del Landing Page. Estas decisiones permiten coordinar el trabajo del equipo, mantener trazabilidad sobre los cambios y asegurar que la solución pueda ejecutarse y publicarse de forma consistente.

### 5.1.1. Software Development Environment Configuration

La siguiente tabla presenta las herramientas utilizadas por el equipo durante el desarrollo del Sprint 1 y la elaboración de los artefactos correspondientes a AV1.

| Producto           | Actividad                | Propósito                                                            | Referencia                                           |
| ------------------ | ------------------------ | -------------------------------------------------------------------- | ---------------------------------------------------- |
| Jira Software      | Project Management       | Gestionar el Product Backlog, Sprint Backlog, tareas y Story Points. | [Jira](https://www.atlassian.com/software/jira)      |
| GitHub             | Source Code Management   | Almacenar el código, aplicar GitFlow y registrar commits.            | [GitHub](https://github.com/)                        |
| Figma              | UX/UI Design             | Elaborar wireframes, mock-ups y prototipos.                          | [Figma](https://www.figma.com/)                      |
| UXPressia          | Requirements / UX Design | Elaborar User Personas, Journey Maps, Empathy Maps e Impact Maps.    | [UXPressia](https://uxpressia.com/)                  |
| Miro               | Domain Modeling          | Elaborar el Big Picture y Design-Level EventStorming.                | [Miro](https://miro.com/)                            |
| Visual Studio Code | Software Development     | Desarrollar el Landing Page con HTML5, CSS3 y JavaScript.            | [Visual Studio Code](https://code.visualstudio.com/) |
| Vercel             | Software Deployment      | Desplegar y publicar la primera versión del Landing Page.            | [Vercel](https://vercel.com/)                        |
| Markdown           | Software Documentation   | Redactar el informe del proyecto y organizar sus capítulos.          | [Markdown Guide](https://www.markdownguide.org/)     |

### 5.1.2. Source Code Management

El código fuente de VitalTrek se administra mediante Git y GitHub. Cada producto mantiene su propio repositorio para separar responsabilidades y facilitar el trabajo colaborativo. Para controlar la evolución del proyecto se utiliza GitFlow, Conventional Commits y Semantic Versioning.

| Producto                  | Repositorio                                                     | Estado en AV1             |
| ------------------------- | --------------------------------------------------------------- | ------------------------- |
| Landing Page              | https://github.com/1ASI0729-2620-16712-G4-Nexatech/landing-page | Implementado y desplegado |
| Frontend Web Applications | URL pendiente                                                   | Planificado               |
| RESTful Web Services      | URL pendiente                                                   | Planificado               |

#### GitFlow Workflow

El flujo de trabajo utiliza las siguientes ramas:

- `main`: versión estable y publicada.
- `develop`: integración de cambios aprobados.
- `feature/*`: desarrollo de funcionalidades.
- `release/*`: preparación de una versión.
- `hotfix/*`: corrección urgente sobre `main`.

Para el Sprint 1 se utiliza la rama:

```text
feature/landing-page-av1
```

### 5.1.3. Source Code Style Guide & Conventions

El equipo utiliza convenciones comunes para mantener un código legible, consistente y fácil de mantener. Todos los nombres de archivos, variables, funciones, clases, identificadores HTML y componentes se redactan en inglés.

| Tecnología | Convenciones principales                                                                                                                           |
| ---------- | -------------------------------------------------------------------------------------------------------------------------------------------------- |
| HTML5      | Elementos semánticos, etiquetas en minúscula, atributos entre comillas dobles y textos alternativos en imágenes.                                   |
| CSS3       | Clases e identificadores en `kebab-case`, variables CSS centralizadas y diseño mobile-first.                                                       |
| JavaScript | Variables y funciones en `camelCase`, constantes en `UPPER_SNAKE_CASE`, uso de `const` y `let`, y funciones con responsabilidades específicas.     |
| Markdown   | Encabezados jerárquicos, enlaces relativos, imágenes con texto alternativo y tablas con formato consistente.                                       |
| Vue.js     | Componentes en `PascalCase`, propiedades y eventos con nombres descriptivos. Aplicación planificada para entregas posteriores.                     |
| C#         | Clases, métodos y propiedades en `PascalCase`; parámetros y variables locales en `camelCase`. Aplicación planificada para el RESTful Web Services. |

Ejemplos:

```html
<section class="safety-features">
  <img src="./assets/checkpoint-icon.svg" alt="Checkpoint synchronization">
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

function toggleLanguage(selectedLocale) {
  document.documentElement.lang = selectedLocale;
}
```

### 5.1.4. Software Deployment Configuration

La primera versión desplegada de VitalTrek corresponde al Landing Page desarrollado con HTML5, CSS3 y JavaScript. La publicación se realiza desde GitHub hacia Vercel, permitiendo disponer de una versión accesible para la revisión de AV1.

| Producto                  | Plataforma | Rama      | Estado      |
| ------------------------- | ---------- | --------- | ----------- |
| Landing Page              | Vercel     | `main`    | Desplegado  |
| Frontend Web Applications | Pendiente  | Pendiente | Planificado |
| RESTful Web Services      | Pendiente  | Pendiente | Planificado |

#### Configuración del Landing Page

- Repositorio: https://github.com/1ASI0729-2620-16712-G4-Nexatech/landing-page
- Plataforma: https://landing-page-mrca1.vercel.app/
- Rama desplegada: `main`
- Framework: Static HTML/CSS/JavaScript
- Build command: No aplica
- Output directory: Directorio raíz del repositorio
- Variables de entorno: No requeridas

#### Proceso de despliegue

1. Se actualiza el código en la rama `develop`.
2. Se validan los cambios del Landing Page.
3. Se integra la versión aprobada en `main`.
4. Vercel detecta el cambio en el repositorio.
5. Se ejecuta el despliegue automático.
6. Se verifica la navegación, el diseño responsive, los enlaces y los call-to-action.

### 5.2. Landing Page, Services & Applications Implementation

Esta sección documenta la implementación, validación y despliegue de los productos incluidos en la solución VitalTrek. Para AV1, el alcance se concentra en la primera versión funcional y desplegada del Landing Page, desarrollado con HTML5, CSS3 y JavaScript. Las Web Applications y el RESTful Web Services quedan planificados para los siguientes Sprints.

#### 5.2.1. Sprint 1

### Sprint 1

El Sprint 1 tiene como objetivo implementar y publicar la primera versión del Landing Page de VitalTrek. El alcance comprende las User Stories US01 a US06, relacionadas con la navegación principal, la propuesta de valor, los planes, la información del equipo, el formulario de contacto y el cambio de idioma. La estimación total del Sprint es de 14 Story Points.

### 5.2.1.1. Sprint Planning 1

La reunión de planificación permitió definir el objetivo, alcance, responsabilidades y tareas del primer Sprint. El trabajo se enfocó en entregar un Landing Page responsive, accesible y coherente con los wireframes, mock-ups, Style Guidelines e Information Architecture definidos en el capítulo IV.

| Campo                 | Información                                                                                                                                                 |
| --------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Sprint                | Sprint 1                                                                                                                                                    |
| Fecha                 | 2026-09-05                                                                                                                                                  |
| Hora                  | 20:00                                                                                                                                                       |
| Ubicación             | Discord — reunión virtual                                                                                                                                   |
| Preparado por         | Rodriguez Rojas, Miler Alexander                                                                                                                            |
| Participantes         | Cayanchi Avila, Milenko Rubén; León Naupari, Jorge Mateo; Mendoza Blanco, Ariel Roberto; Rodriguez Rojas, Miler Alexander; Herrera Enriquez, Diego Fernando |
| Sprint Goal           | Implementar y desplegar la primera versión funcional del Landing Page de VitalTrek.                                                                         |
| Sprint Velocity       | 14 Story Points                                                                                                                                             |
| Total de Story Points | 14                                                                                                                                                          |

**Sprint Goal**

Nuestro enfoque está en comunicar la propuesta de valor de VitalTrek mediante un Landing Page responsive con navegación, información del producto, planes, equipo, contacto y soporte bilingüe. Consideramos que esto permitirá a los visitantes comprender la solución y solicitar una demostración. El cumplimiento se confirmará cuando el Landing Page esté publicado y sus User Stories principales puedan ser recorridas correctamente.

### 5.2.1.2. Aspect Leaders and Collaborators

La siguiente matriz organiza el liderazgo y la colaboración del equipo durante el Sprint 1. La asignación debe coincidir con las tareas registradas en el Sprint Backlog y con la evidencia de commits.

| Integrante                       | Usuario de GitHub | Landing Page structure | Responsive UI | i18n y a11y | QA y deployment | Documentación |
| -------------------------------- | ----------------- | ---------------------- | ------------- | ----------- | --------------- | ------------- |
| Cayanchi Avila, Milenko Rubén    | `MaxghZZ`         | L                      | C             | C           | C               | L             |
| León Naupari, Jorge Mateo        | `mateool10`       | C                      | L             | C           | C               | C             |
| Mendoza Blanco, Ariel Roberto    | `Trepequiper`     | C                      | C             | L           | C               | C             |
| Rodriguez Rojas, Miler Alexander | `Miler2003`       | C                      | C             | C           | L               | L             |
| Herrera Enriquez, Diego Fernando | `DerDFHE`         | C                      | C             | C           | C               | C             |

### 5.2.1.3. Sprint Backlog 1

El Sprint Backlog contiene las seis User Stories del Landing Page seleccionadas desde el Product Backlog. Las tareas se descomponen en actividades de estructura HTML, estilos responsive, contenido, internacionalización, accesibilidad, validación y despliegue.

**Evidencia del board**

![Product Backlog de VitalTrek en Jira](../assets/images/chapter-3/product-backlog-jira.png)

*Figura 5.1. Sprint Backlog del Sprint 1.*

**Adjuntar enlace público del board Jira/Trello:** [Pegar enlace]

| User Story | Tarea | Descripción                                                           | Estimación (horas) | Responsable                      | Estado |
| ---------- | ----- | --------------------------------------------------------------------- | -----------------: | -------------------------------- | ------ |
| US01       | LP-01 | Implementar header, navegación y enlaces a las secciones principales. |                  4 | Cayanchi Avila, Milenko Rubén    | Done   |
| US02       | LP-02 | Implementar Hero, propuesta de valor y beneficios principales.        |                  6 | León Naupari, Jorge Mateo        | Done   |
| US03       | LP-03 | Implementar sección de planes y características.                      |                  5 | Rodriguez Rojas, Miler Alexander | Done   |
| US04       | LP-04 | Implementar sección de equipo y perfiles de Nexum Devs.               |                  4 | Herrera Enriquez, Diego Fernando | Done   |
| US05       | LP-05 | Implementar formulario de contacto y validaciones básicas.            |                  5 | Mendoza Blanco, Ariel Roberto    | Done   |
| US06       | LP-06 | Implementar cambio de idioma entre en-US y es-419.                    |                  6 | Mendoza Blanco, Ariel Roberto    | Done   |
| US01–US06  | LP-07 | Aplicar responsive design para desktop, tablet y mobile.              |                  8 | León Naupari, Jorge Mateo        | Done   |
| US01–US06  | LP-08 | Validar navegación, accesibilidad y enlaces del Landing Page.         |                  4 | Herrera Enriquez, Diego Fernando | Done   |
| US01–US06  | LP-09 | Configurar y verificar el despliegue público.                         |                  2 | Rodriguez Rojas, Miler Alexander | Done   |
### 5.2.1.4. Development Evidence for Sprint Review

Durante el Sprint 1 se implementaron los componentes correspondientes al Landing Page. La evidencia debe relacionar cada cambio con su repositorio, rama, commit y fecha de realización.

| Repositorio                                                                     | Rama   | Commit ID | Mensaje del commit                | Fecha      | User Story relacionada |
| ------------------------------------------------------------------------------- | ------ | --------- | --------------------------------- | ---------- | ---------------------- |
| [Landing Page](https://github.com/1ASI0729-2620-16712-G4-Nexatech/landing-page) | `feature/landing-seo-a11y` | `2cebb2f` | `docs(readme): fix brand asset file extensions` | 2026-09-17 | US01–US06              |
| [Landing Page](https://github.com/1ASI0729-2620-16712-G4-Nexatech/landing-page) | `feature/landing-seo-a11y` | `d216d5e` | `feat(a11y): add skip to main content link` | 2026-09-17 | US01–US06              |
| [Landing Page](https://github.com/1ASI0729-2620-16712-G4-Nexatech/landing-page) | `feature/landing-seo-a11y` | `9252476` | `feat(seo): complete meta tags defined in report 4.2.3` | 2026-09-17 | US01–US06              |
| [Landing Page](https://github.com/1ASI0729-2620-16712-G4-Nexatech/landing-page) | `feature/landing-seo-a11y` | `b296ddc` | `feat(i18n): add skip link translation keys` | 2026-09-17 | US01–US06              |
| [Landing Page](https://github.com/1ASI0729-2620-16712-G4-Nexatech/landing-page) | `feature/landing-seo-a11y` | `36b333b` | `style(a11y): add skip link styles` | 2026-09-17 | US01–US06              |
| [Landing Page](https://github.com/1ASI0729-2620-16712-G4-Nexatech/landing-page) | `main` | `11ac9e2` | `chore(team): fix Team Member`    | 2026-09-17 | US04                   |
| [Landing Page](https://github.com/1ASI0729-2620-16712-G4-Nexatech/landing-page) | `main` | `645afa1` | `chore(team): add Team Member`    | 2026-09-17 | US04                   |
| [Landing Page](https://github.com/1ASI0729-2620-16712-G4-Nexatech/landing-page) | `main` | `9a91594` | `2da version landing page`        | 2026-09-12 | US01–US06              |
| [Landing Page](https://github.com/1ASI0729-2620-16712-G4-Nexatech/landing-page) | `main` | `117ad46` | `docs: add project documentation` | 2026-09-08 | Documentación          |
| [Landing Page](https://github.com/1ASI0729-2620-16712-G4-Nexatech/landing-page) | `main` | `935e346` | `docs: add project documentation` | 2026-09-08 | Documentación          |
| [Landing Page](https://github.com/1ASI0729-2620-16712-G4-Nexatech/landing-page) | `main` | `869b9db` | `Initial commit`                  | 2026-08-30 | Configuración inicial  |

![Commits del Sprint 1](../assets/images/chapter-5/development-commits.png)

*Figura 5.2. Commits relacionados con la implementación del Landing Page durante el Sprint 1.*

### 5.2.1.5. Execution Evidence for Sprint Review

La ejecución del Sprint produjo una primera versión funcional del Landing Page. La página presenta la propuesta de valor de VitalTrek, explica el problema de monitoreo en rutas remotas, muestra el funcionamiento por checkpoints, diferencia los beneficios para operadores y turistas, presenta las funcionalidades, planes, equipo, preguntas frecuentes y formulario de contacto.

![Landing Page desktop](../assets\images\chapter-4\mockups\hero-metrics.png)

*Figura 5.3. Vista desktop del Landing Page implementado.*

![Secciones principales del Landing Page](../assets/images/chapter-5/landing-page-sections.png)

*Figura 5.4. Secciones principales implementadas en el Sprint 1.*

La validación visual debe comprobar la navegación entre secciones, el comportamiento responsive, el cambio de idioma, los call-to-action, el formulario de contacto y la legibilidad del contenido.

**Adjuntar enlace del video de navegación del Landing Page:** [Pegar enlace de Microsoft Stream]

### 5.2.1.6. Services Documentation Evidence for Sprint Review

El alcance del Sprint 1 se limita al Landing Page estático desarrollado con HTML5, CSS3 y JavaScript. No se implementaron endpoints RESTful ni una API en este Sprint; por ello, la documentación OpenAPI y Swagger no aplican a esta entrega. La implementación de Web Services se planifica para una entrega posterior.

| Producto             | Endpoint              | Método HTTP | Estado      |
| -------------------- | --------------------- | ----------- | ----------- |
| RESTful Web Services | No aplica en Sprint 1 | No aplica   | Planificado |

### 5.2.1.7. Software Deployment Evidence for Sprint Review

La primera versión del Landing Page se publica desde el repositorio de GitHub hacia la plataforma de despliegue configurada. La rama estable utilizada y la URL pública deben corresponder con la versión revisada durante el Sprint Review.

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

**Adjuntar enlace del Landing Page desplegado:** [Pegar URL pública]

### 5.2.1.8. Team Collaboration Insights during Sprint

El trabajo colaborativo del Sprint 1 se realizó mediante GitHub, Jira/Trello y herramientas de diseño. Cada integrante participó en actividades de planificación, diseño, implementación, validación o documentación. La evidencia debe mostrar que los aportes registrados corresponden a los integrantes y tareas indicados en el Sprint Backlog.

![GitHub Insights del Sprint 1](../assets/images/chapter-5/github-insights.png)

*Figura 5.7. Analítica de colaboración del repositorio durante el Sprint 1.*

![Participación mediante commits](../assets/images/chapter-5/team-commits.png)

*Figura 5.8. Participación de los integrantes mediante commits.*

| Integrante                       | Actividad realizada     | Evidencia                 |
| -------------------------------- | ----------------------- | ------------------------- |
| Cayanchi Avila, Milenko Rubén    | [Describir aporte real] | [Commit, tarea o captura] |
| León Naupari, Jorge Mateo        | Modelado del Ubiquitous Language, User Task Matrix, diagramas C4 de contexto y contenedores, Design-Level Event Storming (4.6.1) y, en el Landing Page, meta tags de SEO, skip link de accesibilidad e i18n asociado. | 16 commits en report y 6 en landing-page; PRs #13, #15, #20 y #24 (report) y PR #2 (landing-page). Figuras 5.9, 5.10 y 5.11. |
| Mendoza Blanco, Ariel Roberto    | [Describir aporte real] | [Commit, tarea o captura] |
| Rodriguez Rojas, Miler Alexander | [Describir aporte real] | [Commit, tarea o captura] |
| Herrera Enriquez, Diego Fernando | [Describir aporte real] | [Commit, tarea o captura] |

La colaboración debe reflejarse de forma coherente en el Sprint Backlog, los commits, la matriz de líderes y colaboradores, y el reporte de participación individual.

**Evidencia individual - León Naupari, Jorge Mateo (mateool10)**

Los siguientes registros corresponden a la participación verificable del integrante en los repositorios del equipo durante el Sprint 1.

![Commits de mateool10 en el repositorio report](../assets/images/chapter-5/5218-commits-mateo-report.jpg)

*Figura 5.9. Historial de commits de mateool10 en el repositorio report.*

![Commits de mateool10 en el repositorio landing-page](../assets/images/chapter-5/5218-commits-mateo-landing.jpg)

*Figura 5.10. Historial de commits de mateool10 en el repositorio landing-page (rama main).*

![Pull requests creados por mateool10](../assets/images/chapter-5/5218-pull-requests-mateo.jpg)

*Figura 5.11. Pull requests creados y fusionados por mateool10 en el repositorio report.*
