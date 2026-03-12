# Roadmap de implementación

## Fase 0 — documentación
Objetivo: fijar arquitectura y contratos antes del código.

Entregables:

- estructura documental
- arquitectura IONOS
- modelo de datos
- endpoints previstos
- reglas de seguridad

## Fase 1 — backend mínimo
Objetivo: disponer de API básica y almacenamiento JSON operativo.

Entregables:

- `bootstrap.php`
- `get_cases.php`
- `get_case.php`
- `save_meta_lead.php`
- `add_event.php`
- estructura `storage/`

## Fase 2 — frontend mínimo
Objetivo: interfaz usable desde móvil y escritorio.

Entregables:

- `crm.html`
- listado de casos
- filtros básicos
- ficha de caso
- timeline

## Fase 3 — seguridad mínima usable
Objetivo: no dejar la casa abierta.

Entregables:

- `.htaccess`
- almacenamiento bloqueado
- token para integraciones
- login simple
- logs básicos

## Fase 4 — integración Meta/Zapier
Objetivo: entrada automática de leads filtrados.

Entregables:

- webhook o endpoint operativo
- deduplicación por `lead_id`
- creación automática de caso
- trazabilidad en timeline

## Fase 5 — operaciones avanzadas
Objetivo: convertir el CRM en sistema de trabajo real.

Entregables:

- documentos
- tareas
- recontactos
- estados más finos
- automatizaciones con OpenClaw
