# 🛠️ Dominio 2: Diseñar arquitecturas resistentes

Este dominio cubre cómo diseñar sistemas distribuidos que sean tolerantes a fallos, escalables y capaces de mantener operaciones durante interrupciones o cargas impredecibles.

---

## 📚 Tabla de Contenido

- [Arquitectura resiliente con SQS y Auto Scaling](#1-️-arquitectura-resiliente-con-sqs-y-auto-scaling)

---

## 📁 Casos documentados

### 1. 🛠️ [Arquitectura resiliente con SQS y Auto Scaling](./01-job-dispatch-sqs-autoscaling/README.md)

**Resumen del problema**:  
Una aplicación distribuida necesita ser migrada a AWS, reemplazando un coordinador centralizado por una solución más escalable y tolerante a fallos.

**Solución clave**:
- Usar **SQS** para desacoplar la distribución de trabajos.
- Procesar trabajos con instancias EC2 en un **Auto Scaling Group**.
- Escalar automáticamente en base al tamaño de la cola SQS.

---

## 📌 Notas

- 

---

## 📚 Recursos adicionales

-