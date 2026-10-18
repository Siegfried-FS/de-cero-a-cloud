# Semana 07: De cero a produccion: desarrollo asistido por IA y AWS Amplify

**Programa:** De cero a cloud — [AWS User Group Playa Vicente](https://www.awsugplayavicente.com/)  
**Ponente invitado:** John Kleinad (AWS Community Builder en Dev Tools, Full-Stack Dev UX|UI & Cloud Engineer)  
**Host:** Roberto Flores Segundo  
**Modalidad:** Online en vivo (Discord Live)  
**Grabacion en YouTube:** [Ver clase completa en YouTube](https://www.youtube.com/watch?v=aL5Cj5t1i-4)  
**Playlist oficial:** [De cero a cloud en YouTube](https://www.youtube.com/watch?v=8kL1HYphkns&list=PLGzDHDkhvPhg)

---

## 1. Lo que realmente se enseno en vivo

John Kleinad demostro como acelerar el flujo de trabajo de un desarrollador moderno integrando entornos asistidos por agentes inteligentes y despliegue continuo en la nube:

1. **Desarrollo guiado por especificaciones (*Spec-Driven Development*):**  
   Uso de Kiro IDE para estructurar requerimientos tecnicos y delegar tareas de codificacion repetitivas a agentes de inteligencia artificial sin perder el control sobre la arquitectura.
2. **Conexion de repositorios y pipeline CI/CD con AWS Amplify:**  
   Como vincular un repositorio de GitHub directamente a la consola de AWS Amplify Hosting para que cada `git push` dispare de forma automatica las etapas de construccion, verificacion y publicacion global.
3. **Distribucion global y certificados SSL automaticos:**  
   Despliegue de la aplicacion en la red de entrega de contenido (CDN) de AWS con soporte nativo para certificados TLS/SSL gratuitos y renovacion desatendida.
4. **Seguridad en la entrega web (Cabeceras HTTP):**  
   Vimos la importancia de configurar el archivo `amplify.yml` para emitir cabeceras de proteccion perimetral (`Content-Security-Policy`, `X-Frame-Options`, `Strict-Transport-Security`) para prevenir ataques de inyeccion y secuestro de click (*clickjacking*).

---

## 2. Configuracion de despliegue con cabeceras seguras (`amplify.yml`)

```yaml
version: 1
frontend:
  phases:
    preBuild:
      commands:
        - npm ci
    build:
      commands:
        - npm run build
  artifacts:
    baseDirectory: dist
    files:
      - '**/*'
  cache:
    paths:
      - node_modules/**/*
customHeaders:
  - pattern: '**/*'
    headers:
      - key: 'Strict-Transport-Security'
        value: 'max-age=31536000; includeSubDomains'
      - key: 'X-Frame-Options'
        value: 'DENY'
      - key: 'X-Content-Type-Options'
        value: 'nosniff'
      - key: 'Referrer-Policy'
        value: 'strict-origin-when-cross-origin'
```

---

## 3. Lecciones operativas

- **Fallo habitual en la carpeta de compilacion (*baseDirectory*):** Uno de los tropiezos mas comunes al desplegar proyectos en React, Vite o Next.js es configurar erronamente la ruta de artefactos (`build` vs `dist` vs `.next`). Si la ruta no coincide con el archivo de salida generado por el empaquetador, Amplify marcara error al finalizar la fase de construccion.
- **Control de costos en Amplify Hosting:** El nivel gratuito de AWS Amplify incluye 15 GB de datos servidos al mes y 1,000 minutos de compilacion mensuales durante los primeros 12 meses.
