# 🛡️ Dominio 1: Diseñar arquitecturas seguras

Este dominio se centra en cómo proteger la infraestructura de AWS mediante el uso de mecanismos como control de acceso, cifrado, aislamiento de red y prácticas de privilegios mínimos.

---

## 📚 Tabla de Contenido

- [🔐 Lambda accediendo a S3 en otra cuenta](#1--lambda-accediendo-a-s3-en-otra-cuenta)
- [🛡️ VPC compartida con AWS Organizations](#2-️-vpc-compartida-con-aws-organizations)
- [Rotación de credenciales RDS multirregional con Secrets Manager](#3--rotación-de-credenciales-rds-multirregional-con-secrets-manager)
- [Control de salida IPv6 con Egress-Only Gateway y AWS Network Firewall](#4--control-de-salida-ipv6-con-egress-only-gateway-y-aws-network-firewall)
- [Bloqueo inmediato de IPs maliciosas con NACL](#5--bloqueo-inmediato-de-ips-maliciosas-con-nacl)
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



### 4. 🔐 [Control de salida IPv6 con Egress-Only Gateway y AWS Network Firewall](./04-egress-only-firewall-ipv6/README.md)

**Resumen del problema**:  
Una instancia EC2 en una VPC IPv6 debe comunicarse hacia internet, pero sin aceptar tráfico entrante, y con inspección de tráfico saliente.

**Solución clave**:
- Lanzar EC2 en subred privada.
- Usar Egress-Only Internet Gateway para salida IPv6.
- Inspeccionar y filtrar tráfico con AWS Network Firewall.



### 5. 🔐 [Bloqueo inmediato de IPs maliciosas con NACL](./05-bloqueo-ip-nacl/README.md)

**Resumen del problema**:  
La aplicación recibe millones de solicitudes desde unas pocas IP maliciosas, causando degradación de rendimiento.

**Solución clave**:
- Aplicar reglas `DENY` en NACLs asociadas a las subredes del nivel web (ALB).
- Bloquear IPs ofensivas directamente a nivel de red.
- Mitigar el impacto mientras se implementa una solución más completa como WAF.

---

## 📌 Notas

- Se recomienda aplicar el principio de menor privilegio en todas las políticas.
- Las credenciales STS usadas por Lambda son seguras, temporales y gestionadas automáticamente por AWS.

---

## 📚 Recursos adicionales

