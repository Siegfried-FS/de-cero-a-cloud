# Financiamiento de Kiro Pro con vouchers y seguridad con IAM Identity Center

Muchos estudiantes y desarrolladores guardan los cupones de $25 o $100 USD que reciben en meetups locales, conferencias como AWS Community Days o los retos de fin de semana en AWS Builder Center sin saber con exactitud en que utilizarlos, dejando que expiren sin aprovecharlos.

Esta guia documenta la estrategia para hacer que esos creditos cubran al 100% la suscripcion de **Kiro Pro**, implementando al mismo tiempo una arquitectura de seguridad empresarial basada en **AWS Organizations** e **IAM Identity Center**.

---

## 1. Que es Kiro y modalidades de uso

**Kiro** es el entorno de desarrollo asistido por inteligencia artificial de Amazon Web Services disenado para modelar arquitecturas, redactar especificaciones tecnicas (*Spec-Driven Development*) y generar codigo dialogando con modelos avanzados:

- **Kiro Desktop:** Editor de escritorio completo (basado en Visual Studio Code) con integracion nativa de IA en el flujo de trabajo.
- **Kiro CLI:** Herramienta interactiva para terminal, pensada para quienes gestionan servidores remotos o prefieren trabajar desde la linea de comandos.
- **Kiro Web:** Entorno de programacion completo en el navegador web (desbloqueado con la suscripcion Pro activa), que permite desarrollar desde cualquier dispositivo secundario, tableta o laptop ligera sin instalaciones locales.

---

## 2. Como financiar Kiro Pro al 100% con creditos de eventos

El proceso para utilizar saldo promocional en lugar de dinero personal sigue este flujo:

1. **Canjear el voucher en la consola de facturacion:**  
   En la seccion *Billing and Cost Management*, accede a la pestana **Credits** e ingresa el codigo alfanumerico del cupon recibido en el evento de comunidad o reto de Builder Center.
2. **Activar la suscripcion Pro:**  
   Al activar Kiro Pro, AWS deduce el costo mensual de la suscripcion directamente del saldo de creditos disponible en la cuenta, antes de realizar cualquier cargo al metodo de pago principal.
3. **Estrategia para no gastar de mas ($0 USD permanente):**  
   - Si en el mes en curso asistes a otro meetup o completas un nuevo reto de Builder Center con cupones, cubres el siguiente ciclo.
   - Si un mes no dispones de cupones nuevos, cancelas la suscripcion Pro antes de la fecha de corte para que no toque tu tarjeta bancaria.
   - Puedes continuar trabajando de forma indefinida en el **Plan Free de $0 USD permanente**, el cual otorga 50 creditos mensuales para consultas y desarrollo asistido.

---

## 3. Seguridad de nivel empresarial: menor privilegio con IAM Identity Center

Un error comun al habilitar herramientas de desarrollo es utilizar credenciales administrativas con permisos globales (`AdministratorAccess`). La estrategia adecuada utiliza la misma arquitectura que adoptan las empresas reguladas:

1. **Configuracion con AWS Organizations e IAM Identity Center:**  
   Se crea una estructura organizativa donde la cuenta de desarrollo este aislada.
2. **Principio de menor privilegio estricto:**  
   El usuario utilizado para autenticarse en el editor Kiro dispone de libertad total para dialogar con el modelo de IA y generar codigo en el espacio local, pero cuenta con **exactamente cero permisos sobre la infraestructura de produccion de AWS**.
3. **Resultado operativo:**  
   Se elimina por completo el riesgo de que una alucinacion del modelo o un comando mal ejecutado en la terminal aprovisione servidores de alto costo o comprometa recursos existentes en la cuenta.

---

## 4. Referencias y Hub Comunitario de Creadores

- **Articulo tecnico completo con evidencias en AWS Builder Center:**  
  [Leer articulo detallado con capturas de consola y terminal](https://lnkd.in/ed9AZbgm)
- **Hub Comunitario de Creadores (AWS UG Playa Vicente):**  
  [creadores.awsugplayavicente.com](https://creadores.awsugplayavicente.com/)  
  Plataforma comunitaria impulsada por el AWS User Group Playa Vicente disenada especificamente para visibilizar, amplificar y dar alcance a los articulos y tutoriales tecnicos redactados en espanol por builders de toda Latinoamerica.
