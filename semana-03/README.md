# Semana 03: Escalabilidad y bases de datos: Amazon DynamoDB, RDS y Aurora

**Programa:** De cero a cloud — [AWS User Group Playa Vicente](https://www.awsugplayavicente.com/)  
**Ponente invitada:** [Sairi Ávila](https://www.linkedin.com/in/sairiavila/) (AWS Community Builder, AI Developer)  
**Host:** [Roberto Flores Segundo](https://www.linkedin.com/in/roberto-flores-b1a012322/)  
**Modalidad:** Online en vivo (Discord Live)  
**Grabación en YouTube:** [Ver clase completa en YouTube](https://www.youtube.com/watch?v=DjAbRRVF1f4)  
**Playlist oficial:** [De cero a cloud en YouTube](https://www.youtube.com/watch?v=8kL1HYphkns&list=PLGzDHDkhvPhg)

---

## 1. Lo que realmente se enseñó en vivo

Sairi Ávila (desarrolladora de software especializada en visión artificial) guio la sesión explicando el espectro completo de bases de datos en la nube, destacando cómo el rol de un desarrollador o ingeniero de IA inevitablemente interactúa con la persistencia y gestión de datos.

### Panorama de bases de datos en AWS
- **Relacionales (SQL):** Amazon RDS (soporte para PostgreSQL, MySQL, MariaDB, Oracle y SQL Server) y Amazon Aurora (motor nativo cloud de alto rendimiento con replicación automática en 3 Zonas de Disponibilidad).
- **NoSQL (Clave-Valor / Documentos):** Amazon DynamoDB, base de datos serverless de latencia de milisegundos de un solo dígito a cualquier escala.
- **En memoria y series temporales:** Amazon ElastiCache (Redis / Memcached) para caché ultrarrápido y Amazon Timestream para telemetría IoT.
- **Analítica y Data Lakes:** Amazon Redshift, combinación de Amazon S3 con Amazon Athena (consultas SQL serverless sin aprovisionar servidores).
- **Herramientas de escritorio:** La comunidad compartió experiencias sobre gestores universales como DBeaver (bromeando sobre el castor de su logotipo) y su integración con bases de datos remotas.

### La analogía de los clústeres de alta disponibilidad
Para que los estudiantes sin formación previa entendieran la replicación y redundancia, Sairi usó la analogía de **las dos cajitas y las pelotitas**: si tienes una pelota en la cajita A, el clúster garantiza que exactamente la misma pelota se replica y actualiza en la cajita B. Si un servidor o zona sufre una falla imprevista, la otra cajita mantiene el servicio operativo sin pérdida de datos.

---

## 2. Laboratorio en vivo: Modelado y operaciones en Amazon DynamoDB

Sairi abrió la consola web de Amazon DynamoDB para construir y explorar una tabla en directo:

1. **Definición de la tabla:** Nombre `clase_alumnos`.
2. **Diseño de llaves primarias compuestas:**
   - **Clave de partición (*Partition Key*):** `alumno_id` (alfanumérico, ej. `A001`, `A002`). Determina en qué partición física se distribuyen los datos.
   - **Clave de ordenación (*Sort Key*):** `materia`. Permite organizar múltiples registros para un mismo alumno.
3. **Modo de capacidad (*Capacity Mode*):**
   - Se configuró en **Bajo demanda (*On-Demand*)**, explicando que para proyectos personales y etapas tempranas evita el pago por capacidad aprovisionada no utilizada, manteniéndose en la capa gratuita ($0.00 USD).
4. **Protección y ciclo de vida:** Explicación de la opción de protección contra eliminación accidental y cómo exploradores de elementos (*Scan* vs. *Query*) impactan el rendimiento y consumo de unidades de lectura.
5. **Inserción de elementos JSON:** Demostración de cómo DynamoDB permite esquemas flexibles donde cada fila puede almacenar atributos heterogéneos sin requerir migraciones complejas de esquemas relacionales.

---

## 3. Debate vocacional: Carrera, certificaciones y cumplimiento

Al cierre de la sesión se abrió un panel de preguntas en vivo sobre el mercado laboral en tecnología:

- **Especialización (Data/DB vs. Inteligencia Artificial):** Sairi explicó que la ingeniería en sistemas ofrece la ventaja de entender hardware, redes y desarrollo, pero quienes buscan ingresar rápido al mercado actual deben dominar servicios gestionados de IA y bases de datos NoSQL sin reinventar la rueda.
- **Ruta de certificaciones (Cloud Practitioner vs. AI Practitioner):** Recomendó iniciar con *Cloud Practitioner* a quienes deseen comprender presupuestos, gobernanza y arquitectura global en la nube, o *AI Practitioner* para quienes se orienten a la integración de modelos y prompts.
- **La perspectiva de compliance y auditoría:** Roberto complementó explicando que bajo normas internacionales como **ISO/IEC 27001:2022**, las certificaciones oficiales son un requisito formal de evidencia para demostrar la competencia técnica del personal ante auditorías externas y facilitan negociaciones salariales en empresas formales.
- **Anuncio de calendario:** La clase 4 se reprogramó de miércoles a jueves debido a la participación de la comunidad en el AWS Summit Ciudad de México.
