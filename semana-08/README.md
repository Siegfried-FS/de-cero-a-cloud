# Semana 08: Inteligencia artificial generativa sin código con PartyRock y Bedrock

**Programa:** De cero a cloud — [AWS User Group Playa Vicente](https://www.awsugplayavicente.com/)  
**Ponente invitada:** [Joselyn Lagunas](https://www.linkedin.com/in/joselyn-lagunas/) (Shel Ramos, Fundadora de AWSpectrum LATAM y Community Builder en Machine Learning)  
**Host:** [Roberto Flores Segundo](https://www.linkedin.com/in/roberto-flores-b1a012322/)  
**Modalidad:** Online en vivo (Discord Live)  
**Grabación en YouTube:** [Ver clase completa en YouTube](https://www.youtube.com/watch?v=MkO32Tm_kIo)  
**Playlist oficial:** [De cero a cloud en YouTube](https://www.youtube.com/watch?v=8kL1HYphkns&list=PLGzDHDkhvPhg)

---

## 1. Lo que realmente se enseñó en vivo

Joselyn Lagunas (Shel Ramos, líder de la comunidad oficial AWSpectrum LATAM y de Quantum Observers) dirigió un workshop práctico para construir aplicaciones de inteligencia artificial generativa funcionales en minutos, sin necesidad de escribir código ni registrar tarjetas de crédito:

### De la IA predictiva tradicional a los modelos fundacionales
- **IA Tradicional (Clasificación):** Recibe datos o imágenes y clasifica según patrones fijos (ej. determinar si una imagen contiene un gato o un perro).
- **IA Generativa:** A partir de instrucciones en lenguaje natural (*prompts*) y contexto, interactúa con modelos fundacionales preentrenados (disponibles en Amazon Bedrock) para sintetizar contenido completamente nuevo: texto, código, imágenes hiperrealistas, audio y modelos 3D.
- **Acceso universal sin barreras financieras:** Se utilizó **PartyRock** (el entorno lúdico de prototipado rápido impulsado por Amazon Bedrock), demostrando que cualquier estudiante puede acceder gratuitamente iniciando sesión con Google, Apple o AWS Builder ID sin ingresar datos bancarios.

---

## 2. Ingeniería de prompts (*Prompt Engineering*) estructurada por capas

Shel Ramos desmitificó la creencia de que la IA "adivina" o "busca respuestas en una lista prefabricada". Enseñó a formular prompts con rigor técnico para evitar resultados genéricos:

1. **Mal prompt vs. Buen prompt:**  
   * *Mal prompt:* `"Dime mi Pokémon"`. El modelo carece de contexto y genera respuestas predecibles y planas.  
   * *Buen prompt:* Estructuración por capas con rol, contexto y restricciones explícitas.
2. **Los cuatro bloques de un prompt profesional:**
   - **Rol:** Asignar una identidad clara al modelo (*"Eres un sabio y místico adivino de Pokémon..."*).
   - **Contexto y variables:** Inyección dinámica de entradas del usuario (`@nombre`, `@tecnología_favorita`, `@personalidad`).
   - **Tarea concreta:** Instrucción unívoca (*"Selecciona el Pokémon que mejor represente las fortalezas del usuario y vaticina su futuro como arquitecto cloud"*).
   - **Restricciones y formato de salida (*Guardrails*):** Límites de extensión (ej. menos de 100 palabras), tono de comunicación y estructura fija de salida para evitar divagaciones.

---

## 3. Construcción en vivo de la aplicación en PartyRock

En la pantalla en vivo, Shel construyó paso a paso la aplicación *"Adivinador de Pokémon y tu futuro tecnológico"*:

- **Composición modular con Widgets:**
  * `User Input`: Bloques interactivos donde el usuario ingresa su nombre, su stack técnico preferido y sus rasgos de personalidad.
  * `Text Generation`: Conexión de variables mediante menciones (`@nombre`, `@tecnología`) para redactar la predicción personalizada.
  * `Image Generation`: Generación automática de una ilustración del Pokémon seleccionado en un entorno de servidores y centros de datos de AWS.
  * `File Upload`: Demostró cómo adjuntar una lista externa de Pokémons oficiales para evitar **alucinaciones** (evitando que el modelo invente criaturas que no existen).
- **El asistente Whiskers:** Uso de la herramienta interna de PartyRock para auditar la calidad y claridad de los prompts en cada widget antes de publicar.
- **Publicación y compartición comunitaria:** Cómo generar el enlace público de la aplicación con un solo clic para que cualquier compañero de la comunidad la pruebe e interactúe en vivo.
