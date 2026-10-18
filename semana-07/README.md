# Semana 07: De cero a producción: desarrollo asistido por IA y AWS Amplify

**Programa:** De cero a cloud — [AWS User Group Playa Vicente](https://www.awsugplayavicente.com/)  
**Ponente invitado:** [John Kleinad](https://www.linkedin.com/in/johnkleinad/) (AWS Community Builder en Dev Tools, Full-Stack UX/UI Developer)  
**Host:** [Roberto Flores Segundo](https://www.linkedin.com/in/roberto-flores-b1a012322/)  
**Modalidad:** Online en vivo (Discord Live)  
**Grabación en YouTube:** [Ver clase completa en YouTube](https://www.youtube.com/watch?v=aL5Cj5t1i-4)  
**Playlist oficial:** [De cero a cloud en YouTube](https://www.youtube.com/watch?v=8kL1HYphkns&list=PLGzDHDkhvPhg)

---

## 1. Lo que realmente se enseñó en vivo

John Kleinad (desarrollador Full-Stack con especialidad en UX/UI y Community Builder en Dev Tools) lideró una sesión exhaustiva sobre cómo acelerar el ciclo de desarrollo de software conectando dos tecnologías clave: **AWS Amplify Gen 2** y el entorno de desarrollo con IA **Kiro IDE**.

### El salto de Frontend a Full-Stack en la nube
John relató su propia experiencia: cómo para un desarrollador frontend la consola de AWS puede resultar abrumadora por la cantidad de servicios aislados. Explicó que **AWS Amplify** actúa como un *framework como servicio* que abstrae la complejidad de la infraestructura para permitir construir aplicaciones completas y robustas a gran velocidad:
- **Autenticación sin esfuerzo:** Conexión nativa con Amazon Cognito para login, registro, tokens JWT y MFA.
- **APIs y almacenamiento de datos:** Generación automática de endpoints GraphQL en tiempo real mediante AWS AppSync y persistencia en Amazon DynamoDB.
- **Hosting global:** Despliegue continuo con CDN global integrado, gestión de dominios en Amazon Route 53 y protección con AWS WAF.

---

## 2. Arquitectura de AWS Amplify Gen 2 basada en TypeScript

John desglosó la estructura de proyectos con la nueva generación de Amplify (Gen 2), donde la infraestructura se define como código (*IaC*) usando TypeScript en una carpeta `/amplify`:

1. **`amplify/auth/resource.ts`:** Especificación de políticas de autenticación, atributos requeridos (correo, usuario, teléfono) y reglas de verificación gestionadas automáticamente en Cognito User Pools.
2. **`amplify/data/resource.ts`:** Modelado declarativo de esquemas de datos y relaciones sin escribir SQL manual.
3. **El archivo crítico `amplify_outputs.json`:** Explicó que al desplegar o iniciar un entorno, Amplify compila stacks en AWS CloudFormation y emite este archivo con las direcciones exactas, IDs de clientes y credenciales necesarias para que el cliente web (Next.js/React) se comunique con la nube.

---

## 3. Entornos Sandbox en la nube (*Cloud Sandboxes*): Salvar la memoria RAM

John abordó uno de los mayores dolores de los estudiantes y desarrolladores que trabajan con computadoras de recursos limitados (8 GB de RAM):

- **El problema de Docker local:** Levantar Docker Desktop, emuladores y bases de datos locales consume entre 4 y 6 GB de RAM, congelando la computadora e impidiendo programar con fluidez.
- **La solución con `npx ampx sandbox`:**  
  Cada desarrollador ejecuta un comando en su terminal y AWS levanta un **Sandbox efímero e independiente en la nube**.
  * Toda la base de datos (DynamoDB), la autenticación (Cognito) y las APIs serverless se ejecutan en los centros de datos de AWS.
  * La computadora del estudiante queda con el 100% de su memoria RAM libre únicamente para el editor y el servidor ligero de frontend.
  * Múltiples desarrolladores pueden trabajar en paralelo sin colisionar datos ni afectar el entorno de producción.

---

## 4. Desarrollo acelerado con Kiro IDE

John mostró cómo potenciar este flujo integrando **Kiro IDE**, el entorno de desarrollo impulsado por inteligencia artificial de AWS:
- **Flujo guiado por fases:** En lugar de autocompletar código a ciegas, Kiro estructura el proyecto recopilando requerimientos técnicos, descomponiendo la lógica en tareas y generando componentes frontend integrados directamente con el backend de Amplify.
- **Productividad real:** Demostración de cómo prototipar una aplicación interactiva con login seguro y base de datos conectada en cuestión de minutos sin configurar servidores manualmente.
