# Semana 10: IA aplicada y accesibilidad: el caso real de CogniPath

**Programa:** De cero a cloud — [AWS User Group Playa Vicente](https://www.awsugplayavicente.com/)  
**Ponente invitado:** [Misael Calisaya](https://www.linkedin.com/in/misaelcalisaya/) (Creador de CogniPath, Finalista Global en AWS 10,000 AIdeas, Líder AWS SBG UCASAL, Salta, Argentina)  
**Host:** [Roberto Flores Segundo](https://www.linkedin.com/in/roberto-flores-b1a012322/)  
**Modalidad:** Online en vivo (Discord Live)  
**Grabación en YouTube:** [Ver clase completa en YouTube](https://www.youtube.com/watch?v=XyhME9QdBnI)  
**Playlist oficial:** [De cero a cloud en YouTube](https://www.youtube.com/watch?v=8kL1HYphkns&list=PLGzDHDkhvPhg)

---

## 1. Lo que realmente se enseñó en vivo

Misael Calisaya (estudiante de la Universidad Católica de Salta, Argentina, y líder del AWS Student Builder Group local) compartió la historia de desarrollo detrás de **CogniPath**, proyecto seleccionado entre los finalistas globales del concurso oficial **AWS 10,000 AIdeas**:

### El origen empático del proyecto
CogniPath nació originalmente para asistir a estudiantes universitarios con diagnóstico de **TDA y TDAH** (Déficit de Atención con o sin Hiperactividad) mediante la simplificación de lecturas académicas densas. Sin embargo, la aplicación dio un giro radical a partir de una experiencia cotidiana en el aula universitaria:
- Un compañero de estudios con discapacidad visual le comentó: *"Yo no entiendo lo que dicen las imágenes ni los diagramas de los apuntes; me los tengo que imaginar"*.
- Misael se cuestionó cómo era posible que en pleno 2026 una persona tuviera que estudiar imaginando el contenido visual por falta de tecnología accesible. Decidió transformar CogniPath en una plataforma universal guiada por voz para personas no videntes y neurodivergentes.

---

## 2. Arquitectura técnica y servicios de AWS integrados

Misael demostró cómo resolvió cada barrera de accesibilidad combinando servicios de IA en la nube:

1. **Amazon Bedrock (Claude Sonnet):**
   - Análisis multimodal de documentos PDF: el modelo extrae texto, interpreta diagramas y traduce descripciones complejas a cuatro niveles adaptativos de dificultad cognitiva.
2. **Amazon Polly:**
   - Síntesis de voz natural y narración dinámica del material procesado para usuarios no videntes.
3. **Bionic Reading y técnicas cognitivas:**
   - Algoritmo que resalta visualmente las primeras letras de cada palabra para guiar el ojo y fragmentar párrafos densos, reduciendo drásticamente la sobrecarga de atención en personas con TDAH.
   - Eliminación intencional de cronómetros tradicionales tipo Pomodoro al comprobar en pruebas que generaban ansiedad en los alumnos.
4. **Amazon Titan Image Generator:**
   - Generación de pictogramas contextuales para apoyar el aprendizaje visual de conceptos técnicos abstractos.
5. **Navegación por voz y detector de inactividad:**
   - Interfaz 100% operable mediante comandos de voz. Si el sistema detecta silencio prolongado, la aplicación interviene activamente ofreciendo asistencia auditiva para guiar la navegación por los módulos.
6. **Reemplazo de hardware costoso:**
   - Explicó que en Latinoamérica los dispositivos de escaneo asistido para personas ciegas (barras lectoras dedicadas) tienen costos inaccesibles. La meta de CogniPath es que cualquier estudiante con la cámara de un teléfono celular común pueda escanear y escuchar un texto físico en segundos.

---

## 3. Momento comunitario: Sandra Olier y la reinvención personal

Durante la sesión, **Sandra Elizabeth Olier** (estudiante del programa, 55 años, proveniente del rubro gastronómico, madre de un joven con TDAH y graduada de AWS re/Start) tomó la palabra visiblemente conmovida:
- Agradeció a Misael por la nobleza y empatía de su desarrollo, relatando en primera persona el desafío que implica la educación de una persona con TDAH y cómo la tecnología inclusiva cambia vidas.
- Compartió su propio testimonio de reinvención: cómo a los 55 años decidió ingresar al mundo de la tecnología tras la pandemia, demostrando a toda la comunidad que no existe edad límite para aprender cómputo en la nube.

---

## 4. Reflexión de Roberto Flores: "La vida no es lineal"

Roberto cerró la sesión conectando el testimonio de Misael y Sandra con su propia trayectoria como carpintero:
- *"La vida no es lineal y muchas veces caminamos a ciegas, pero lo importante es seguir adelante"*.
- Relató cómo en sus inicios intentaba aprender tomando cursos nivel 100 y 300 desordenados al mismo tiempo por la presión laboral, sufriendo rechazos en múltiples convocatorias de becas antes de ser aceptado, y enfatizó que *De cero a cloud* fue diseñado justamente para ahorrarles ese camino solitario a los nuevos estudiantes.
