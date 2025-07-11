# ⚡ Dominio 3: Diseñar arquitecturas de alto rendimiento

Este dominio evalúa tu capacidad para diseñar soluciones que sean escalables, eficientes y rápidas bajo carga. Aquí encontrarás casos prácticos con sus respectivas soluciones arquitectónicas, diagramas y buenas prácticas.

---

## 📚 Tabla de Contenido

- [Lambda dentro de una VPC](#1--lambda-dentro-de-una-vpc)
- [Transmisión de datos desde S3 a Kinesis con AWS DMS](#2--transmisión-de-datos-desde-s3-a-kinesis-con-aws-dms)
- [Desacoplamiento a gran escala con SNS + SQS](#3--desacoplamiento-a-gran-escala-con-sns--sqs)
- [Procesamiento ordenado de pedidos con API Gateway + FIFO SQS + Lambda](#4--procesamiento-ordenado-de-pedidos-con-api-gateway--fifo-sqs--lambda)
- [Optimización de rendimiento web con CloudFront + S3 + ALB + Route 53](#5--optimización-de-rendimiento-web-con-cloudfront--s3--alb--route-53)
- [Escalado de lecturas con Aurora Replicas y Auto Scaling](#6--escalado-de-lecturas-con-aurora-replicas-y-auto-scaling)
- [📌 Notas](#-notas)
- [📚 Recursos complementarios](#-recursos-complementarios)

---

## 📁 Casos documentados

### 1. 🧠 [Lambda dentro de una VPC](./01-lambda-vpc/README.md)

**Resumen del problema**:  
Se requiere migrar una aplicación a arquitectura sin servidor. La función Lambda necesita acceder a recursos privados como RDS, pero también conservar la capacidad de conectarse a servicios públicos de AWS.

**Solución clave**:
- Asociar Lambda a una VPC solo cuando necesite acceder a recursos privados.
- Configurar una NAT Gateway en una subred pública para mantener acceso a Internet.
- Ajustar tablas de rutas y permisos adecuados (IAM + Security Groups).

### 2. ⚡ [Transmisión de datos desde S3 a Kinesis con AWS DMS](./02-s3-to-kinesis-dms/README.md)

**Resumen del problema**:  
La empresa necesita transmitir archivos históricos y actualizaciones de S3 a Kinesis para análisis en tiempo real, en el menor tiempo posible.

**Solución clave**:
- Usar **AWS DMS** como puente entre S3 y Kinesis.
- Sin necesidad de desarrollo de código.
- Soporta procesamiento completo y de cambios (CDC).
- Los consumidores en Kinesis pueden escalar de forma independiente.


### 3. ⚡ [Desacoplamiento a gran escala con SNS + SQS](./03-sns-sqs-fanout/README.md)

**Resumen del problema**:  
Una aplicación publica mensajes en volúmenes que pueden llegar a 100,000 por segundo. Decenas de aplicaciones consumidoras deben procesarlos sin afectar al productor ni entre ellas.

**Solución clave**:
- Utilizar un tema SNS como punto de entrada.
- Conectar múltiples colas SQS como suscriptores (fan-out).
- Cada consumidor procesa mensajes desde su cola.
- Arquitectura desacoplada, escalable y tolerante a fallos.


### 4. 🛒 [Procesamiento ordenado de pedidos con API Gateway + FIFO SQS + Lambda](./04-api-orders-fifo-sqs-lambda/README.md)

**Resumen del problema**:  
Se requiere procesar pedidos en el mismo orden en que llegan desde una aplicación web. La solución debe ser escalable, sin pérdida ni duplicación de mensajes.

**Solución clave**:
- Usar API Gateway como endpoint de recepción.
- Publicar en una cola FIFO de SQS.
- Invocar una función Lambda desde la cola para procesar cada pedido en orden.

### 5. 🌍 [Optimización de rendimiento web con CloudFront + S3 + ALB + Route 53](./05-cloudfront-s3-alb/README.md)

**Resumen del problema**:  
Una aplicación web global necesita reducir la latencia tanto en contenido estático como dinámico.

**Solución clave**:
- Usar CloudFront con múltiples orígenes (S3 + ALB).
- Enrutar el tráfico del dominio personalizado con Route 53.
- Cachear el contenido estático y distribuir dinámicamente el dinámico.



### 6. 🧩 [Escalado de lecturas con Aurora Replicas y Auto Scaling](./06-aurora-replicas-autoscaling/README.md)

**Resumen del problema**:  
Una base de datos en EC2 no escala adecuadamente para atender una aplicación con muchas lecturas.

**Solución clave**:
- Migrar a Amazon Aurora con implementación Multi-AZ.
- Habilitar Aurora Auto Scaling para crear/detener réplicas de forma dinámica.
- Balancear el tráfico de lectura mediante Aurora Reader Endpoint.


---

## 📌 Notas

- Cada solución está acompañada de un diagrama visual y editable para que puedas adaptar los casos a tus propios escenarios.
- Sigue las recomendaciones del AWS Well-Architected Framework, especialmente el pilar de **eficiencia del rendimiento**.

---

## 📚 Recursos complementarios

- [Well-Architected Framework – Performance Efficiency Pillar](https://docs.aws.amazon.com/wellarchitected/latest/performance-efficiency-pillar/)

