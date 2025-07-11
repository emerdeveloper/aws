# 🛡️ Dominio 1: Diseñar arquitecturas seguras

Este dominio se centra en cómo proteger la infraestructura de AWS mediante el uso de mecanismos como control de acceso, cifrado, aislamiento de red y prácticas de privilegios mínimos.

---

## 📚 Tabla de Contenido

- [🔐 Lambda accediendo a S3 en otra cuenta](#1--lambda-accediendo-a-s3-en-otra-cuenta)
- [🛡️ VPC compartida con AWS Organizations](#2-️-vpc-compartida-con-aws-organizations)
- [Rotación de credenciales RDS multirregional con Secrets Manager](#3--rotación-de-credenciales-rds-multirregional-con-secrets-manager)
- [📌 Notas](#-notas)
- [📚 Recursos complementarios](#-recursos-complementarios)


---

## 📁 Casos documentados

### 1. 🔐 [Lambda accediendo a S3 en otra cuenta](./01-lambda-access-s3-another-account/README.md)

**Resumen del problema**:  
Una función Lambda en la Cuenta A necesita acceder a un bucket S3 ubicado en la Cuenta B.

**Solución clave**:
- Crear un rol IAM en la Cuenta A con permisos sobre el bucket.
- Asociar este rol a la función Lambda.
- Actualizar la política del bucket en la Cuenta B para permitir el acceso al rol.
- Lambda utilizará credenciales temporales STS automáticamente.


### 2. 🛡️ [VPC compartida con AWS Organizations](./02-vpc-compartida-organizations/README.md)

**Resumen del problema**:  
Varios departamentos usan cuentas separadas de AWS y necesitan una red compartida con alto grado de interconectividad y administración centralizada.

**Solución clave**:
- Crear VPC en una cuenta propietaria y compartir subredes con otras cuentas mediante AWS Resource Access Manager.
- Las cuentas participantes pueden desplegar recursos propios sin gestionar infraestructura de red.
- Tráfico interno entre instancias sin necesidad de VPC Peering.


### 3. 🔐 [Rotación de credenciales RDS multirregional con Secrets Manager](./03-secrets-manager-rotation-multiregion/README.md)

**Resumen del problema**:  
Durante mantenimientos mensuales, una empresa necesita rotar credenciales de RDS en múltiples regiones sin procesos manuales.

**Solución clave**:
- Usar AWS Secrets Manager con rotación automática.
- Habilitar replicación multirregional del secreto.
- Integrar con RDS for MySQL sin escribir código adicional.


---

## 📌 Notas

- Se recomienda aplicar el principio de menor privilegio en todas las políticas.
- Las credenciales STS usadas por Lambda son seguras, temporales y gestionadas automáticamente por AWS.

---

## 📚 Recursos adicionales

