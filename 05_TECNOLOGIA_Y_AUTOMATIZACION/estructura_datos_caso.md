# Estructura de datos del caso (source of truth)

## Objetivo
Que humanos y agentes recojan SIEMPRE lo mismo, en el mismo orden, para:
- reducir llamadas eternas,
- subir el close rate,
- y alimentar la IA de redacción.

## 1) Campos mínimos (obligatorios)

### Identificación
- `case_id`
- `fecha_creacion`
- `updated_at`
- `fuente_canal` (`meta_form`, `orgánico`, `abogado`, `referido`, etc.)
- `fuente_campaña`
- `fuente_conjunto`
- `fuente_anuncio`
- `fuente_formulario`
- `fuente_lead_id`
- `estado_pipeline`

### Cliente
- `nombre`
- `teléfono`
- `email`
- `provincia_ciudad`

### Vehículo
- `marca_modelo`
- `matrícula`
- `km_compra`
- `km_actual`
- `precio_compra_vehiculo`
- `vendedor_tipo`
- `fecha_compra_entrega`

### Problema
- `purchase_window` (si aún solo tenemos rango)
- `fecha_aparicion_fallo`
- `tipo_problema`
- `sintomas_principales`
- `gravedad` (`uso_normal`, `uso_limitado`, `inmovilizado`, `riesgo_seguridad`)
- `detectabilidad_previas` (`evidente`, `dudoso`, `oculto`)
- `vehicle_usable`
- `problem_summary`

### Economía
- `cuantia_a_reclamar_estimada`
- `objetivo_cliente`
- `probabilidad_no_compensa`

### Evidencias
- `documentacion_disponible`
- `contrato_factura`
- `anuncio`
- `mensajes_vendedor`
- `diagnosis_taller`
- `fotos_videos`

### Comercial
- `qualification_status`
- `precio_ofertado`
- `motivo_precio`
- `estado_venta`
- `motivo_perdida`
- `fecha_followup_programada`

## 2) Pipeline recomendado (estados)
1. `nuevo`
2. `pendiente_revision`
3. `pendiente_documentacion`
4. `precalificado`
5. `llamada_programada`
6. `llamada_realizada`
7. `oferta_enviada`
8. `followup_programado`
9. `venta_ganada`
10. `pago_confirmado`
11. `peritacion_programada`
12. `peritacion_realizada`
13. `informe_generado_ia`
14. `revision_perito`
15. `informe_enviado`
16. `caso_cerrado`

## 3) Orden de captura
### En Meta v1
1. nombre
2. teléfono
3. email opcional
4. provincia
5. antigüedad de compra
6. vendedor
7. tipo de problema
8. si el coche se puede usar
9. documentación disponible
10. matrícula opcional
11. resumen breve del problema opcional

### En llamada de cualificación
1. precio de compra del vehículo
2. cuantía aproximada a reclamar
3. fecha real de aparición del fallo
4. detalles de diagnosis / taller
5. objetivo económico del cliente
6. presupuesto a ofrecer

## 4) Regla operativa de precios
- cuantía ≤ 2.000 € → candidato a `220 €`
- vehículo < 4.000 € → candidato a `290 €`
- si ambos → `220 €`
- resto → `390 €` por defecto
- `590 €` si hay complejidad real superior

## 5) Principio de diseño
El formulario de Meta NO es la ficha completa del caso.
Solo es la entrada filtrada al sistema.
El caso se considera completo cuando CRM + llamada + documentación dejan el expediente con contexto suficiente para decidir o producir.
