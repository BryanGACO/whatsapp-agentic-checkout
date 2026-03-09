# 🤖 WhatsApp Agentic Checkout (Agente de Recaudo Automático)

Un motor de transacciones impulsado por IA que convierte conversaciones de WhatsApp en dinero verificado en cuenta. Diseñado para el comercio de alto volumen en LATAM, elimina los procesos manuales de conciliación y erradica el fraude por "pantallazos" utilizando transferencias A2A (Account-to-Account) y webhooks bancarios en tiempo real.

## 🚀 Problema vs. Solución

**El Problema:** El comercio social depende de transferencias manuales. Los vendedores pierden horas cruzando chats con sus apps bancarias y asumen el riesgo diario de estafas con comprobantes editados (fraude de aplicaciones clonadas).
**Nuestra Solución:** El bot captura la intención, estructura la orden, dispara un cobro "Push" directo a la app bancaria del cliente (Bre-B/Nequi/DaviPlata) y solo aprueba el despacho cuando el servidor recibe el Webhook del banco confirmando los fondos.

## ✨ Características Principales (Core Features)

- **🛍️ WhatsApp Flows Integration:** Formularios nativos en el chat para capturar direcciones y datos de facturación sin fricción.
- **🧠 Guardrails Anti-Alucinación:** Separación estricta entre el motor conversacional (LLM) y el motor de *pricing* (Base de Datos). La IA no puede inventar precios ni descuentos.
- **💸 Cobro Push A2A (Fricción Cero):** El usuario recibe una notificación nativa de su banco con el cobro exacto prellenado. No tiene que digitar números de cuenta ni montos.
- **🔗 Conciliación Event-Driven (Webhooks):** El sistema "escucha" la red bancaria. Validación 100% criptográfica, cero dependencia de comprobantes visuales u OCR.
- **🛡️ Manejo de Excepciones Autónomo:** Detección de *timeouts* y caídas de la red bancaria con notificaciones proactivas al usuario.

## 🏗️ Arquitectura (Propuesta)

- **Canal:** WhatsApp Business Platform (Cloud API).
- **Cerebro (LLM):** OpenAI API (gpt-4o-mini) o Anthropic (Claude 3.5 Haiku) para NLU rápido y económico.
- **Backend:** Node.js (TypeScript) o Python (FastAPI) para manejar la concurrencia de webhooks.
- **Base de Datos:** PostgreSQL para estados transaccionales + Redis para encolamiento de mensajes y manejo de memoria a corto plazo del chat.
- **Integración Financiera:** API de Agregador Local (soporte Bre-B / Nequi / DaviPlata).

## ⚙️ Flujo Transaccional Básico

1. `User` -> Envía intención de compra.
2. `Agent` -> Muestra catálogo y captura datos vía WA Flows.
3. `System` -> Calcula total y envía resumen.
4. `System` -> Dispara solicitud API de recaudo al Banco.
5. `Bank` -> Envía notificación Push al celular del usuario.
6. `User` -> Aprueba el pago en su app bancaria (Huella/FaceID).
7. `Bank` -> Dispara Webhook de éxito al Servidor.
8. `System` -> Concilia orden, marca como "Pagado" y avisa al Agente.
9. `Agent` -> Notifica despacho al usuario en WhatsApp.

## 🛠️ Variables de Entorno (.env)

Para levantar este proyecto localmente, necesitarás configurar las siguientes variables (crea un archivo `.env` basado en `.env.example`):

```env
# Meta / WhatsApp
WA_PHONE_NUMBER_ID="tu_numero_id"
WA_ACCESS_TOKEN="tu_token_de_acceso"
WA_WEBHOOK_VERIFY_TOKEN="tu_token_secreto_webhook"

# IA
OPENAI_API_KEY="sk-..."

# Base de Datos
DATABASE_URL="postgresql://user:password@localhost:5432/db_name"

# Pasarela / Bre-B
PAYMENT_GATEWAY_API_KEY="tu_llave_pasarela"
PAYMENT_WEBHOOK_SECRET="tu_secreto_para_validar_firmas"
