# Semana 05: Redes en la nube: Amazon VPC, subredes y acceso seguro con SSM

**Programa:** De cero a cloud — AWS User Group Playa Vicente  
**Ponente:** Roberto Flores Segundo (Lider AWS UG Playa Vicente)  
**Modalidad:** Online en vivo (Discord Live)  
**Grabacion en YouTube:** [Ver clase completa en YouTube](https://www.youtube.com/watch?v=RcCGLSTSV0U)  
**Playlist oficial:** [De cero a cloud en YouTube](https://www.youtube.com/watch?v=8kL1HYphkns&list=PLGzDHDkhvPhg)

---

## 1. Lo que realmente se enseno en vivo

En esta clase construimos la topologia de red que sustenta cualquier arquitectura empresarial en la nube, cuidando de no incurrir en gastos involuntarios:

1. **Creacion de una VPC desde cero:**  
   Asignacion de bloque CIDR principal (`10.0.0.0/16`) y explicacion de calculo de mascaras de red para dimensionar subredes sin desperdiciar direcciones IP privadas.
2. **Subred publica vs subred privada:**  
   - **Subred publica (`10.0.1.0/24`):** Conectada a un Internet Gateway (IGW) mediante una tabla de ruteo con destino `0.0.0.0/0`.
   - **Subred privada (`10.0.2.0/24`):** Aislada de conexiones directas desde el exterior, pensada para bases de datos y logica de backend.
3. **El riesgo financiero de los NAT Gateways:**  
   Advertimos que un NAT Gateway administrado tiene un costo base aproximado de $32 USD mensuales aunque no transmita datos. En su lugar, ensenamos a conectar servicios de almacenamiento mediante **VPC Gateway Endpoints** para Amazon S3, los cuales son 100% gratuitos y mantienen el trafico viajando de forma segura dentro de la red interna de AWS.
4. **Firewalls en dos niveles (Security Groups vs NACLs):**  
   Demostracion practica de la diferencia entre Security Groups (con estado, aplican a nivel de interfaz de red de la instancia) y Network ACLs (sin estado, aplican a nivel de toda la subred y requieren numeracion secuencial de reglas de entrada y salida).
5. **Acceso administrativo sin SSH (Puerto 22 cerrado):**  
   Configuracion de endpoints y roles para interactuar con la terminal de instancias en subredes privadas mediante AWS Systems Manager Session Manager.

---

## 2. Creacion de un VPC Endpoint gratuito para Amazon S3

```bash
# Crear un Gateway Endpoint hacia S3 sin costo asociado
aws ec2 create-vpc-endpoint \
  --vpc-id vpc-0123456789abcdef0 \
  --service-name com.amazonaws.us-east-1.s3 \
  --route-table-ids rtb-0123456789abcdef0 \
  --region us-east-1
```

---

## 3. Reto mayor: AWS Cloud Quest (Cloud Practitioner)

A partir de esta sesion se abrio el reto principal para los alumnos:

- **Plataforma:** [AWS Cloud Quest en Skill Builder](https://skillbuilder.aws/learn/FU5WCYVGKY/aws-cloud-quest-cloud-practitioner/UBG3N32DBX)
- **Objetivo:** Recorrer la ciudad virtual completando misiones practicas de redes, computo y bases de datos.
- **Premio oficial:** Insignia digital oficial en Credly que certifica la resolucion autonoma de laboratorios practicos.
