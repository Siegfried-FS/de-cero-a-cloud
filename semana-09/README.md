# Semana 09: Chatbots con IA: Amazon Lex, Bedrock, OpenSearch y Amazon S3

**Programa:** De cero a cloud — [AWS User Group Playa Vicente](https://www.awsugplayavicente.com/)  
**Ponente invitado:** [Daniel Paredes](https://www.linkedin.com/in/wallsified/) (@wallsified, Líder AWS Student Builder Group UNAM y fundador de `sudofciencias`)  
**Host:** [Roberto Flores Segundo](https://www.linkedin.com/in/roberto-flores-b1a012322/)  
**Modalidad:** Online en vivo (Discord Live)  
**Grabación en YouTube:** [Ver clase completa en YouTube](https://www.youtube.com/watch?v=ds_IrxVN-YI)  
**Playlist oficial:** [De cero a cloud en YouTube](https://www.youtube.com/watch?v=8kL1HYphkns&list=PLGzDHDkhvPhg)

---

## 1. Lo que realmente se enseñó en vivo

Daniel Paredes (estudiante de Ciencias de la Computación en la Facultad de Ciencias de la UNAM y embajador del editor Zed) presentó una arquitectura real de **Generación Aumentada por Recuperación (*RAG - Retrieval-Augmented Generation*)** a través de un proyecto lúdico y altamente técnico: **LuthorBot**.

### La premisa de LuthorBot
Inspirado en la mitología de cómics y la película de Superman, Daniel planteó: *¿Cómo construiría su asistente de inteligencia artificial un supervillano millonario como Lex Luthor para consultar debilidades tácticas de superhéroes sin alucinaciones?*

Para lograrlo, demostró cómo un modelo fundacional genérico no basta: necesita alimentarse de una base de conocimiento privada (*Knowledge Base*) indexada matemáticamente y expuesta mediante un canal conversacional.

---

## 2. Arquitectura RAG completa implementada en vivo

Daniel conectó cuatro servicios esenciales de AWS en una cadena de procesamiento sin servidores:

```
[Documentos Markdown en Amazon S3] 
       │
       ▼ (Ingesta y Chunking)
[Amazon Bedrock Knowledge Bases] ──▶ [Embeddings vectoriales con Titan]
       │
       ▼ (Indexación y Búsqueda por Proximidad)
[Amazon OpenSearch Serverless Vector Store]
       ▲
       │ (Consulta semántica enriquecida)
[Amazon Lex (Motor de Alexa) con personalidad de Lex Luthor] ◀── [Usuario]
```

### Componentes y configuración en la consola

1. **Almacenamiento de conocimiento en Amazon S3:**
   - Bucket `superhero-info-bucket` con expedientes estructurados en Markdown (`.md`) que contienen historiales, debilidades biológicas (como la radiación de kryptonita), identidades secretas y alianzas tácticas de superhéroes.
2. **Transformación en Embeddings vectoriales:**
   - Explicación matemática de los *embeddings*: convertir frases y conceptos en vectores numéricos dentro de un espacio multidimensional. Cuando el usuario pregunta, el sistema no busca coincidencias de palabras exactas, sino **proximidad semántica**.
3. **Base de datos vectorial con Amazon OpenSearch Serverless:**
   - Explicación de por qué se usa en modo Serverless: no requiere aprovisionar clústeres EC2 fijos ni pagar instancias 24/7; se paga únicamente por las unidades de computación consumidas durante la indexación y las consultas de búsqueda.
4. **Motor conversacional con Amazon Lex:**
   - Daniel explicó que **Amazon Lex** es la tecnología subyacente que le da vida al asistente de voz **Alexa**.
   - Configuración de intents, capturadores de entidades (*Slots*) y derivación automática de preguntas abiertas hacia el *Fallback Intent* conectado a la Knowledge Base de Bedrock.
   - El modelo responde sintetizando la respuesta técnica real de los documentos, pero adoptando el tono arrogante, culto y maquiavélico del personaje.

---

## 3. Lecciones operativas de IAM y buenas prácticas de seguridad

- **Bedrock jamás se ejecuta con la cuenta Root:** Daniel enfatizó que Amazon Bedrock bloquea intencionalmente ciertas operaciones si se intenta trabajar con credenciales Root. Es mandatorio crear un usuario o rol IAM con las políticas específicas para orquestar S3, Bedrock y OpenSearch.
- **Trazabilidad obligatoria para villanos y empresas:** Se configuró un segundo bucket (`lutorbot-knowledge-base-logs`) para almacenar los logs de llamadas y consultas, demostrando que ningún sistema de IA debe salir a producción sin registro de auditoría.
