# Endpoints previstos

## Objetivo
Definir la API interna del CRM antes de implementarla.

Todos los endpoints devolverán JSON.

## Convenciones
- método HTTP claro por responsabilidad
- validación de token o sesión
- respuestas consistentes
- errores con mensaje entendible
- logs de operación

## Endpoints mínimos v1

### `GET /api/get_cases.php`
Devuelve listado resumido de casos con filtros básicos.

Filtros previstos:
- estado
- provincia
- fecha
- teléfono
- matrícula
- texto libre

### `GET /api/get_case.php`
Devuelve el detalle completo de un caso.

Parámetros previstos:
- `case_id`

### `POST /api/create_case.php`
Crea un caso manual desde la interfaz o una integración interna.

### `POST /api/save_meta_lead.php`
Recibe el lead desde Zapier o futura integración directa con Meta.

#### Responsabilidades
- validar token
- validar payload mínimo
- evitar duplicados por `lead_id`
- normalizar teléfono
- crear o vincular contacto
- crear caso o añadir evento
- registrar evento `meta_form_submitted`
- dejar trazabilidad del origen

#### Payload lógico esperado
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
  "vehicle": {
    "plate": "1234ABC"
  },
  "case_summary": {
    "purchase_window": "menos_30_dias",
    "seller_type": "profesional",
    "problem_type": "motor",
    "vehicle_usable": "usable_con_fallos",
    "documents_available": "tengo_algo",
    "problem_summary": "testigo motor y tirones a la semana"
  }
}
```

#### Header requerido
- `X-CRM-Token: <token>`

### `POST /api/add_event.php`
Añade un evento al timeline de un caso.

Ejemplos:
- llamada realizada
- mensaje enviado
- documentación solicitada
- recontacto agendado
- lead revisado
- lead descartado

### `POST /api/update_case.php`
Actualiza campos editables del caso.

### `POST /api/update_status.php`
Cambia `status_pipeline` y registra el evento correspondiente.

### `GET /api/search_cases.php`
Búsqueda rápida por:
- teléfono
- matrícula
- nombre
- `case_id`

### `POST /api/upload_document.php`
Sube o registra un documento asociado al caso.

### `POST /api/login.php`
Inicio de sesión.

### `POST /api/logout.php`
Cierre de sesión.

## Respuesta JSON tipo
```json
{
  "ok": true,
  "data": {},
  "error": null
}
```

## Respuesta de error tipo
```json
{
  "ok": false,
  "data": null,
  "error": {
    "code": "INVALID_TOKEN",
    "message": "Token inválido o ausente"
  }
}
```

## Consideraciones
- los nombres finales podrán ajustarse, pero el contrato funcional debe mantenerse
- ninguna integración escribirá directamente en los archivos del CRM
- Zapier solo actúa como puente de entrada
- el CRM es el sistema operativo real del lead
