# Semana 02: Computo con Amazon EC2, modelos cloud e introduccion a IAM roles

**Programa:** De cero a cloud — [AWS User Group Playa Vicente](https://www.awsugplayavicente.com/)  
**Ponente:** [Roberto Flores Segundo](https://www.linkedin.com/in/roberto-flores-b1a012322/) (Líder [AWS UG Playa Vicente](https://www.awsugplayavicente.com/))  
**Modalidad:** Online en vivo (Discord Live)  
**Grabacion en YouTube:** [Ver clase completa en YouTube](https://www.youtube.com/watch?v=Q4GIVWs0qBg)  
**Playlist oficial:** [De cero a cloud en YouTube](https://www.youtube.com/watch?v=8kL1HYphkns&list=PLGzDHDkhvPhg)

---

## 1. Lo que realmente se enseno en vivo

En esta clase aterrizamos los conceptos que suelen confundir en los examenes de certificacion mediante un servidor real en ejecucion:

1. **Modelos cloud en la práctica (IaaS, PaaS, SaaS):**  
   Comparamos la administracion directa del sistema operativo en una maquina virtual (IaaS con EC2) frente a servicios de plataforma (PaaS) y software terminado (SaaS).
2. **Lanzamiento de una instancia en capa gratuita:**  
   Aprovisionamos una instancia `t2.micro` utilizando Amazon Linux 2023 en `us-east-1`.
3. **El dilema de la llave SSH vs IAM Role con SSM:**  
   Explicamos el riesgo que implica crear llaves `.pem` locales que luego terminan olvidadas en descargas o repositorios. Mostramos como crear un IAM Role con la política `AmazonSSMManagedInstanceCore` para conectarse a la terminal de Linux via AWS Systems Manager Session Manager, manteniendo el puerto 22 cerrado.
4. **Automatizacion con User Data:**  
   Inyectamos un script bash en el arranque de la instancia para que actualizara paquetes, instalara un servidor web y sirviera una pagina de estado sin intervencion manual.
5. **Configuracion de Security Groups:**  
   Regla de entrada (*Inbound rule*) en el puerto 80 (HTTP) permitida para cualquier origen (`0.0.0.0/0`) con el proposito de acceder al sitio desde el navegador web.

---

## 2. Script de inicio utilizado (User Data)

```bash
#!/bin/bash
dnf update -y
dnf install -y httpd
systemctl start httpd
systemctl enable httpd
echo "<h1>Servidor Web en Amazon EC2 - De Cero a Cloud</h1><p>Desplegado en us-east-1</p>" > /var/www/html/index.html
```

---

## 3. Lecciones operativas y errores comunes

- **Olvidar asociar la IP publica:** Al lanzar la instancia, si la subred no tiene habilitada la asignacion automatica de IPv4 publica (*Auto-assign public IPv4*), no podras acceder a la pagina web desde Internet.
- **Confusion entre Security Group y Network ACL:** El Security Group es a nivel de instancia y tiene estado (*stateful*); no requiere abrir reglas de salida para que las respuestas HTTP regresen al usuario.
- **Instancias en ejecucion innecesaria:** Si no necesitas el servidor activo, detenlo (*Stop*) o eliminalo (*Terminate*) para no agotar las 750 horas mensuales de la capa gratuita.

---

## 4. Cuidado del bolsillo y verificacion de apagado

Para asegurarte de que la instancia no siga consumiendo almacenamiento de volumen EBS:

```bash
# Terminar la instancia
aws ec2 terminate-instances --instance-ids i-0123456789abcdef0

# Confirmar estado terminated
aws ec2 describe-instances \
  --instance-ids i-0123456789abcdef0 \
  --query "Reservations[*].Instances[*].[InstanceId,State.Name]" \
  --output table
```
