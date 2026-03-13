# Flujos de automatización — campaña Meta v1

## Objetivo
Definir cómo entra un lead desde Meta hasta quedar registrado y operativo dentro del CRM.

## Flujo principal
### 1. Captación
- el usuario ve el anuncio en Meta
- abre el formulario instantáneo
- completa y envía el formulario

### 2. Tránsito de datos
- Meta entrega el lead a Zapier
- Zapier normaliza el payload
- Zapier hace `POST` a `https://ap-crm.rafaizquierdo.es/api/save_meta_lead.php`

### 3. Ingesta en CRM
El endpoint:
- valida token
- valida estructura mínima
- revisa `lead_id`
- evita duplicados
- crea caso nuevo o vincula al existente
- registra evento `meta_form_submitted`
- deja el caso en estado inicial `nuevo`

### 4. Revisión humana
- se revisa el lead en CRM
- se decide:
  - apto para llamada
  - pedir más información
  - descartar

### 5. Llamada y venta
- si encaja, se llama
- se completa información económica
- se registra resultado
- se oferta
- se deja seguimiento o cierre

## Payload lógico esperado desde Zapier
```json
{
  "source": {
    "channel": "meta_lead_form",
    "campaign": "AP | Leads | Vicios ocultos | ES | Form v1",
    "adset": "ES | Broad | 25-65 | Form v1",
    "ad_name": "Ad 1 | Dolor | Avería tras compra",
    "form_name": "AP | Vicios ocultos | Filtro inicial v1",
    "lead_id": "1234567890"
  },
  "contact": {
    "name": "Juan Prueba",
    "phone": "600111222",
    "email": "juan@test.com",
    "province": "Madrid"
  },
  "case_summary": {
    "purchase_window": "menos_30_dias",
    "seller_type": "profesional",
    "problem_type": "motor",
    "vehicle_usable": "usable_con_fallos",
    "problem_summary": "testigo motor y tirones a la semana"
  }
}
```

## Campos del formulario que entran al CRM
- nombre
- teléfono
- email
- provincia
- rango de antigüedad de compra
- tipo de vendedor
- tipo de problema
- estado de uso del vehículo
- resumen del problema

## Campos que NO llegan del formulario y deben completarse después
- matrícula
- documentación disponible
- precio de compra del vehículo
- cuantía estimada a reclamar
- fecha exacta de aparición del fallo
- diagnosis/presupuesto de taller detallado
- objetivo económico del cliente
- precio ofertado

## Eventos de timeline mínimos
- `meta_form_submitted`
- `lead_reviewed`
- `call_attempted`
- `call_completed`
- `documentation_requested`
- `documentation_received`
- `quote_sent`
- `lead_discarded`

## Reglas de deduplicación
### Duplicado fuerte
Si entra el mismo `lead_id`, no crear caso nuevo.

### Duplicado probable
Si cambia `lead_id` pero coincide teléfono:
- revisar si es el mismo caso
- si lo es, añadir evento
- si no lo es, crear caso nuevo vinculado al mismo contacto

## Errores que deben dejar traza
- token inválido
- payload mal formado
- lead sin teléfono
- escritura fallida
- índice inconsistente
- lead duplicado

## Estado inicial recomendado
- `nuevo`

## Estado tras primera revisión
- `pendiente_revision`
- `pendiente_documentacion`
- `precalificado`
- `descartado`

## Principio operativo
El CRM es la fuente operativa de verdad.
Ni Meta ni Zapier son el sistema de trabajo; solo son canales de entrada.
