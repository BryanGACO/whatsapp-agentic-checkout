# Product Vision Board — Agente de Cierre y Recaudo Automático en WhatsApp
**Versión:** 2.0 | **Fecha:** Marzo 2026 | **Industria:** Agentic Commerce / Embedded Fintech

---

## 🧠 Vision
**Describe en una o dos frases la visión general de tu producto. ¿Por qué existe y a qué aspira?**

- Ser el motor transaccional nativo de WhatsApp para el comercio de alto volumen en Colombia: el sistema que convierte una conversación en dinero verificado en cuenta, de forma autónoma y sin fraude.
- Capitalizar la ventana histórica que abre Bre-B (operativo desde octubre 2025) para cerrar el "abismo transaccional" del social commerce colombiano antes de que lo haga un actor de mayor escala.

> **Nota crítica frente a v1:** La visión anterior era aspiracional pero genérica. Esta versión ancla la urgencia en un evento de mercado real (Bre-B) y en una ventana de tiempo accionable (2026), lo que orienta decisiones de priorización.

---

## 🎯 Target Group
**Identifica a tus usuarios objetivo. ¿Quiénes son sus principales características y qué problemas les estás resolviendo?**

- **Segmento MVP — Prioridad 1 (primeros 60 días):**
  - **Dark Kitchens y restaurantes de alto pedido nocturno:** Mínimo 30–80 órdenes/día. Ticket promedio $25,000–$60,000 COP. El tiempo real entre cobro y despacho es su ventaja competitiva. No pueden permitirse parar 5 minutos a confirmar si un Nequi entró.
  - **Social Commerce de Indumentaria / Retail:** Tiendas nacidas en Instagram o TikTok con 50–150 pedidos/día y ticket promedio $45,000–$200,000 COP. Su canal de venta exclusivo es WhatsApp. Tienen miedo real al Falso Nequi.

- **Segmento Ola 2 — Prioridad 2 (a partir del mes 3):**
  - **Distribuidores B2B mayoristas a tienderos:** Empresas que despachan pedidos recurrentes a tiendas de barrio por WhatsApp. El cobro contra entrega o transferencia manual genera descuadres, riesgo de efectivo y fricción operativa en campo.

- **Características del perfil decisor (quién compra):**
  - Dueño o gerente de operaciones con visión práctica, no técnica. Toma decisiones en semanas, no trimestres.
  - Ya usa WhatsApp Business pero de forma manual. Ha sufrido al menos 1 intento de estafa con comprobante falso.
  - Tiene un equipo de 2–5 personas que hoy dedican horas a conciliar pagos.

- **Contexto de uso crítico (cuándo el dolor es máximo):**
  - **Picos de demanda:** Viernes noche (restaurantes), lanzamientos de colección o días de pago (retail), inicio de semana de pedidos (B2B).
  - **Picos de fraude:** Temporadas altas (diciembre, día de las madres) cuando el volumen de órdenes supera la capacidad de validación manual del equipo.

- **Problemas actuales que viven:**
  - Pérdidas económicas directas por "Falso Nequi": APKs piratas que generan SMS y comprobantes indistinguibles del original. Solo en Bogotá, más de 168 casos documentados en las primeras 6 semanas de 2026.
  - Desgaste operativo extremo cruzando chats con apps bancarias para conciliar manualmente en picos.
  - Abandono de carrito por fricción: el cliente debe salir de WhatsApp, abrir su banco, digitar monto y número, volver con pantalllazo. En ese salto, una fracción significativa no completa.
  - Parálisis operativa cuando la app bancaria del dueño cae: toda la operación de despacho se detiene hasta que el sistema vuelve.

> **Nota crítica frente a v1:** La v1 no distinguía entre segmento MVP y segmento de expansión, lo que dificulta el foco del equipo y el mensaje de ventas. Se agrega el pain point de "app caída" (documentado en ICP) que no aparecía antes.

---

## 💚 Needs
**Enumera las necesidades y dolores específicos de tus usuarios. ¿Qué quieren lograr que tu producto les facilitará?**

- **Dolores / frustraciones actuales:**
  - Miedo diario a ser estafados con pantallazos editados o APKs clonadas; el banco los recomienda no confiar en imágenes pero no les da alternativa.
  - Horas de trabajo administrativo destruidas en conciliación manual: cruzar 80 chats con los movimientos de Nequi un viernes de noche.
  - Clientes que abandonan la compra por la fricción del proceso de pago manual (cambio de app, tipeo de datos, envío de comprobante).
  - Dependencia de la disponibilidad de la app bancaria del vendedor para poder despachar: un punto único de falla operativa.

- **Necesidades funcionales (qué necesitan hacer):**
  - Cobrar el monto exacto de una orden directamente en el celular del cliente sin que el cliente salga de WhatsApp.
  - Recibir confirmación bancaria automatizada y verificada criptográficamente, no visual.
  - Que el sistema dispare la orden de despacho automáticamente al confirmar el pago, sin intervención humana.
  - Poder operar durante picos de demanda sin necesidad de escalar el equipo humano.
  - Onboarding rápido ("Plug & Play"): conectar su número y catálogo sin meses de integración técnica compleja.

- **Necesidades emocionales (cómo quieren sentirse):**
  - **Paz mental:** "Si el bot dice Pagado, el dinero está en mi cuenta." Certeza absoluta, sin segundas verificaciones.
  - **Control sin dependencia:** No quieren que su operación de despacho dependa de si la app bancaria del dueño está disponible.
  - **Modernidad sin fricción técnica:** Quieren subirse al ecosistema Bre-B sin tener que entender APIs ni contratar un equipo de tecnología.

- **Resultado deseado (qué significa "éxito" para el usuario):**
  - Cero pérdidas por fraude de comprobantes en el primer mes de uso.
  - Recuperar 2–3 horas diarias de trabajo administrativo reasignadas a despacho o atención al cliente.
  - Mayor conversión: menos clientes que abandonan en el paso del pago.
  - Flujo de caja y estado de pedidos visible en tiempo real, sin trabajo manual.

---

## 📦 Product
**Describe la solución que estás construyendo. ¿Cuáles son las características clave y cómo se diferencia de la competencia?**

- **Descripción corta del producto (1 frase):**
  - Un agente de IA en WhatsApp que acompaña al cliente desde la intención de compra, liquida la orden mediante un cobro "Push" directo a su app bancaria (Bre-B / Nequi / DaviPlata) y confirma el despacho automáticamente cuando el servidor bancario certifica el ingreso del dinero.

- **Características clave (Top 5):**
  - **Captura estructurada con WhatsApp Flows:** Formularios nativos para pedido, dirección y billetera. Elimina errores de tipeo y reduce el trabajo del motor de IA.
  - **Cobro Push A2A sin links externos:** El sistema dispara la notificación de cobro directamente a la app del banco del comprador. El cliente solo acepta con biometría. Sin salir de WhatsApp.
  - **Conciliación vía Webhooks bancarios cifrados:** La única fuente de verdad es el evento criptográfico del banco. El agente nunca acepta imágenes, pantallazos ni confirmaciones visuales. Si el webhook no llega, la venta no cierra.
  - **Rule Engine determinístico para cálculo de precios:** El LLM captura la intención del cliente, pero los cálculos de totales, impuestos y envío son delegados a una base de datos relacional (PostgreSQL) y funciones determinísticas en servidor. Sin margen de error matemático ni alucinaciones de precio.
  - **Observabilidad y manejo proactivo de intermitencias:** El sistema monitorea en tiempo real el estado de las APIs bancarias (Bre-B / Nequi). Si detecta caídas o timeouts, pausa el flujo de recaudo y notifica al cliente y al comercio antes de que el dinero "quede en el limbo".

- **Cómo funciona (resumen del flujo completo):**
  - Cliente inicia conversación → IA entiende intención y presenta catálogo → Cliente estructura pedido vía WhatsApp Flow (datos exactos) → Rule Engine calcula total → IA presenta resumen para aprobación del cliente → Sistema conecta con agregador Bre-B y dispara notificación Push al banco del cliente → Cliente aprueba en su app bancaria con biometría → Banco envía Webhook cifrado al servidor → IA confirma pago en el chat, registra la orden y activa despacho → Comercio despacha sin intervenir en la verificación.

- **Diferenciadores vs competencia / alternativas:**
  - **vs. bots de catálogo (la mayoría del mercado):** Estos bots cierran la conversación en el catálogo y derivan a pago manual. El agente cierra el ciclo financiero completo dentro del mismo chat.
  - **vs. soluciones de validación por OCR (ej. MoneT Check):** Leer pantallazos con IA sigue siendo vulnerable a APKs clonadas y SMS falsos. Nuestro modelo elimina el pantallazo de la ecuación desde el diseño. No es un parche, es un rediseño.
  - **vs. pasarelas tradicionales (Wompi, MercadoPago):** Requieren redirigir al usuario a una URL externa, rompiendo la experiencia de WhatsApp. Son optimizadas para tarjeta de crédito (costo 2.95% + $900 COP), no para A2A. Nuestro costo por transacción estimado es ~$600 COP (aprox. 1.7% en un ticket de $35,000 COP).
  - **vs. Bre-B directo:** La integración directa con el Banco de la República o múltiples wallets requiere capacidad técnica significativa. El producto ofrece acceso "Plug & Play" a la red Bre-B empaquetado dentro del canal que los comercios ya usan.

- **Lo que NO es / fuera de alcance (por ahora):**
  - No acepta pagos con tarjeta de crédito ni débito (solo transferencias A2A / Bre-B).
  - No es un chatbot conversacional de propósito general (charla abierta, soporte multi-tema).
  - No valida pagos por imagen ni pantallazos bajo ninguna circunstancia (decisión de diseño irrenunciable).
  - No es un ERP ni sistema de inventario. No gestiona devoluciones ni disputas.
  - No es viable para negocios con ticket promedio por debajo de $15,000 COP (la economía unitaria no cierra: COGS ~$600 COP absorbe el margen).
  - No se construye para múltiples países en el MVP (foco exclusivo en Colombia 2026 por la especificidad de Bre-B).

> **Nota crítica frente a v1:** La v1 omitía el Rule Engine (pieza técnica crítica de la propuesta de valor), la observabilidad de APIs bancarias (feature necesaria para confianza del usuario) y no definía el umbral de ticket mínimo viable, lo que puede generar ventas a clientes que destruyen margen.

---

## 📈 Business Goals
**Establece tus objetivos comerciales. ¿Qué KPIs o métricas quieres alcanzar con este producto?**

- **Objetivo comercial principal:**
  - Validar que el ICP paga por la solución, alcanzar un margen bruto positivo por transacción desde el día 1 (sin necesitar escala para ser rentable por unidad) y demostrar retención: que el % de órdenes que pasan por el bot crece semana a semana.

- **KPIs principales (North Star):**
  - **TPV (Total Payment Volume):** Volumen total de pagos procesados exitosamente por el sistema. Es la métrica que mueve la aguja financiera.
  - **Tasa de éxito transaccional:** % de conversaciones donde el cliente inicia el pago y termina con un Webhook bancario exitoso. Objetivo: ≥ 85% en condiciones normales de red.
  - **Fraud Rate:** Número de fraudes procesados por el sistema. Objetivo no negociable: 0 en toda la historia del producto (por diseño arquitectónico, no por revisión manual).

- **Métricas de adopción:**
  - **Time-to-value (TTV):** Días desde que el comercio firma hasta que procesa su primera transacción exitosa. Objetivo: ≤ 5 días hábiles.
  - **Comercios activos:** Número de comercios que procesaron al menos 1 transacción en los últimos 30 días.

- **Métricas de retención / engagement:**
  - **Bot Penetration Rate:** % de órdenes totales del negocio que pasan por el agente vs. atención manual. Objetivo: ≥ 40% en el mes 1, ≥ 70% en el mes 3 para comercios activos.
  - **Churn mensual de comercios:** Objetivo: ≤ 5% en los primeros 6 meses.

- **Métricas financieras (Unit Economics):**
  - **COGS por transacción:** ~$420–$640 COP (Meta API + LLM + agregador Bre-B).
  - **Ingreso por transacción (Modelo Híbrido recomendado):** $900 COP flat fee. Margen bruto transaccional: ~$260–$480 COP por orden. Positivo desde la primera transacción.
  - **MRR:** Suscripción fija de $150,000 COP/mes por comercio + fees variables. Con 10 comercios activos y 200 transacciones/mes c/u = $1,500,000 COP/mes en suscripciones + $1,800,000 COP en fees ≈ $3.3M COP/mes MRR.
  - **CAC vs LTV:** El LTV de un comercio de alto volumen (200 tx/mes × $900 COP + $150K/mes × 12 meses) = **$3,960,000 COP/año**. El CAC debe mantenerse por debajo de 3 meses de MRR por comercio (~$990,000 COP) para un ratio LTV/CAC ≥ 4x.

- **Meta inicial — Hitos 30 / 60 / 90 días:**
  - **30 días:** Firmar 2 pilotos con Dark Kitchens o tiendas de Instagram con ticket promedio > $25,000 COP. Procesar las primeras 100 transacciones reales sin incidentes de fraude. Validar el flujo Push → Webhook end-to-end en producción.
  - **60 días:** Alcanzar 5 comercios activos en beta cerrada. Procesar 500 transacciones exitosas. Recopilar evidencia de NPS ≥ 8 y al menos 3 testimonios de "cero fraude" documentados. Confirmar BOT Penetration Rate > 40% en comercios activos.
  - **90 días:** Llegar a 10 comercios. MRR ≥ $3,000,000 COP. Primera iteración del dashboard de ventas para el comercio. Evaluar el go/no-go para incorporar el segmento B2B mayorista.

> **Nota crítica frente a v1:** La v1 no incluía los unit economics concretos del modelo de pricing (documentados en `Estructura_costos_modelo_pricing.md`), lo que hacía los Business Goals imposibles de conectar con la viabilidad financiera. Se agrega el cálculo explícito de LTV/CAC y el umbral de ticket mínimo.

---

## ✅ Notas, Supuestos y Riesgos

- **Supuestos clave:**
  - El AOV (ticket promedio) de los comercios en el ICP objetivo es consistentemente superior a **$15,000 COP**. Por debajo de este umbral, el COGS (~$600 COP) erosiona el margen al punto de no viabilidad. Es un criterio de calificación de cliente, no una preferencia.
  - Los compradores finales (clientes del comercio) confían en la notificación Push de su app bancaria oficial como mecanismo de pago. La confianza en Bre-B como estándar interoperable es un supuesto de adopción del mercado que aún está construyéndose.
  - Los agregadores financieros B2B (ej. Cobre / TechPay) mantienen sus condiciones de acceso a la red Bre-B y su modelo de precios estable durante al menos 12 meses.
  - Meta mantiene la categoría "Transaccional / Utilidad" habilitada en WhatsApp Business Platform para Colombia y no introduce restricciones adicionales al modelo de uso en 2026.

- **Riesgos principales (por probabilidad × impacto):**
  - 🔴 **CRÍTICO — Intermitencias de infraestructura bancaria:** Bre-B, Nequi y DaviPlata presentan caídas documentadas. Una experiencia de pago fallida durante un pico de demanda destruye la confianza del comercio y del cliente final. **Mitigación:** Observabilidad activa + notificación proactiva de estado al usuario en el flujo del bot.
  - 🔴 **CRÍTICO — Dependencia de aprobación WABA y BSP:** El tiempo de aprobación del número oficial de WhatsApp (WABA) por parte de Meta vía un BSP (Twilio, Gupshup) puede tomar 2–6 semanas. Es el cuello de botella #1 para el MVP. **Acción inmediata:** Iniciar el proceso de aplicación en paralelo con el desarrollo, no secuencialmente.
  - 🟡 **ALTO — Adopción del flujo Push por parte del comprador final:** Si el cliente final del comercio no reconoce o desconfía de la notificación Push de su banco (por desconocimiento de Bre-B o asociación con phishing), la tasa de éxito transaccional cae. **Mitigación:** Diseñar mensajes de educación en el flujo del bot ("Acabas de recibir una notificación de pago de tu banco, es segura, solo apruébala").
  - 🟡 **ALTO — Cambios de política de Meta (WhatsApp):** Meta puede cambiar su modelo de pricing por conversación o restringir casos de uso transaccionales sin previo aviso (como ocurrió con la deprecación de templates en 2024). **Mitigación:** No construir dependencias exclusivas de un solo BSP. Diseñar la capa de mensajería como intercambiable.
  - 🟠 **MEDIO — Cumplimiento regulatorio Ley 1581 (Habeas Data):** Al capturar números de billeteras digitales y datos de pedidos, el producto actúa como encargado del tratamiento de datos personales. Requiere política de privacidad, opt-in explícito, cifrado en reposo y tránsito, y política de retención de datos. No es un blocker para el MVP, pero sí un riesgo legal si se escala sin este framework.

- **Dependencias críticas (tech, partners, regulación):**
  - Acceso a API de agregador financiero con cobertura Bre-B (Cobre, TechPay o equivalente): **blocker para el flujo de pago Push**.
  - Aprobación de número WABA oficial por Meta vía BSP (Twilio o Gupshup): **blocker para el MVP en producción**.
  - Infraestructura cloud con colas de mensajes resilientes (SQS / RabbitMQ) para garantizar que ningún Webhook bancario se pierda durante picos de tráfico o caídas momentáneas del servidor.
  - PostgreSQL como fuente de verdad determinística de precios y catálogo (no el LLM).
