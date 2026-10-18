# Semana 01: Fundamentos de AWS, Amazon S3, AWS CLI y despliegue estático

**Programa:** De cero a cloud — [AWS User Group Playa Vicente](https://www.awsugplayavicente.com/)  
**Ponente:** [Roberto Flores Segundo](https://www.linkedin.com/in/roberto-flores-b1a012322/) (Líder [AWS UG Playa Vicente](https://www.awsugplayavicente.com/))  
**Modalidad:** Online en vivo (Discord Live)  
**Grabación en YouTube:** [Ver clase completa en YouTube](https://www.youtube.com/watch?v=8kL1HYphkns)  
**Playlist oficial:** [De cero a cloud en YouTube](https://www.youtube.com/watch?v=8kL1HYphkns&list=PLGzDHDkhvPhg)

---

## 1. Lo que realmente se enseñó en vivo

En la sesión de apertura, Roberto compartió el origen de la iniciativa desde Playa Vicente, Veracruz, y analizó los resultados de la encuesta diagnóstica de la comunidad: más del 75% de los inscritos nunca habían utilizado AWS o no contaban con experiencia previa en tecnología, mientras que solo un 5% se encontraba activo en la nube.

Se enfatizó que no se requiere equipo de gama alta: una computadora básica o "tostadora" (incluso un Core i3 con 8 GB de RAM) es suficiente, dado que todo el procesamiento pesado se ejecuta en la infraestructura remota de AWS. La dinámica semanal se estructuró con clases formales los miércoles a las 7:00 PM CST (grabadas) y sesiones opcionales de asesoría por Meet los viernes y domingos para resolver bloqueos puntuales sin grabación.

### Fundamentos de Amazon S3
- **Almacenamiento de objetos serverless:** Explicación de por qué S3 es el servicio fundamental ("el Hola Mundo de la nube") para alojar archivos multimedia, respaldos, integraciones analíticas (Amazon QuickSight) y sitios estáticos (HTML, CSS, JS).
- **Disponibilidad y durabilidad:** 99.99% de disponibilidad y los 11 nueves de durabilidad (99.999999999%), distinguiendo la disponibilidad nativa del servicio frente a los cálculos arquitectónicos de SLA cuando se diseñan aplicaciones con instancias EC2 en una sola Zona de Disponibilidad.

---

## 2. Las 3 formas demostradas en vivo para desplegar en Amazon S3

Roberto demostró en tiempo real tres alternativas para desplegar un sitio web en Amazon S3, de menor a mayor automatización:

### Forma 1: Consola web de AWS (despliegue manual)
1. Creación de un bucket con nombre globalmente único a nivel mundial (`aws-user-group-playa-vicente-2026`).
2. Desactivación intencional del bloqueo de acceso público (*Block Public Access*), aceptando la confirmación de seguridad.
3. Subida manual de archivos (`index.html` y estilos) a la raíz del bucket.
4. Habilitación de la opción de **Alojamiento de sitios web estáticos** en la pestaña de Propiedades, definiendo el documento de índice (`index.html`).
5. Configuración de la política de bucket (*Bucket Policy*) para conceder permisos exclusivos de lectura pública a cualquier usuario (`s3:GetObject`):

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "PublicReadGetObject",
      "Effect": "Allow",
      "Principal": "*",
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::aws-user-group-playa-vicente-2026/*"
    }
  ]
}
```

### Forma 2: AWS CLI (despliegue desde la terminal)
Uso de la interfaz de línea de comandos para evitar pasos repetitivos en la consola gráfica:
```bash
# Validar identidad activa antes de operar
aws sts get-caller-identity

# Crear el bucket en la región designada
aws s3 mb s3://mi-sitio-estático-augpv --region us-east-1

# Sincronizar directorio local directamente hacia S3
aws s3 sync ./sitio-web s3://mi-sitio-estático-augpv
```

### Forma 3: CI/CD automatizado con GitHub Actions y Kiro IDE
- Introducción a **Kiro IDE**, el entorno de desarrollo asistido por IA de AWS, tanto en su interfaz gráfica como en terminal.
- Creación de la estructura del proyecto y del archivo de flujo de trabajo `.github/workflows/deploy.yml`.
- Demostración de despliegue continuo: cómo un simple `git push` a la rama principal dispara el workflow para sincronizar los cambios en S3 en segundos.
- **Anécdota real de la demo en vivo:** Se produjo un fallo de autenticación en GitHub Actions por credenciales apuntando a otra prueba anterior. Roberto aprovechó el incidente para enseñar depuración de pipelines en vivo y recalcó una lección indispensable: *"Nunca hagas cambios de última hora al código antes de salir a una demo en directo"*.

---

## 3. Reto de la semana y laboratorio en AWS Skill Builder

Para eliminar el miedo a cargos accidentales en tarjetas de crédito, la primera tarea oficial no requirió el uso de cuentas bancarias personales:

1. **Laboratorio guiado oficial:** Realizar el curso práctico con consola real [Introduction to Amazon Simple Storage Service (Amazon S3) en AWS Skill Builder](https://skillbuilder.aws/learn/R54NZHEX5K/introduction-to-amazon-simple-storage-service-s3-espaol-latam/NKN6UQ8A5Q) (100% gratuito, en español y sin tarjeta de crédito).
2. **Objetivos del laboratorio:** Creación de bucket, subida de objetos, gestión de permisos, aplicación de políticas JSON y control de versiones.
3. **Cómo validar el entorno seguro:** Se mostró en vivo cómo comprobar que la consola abierta pertenece a un usuario temporal aprovisionado por AWS (`aws-student-lab-user...`) y no a la cuenta propia, garantizando un entorno 100% aislado con costo $0.00 USD.
4. **Reto avanzado opcional:** Clonar tu propio sitio web y sincronizarlo con AWS CLI usando `aws s3 sync` o mediante un pipeline de GitHub Actions como el visto en clase.
