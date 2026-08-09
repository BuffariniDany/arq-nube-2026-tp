# 05 · Estimación de costos

> ✍️ Usá la [AWS Pricing Calculator](https://calculator.aws/) con los servicios que elegiste en
> `03-arquitectura-aws.md` y completá esta tabla con tus propios números. Los valores de acá son
> solo placeholders de ejemplo, no está actualizados con tarifas reales — reemplazalos.

## Estimación mensual (borrador)

| Servicio                  | Configuración estimada        | Costo mensual aprox. |
| -------------------------- | ------------------------------ | --------------------- |
| ECS Fargate (app)          | ej: 0.25 vCPU / 0.5 GB, 1 tarea | `$ ...`                |
| RDS PostgreSQL              | ej: `db.t4g.micro`, single-AZ  | `$ ...`                |
| Application Load Balancer   | —                               | `$ ...`                |
| Data transfer / CloudWatch  | —                               | `$ ...`                |
| **Total estimado**          |                                 | **`$ ...`**            |

## Servicios más costosos de tu arquitectura

> ✍️ Completar: normalmente en este tipo de arquitectura el componente más caro suele ser la
> base de datos (sobre todo si la ponés en Multi-AZ) o el Load Balancer si el tráfico es bajo.
> Identificá cuál es en tu caso y por qué.

## Decisiones para optimizar costos

> ✍️ Completar. Ideas para pensar (no las copies, adaptalas a tu decisión real):
> - ¿Usarías Fargate Spot para la app, ya que no es un servicio crítico 24/7?
> - ¿Te alcanza una instancia `db.t4g.micro` de RDS o necesitás algo más grande?
> - ¿Necesitás Multi-AZ desde el día 1, o lo dejarías para una v2 cuando haya más usuarios?

## Qué evitarías o simplificarías en una primera versión

> ✍️ Completar. Por ejemplo: arrancar sin Multi-AZ, sin CDN, con una sola instancia de ECS sin
> auto scaling, y agregar eso más adelante si el uso lo justifica.
