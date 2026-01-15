# Support Ticket Automation with AI (n8n)

## 📌 Descripción general

Este proyecto implementa una automatización empresarial para la **gestión inteligente de tickets de soporte**, utilizando **n8n** y **modelos de lenguaje (LLM)**.

El sistema clasifica automáticamente los tickets entrantes, prioriza incidentes críticos, los enriquece con una base de conocimiento interna y notifica al equipo correspondiente.  
Además, mantiene trazabilidad completa mediante logs y backlogs estructurados.

---

## 🖼️ Diagrama general del workflow

> 📍 Diagrama visual del flujo completo  

![Support Ticket Automation Diagram](imgs/Trabajo%20Final%20-%20Support%20Ticket%20Automation%20with%20AI.png)

## 🖼️ Diagrama control errores en workflows

![Support Ticket Automation Diagram](imgs/Worflow%20Error%20Trigger.png)

---

## 🧭 Diagrama lógico del flujo (Mermaid)

```mermaid
flowchart TD
    A[Google Sheets Trigger<br/>Nuevo Ticket] --> B[LLM - Clasificar Prioridad]
    B --> C[Parser - Normalizar Salida]
    C --> D{¿CRITICO?}

    D -- Sí --> E[Buscar en Knowledge Base]
    E --> F[Eliminar Duplicados]
    F --> G[Descargar Archivos MD]
    G --> H[Extraer Texto]
    H --> I[Construir Contexto Unificado]
    I --> J[LLM - Análisis del Ticket Crítico]
    J --> K[Parser - Normalizar Respuesta]
    K --> L[Enviar Email de Alerta]

    D -- No --> M{¿NO_CRITICO?}
    M -- Sí --> N[Registrar en Backlog]
    M -- No --> O[Registrar en Audit Log]
```

### 🛠️ Diagrama del workflow de manejo de errores

```mermaid
flowchart TD
    A[Error Trigger] --> B[Normalizar Error]
    B --> C[Registrar en Google Sheets - Error Log]
    C --> D[Enviar Email de Alerta]
```

🔁 Flujo detallado

1️⃣ Ingreso de tickets

    Fuente: Google Sheets

    Evento: nueva fila agregada

    Campos clave:

        ticket_id

        cliente

        mensaje

        fecha

2️⃣ Clasificación automática con IA

    LLM analiza el contenido del ticket

    Clasifica como:

        CRITICO

        NO_CRITICO

    La salida se normaliza para evitar errores de formato o alucinaciones del modelo

3️⃣ Gestión de tickets críticos

Los tickets críticos:

    Consultan una base de conocimiento interna en archivos .md

    Se genera un análisis enriquecido con:

        Resumen ejecutivo

        Posibles causas

        Acciones sugeridas

    Se envía un email automático al equipo responsable

4️⃣ Gestión de tickets no críticos

    Se almacenan en un backlog estructurado

    Permiten atención asincrónica y planificación futura

5️⃣ Auditoría y control

    Cualquier valor inesperado del LLM se registra en un log

    Permite monitoreo, mejora continua y trazabilidad

🧠 Buenas prácticas aplicadas

    Diseño modular y escalable

    Manejo de errores del LLM

    Separación de responsabilidades

    Enfoque enterprise-ready

    Automatización basada en eventos

🚀 Tecnologías utilizadas

    n8n

    Google Sheets

    Google Drive

    Gemini (LLM)

    Markdown Knowledge Base

📎 Autor

Fernández Nicolás

Proyecto académico – Coderhouse
Automatización y Orquestación con IA
