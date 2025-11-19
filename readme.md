# I. ORIGEN

El presente **Informe de Auditoría de Sistemas** se origina en la ejecución del *Examen de la Unidad III – Auditoría de Sistemas*, cuyo objetivo es evaluar exhaustivamente el **código fuente**, el **funcionamiento operativo**, la **arquitectura técnica**, los **controles implementados** y el **despliegue del sistema de Mesa de Ayuda con IA** perteneciente a **Corporate EPIS Pilot**.

La auditoría se realiza debido a los siguientes motivos:

- **Requerimiento académico formal**, que establece que el estudiante debe ejecutar una auditoría completa de un sistema real basado en tecnologías modernas (RAG, LLMs, Ollama, ChromaDB, Docker y Kubernetes).
- **Validar la conformidad entre el diseño declarado y la implementación real**, verificando que:
  - El backend (FastAPI) implemente correctamente el router de intenciones, el pipeline RAG y el flujo de creación de tickets.
  - El frontend (React + MUI) gestione correctamente el ciclo conversacional y las acciones del usuario.
  - El sistema RAG funcione mediante embeddings y búsqueda vectorial en ChromaDB.
  - El modelo LLM funcione en entorno local mediante Ollama.
- **Revisión técnica detallada del código**, incluyendo:
  - `main.py` (router, procesamiento de preguntas, creación de tickets, logging estructurado).
  - `ingest.py` (ingesta de documentos, generación de embeddings y creación de la base vectorial).
  - `database_setup.py` (creación automática de tabla de tickets).
  - Dockerfiles del backend y frontend.
  - Configuración del reverse proxy Nginx.
  - Código frontend que implementa el flujo conversacional guiado.
- **Asegurar la integridad del flujo de soporte**, verificando:
  - Clasificación de intenciones.
  - Bucle de retroalimentación (¿La solución fue útil?).
  - Registro correcto de tickets.
  - Persistencia de datos en SQLite.
- **Cumplir con las indicaciones del docente**, quien especificó que el estudiante debe:
  1. Clonar el repositorio del sistema.
  2. Levantar el servicio completamente con Docker y Ollama.
  3. Ejecutar pruebas técnicas y funcionales.
  4. Registrar evidencias de todas las actividades.
  5. Elaborar este Informe de Auditoría según el formato oficial.

---

# II. INFORMACIÓN DE LA ENTIDAD O DEPENDENCIA

**Corporate EPIS Pilot** es una entidad dedicada a la creación de prototipos empresariales basados en Inteligencia Artificial, enfocándose en sistemas conversacionales avanzados, automatización de soporte técnico, y soluciones listas para despliegue en entornos reales.

### **Datos relevantes sobre la entidad y el sistema auditado**

- **Nombre del sistema:**  
  *Asistente de IA – Mesa de Ayuda con IA para entornos empresariales*.

- **Objetivo general del sistema:**  
  Brindar asistencia técnica automatizada, basada en un flujo conversacional guiado y un modelo de IA que accede a una **base de conocimiento privada**.

- **Características clave del sistema según su implementación real:**
  - Arquitectura **RAG (Retrieval-Augmented Generation)**.
  - Router de intenciones mediante **LLM ejecutado en Ollama**.
  - Vector Store basado en **ChromaDB** con embeddings *multilingual-e5-large*.
  - Flujo de conversación con retroalimentación y creación guiada de tickets.
  - Backend **FastAPI** con pipeline RAG y generación de tickets en **SQLite**.
  - Frontend **React** con Material UI y estados conversacionales controlados.
  - Sistema 100% local, sin dependencias hacia nubes externas.
  - Despliegue mediante **Docker**, **Docker Compose** y manifiestos de **Kubernetes**.

- **Equipo responsable del desarrollo:**  
  Unidad de Ingeniería y Automatización – Corporate EPIS Pilot.

- **Repositorio auditado:**  
  Repositorio GitHub entregado por el docente como base del examen.

---

# III. DENOMINACIÓN DE LA MATERIA DE CONTROL

### 1. Materia de Control
La materia de control corresponde a la revisión del **código fuente, funcionamiento operativo y arquitectura técnica** del sistema de Mesa de Ayuda con IA de Corporate EPIS Pilot, verificando que cada componente implementado (backend, frontend, RAG, creación de tickets, Docker, Ollama y ChromaDB) funcione conforme a lo establecido en el diseño original.

### 2. Tipo de Auditoría
El tipo de auditoría aplicable es una **Auditoría de Sistemas de Código y Funcionamiento**, enfocada en validar la estructura interna del software, su comportamiento real durante la ejecución y la integridad de los procesos que conforman el sistema inteligente de soporte.

### 3. Finalidad
La finalidad es **comprobar que el sistema opera correctamente**, que su arquitectura está implementada de forma adecuada y que los procesos críticos (ingesta, recuperación de información, clasificación de intenciones, flujo conversacional y creación de tickets) funcionan sin errores ni desviaciones.

### 4. Criterios de Control
Los criterios de control se basan en la **correctitud técnica del código**, la integridad de los datos almacenados, el funcionamiento esperado de cada módulo, la coherencia del flujo conversacional, el despliegue adecuado en contenedores Docker y el cumplimiento de principios mínimos de seguridad lógica.

### 5. Propósito
El propósito de la auditoría es **evaluar la confiabilidad, consistencia y operatividad completa del sistema**, identificando posibles riesgos o fallas y verificando que el sistema esté listo para uso académico o despliegue real, según los objetivos del proyecto Corporate EPIS Pilot.

# IV. ALCANCE

El alcance de la auditoría comprende la evaluación integral del **código fuente, funcionamiento operativo, arquitectura conversacional, procesos internos y despliegue técnico** del sistema *Mesa de Ayuda con IA* desarrollado por Corporate EPIS Pilot. La revisión incluye todos los componentes que intervienen en el flujo de soporte inteligente, desde la ingesta de documentos para el modelo RAG hasta la creación de tickets en la base de datos local, verificando su coherencia, operatividad y correspondencia con el diseño declarado.

Límites del alcance:
- La auditoría se enfoca exclusivamente en el sistema de Mesa de Ayuda con IA provisto por Corporate EPIS Pilot, incluyendo su backend en FastAPI, frontend en React/MUI, scripts de ingesta, vector store en ChromaDB, modelo LLM ejecutado mediante Ollama y base de datos SQLite.
- Se revisará el funcionamiento del pipeline RAG, el router de intenciones, el flujo conversacional guiado, la interacción frontend–backend y el proceso completo de creación de tickets.
- Se evaluará la estructura de contenedores, Dockerfiles, configuración del proxy Nginx y la correcta ejecución mediante Docker Compose y/o Kubernetes.
- Quedan excluidas del alcance todas las plataformas, sistemas externos, aplicaciones adicionales o servicios ajenos al proyecto, así como evaluaciones sobre infraestructura física, redes, seguridad perimetral o aspectos financieros.
- La auditoría se limita a revisión documental, pruebas funcionales, inspección del código, ejecución controlada del sistema y recopilación de evidencias, sin realizar pruebas destructivas, ataques de intrusión o pruebas de carga extremas.

---

# V. OBJETIVOS

## Objetivo General
Evaluar el correcto funcionamiento, integridad técnica, calidad del código y cumplimiento del diseño arquitectónico del sistema de Mesa de Ayuda con IA de Corporate EPIS Pilot, verificando que sus componentes conversacionales, mecanismos de recuperación de información, flujo inteligente de soporte y proceso de creación de tickets operen de acuerdo con las especificaciones declaradas para garantizar confiabilidad, precisión y consistencia del servicio.

## Objetivos Específicos
- **Verificar la correcta implementación del router de intenciones**, asegurando que el modelo LLM clasifique adecuadamente las consultas en pregunta general, reporte de problema y despedida, manteniendo coherencia con el flujo conversacional establecido.
- **Evaluar el funcionamiento del pipeline RAG** mediante la revisión de la ingesta de documentos, generación de embeddings, creación del vector store y exactitud de las respuestas recuperadas desde la base de conocimiento.
- **Comprobar la integridad y operatividad del proceso de creación de tickets**, validando la construcción del mensaje de acción (`ACTION_CREATE_TICKET`), el registro en la base de datos SQLite y la respuesta correspondiente del sistema.
- **Analizar la estructura técnica del despliegue** mediante la revisión de Dockerfiles, Docker Compose, configuración de Nginx y el correcto funcionamiento del sistema completo en contenedores, garantizando consistencia entre servicios y comunicación con Ollama.

# VI. PROCEDIMIENTOS DE AUDITORÍA

Los procedimientos que se aplicarán durante la auditoría se presentan en la siguiente tabla:

### Cuadro N.° 1 – Procedimientos de Auditoría

| **Objetivo Específico** | **Procedimientos de Auditoría** | **Referencia Normativa / Criterio Técnico** | **Responsable (Rol)** |
|-------------------------|----------------------------------|---------------------------------------------|------------------------|
| **1. Verificar la correcta implementación del router de intenciones.** | 1.1. Revisión del código del router (`router_prompt`, `extract_json_from_string`, `RouteQuery`).<br>1.2. Ejecución de pruebas con consultas de diferente intención para validar clasificación real del LLM.<br>1.3. Evaluación de la coherencia entre el prompt, el parser JSON y la respuesta del modelo.<br>1.4. Verificación de manejo de errores ante entradas ambiguas o sin formato.<br>1.5. Registro de hallazgos sobre inconsistencias en detección de intención. | Buenas prácticas de diseño de modelos conversacionales (LLM Prompt Engineering).<br>Control técnico de calidad de código (linters y revisión de lógica). | Responsable Principal: Auditor de Sistemas Inteligentes.<br>Soporte: Auditor Backend.<br>Revisión de líder: Ericka E. Martínez Yufra. |
| **2. Evaluar el funcionamiento del pipeline RAG (ingesta, embeddings, vector store y recuperación).** | 2.1. Revisión del script `ingest.py` definiendo procesos de carga, segmentación y embeddings.<br>2.2. Verificación de la generación de la carpeta `vector_store/` y persistencia correcta en ChromaDB.<br>2.3. Validación de la calidad de recuperación mediante preguntas basadas en los documentos cargados.<br>2.4. Análisis del modelo de embeddings `multilingual-e5-large` y su coherencia con el idioma de consulta.<br>2.5. Registro de hallazgos sobre fallos de ingesta o baja relevancia en recuperación. | Buenas prácticas de RAG (Retrieval-Augmented Generation).<br>Controles de calidad de datos y recuperación semántica. | Responsable Principal: Auditor de IA y Datos.<br>Soporte: Auditor Técnico.<br>Revisión de líder: Ericka E. Martínez Yufra. |
| **3. Comprobar la integridad y operatividad del proceso de creación de tickets.** | 3.1. Revisión del código de extracción y procesamiento del mensaje `ACTION_CREATE_TICKET`.<br>3.2. Validación del flujo completo desde el frontend: solicitud de detalles → envío → registro.<br>3.3. Inspección directa del archivo `tickets.db` verificando inserciones y consistencia de campos.<br>3.4. Revisión del endpoint `/ask` y su manejo de la acción.<br>3.5. Elaboración de hallazgos sobre fallas, duplicidades o inconsistencias en SQLite. | Controles de gestión de datos y persistencia.<br>Buenas prácticas de integridad de datos en sistemas locales. | Responsable Principal: Auditor Backend.<br>Soporte: Auditor de Base de Datos.<br>Revisión de líder: Ericka E. Martínez Yufra. |
| **4. Analizar la estructura técnica del despliegue (Docker, Nginx, comunicación con Ollama).** | 4.1. Revisión de Dockerfiles del backend y frontend, validando construcción correcta.<br>4.2. Ejecución de `docker compose up` verificando inicio simultáneo de backend, frontend y proxy.<br>4.3. Validación de la comunicación backend ↔ Ollama mediante pruebas de consulta reales.<br>4.4. Inspección del archivo `nginx.conf` validando el enrutamiento hacia el frontend y backend.<br>4.5. Registro de hallazgos sobre puertos expuestos, dependencias, rutas o problemas de contenedorización. | Buenas prácticas de despliegue en contenedores.<br>Principios de arquitectura basada en microservicios. | Responsable Principal: Auditor de Infraestructura de Software.<br>Soporte: Auditor DevOps.<br>Revisión de líder: Ericka E. Martínez Yufra. |


# VII. PLAZO DE LA AUDITORÍA Y CRONOGRAMA

La auditoría del sistema de Mesa de Ayuda con IA se desarrollará en fases claramente estructuradas, abarcando desde la planificación, revisión documental, evaluación técnica, validación operativa y elaboración del informe final. Cada fase está alineada con prácticas de auditoría de sistemas, evaluación de código, revisión de modelos de IA y verificación de despliegues en contenedores.

## Cuadro N.° 2 – Fases del Plan de Auditoría

| **Fase** | **Fechas** | **Referencia Técnica Aplicable** | **Explicación de Aplicación Concreta** |
|----------|------------|-----------------------------------|----------------------------------------|
| **Planificación** | 01 al 03 de febrero de 2025 | Auditoría de sistemas – Preparación y delimitación del alcance | Se definen el alcance de la auditoría, los objetivos específicos, los entregables, los módulos a evaluar (backend, frontend, RAG, tickets y Docker) y se establecen criterios de control. |
| **Revisión Documental** | 04 al 06 de febrero de 2025 | Evaluación de artefactos de software y documentación técnica | Se revisan scripts (`main.py`, `ingest.py`, `database_setup.py`), estructura del frontend, Dockerfiles, configuración de Nginx, documentación en el repositorio y estructura del proyecto. |
| **Análisis Técnico Funcional** | 07 al 10 de febrero de 2025 | Buenas prácticas de IA, RAG, DevOps y desarrollo backend/frontend | Se ejecuta el sistema, se prueba el router de intenciones, pipeline RAG, creación de tickets en SQLite, interacción frontend–backend y comunicación con Ollama. |
| **Validación Operativa y Consistencia** | 11 al 12 de febrero de 2025 | Pruebas funcionales y verificación operativa | Se realizan pruebas reales del flujo conversacional completo, se valida el comportamiento del bot, se evalúa la persistencia de datos y se verifican las respuestas del modelo. |
| **Informe y Cierre** | 13 al 14 de febrero de 2025 | Auditoría de resultados y consolidación de hallazgos | Se consolidan hallazgos, se redacta el informe final en `README.md`, se organizan evidencias y se formulan recomendaciones finales. |

---

## Cuadro N.° 3 – Cronograma de Actividades

### **Fase 1: Planificación (Semanas 1)**

| **Semana** | **Fechas** | **Actividades Detalladas** | **Responsable (Lead / Soporte)** | **Entregable** | **Instrumento** |
|------------|------------|-----------------------------|-----------------------------------|-----------------|------------------|
| **Semana 1** | 01/02 – 03/02 | - Reunión inicial de planificación.<br>- Revisión del repositorio y estructura del sistema.<br>- Definición del alcance, objetivos y criterios.<br>- Identificación de componentes críticos: backend, frontend, RAG, SQLite, Docker.<br>- Elaboración del plan preliminar. | Lead: Ericka E. Martínez Yufra<br>Soporte: Auditor Backend | Plan de auditoría aprobado | Acta de reunión inicial, plan preliminar |

---

### **Fase 2: Revisión Documental (Semana 2)**

| **Semana** | **Fechas** | **Actividades Detalladas** | **Responsable (Lead / Soporte)** | **Entregable** | **Instrumento** |
|------------|------------|-----------------------------|-----------------------------------|-----------------|------------------|
| **Semana 2** | 04/02 – 06/02 | - Revisión de scripts backend (`main.py`, `ingest.py`).<br>- Revisión del código del pipeline RAG.<br>- Verificación de la estructura del frontend.<br>- Revisión completa de Dockerfiles y `docker-compose.yml`.<br>- Revisión de la configuración de Nginx. | Lead: Auditor Técnico<br>Soporte: Auditor IA | Informe de revisión documental | Evidencias de código, capturas del repositorio |

---

### **Fase 3: Análisis Técnico Funcional (Semana 2 – 3)**

| **Semana** | **Fechas** | **Actividades Detalladas** | **Responsable (Lead / Soporte)** | **Entregable** | **Instrumento** |
|------------|------------|-----------------------------|-----------------------------------|-----------------|------------------|
| **Semana 2 (continuación)** | 07/02 – 08/02 | - Pruebas del router de intenciones.<br>- Ejecución del modelo LLM en Ollama.<br>- Evaluación del parser JSON y detección de errores.<br>- Validación de respuestas para cada intención. | Lead: Auditor de Sistemas Inteligentes<br>Soporte: Auditor Backend | Informe de pruebas del router | Capturas, logs, pruebas de intención |
| **Semana 3** | 09/02 – 10/02 | - Pruebas del pipeline RAG: ingesta, chunking, embeddings, vector store.<br>- Pruebas de recuperación real desde la base de conocimiento.<br>- Análisis de relevancia y precisión semántica.<br>- Verificación de la estructura `vector_store/`. | Lead: Auditor IA y Datos<br>Soporte: Auditor Técnico | Informe técnico RAG | Evidencias de ingesta, resultados de recuperación |

---

### **Fase 4: Validación Operativa (Semana 3)**

| **Semana** | **Fechas** | **Actividades Detalladas** | **Responsable (Lead / Soporte)** | **Entregable** | **Instrumento** |
|------------|------------|-----------------------------|-----------------------------------|-----------------|------------------|
| **Semana 3 (continuación)** | 11/02 – 12/02 | - Pruebas del flujo conversacional completo.<br>- Validación del ciclo de retroalimentación (Sí / No).<br>- Pruebas del flujo de creación de tickets en SQLite.<br>- Evaluación del despliegue Docker (backend, frontend y proxy).<br>- Validación de comunicación backend ↔ Ollama. | Lead: Auditor DevOps<br>Soporte: Auditor Backend | Informe de validación operativa | Capturas de Docker, frontend, tickets.db |

---

### **Fase 5: Informe y Cierre (Semana 3)**

| **Semana** | **Fechas** | **Actividades Detalladas** | **Responsable (Lead / Soporte)** | **Entregable** | **Instrumento** |
|------------|------------|-----------------------------|-----------------------------------|-----------------|------------------|
| **Semana 3** | 13/02 – 14/02 | - Consolidación de hallazgos de todas las fases.<br>- Elaboración del informe final en formato Markdown.<br>- Organización de la carpeta `/evidencias`.<br>- Revisión final del informe y cierre de auditoría. | Lead: Ericka E. Martínez Yufra<br>Soporte: Equipo auditor | Informe final de auditoría<br>Carpeta de evidencias | README.md final<br>Carpeta `/evidencias` |


