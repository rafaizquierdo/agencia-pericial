# Campaña Meta v1 — Leads de vicios ocultos con formulario

## Objetivo
Generar leads cualificados de personas que han comprado un vehículo recientemente y han detectado una avería, fallo grave o indicio de reparación deficiente, filtrando desde el propio formulario para evitar consumir tiempo humano en casos de bajo encaje.

## Hipótesis de trabajo
1. La intención pesa más que el perfil demográfico o los intereses.
2. Un formulario de Meta con fricción moderada filtra mejor que enviar directamente a WhatsApp.
3. La primera llamada humana debe reservarse para leads que ya han mostrado:
   - compra reciente,
   - problema relevante,
   - posibilidad de contacto,
   - y un mínimo de contexto para revisión.
4. El CRM debe capturar el lead desde el minuto 1 para poder medir calidad real, no solo coste por lead.

## Estructura de campaña
- 1 campaña
- 1 conjunto de anuncios
- 2 anuncios

## Naming
### Campaña
`AP | Leads | Vicios ocultos | ES | Form v1`

### Conjunto de anuncios
`ES | Broad | 25-65 | Form v1`

### Anuncios
- `Ad 1 | Dolor | Avería tras compra`
- `Ad 2 | Autoridad | Revisión pericial`

## Configuración recomendada
### Objetivo
Leads

### Ubicación de conversión
Formulario instantáneo de Meta

### Tipo de formulario
Higher intent

### Público inicial
- ubicación: España
- edad: 25–65+
- sexo: todos
- idioma: español
- segmentación detallada: amplia en v1

## Presupuesto inicial recomendado
- referencia operativa: 20–30 €/día
- mínimo razonable para empezar a leer datos: 15 €/día

## Creatividades
Se usarán imágenes ya diseñadas orientadas a:
1. problema inesperado tras la compra
2. inspección técnica / criterio profesional

## Mensaje estratégico
No vender “esperanza jurídica”.
Sí vender:
- validación técnica,
- criterio,
- y filtro honesto.

La promesa correcta no es:
> “te garantizamos ganar”

La promesa correcta es:
> “revisamos si tu caso encaja y si merece la pena moverlo”

## Copy base del anuncio — versión dolor
### Texto principal
¿Has comprado un coche de ocasión y te ha salido una avería importante poco después?

No todos los casos encajan, pero en muchos sí merece la pena revisar avería y contexto de la compra.

Completa el formulario y haré una primera valoración del caso.

### Titular
Revisa si tu caso merece reclamación

### Descripción
Filtro inicial antes de hablar por WhatsApp

### CTA
Más información

## Copy base del anuncio — versión autoridad
### Texto principal
Un informe pericial puede marcar la diferencia entre tener una sospecha y tener una base técnica seria para reclamar.

Si has comprado un vehículo recientemente y ha aparecido un problema importante, completa el formulario y revisaré si el caso encaja antes de hacerte perder tiempo o dinero.

### Titular
Primera revisión técnica del caso

### Descripción
Cuéntame qué ha pasado y te diré si compensa revisarlo

### CTA
Más información

## Formulario usado
Nombre interno:
`AP | Vicios ocultos | Filtro inicial v1`

## Campos del formulario
### Obligatorios
- nombre completo
- teléfono
- provincia
- ¿cuándo compraste el vehículo?
- ¿a quién compraste el vehículo?
- ¿qué tipo de problema ha aparecido?
- ¿el vehículo se puede usar ahora mismo?

### Opcionales
- email
- resume el problema en una frase

## Nota importante sobre fricción
En esta v1 NO se piden en el formulario:
- precio de compra del vehículo
- cuantía estimada a reclamar
- matrícula
- documentación disponible

Estos datos siguen siendo críticos para ventas y operación, pero se desplazan a la llamada de cualificación o al seguimiento posterior para no elevar demasiado la fricción inicial del formulario.

## Lógica operativa del funnel
1. Usuario ve anuncio
2. Usuario abre formulario
3. Usuario deja datos
4. Meta envía lead a Zapier
5. Zapier hace POST a `save_meta_lead.php`
6. El CRM crea o actualiza caso
7. El lead entra con estado inicial `nuevo`
8. Se revisa manualmente
9. Si encaja, se llama
10. Si no encaja, se marca como descartado con motivo

## Criterios de descarte en revisión humana
- no ha comprado aún el vehículo
- problema puramente estético o de mantenimiento
- falta total de encaje temporal y técnico
- lead imposible de contactar
- expectativa jurídica irreal sin apertura a escuchar criterio técnico

## Objetivo real de esta campaña
No optimizar por volumen bruto de formularios.
Optimizar por:
- lead válido,
- llamada útil,
- caso viable,
- y venta cerrada.

## Métricas mínimas a seguir
- gasto
- impresiones
- CTR
- CPC
- coste por lead
- leads recibidos en CRM
- leads válidos
- llamadas realizadas
- ofertas enviadas
- ventas cerradas
- coste por venta
- tasa lead → venta
- tasa lead válido → venta

## Decisiones de versión
### v1
- formulario en Meta
- conexión vía Zapier
- CRM propio en IONOS
- validación humana tras entrada
- test dummy CRM/Zapier superado correctamente

### v2 potencial
- más lógica de exclusión
- automatización adicional de scoring
- test de nuevos ángulos creativos
- retargeting a visitantes / engagers
