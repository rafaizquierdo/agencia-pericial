# Flujos de automatización

## Objetivo

Definir cómo entran y evolucionan los casos en el CRM sin depender de memoria manual ni de copiar y pegar datos entre herramientas.

## Flujo 1: entrada desde formulario de Meta

1. El usuario ve un anuncio en Meta.
2. El usuario completa el formulario de lead.
3. Meta entrega el lead a Zapier.
4. Zapier hace `POST` a `save_meta_lead.php`.
5. El backend:
   - valida el token de entrada
   - comprueba duplicados por `lead_id`
   - normaliza teléfono
   - crea o vincula contacto
   - crea caso nuevo o añade evento según reglas
   - registra evento `meta_form_submitted`
   - asigna estado inicial

## Flujo 2: recontacto manual desde CRM

1. El operador abre un caso.
2. Añade una nota o seguimiento.
3. Se crea un evento en timeline.
4. Si procede, se genera tarea de seguimiento.

## Flujo 3: actualización de estado

1. El operador cambia el estado del caso.
2. El backend valida el nuevo estado.
3. Se actualiza el JSON del caso.
4. Se añade un evento interno de cambio de estado.
5. Se actualizan índices auxiliares.

## Flujo 4: subida de documentación

1. El operador sube archivos vinculados al caso.
2. El backend guarda el archivo en carpeta protegida o controlada.
3. El caso registra el documento en el array `documents`.
4. Se añade evento `document_uploaded`.

## Flujo 5: automatizaciones con OpenClaw

OpenClaw no accederá directamente a los JSON internos.  
OpenClaw consumirá endpoints definidos por la API del CRM para:

- leer casos concretos
- añadir eventos
- crear tareas
- marcar estados si se le autoriza

## Reglas generales

- toda automatización debe dejar rastro en timeline o log
- toda escritura debe pasar por backend
- toda integración externa debe autenticarse con token
- no se debe modificar manualmente el JSON salvo mantenimiento excepcional
