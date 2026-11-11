# Conclusiones

## Conclusiones y recomendaciones

1. Las entrevistas y los artefactos de Needfinding identifican la pérdida de conectividad, la dificultad para conocer el estado de los grupos y la preocupación por emergencias como problemas relevantes para los segmentos analizados. Los resultados describen la muestra entrevistada y no representan por sí solos a todo el mercado.

2. El diseño de VitalTrek mantiene coherencia entre el problema y la solución propuesta: el wearable registra datos sin conexión, los checkpoints sincronizan la telemetría y la plataforma evalúa los datos recibidos para apoyar la supervisión operativa.

3. Al cierre del Sprint 3 (AV2), el RESTful Web Services se encuentra desplegado en Render con base de datos MySQL en Railway, exponiendo 41 endpoints documentados con OpenAPI y Scalar. Los bounded contexts IAM, Expedition Setup, Field Tracking, Checkpoint Sync, Safety Monitoring, Incident Response y Tour Closure están implementados en el backend. Las Web Applications consumen el API para los flujos de autenticación y configuración de expediciones; los bounded contexts de Field Tracking, Safety Monitoring y Tour Closure quedan pendientes de integración en el frontend para la entrega final.

4. Las hipótesis de Lean UX sobre la utilidad del seguimiento en tiempo real y la supervisión de alertas de seguridad no han podido contrastarse aún con usuarios reales, dado que las entrevistas de validación están pendientes. La siguiente etapa debe completar las entrevistas de validación con representantes de los dos segmentos, integrar los bounded contexts restantes en el frontend y conectar el flujo de datos de los dispositivos wearable con la API.

## Video About-the-Team

<!-- COMPLETAR: descripción del contenido del Video About-the-Team, pauta de secuencias con timings (hh:mm:ss) por sección, cuadro de video representativo, URL de Microsoft Stream y URL de YouTube. -->
