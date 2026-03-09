# Producto — Agente de Cierre y Recaudo Automático en WhatsApp
**Industria:** Agentic Commerce / Embedded Fintech

---

## Qué construyes
Un motor de transacciones en WhatsApp que acompaña al cliente desde la intención de compra, liquida la orden y **dispara un cobro directo a su app bancaria (Nequi/DaviPlata/Bre-B)**. El agente no pide pantallazos: verifica el ingreso exacto del dinero mediante webhooks bancarios en tiempo real y cierra la venta de forma autónoma.

**Propuesta de valor central:** Convertir conversaciones en dinero verificado en cuenta, eliminando procesos manuales de conciliación y erradicando el fraude por comprobantes falsos.

---

## Por qué este producto importa ahora
El comercio conversacional está madurando, pero en Colombia (2026) choca contra el "abismo del recaudo": la fricción y la inseguridad de la transferencia manual.

- **El dolor local:** El 90% del comercio informal/social depende de transferencias donde el vendedor pierde horas cruzando chats con su app bancaria y asume el riesgo diario de estafas con comprobantes editados.
- **La infraestructura A2A (Account-to-Account):** Con la consolidación del ecosistema **Bre-B** y las APIs de billeteras digitales, los pagos inmediatos y automatizados reemplazan a los links de tarjetas de crédito, que tienen baja adopción para micropagos.
- **Señal Macro:** El 39% de retailers en Brasil ya usan WhatsApp para pedidos (Yalo, 2024). Automatizar la *tesorería* de esos pedidos es el siguiente paso lógico para rentabilizar el canal.

Desde enero 2026, **WhatsApp Business Platform permite bots orientados a negocio**. Esta solución encaja perfectamente como una herramienta de utilidad y transaccional.

---

## Qué construyes en el MVP (Rule of One)
El MVP se centra en **un solo tipo de flujo comercial** — por ejemplo, tiendas de Instagram de alto volumen o *Dark Kitchens* nocturnas que ya no dan abasto validando pagos.

Los componentes clave que implementarás:

- **WhatsApp Flows:** para capturar datos estructurados (dirección, opciones de envío, número asociado a la billetera digital).
- **Chat conversacional:** para capturar intención, responder dudas y calcular el total exacto.
- **Motor de cobro "Push" / Bre-B:** Integración vía API (directa o por agregador) para enviar la notificación de cobro al celular del cliente, eliminando la digitación manual.
- **Webhooks de Conciliación:** La base del producto. El bot "escucha" al banco y solo aprueba el despacho cuando el servidor bancario confirma la recepción de los fondos.

---

## Restricciones de diseño (críticas)

| Restricción | Cómo la manejas |
|---|---|
| **Política WhatsApp 2026** | El bot es claramente transaccional/utilitario, no de charla general. |
| **Riesgo de error (alucinación)** | Guardrail obligatorio: Resumen de orden estricto antes de disparar el cobro al banco. |
| **Fraude por pantallazos falsos** | Resuelto de raíz. El usuario no envía comprobantes; el webhook bancario es la única fuente de verdad. |
| **Inestabilidad Bancaria (Caídas de Nequi/Bre-B)** | El agente debe detectar *time-outs* de la API y avisar proactivamente: *"La red bancaria presenta demoras, tu orden está pausada hasta confirmación"*. |

---

## Señal de mercado (2026)
Delhi anunció en marzo 2026 un piloto de servicios gubernamentales con chatbot + Flows + pagos **UPI** dentro de WhatsApp. *UPI es la versión india de Bre-B/Nequi.* Esto valida globalmente que el modelo de "Trámite + Pago Account-to-Account + Conciliación automática" en el chat es el estándar del futuro, superando a los tradicionales links de tarjetas de crédito impulsados por Visa y Mastercard.