# grill-the-plan

> Resolver cada decisión abierta antes de escribir código.

**Interrogar el plan** · Skill para agentes de código de la comunidad [nvvdev](https://github.com/nvv-dev). Funciona en Claude Code como plugin o como skill suelta, y en cualquier agente compatible con el formato abierto [`SKILL.md`](https://agentskills.io).

*English summary at the end.*

## Qué hace

Recorre una spec o un plan como un árbol de decisiones y te hace una pregunta a la vez, con opciones y una recomendación. Con cada respuesta actualiza el glosario del dominio y redacta un ADR si la decisión es costosa de revertir. No deja pasar del spec al plan con dudas abiertas.

## Objetivo

Que la ambigüedad cueste una pregunta hoy y no una reescritura en la revisión.

## Cuándo usarla

- Antes de pasar de la especificación al plan técnico
- Cuando un plan "se siente" incompleto

## Cuándo no

- Tareas pequeñas y claras

## Ejemplo

```text
/grill-the-plan sobre specs/001-checkout/spec.md
```

## Cómo se activa

Esta skill **solo se activa a mano** (`disable-model-invocation: true`): no ocupa contexto en cada sesión y la invocas cuando la necesitas:

- Instalada como plugin: `/grill-the-plan:grill-the-plan`
- Copiada a `.claude/skills/`: `/grill-the-plan`

## Instalación

### Opción 1: Claude Code, como plugin (recomendada)

Dentro de Claude Code:

```text
/plugin marketplace add nvv-dev/claude-plugins
/plugin install grill-the-plan@nvvdev
```

La primera línea agrega el catálogo de nvvdev una sola vez; la segunda instala esta skill. Si prefieres el paquete completo, instala `dev-workflow@nvvdev` en su lugar (incluye esta skill y las demás de [dev-workflow](https://github.com/nvv-dev/dev-workflow)); no instales los dos a la vez.

### Opción 2: Claude Code, copiando la skill

Para un solo proyecto (se comparte con tu equipo por git):

```bash
git clone --depth 1 https://github.com/nvv-dev/grill-the-plan.git /tmp/grill-the-plan
mkdir -p .claude/skills
cp -R /tmp/grill-the-plan/skills/grill-the-plan .claude/skills/
```

Para todos tus proyectos, cópiala en `~/.claude/skills/` en lugar de `.claude/skills/`.

### Opción 3: otros agentes

Copia la carpeta `skills/grill-the-plan/` en la carpeta de skills de tu agente (cada agente documenta la suya). Con la CLI [skills](https://github.com/vercel-labs/skills) de Vercel Labs:

```bash
DISABLE_TELEMETRY=1 npx skills add nvv-dev/grill-the-plan
```

### Verificar

Abre una sesión nueva y pregunta "¿qué skills tienes disponibles?"; `grill-the-plan` debe aparecer. Con el plugin, `/plugin` la muestra como instalada.

### Actualizar o desinstalar

- Plugin: `/plugin marketplace update nvvdev` para actualizar; `/plugin uninstall grill-the-plan@nvvdev` para quitarla.
- Copia manual: repite la copia para actualizar, o borra la carpeta `.claude/skills/grill-the-plan`.

Antes de instalar cualquier skill, incluida esta, conviene leerla: es un solo archivo, [`skills/grill-the-plan/SKILL.md`](skills/grill-the-plan/SKILL.md). Ver [vetting-external-skills](https://github.com/nvv-dev/vetting-external-skills).

## Contenido

| Ruta | Qué es |
|---|---|
| `skills/grill-the-plan/SKILL.md` | La skill: instrucciones en inglés para que los escáneres de seguridad las analicen completas; el agente responde en tu idioma |
| `.claude-plugin/plugin.json` | Manifiesto para instalarla como plugin |
| `.github/workflows/` | Validación de estructura y escaneo con SkillSpector en cada cambio |

## Contribuir

Este repo se **genera** desde [nvv-dev/dev-workflow](https://github.com/nvv-dev/dev-workflow), donde vive la versión canónica. Abre issues y PRs allí. La mejor contribución es un caso real en la sección *Known failures* de la skill, con la regla que lo evita.

## Origen

Escrita desde cero por nvvdev. Inspirada en: [mattpocock/skills](https://github.com/mattpocock/skills) (grill-with-docs).

## Licencia

MIT.

---

## English

**grill-the-plan** — Walks a spec or plan one question at a time, updating the glossary and drafting ADRs as decisions are made.

Install in Claude Code with `/plugin marketplace add nvv-dev/claude-plugins` and `/plugin install grill-the-plan@nvvdev`, or copy `skills/grill-the-plan/` into `.claude/skills/` (project) or `~/.claude/skills/` (personal). Other agents: copy the folder into their skills directory, or run `DISABLE_TELEMETRY=1 npx skills add nvv-dev/grill-the-plan`. Manual-only skill: invoke it with `/grill-the-plan:grill-the-plan` (plugin) or `/grill-the-plan` (copied). Canonical source: [nvv-dev/dev-workflow](https://github.com/nvv-dev/dev-workflow). License: MIT.
