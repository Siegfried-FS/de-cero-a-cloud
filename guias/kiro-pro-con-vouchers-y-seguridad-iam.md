# Financiamiento de Kiro Pro con vouchers y seguridad con IAM Identity Center

Muchos estudiantes y desarrolladores guardan los cupones de $25 o $100 USD que reciben en meetups locales, conferencias como AWS Community Days o los retos de fin de semana en AWS Builder Center sin saber con exactitud en qué utilizarlos, dejando que expiren sin aprovecharlos.

Esta guía documenta la estrategia para hacer que esos créditos cubran al 100% la suscripción de **Kiro Pro**, implementando al mismo tiempo una arquitectura de seguridad empresarial basada en **AWS Organizations** e **IAM Identity Center**.

---

## 1. Qué es Kiro y modalidades de uso

**Kiro** es el entorno de desarrollo asistido por inteligencia artificial de Amazon Web Services diseñado para modelar arquitecturas, redactar especificaciones técnicas (*Spec-Driven Development*) y generar código dialogando con modelos avanzados:

- **Kiro Desktop:** Editor de escritorio completo (basado en Visual Studio Code) con integración nativa de IA en el flujo de trabajo.
- **Kiro CLI:** Herramienta interactiva para terminal, pensada para quienes gestionan servidores remotos o prefieren trabajar desde la línea de comandos.
- **Kiro Web:** Entorno de programación completo en el navegador web (desbloqueado con la suscripción Pro activa), que permite desarrollar desde cualquier dispositivo secundario, tableta o laptop ligera sin instalaciones locales.

---

## 2. Cómo financiar Kiro Pro al 100% con créditos de eventos

El proceso para utilizar saldo promocional en lugar de dinero personal sigue este flujo:

1. **Canjear el voucher en la consola de facturación:**  
   En la sección *Billing and Cost Management*, accede a la pestaña **Credits** e ingresa el código alfanumérico del cupón recibido en el evento de comunidad o reto de Builder Center.
2. **Activar la suscripción Pro:**  
   Al activar Kiro Pro, AWS deduce el costo mensual de la suscripción directamente del saldo de créditos disponible en la cuenta, antes de realizar cualquier cargo al método de pago principal.
3. **Estrategia para no gastar de más ($0 USD permanente):**  
   - Si en el mes en curso asistes a otro meetup o completas un nuevo reto de Builder Center con cupones, cubres el siguiente ciclo.
   - Si un mes no dispones de cupones nuevos, cancelas la suscripción Pro antes de la fecha de corte para que no toque tu tarjeta bancaria.
   - Puedes continuar trabajando de forma indefinida en el **Plan Free de $0 USD permanente**, el cual otorga 50 créditos mensuales para consultas y desarrollo asistido.

---

## 3. Seguridad de nivel empresarial: menor privilegio con IAM Identity Center

Un error común al habilitar herramientas de desarrollo es utilizar credenciales administrativas con permisos globales (`AdministratorAccess`). La estrategia adecuada utiliza la misma arquitectura que adoptan las empresas reguladas:

1. **Configuración con AWS Organizations e IAM Identity Center:**  
   Se crea una estructura organizativa donde la cuenta de desarrollo esté aislada.
2. **Principio de menor privilegio estricto:**  
   El usuario utilizado para autenticarse en el editor Kiro dispone de libertad total para dialogar con el modelo de IA y generar código en el espacio local, pero cuenta con **exactamente cero permisos sobre la infraestructura de producción de AWS**.
3. **Resultado operativo:**  
   Se elimina por completo el riesgo de que una alucinación del modelo o un comando mal ejecutado en la terminal aprovisione servidores de alto costo o comprometa recursos existentes en la cuenta.

---

## 4. Referencias y Hub Comunitario de Creadores

- **Artículo técnico completo con evidencias en AWS Builder Center:**  
  [Leer artículo detallado con capturas de consola y terminal](https://lnkd.in/ed9AZbgm)
- **Hub Comunitario de Creadores ([AWS UG Playa Vicente](https://www.awsugplayavicente.com/)):**  
  [creadores.awsugplayavicente.com](https://creadores.awsugplayavicente.com/)  
  Plataforma comunitaria impulsada por el [AWS User Group Playa Vicente](https://www.awsugplayavicente.com/) diseñada específicamente para visibilizar, amplificar y dar alcance a los artículos y tutoriales técnicos redactados en español por builders de toda Latinoamérica.
