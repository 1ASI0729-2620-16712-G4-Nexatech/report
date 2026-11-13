# Conclusiones

## Conclusiones y recomendaciones

### Conclusiones generales

1. Las entrevistas y los artefactos de Needfinding identifican la pérdida de conectividad, la dificultad para conocer el estado de los grupos y la preocupación por emergencias como problemas relevantes para los segmentos analizados. En ambos segmentos, la necesidad de monitoreo y los problemas de conectividad coincidieron en toda la muestra, y la privacidad de los datos apareció como condición de adopción para los turistas. Los resultados describen la muestra entrevistada y no representan por sí solos a todo el mercado.

2. El diseño de VitalTrek mantiene coherencia entre el problema y la solución propuesta: el wearable registra datos sin conexión, los checkpoints sincronizan la telemetría y la plataforma evalúa los datos recibidos para apoyar la supervisión operativa. Esta coherencia se conservó durante la implementación: la separación en bounded contexts definida en el diseño estratégico y táctico se reflejó en la estructura de carpetas del RESTful Web Services y en las capas `domain`, `application`, `infrastructure` y `presentation` de las Web Applications.

3. Al cierre del Sprint 3 (AV2), el RESTful Web Services se encuentra desplegado en Render con base de datos MySQL en Railway, y su documentación OpenAPI, publicada con Scalar, describe 41 endpoints de los contextos IAM y Expedition Setup. Los bounded contexts IAM, Expedition Setup, Field Tracking, Checkpoint Sync, Safety Monitoring, Incident Response y Tour Closure están implementados en el backend. Las Web Applications consumen el API para los flujos de autenticación y configuración de expediciones; los bounded contexts de Field Tracking, Safety Monitoring y Tour Closure quedan pendientes de integración en el frontend para la entrega final.

4. Las entrevistas de validación con tres dueños o responsables de agencias y tres turistas de aventura mostraron que los participantes pudieron completar los flujos principales del Landing Page y de las Web Applications, y que valoran el monitoreo por checkpoints frente a su práctica actual (protocolos en papel y hojas de cálculo). Todos los turistas indicaron que recomendarían o preferirían una agencia que use la solución. La evaluación heurística identificó seis problemas de usabilidad: tres de severidad 3 y tres de severidad 2, ninguno de severidad 4, es decir, ninguno impide completar las tareas evaluadas.

5. Los problemas detectados tienen un origen común: la interfaz usa unidades y flujos del modelo de dominio técnico (minutos, horas, formularios separados) en lugar del lenguaje operativo de las agencias (horas, días, un solo alta de guía). Esto confirma el valor de validar con usuarios reales aun cuando el producto cumpla sus criterios de aceptación, y orienta las mejoras prioritarias del Product Backlog: unidades de tiempo naturales, información de salud en el manifiesto, identificación de guías y claridad sobre el paso de habilitar una ruta.

6. La validación evaluó solo las tareas disponibles de extremo a extremo en las versiones desplegadas. El seguimiento en tiempo real, las alertas tempranas, la captura offline y sincronización de telemetría, la gestión de incidentes y el cierre del tour no fueron sometidos a evaluación. Por ello, las hipótesis de Lean UX sobre la utilidad del seguimiento en tiempo real y de la supervisión de alertas de seguridad aún no han podido contrastarse con usuarios reales. Los turistas pidieron ver su ubicación y el progreso por tramos, y una agencia pidió exportar el historial de cada grupo; ambas demandas deben considerarse al cerrar esas funcionalidades.

7. La aplicación de GitFlow, Pull Requests revisados, Conventional Commits y Semantic Versioning permitió mantener trazabilidad entre historias de usuario, ramas, commits y versiones publicadas (`v1.0.0` del RESTful Web Services y `v1.1.0` del Landing Page y las Web Applications). Todos los integrantes contribuyeron en los tres sprints y la carga estimada se mantuvo equilibrada: entre 105 y 115 horas por sprint, con diferencias moderadas entre integrantes.

8. Se recomienda, para la entrega final: (a) integrar en el frontend los bounded contexts de Field Tracking, Safety Monitoring, Incident Response y Tour Closure; (b) conectar el flujo de datos de los dispositivos wearable con el API; (c) incorporar al Product Backlog las correcciones de los seis problemas heurísticos, comenzando por los de severidad 3; (d) ampliar la validación con usuarios a las funcionalidades aún no evaluadas; y (e) evaluar un plan de hosting superior al plan Free de Render, cuyo arranque en frío puede afectar la experiencia de uso.

### Conclusiones del Sprint 1

1. El Sprint 1 cumplió su objetivo: se publicó la primera versión del Landing Page de VitalTrek, bilingüe (español e inglés), responsive y desplegada en Vercel, con las 11 historias comprometidas (US01 a US06, US33 y TS01 a TS04) y los 30 Story Points planificados.

2. La descomposición de las historias en 21 tasks de entre 4 y 8 horas (105 horas en total) y la matriz de líderes y colaboradores permitieron repartir el trabajo en paralelo y sin bloqueos, con una carga entre 17 y 28 horas por integrante.

3. Las decisiones de calidad se tomaron desde el inicio: tokens de estilo centralizados, adaptación a los anchos de 360, 768, 1024 y 1440 px, paridad de claves entre los idiomas, contraste según WCAG 2.1 AA, acceso directo al contenido principal, metadatos SEO y validación del marcado con el W3C. Esto dejó una base de interfaz y de identidad visual reutilizable en las Web Applications.

4. El Landing Page cumple su función de captación: presenta la propuesta de valor por segmento, los planes, el equipo, el formulario de solicitud de información y el tratamiento de datos personales. En la validación, todos los participantes comprendieron el monitoreo por checkpoints en zonas sin cobertura; las observaciones se limitaron a la falta de un formulario de contacto visible para uno de los participantes.

5. La retrospectiva identificó que la integración del trabajo se concentró al final del Sprint, lo que dificultó revisar los cambios con anticipación. Como acción de mejora, desde el Sprint 2 se adoptaron feature branches y Pull Requests revisados, y desde el 7 de septiembre de 2026 se aplican las convenciones de commits y de nombres de ramas.

### Conclusiones del Sprint 2

1. El Sprint 2 cumplió su objetivo para TB1: se entregó la primera versión de las Web Applications con Vue 3 y Vite, desplegada en Vercel, que cubre la preparación completa de una expedición (rutas, checkpoints, ventanas de tiempo esperadas, grupos, asignación de guía y manifiesto) y la consulta del progreso estimado. Se completaron las 7 historias comprometidas, equivalentes a 28 Story Points y 109 horas en 20 tasks.

2. El uso de una Fake API con json-server permitió desarrollar y validar la interfaz y las reglas de negocio (rechazo de nombres de ruta duplicados, órdenes de checkpoint repetidos, ventanas con límites inconsistentes, fechas pasadas, documentos duplicados y capacidad excedida) antes de contar con el backend, y redujo el riesgo de la integración posterior.

3. La arquitectura por capas (`domain`, `application`, `infrastructure` y `presentation`), junto con los assemblers y los stores de Pinia, aisló el acceso a datos del resto de la aplicación. Esta decisión permitió reemplazar la Fake API por el RESTful Web Services en el Sprint 3 sin rehacer las vistas.

4. El Sprint 2 incorporó la internacionalización con vue-i18n, la selección de espacio de trabajo según el rol (Operations Administrator y Field Guide) y mensajes de validación localizados. La retroalimentación de TB1 mostró que el Landing Page aún tenía aspectos de Responsive Web Design y de contenido por mejorar, y que debía evidenciarse la participación de todos los integrantes; ambos puntos se atendieron en el Sprint 3.

5. Como limitación, el seguimiento de progreso (US20) se apoyó en datos simulados y la aplicación no incluía autenticación real ni persistencia productiva. El dashboard sirvió para validar la presentación del tramo actual, del último checkpoint y de la antigüedad de la sincronización, pero no puede considerarse evidencia del funcionamiento con telemetría real.

### Conclusiones del Sprint 3

1. El Sprint 3 cumplió su objetivo: se implementó y desplegó el RESTful Web Services con ASP.NET Core 10, Entity Framework Core y MySQL, y se integró con las Web Applications ya publicadas. Se completaron las 13 historias comprometidas (TS06, TS07, TS09 y US07 a US16), equivalentes a 57 Story Points, el sprint de mayor alcance del proyecto, casi el doble de los anteriores.

2. El backend se organizó en bounded contexts con capas de dominio, aplicación, infraestructura e interfaces. Cada integrante asumió al menos un contexto completo (IAM y Expedition Setup, Safety Monitoring, Incident Response, Tour Closure y Checkpoint Sync), con fachadas ACL entre contextos y migraciones versionadas, lo que dejó evidencia individual verificable y una base preparada para integrar la telemetría de los wearables.

3. La seguridad se resolvió desde el inicio: contraseñas cifradas con BCrypt, tokens JWT firmados con HS256, autorización por rol y por agencia, y aislamiento de los datos de cada agencia en todas las consultas. Las credenciales se retiraron de los archivos versionados y se gestionan mediante variables de entorno en Render.

4. La documentación con OpenAPI y Scalar, con respuestas estandarizadas (`201`, `400`, `401`, `403`, `404` y `409`) y descripciones localizadas, permitió probar el servicio desplegado desde el navegador y facilita su consumo por las Web Applications y por futuros clientes.

5. El despliegue con Docker en Render, MySQL administrado en Railway y Vercel para el frontend, con migraciones y datos de demostración aplicados al iniciar, permitió publicar tres productos versionados con GitFlow y Semantic Versioning. La integración del frontend se limitó a IAM y Expedition Setup; el seguimiento en campo, la sincronización de checkpoints, las alertas, los incidentes y el cierre del tour se muestran como funcionalidades de un próximo sprint.

6. Las entrevistas de validación, realizadas sobre las versiones desplegadas, aportaron los primeros hallazgos con usuarios reales. Validaron el flujo de configuración de expediciones y el registro de la preparación del turista, y revelaron mejoras de usabilidad sobre funcionalidades ya entregadas en los sprints anteriores, que se incorporan al Product Backlog para la entrega final.