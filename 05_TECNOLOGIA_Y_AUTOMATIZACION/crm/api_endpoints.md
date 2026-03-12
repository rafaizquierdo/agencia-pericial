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

Responsabilidades:

- validar token
- evitar duplicados
- crear o vincular contacto
- crear caso o añadir evento

### `POST /api/add_event.php`
Añade un evento al timeline de un caso.

Ejemplos:

- llamada realizada
- mensaje enviado
- documentación solicitada
- recontacto agendado

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
