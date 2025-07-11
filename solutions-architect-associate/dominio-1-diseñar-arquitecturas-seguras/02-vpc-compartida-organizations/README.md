# 🛡️ VPC compartida con AWS Organizations

## 📝 Descripción del problema

Una empresa utiliza múltiples cuentas AWS organizadas bajo **AWS Organizations**, donde cada departamento opera su propia cuenta con recursos como EC2 y RDS. El objetivo es facilitar un alto grado de interconectividad entre aplicaciones distribuidas sin perder control administrativo ni seguridad, permitiendo **gestión centralizada de redes**.

## ✅ Solución

Se recomienda utilizar **VPC Sharing (Uso compartido de VPC)**, una funcionalidad habilitada mediante **AWS Resource Access Manager (RAM)**.

Con esta solución:

- Una **cuenta central (propietaria)** crea y administra la VPC.
- Esta cuenta **comparte subredes específicas** con otras cuentas **miembro (participantes)** de la misma organización.
- Las cuentas participantes pueden lanzar recursos como EC2, RDS, Lambda, etc., en las subredes compartidas, pero no pueden modificar recursos de otras cuentas.

### 🔧 Beneficios

- Reducción de número de VPC gestionadas.
- Enrutamiento implícito entre recursos de la misma VPC (menor complejidad de red).
- Separación de permisos, seguridad y facturación por cuenta.
- Gestión de redes centralizada, sin comprometer la autonomía de los equipos.

---

## 🖼️ Diagrama de arquitectura

![Uso compartido de VPC con AWS Organizations](./02-vpc-compartida-organizations.png)

> 🎯 Diagrama editable: [02-vpc-compartida-organizations.drawio](./02-vpc-compartida-organizations.drawio)

---

## 🔧 Consideraciones técnicas

- El uso compartido de VPC solo está disponible entre cuentas dentro de **la misma organización de AWS Organizations**.
- Los participantes **no pueden ver ni modificar** recursos de red ni de otras cuentas, solo los suyos.
- El tráfico entre recursos en subredes compartidas **fluye mediante enrutamiento interno**, sin necesidad de VPC Peering.
- Aplica mejores prácticas de seguridad: **Security Groups** y **NACLs bien definidos**, monitoreo con **VPC Flow Logs**, y segmentación según el tipo de aplicación.

---

## 📚 Recursos útiles

- [VPC Sharing – Documentación oficial](https://docs.aws.amazon.com/vpc/latest/userguide/vpc-sharing.html)
- [Resource Access Manager](https://docs.aws.amazon.com/ram/latest/userguide/what-is.html)
- [AWS Organizations](https://docs.aws.amazon.com/organizations/latest/userguide/orgs_introduction.html)
