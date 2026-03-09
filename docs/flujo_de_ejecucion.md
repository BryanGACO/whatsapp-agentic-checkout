# Documento de Flujo de Ejecución: Agente Transaccional en WhatsApp

Este documento describe el ciclo de vida completo de una transacción gestionada por el Agente de Cierre y Recaudo. El diseño se basa en una arquitectura impulsada por eventos (Event-Driven) donde la fuente de verdad absoluta para la liberación de un pedido es el Webhook bancario, no el input visual del usuario.



---

## 1. Flujo Principal: De la Intención al Dinero en Cuenta (Happy Path)

Este es el escenario ideal donde el usuario interactúa, aprueba el cobro y la red bancaria (Bre-B/Nequi/DaviPlata) responde en tiempo real.

1. **Captura de Intención (Inicio de Sesión):**
   * El usuario envía un mensaje (ej. "Hola, quiero pedir una hamburguesa") al número oficial de WhatsApp del comercio.
   * El Agente de IA (LLM) interpreta la intención, presenta el catálogo interactivo y asiste al cliente en la selección de productos.

2. **Estructuración de la Orden (WhatsApp Flows):**
   * Una vez el usuario decide su compra, el Agente despliega un formulario nativo dentro de la interfaz de WhatsApp.
   * El usuario ingresa datos logísticos (dirección) y financieros (número de celular o alias de su billetera digital) sin abandonar el chat.

3. **Consolidación y Disparo del Cobro (Push API):**
   * El Servidor (Backend) calcula el valor exacto de la compra, incluyendo costos de envío o impuestos.
   * El Agente envía un **resumen estricto y no modificable** al chat para confirmación final.
   * Al confirmar, el Servidor se conecta vía API con el agregador financiero de la red Bre-B y lanza una solicitud de recaudo (Cobro "Push").

4. **Autorización del Usuario (Fricción Cero):**
   * El usuario recibe una notificación *Push* nativa en su celular proveniente de la app de su banco (ej. "El comercio X te solicita $35.000").
   * El usuario abre la notificación, se autentica con biometría en su banco y aprueba la transacción prellenada. No digita montos ni toma pantallazos.

5. **Confirmación Bancaria (Webhooks):**
   * Los servidores del banco o del agregador financiero procesan el movimiento del dinero.
   * En milisegundos, el banco dispara una alerta silenciosa (Webhook) hacia el Servidor del comercio: *"Transferencia de $35.000 exitosa para la orden #1234"*.

6. **Conciliación Automatizada:**
   * El Servidor recibe el Webhook, verifica la firma criptográfica (para evitar webhooks falsos) y cruza el monto recibido con el total esperado de la orden #1234.
   * El estado de la orden cambia en la base de datos a "Pagado".

7. **Notificación y Despacho:**
   * El Servidor instruye al Agente de WhatsApp para que envíe el mensaje de éxito: *"¡Pago confirmado! Tu orden #1234 ya está en preparación"*.
   * El sistema notifica al panel de operaciones (cocina/bodega) para liberar el producto.

---

## 2. Manejo de Excepciones y Casos Borde (Edge Cases)

La robustez del producto se mide en cómo maneja los fallos. El Agente debe estar programado para actuar proactivamente en los siguientes escenarios:

| Situación de Falla | Acción Automática y Respuesta del Agente |
| :--- | :--- |
| **Demora en el Pago (Timeout del Cliente)** | Si pasados **10 minutos** desde el envío del Push no se recibe el Webhook, el Agente envía un recordatorio: *"Hola, veo que tu orden #1234 sigue pendiente de pago. ¿Tuviste algún inconveniente con la notificación de tu banco?"* |
| **Caída de la Red (Timeout del Banco)** | Si el Servidor detecta que la API de Bre-B/Nequi está caída al intentar enviar el cobro, el Agente pausa el flujo: *"En este momento la red bancaria presenta intermitencias. Tu orden está pausada. Te avisaré cuando el sistema regrese para que puedas pagar."* |
| **Intento de Fraude (Envío de Pantallazos)** | Si el usuario sube una imagen o PDF intentando saltarse el flujo, el Agente la ignora y advierte: *"Por seguridad, nuestro sistema no procesa imágenes. Solo despacharemos tu orden cuando recibamos la confirmación interna de tu banco. Por favor aprueba la notificación en tu app."* |
| **Pago Parcial o Rechazado** | Si el usuario rechaza el cobro en su app, o el banco devuelve un Webhook de "Fondos Insuficientes", el Agente notifica: *"Tu banco ha declinado la transacción o los fondos son insuficientes. ¿Deseas intentar con otro medio de pago?"* |

---

## 3. Requisitos Técnicos para el Flujo

Para que este flujo opere sin interrupciones, se requiere la siguiente infraestructura mínima:
* **Cola de Mensajería (Message Broker):** Servicios como AWS SQS o RabbitMQ para encolar los Webhooks entrantes. Si el servidor principal se reinicia, no se perderá ninguna confirmación de pago.
* **Firmas Criptográficas (HMAC):** Todo Webhook entrante debe validar su firma. Esto evita que un atacante simule ser el banco enviando peticiones falsas al servidor.
* **Idempotencia:** El sistema debe garantizar que si el banco envía el mismo Webhook de confirmación dos veces por error de red, la orden no se procese por duplicado ni se despache dos veces.