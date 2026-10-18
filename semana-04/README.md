# Semana 04: Seguridad práctica, IAM, auditoria en CloudTrail y mitigacion

**Programa:** De cero a cloud — [AWS User Group Playa Vicente](https://www.awsugplayavicente.com/)  
**Ponente:** [Roberto Flores Segundo](https://www.linkedin.com/in/roberto-flores-b1a012322/) (Lead Auditor ISO 27001:2022 y AWS Certified Cloud Practitioner)  
**Modalidad:** Online en vivo (Discord Live)  
**Grabacion en YouTube:** [Ver clase completa en YouTube](https://www.youtube.com/watch?v=czvDo611i8A)  
**Playlist oficial:** [De cero a cloud en YouTube](https://www.youtube.com/watch?v=8kL1HYphkns&list=PLGzDHDkhvPhg)

---

## 1. Lo que realmente se enseno en vivo

En esta sesión abordamos el dominio que representa el 30% del examen CLF-C02, analizado desde la perspectiva de la auditoria operativa y el control de evidencias:

1. **Modelo de responsabilidad compartida:**  
   Delimitacion clara entre la seguridad **de** la nube (infraestructura fisica, hipervisores y centros de datos que gestiona AWS) y la seguridad **en** la nube (cifrado de datos, gestion de identidades, configuracion de firewalls y parches del sistema operativo que corresponden al usuario).
2. **Gestion de identidades y políticas de menor privilegio:**  
   Analizamos por que los roles con permisos comodin (`"Action": "*"`) son el vector mas comun de incidentes. Mostramos la estructura formal de una política JSON (`Effect`, `Action`, `Resource`, `Condition`).
3. **MFA y cuenta raiz:**  
   Buenas practicas obligatorias para bloquear la cuenta raiz, activar autenticacion multifactores y delegar tareas diarias a identidades IAM especificas.
4. **Trazabilidad y la gran trampa de CloudTrail:**  
   Demostramos como CloudTrail registra eventos de gestion (*Management Events*) de forma automatica y gratuita por 90 dias. Aclaramos por que los eventos de datos (*Data Events*, como lecturas a nivel de objetos en S3) no vienen activados por defecto: debido al volumen y al costo que implicaria en cuentas con alto trafico.
5. **Evidencias de cumplimiento con AWS Artifact:**  
   Navegacion en vivo por AWS Artifact para descargar acuerdos legales y reportes formales de auditoria como SOC 2 Type II e ISO 27001:2022.

---

## 2. Inspeccion de eventos de auditoria con AWS CLI

```bash
# Consultar los ultimos eventos de modificacion de identidades en CloudTrail
aws cloudtrail lookup-events \
  --lookup-attributes AttributeKey=EventName,AttributeValue=CreateUser \
  --max-results 5 \
  --region us-east-1
```

---

## 3. Reto práctico para obtener tu primera insignia oficial

Para obtener tu insignia de Credly vinculada a este modulo:

1. Completa el laboratorio guiado en AWS Skill Builder:
   [Introduction to AWS Identity and Access Management (IAM) - Espanol LATAM](https://skillbuilder.aws/learn/XFPX3M7HAQ/introduction-to-aws-identity-and-access-management-iam-espaol-latam/GH1QMNRZBQ)
2. Realiza el laboratorio complementario de auditoria:
   [Performing a Basic Audit of your AWS Environment - Espanol LATAM](https://skillbuilder.aws/learn/3M2AHK66HV/performing-a-basic-audit-of-your-aws-environment-espaol-latam/AW5VQJCEFM)
3. Confirma la recepcion de la notificacion en tu cuenta vinculada de Credly.

---

## 4. Leccion clave de auditoria

En una revision de cumplimiento o investigacion forense, **lo que no queda registrado en un registro de eventos formal, no existe**. Nunca asumas que un servicio esta seguro; verifica las políticas activas y audita quien tuvo acceso a que recurso mediante trazas de CloudTrail.
