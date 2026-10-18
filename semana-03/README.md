# Semana 03: Escalabilidad y bases de datos: Amazon DynamoDB, RDS y Aurora

**Programa:** De cero a cloud — [AWS User Group Playa Vicente](https://www.awsugplayavicente.com/)  
**Ponente invitada:** [Sairi Ávila](https://www.linkedin.com/in/sairiavila/) (AWS Community Builder en AI, AI Developer @ SICE)  
**Host:** [Roberto Flores Segundo](https://www.linkedin.com/in/roberto-flores-b1a012322/)  
**Modalidad:** Online en vivo (Discord Live)  
**Grabacion en YouTube:** [Ver clase completa en YouTube](https://www.youtube.com/watch?v=DjAbRRVF1f4)  
**Playlist oficial:** [De cero a cloud en YouTube](https://www.youtube.com/watch?v=8kL1HYphkns&list=PLGzDHDkhvPhg)

---

## 1. Lo que realmente se enseno en vivo

En esta sesión magistral a cargo de Sairi Avila se desmitifico el almacenamiento estructurado y no estructurado en AWS:

1. **Relacional (SQL) vs NoSQL en la vida real:**  
   Cuando conviene una base de datos relacional estricta (cumplimiento ACID, tablas financieras, transacciones) frente a un esquema flexible y horizontalmente escalable de documentos o clave-valor.
2. **Amazon RDS y sus mecanismos de resiliencia:**  
   Explicacion práctica del despliegue Multi-AZ (replicacion sincrona para recuperacion ante desastres) y las replicas de lectura (*Read Replicas*, replicacion asincrona para balancear trafico de consultas pesadas).
3. **La arquitectura de Amazon Aurora:**  
   Como desacopla el motor de computo del motor de almacenamiento, distribuyendo 6 copias de los datos a lo largo de 3 zonas de disponibilidad de forma automatica.
4. **Diseno práctico en Amazon DynamoDB:**  
   Creacion de una tabla sin servidores (*serverless*), seleccion adecuada de la clave de particion (*Partition Key*) y clave de ordenamiento (*Sort Key*), e insercion de registros en formato JSON.
5. **Modo de facturacion en DynamoDB:**  
   Diferencia entre capacidad provisionada (*Provisioned*) y pago por peticion (*On-Demand*), ideal para entornos de desarrollo y aprendizaje con trafico intermitente.

---

## 2. Comandos basicos para DynamoDB desde el CLI

### Crear una tabla en modo On-Demand
```bash
aws dynamodb create-table \
  --table-name EstudiantesCloud \
  --attribute-definitions AttributeName=EstudianteId,AttributeType=S \
  --key-schema AttributeName=EstudianteId,KeyType=HASH \
  --billing-mode PAY_PER_REQUEST \
  --region us-east-1
```

### Insertar un elemento
```bash
aws dynamodb put-item \
  --table-name EstudiantesCloud \
  --item '{"EstudianteId": {"S": "EST-001"}, "Nombre": {"S": "Ana"}, "Modulo": {"S": "Bases de Datos"}}'
```

---

## 3. Lecciones operativas y advertencia de costos

- **Cuidado con las instancias de RDS:** A diferencia de S3 o Lambda, una instancia de Amazon RDS (incluso en `db.t3.micro`) consume horas continuas mientras este encendida. Si se deja activa por semanas sin monitoreo, puede generar cobros al sobrepasar las 750 horas de la capa gratuita.
- **Ventaja de DynamoDB para principiantes:** En modo *Pay Per Request*, si no realizas lecturas ni escrituras, el costo mensual de almacenamiento es de $0.00 USD para tablas pequenas dentro de la cuota gratuita de 25 GB.
- **Acceso público en RDS:** En produccion, una base de datos **nunca** debe tener IP publica habilitada; debe residir en una subred privada y accederse unicamente a traves de la capa de aplicacion o un bastion seguro.
