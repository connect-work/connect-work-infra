# connect-work-infra

Repositorio de infraestructura de **Conectar Trabajo**.

Define cómo se ejecutan y se conectan los componentes del proyecto en los
entornos local, staging y producción. No contiene código de aplicación ni
construye las imágenes de sus servicios.

## Responsabilidades

Este repositorio será la fuente de verdad para:

- La orquestación de servicios con Docker Compose.
- La configuración del proxy inverso y HTTPS con Caddy.
- La configuración de cada entorno mediante archivos `.env.example`.
- Los scripts de provisión, backup y restauración del VPS.
- La documentación de despliegue y las decisiones de infraestructura.

Los secretos, archivos `.env` reales, claves privadas, dumps de base de datos
y datos de producción no deben versionarse.

## Relación con los otros repositorios

- `connect-work-api` contiene la API desarrollada con FastAPI y publica su
  propia imagen de contenedor.
- `connect-work-web` contiene la aplicación Next.js y publica su propia imagen
  de contenedor.
- `connect-work-infra` referencia esas imágenes y define cómo se ejecutan junto
  con PostgreSQL y Caddy.

## Estado actual

El repositorio se encuentra en su etapa inicial. La configuración de Docker
Compose, los entornos y los scripts operativos se incorporarán de forma
incremental y se documentarán a medida que existan.
