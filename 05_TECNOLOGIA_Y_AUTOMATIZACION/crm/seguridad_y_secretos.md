# Seguridad y gestión de secretos

## Principio general

El CRM manejará datos sensibles de potenciales clientes y expedientes.  
Por tanto, la v1 debe ser simple, pero no ingenua.

## Reglas obligatorias

### 1. No subir secretos al repositorio
No se subirá a GitHub público:

- tokens
- rutas reales privadas del hosting
- credenciales
- claves de integración
- ejemplos con datos personales reales

### 2. Carpeta `storage/` bloqueada
La carpeta `storage/` y su contenido deberán estar protegidos por `.htaccess`.

### 3. Nada sensible en el frontend
No se incluirán secretos en:

- `app.js`
- `config.js`
- HTML
- atributos expuestos al navegador

### 4. Acceso a datos solo mediante backend
El navegador no leerá archivos privados directamente.

### 5. Logs controlados
Los logs no deben exponer tokens ni datos innecesarios.

## Ubicación prevista de secretos

Archivo local no versionado:

`/storage/config/secrets.php`

Contenido esperado:

- token de Zapier
- tokens de integraciones
- flags de entorno
- credenciales futuras

## Reglas para integraciones externas

Toda integración que escriba en el CRM deberá autenticarse.

Opciones previstas:

- token estático en header
- token rotado manualmente
- sesión autenticada en caso de UI

## Medidas mínimas v1

- HTTPS
- token de entrada para Zapier
- validación básica de sesión o contraseña
- `.htaccess` en almacenamiento
- bloqueo de ejecución PHP en zonas de archivos
- backup periódico

## Riesgos conocidos de la v1

- autenticación todavía simple
- almacenamiento en JSON en vez de base de datos
- posible colisión si no se implementan bien los bloqueos de escritura
- permisos todavía no granulares

## Criterio de mejora futura

La seguridad de la v1 debe ser suficiente para operar con cautela, pero se deja preparada la transición a:

- login robusto
- roles
- base de datos
- cifrado de ciertos campos
- trazabilidad más fuerte
