# Semana 04: Seguridad práctica, IAM, auditoría en CloudTrail y mitigación

**Programa:** De cero a cloud — [AWS User Group Playa Vicente](https://www.awsugplayavicente.com/)  
**Ponente:** [Roberto Flores Segundo](https://www.linkedin.com/in/roberto-flores-b1a012322/) (Lead Auditor ISO 27001:2022)  
**Modalidad:** Online en vivo (Discord Live)  
**Grabación en YouTube:** [Ver clase completa en YouTube](https://www.youtube.com/watch?v=czvDo611i8A)  
**Playlist oficial:** [De cero a cloud en YouTube](https://www.youtube.com/watch?v=8kL1HYphkns&list=PLGzDHDkhvPhg)

---

## 1. Lo que realmente se enseñó en vivo

La cuarta sesión estuvo dedicada a la seguridad en la nube y cumplimiento normativo desde la perspectiva de auditoría de Roberto Flores (Lead Auditor ISO/IEC 27001:2022). La clase abrió con una sorpresa comunitaria: gracias a la alianza con Nica Security y donantes, se otorgaron **tres becas de 1 año de acceso completo a plataformas educativas especializadas** para los tres alumnos con entregas más disciplinadas (Luis Fernando Espinosa, Natasha Lucas y Lucas Santoli).

### El modelo de responsabilidad compartida aterrizado
- **La analogía del departamento rentado:** El casero (AWS) garantiza que no se desplome el techo, que no fallen las tuberías y que la estructura sea sólida (seguridad *de* la nube: centros de datos físicos, energía, servidores y capa de virtualización). Pero si tú dejas la puerta abierta de tu departamento con un cartel que dice "pase, es gratis", el robo es tu responsabilidad (seguridad *en* la nube: IAM, credenciales, parches, reglas de firewall y cifrado).
- **MFA obligatorio y cumplimiento normativo:** Roberto vinculó la autenticación multifactor con el control **5.2 de la norma ISO/IEC 27001:2022**, explicando por qué cualquier cuenta (desde AWS hasta correo o redes sociales) debe blindarse con MFA.
- **Higiene de contraseñas:** Demostró los riesgos de almacenar contraseñas en texto claro en navegadores web y mostró el funcionamiento de gestores seguros (Vaultwarden/Bitwarden) generando credenciales de 60 caracteres aleatorios.

---

## 2. Gestión de identidades (IAM) y principio de mínimo privilegio

- **La llave maestra vs. el gafete de turno:** Utilizar el usuario Root para tareas cotidianas es el equivalente a entregar las llaves maestras de toda tu casa para que alguien cambie un foco. El usuario Root se debe bloquear con MFA físico o virtual y guardar bajo llave.
- **Usuarios, Grupos y Roles:**
  * **Usuarios IAM:** Personas individuales con credenciales propias.
  * **Grupos IAM:** Organización por roles operativos (Desarrolladores, Finanzas, DevOps) para simplificar auditorías periódicas de accesos bajo esquemas SOC 1 Tipo 2 e ISO 27001 sin gestionar permisos usuario por usuario.
  * **Roles IAM:** Permisos temporales y rotativos asignados a servicios de AWS (como EC2 o Lambda) para interactuar entre sí sin credenciales hardcodeadas en el código fuente.
- **Anatomía de una política JSON:** Revisión de los bloques fundamentales: `Effect` (Allow/Deny), `Action` (acciones de API permitidas), `Resource` (ARN específico del recurso) y `Condition`.

---

## 3. Servicios clave de auditoría, cifrado y cumplimiento

Roberto desglosó los servicios esenciales que componen la arquitectura de seguridad y que son evaluados en el examen AWS Certified Cloud Practitioner:

1. **AWS CloudTrail:** La grabadora de caja negra de tu cuenta. Registra cada llamada a la API (quién ejecutó la acción, cuándo, desde qué IP y qué respuesta obtuvo). Se explicó cómo auditar llamadas sospechosas o intentos de escalación de privilegios.
2. **AWS WAF (Web Application Firewall):** Filtrado perimetral en capa 7 contra ataques web comunes (inyecciones SQL, ataques XSS y bots maliciosos).
3. **AWS KMS (Key Management Service):** Gestión centralizada de llaves criptográficas para cifrado de datos en reposo y en tránsito.
4. **Amazon GuardDuty y AWS Security Hub:** Monitoreo continuo con machine learning para detección de anomalías y centralización de la postura de seguridad.
5. **AWS Artifact:** El repositorio oficial donde clientes y auditores descargan los reportes de cumplimiento de AWS (reportes SOC 1, SOC 2, certificaciones ISO 27001 y PCI-DSS). Roberto relató que fue uno de los servicios que más utilizó en su etapa en seguridad de la información.

---

## 4. Reto de la semana y laboratorio práctico

1. **Laboratorio de auditoría con AWS CloudTrail:** Inspección de eventos de API y almacenamiento seguro de logs en Amazon S3.
2. **Laboratorio de IAM:** Creación estructurada de grupos, usuarios con mínimo privilegio y asignación de políticas JSON restringidas.
3. **Insignia oficial en AWS Educate:** Ruta de aprendizaje en fundamentos de ciberseguridad para añadir al perfil digital de Credly.
4. **Frase de cierre:** *"La seguridad en la nube no es un freno para la velocidad, son los frenos de un auto de carreras: están diseñados para permitirte ir más rápido con total confianza"*.
