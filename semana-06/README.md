# Semana 06: Arquitecturas serverless: AWS Lambda, EventBridge y API Gateway

**Programa:** De cero a cloud — AWS User Group Playa Vicente  
**Ponente invitado:** David Sol (Senior Cloud Architect en Caylent, AWS Community Builder y especialista Serverless)  
**Host:** Roberto Flores Segundo  
**Modalidad:** Online en vivo (Discord Live)  
**Grabacion en YouTube:** [Ver clase completa en YouTube](https://www.youtube.com/watch?v=VlJrT8vMgEg)  
**Playlist oficial:** [De cero a cloud en YouTube](https://www.youtube.com/watch?v=8kL1HYphkns&list=PLGzDHDkhvPhg)

---

## 1. Lo que realmente se enseno en vivo

David Sol guio una masterclass de nivel arquitectonico sobre como estructurar aplicaciones modernas sin la carga operativa de administrar sistemas operativos:

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

## 2. Ejemplo basico de funcion Lambda en Python

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

## 3. Lecciones operativas

- **Timeout predeterminado:** Por omision, Lambda viene configurado con un tiempo de espera de 3 segundos. Si tu funcion realiza consultas externas lentas o procesa archivos pesados, fallara con error de tiempo agotado si no ajustas el parametro de timeout adecuadamente.
- **Politica de ejecucion en IAM:** Toda funcion Lambda requiere un rol con permisos basicos (`AWSLambdaBasicExecutionRole`) para poder escribir sus registros de depuracion en Amazon CloudWatch Logs.
