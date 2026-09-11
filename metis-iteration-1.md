# METIS — Instrucciones de Iteración #1

> Documento de iteración derivado de la reunión de demostración del 11 de septiembre de 2026.
> Diseñado para ser enviado directamente a una herramienta de prototipado AI (ej. Open Sign / Lovable) junto con `evalia-prompt.md`.

## Contexto

Reunión de demostración donde Rob Moya (Pengyi Labs) presentó el prototipo de METIS a un colega académico experto en educación. El objetivo fue recoger feedback sobre la plataforma de evaluación educativa impulsada por IA.

### Problema identificado
Los estudiantes usan IA para sus tareas y evaluaciones. Los docentes no tienen visibilidad sobre cómo los estudiantes llegaron a sus respuestas, ni del tiempo o el proceso de razonamiento que siguieron.

### Propuesta de METIS
Agente de IA configurado por el docente con rúbricas e instrucciones específicas. El agente **no** da la respuesta final — guía el razonamiento del estudiante con preguntas y pistas pedagógicas. Todas las conversaciones quedan registradas y visibles para el docente.

### Flujo de la evaluación
1. El docente configura el agente con rúbricas e instrucciones.
2. El estudiante interactúa libremente con el agente durante la evaluación.
3. El agente guía el razonamiento sin revelar la respuesta correcta.
4. Las conversaciones quedan registradas y visibles.

---

## Lista de elementos para esta iteración

### 1. Agente Inteligente (IA)
- **[ALTA]** Mejorar el sistema de configuración de rúbricas para que el docente defina fácilmente las instrucciones del agente (no dar respuestas directas, guiar el razonamiento, proporcionar pistas pedagógicas).
- **[ALTA]** Implementar lógica para que el agente adapte su comportamiento según el tipo de pregunta (selección múltiple vs. desarrollo) — permitir al docente habilitar/deshabilitar el agente por pregunta.
- **[MEDIA]** Agregar capacidades para que el agente proporcione ejercicios de ejemplo y material de repaso configurado por el docente durante la interacción.
- **[MEDIA]** Implementar sistema de "niveles de ayuda" configurables por el docente (nivel 1 = solo preguntas guía; nivel 2 = pistas más directas; nivel 3 = ejemplos parciales).
- **[BAJA]** Agregar opción para que el agente sugiera materiales de estudio específicos según las dificultades detectadas en la conversación.

### 2. Experiencia del Estudiante (UX)
- **[ALTA]** Diseñar interfaz de chat intuitiva para que el estudiante interactúe naturalmente con el agente durante la evaluación.
- **[ALTA]** Crear vista de historial de conversación donde el estudiante pueda revisar su propio proceso de razonamiento después de la evaluación.
- **[MEDIA]** Implementar indicadores visuales de progreso que muestren en qué punto del proceso de razonamiento está el estudiante.
- **[MEDIA]** Agregar opción para que el estudiante marque preguntas donde necesitó más ayuda del agente (auto-reflexión).
- **[BAJA]** Diseñar modo "vista padre" donde los padres puedan ver un resumen simplificado de cómo sus hijos interactúan con la IA.

### 3. Reportes para Docentes (Analíticas)
- **[ALTA]** Crear dashboard de docente que muestre todas las conversaciones de estudiantes, filtrables por pregunta, estudiante o nivel de dificultad.
- **[ALTA]** Implementar sistema de "preguntas más comunes" que identifique automáticamente las dudas frecuentes durante la evaluación.
- **[MEDIA]** Generar reportes comparativos mostrando cómo diferentes estudiantes abordaron la misma pregunta (patrones de razonamiento).
- **[MEDIA]** Crear analíticas de tiempo (cuánto dedicó cada estudiante a cada pregunta y cómo varió con el nivel de ayuda del agente).
- **[BAJA]** Implementar sistema de alertas notificando al docente patrones de dificultad inusuales (ej. muchas preguntas en poco tiempo).

### 4. Funcionalidades Nuevas (Feature)
- **[ALTA]** Crear módulo de "Evaluación Continua" para que el agente haga seguimiento del progreso del estudiante a lo largo del curso.
- **[ALTA]** Implementar "banco de preguntas inteligente" donde el docente cree preguntas con niveles de dificultad y el agente seleccione según el desempeño.
- **[MEDIA]** Agregar "evaluación entre pares" donde estudiantes vean (anónimamente) cómo otros abordaron las mismas preguntas.
- **[MEDIA]** Crear sistema de "rúbricas colaborativas" donde docentes compartan y reutilicen configuraciones de agentes exitosas.
- **[BAJA]** Implementar exportación de datos para investigación académica (formatos de análisis cualitativo).

### 5. Colaboración Académica (Integración)
- **[ALTA]** Crear programa de "investigadores invitados" que usen METIS como artefacto de investigación a cambio de publicar hallazgos.
- **[ALTA]** Establecer partnership con departamentos de evaluación educativa para feedback experto durante el desarrollo.
- **[MEDIA]** Crear módulo de "experimentos controlados" comparando resultados con y sin el agente METIS.
- **[MEDIA]** Implementar sistema de "casos de éxito" para compartir mejores prácticas.
- **[BAJA]** Desarrollar API para integración con LMS existentes (Canvas, Moodle, Classroom, etc.).

### 6. Datos y Privacidad (Backend)
- **[ALTA]** Implementar anonimización de datos para reportes agregados que proteja la privacidad de estudiantes.
- **[ALTA]** Crear sistema de permisos granular para que el docente controle qué información comparte con la organización.
- **[MEDIA]** Implementar retención de datos configurable (conversaciones eliminadas tras X meses si no se marcan como "caso de estudio").
- **[MEDIA]** Crear sistema de backup y exportación para que las instituciones puedan migrar sus datos.

---

## Notas adicionales para el prototipado

- **Enfoque pedagógico:** la IA debe ser una herramienta de aprendizaje, no un sustituto del pensamiento. El agente debe guiar, no dar respuestas.
- **Visibilidad es clave:** el mayor valor diferencial de METIS es que el docente puede ver el proceso de razonamiento del estudiante, no solo el resultado.
- **Mercado objetivo:** docentes innovadores que ya usan tecnología, instituciones educativas preocupadas por el uso ético de IA, y padres de familia en niveles preuniversitarios.
- **Potencial de investigación:** METIS puede servir como artefacto para estudios sobre el impacto de la IA en la educación.
- **Escalabilidad:** diseñar para múltiples niveles educativos (primaria, secundaria, universidad) y tipos de evaluación (selección múltiple, desarrollo, ensayos).

---

*Generado el 12 de septiembre de 2026 | Pengyi Labs — Proyecto METIS (CRCLCN/EVALIA)*