# connect-work-infra

## Qué es

Repositorio de infraestructura de Conectar Trabajo. Define cómo se ejecutan
juntos la API, la aplicación web, PostgreSQL y el proxy, pero no contiene
código de aplicación ni construye las imágenes de la API o del front.

## Stack previsto

- Docker Compose para orquestar los servicios.
- Caddy como proxy inverso y terminación HTTPS.
- PostgreSQL como base de datos.
- Scripts de shell para provisión, backup y restauración.
- GitHub Actions para validación y sincronización de configuración.

## Comandos

Ejecuta estos comandos desde `local/` después de copiar `.env.example` a
`.env`.

- Validar Compose: `docker compose --env-file .env config`.
- Levantar PostgreSQL: `docker compose --env-file .env up -d db`.
- Ver el estado: `docker compose --env-file .env ps`.
- Ver logs: `docker compose --env-file .env logs -f db`.
- Detener el entorno: `docker compose --env-file .env down`.

## Reglas

- No agregues código de aplicación ni Dockerfiles de `connect-work-api` o
  `connect-work-web`.
- Nunca versiones secretos, archivos `.env` reales, claves SSH, certificados
  privados, dumps de base de datos ni datos de producción.
- Usa tags explícitos para las imágenes; nunca uses `latest`.
- En local, PostgreSQL puede publicar su puerto únicamente en `127.0.0.1`.
- En staging y producción, PostgreSQL debe usar una red interna y no publicar
  puertos hacia el host.
- En staging y producción, solo Caddy puede publicar los puertos 80 y 443.
- No ejecutes `docker compose down -v` en staging ni en producción: elimina
  los volúmenes persistentes.
- No conviertas una decisión pendiente en una regla sin registrarla y obtener
  confirmación del equipo.
- No hagas commits ni push salvo que el desarrollador lo pida explícitamente.

## Contrato con los otros repositorios

`connect-work-api` y `connect-work-web` construyen y publican sus propias
imágenes. Este repositorio referencia esas imágenes y define cómo se
conectan. Comunica cualquier cambio en nombres de servicios, variables de
entorno, healthchecks o procedimientos de despliegue que requiera cambios
coordinados.

## Idioma

- Commits: inglés y siguiendo Conventional Commits.
- Documentación y comunicación con el equipo: español.

## Documentación del proyecto

- Estado general: `docs/STATUS.md`.
- Flujo con agentes y prompts: `docs/WORKFLOW.md`.
- Convención de commits: `docs/COMMITS.md`.
- Decisiones de arquitectura: `docs/decisions/`.
- Traspaso de tareas: `docs/tasks/`.
- Plantilla de pull request: `.github/pull_request_template.md`.

## Al empezar y al terminar

Antes de modificar archivos, revisa el estado de Git, `docs/STATUS.md` y el
archivo de la rama en `docs/tasks/` si existe. Resume el alcance, enumera los
archivos previstos y señala riesgos.

Al terminar, sigue `docs/WORKFLOW.md`, muestra los cambios y su verificación.
No hagas commit salvo que se te solicite expresamente.
