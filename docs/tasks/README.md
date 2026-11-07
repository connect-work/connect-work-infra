# Traspaso de tareas

Esta carpeta contiene el contexto temporal de tareas que todavía no terminaron.
Cada tarea en curso debe tener un único archivo asociado a su rama.

Por ejemplo, para la rama `chore/bootstrap-infra-repository` se usaría:

```text
docs/tasks/chore/bootstrap-infra-repository.md
```

El archivo debe crearse o actualizarse antes de entregar la tarea a otra
persona o agente, y eliminarse cuando la rama se fusione.

## Plantilla

```markdown
# <rama>

Objetivo:

Hecho:

Falta:

Archivos tocados:

Cómo verificar (comandos):

Problemas conocidos / dudas:

Última actualización: <fecha> · <agente o desarrollador>
```

## Criterios de uso

- Registra solo información necesaria para retomar la tarea.
- Mantén el estado general del proyecto en `docs/STATUS.md`.
- No copies reglas permanentes de `AGENTS.md`.
- No incluyas secretos, credenciales ni datos personales.
- Borra el archivo de la tarea después del merge.
