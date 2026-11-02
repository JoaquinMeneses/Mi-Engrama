# AGENTS.md

Contrato de trabajo para cualquier agente de IA que opere sobre la bóveda.

El `README.md` explica el *por qué* en lenguaje humano. Este archivo define el *qué* y el *cómo*. **Si los dos se contradicen, gana este archivo.**

---

## 1. Protocolo de arranque

Antes de escribir una sola línea:

1. Leer este archivo completo.
2. Leer el `_index.md` y el `_log.md` del tema involucrado.
3. Verificar que la estructura real coincida con la de la sección 2.
4. Si no coincide: **no escribir nada**. Reportar la diferencia y esperar instrucciones.

Una discrepancia entre el filesystem y este documento significa que el esquema quedó desactualizado. Nunca se resuelve improvisando: se resuelve reportando.

## 2. Mapa de la bóveda

| Ruta | Qué es | Quién escribe |
|---|---|---|
| `00-Inbox/` | Bandeja de entrada. Todo entra acá primero | Humano |
| `01-Proyectos/` | Esfuerzos con objetivo y fecha de cierre | Humano |
| `02-Áreas/` | Responsabilidades continuas, sin fecha de fin | Humano |
| `03-Recursos/[Tema]/` | Fuentes crudas del tema | Humano |
| `03-Recursos/[Tema]/Síntesis/` | Wiki generada y mantenida por IA | **Agente** |
| `04-Archivos/` | Espejo inactivo de 01, 02 y 03 | Humano |

Reglas de estructura:

- Las cinco raíces llevan prefijo de dos dígitos (`00` a `04`). Son fijas: no se renombran, no se reordenan alfabéticamente, no se agregan.
- `04-Archivos/` espeja la numeración: `01-Proyectos/`, `02-Áreas/`, `03-Recursos/`.
- El resto de las carpetas se ordena alfabéticamente.
- Las carpetas de tema (`03-Recursos/[Tema]/`) **las crea el humano**. El agente puede sugerir nombres y reorganizaciones; nunca crea la carpeta por su cuenta.
- Cada `Síntesis/` contiene obligatoriamente `_index.md` y `_log.md`.
- Toda carpeta que pueda quedar vacía conserva un `.gitkeep`: git no versiona carpetas vacías. El agente no lo modifica ni lo borra.

## 3. Autoridad por capa

| Capa | Puede | No puede |
|---|---|---|
| **Fuentes** | Mover de `00-Inbox/` al tema. Normalizar el frontmatter. Leer. | Editar el cuerpo. Renombrar. Borrar. |
| **Síntesis** | Crear páginas, actualizarlas, enlazarlas, marcar `estado`. | Borrar o reescribir una página completa sin permiso. |
| **Esquema** | Proponer cambios a `AGENTS.md` y `README.md`. | Aplicarlos sin pedido explícito. |

Cuatro prohibiciones absolutas:

1. **Nunca borrar un archivo** sin confirmación explícita.
2. **Nunca reescribir por completo** una página de síntesis existente sin confirmación explícita.
3. **Nunca modificar el cuerpo ni el nombre** de una fuente.
4. **Nunca tocar** `.obsidian/` ni `.git/`.

Actualizar una página con una sección nueva, un enlace o una corrección puntual no requiere permiso. Reemplazarla entera, sí.

## 4. Nomenclatura

- **El título de una nota es único en toda la bóveda.** Obsidian resuelve `[[enlace]]` por nombre de archivo: dos notas con el mismo título producen enlaces ambiguos.
- La página de síntesis lleva el nombre del **concepto**, nunca el del archivo fuente.
- Sin prefijos, sin numeración, sin `_` ni `-` como separadores de palabras, sin fechas en el nombre.
- `_index.md` y `_log.md` usan guion bajo para ordenar primero.

## 5. Frontmatter

**Fuentes.** Se normalizan una sola vez, al ingerir, y después no se tocan:

- `author` como texto plano. Algunas herramientas de origen (un clipper, un exportador, un copiar y pegar desde otra aplicación) escriben ese campo como wikilink (`[[Tiago Forte]]`) o como ID numérico de cuenta (`[[262588213843476]]`); ambos apuntan a notas inexistentes y ensucian el grafo.
- No agregar campos nuevos ni reescribir el cuerpo de la fuente.

**Síntesis.**

```yaml
---
tipo: sintesis
tema: Productividad
estado: vigente
fuentes:
  - "[[Método PARA]]"
actualizado: 2026-11-02
---
```

- `estado`: `vigente` | `revisar` | `obsoleto`. `revisar` marca deuda de verificación.
- `actualizado` se reescribe en cada modificación de la página.

## 6. Flujo de ingesta

Una fuente por vez. En lote solo si el humano lo pide explícitamente.

1. Detectar la fuente nueva en `00-Inbox/`.
2. Clasificar con la pregunta de accionabilidad: ¿tiene fecha de cierre? → proyecto. ¿Responsabilidad continua? → área. ¿Tema de estudio? → recurso.
3. Normalizar el frontmatter y mover la fuente a `03-Recursos/[Tema]/`. Sin cambiarle el nombre ni el cuerpo.
4. Leer la fuente completa y decir en cinco líneas de qué trata y qué cambia respecto de lo que ya está en la wiki.
5. Crear o actualizar páginas en `Síntesis/`.
6. Actualizar `_index.md`.
7. Agregar la entrada en `_log.md`.
8. Verificar: sin huérfanas, sin enlaces rotos, sin títulos duplicados.
9. Reportar.

**Formato de reporte**, siempre igual:

```text
Fuente: <nombre> → <tema>
Páginas creadas: [[...]]
Páginas actualizadas: [[...]]
Índice: actualizado
Log: [YYYY-MM-DD] ingesta | <título>
Enlaces: OK | rotos: <lista>
```

## 7. Reglas de escritura en la síntesis

- **Toda afirmación se rastrea a una fuente.** Sin fuente, no se escribe.
- **Una idea por página.** Si el concepto ya existe, se actualiza; no se duplica.
- **Toda página se alcanza desde `_index.md`.** Una página sin enlaces entrantes es un error.
- **La síntesis no enlaza a proyectos ni a áreas.** Debe poder archivarse junto con el tema sin dejar enlaces rotos. La dirección es unidireccional.
- **Toda página enlaza hacia atrás a la fuente** que la originó.
- **No se dejan enlaces `[[...]]` sin destino** al terminar una operación.
- **Español neutro.** Sin voseo, sin slang, sin primera persona.
- **No inventar** fechas, autores, citas ni datos.

### 7.1 Granularidad de la síntesis

Una fuente no genera una página con su nombre: genera **páginas de concepto**.

- **Una idea, una página.** Si el concepto ya existe, se actualiza.
- **Dos fuentes sobre el mismo sistema no se duplican: se cruzan.** Una página, dos fuentes en el frontmatter.
- **Proporción:** 1 fuente ≈ 1-2 páginas propias, más las actualizaciones que provoca en las existentes.
- **Tamaño:** 40 a 80 líneas, y una sola pregunta respondida por página.

**Indicador de salud:** cuando el tema ya tiene contenido, toda ingesta debe **tocar al menos una página existente**. Si una fuente solo crea páginas nuevas, se está apilando información, no sintetizando.

| Anti-patrón | Por qué está mal |
|---|---|
| Una página por sección del artículo | Es un índice disfrazado, no una wiki |
| Página nombrada como el archivo fuente | Ata la página a un archivo; tres fuentes sobre el mismo tema producen tres resúmenes redundantes |
| Una página gigante que cubre todo el artículo | No se puede enlazar: no hay concepto que enlazar |
| Doce páginas por artículo | El `_index.md` deja de ser navegable y el lint se vuelve imposible |

## 8. Consulta

1. Leer `_index.md` del tema.
2. Bajar solo a las páginas relevantes.
3. Responder con cita a la fuente.
4. Si la respuesta aporta algo nuevo y estable, proponer archivarla como página nueva.

## 9. Lint

Reportar, no corregir sin permiso:

- Contradicciones entre páginas.
- Afirmaciones que una fuente nueva dejó obsoletas.
- Huérfanas sin enlaces entrantes.
- Títulos duplicados.
- Enlaces sin destino.
- Conceptos mencionados sin página propia.
- Páginas con `estado: revisar`.

## 10. Notas de ejemplo

La plantilla se distribuye con notas introductorias marcadas `estado: ejemplo` en el frontmatter.

- El agente **no las cita, no las indexa y no las modifica**.
- Si detecta notas de ejemplo al empezar a trabajar en un tema, pregunta **una sola vez** si se quieren borrar para dejar la bóveda vacía.
- Borrarlas es la única excepción autorizada de antemano a la prohibición 1 de la sección 3, y solo ante respuesta afirmativa.

## 11. Git

El agente no asume que el humano conoce git. Por eso:

- **No commitea por iniciativa propia.** El backup automático puede estar activo y es suficiente.
- **Si el humano lo pide**, ejecuta él mismo el commit: `git add` solo de los archivos que tocó, mensaje en Conventional Commits, sin atribución ni `Co-Authored-By`. Explica en una línea qué hizo.
- Nunca `git add -A`, nunca `git reset --hard`, nunca `git push --force`.
- Si el pedido incluye subir los cambios, hace el push después del commit.

## 12. Cuando falta información

- Una sola pregunta, con la decisión concreta y la consecuencia de cada opción.
- Si el tema no existe: proponer el nombre y esperar.
- Si la fuente no encaja en ningún tema: proponer y esperar.
- Si dos temas compiten: presentar los dos y esperar.
