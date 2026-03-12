# Despliegue y operación

## Objetivo

Definir cómo se desplegará y mantendrá la v1 del CRM en IONOS.

## Entornos

### Repositorio GitHub
Solo contendrá:

- documentación
- estructura
- frontend sin secretos
- backend sin secretos embebidos
- ejemplos ficticios

### Hosting IONOS
Contendrá:

- frontend publicado
- endpoints PHP
- carpeta `storage/`
- secretos locales
- datos reales
- documentos reales

## Flujo de despliegue recomendado

1. trabajar en rama `dev`
2. documentar la estructura
3. implementar backend y frontend sin secretos en local
4. subir a IONOS por SFTP
5. crear manualmente archivos de secretos
6. probar endpoints
7. probar UI
8. conectar integración de leads

## Operación diaria prevista

- revisar nuevos leads
- actualizar estados
- registrar eventos
- subir documentación
- revisar tareas pendientes
- generar backups

## Backups

Se recomienda mantener:

- copia periódica de `/storage/data/`
- copia periódica de `/storage/documents/`
- copia periódica de `/storage/config/` en entorno seguro
- export manual antes de cambios grandes

## Logs mínimos

- `api.log`
- `errors.log`
- `meta_ingest.log`

## Mantenimiento

- revisar archivos huérfanos
- comprobar integridad de índices
- verificar permisos de `storage/`
- limpiar `info.php` o archivos de prueba
- comprobar que no se exponen rutas privadas

## Nota operativa

La documentación debe poder vivir en GitHub sin comprometer producción.  
Todo lo que haga falta para operar con datos reales deberá residir únicamente en IONOS.
