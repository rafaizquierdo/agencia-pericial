# Modelo de datos del CRM

## Enfoque

Se adopta un modelo de datos orientado a expediente.

Cada caso contiene:

- metadatos
- contacto
- vehículo
- resumen del problema
- timeline
- tareas
- documentos

## Entidades lógicas

### Contacto
Persona o entidad que inicia o representa el caso.

Campos típicos:

- nombre
- teléfono normalizado
- teléfono en bruto
- email
- provincia
- rol

### Caso
Unidad operativa principal.

Campos típicos:

- `case_id`
- estado
- cualificación
- origen
- resumen
- fechas
- arrays asociados

### Evento
Registro cronológico de una acción o hecho.

Campos típicos:

- `event_id`
- `type`
- `channel`
- `created_at`
- `created_by`
- `text`
- `payload`

### Tarea
Acción pendiente o completada vinculada al caso.

Campos típicos:

- `task_id`
- `title`
- `due_at`
- `priority`
- `status`
- `assigned_to`

### Documento
Metadato de archivo vinculado al caso.

Campos típicos:

- `document_id`
- `document_type`
- `filename`
- `path`
- `uploaded_at`
- `uploaded_by`

## Índices auxiliares

Para búsqueda rápida se mantendrán índices JSON externos al caso:

### `contacts_by_phone.json`
Mapa de teléfono a uno o varios `case_id`.

### `cases_by_status.json`
Mapa de estado a lista de casos.

### `cases_by_plate.json`
Mapa de matrícula a lista de casos.

### `meta_leads_processed.json`
Control de `lead_id` ya consumidos para evitar duplicados.

## Criterios de diseño

- el caso es autosuficiente
- los índices aceleran búsquedas, pero no son la fuente maestra
- el timeline es obligatorio
- no se pisan eventos antiguos; se añaden nuevos
- las tareas y documentos siempre van ligados a un caso
