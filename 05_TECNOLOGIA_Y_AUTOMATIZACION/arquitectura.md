# Arquitectura general

## Resumen

La arquitectura elegida para la v1 del CRM es:

**IONOS + subdominio propio + HTML/JS + PHP + JSON privado protegido por `.htaccess`**

Subdominio previsto:

`ap-crm.rafaizquierdo.es`

## Capas del sistema

### 1. Capa de interfaz
Web responsive accesible desde escritorio y móvil.

Componentes previstos:

- `crm.html`
- recursos estáticos JS/CSS en `/assets/`

Funciones:

- ver lista de casos
- filtrar y buscar
- abrir ficha de caso
- ver timeline
- añadir eventos
- cambiar estado
- crear casos manuales

### 2. Capa de aplicación
Mini backend PHP expuesto en `/api/`.

Responsabilidades:

- leer casos
- crear casos
- actualizar campos
- añadir eventos
- procesar leads entrantes desde Meta/Zapier
- validar tokens o sesiones
- devolver respuestas JSON consistentes

### 3. Capa de datos
Almacenamiento en archivos JSON dentro de carpeta protegida por `.htaccess`.

Criterios:

- un JSON por caso
- índices auxiliares por teléfono, matrícula, estado y leads ya procesados
- logs separados
- carpeta de documentos adjuntos

## Decisiones técnicas ya cerradas

### Hosting
Se usará **IONOS**, ya que el entorno del subdominio ya ejecuta PHP correctamente.

### Dominio
Se usará el subdominio:

`ap-crm.rafaizquierdo.es`

### Estrategia de datos
No se usará Google Sheets como CRM principal.  
No se usará un JSON público servido directamente al navegador.  
Los archivos JSON estarán detrás de endpoints PHP.

### Estrategia de integración
La API del CRM será el punto único de entrada para:

- leads desde Meta
- automatizaciones vía Zapier
- acciones internas desde la UI
- futuras acciones de agentes OpenClaw

## Restricciones

- el repositorio GitHub es público
- no deben subirse secretos
- no deben subirse rutas privadas reales del hosting
- no deben subirse datos personales reales
- no debe dependerse de un backend complejo o desconocido para la v1

## Evolución futura posible

La arquitectura actual está pensada como una base simple, pero deja abierta una futura migración a:

- base de datos relacional
- autenticación más robusta
- colas de automatización
- almacenamiento separado de documentos
- panel multiusuario con permisos

La documentación y el modelo de datos ya se escriben pensando en que esa migración futura sea posible sin rehacerlo todo.
