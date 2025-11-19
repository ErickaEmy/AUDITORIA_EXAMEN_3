I. ORIGEN

El presente Informe de Auditoría de Sistemas tiene su origen en la ejecución del Examen de la Unidad III – Auditoría de Sistemas, cuyo objetivo es evaluar la conformidad, el funcionamiento, el código fuente, la arquitectura técnica y los controles implementados en el sistema Mesa de Ayuda con IA desarrollado por Corporate EPIS Pilot.

La necesidad de esta auditoría surge de:

La obligación académica de aplicar un proceso formal de auditoría sobre un sistema real que incorpora arquitectura RAG (Retrieval-Augmented Generation), un router de intenciones mediante LLM, un flujo conversacional guiado, generación de tickets con SQLite, y despliegue mediante Docker y Kubernetes.

La verificación del cumplimiento del diseño declarado por el equipo desarrollador, comparando la implementación real (código, contenedores y comportamiento del sistema) frente al diseño previsto.

La revisión exhaustiva del código backend (FastAPI), código frontend (React + MUI), scripts de ingesta, construcción automática de embeddings, vector store (ChromaDB), y del funcionamiento del modelo LLM ejecutado mediante Ollama.

La necesidad de asegurar la integridad del flujo de creación de tickets, seguimiento de entradas de usuario, manejo de errores, validaciones, seguridad, y consistencia del ciclo de vida conversacional.

La solicitud del docente para que el estudiante:

Clone el sistema.

Levante localmente el servicio con Docker.

Ejecute pruebas técnicas y funcionales.

Documente evidencias.

Elabore el Informe de Auditoría utilizando estructura oficial.

Este Informe constituye el documento formal que consolida todos los resultados obtenidos en el proceso de auditoría ejecutado.

II. INFORMACIÓN DE LA ENTIDAD O DEPENDENCIA

Corporate EPIS Pilot es una unidad de desarrollo experimental enfocada en soluciones empresariales basadas en Inteligencia Artificial, soporte técnico automatizado y sistemas conversacionales avanzados. Desarrolla prototipos listos para producción y herramientas prácticas para gestión empresarial.

Información relevante de la entidad

Nombre del sistema auditado:
Asistente de IA – Mesa de Ayuda Corporativa EPIS Pilot.

Finalidad del sistema:
Proporcionar soporte técnico inteligente a los usuarios, utilizando IA para clasificar consultas, buscar información interna y crear tickets de soporte cuando es necesario.

Naturaleza del sistema:
Sistema modular distribuido compuesto por:

Backend FastAPI con pipeline RAG.

Frontend React/MUI con manejo dinámico del estado conversacional.

Base local vectorial (ChromaDB).

Motor de IA local Ollama (sin dependencias cloud).

SQLite para registro de tickets.

Contenedores Docker con imagenes generadas automáticamente.

Manifiestos Kubernetes para despliegue escalable.

Equipo responsable del desarrollo:
Corporate EPIS Pilot – División de Ingeniería y Automatización.

Ubicación del código fuente:
Repositorio GitHub entregado para el examen.

Características técnicas confirmadas (según código auditado)

Backend ubicado en /backend:

main.py contiene:

Router de intenciones mediante LLM.

Endpoint /ask.

Cadena RAG (RetrievalQA).

Clasificación de intención (pregunta_general, reporte_de_problema, despedida).

Creación real de tickets con SQLite.

Scripts críticos:

ingest.py: creación automática de vector_store.

database_setup.py: creación de tabla tickets.

Dockerfile que genera embeddings dentro de la imagen.

Frontend en /frontend:

Chat completo con:

Bucle de feedback.

Botones condicionales.

Integración del mensaje ACTION_CREATE_TICKET.

Flujo de recopilación de detalles del usuario.

Orquestación:

docker-compose.yml con backend + frontend + proxy.

Nginx como reverse proxy (puerto 5173 → 80).

Esta información constituye la línea base para los procedimientos de auditoría desarrollados más adelante.

III. DENOMINACIÓN DE LA MATERIA DE CONTROL

La materia de control objeto de la auditoría es:

“Auditoría de Sistemas de Código Fuente y Funcionamiento Operativo del Sistema de Mesa de Ayuda con IA – Corporate EPIS Pilot”

El ámbito de control incluye, con carácter obligatorio y verificable:

1. Control del código fuente (backend y frontend)

Validación de correctitud del código Python (FastAPI).

Validación del código React/MUI e interacción con el backend.

Revisión de scripts auxiliares (ingest.py, database_setup.py).

Verificación de modelos y librerías especificadas en requirements.txt.

2. Control de arquitectura RAG implementada

Generación, persistencia y consistencia de la base vector_store/.

Proceso de segmentación, embeddings y carga al vector store.

Funcionamiento de la cadena de recuperación (RetrievalQA).

Integridad y disponibilidad del repositorio de conocimiento (PDF/TXT).

3. Control del router de intenciones

Validación del funcionamiento del LLM llama3.1:8b o smollm:360m.

Verificación del prompt del router.

Pruebas de clasificación en las intenciones declaradas.

Manejo de mensajes ambiguos o sin JSON.

4. Control del flujo de conversación

Validación del bucle de feedback:

“¿Esta información soluciona tu problema?”

Botones (sí/no).

Acciones siguientes (abrir ticket / explicar más).

Confirmación de envío de acciones ACTION_CREATE_TICKET.

5. Control de creación de tickets

Revisión del INSERT en SQLite.

Verificación de persistencia del archivo tickets.db.

Validación del flujo:

Solicitud de descripción → creación de ticket → respuesta del bot.

6. Control de despliegue

Verificación de Dockerfiles del frontend y backend.

Funcionamiento correcto bajo docker compose.

Validación de comunicación backend ↔ Ollama.

Verificación del reverse proxy Nginx.

7. Control de seguridad técnica

Validación de exposición de puertos.

Manejo de CORS.

Uso de extra_hosts y contexto Docker.

Revisión de logs estructurados (loguru).

Evaluación básica de manejo de excepciones.

8. Control de funcionamiento interno

Verificación del endpoint /ask.

Pruebas de recuperación RAG.

Pruebas de error.

Logs de prometheus_fastapi_instrumentator
