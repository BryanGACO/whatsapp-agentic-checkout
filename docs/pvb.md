# AI Product Vision Board — Agente de Cierre y Recaudo Automático en WhatsApp
**Versión:** 3.0 | **Fecha:** Marzo 2026 | **Industria:** Agentic Commerce / Embedded Fintech

> Este documento aplica los frameworks del documento base *"De la Idea al Product Vision Board para Productos Agénticos"* (ai-product-base.md): AI Strategic Lens (3 Lenses), 4D Method, FTCEM, AI Decision Triangle, 3 Moats y las 5 Preguntas Incómodas. Es una evolución crítica de las versiones 1 y 2 del PVB.

---

## 1. VISIÓN

**Frase de visión:**
Ser la capa transaccional invisible que convierte cada conversación de WhatsApp en dinero verificado en cuenta — un agente autónomo que cierra ventas, erradica el fraude de comprobantes falsos y libera al comercio colombiano de alto volumen de la conciliación manual, aprovechando la ventana histórica de Bre-B (operativo desde octubre 2025) antes de que un incumbente lo empaquete.

**Test de durabilidad de la visión:**
La visión no depende de una capacidad de modelo (summarización, generación de texto) que pueda commoditizarse. Depende de la *orquestación de un workflow transaccional real* (Push A2A + Webhook + despacho) embebido en un canal de distribución masivo (WhatsApp). Esto no desaparece con GPT-5 ni GPT-6 porque el problema es de *integración financiera y operativa*, no de *generación de contenido*.

---

## 2. POSICIONAMIENTO ESTRATÉGICO (AI Strategic Lens)

### Lens 1: Market Lens — ¿Dónde jugamos?

**Arena competitiva: Disruptor (AI-Disrupted)**

No estamos creando un mercado nuevo (los comercios ya venden por WhatsApp) ni somos un incumbente agregando AI a un producto existente. Estamos *reimaginando fundamentalmente* el workflow de cobro y conciliación del social commerce: de un proceso manual, fragmentado y propenso a fraude, a uno autónomo, verificado criptográficamente y cerrado dentro del mismo chat.

**Sobrevivir a los gigantes:**

| Gigante potencial | Riesgo | Nuestra estrategia de complemento (no confrontación) |
|---|---|---|
| Meta (pagos nativos en WhatsApp) | Meta podría integrar pagos A2A nativos en WhatsApp para Colombia | Meta opera a escala global y no optimiza para la infraestructura local de Bre-B, las billeteras colombianas ni los edge cases del comercio informal. Nuestro wedge es la profundidad local: integración Bre-B + Nequi + DaviPlata + lógica de negocio del comercio (catálogos, precios, despacho). Si Meta entra, nos posicionamos como middleware especializado entre Meta Payments y el comercio. |
| Nequi / Bancolombia | El banco líder podría construir su propio bot transaccional en WhatsApp | Los bancos son buenos moviendo dinero, no construyendo experiencias conversacionales AI. Su incentivo es procesar transacciones, no resolver la operación del comercio (catálogo, pedido, despacho). Somos complementarios: usamos su infraestructura de pago, ellos ganan fees por transacción. |
| Pasarelas existentes (Wompi, MercadoPago) | Podrían integrar WhatsApp como canal | Están optimizadas para tarjeta de crédito y links de pago web. El modelo A2A con Push + Webhook es arquitectónicamente diferente. Migrar su stack requiere rediseño, no una feature más. |

### Lens 2: Value Lens — ¿Cómo ganamos?

**No es "AI Fairy Dust":** Este producto no espolvorea AI sobre un workflow viejo. Reimagina el workflow completo: la IA captura intención y acompaña al cliente, pero el valor diferencial real es el *cierre financiero autónomo* (Push A2A → Webhook → despacho automático). Sin IA el producto pierde experiencia conversacional; sin la integración bancaria, el producto no existe.

**Moat primario: Data Moat (transaccional) + Distribution Moat (WhatsApp embebido)**

| Moat | Qué poseemos / construimos | Por qué un competidor no puede copiarlo en 6 semanas |
|---|---|---|
| **Data Moat** | Cada transacción genera datos propietarios: patrones de compra por horario/barrio, tasas de éxito por billetera, tiempos de respuesta bancarios, SKUs más vendidos por tipo de comercio, tasa de abandono en cada paso del flujo. Este dataset se compone con cada comercio y transacción. | Un nuevo entrante con la misma API no tiene el dataset de comportamiento transaccional acumulado. No puede optimizar el routing de pagos, predecir timeouts bancarios ni personalizar el flujo sin meses de operación real. |
| **Distribution Moat** | Cada comercio activo es un nodo de distribución: sus clientes experimentan el flujo de pago y lo normalizan. El producto vive *dentro* del canal donde ya ocurren las ventas (WhatsApp), no en una app separada. | No requiere que el usuario descargue nada ni visite una URL. El switching cost es alto: migrar implica reconectar el número WABA, reconfigurar catálogos y reentrenar al equipo. |
| **Trust Moat** (secundario, construido con el tiempo) | Historial verificable de 0 fraudes procesados por diseño arquitectónico (no por revisión manual). Cada mes de operación sin fraude es evidencia acumulable para el siguiente cliente. | La confianza se compone lentamente. Un competidor puede clonar el feature, pero no puede clonar 6 meses de track record de cero fraudes en producción real. |

### Lens 3: Execution Lens — ¿Cómo entregamos?

**AI Decision Triangle — Optimización primaria: Speed**

| Optimizado para | Justificación |
|---|---|
| **Speed** (primario) | El caso de uso exige respuesta en tiempo real: una Dark Kitchen necesita confirmar el pago en segundos para liberar la cocina. Si el agente tarda más de lo que tardaría un humano, el comercio vuelve a la verificación manual. La latencia mata la adopción. |
| Capability (secundario) | El LLM solo necesita capacidad conversacional moderada (captura de intención, presentación de catálogo, manejo de objeciones simples). No requiere razonamiento complejo ni generación creativa. Un modelo mediano (Haiku/GPT-4o-mini) es suficiente. |
| Cost (gestionado vía arquitectura) | El costo se controla por diseño: model routing (modelo barato para interacciones simples, modelo capaz solo para edge cases), Rule Engine determinístico para cálculos financieros (cero tokens gastados en matemáticas), y context window comprimido (no se envía el historial completo, solo el estado actual del pedido). |

**Trade-offs aceptados:**
- Sacrificamos profundidad conversacional (no es un chatbot de charla abierta) a cambio de velocidad transaccional.
- El LLM no "inventa" respuestas sobre precios o disponibilidad; delega a funciones determinísticas. Esto limita la flexibilidad pero garantiza precisión financiera absoluta.

---

## 3. PROBLEMA (que persiste post-GPT-5)

**Formulación del problema:**
Los comercios de alto volumen en Colombia que venden por WhatsApp pierden dinero, tiempo y clientes porque el cobro y la conciliación son manuales, fragmentados y vulnerables a fraude. Un vendedor de Dark Kitchen un viernes en la noche debe atender 80 pedidos simultáneos Y verificar en su app bancaria si cada transferencia llegó Y detectar comprobantes falsos. El resultado: estafas diarias (168+ casos solo en Bogotá en 6 semanas de 2026), 3 horas/día de trabajo administrativo destruidas, y clientes que abandonan la compra por la fricción de cambiar de app.

**Durability Score: 4.5/5**

| Criterio | Score | Justificación |
|---|---|---|
| ¿Sobrevive a GPT-5/6? | 5/5 | El problema no es de generación de contenido (commoditizable). Es de integración financiera operativa: conectar WhatsApp → banco → despacho en tiempo real. Ningún upgrade de modelo resuelve la orquestación de webhooks bancarios ni la interoperabilidad con Bre-B. |
| ¿Podemos asegurar data defensible? | 4/5 | Sí: datos transaccionales propietarios generados por cada comercio (patrones, tasas, SKUs). El riesgo es que los agregadores financieros podrían limitar el acceso a APIs o cambiar condiciones. |
| ¿Quién controla el veto de trust? | 4/5 | El veto primario lo tiene el dueño del comercio (decisor de compra). Pero hay un veto secundario del comprador final: si desconfía de la notificación Push de su banco, la tasa de éxito cae. Bre-B aún está construyendo confianza pública. |
| **Promedio** | **4.3/5** | Por encima del umbral de 3.5. El problema es durable y accionable. |

---

## 4. SEGMENTO TARGET

**ICP — Segmento MVP (primeros 60 días):**

- **Dark Kitchens y restaurantes de alto pedido nocturno:** 30–80 órdenes/día. Ticket promedio $25,000–$60,000 COP. El tiempo entre cobro y despacho define su ventaja competitiva. No pueden parar 5 minutos por pedido a confirmar si un Nequi llegó.
- **Social Commerce de Indumentaria / Retail:** Tiendas nacidas en Instagram/TikTok con 50–150 pedidos/día. Ticket promedio $45,000–$200,000 COP. WhatsApp como canal exclusivo de venta. Han sufrido al menos 1 intento de estafa con comprobante falso.

**Segmento Ola 2 (a partir del mes 3):**
- **Distribuidores B2B mayoristas a tienderos:** Pedidos recurrentes por WhatsApp donde el cobro contra entrega genera descuadres, riesgo de efectivo y fricción operativa.

**Perfil del decisor (quién compra):**
- Dueño o gerente de operaciones con visión práctica, no técnica. Toma decisiones en semanas, no trimestres. Ya usa WhatsApp Business manualmente. Ha sido estafado o tiene miedo real de serlo. Tiene 2–5 personas dedicando horas a conciliar pagos.

**Veto holder de confianza:**
- **Primario:** El dueño del comercio. Si la primera transacción falla o genera confusión, mata la adopción.
- **Secundario:** El comprador final del comercio. Si desconfía del Push bancario (lo asocia con phishing) o la experiencia es confusa, la tasa de éxito transaccional colapsa y el comercio abandona el producto.

**Contexto de dolor máximo:**
- Picos de demanda (viernes noche, lanzamientos, días de pago).
- Picos de fraude (diciembre, día de las madres) cuando el volumen supera la capacidad de validación manual.

---

## 5. UX PARADIGM

**Paradigma elegido: Agent (actor autónomo que ejecuta tareas)**

El producto no es un assistant pasivo (que sugiere y espera aprobación humana en cada paso) ni un sistema fully autonomous (que opera sin supervisión). Es un *agente transaccional* que ejecuta autónomamente dentro de límites definidos:

- **Autonomía:** Captura intención, estructura pedido, calcula totales, dispara cobro Push, concilia webhook y libera despacho — sin intervención humana del lado del comercio.
- **Límites:** No inventa precios (Rule Engine determinístico). No acepta pantallazos (por diseño). No cierra la venta si el webhook no llega (fuente de verdad inmutable). Pausa el flujo si detecta caída bancaria.
- **Human-in-the-loop:** El comprador final autoriza el pago con su biometría. El comercio puede ver el dashboard y escalar excepciones.

**Justificación del paradigma:**
El valor del producto es precisamente que el comercio *no tiene que intervenir* en el proceso de cobro y verificación. Un paradigma "Assistant" (donde el dueño aprueba cada pago) no resuelve el cuello de botella operativo. Un paradigma "Autonomous" (sin supervisión alguna) genera riesgos de confianza en un mercado donde la desconfianza en AI financiero aún es alta.

---

## 6. PRODUCTO

**Descripción (1 frase):**
Un agente de IA en WhatsApp que acompaña al cliente desde la intención de compra, liquida la orden mediante un cobro Push directo a su app bancaria (Bre-B / Nequi / DaviPlata) y confirma el despacho automáticamente cuando el servidor bancario certifica criptográficamente el ingreso del dinero.

**Características clave (Top 5):**

1. **Captura estructurada con WhatsApp Flows:** Formularios nativos para pedido, dirección y billetera. Elimina errores de tipeo y estructura la data para el Rule Engine.
2. **Cobro Push A2A sin links externos:** Disparo de notificación de cobro directo a la app del banco del comprador. El cliente acepta con biometría. Sin salir de WhatsApp. Sin digitar montos.
3. **Conciliación vía Webhooks bancarios cifrados:** Única fuente de verdad. El agente nunca acepta imágenes, pantallazos ni confirmaciones visuales. Si el webhook no llega, la venta no cierra. Punto.
4. **Rule Engine determinístico:** El LLM captura intención; los cálculos financieros son delegados a PostgreSQL y funciones determinísticas. Cero margen de alucinación matemática.
5. **Observabilidad y manejo proactivo de intermitencias:** Monitoreo en tiempo real del estado de APIs bancarias. Si detecta caídas, pausa el flujo y notifica antes de que el dinero quede "en el limbo".

**Diferenciadores clave:**

| vs. Alternativa | Nuestro diferenciador |
|---|---|
| Bots de catálogo (mayoría del mercado) | Cierran en el catálogo y derivan a pago manual. Nosotros cerramos el ciclo financiero completo dentro del chat. |
| Validación por OCR (MoneT Check) | Leer pantallazos sigue siendo vulnerable a APKs clonadas. Nosotros eliminamos el pantallazo de la ecuación por diseño. |
| Pasarelas (Wompi, MercadoPago) | Redirigen a URL externa (fricción). Cobran 2.95% + $900 COP (tarjeta). Nuestro costo: ~$600 COP (~1.7% en ticket $35K). |
| Bre-B directo | Requiere integración técnica significativa con múltiples bancos. Nosotros ofrecemos acceso "Plug & Play" vía agregador, empaquetado en WhatsApp. |

**Fuera de alcance (decisiones de diseño, no limitaciones):**
- No acepta tarjeta de crédito/débito (solo A2A).
- No es chatbot de charla abierta ni soporte multi-tema.
- No valida pagos por imagen bajo ninguna circunstancia (irrenunciable).
- No es ERP ni sistema de inventario.
- No es viable para ticket promedio < $15,000 COP (COGS ~$600 COP destruye el margen).
- Foco exclusivo Colombia 2026 (Bre-B es infraestructura local).

---

## 7. MODELO ECONÓMICO

**Pricing model: Hybrid Tiered (SaaS + Fee Transaccional)**

Seleccionado porque alinea incentivos (ganamos más cuando el comercio procesa más), mantiene predictibilidad para el cliente (suscripción fija) y genera margen positivo desde la primera transacción.

### Unit Economics por transacción

| Componente | Costo estimado |
|---|---|
| WhatsApp Business API (Meta + BSP) | ~$60 COP |
| LLM (tokens entrada/salida, modelo mediano) | ~$60–$80 COP |
| Agregador Bre-B (flat fee webhook + conciliación) | ~$300–$500 COP |
| **COGS total por transacción exitosa** | **~$420–$640 COP** |

### Modelo de pricing (Opción recomendada: Híbrido)

| Concepto | Valor |
|---|---|
| Suscripción mensual | $150,000 COP/mes |
| Fee por transacción exitosa | $900 COP (o 1.5% del valor de la orden) |
| Margen bruto por transacción | ~$260–$480 COP (positivo desde tx #1) |

### Test de 10x escala

| Escenario | 10 comercios | 100 comercios |
|---|---|---|
| Transacciones/mes (200 tx/comercio promedio) | 2,000 | 20,000 |
| Ingreso suscripciones | $1.5M COP | $15M COP |
| Ingreso fees transaccionales | $1.8M COP | $18M COP |
| **Revenue total** | **$3.3M COP** | **$33M COP** |
| COGS transaccional (~$600 COP × tx) | $1.2M COP | $12M COP |
| **Margen bruto transaccional** | ~$2.1M COP (64%) | ~$21M COP (64%) |

**¿El pricing escala a 10x usuarios?** Sí. El margen bruto se mantiene estable porque el COGS es variable por transacción (no hay "compute multiplier" descontrolado como en productos de generación). Los costos fijos de infra (cloud, monitoreo) crecen sublinealmente. El riesgo está en el *Context Multiplier* del LLM: si las conversaciones se alargan innecesariamente, los tokens se inflan. Mitigación: WhatsApp Flows estructurados (reducen tokens) + model routing (modelo barato para 80% de interacciones).

**Umbral de viabilidad:** Ticket promedio del comercio > $15,000 COP. Por debajo, el COGS absorbe el margen. Esto es criterio de calificación de cliente, no preferencia.

---

## 8. MÉTRICAS DE ÉXITO

### User Metrics (North Star)
1. **TPV (Total Payment Volume):** Volumen total de pagos procesados. Métrica que mueve la aguja financiera.
2. **Tasa de éxito transaccional:** % de intenciones de pago que terminan en webhook exitoso. Objetivo: ≥ 85%.
3. **Bot Penetration Rate:** % de órdenes del negocio que pasan por el agente vs. manual. Objetivo: ≥ 40% mes 1, ≥ 70% mes 3.

### AI-Specific Metrics
1. **Fraud Rate:** Objetivo no negociable: 0 fraudes procesados. Por diseño arquitectónico.
2. **Latencia end-to-end:** Tiempo desde que el cliente confirma el pedido hasta que recibe la notificación Push. Objetivo: < 8 segundos.
3. **Costo de LLM por transacción exitosa:** Monitoreo continuo para detectar *cost drift* (conversaciones que se alargan, retries innecesarios, context windows inflados).
4. **Tasa de fallback a modelo caro:** % de conversaciones que escalan del modelo barato al modelo capaz. Si supera 30%, el routing necesita ajuste.

### Métricas de adopción y retención
- **Time-to-value:** ≤ 5 días hábiles desde firma hasta primera transacción exitosa.
- **Churn mensual de comercios:** ≤ 5% en primeros 6 meses.
- **NPS:** ≥ 8 en los primeros 60 días de beta.

---

## 9. GESTIÓN DE DRIFT (Engineering for Drift)

El producto opera en un entorno donde tres tipos de drift pueden degradar silenciosamente la experiencia:

| Tipo de Drift | Manifestación concreta | Sistema de detección y manejo |
|---|---|---|
| **Model Drift** | El LLM empieza a interpretar mal intenciones de compra por cambios en el lenguaje coloquial colombiano o nuevos productos/SKUs no mapeados. | Golden dataset de 200+ conversaciones reales etiquetadas. Regression tests semanales. Alerta cuando la tasa de "intención no reconocida" supere 10%. |
| **Cost Drift** | Meta cambia pricing de conversaciones. El agregador bancario ajusta el flat fee. Los tokens por conversación se inflan porque los clientes hacen más preguntas. | Dashboard de costo por transacción exitosa (no por API call). Alerta cuando COGS supere $800 COP/tx. Review mensual de token consumption promedio. |
| **Behavior Drift** | El modelo es "preciso" pero los comercios sienten que las respuestas del bot son más genéricas, más lentas o menos confiables. El NPS baja sin que ninguna métrica técnica parpadee. | Encuesta de satisfacción mensual al comercio. Tracking de "resolución en primer intento" (el cliente no necesita repetir su pedido). Señales de trust: ¿el comercio activa/desactiva el bot en picos? |

**Drift Triangle — Trade-off activo:**
- Performance ↔ Cost ↔ Trust
- Prioridad: **Trust > Speed > Cost**. Preferimos gastar más tokens en una respuesta clara que ahorrar centavos y generar confusión. La confianza del comercio es el activo más difícil de reconstruir.

---

## 10. FAILURE MODE ANALYSIS (FTCEM Framework)

| Failure Mode | Trigger | Consequence | Early Warning | Mitigation |
|---|---|---|---|---|
| **Caída de Bre-B/Nequi durante pico de demanda** | Intermitencia bancaria (documentada, frecuente) | Pagos que no se completan → comercio pierde ventas → culpa al producto → churn | Monitoreo de latencia API bancaria > 5s; spike en timeouts | Pausar flujo de cobro proactivamente. Notificar a cliente y comercio. Reintentar automáticamente cuando se estabilice. |
| **Alucinación de precio por el LLM** | Prompt ambiguo o producto con variantes complejas | Cobro incorrecto → pérdida financiera para comercio o cliente → destrucción de confianza | Discrepancia entre precio calculado por LLM vs. Rule Engine > $0 | Rule Engine es la fuente de verdad. El LLM nunca calcula precios. Guardrail: si el LLM sugiere un monto, se compara con el Rule Engine antes de presentar al cliente. Si hay discrepancia, se usa el del Rule Engine y se loguea el incidente. |
| **Webhook bancario perdido (infraestructura propia)** | Caída del servidor, reinicio durante pico, cola de mensajes saturada | Pago exitoso no confirmado → pedido no despachado → cliente furioso → doble pago o disputa | Alertas de cola SQS/RabbitMQ llena. Gap entre Push enviados y webhooks recibidos. | Colas de mensajes persistentes (SQS con dead-letter queue). Idempotencia obligatoria. Job de reconciliación periódico que cruza pagos enviados vs. confirmados. |
| **Fraude por webhook falso (atacante simula al banco)** | Atacante envía petición HTTP simulando un webhook de confirmación | Orden despachada sin pago real → pérdida financiera directa | N/A (debe prevenirse, no detectarse) | Validación de firma criptográfica HMAC en cada webhook. IP whitelist del agregador. Rechazo automático de cualquier webhook sin firma válida. |
| **Adopción baja del Push por comprador final** | Desconocimiento de Bre-B. Asociación del Push con phishing. | Tasa de éxito transaccional < 50% → comercio considera que el producto "no funciona" | Tasa de éxito < 70% en primera semana de piloto. Feedback de compradores: "no me llegó nada" / "no confío en eso". | Mensajes de educación en el flujo: "Acabas de recibir una notificación de pago de tu banco — es segura, solo apruébala." Piloto controlado con comercios que puedan comunicar el cambio a sus clientes recurrentes. |

---

## 11. LAS 5 PREGUNTAS INCÓMODAS

### 1. ¿Qué si el problema desaparece en 12 meses por commoditización de modelos?
**Respuesta:** El problema no es de OUTPUT (generar texto, resumir, traducir) sino de WORKFLOW (integración financiera + conciliación + despacho). Los modelos de lenguaje más capaces no resuelven la plomería de conectar WhatsApp → API bancaria Bre-B → Webhook → despacho. Este workflow se vuelve más valioso, no menos, conforme más comercios migran a pagos digitales. El riesgo real no es la commoditización de AI, sino que Meta integre pagos nativos o que un banco construya su propio bot. Ambos escenarios requieren años de ejecución local que nosotros podemos capturar primero.

### 2. ¿Quién realmente es dueño de la data, y podrían revocar acceso?
**Respuesta:** Dependemos de tres fuentes de data con diferentes niveles de control:
- **Data transaccional propia (alta):** Patrones de compra, tasas de éxito, SKUs, horarios. Generada por nuestro sistema. La poseemos.
- **Data de mensajería (media):** Conversaciones en WhatsApp. Meta es dueña de la plataforma y podría cambiar políticas de acceso. Mitigación: no construir dependencias exclusivas de un BSP; diseñar capa de mensajería intercambiable.
- **Data bancaria (baja):** Los webhooks vienen del agregador financiero (Cobre/TechPay), no directamente de los bancos. Si el agregador cambia condiciones, el flujo de pago se detiene. **Es la dependencia más riesgosa.** Mitigación: mantener relaciones con 2+ agregadores desde el inicio.

### 3. ¿Los reguladores se sentirían avergonzados si nuestro producto fallara públicamente?
**Respuesta:** Sí. Un fallo donde el producto confirma un pago que no existió (webhook falso o perdido) y despacha producto sin cobro sería reportado como "fraude facilitado por AI" en medios. Un fallo donde el producto cobra y no despacha (webhook recibido pero no procesado) generaría denuncias ante la SIC. **Mitigación:** Firma criptográfica obligatoria en webhooks. Colas persistentes con dead-letter queue. Job de reconciliación. Política de retención y Habeas Data (Ley 1581). Opt-in explícito del comprador. El producto debe ser más auditable y trazable que el proceso manual que reemplaza.

### 4. ¿Puede un competidor replicar este producto con la misma API en menos de 6 semanas?
**Respuesta:** Parcialmente sí, parcialmente no.
- **Sí se puede replicar en 6 semanas:** La capa conversacional (LLM + WhatsApp API). Es commodity.
- **No se puede replicar en 6 semanas:** La integración con agregador Bre-B (requiere aprobación, contratos, certificación). El número WABA aprobado (2–6 semanas solo la aprobación). El dataset de comportamiento transaccional acumulado. Los edge cases resueltos (timeouts, caídas, fraude, pedidos complejos). El trust track record de 0 fraudes en producción.
- **Conclusión:** Hay una ventana de ~6 meses donde la ejecución rápida y la acumulación de data/trust crea una barrera real. Después de eso, el moat de data y confianza se compone.

### 5. Si tenemos éxito a escala, ¿cuál es la primera forma en que trust se rompe?
**Respuesta:** El primer punto de quiebre será la **intermitencia bancaria a escala**. Con 10 comercios, una caída de Nequi a las 8pm un viernes afecta a decenas de pedidos. Con 100 comercios, afecta a miles. Si nuestro sistema de observabilidad no es rápido pausando el flujo, comercios tendrán clientes furiosos que "aprobaron el pago pero el bot dice que no llegó". La percepción será: "el bot perdió mi plata." Esto destruye confianza más rápido que cualquier bug de AI. **Mitigación primaria:** Observabilidad en tiempo real + notificación proactiva + job de reconciliación automática post-caída.

---

## 12. DISCOVERY DEBT LOG

| Hipótesis | Evidence Strength | Validation Method | Risk If Wrong | Owner | Recheck Date |
|---|---|---|---|---|---|
| Los compradores finales confían en la notificación Push de Bre-B y la aprueban sin fricción | **Weak** (no hay data propia, solo adopción general de Bre-B) | Piloto con 3 comercios: medir tasa de aprobación del Push en primeras 100 transacciones | **Existential** — si < 50% de compradores aprueban, el producto no funciona | Founder | Día 30 de piloto |
| Los comercios están dispuestos a pagar $900 COP/tx + $150K/mes por automatización | **Weak** (feedback verbal, no hay transacciones reales) | Primeros 2 contratos firmados con precio real. Medir churn a 60 días | **Existential** — sin willingness to pay no hay negocio | Founder | Día 60 |
| El agregador Bre-B (Cobre/TechPay) mantiene condiciones estables 12 meses | **Medium** (contratos iniciales firmados, pero son startups en mercado nuevo) | Review trimestral de contrato y pricing. Mantener contacto con 2 agregadores | **High** — si el agregador cierra o sube precios 3x, los unit economics colapsan | Founder | Trimestral |
| WhatsApp Flows + LLM reducen el tiempo de pedido vs. proceso manual | **Medium** (demos con comercios, reacciones positivas pero no en producción real) | A/B test: medir tiempo promedio de pedido completo con bot vs. humano en los primeros 5 comercios | **Medium** — si no es más rápido, el value prop se debilita pero no muere (el anti-fraude sigue) | Product | Día 45 |
| El LLM mediano (Haiku/GPT-4o-mini) es suficiente para la conversación de pedido | **Medium** (tests internos con prompts representativos) | Medir tasa de "intención no reconocida" y "pedido mal capturado" en primeras 500 conversaciones reales | **Low** — si falla, escalamos a modelo capaz con impacto en COGS pero no en viabilidad | Tech Lead | Día 30 |

---

## 13. HITOS 30 / 60 / 90 DÍAS (4D Method)

### Semana 1–4: DISCOVERY + MVP Build
- Firmar 2 pilotos con Dark Kitchens o retail de Instagram (ticket > $25K COP).
- Completar integración end-to-end: WhatsApp → LLM → Rule Engine → Push API (agregador Bre-B) → Webhook → confirmación.
- Iniciar proceso de aprobación WABA en paralelo (no secuencial al desarrollo).
- Procesar primeras 100 transacciones reales.
- **Validar hipótesis #1:** Tasa de aprobación del Push por comprador final ≥ 70%.

### Semana 5–8: DESIGN + Scale piloto
- Alcanzar 5 comercios activos en beta cerrada.
- 500 transacciones exitosas procesadas.
- 0 fraudes (por diseño — validar que no hubo ni un intento que penetrara).
- **Validar hipótesis #2:** Al menos 2 comercios pagando precio real sin descuento.
- NPS ≥ 8. Recopilar 3 testimonios de "cero fraude" documentados.
- Bot Penetration Rate > 40% en comercios activos.
- Implementar dashboard v1 para el comercio (órdenes, pagos, estado).

### Semana 9–12: DEVELOP + Evaluate expansion
- 10 comercios activos.
- MRR ≥ $3,000,000 COP.
- Regression tests de AI con golden dataset. Evaluar si hay model drift.
- Review de unit economics reales vs. proyectados. Ajustar pricing si es necesario.
- Evaluar go/no-go para segmento B2B mayorista.
- Evaluar go/no-go para segundo agregador financiero (reducir dependencia).

---

## 14. SUPUESTOS, RIESGOS Y DEPENDENCIAS

### Supuestos clave
- AOV del ICP > $15,000 COP (criterio de calificación, no preferencia).
- Los compradores confían en el Push de Bre-B como mecanismo de pago.
- Agregadores financieros mantienen condiciones estables 12 meses.
- Meta mantiene categoría transaccional habilitada en WhatsApp para Colombia en 2026.

### Riesgos priorizados (Probabilidad × Impacto)

| Nivel | Riesgo | Mitigación |
|---|---|---|
| CRÍTICO | Intermitencias bancarias (Bre-B/Nequi/DaviPlata) en picos de demanda | Observabilidad activa + pausa proactiva + notificación al usuario + reconciliación post-caída |
| CRÍTICO | Demora en aprobación WABA (2–6 semanas) — cuello de botella #1 del MVP | Iniciar aplicación en paralelo con desarrollo. No esperar a tener el producto listo. |
| ALTO | Baja adopción del Push por compradores finales (desconocimiento de Bre-B) | Mensajes de educación en el flujo. Piloto con comercios que puedan comunicar el cambio a clientes recurrentes. |
| ALTO | Cambios de política de Meta (pricing, restricciones de uso) | Capa de mensajería diseñada como intercambiable. No depender de un solo BSP. |
| MEDIO | Cumplimiento Ley 1581 Habeas Data | Política de privacidad, opt-in explícito, cifrado en reposo/tránsito. No es blocker para MVP pero sí para escala. |

### Dependencias bloqueantes
1. **Acceso a API de agregador financiero Bre-B** (Cobre, TechPay o equivalente): sin esto, no hay flujo de pago Push.
2. **Aprobación WABA por Meta vía BSP** (Twilio, Gupshup): sin esto, no hay producto en producción.
3. **Infraestructura cloud con colas persistentes** (SQS/RabbitMQ): sin esto, los webhooks se pierden y el trust se destruye.

---

## 15. RESUMEN EJECUTIVO (AI Product Vision Board Canvas)

```
┌─────────────────────────────────────────────────────────────────────────┐
│                    AI PRODUCT VISION BOARD v3.0                         │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                         │
│  PROBLEMA (que persiste post-GPT-5)                                    │
│  Comercios de alto volumen en WhatsApp pierden dinero, tiempo y        │
│  clientes por cobro manual, conciliación fragmentada y fraude de       │
│  comprobantes falsos. Es un problema de WORKFLOW e INTEGRACIÓN         │
│  FINANCIERA, no de generación de contenido.                            │
│                                                                         │
│  Durability Score: 4.3/5                                               │
│                                                                         │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                         │
│  SEGMENTO TARGET                                                        │
│  Dark Kitchens (30-80 tx/día, ticket $25K-$60K COP)                   │
│  Social Commerce Retail (50-150 tx/día, ticket $45K-$200K COP)        │
│                                                                         │
│  Veto holder: Dueño del comercio + comprador final (confianza Push)   │
│                                                                         │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                         │
│  MOAT PRIMARIO                                                          │
│  [x] Data Moat    [x] Distribution Moat    [ ] Trust Moat (secundario)│
│                                                                         │
│  Data transaccional propietaria que se compone con cada comercio.      │
│  Producto embebido en WhatsApp = switching cost alto.                  │
│  Track record de 0 fraudes acumulable como evidencia de trust.         │
│                                                                         │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                         │
│  ARENA COMPETITIVA                                                      │
│  [ ] Pioneer (AI-Native)                                               │
│  [x] Disruptor (AI-Disrupted)                                         │
│  [ ] Enhancer (AI-Enhanced)                                            │
│                                                                         │
│  Complementamos a los gigantes, no los confrontamos. WhatsApp no       │
│  optimiza para Bre-B local. Bancos no construyen UX conversacional.   │
│  Pasarelas están optimizadas para tarjeta, no A2A.                    │
│                                                                         │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                         │
│  UX PARADIGM                                                            │
│  [ ] Assistant                                                          │
│  [x] Agent (actor autónomo dentro de límites definidos)                │
│  [ ] Autonomous                                                         │
│  [ ] Embedded Intelligence                                              │
│                                                                         │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                         │
│  AI DECISION TRIANGLE                                                   │
│  [ ] Cost    [ ] Capability    [x] Speed                               │
│                                                                         │
│  Trade-offs: Sacrificamos profundidad conversacional por velocidad      │
│  transaccional. Modelo mediano suficiente. Rule Engine para precisión. │
│                                                                         │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                         │
│  MODELO ECONÓMICO                                                       │
│  [x] Hybrid Tiered    [ ] Usage-Based    [ ] Credit Pools             │
│  [ ] Outcome-Based    [ ] Seat+AI        [ ] Freemium                 │
│                                                                         │
│  ¿El pricing escala a 10x usuarios? [x] Sí                            │
│                                                                         │
│  COGS por transacción: ~$600 COP                                      │
│  Revenue por transacción: $900 COP + prorrateo suscripción            │
│  Gross margin transaccional: ~64%                                      │
│                                                                         │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                         │
│  MÉTRICAS DE ÉXITO                                                      │
│                                                                         │
│  User Metrics:                                                          │
│  1. TPV (Total Payment Volume)                                          │
│  2. Tasa de éxito transaccional ≥ 85%                                  │
│                                                                         │
│  AI-Specific Metrics:                                                   │
│  1. Fraud Rate = 0 (por diseño)                                        │
│  2. Latencia end-to-end < 8 segundos                                   │
│                                                                         │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                         │
│  RIESGOS CRÍTICOS                                                       │
│                                                                         │
│  1. ¿Desaparece en 12 meses? No. Es workflow, no output.              │
│  2. ¿Replicable en 6 semanas? La capa AI sí. La integración           │
│     bancaria + trust track record, no.                                  │
│  3. ¿Cómo se rompe trust a escala? Intermitencia bancaria              │
│     en picos de demanda sin observabilidad suficiente.                  │
│                                                                         │
└─────────────────────────────────────────────────────────────────────────┘
```

---

*Documento generado como evolución crítica del PVB v1 y v2, aplicando los frameworks de ai-product-base.md: AI Strategic Lens (Market, Value, Execution), 4D Method, FTCEM, AI Decision Triangle, Discovery Debt Log y las 5 Preguntas Incómodas.*
