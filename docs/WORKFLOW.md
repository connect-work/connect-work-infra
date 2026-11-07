# Flujo de trabajo con agentes

Este documento estandariza cómo iniciar, continuar y cerrar una tarea cuando
participan distintos desarrolladores o agentes de programación.

## Principios

- `AGENTS.md` contiene reglas permanentes y debe cambiar poco.
- `docs/STATUS.md` refleja hitos y estado general, no el detalle diario.
- `docs/tasks/<rama>.md` conserva el contexto temporal de una tarea en curso.
- El agente propone; el desarrollador revisa y decide.
- El agente no hace commit ni push salvo que se le solicite explícitamente.

## Al iniciar una tarea

Crea primero una rama corta (`feat/...`, `fix/...`, `docs/...` o `chore/...`) y
usa este prompt:

```text
Lee AGENTS.md y docs/STATUS.md. Si existe docs/tasks/<rama>.md, léelo también.

Mi tarea: <descripción>.

Antes de escribir código o configuración: resume lo que entendiste, lista los
archivos que planeas tocar y los riesgos. Espera mi confirmación.
```

## Después de implementar y verificar

Usa este prompt antes de cerrar la tarea:

```text
La implementación terminó. Ahora:
1) Actualiza docs/STATUS.md solo si cambió el estado general.
2) Si tomamos una decisión de arquitectura, crea un ADR en docs/decisions/.
3) Revisa si hay que actualizar README.md o algún .env.example.
4) Indica si connect-work-api o connect-work-web deben cambiar.
5) Redacta la descripción del PR usando la plantilla del repositorio.

No hagas commit: muéstrame primero el diff de la documentación.
```

## Pedir un mensaje de commit

```text
Write the commit message for the staged changes following docs/COMMITS.md.
Show it to me; do not commit.
```

## Traspasar una tarea incompleta

Antes de cambiar de persona o agente, usa este prompt:

```text
Crea o actualiza docs/tasks/<rama>.md con el objetivo, qué está hecho, qué
falta, archivos tocados, comandos para verificar y problemas conocidos.
Propón un mensaje de commit WIP en inglés siguiendo docs/COMMITS.md.
Muéstrame el diff y el mensaje; no hagas commit hasta que te lo confirme.
```

El archivo de traspaso debe seguir la plantilla de `docs/tasks/README.md`.

## Retomar el trabajo de otra persona o agente

```text
Lee AGENTS.md, docs/STATUS.md y docs/tasks/<rama>.md. Revisa `git log -10` y
`git diff main...HEAD`. Dime qué entendiste, qué falta y qué dudas tienes
antes de continuar.
```

## Después del merge

- Elimina `docs/tasks/<rama>.md` si existía.
- Actualiza `docs/STATUS.md` solo si se alcanzó un hito o cambió el estado
  general.
- Si se usa squash merge, el título del PR debe seguir `docs/COMMITS.md`.
