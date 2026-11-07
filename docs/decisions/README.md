# Decisiones de arquitectura

Esta carpeta contiene los registros de decisiones de arquitectura (ADR) de
`connect-work-infra`. Un ADR explica el contexto de una decisión importante,
la alternativa elegida y sus consecuencias.

## Cuándo crear un ADR

Crea un ADR cuando una decisión sea costosa de revertir o afecte a más de un
entorno o repositorio. Por ejemplo:

- Arquitectura de despliegue y ubicación de los entornos.
- Redes, persistencia y exposición de servicios.
- Estrategia de backups y restauración.
- Proxy, dominios, certificados y seguridad del VPS.
- Coordinación del despliegue entre API, web e infraestructura.

No hace falta un ADR para ajustes rutinarios que no cambien la arquitectura.

## Nombre y estado

Usa un número secuencial y un título corto:

```text
NNNN-titulo-corto.md
```

Estados posibles:

- `propuesta`: todavía está en discusión.
- `aceptada`: el equipo decidió aplicarla.
- `reemplazada por NNNN`: una decisión posterior la sustituyó.

Cuando cambie una decisión aceptada, crea un ADR nuevo y marca el anterior
como reemplazado en lugar de borrar su historia.

## Plantilla

```markdown
# NNNN. Título

Fecha: AAAA-MM-DD · Estado: propuesta | aceptada | reemplazada por NNNN

## Contexto

## Decisión

## Alternativas descartadas

## Consecuencias
```

Los ADR se escriben en español y nunca deben contener secretos ni datos
personales.
