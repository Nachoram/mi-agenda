# CLAUDE.md

Guía para asistentes de IA que trabajen sobre este repositorio.

> ℹ️ **Idioma del repositorio**: español. Todos los archivos, plantillas, commits y respuestas al usuario deben mantenerse en español.

---

## ¿Qué es este repositorio?

`mi-agenda` **no es un proyecto de software**. Es una bóveda de notas en Markdown (estilo Obsidian) para gestionar la vida profesional y personal del usuario: clientes legales, juicios, finanzas, cumpleaños, eventos, compras y tareas diarias.

No hay `package.json`, build, tests ni dependencias. El "producto" son los archivos `.md` y la coherencia entre ellos.

---

## Estructura

```
mi-agenda/
├── INDEX.md                 # Índice general de la bóveda
├── TAREAS.md                # Lista maestra de tareas (fuente de verdad)
├── Agenda-Hoy.md            # Agenda diaria activa — se REGENERA cada día
├── Agenda/
│   └── Agenda-Hoy.md        # Plantilla original detallada (no se reescribe a diario)
├── Clientes/TEMPLATE.md     # Ficha por cliente
├── Juicios/TEMPLATE.md      # Ficha por caso/juicio
├── Finanzas/TEMPLATE.md     # Resumen mensual
├── Cumpleaños/TEMPLATE.md   # Fechas y regalos (ojo con la ñ en el nombre)
├── Eventos-Sociales/TEMPLATE.md
├── Compras/TEMPLATE.md
├── Vida-Personal/TEMPLATE.md
└── .claude/skills/          # email-composer, mermaid-diagrams, obsidian-markdown
```

**Nota**: `INDEX.md` menciona `Documentos/`, `Negocio/` y `Tareas/` — estas carpetas todavía no existen. Si el usuario pide trabajar con ellas, créalas con un `TEMPLATE.md` siguiendo el patrón del resto.

---

## Flujo de trabajo principal: regenerar la agenda diaria

El uso recurrente es: cada día reescribir `/Agenda-Hoy.md` (raíz) leyendo `TAREAS.md` y las carpetas temáticas. Los commits recientes lo confirman (`Update daily agenda to 2026-05-08`, etc.).

Pasos al regenerar:
1. Lee la fecha actual del contexto del sistema (no la inventes).
2. Lee `TAREAS.md` y cualquier carpeta relevante (Juicios, Clientes, Finanzas, Cumpleaños, Eventos-Sociales, Compras).
3. Reescribe `/Agenda-Hoy.md` (raíz) con el formato existente:
   - Encabezado con día de la semana + fecha en español ("Viernes 8 de Mayo de 2026").
   - Secciones 🔴 URGENTES → 🟡 IMPORTANTES → 🟢 NORMAL → ✅ COMPLETADAS HOY.
   - Cada sección dividida en **Trabajo** y **Personal**.
   - Tabla de "Resumen ejecutivo" con métricas.
   - "💡 CONSEJO DEL DÍA" breve y motivador, adaptado al día de la semana.
   - Pie con "Próximo escaneo: …".
4. Si `TAREAS.md` solo contiene la plantilla vacía ("Tarea 1", "Tarea 2"), **adviértelo explícitamente** en el resumen ejecutivo (como ya se hace en `Agenda-Hoy.md` actual). No inventes tareas reales.
5. **No toques** `/Agenda/Agenda-Hoy.md` (es la plantilla maestra detallada, no la agenda viva).

---

## Convenciones de contenido

- **Markdown sabor Obsidian**: usa wikilinks (`[[Cliente-Nombre]]`, `[[Caso-001]]`) para enlazar entidades entre carpetas. Está la skill `obsidian-markdown` disponible si necesitas callouts, properties o embeds.
- **TEMPLATE.md**: archivo plantilla por carpeta. Cuando crees un registro nuevo (un cliente, un juicio), **copia** el TEMPLATE a un archivo nuevo con nombre descriptivo (p. ej. `Clientes/Juan-Perez.md`); no edites el TEMPLATE.
- **Emojis de prioridad**: 🔴 urgente · 🟡 importante · 🟢 normal · ✅ completado · ⬜ pendiente. Mantén la coherencia.
- **Checkboxes**: `- [ ]` pendiente, `- [x]` hecho.
- **Tablas**: respeta las columnas existentes (Cliente / Caso / Fecha / Estado…). No las renombres por estilo.
- **Fechas**: formato largo en español ("8 de Mayo de 2026") en encabezados; ISO (`2026-05-08`) sólo si el campo lo pide.
- **Moneda**: `$` con monto (sin símbolo de país salvo que ya esté en el archivo).

---

## Convenciones de Git

- Rama de trabajo asignada para cambios de Claude: `claude/add-claude-documentation-ig5FR`. Crea ramas similares para futuras tareas si se piden.
- **Estilo de commits** (observado en historial): título corto en inglés con verbo imperativo, una línea, p. ej.:
  - `Update daily agenda to 2026-05-08`
  - `Add generated daily agenda for 2026-05-05`
  - `Initial commit: Mi_agenda structure with tasks system`
- Tras `push -u origin <rama>`, abre PR en **draft** salvo instrucción contraria.
- No hagas force-push, rebases destructivos ni amends sin pedir permiso.

---

## Qué hacer y qué no hacer

**Sí**:
- Edita archivos existentes preferentemente; no dupliques estructura.
- Pregunta antes de borrar registros del usuario (clientes, casos, finanzas) — son datos personales reales o futuros.
- Si el usuario pide algo ambiguo ("agrega una tarea"), confirma a qué archivo y bloque (Trabajo/Personal, urgente/importante/normal).

**No**:
- No introduzcas código (scripts, automatizaciones) salvo que se pida explícitamente. Este repo es de notas.
- No inventes datos personales (nombres de clientes, juicios, montos) para "rellenar" plantillas.
- No conviertas archivos a otros formatos ni traduzcas al inglés.
- No añadas emojis fuera de los ya establecidos en las plantillas.
- No reescribas `INDEX.md` para "limpiarlo" — las secciones aspiracionales (Documentos/Negocio/Tareas) son intencionales.

---

## Skills disponibles localmente

Bajo `.claude/skills/`:
- `obsidian-markdown` — sintaxis Obsidian (wikilinks, callouts, frontmatter).
- `mermaid-diagrams` — diagramas si se piden visualizaciones.
- `email-composer` — borradores de correo (útil si el usuario pide redactar mensajes a clientes).

Invócalas vía la herramienta Skill cuando apliquen.
