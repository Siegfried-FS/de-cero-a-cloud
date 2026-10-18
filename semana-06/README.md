# Semana 06: Arquitecturas serverless: AWS Lambda, EventBridge y API Gateway

**Programa:** De cero a cloud — AWS User Group Playa Vicente  
**Ponente invitado:** David Jonathan Sol Llaven (Senior Cloud Architect en Caylent, AWS Community Builder y especialista Serverless)  
**Host:** Roberto Flores Segundo  
**Modalidad:** Online en vivo (Discord Live)  
**Grabacion en YouTube:** [Ver clase completa en YouTube](https://www.youtube.com/watch?v=VlJrT8vMgEg)  
**Playlist oficial:** [De cero a cloud en YouTube](https://www.youtube.com/watch?v=8kL1HYphkns&list=PLGzDHDkhvPhg)

---

## 1. Lo que realmente se enseno en vivo

David Sol guio una masterclass de nivel arquitectonico sobre como estructurar aplicaciones modernas sin la carga operativa de administrar sistemas operativos ni provisionar servidores:

1. **La filosofia serverless en produccion:**  
   No se trata de la ausencia de servidores, sino de la transferencia de la responsabilidad del escalado, la disponibilidad y los parches hacia AWS. Si nadie utiliza tu aplicacion, el costo de ejecucion es exactamente $0.00 USD.
2. **Anatomia de una funcion AWS Lambda:**  
   Analisis del manejador (*handler*), recepcion de parametros en el objeto `event`, contexto de ejecucion en `context`, configuracion de memoria y el concepto de inicio en frio (*cold start*).
3. **Exposicion de servicios con Amazon API Gateway:**  
   Configuracion de endpoints HTTP para recibir peticiones web desde navegadores o aplicaciones moviles y redirigirlas hacia la funcion Lambda correspondiente.
4. **Desacoplamiento con Amazon EventBridge:**  
   Uso del bus de eventos para crear arquitecturas guiadas por eventos (*Event-Driven Architecture*), donde un servicio emite un suceso y multiples consumidores reaccionan de forma asincrona sin bloquear el flujo principal.
5. **Capa gratuita permanente:**  
   Destacamos que AWS Lambda ofrece 1,000,000 de peticiones mensuales gratuitas de por vida, lo que lo convierte en el servicio predilecto para proyectos estudiantiles y portafolios personales.

---

## 2. Recursos y materiales oficiales compartidos por David Sol

Durante y despues de la sesion en vivo, David Sol puso a disposicion de los alumnos materiales complementarios de libre acceso:

- **Repositorio oficial en GitLab:** [gitlab.com/soldavid/20260826playavicente](https://gitlab.com/soldavid/20260826playavicente)  
  Contiene el codigo fuente, las funciones Lambda de demostracion, los esquemas de eventos y las arquitecturas de referencia analizadas en la clase.
- **Diapositivas interactivas en Canva:** [Presentacion oficial de la clase](https://canva.link/t3j2y05dwueta4v)  
  Diapositivas completas con diagramas arquitectonicos de integracion entre API Gateway, Lambda y EventBridge.
- **Perfil profesional del ponente:** [LinkedIn de David Sol](https://www.linkedin.com/in/soldavidcloud/)  
  Senior Cloud Architect en Caylent, AWS Community Builder, AWS Certified Solutions Architect - Professional y referente tecnico en computacion serverless en Latinoamerica.
- **Dinamica de evaluacion e incentivo a la comunidad:**  
  Al cierre de la sesion se realizo un Kahoot tecnico interactivo. David Sol dono generosamente **$100 USD en creditos oficiales de AWS** para el estudiante en primer lugar (Manu Morales), mientras que el AWS User Group Playa Vicente aporto **$25 USD adicionales en creditos** para el segundo lugar (Henry_to), con el fin de financiar laboratorios avanzados sin comprometer recursos personales.

---

## 3. Ejemplo basico de funcion Lambda en Python

```python
import json

def lambda_handler(event, context):
    nombre = event.get('queryStringParameters', {}).get('nombre', 'Estudiante')
    
    cuerpo_respuesta = {
        'mensaje': f'Hola {nombre}, bienvenido al modulo Serverless de De Cero a Cloud',
        'origen': 'AWS Lambda + API Gateway'
    }
    
    return {
        'statusCode': 200,
        'headers': {'Content-Type': 'application/json'},
        'body': json.dumps(cuerpo_respuesta)
    }
```

---

## 4. Lecciones operativas

- **Timeout predeterminado:** Por omision, Lambda viene configurado con un tiempo de espera de 3 segundos. Si tu funcion realiza consultas externas lentas o procesa archivos pesados, fallara con error de tiempo agotado si no ajustas el parametro de timeout adecuadamente.
- **Politica de ejecucion en IAM:** Toda funcion Lambda requiere un rol con permisos basicos (`AWSLambdaBasicExecutionRole`) para poder escribir sus registros de depuracion en Amazon CloudWatch Logs.
