# Semana 08: Inteligencia artificial generativa sin codigo con PartyRock y Bedrock

**Programa:** De cero a cloud — AWS User Group Playa Vicente  
**Ponente invitada:** Joselyn Lagunas (Shel Ramos, Fundadora de AWSpectrum LATAM)  
**Host:** Roberto Flores Segundo  
**Modalidad:** Online en vivo (Discord Live)  
**Grabacion en YouTube:** [Ver clase completa en YouTube](https://www.youtube.com/watch?v=MkO32Tm_kIo)  
**Playlist oficial:** [De cero a cloud en YouTube](https://www.youtube.com/watch?v=8kL1HYphkns&list=PLGzDHDkhvPhg)

---

## 1. Lo que realmente se enseno en vivo

Shel Ramos mostro como cualquier persona puede pasar de tener una idea a desplegar una aplicacion inteligente funcional en cuestion de minutos sin requerir infraestructura ni conocimientos avanzados de programacion:

1. **Introduccion a Amazon Bedrock y Modelos Fundacionales:**  
   Conceptos elementales sobre como interactuan los modelos fundacionales (FMs) de lenguaje y vision multimodal alojados en AWS.
2. **Construccion de aplicaciones con PartyRock:**  
   Uso del entorno visual [partyrock.aws](https://partyrock.aws/), que no requiere tarjeta de credito ni suscripcion previa para experimentar.
3. **Encadenamiento modular de widgets:**  
   Conexion logica entre elementos de entrada de usuario (*User Input*), generadores de texto analitico (*Text Generation*) y generadores de imagenes con Amazon Titan Image Generator.
4. **Ingenieria de prompts orientada a resultados:**  
   Tecnicas para definir roles claros, limitar el alcance de las respuestas, forzar estructuras consistentes (como tablas o viñetas tecnicas) y reducir la aparicion de datos inventados (alucinaciones).
5. **Publicacion comunitaria:**  
   Como compartir la aplicacion terminada mediante un enlace publico para que otros estudiantes y evaluadores puedan probarla en tiempo real.

---

## 2. Componentes clave utilizados en una app de PartyRock

- **User Input Widget:** Recibe el requerimiento o texto inicial proporcionado por el usuario final.
- **Prompt Widget:** Aplica la plantilla de instrucciones del sistema, incorporando referencias a variables mediante sintaxis `@Input`.
- **Image Generation Widget:** Toma la descripcion sintetica producida por el modelo de texto y la transfiere al modelo de difusion visual de Amazon Titan.

---

## 3. Lecciones operativas

- **Sensibilidad al contexto:** Los modelos fundacionales responden mejor cuando se les delimita con exactitud que rol deben asumir y cual es la audiencia de la salida (por ejemplo: "Eres un auditor de seguridad explicando un reporte a un director de tecnologia").
- **Herramienta ideal para prototipado rapido:** PartyRock demostro ser el entorno predilecto para validar ideas antes de pasar a desarrollar una solucion serverless completa con Amazon Bedrock en codigo Python o TypeScript.
