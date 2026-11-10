# Estado del proyecto

Última actualización: 2026-11-07 · por: Codex

## Hecho

- Repositorio `connect-work-infra` creado con `main` como rama predeterminada.
- Ruleset `Protect main` activo: exige pull requests, bloquea eliminaciones y
  force pushes, y requiere resolver las conversaciones antes del merge.
- Base inicial del repositorio preparada con README, exclusión de secretos,
  reglas para agentes, flujo de trabajo, convención de commits, plantilla de
  pull request y registro de decisiones.
- Entorno local de PostgreSQL 18 preparado con volumen persistente,
  healthcheck, rotación de logs y puerto limitado a `127.0.0.1`.
- Validaciones locales y CI configurados con pre-commit, lint de YAML y
  GitHub Actions, detección de secretos y verificación del Compose local.
- Check `Validate repository` ejecutado correctamente y configurado como
  obligatorio para `main`.

## En curso

- Ninguna tarea general en curso.

## Próximo

- Incorporar API y web al Compose local cuando ambos proyectos estén listos.

## Decisiones pendientes

- Proveedor, región y tamaño del VPS.
- Ubicación de staging: mismo VPS que producción o servidor separado.
- Estrategia de merge: merge commit, squash o rebase.
- Estrategia de despliegue a producción: manual o por etiqueta de versión.
- Proveedor, cifrado y retención de los backups externos.

## Bloqueos

- Ninguno.
