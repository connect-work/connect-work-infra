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
- `connect-work-infra` referencia esas imágenes y define cómo se ejecutan
  junto con PostgreSQL y Caddy.

## Entorno local

### Requisitos

- Docker con el plugin Docker Compose.
- Python 3.9 o superior y `pipx` para las validaciones locales.

### Validaciones

Desde la raíz del repositorio, instala y activa los hooks locales:

```bash
pipx install pre-commit==4.3.0
pre-commit install
```

Para ejecutar manualmente todas las validaciones:

```bash
pre-commit run --all-files
```

Los hooks comprueban formato básico, YAML, workflows de GitHub Actions,
secretos y la configuración de Docker Compose. El CI repite estas validaciones
y además analiza el historial completo del repositorio en busca de secretos.

### PostgreSQL

Desde la raíz del repositorio:

```bash
cd local
cp .env.example .env
```

Edita `.env` y reemplaza la contraseña de ejemplo antes del primer inicio.

Valida la configuración:

```bash
docker compose --env-file .env config
```

Inicia PostgreSQL:

```bash
docker compose --env-file .env up -d db
docker compose --env-file .env ps
```

La base queda disponible solamente en `127.0.0.1` y en el puerto configurado
por `POSTGRES_PORT`.

Para consultar los logs:

```bash
docker compose --env-file .env logs -f db
```

Para detener el entorno conservando los datos:

```bash
docker compose --env-file .env down
```

No agregues `-v` al comando anterior salvo que quieras eliminar también el
volumen y todos los datos locales.

## Estado actual

El entorno local incluye PostgreSQL con persistencia, healthcheck y acceso
limitado a `127.0.0.1`. La API y la aplicación web se incorporarán cuando sus
repositorios estén disponibles.
