# Semana 05: Redes en la nube: Amazon VPC, subredes y acceso seguro con SSM

**Programa:** De cero a cloud — [AWS User Group Playa Vicente](https://www.awsugplayavicente.com/)  
**Ponente:** [Roberto Flores Segundo](https://www.linkedin.com/in/roberto-flores-b1a012322/) (Líder [AWS UG Playa Vicente](https://www.awsugplayavicente.com/))  
**Modalidad:** Online en vivo (Discord Live)  
**Grabación en YouTube:** [Ver clase completa en YouTube](https://www.youtube.com/watch?v=RcCGLSTSV0U)  
**Playlist oficial:** [De cero a cloud en YouTube](https://www.youtube.com/watch?v=8kL1HYphkns&list=PLGzDHDkhvPhg)

---

## 1. Lo que realmente se enseñó en vivo

Roberto inició la sesión explicando la infraestructura global de AWS, la nomenclatura estandarizada de regiones y centros de datos, y los casos de cumplimiento normativo que obligan a considerar la ubicación física de las cargas de trabajo:

### Anatomía de regiones y Zonas de Disponibilidad (AZs)
- **Nomenclatura técnica:** Cómo descifrar códigos como `us-east-1` (País `us` + Punto cardinal `east` + Número `1`) o zonas específicas como `us-east-1a`, `us-east-1b`.
- **Soberanía de datos y regulación bancaria:** Roberto compartió su experiencia en auditorías con la Comisión Nacional Bancaria y de Valores (CNBV) en México, donde ciertas regulaciones financieras prohíben estrictamente que la información sensible de clientes salga del territorio nacional, contextualizando la relevancia de la región local de AWS en Querétaro (`mx-central-1`).
- **Diferencia de costos entre regiones:** El costo de energía, agua y regulaciones locales varía entre Virginia, Oregón, São Paulo o Europa, impactando la factura final de cómputo.
- **Zonas de Disponibilidad independientes:** Centros de datos físicos separados por kilómetros con suministro eléctrico, enfriamiento y conectividad redundante para resistir desastres naturales o cortes mayores.

---

## 2. Amazon VPC explicada con la analogía del fraccionamiento privado

Para simplificar conceptos densos de redes, Roberto utilizó la analogía de un desarrollo habitacional cerrado:

- **Amazon VPC (Virtual Private Cloud):** Es el **fraccionamiento privado completo**, delimitado por bardas perimetrales y con un rango de direcciones IP asignado (CIDR, ej. `10.0.0.0/16`). Nadie entra sin autorización.
- **Subredes (Subnets):** Son las **calles o privadas internas** dentro del fraccionamiento:
  * *Subred pública (`10.0.1.0/24`):* Calles con vista y acceso directo a la entrada principal.
  * *Subred privada (`10.0.2.0/24`):* Calles interiores sin salida exterior directa, diseñadas para proteger bases de datos y servidores backend.
- **Internet Gateway (IGW):** La **caseta de vigilancia principal** con pluma de acceso hacia la avenida pública exterior (Internet).
- **Tablas de ruteo (*Route Tables*):** Los **señalamientos viales** que dictan el flujo de tráfico: si una calle tiene ruta hacia el Internet Gateway (`0.0.0.0/0 -> igw-xxxx`), se convierte en pública.
- **Security Groups vs. Network ACLs:**
  * *Security Group:* El guardia de seguridad privado en la puerta de tu casa (opera a nivel de instancia, con estado / *stateful*).
  * *NACL (Network Access Control List):* El retén perimetral a la entrada de toda la calle (opera a nivel de subred, sin estado / *stateless*).

---

## 3. Direcciones IP y la trampa de costos con IPs Elásticas

Roberto desglosó los tres tipos de direcciones IP en Amazon EC2 y sus reglas de facturación:

1. **IP Privada (Interna):** Como la extensión telefónica interna de una oficina. Es fija durante la vida útil de la instancia e invisible desde el internet público.
2. **IP Pública Dinámica (Efímera):** Como la llave prestada de una habitación de hotel. Es gratuita mientras la instancia esté encendida, pero cambia automáticamente al apagarla o reiniciarla.
3. **IP Elástica (*Elastic IP*):** Como un número telefónico móvil personal reservado. Permanece fijo sin importar cuántas veces reinicies o reemplaces el servidor.
4. **Principio fundamental de costos ($0.00 USD):**  
   > Una IP Elástica que esté reservada en tu cuenta pero **NO esté asociada a una instancia encendida genera un cobro por hora**. AWS implementó esta regla para penalizar el desperdicio de direcciones IPv4 públicas escasas. Al terminar una práctica, la IP elástica debe liberarse (*Release*).

---

## 4. Kiro IDE financiado con cupones y Kahoot comunitario

Al cierre de la clase, Roberto mostró cómo utilizar herramientas modernas de desarrollo con IA sin gastar de tu propio bolsillo:

- **Demostración de Kiro IDE:** Mostró el flujo de trabajo estructurado de Kiro en terminal y escritorio: generación de especificación de requerimientos, desglose de tareas técnicas y ejecución de código asistido.
- **Estrategia para financiar Kiro Pro:** Explicó cómo aplicar cupones de eventos comunitarios ($25 USD) directamente en el panel de facturación de AWS para activar la suscripción mensual de Kiro Pro ($20 USD) y conservar $5 USD para laboratorios adicionales sin ingresar tarjetas de crédito personales.
- **Kahoot en vivo con premios:** Se realizó una dinámica interactiva de preguntas y respuestas sobre las primeras 5 semanas, donde el User Group premió a los ganadores con créditos oficiales de AWS.
