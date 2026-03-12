# Estructura de datos del caso

## Principio general

La unidad principal del CRM es el **caso**.

Cada caso representa un expediente operativo desde el primer contacto hasta el cierre, incluyendo:

- lead inicial
- cualificación
- comunicaciones
- seguimiento
- documentación
- presupuesto o factura
- informe enviado
- cierre

## Reglas clave

### 1. El caso tiene identificador propio
El identificador interno será `case_id`.

Formato propuesto:

`AP-AAAA-NNNNNN`

Ejemplo:

`AP-2026-000001`

### 2. El teléfono identifica al contacto
El teléfono es una clave fuerte del contacto, pero no una clave única del caso.

Esto evita problemas cuando:

- un mismo cliente abre varios asuntos
- un abogado trae varios casos
- se escribe desde el teléfono de otra persona
- cambia el número del cliente

### 3. El caso contiene timeline
Toda interacción relevante debe quedar registrada en el histórico del caso.

## Campos principales del caso

### Metadatos
- `case_id`
- `created_at`
- `updated_at`

### Estado
- `status_pipeline`
- `qualification_status`
- `close_reason`

### Origen
- `source.channel`
- `source.campaign`
- `source.form_name`
- `source.lead_id`

### Contacto
- `contact.name`
- `contact.phone_e164`
- `contact.phone_raw`
- `contact.email`
- `contact.province`
- `contact.role`

### Vehículo
- `vehicle.plate`
- `vehicle.make`
- `vehicle.model`
- `vehicle.version`
- `vehicle.vin`
- `vehicle.km`

### Resumen jurídico/comercial preliminar
- `case_summary.seller_type`
- `case_summary.purchase_date`
- `case_summary.problem_summary`
- `case_summary.claim_goal`
- `case_summary.urgency_level`

### Timeline
Lista ordenada de eventos del caso.

### Tasks
Tareas abiertas o cerradas asociadas al caso.

### Documents
Metadatos de documentos subidos o generados.

## Estados operativos propuestos

### `status_pipeline`
- `nuevo`
- `pendiente_revision`
- `pendiente_documentacion`
- `precalificado`
- `descartado`
- `llamada_programada`
- `presupuesto_enviado`
- `aceptado`
- `peritacion_agendada`
- `peritacion_realizada`
- `informe_en_redaccion`
- `informe_enviado`
- `facturado`
- `pagado`
- `cerrado_ganado`
- `cerrado_perdido`

### `qualification_status`
- `sin_revisar`
- `apto`
- `dudoso`
- `no_apto`

## Ejemplo resumido

Ver ejemplo completo en:

- `crm/examples/caso_ejemplo.json`
