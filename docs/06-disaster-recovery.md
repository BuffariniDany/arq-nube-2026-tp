# 06 · Pensamiento arquitectónico y Disaster Recovery

> ⚠️ Esta es la sección con más peso (25%) y la que más tiene que reflejar tu propio análisis.
> Te dejo la estructura y preguntas del enunciado, con algunas pistas específicas de esta app,
> pero las respuestas y las decisiones (RTO/RPO, estrategia de DR) tenés que definirlas vos en
> base a lo que respondiste en `01-descripcion.md` sobre los usuarios.

## Usuarios y disponibilidad

- ¿Quiénes usan la app? (depende de lo que definiste en `01-descripcion.md`)
- ¿En qué horarios la usan? → ¿cuándo podés hacer mantenimiento sin impacto?
- ¿Qué pasa si la app cae en horario pico? ¿Cuál es el impacto real?

> ✍️ Completar. Pensalo en función de si elegiste usuarios internos (impacto = gente de la
> empresa no puede gestionar sus tareas, molesto pero no catastrófico) vs. público general.

## Riesgos y reglas

- ¿Qué reglas o regulaciones afectan a tu app? (privacidad de datos, compliance, etc.)
- ¿Qué riesgos técnicos o de negocio identificás?

> ✍️ Completar. Para una to-do list simple, pensá si hay datos sensibles (¿las descripciones de
> tareas podrían contener información personal o confidencial?) y qué implicancias tiene eso.

## Plan de recuperación

**Escenarios de falla a contemplar** (pensalos para tu arquitectura de AWS, no la local):

- Caída de una Availability Zone completa.
- Corrupción o borrado accidental de datos (ej: alguien corre un `DELETE` sin `WHERE`).
- Error humano en un deploy (ej: se rompe la imagen de la app y no arranca ningún contenedor).

> ✍️ Completar: elegí 2 o 3 escenarios concretos y explicá qué pasaría y cómo lo mitigarías.

**RTO (Recovery Time Objective):** ¿cuánto tiempo podés estar caída?

> ✍️ Completar con un número concreto (ej: "30 minutos" o "4 horas") y la justificación de por
> qué ese número tiene sentido para tus usuarios.

**RPO (Recovery Point Objective):** ¿cuántos datos podés perder?

> ✍️ Completar (ej: "hasta 1 hora de datos" si hacés backups horarios de RDS).

**Estrategia de DR:** Backup & Restore / Pilot Light / Warm Standby / Multi-Site

> ✍️ Completar y justificar cuál elegiste. Para una app de este tamaño y criticidad, probablemente
> **Backup & Restore** sea razonable (es la más económica) — pero justificá vos por qué, o por
> qué elegirías otra.

**¿Cómo harías backups?**

> ✍️ Completar. Pistas: snapshots automáticos de RDS, retención (¿cuántos días?), si los
> replicarías a otra región.
