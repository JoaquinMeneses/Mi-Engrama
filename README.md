# Mi-Engrama

Bóveda de Obsidian para construir un segundo cerebro: una wiki personal que **acumula** conocimiento en lugar de re-descubrirlo en cada consulta. Combina el método **PARA** para decidir dónde vive cada cosa con el patrón **LLM Wiki** para que un agente de IA mantenga la síntesis.

Es una plantilla: clona el repo, coloca tus fuentes y el agente hace la contabilidad (resúmenes, enlaces, índices, registro).

> **Este documento explica el criterio.** Las reglas que el agente debe cumplir viven en [[AGENTS]], que es el contrato normativo. Si los dos se contradicen, gana `AGENTS.md`.

---

## Requisitos e Integración con Obsidian

**Obsidian** es una aplicación de gestión del conocimiento personal que opera sobre una bóveda (_vault_) de archivos en formato Markdown plano almacenados localmente en tu dispositivo. A diferencia de las herramientas tradicionales que guardan la información en bases de datos propietarias, Obsidian garantiza la portabilidad y propiedad absoluta de tus datos.

Esta arquitectura requiere y aprovecha las capacidades centrales de Obsidian:

- **Enlaces bidireccionales (`[[nota]]`)**: Permiten conectar conceptos e ideas de forma fluida entre la wiki procesada y tus proyectos o áreas.
- **Navegación y Vista de Grafo**: Permite visualizar de forma gráfica la red interconectada de engramas de conocimiento que se van acumulando.
- **Almacenamiento local y abierto**: Al ser archivos `.md` estándar, cualquier modelo de lenguaje o agente de IA puede leer y actualizar la estructura sin depender de exportaciones ni intermediarios.
- **Compatibilidad con plugins**: Permite la integración con herramientas como `obsidian-git` para automatizar el versionado y copia de respaldo en GitHub.

---

## ¿Qué es un "Engrama"?

En neurociencia, un **engrama** es la traza o huella biológica que deja un recuerdo en el cerebro. **Mi-Engrama** traslada ese concepto al ámbito digital: una red viva de notas interconectadas mediante enlaces bidireccionales donde cada nueva fuente de información fortalece y expande tu mapa de conocimiento.

---

## El Método PARA (Tiago Forte)

La estructura raíz del vault sigue el método **PARA** de Tiago Forte, diseñado para organizar la información según su **nivel de accionabilidad** en cuatro categorías principales:

1. **Projects (Proyectos)**: Esfuerzos a corto plazo con un objetivo concreto y una fecha límite definida (ej. *Rediseñar sitio web*, *Comprar computadora*).
2. **Areas (Áreas)**: Responsabilidades continuas que requieren mantenimiento constante a lo largo del tiempo sin fecha de finalización (ej. *Finanzas*, *Salud*, *Marketing*).
3. **Resources (Recursos)**: Temas o materias de interés e investigación activa en el presente (ej. *Inteligencia Artificial*, *Productividad*, *Programación*).
4. **Archives (Archivos)**: Elementos inactivos procedentes de las tres categorías anteriores conservados para consulta futura.

El desarrollo del método está sintetizado en [[PARA]].

---

## El Patrón LLM Wiki (Arquitectura de Karpathy)

En lugar de realizar búsquedas tradicionales tipo RAG (donde la IA relee documentos brutos y redescubre el conocimiento desde cero en cada consulta), este repositorio implementa la **arquitectura de 3 capas propuesta por Andrej Karpathy** para construir una wiki acumulativa y persistente:

```text
┌───────────────────────────────────────────────────────────┐
│  Capa 1: Raw Sources (Fuentes Brutas)                     │
│  Documentos inmutables (PDFs, Markdown, notas humanas)    │
└─────────────────────────────┬─────────────────────────────┘
                              │ Ingestión / Lectura
┌─────────────────────────────▼─────────────────────────────┐
│  Capa 2: The Wiki (Capa de Síntesis del LLM)              │
│  Conceptos [[enlazados]], _index.md y _log.md             │
└─────────────────────────────▲─────────────────────────────┘
                              │ Reglas y flujos
┌─────────────────────────────┴─────────────────────────────┐
│  Capa 3: The Schema (Configuración del Modelo)            │
│  Archivo AGENTS.md / README.md con instrucciones del LLM  │
└─────────────────────────────▲─────────────────────────────┘
```

- **Raw Sources (Fuentes Brutas)**: Colección inmutable de documentos primarios. El modelo lee de aquí pero nunca los modifica.
- **The Wiki (La Wiki)**: Carpeta de archivos Markdown generada y mantenida por la IA (síntesis, páginas de conceptos, relaciones cruzadas, `_index.md` como mapa de navegación y `_log.md` como registro cronológico).
- **The Schema (El Esquema)**: Archivo de instrucciones (`AGENTS.md`, `README.md` o `conventions.md`) que establece las pautas de síntesis, formato y rigor de citas para el modelo.

El patrón completo está sintetizado en [[Patrón LLM Wiki]], y el encastre de ambos métodos en esta bóveda en [[Arquitectura Mi-Engrama]].

---

## Estructura de Carpetas

```text
Mi-Engrama/
├── AGENTS.md                    ← Esquema para el agente de IA (capa 3)
├── README.md                    ← Este documento: reglas de la bóveda
├── 00-Inbox/                    ← Bandeja de entrada: todo entra aquí primero
├── 01-Proyectos/                ← Esfuerzos con objetivo y fecha de cierre
├── 02-Áreas/                    ← Responsabilidades continuas, sin fecha de fin
├── 03-Recursos/                 ← Temas de estudio e investigación activa
│   └── [Tema]/
│       ├── [fuente].md          ← Capa 1: fuentes crudas (inmutables)
│       └── Síntesis/            ← Capa 2: wiki mantenida por la IA
│           ├── _index.md        ← Catálogo de páginas del tema
│           ├── _log.md          ← Registro cronológico de operaciones
│           └── [página].md      ← Páginas de síntesis y conceptos
└── 04-Archivos/                 ← Elementos inactivos de las tres anteriores
    ├── 01-Proyectos/
    ├── 02-Áreas/
    └── 03-Recursos/
        └── [Tema]/
```

El prefijo numérico fija el orden en el explorador de archivos y lo mantiene igual entre sistemas operativos.

---

## Reglas de la bóveda

### 1. Las tres capas y quién escribe en cada una

| Capa | Dónde vive | Quién escribe | ¿Se modifica? |
|---|---|---|---|
| **Fuentes** | `03-Recursos/[Tema]/` | El humano (Web Clipper, copiar y pegar) | No. Son inmutables |
| **Síntesis** | `03-Recursos/[Tema]/Síntesis/` | La IA (o el humano a mano) | Sí. Se reescriben y se cruzan |
| **Esquema** | `AGENTS.md`, `README.md` | Humano e IA, juntos | Sí, versionado en git |

La regla que sostiene todo: **la IA nunca edita una fuente y nunca deja de actualizar la síntesis.**

### 2. Nomenclatura

| Qué | Regla | Ejemplo |
|---|---|---|
| Carpetas raíz | Prefijo numérico de dos dígitos | `03-Recursos/` |
| Carpeta de tema | Nombre del tema, capitalizado, singular | `Productividad/` |
| Nota | Título legible, con espacios y tildes | `Método PARA.md` |
| Índice y log | Guion bajo, para que ordenen primero | `_index.md`, `_log.md` |

Sin numeración en notas, sin `_` ni `-` como separadores de palabras, sin fechas en el nombre. El orden lo dan los enlaces y el índice, no el título.

**Regla de oro: el título de una nota es único en toda la bóveda.** Obsidian resuelve `[[enlace]]` por nombre de archivo; dos notas con el mismo título generan enlaces ambiguos. Si una fuente y su síntesis tratan el mismo tema, la página de síntesis lleva el nombre del **concepto**, no el del archivo original.

### 3. Qué va en cada carpeta

La única pregunta que decide: **¿qué tan accionable es esto hoy?**

| Situación | Destino |
|---|---|
| Esfuerzo con objetivo y fecha de cierre | `01-Proyectos/` |
| Responsabilidad que nunca termina | `02-Áreas/` |
| Tema que se está estudiando | `03-Recursos/` |
| Todavía no se sabe | `00-Inbox/` |
| Dejó de estar activo | `04-Archivos/` |

Si no se puede escribir **cuándo termina**, es un área. Si se puede, es un proyecto.

`00-Inbox/` es una bandeja, no un destino. Una nota que lleva más de una semana ahí se clasifica o se archiva.

### 4. Frontmatter

Las fuentes entran con el frontmatter que genera el Web Clipper (`title`, `source`, `author`, `published`, `created`, `tags`). Se **normaliza una sola vez, al ingerir**, y desde ese momento no se vuelve a tocar.

Normalización mínima:

- `author` va como texto plano. El clipper a veces escribe un wikilink con el nombre (`[[Tiago Forte]]`) y, cuando no encuentra un nombre visible, un ID numérico de cuenta (`[[262588213843476]]`). En ambos casos el enlace apunta a una nota que no existe y ensucia el grafo.
- No se agregan campos nuevos ni se reescribe el contenido del clipping.

Normalizar no es editar el conocimiento: es corregir la metadata para que el grafo no tenga nodos fantasma.

Las páginas de síntesis usan este formato:

```yaml
---
tipo: sintesis          # sintesis | indice | log | area | proyecto
tema: Productividad
estado: vigente         # vigente | revisar | obsoleto
fuentes:
  - "[[Método PARA]]"
actualizado: 2026-11-02
---
```

`estado: revisar` marca la deuda de verificación: una afirmación que una fuente nueva contradijo, o una página que quedó desactualizada. Es la señal que consume el chequeo de salud.

### 5. Enlaces

- Toda página de síntesis se alcanza desde `_index.md`. Una página sin enlaces entrantes es una huérfana: es un error, no un detalle.
- Toda página de síntesis enlaza **hacia atrás a la fuente** que la originó.
- Las páginas de `Síntesis/` **no enlazan a proyectos ni a áreas**. Deben poder archivarse junto con el tema sin dejar enlaces rotos. La dirección es unidireccional: proyectos y áreas enlazan hacia la wiki.
- No se dejan enlaces `[[a notas que no existen]]` al terminar una ingesta.

### 6. Flujo de ingesta

1. La fuente entra a `00-Inbox/`.
2. Se clasifica con la pregunta de accionabilidad, se normaliza el frontmatter del clipper (ver §4) y se mueve a `03-Recursos/[Tema]/`.
3. La IA la lee y discute los puntos clave con el humano.
4. Se crean o actualizan páginas en `Síntesis/`. Una fuente puede tocar varias páginas.
5. Se actualiza `_index.md`.
6. Se agrega la entrada en `_log.md`.
7. Se verifican los enlaces: sin huérfanas, sin rotos.

### 7. Formato de `_index.md` y `_log.md`

**`_index.md` es de contenido.** Catálogo de todo lo que existe en la wiki del tema: una fila por página con enlace y una línea que explique qué responde. Se lee **primero** ante cualquier pregunta y desde ahí se baja a las páginas. Escala bien hasta unas cien fuentes; con más, hace falta un buscador aparte.

**`_log.md` es cronológico y de solo agregar.** Qué pasó y cuándo. Cada entrada empieza con un prefijo fijo para poder filtrarlo desde la terminal:

```text
## [2026-11-02] ingesta | Método PARA
```

```bash
grep "^## \[" _log.md | tail -5
```

Tipos de entrada: `ingesta`, `consulta`, `lint`, `esquema`.

### 8. Consulta y mantenimiento

**Consulta.** Se lee `_index.md`, se bajan las páginas relevantes y se responde con citas a la fuente. Una respuesta valiosa no se pierde en el chat: se archiva como página nueva de la wiki. Las exploraciones también acumulan.

**Lint** (una vez por mes). Contradicciones entre páginas, afirmaciones que una fuente nueva dejó obsoletas, huérfanas sin enlaces entrantes, conceptos mencionados sin página propia, enlaces rotos, y páginas con `estado: revisar`.

### 9. Archivado

Se mueve la carpeta completa, nunca notas sueltas:

```text
03-Recursos/[Tema]/  →  04-Archivos/03-Recursos/[Tema]/
```

La unidad de archivado es la unidad de PARA. Si el tema vuelve, se mueve de vuelta con su historial y sus enlaces intactos.

### 10. Nota de proyecto (plantilla)

Toda nota en `01-Proyectos/` responde:

1. **Motivo**: por qué existe el proyecto.
2. **Hábito**: qué hábito busca instalar y por qué vale la pena.
3. **Ventajas y desventajas** de hacerlo a mano y de hacerlo con IA.
4. **Criterio de cierre**: cómo se sabe que está terminado.

Una nota de proyecto que no puede responder el punto 4 todavía es un área.

---

## ¿Por qué esta estructura optimiza la productividad?

- **Flexibilidad (con o sin IA)**:
  - **Sin IA**: Si prefieres no usar modelos de lenguaje, la bóveda funciona como un sistema **PARA** tradicional en Obsidian. Al colocar las lecturas primarias (PDFs, notas brutas) en la raíz del `[Tema]` y reservar `Síntesis/` para las notas procesadas o resúmenes, mantienes el material de consulta bien delimitado del conocimiento refinado sin saturar la navegación visual ni agregar clics innecesarios.
  - **Con IA**: Al activar un agente, la productividad se multiplica. El trabajo tedioso de "contabilidad digital" (crear notas de conceptos, actualizar enlaces bidireccionales `[[...]]`, mantener el `_index.md` y redactar resúmenes) se delega por completo en el modelo. El rol humano se enfoca en aportar buenas fuentes en la raíz del tema y realizar las preguntas adecuadas.

- **Archivado atómico**: Si un tema o proyecto deja de ser relevante, basta con trasladar la carpeta correspondiente (`01-Proyectos/[Proyecto]`, `02-Áreas/[Área]` o `03-Recursos/[Tema]`) a su subcarpeta equivalente dentro de `04-Archivos/` en un solo paso y sin dejar archivos huérfanos.

---

## Empezar a usar esta plantilla

- [ ] Clonar el repo y abrirlo como bóveda en Obsidian.
- [ ] Revisar que `AGENTS.md` describa la misma estructura que este `README.md`.
- [ ] Vaciar las notas de ejemplo de `01-Proyectos/`, `02-Áreas/` y `03-Recursos/`, o adaptarlas.
- [ ] Colocar la primera fuente en `03-Recursos/[Tema]/`.
- [ ] Ejecutar una ingesta completa y verificar que `_index.md` y `_log.md` quedaron actualizados.
- [ ] Agendar el lint mensual.
