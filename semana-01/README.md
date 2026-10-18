# Semana 01: Fundamentos de AWS, Amazon S3, AWS CLI y despliegue estatico

**Programa:** De cero a cloud — [AWS User Group Playa Vicente](https://www.awsugplayavicente.com/)  
**Ponente:** Roberto Flores Segundo (Líder [AWS UG Playa Vicente](https://www.awsugplayavicente.com/))  
**Modalidad:** Online en vivo (Discord Live)  
**Grabacion en YouTube:** [Ver clase completa en YouTube](https://www.youtube.com/watch?v=8kL1HYphkns)  
**Playlist oficial:** [De cero a cloud en YouTube](https://www.youtube.com/watch?v=8kL1HYphkns&list=PLGzDHDkhvPhg)

---

## 1. Lo que realmente se enseno en vivo

En esta primera sesión no nos quedamos en diapositivas teoricas. Fuimos directo a la consola de AWS y a la terminal para resolver las dudas iniciales que frenan a cualquiera que empieza en la nube:

1. **Configuracion de cuenta y seleccion de region:**  
   Explicamos la diferencia entre Regiones y Zonas de Disponibilidad (AZs), justificando por que trabajamos en `us-east-1` (Norte de Virginia) para contar con mayor cobertura de servicios en capa gratuita.
2. **Instalacion y configuracion de AWS CLI:**  
   Mostramos el uso de `aws configure`, detallando que representa cada parametro (`AWS Access Key ID`, `AWS Secret Access Key`, region predeterminada y formato `json`).
3. **Validacion de identidad en terminal:**  
   Ejecucion del comando basico para confirmar que las credenciales estan activas antes de lanzar recursos:
   ```bash
   aws sts get-caller-identity
   ```
4. **Despliegue de un sitio estatico en Amazon S3:**  
   Creamos un bucket con nombre globalmente unico, subimos archivos HTML y CSS, y activamos la funcion de Static Website Hosting.
5. **La trampa real del error 403 Forbidden:**  
   Vimos en vivo por que el sitio no cargaba de inicio: la funcion de *Block Public Access* viene activada por omision en S3. Ensenamos a desactivarla responsablemente y a colocar una política de bucket (*Bucket Policy*) que limite el acceso exclusivamente a lectura publica (`s3:GetObject`).

---

## 2. Comandos ejecutados en el laboratorio

### Crear el bucket y subir los archivos
```bash
# Crear bucket en us-east-1
aws s3 mb s3://mi-primer-sitio-estatico-augpv --region us-east-1

# Sincronizar archivos locales
aws s3 sync ./sitio-web s3://mi-primer-sitio-estatico-augpv
```

### Política de lectura publica aplicada al bucket
```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "PublicReadGetObject",
      "Effect": "Allow",
      "Principal": "*",
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::mi-primer-sitio-estatico-augpv/*"
    }
  ]
}
```

---

## 3. Lecciones operativas y errores comunes

- **Nombres de bucket repetidos:** Varios estudiantes intentaron nombres genericos como `mi-sitio-web`. El namespace de S3 es global; se debe usar un prefijo unico como tu nombre o alias.
- **Region por omision:** Si configuras el CLI en una region distinta a la del bucket, los comandos de sincronizacion pueden arrojar advertencias de redireccionamiento.
- **Riesgo de seguridad en llaves de acceso:** Enfatizamos que nunca se debe hacer commit de archivos `.env` o credenciales de AWS hacia repositorios publicos de GitHub.

---

## 4. Cuidado del bolsillo y limpieza de recursos

El almacenamiento estatico en S3 para pocos archivos HTML entra holgadamente en los 5 GB mensuales de la capa gratuita. Si deseas eliminar el laboratorio para mantener tu cuenta en cero:

```bash
# Vaciar y borrar el bucket
aws s3 rb s3://mi-primer-sitio-estatico-augpv --force
```
