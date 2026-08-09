# 01 · Descripción de la app

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
Estoy practicando aprende Rust de forma autodidacta porque me interesa el diseño de software bajo principios SOLID:
| Letra | Principio                     | En inglés                                 | Idea principal                                                                                      |
| ----- | ----------------------------- | ----------------------------------------- | --------------------------------------------------------------------------------------------------- |
| **S** | **Responsabilidad Única**     | **Single Responsibility Principle (SRP)** | Una clase debe tener **una sola razón para cambiar**.                                               |
| **O** | **Abierto/Cerrado**           | **Open/Closed Principle (OCP)**           | El software debe estar **abierto a extensión, pero cerrado a modificación**.                        |
| **L** | **Sustitución de Liskov**     | **Liskov Substitution Principle (LSP)**   | Una subclase debe poder **sustituir a su clase base** sin romper el comportamiento esperado.        |
| **I** | **Segregación de Interfaces** | **Interface Segregation Principle (ISP)** | Es mejor tener **interfaces pequeñas y específicas** que una interfaz grande y general.             |
| **D** | **Inversión de Dependencias** | **Dependency Inversion Principle (DIP)**  | Los módulos de alto nivel no deben depender de detalles; ambos deben depender de **abstracciones**. |



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
