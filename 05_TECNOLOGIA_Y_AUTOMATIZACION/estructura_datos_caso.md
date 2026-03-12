# Estructura de datos del caso (source of truth)

Objetivo: que humanos y agentes recojan SIEMPRE lo mismo, en el mismo orden, para:
- reducir llamadas eternas,
- subir el close rate,
- y alimentar la IA de redacción.

---

## 1) Campos mínimos (obligatorios)
### Identificación
- case_id
- fecha_creacion
- fuente (ads / orgánico / abogado / etc.)
- estado_pipeline (ver sección 2)

### Cliente
- nombre
- teléfono
- email
- provincia/ciudad

### Vehículo (lo que mueve la decisión de compra)
- marca_modelo
- matrícula (si la da)
- km_compra / km_actual
- **precio_compra_vehiculo (€)** ✅ (preguntar al principio)
- vendedor_tipo: particular / profesional
- fecha_compra_entrega

### Problema
- fecha_aparicion_fallo
- sintomas_principales (texto corto)
- gravedad: uso_normal / uso_limitado / inmovilizado / riesgo_seguridad
- detectabilidad_previas: evidente / dudoso / oculto

### Economía (lo que mueve la decisión de reclamar)
- **cuantia_a_reclamar_estimada (€)** ✅ (preguntar al principio)
- objetivo_cliente: reparación / rebaja / devolución / otro
- probabilidad_no_compensa (baja/media/alta) [auto por reglas]

### Evidencias
- contrato_factura (sí/no + enlace)
- anuncio (sí/no + enlace)
- mensajes_vendedor (sí/no + enlace)
- diagnosis_taller (sí/no + enlace)
- fotos/videos (sí/no + enlace)

### Comercial
- precio_ofertado (590/390/290/220)
- motivo_precio (complexidad / vehiculo<4000 / cuantia<=2000 / rescate)
- estado_venta: pendiente / ganado / perdido
- motivo_perdida (presupuesto / no compensa / no encaja / no responde / otro)
- fecha_followup_programada

---

## 2) Pipeline recomendado (estados)
1) lead_nuevo
2) cualificacion_pendiente
3) llamada_programada
4) llamada_realizada
5) oferta_enviada
6) followup_programado
7) venta_ganada
8) pago_confirmado
9) peritacion_programada
10) peritacion_realizada
11) informe_generado_ia
12) revision_perito
13) informe_enviado
14) caso_cerrado

---

## 3) Orden de preguntas (para formularios/bot)
Orden ideal para reducir “no compensa” y ahorrar tiempo humano:
1) vendedor (particular/profesional)
2) fecha compra
3) **precio compra vehículo**
4) **cuantía a reclamar estimada**
5) gravedad (¿se puede usar?)
6) síntomas principales
7) ubicación del coche
8) documentación disponible (checklist)
9) teléfono/email

---

## 4) Regla automática de precio (para bot/CRM)
- cuantía ≤ 2.000€ → candidato a 220€
- vehículo < 4.000€ → candidato a 290€
- si ambos → 220€
- resto → 390€ por defecto (salvo “complex”)

> El closer puede subir/bajar según complejidad real, pero el sistema propone un default.
