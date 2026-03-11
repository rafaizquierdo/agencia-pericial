# AGENCIA-PERICIAL — Operación “máquina engrasada”

Este repositorio contiene **toda la documentación operativa** para construir y escalar una agencia de **informes periciales** (principalmente vicios ocultos y casos afines) con mentalidad de **ingeniería de negocio**: procesos claros, automatización, uso intensivo de IA y el **mínimo personal imprescindible**.

El objetivo es que cualquier persona nueva (humano o agente IA) pueda entender en 10–15 minutos:
- qué es el proyecto,
- cómo funciona la “fábrica” (marketing → venta → peritación → IA → entrega),
- dónde está cada cosa,
- y cuáles son los documentos fuente de verdad.

---

## 1) Qué hacemos (en una frase)
Convertimos leads con problemas reales en **casos cerrados y entregados** con un **informe pericial sólido**, mediante un proceso repetible y medible.

---

## 2) Principios del proyecto
1. **Proceso > heroicidades.** Si algo depende de una persona “salvando el día”, es un fallo de sistema.
2. **Datos estructurados.** La IA redacta bien cuando le damos inputs limpios y completos.
3. **Calidad y consistencia.** Un informe tiene que aguantar abogados/jueces: claridad, pruebas y coherencia.
4. **Capacidad limitada.** Ventas y peritación tienen cuellos de botella: se modelan y se gestionan.
5. **Una sola fuente de verdad por tema.** Nada de 14 versiones del mismo guion.

---

## 3) Flujo de trabajo (end-to-end)
Resumen del “producto” en forma de pipeline:

1. **Captación:** campañas + referrals + orgánico.
2. **Cualificación:** separar casos aptos vs no aptos (sin vender humo).
3. **Venta:** llamada humana persuasiva (calma + confianza + cierre).
4. **Seguimiento:** bot/WhatsApp para cerrar lo que no se cerró en llamada, con reglas de descuento.
5. **Operación pericial:** llamada del perito + coordinación + peritación en campo + fotos + conclusiones.
6. **Redacción con IA:** generación de informe basado en datos + conclusiones + evidencias.
7. **Revisión y firma:** el perito valida, corrige si hace falta y firma.
8. **Entrega y postventa:** envío, aclaraciones, y canal con despachos si aplica.

El detalle está documentado en:
- `04_OPERACIONES/SOP_end_to_end.md`

---

## 4) Cómo está organizada la documentación
La estructura está pensada para ser **manejable**. Pocas carpetas, nombres obvios.

### 00_README/
Documentos de entrada.
- `README.md` (este documento)
- `ROADMAP.md` (qué se va a construir y en qué orden)
- `GLOSARIO.md` (términos y definiciones)

### 01_PRODUCTO_Y_OFERTA/
Qué vendemos y bajo qué condiciones.
- `oferta_y_precios.md`
- `alcance_servicio.md`
- `politicas.md`
- `casos_no_aplican.md`

### 02_MARKETING/
Cómo generamos demanda.
- `posicionamiento.md`
- `mensajes_clave.md`
- `creatividades/` (prompts y copies)
- `campañas/` (1 doc por campaña)

### 03_VENTAS/
Cómo convertimos demanda en ventas.
- `guion_llamada.md` (script + objeciones)
- `checklist_cualificacion.md`
- `oferta_y_descuentos.md`
- `plantillas_mensajes/` (WhatsApp/email)

### 04_OPERACIONES/
Cómo producimos el informe (la “fábrica”).
- `SOP_end_to_end.md`
- `SLA_y_plazos.md`
- `checklist_peritacion.md`
- `plantilla_conclusiones_perito.md`
- `control_calidad.md`

### 05_TECNOLOGIA_Y_AUTOMATIZACION/
Cómo lo automatizamos (datos, integraciones, IA).
- `arquitectura.md`
- `flujos_automatizacion.md`
- `estructura_datos_caso.md`
- `prompts_ia/`
- `integraciones/`

### 06_FINANZAS_Y_KPIS/
Modelo económico y métricas.
- `modelo_economico/modelo_agencia_pericial_24m.xlsx`
- `modelo_economico/supuestos_y_escenarios.md`
- `kpis.md`
- `reporting_mensual.md`

### 07_LEGAL_Y_PLANTILLAS/
Contratos, RGPD y plantillas.
- `contratos/`
- `rgpd/`
- `plantillas/`

### 08_PERSONAS_Y_ROLES/
Cómo trabajamos con humanos y agentes.
- `roles_y_responsabilidades.md` (RACI simple)
- `onboarding.md`
- `directorio_colaboradores.md`

### 99_ARCHIVO/
Cosas antiguas o fuera de uso.
- `_old/` (se conserva, pero no molesta)

---

## 5) Convenciones (para no acabar en caos)
- **Edita lo mínimo y mejor.** Si cambias un documento “core”, hazlo con intención.
- **Evitar duplicados.** Si existe `guion_llamada.md`, no crees `guion_llamada_v2.md`. Actualiza el original.
- **Plantillas y assets separados.** Copys y prompts en `02_MARKETING/creatividades/`.
- **Documentos “core” (fuente de verdad):**
  - `03_VENTAS/guion_llamada.md`
  - `04_OPERACIONES/SOP_end_to_end.md`
  - `05_TECNOLOGIA_Y_AUTOMATIZACION/estructura_datos_caso.md`
  - `06_FINANZAS_Y_KPIS/modelo_economico/modelo_agencia_pericial_24m.xlsx`

---

## 6) Para empezar si eres nuevo/a
1. Lee este README.
2. Abre `04_OPERACIONES/SOP_end_to_end.md` para entender el proceso real.
3. Abre `03_VENTAS/guion_llamada.md` para entender cómo se vende.
4. Revisa `06_FINANZAS_Y_KPIS/modelo_economico/modelo_agencia_pericial_24m.xlsx` para entender el motor económico.

---

## 7) Estado actual
Este repo es una **plantilla de arranque**: muchos documentos están en blanco a propósito.
Se irán rellenando en orden de impacto (ventas → operaciones → automatización → legal).

El plan está en `00_README/ROADMAP.md`.

---
