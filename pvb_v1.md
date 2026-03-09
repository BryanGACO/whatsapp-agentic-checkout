# Product Vision Board: Agente de Cierre y Recaudo Automático en WhatsApp

## 🧠 Vision
**Describe en una o dos frases la visión general de tu producto. ¿Por qué existe y a qué aspira?**

- Transformar WhatsApp de un simple canal de chat a un motor transaccional autónomo y seguro para el ecosistema comercial de Colombia.
- Erradicar la fricción y el fraude en el social commerce, haciendo que cobrar por chat sea tan instantáneo e invisible como enviar un mensaje.

---

## 🎯 Target Group
**Identifica a tus usuarios objetivo. ¿Quiénes son sus principales características y qué problemas les estás resolviendo?**

- **Usuarios objetivo (ICP / segmento):**
  - Dueños y gerentes de operaciones de Social Commerce de alto volumen (Retail/Moda), Dark Kitchens y distribuidores B2B a tienderos.
- **Características principales:**
  - Operan en entornos de ritmo rápido (alta transaccionalidad diaria). Su canal principal o exclusivo de ventas es WhatsApp.
- **Contexto de uso (cuándo / dónde / por qué):**
  - Durante picos de demanda (ej. viernes en la noche para restaurantes, lanzamientos de colecciones para retail), cuando el equipo humano colapsa intentando vender y cobrar simultáneamente.
- **Problemas actuales que viven:**
  - Pérdidas financieras por estafas de comprobantes falsos ("Falso Nequi").
  - Desgaste operativo extremo cruzando chats con la app del banco para conciliar pagos manualmente.

---

## 💚 Needs
**Enumera las necesidades y dolores específicos de tus usuarios. ¿Qué quieren lograr que tu producto les facilitará?**

- **Dolores / frustraciones actuales:**
  - Miedo constante a ser estafados por clientes malintencionados.
  - El cliente abandona la compra por la pereza de salir del chat, abrir su banco, digitar montos y enviar pantallazos.
- **Necesidades funcionales (qué necesitan hacer):**
  - Cobrar el monto exacto de una orden directamente en el celular del cliente y recibir confirmación bancaria automatizada sin intervención humana.
- **Necesidades emocionales (cómo quieren sentirse):**
  - Tranquilidad absoluta ("Paz mental") de que si el bot dice que la orden está pagada, la plata realmente está en la cuenta.
- **Resultado deseado (qué significa “éxito” para el usuario):**
  - Aumento en la velocidad de despacho, cero pérdidas por fraude y recuperación de horas de trabajo administrativo.

---

## 📦 Product
**Describe la solución que estás construyendo. ¿Cuáles son las características clave y cómo se diferencia de la competencia?**

- **Descripción corta del producto (1 frase):**
  - Un agente de IA en WhatsApp que atiende al cliente, estructura la orden y dispara un cobro directo a su app bancaria, conciliando el pago en tiempo real mediante webhooks.
- **Características clave (Top 3–5):**
  - Captura de intención y carrito de compras nativo vía *WhatsApp Flows*.
  - Disparo de cobro directo (Push A2A) apalancado en la red Bre-B/Nequi/DaviPlata.
  - Conciliación automática vía webhooks bancarios en segundo plano.
  - Guardrails anti-alucinación para cálculo estricto de precios.
- **Cómo funciona (resumen del flujo):**
  - Cliente pide -> IA cotiza exacto -> Cliente aprueba -> Sistema envía Push al banco del cliente -> Cliente acepta en su app bancaria -> Banco avisa al Servidor (Webhook) -> IA confirma el pago en WhatsApp y ordena el despacho.
- **Diferenciadores vs competencia / alternativas:**
  - No requiere links de pago externos (fricción cero) y prohíbe el uso de pantallazos (cero fraudes), a diferencia de las soluciones actuales que intentan leer imágenes con OCR.
- **Lo que NO es / fuera de alcance (por ahora):**
  - No es un chatbot conversacional de charla abierta. No es un ERP contable complejo. No acepta pagos con tarjeta de crédito (solo transferencias A2A/Bre-B).

---

## 📈 Business Goals
**Establece tus objetivos comerciales. ¿Qué KPIs o métricas quieres alcanzar con este producto? (e.g., ingresos, adopción, retención)**

- **Objetivo comercial principal:**
  - Validar la disposición a pagar del ICP y alcanzar un margen bruto positivo por transacción procesada.
- **KPIs principales:**
  - Volumen Total de Pagos Procesados (TPV - Total Payment Volume).
  - Tasa de éxito transaccional (% de intenciones de compra que terminan en un webhook exitoso).
- **Métricas de adopción:**
  - Tiempo de configuración (Time-to-value): Días desde que el comercio firma hasta que procesa su primer pago automático.
- **Métricas de retención / engagement:**
  - Frecuencia de uso (% de órdenes totales del negocio que pasan por el bot vs. atención manual).
- **Métricas financieras (si aplica):**
  - Ingreso Mensual Recurrente (MRR) por suscripciones + Fee Transaccional acumulado. Costo de Adquisición de Cliente (CAC) vs. Valor del Ciclo de Vida (LTV).
- **Meta inicial (ej: 30/60/90 días):**
  - Cerrar un piloto (Beta cerrada) con 3 a 5 *Dark Kitchens* o tiendas en los primeros 60 días, logrando procesar al menos 500 transacciones exitosas sin un solo fraude.

---

## ✅ Notas (opcional)
- **Supuestos clave:**
  - Los usuarios finales (compradores) confían en aprobar notificaciones Push desde su app bancaria en lugar de hacer la transferencia manual.
  - Los comercios están dispuestos a ceder un pequeño fee transaccional a cambio de la automatización.
- **Riesgos principales:**
  - Intermitencias y caídas frecuentes de la infraestructura bancaria (Nequi/Bre-B) que frustren al usuario final.
  - Cambios en las políticas de *pricing* o restricciones de casos de uso por parte de Meta (WhatsApp).
- **Dependencias (tech, partners, data, etc.):**
  - Aprobación de acceso a APIs de agregadores financieros (ej. Cobre, TechPay) para operar sobre la red Bre-B.
  - Aprobación del número oficial (WABA) por parte de un proveedor de soluciones de Meta (BSP como Twilio o Gupshup).