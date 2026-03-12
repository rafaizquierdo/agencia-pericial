# Arquitectura concreta en IONOS

## Decisión de hosting

La v1 del CRM se desplegará en **IONOS** bajo el subdominio:

`ap-crm.rafaizquierdo.es`

## Decisión de almacenamiento

Se usará **Opción B**:

- todo bajo la raíz del subdominio
- carpeta `storage/` protegida por `.htaccess`
- acceso a datos solo mediante endpoints PHP

## Estructura propuesta

```text
/ap-crm/
  crm.html
  index.html
  .htaccess

  /assets/
    app.js
    api.js
    ui.js
    styles.css
    config.js

  /api/
    bootstrap.php
    auth.php
    helpers.php
    response.php
    get_cases.php
    get_case.php
    create_case.php
    save_meta_lead.php
    add_event.php
    update_case.php
    update_status.php
    search_cases.php
    upload_document.php
    login.php
    logout.php

  /storage/
    .htaccess
    /config/
      app_config.php
      secrets.php
    /data/
      /cases/
        /2026/
      /indexes/
        contacts_by_phone.json
        cases_by_status.json
        cases_by_plate.json
        meta_leads_processed.json
      /backups/
    /documents/
      /2026/
    /logs/
      api.log
      errors.log
      meta_ingest.log
```

## Reglas de esta estructura

### 1. Lo público
Solo deben ser accesibles públicamente:

- `crm.html`
- `index.html`
- `/assets/`
- `/api/` en la medida en que sus endpoints lo permitan

### 2. Lo privado
Debe estar bloqueado por `.htaccess`:

- `/storage/config/`
- `/storage/data/`
- `/storage/documents/`
- `/storage/logs/`

### 3. Escrituras
Toda escritura de datos debe pasar por `/api/`.

### 4. Secretos
Los secretos irán en:

- `/storage/config/secrets.php`

Ese archivo no se subirá al repositorio público.

## Archivo `.htaccess` en `/storage/`

Versión base prevista:

```apache
Require all denied
```

Compatibilidad adicional, si el hosting lo requiriera:

```apache
Order allow,deny
Deny from all
```

## Decisiones descartadas

- JSON público servido directamente al navegador
- Google Sheets como CRM principal
- GitHub como almacén operativo del dato
- frontend con acceso directo al sistema de archivos
