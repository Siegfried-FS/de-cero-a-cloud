# Semana 02: Cómputo con Amazon EC2, modelos cloud e introducción a IAM roles

**Programa:** De cero a cloud — [AWS User Group Playa Vicente](https://www.awsugplayavicente.com/)  
**Ponente:** [Roberto Flores Segundo](https://www.linkedin.com/in/roberto-flores-b1a012322/) (Líder [AWS UG Playa Vicente](https://www.awsugplayavicente.com/))  
**Modalidad:** Online en vivo (Discord Live)  
**Grabación en YouTube:** [Ver clase completa en YouTube](https://www.youtube.com/watch?v=Q4GIVWs0qBg)  
**Playlist oficial:** [De cero a cloud en YouTube](https://www.youtube.com/watch?v=8kL1HYphkns&list=PLGzDHDkhvPhg)

---

## 1. Lo que realmente se enseñó en vivo

La segunda sesión inició reconociendo a los primeros diez estudiantes de la comunidad (de entre 132 inscritos) que completaron el reto de S3 en AWS Skill Builder, destacando la ayuda mutua en el grupo de WhatsApp para resolver errores de permisos y nombres de buckets.

### Modelos de nube explicados desde la carpintería
Roberto compartió su trayectoria como carpintero en Playa Vicente hasta obtener la beca de AWS para re:Invent en Las Vegas, utilizando esa misma vivencia para aterrizar conceptos técnicos abstractos:

- **On-Premises:** Como tener un taller físico tradicional donde eres responsable absoluto: comprar el terreno, pagar la luz, reparar maquinaria averiada y asumir meses de retraso para ampliar instalaciones. Se contrastó con la migración masiva a la nube de corporativos reales (como Chevrolet, Nu o Coppel).
- **IaaS (Infraestructura como Servicio — Amazon EC2):** El equivalente a rentar un taller con espacio, electricidad y mantenimiento de hardware garantizados por AWS. El constructor solo se encarga de la seguridad perimetral, las cerraduras y el trabajo que ejecuta adentro.
- **S3 vs. EC2:** Mientras S3 es la bodega de producto terminado donde nada se modifica al vuelo, EC2 es la máquina en el taller que recibe materia prima, ejecuta lógica y procesa solicitudes dinámicas.

---

## 2. Componentes clave de Amazon EC2 revisados en vivo

1. **AMI (Amazon Machine Image):** La plantilla del sistema operativo base. Se utilizó Amazon Linux 2023, optimizada y elegible para la capa gratuita.
2. **Tipo de instancia:** Selección de `t2.micro` (1 vCPU, 1 GB de memoria RAM). Se explicó la política de apagado obligatorio para evitar sorpresas en la facturación mensual. Como anécdota personal, Roberto relató que su primer proyecto real en AWS fue un servidor autohospedado de Bitwarden en una `t2.micro` gratuita.
3. **Security Groups:** El "portero de red" de la instancia. Se configuraron reglas de entrada (*Inbound Rules*) para el puerto 80 (tráfico web HTTP) y puerto 22 (administración remota SSH).
4. **User Data (scripts de arranque):** Automatización del aprovisionamiento para que la máquina instale el servidor web Apache/Nginx y arranque la aplicación en el primer encendido sin requerir conexión manual por terminal.
5. **IAM Roles vs. Credenciales hardcodeadas:** Demostración de por qué NUNCA se deben escribir claves de acceso (`AWS_ACCESS_KEY_ID` o contraseñas) dentro del servidor EC2, ya que los bots maliciosos escanean repositorios e instancias continuamente. En su lugar, se asocia un **IAM Role** para que la instancia obtenga credenciales temporales rotativas de forma transparente.

---

## 3. El laboratorio en vivo y experimento de seguridad

En la consola dividida en tiempo real, Roberto desplegó una arquitectura interactiva donde una instancia EC2 recibía imágenes subidas por los estudiantes y las almacenaba en un bucket de Amazon S3:

- **Verificación en vivo:** Mostró cómo la instancia interactuaba con el bucket S3 gracias al rol IAM asignado.
- **El experimento de degradación controlada:** En plena transmisión, retiró los permisos de la política del IAM Role asociado a la EC2. La aplicación web tronó en vivo al intentar subir un nuevo archivo, demostrando el impacto directo del principio de mínimo privilegio (*Least Privilege*) y cómo diagnosticar errores de autorización en AWS.

---

## 4. Reto de la semana y consejos profesionales

1. **Laboratorio en AWS Skill Builder:** Completar el módulo práctico guiado sobre cómputo en Amazon EC2.
2. **Cómo exportar tu evidencia oficial:** Roberto enseñó a navegar a la pestaña de **Logros / Historial** en Skill Builder para descargar el certificado oficial en PDF y publicarlo en LinkedIn.
3. **Consejo para entrevistas laborales:** *"Documentar todo lo que construyes te salva en una entrevista técnica. Cuando el reclutador apenas tiene 5 minutos para revisar quién eres, mostrar un repositorio documentado paso a paso demuestra curiosidad real y disciplina técnica"*.
