# Estructura de Costos y Modelo de Pricing (Unit Economics)

## 1. Costos Variables (Por cada venta/conversación)

Para calcular la viabilidad, debemos entender cuánto nos cuesta procesar **una orden exitosa**. Estos costos se componen de tres capas tecnológicas:

| Componente | Descripción del Costo (Estimado 2026) | Costo COP (Aprox.) |
| :--- | :--- | :--- |
| **WhatsApp Business API (Meta)** | Tarifa por conversación de "Utilidad" o "Servicio" (ventana de 24h). Meta cobra aprox. $0.01 USD por conversación en Colombia, más el margen del BSP (ej. Twilio/Gupshup) de $0.005 USD. | ~$60 COP |
| **Cerebro IA (LLM)** | Costo de tokens de entrada/salida (OpenAI/Anthropic/Google) para interpretar al cliente, calcular totales y estructurar el JSON. Una charla corta de pedido consume aprox. $0.01 - $0.02 USD. | ~$60 - $80 COP |
| **Procesamiento de Pago (Agregador / Bre-B)** | Las transferencias A2A (Cuenta a Cuenta) son más baratas que las tarjetas de crédito. Un agregador B2B (como Cobre o similar) suele cobrar un *flat fee* (tarifa plana) por el webhook y conciliación, en lugar de un % alto. | ~$300 - $500 COP |
| **Costo Variable Total (COGS)** | **Costo directo por cada venta procesada exitosamente.** | **~$420 - $640 COP** |

> **Insight Clave:** El costo de procesar un pedido por este canal automatizado ronda los **$600 COP**. Si una *Dark Kitchen* vende una hamburguesa de $35.000 COP, el costo de nuestra pasarela automatizada representa apenas el **1.7%** del ticket. Esto es significativamente más barato que el modelo tradicional de tarjeta de crédito (que suele cobrar 2.95% + $900 COP = ~$1.932 COP).

## 2. Costos Fijos y Operativos (Mensuales)

Estos son los costos de infraestructura para mantener la plataforma "viva", sin importar si vendes 10 o 10.000 transacciones.

* **Infraestructura Cloud (AWS / GCP):** Servidores para alojar la aplicación, gestionar el encolamiento de mensajes (colas SQS/RabbitMQ para no perder webhooks bancarios si hay picos) y bases de datos PostgreSQL. *(Aprox. $150 - $300 USD / mes en fase MVP).*
* **Suscripción a Proveedores (BSPs):** Mantenimiento del número de WhatsApp oficial (WABA) a través del proveedor. *(Aprox. $15 - $30 USD / mes).*
* **Herramientas de Monitoreo/Observabilidad:** Datadog o Sentry para detectar caídas de Nequi/Bre-B en tiempo real. *(Aprox. $30 USD / mes).*

## 3. Propuesta de Modelo de Pricing (Cómo cobrarle al Cliente)

Basado en el ICP (Comercios de alto volumen y B2B), un modelo de **SaaS de Nicho + Fee Transaccional** es el más escalable y justo. 

### Opción A: Modelo Híbrido (El más recomendado)
Cobras una suscripción mensual fija para cubrir tus costos de servidor e IA, más una pequeña comisión por cada recaudo exitoso que le ahorra dolores de cabeza al negocio.

* **Suscripción Fija (SaaS):** $150.000 COP / mes. 
  * *Incluye:* Conexión del número de WhatsApp, dashboard de ventas, mantenimiento del bot y acceso a la red Bre-B/Nequi.
* **Fee por Transacción Exitosa:** $900 COP (o 1.5% del valor de la orden).
  * *El negocio:* Te cuesta ~$600 COP. Le cobras $900 COP. Tienes un margen bruto transaccional positivo desde el día 1, más el ingreso recurrente de la mensualidad.

### Opción B: Modelo 100% Transaccional (Cero Fricción de Entrada)
Ideal para capturar rápido a las *Dark Kitchens* y tiendas de Instagram, eliminando la barrera de la suscripción mensual. Solo ganan si ellos ganan.

* **Sin mensualidad.**
* **Fee por Transacción:** $1.500 COP + 1% por orden procesada y conciliada.
  * *Por qué funciona:* El comercio lo percibe como una pasarela de pagos tradicional (como Wompi o MercadoPago), pero con el súper-poder de vender de forma autónoma por WhatsApp.

## 4. Conclusión de Viabilidad

El modelo es **altamente viable económicamente** siempre y cuando el ticket promedio (Average Order Value) del comercio sea superior a los **$15.000 COP**. 
Si intentamos aplicar esto a negocios de micro-transacciones (ej. vender tintos de $2.000 COP por WhatsApp), el costo de Meta y del LLM absorberá todo el margen. Al apuntar a *Foodtech* y *Retail B2B* (tickets de $35.000 a $500.000 COP), la economía unitaria es muy sólida.