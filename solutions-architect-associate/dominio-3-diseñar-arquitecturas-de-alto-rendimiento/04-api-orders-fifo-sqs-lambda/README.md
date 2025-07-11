# 🛒 Procesamiento ordenado de pedidos con API Gateway, SQS FIFO y Lambda

## 📝 Descripción del problema

Una empresa está desarrollando una aplicación web de comercio electrónico que envía información de nuevos pedidos a través de una API REST expuesta mediante **Amazon API Gateway**. El objetivo es asegurar que **los pedidos se procesen en el orden exacto en que se reciben**, sin duplicación ni pérdida de eventos.

## ✅ Solución

Se implementa una arquitectura basada en eventos utilizando los siguientes servicios de AWS:

1. **Amazon API Gateway**: recibe solicitudes HTTP de nuevos pedidos.
2. **Amazon SQS FIFO Queue (First-In, First-Out)**: asegura que los pedidos se procesen en **el mismo orden en que se enviaron**.
3. **AWS Lambda**: suscrita a la cola FIFO para procesar los pedidos de forma automática y sin intervención manual.

- Este patrón desacopla la capa de recepción de la capa de procesamiento, y al usar una **cola FIFO**, se garantiza el **orden estricto** de los mensajes.
    API Gateway captura el pedido y lo envía de manera confiable a la cola SQS FIFO. La cola actúa como un búfer y garantiza el orden. Lambda procesa los pedidos uno por uno (o en lotes ordenados) desde la cola. Esto cumple con el requisito de orden estricto de manera escalable y resiliente.
---

## 🖼️ Diagrama de arquitectura

![API Gateway -> FIFO SQS -> Lambda](./04-api-orders-fifo-sqs-lambda.png)

> 🎯 Diagrama editable: [04-api-orders-fifo-sqs-lambda.drawio](./04-api-orders-fifo-sqs-lambda.drawio)

---

## 💡 Beneficios clave

- ✅ **Orden garantizado** de procesamiento (FIFO con `MessageGroupId`).
- 🔄 **Alta disponibilidad** y resiliencia frente a picos de tráfico.
- 🔀 **Desacoplamiento** entre recepción y procesamiento.
- ⚙️ **Escalabilidad automática** con Lambda para el procesamiento.
- 🧹 **Tolerancia a fallos** con reintentos y Dead Letter Queue (opcional).

---

## 🔧 Consideraciones

- La cola **SQS debe ser FIFO**, no estándar.
- Se debe establecer correctamente el `MessageGroupId` para asegurar el orden dentro del grupo.
- El **API Gateway** debe tener integración directa con SQS o a través de un proxy Lambda.
- Configura el **concurrency limit de Lambda** si necesitas procesamiento estrictamente secuencial.
- Usa **DLQ (Dead Letter Queue)** para capturar mensajes que fallen repetidamente.

---

## 📚 Recursos útiles

- [API Gateway Integration with SQS](https://docs.aws.amazon.com/prescriptive-guidance/latest/patterns/integrate-amazon-api-gateway-with-amazon-sqs-to-handle-asynchronous-rest-apis.html)
