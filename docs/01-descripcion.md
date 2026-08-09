# 01 · Descripción de la app

> ⚠️ **Esta sección tiene que ser tuya.** Lo que sigue es un esqueleto con la info técnica objetiva
> de la app (para que no la tengas que ir a buscar) y preguntas guía. Las respuestas a "por qué la
> elegiste" y "quiénes son los usuarios" las tenés que escribir vos, con tu propio criterio.

## ¿Qué hace la app?

Es una **lista de tareas (to-do list)** web, hecha en Rust:

- Muestra todas las tareas cargadas.
- Permite agregar una tarea nueva (formulario simple, un campo de texto).
- Permite marcar una tarea como completada / no completada.
- Permite borrar una tarea.
- Muestra un mensaje de confirmación/error (flash message) después de cada acción.

Es una única página (`/`) que se recarga en cada acción — no usa JavaScript ni SPA, todo el
render es server-side con templates de Tera.

**Stack técnico:**

| Capa           | Tecnología                                  |
| -------------- | -------------------------------------------- |
| Lenguaje       | Rust                                         |
| Framework web  | Actix-web 4                                  |
| Base de datos  | PostgreSQL (vía `sqlx`, con queries verificadas en tiempo de compilación) |
| Templates      | Tera (motor de templates tipo Jinja2)        |
| Sesiones       | Cookie firmada (`actix-session`)             |

**Código fuente base:** [render-examples/actix_todo](https://github.com/render-examples/actix_todo)
(fork del ejemplo oficial de `actix/examples`), licencia MIT.

## ¿Por qué la elegiste?

> ✍️ **Completar.** Ideas para pensar la respuesta (no copies esto tal cual, es solo para
> orientarte):
> - ¿Te interesa Rust como lenguaje / querías ver un ejemplo real de backend en Rust?
> - ¿Te resultó útil por ser chica y simple, y así poder enfocarte en la parte de arquitectura
>   más que en pelear con el código?
> - ¿Pensás usar algo similar (gestión de tareas/estado) como base de alguna idea propia?

## ¿Quiénes son los usuarios?

> ✍️ **Completar.** Por ejemplo, podés imaginar un escenario concreto:
> - ¿Es una app personal (un solo usuario, vos)?
> - ¿Es para un equipo interno (empleados de una empresa gestionando tareas propias)?
> - ¿Es pública (cualquiera puede crear su lista)?
>
> Esta decisión va a impactar directamente en `03-arquitectura-aws.md` (necesidad de auth,
> multi-tenancy, escalado) y en `06-disaster-recovery.md` (horarios de uso, criticidad).

## Base de datos

**Sí usa base de datos: PostgreSQL.**

Esquema (una sola tabla):

```sql
CREATE TABLE tasks (
  id SERIAL PRIMARY KEY,
  description VARCHAR NOT NULL,
  completed BOOLEAN NOT NULL DEFAULT 'f'
);
```

> ✍️ **Completar:** justificá por qué una base relacional (Postgres) tiene sentido acá — por
> ejemplo, pensá en que los datos son estructurados y con pocas relaciones, que no hay necesidad
> de escalado masivo ni de un modelo de documentos, etc. Si en tu arquitectura AWS pensás
> reemplazarla por otra cosa (DynamoDB, Aurora, RDS), explicá por qué.
