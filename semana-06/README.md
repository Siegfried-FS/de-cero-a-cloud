# Semana 06: Arquitecturas serverless: AWS Lambda, EventBridge y API Gateway

**Programa:** De cero a cloud — [AWS User Group Playa Vicente](https://www.awsugplayavicente.com/)  
**Ponente invitado:** [David Jonathan Sol Llaven](https://www.linkedin.com/in/soldavidcloud/) (Senior Cloud Architect en Caylent, AWS Community Builder y especialista Serverless)  
**Host:** [Roberto Flores Segundo](https://www.linkedin.com/in/roberto-flores-b1a012322/)  
**Modalidad:** Online en vivo (Discord Live)  
**Grabación en YouTube:** [Ver clase completa en YouTube](https://www.youtube.com/watch?v=VlJrT8vMgEg)  
**Playlist oficial:** [De cero a cloud en YouTube](https://www.youtube.com/watch?v=8kL1HYphkns&list=PLGzDHDkhvPhg)

---

## 1. Lo que realmente se enseñó en vivo

David Sol (arquitecto de nube con más de 30 años de experiencia técnica) impartió una clase magistral sobre la evolución de la computación, el dolor operativo del hardware tradicional y los principios de diseño serverless:

### El costo total de propiedad (TCO) y el trabajo pesado no diferenciado
- **El pasado de la infraestructura:** David relató cómo antes de la nube, alojar un sitio web obligaba a comprar mesas, contratar enlaces dedicados, tender cableado eléctrico e importar servidores físicos durante meses (*"estudié computación pero terminé haciendo albañilería y plomería"*).
- **La metáfora de la fábrica de cierres (*zippers*):** El 95% de los cierres de ropa en el mundo se fabrican en la misma planta. Un cierre perfecto no garantiza que la prenda sea hermosa; pero si el cierre falla, la prenda queda arruinada. El hardware, el sistema operativo y la plataforma son el cierre: un mal necesario que no genera valor de negocio por sí mismo. La aplicación y la solución al cliente son la prenda.
- **De IaaS a Serverless:**  
  * *IaaS:* Comprar la leche en vez de comprar la vaca (máquinas en minutos en vez de meses).  
  * *PaaS:* Delegar la plataforma y el sistema operativo al proveedor.  
  * *Serverless:* Abstracción total del servidor. **Sí existen servidores físicos**, pero el constructor se desentiende de parches, mantenimiento y aprovisionamiento para enfocarse 100% en la lógica de negocio.

---

## 2. Pilares de la arquitectura Serverless y microservicios

1. **Escalamiento automático y escala a cero:** Si no hay tráfico, el servicio reduce su capacidad a cero y **el costo es exactamente $0.00 USD**. Si un servicio te cobra cuando nadie lo usa, no es verdaderamente serverless.
2. **Ejecución basada en eventos:** Los componentes reaccionan a estímulos (una carga en S3, una petición HTTP, un mensaje en cola o una hora programada).
3. **Monolito vs. Microservicios (Cambiarle la llanta a un auto en movimiento):**
   - En un monolito estrechamente acoplado (recordando diagramas entidad-relación de 547 tablas), cambiar un campo o una función implicaba un fin de semana de alto riesgo.
   - Con microservicios se diseña con piezas intercambiables tipo Lego: se puede reemplazar un módulo sin detener el resto del sistema.
4. **AWS Lambda (FaaS - Function as a Service):**
   - Lanzado en AWS re:Invent 2014.
   - Modelo *stateless* y cobro estricto por tiempo de cómputo y número de peticiones (20 centavos de dólar por millón de invocaciones).
   - Límite de ejecución de 15 minutos por función.
   - **Principio de diseño de David Sol:**  
     > *"Las Lambdas son para transformar datos, no para transportarlos. Si tu función solo toma bytes de un lado y los pasa a otro sin procesarlos, está mal arquitectada"*.

---

## 3. Coordinación en sistemas distribuidos: Orquestación vs. Coreografía

David explicó cómo conectar servicios desacoplados para que trabajen en armonía sin generar cuellos de botella:

- **Orquestación (AWS Step Functions):** Como un **director de orquesta** parado frente a los músicos (violines, vientos, percusión). El orquestador define centralizadamente el orden, los reintentos y la gestión de errores entre múltiples pasos.
- **Coreografía (Amazon EventBridge y Amazon SNS):** Como un **flashmob o grupo de baile**. No hay un director central al frente; cada servicio conoce su coreografía y reacciona de forma autónoma cuando escucha el evento musical correspondiente.
- **Amazon SQS (Simple Queue Service):** La cola de mensajes que actúa como el **embrague o desacoplador** del sistema, absorbiendo picos de tráfico para que las funciones procesen a su propio ritmo sin saturarse.
- **Amazon API Gateway:** La puerta de entrada perimetral que expone endpoints REST/HTTP seguros y enruta las solicitudes hacia las funciones Lambda.

---

## 4. Kahoot técnico y donación de créditos oficiales ($125 USD)

Al cierre de la sesión se realizó una dinámica interactiva de alta exigencia sobre los conceptos explicados (abstracción serverless, límite de 15 minutos en Lambda, diferencia entre orquestación y coreografía, y fenómeno de *Cold Start*):

- **Primer lugar:** Manu Morales — Ganador de **$100 USD en créditos oficiales de AWS** (donados generosamente por David Sol).
- **Segundo lugar:** Henry_to (Perú) — Ganador de **$25 USD en créditos oficiales de AWS** (aportados por el AWS User Group Playa Vicente).
- **Mención honorífica:** Felipe (tercer lugar).
- **Consejo de carrera:** Ambos ponentes coincidieron en que nunca han pagado de su bolsillo por una certificación de AWS: las oportunidades, vouchers y créditos se consiguen participando activamente en comunidades, Meetups y completando retos oficiales para estudiantes.

---

## 5. Material complementario oficial de David Sol

- **Repositorio oficial de la clase:** [gitlab.com/soldavid/20260826playavicente](https://gitlab.com/soldavid/20260826playavicente)
- **Presentación interactiva en Canva:** [Ver diapositivas de Serverless](https://www.canva.com/design/DAGvdB80fT8/07s6zWp413zUaT77x87lUw/view)
- **Perfil profesional:** [David Jonathan Sol Llaven en LinkedIn](https://www.linkedin.com/in/soldavidcloud/)
