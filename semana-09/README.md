# Semana 09: Chatbots con IA: Amazon Lex, Bedrock, OpenSearch y Amazon S3

**Programa:** De cero a cloud — AWS User Group Playa Vicente  
**Ponente invitado:** Daniel Paredes (@wallsified, Lider AWS Student Builder Group UNAM)  
**Host:** Roberto Flores Segundo  
**Modalidad:** Online en vivo (Discord Live)  
**Grabacion en YouTube:** [Ver clase completa en YouTube](https://www.youtube.com/watch?v=ds_IrxVN-YI)  
**Playlist oficial:** [De cero a cloud en YouTube](https://www.youtube.com/watch?v=8kL1HYphkns&list=PLGzDHDkhvPhg)

---

## 1. Lo que realmente se enseno en vivo

Daniel Paredes presento una arquitectura completa de generacion aumentada por recuperacion (*RAG - Retrieval-Augmented Generation*) conectada a un bot conversacional interactivo:

1. **RAG sin rodeos:**  
   Como otorgar contexto privado y actualizado a modelos de lenguaje (LLMs) mediante documentos almacenados en la nube, evitando el costoso y complejo proceso de reentrenamiento (*Fine-Tuning*).
2. **Embeddings y base vectorial con OpenSearch Serverless:**  
   Conversion de documentos cargados en Amazon S3 a vectores multidimensionales mediante Amazon Titan Embeddings y almacenamiento en una coleccion de Amazon OpenSearch Serverless.
3. **Flujo conversacional con Amazon Lex V2:**  
   Diseno de intenciones (*Intents*), expresiones de entrenamiento (*Utterances*) y uso de la intencion especial `AMAZON.QnAIntent` para consultar directamente bases de conocimiento de Amazon Bedrock (*Knowledge Bases*).
4. **Demostracion practica en vivo ("LuthorBot"):**  
   Pruebas de respuestas contextualizadas basadas exclusivamente en la documentacion cargada en el bucket, demostrando como el bot rehusa responder preguntas ajenas a su base de conocimiento.
5. **Articulo tecnico de apoyo en Builder Center:**  
   [De los comics a la nube: construyendo chatbots con Lex, Bedrock, S3 y OpenSearch](https://builder.aws.com/content/3GO5EqpR0Bvo14KotkDQWKx88Yl/de-los-comics-a-la-nube-construyendo-chatbots-con-lex-bedrock-s3-y-opensearch)

---

## 2. Diagrama de arquitectura del flujo RAG

```text
[Usuario en Discord/Web] 
         │
         ▼
[Amazon Lex V2 (AMAZON.QnAIntent)]
         │
         ▼
[Amazon Bedrock Knowledge Bases] ──> [Titan Embeddings V2]
         │                                   │
         ▼                                   ▼
[Documentos en Amazon S3] ───────> [OpenSearch Serverless (Vectores)]
```

---

## 3. Lecciones operativas y advertencia critica de costos

- **Costo de OpenSearch Serverless:** OpenSearch Serverless factura por unidades de computo (*OCUs - OpenSearch Compute Units*). Incluso para pruebas cortas, mantener activa una coleccion de indexacion y busqueda puede generar un costo de entre $2.00 y $3.00 USD por pocas horas de uso.
- **Desmantelamiento inmediato obligatorio:** Al terminar la prueba, se debe eliminar la coleccion de OpenSearch Serverless y la base de conocimiento en Bedrock para evitar cargos recurrentes en la facturacion mensual.
