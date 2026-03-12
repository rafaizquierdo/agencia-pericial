# Tecnología y automatización

Esta carpeta documenta la arquitectura técnica del proyecto **Agencia Pericial** en su versión CRM propia, alojada en **IONOS** bajo el subdominio:

`ap-crm.rafaizquierdo.es`

## Objetivo de esta carpeta

Dejar definida la base técnica antes de escribir código, para que el desarrollo del CRM no dependa de decisiones improvisadas.

Aquí se documenta:

- la arquitectura general del CRM
- la estructura de carpetas en IONOS
- el modelo de datos del caso
- los flujos de automatización previstos
- los endpoints PHP que se implementarán
- las reglas de seguridad y gestión de secretos
- el orden recomendado de implementación

## Principios de diseño

1. **Frontend simple, backend controlado**  
   La interfaz será una web HTML/JS ligera y responsive. Toda modificación de datos pasará por endpoints PHP.

2. **JSON privado, no público**  
   El navegador nunca editará archivos JSON directamente. Los datos vivirán en una carpeta protegida por `.htaccess`.

3. **Un caso = un archivo JSON**  
   No se usará un único `cases.json` gigante. Cada caso tendrá su propio archivo y existirán índices auxiliares.

4. **El teléfono identifica al contacto, no necesariamente al caso**  
   Un mismo teléfono puede estar asociado a varios casos. El identificador del caso será un `case_id` interno.

5. **Integraciones desacopladas**  
   Meta, Zapier, WhatsApp y agentes OpenClaw hablarán con la API del CRM, no con los archivos internos.

6. **Nada sensible al repositorio público**  
   Esta carpeta documenta estructura y contratos técnicos. No incluirá secretos ni código listo para producción.

## Estructura documental

- `arquitectura.md`: visión de conjunto
- `estructura_datos_caso.md`: definición del dato maestro
- `flujos_automatizacion.md`: recorrido del lead y del caso
- `crm/README.md`: módulo CRM
- `crm/arquitectura_ionos.md`: estructura concreta de despliegue en IONOS
- `crm/modelo_datos.md`: entidades y relaciones
- `crm/api_endpoints.md`: endpoints previstos
- `crm/seguridad_y_secretos.md`: reglas de protección y despliegue
- `crm/despliegue_y_operacion.md`: guía operativa y backups
- `crm/roadmap_implementacion.md`: orden de ejecución
- `crm/examples/`: ejemplos de payloads y esquemas

## Alcance de esta documentación

Esta documentación **no implementa**:

- autenticación real
- endpoints PHP definitivos
- UI final del CRM
- sincronización real con Meta
- subida real de documentos
- automatizaciones de OpenClaw

Su función es fijar el mapa antes de empezar a construir.
