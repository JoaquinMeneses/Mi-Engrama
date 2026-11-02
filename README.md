# Mi-Engrama

Bóveda de Obsidian para construir un segundo cerebro: una wiki personal que **acumula** conocimiento en lugar de re-descubrirlo en cada consulta.

Combina dos ideas. El método **PARA** de Tiago Forte decide dónde vive cada cosa. El patrón **LLM Wiki** de Andrej Karpathy delega en un agente la contabilidad de mantenerla viva. El resultado es una red de notas enlazadas que crece con cada fuente que agregas.

Funciona con o sin IA. Sin agente es un sistema PARA normal, que vos mantenés a mano. Con agente, la parte tediosa la hace él.

> **Las reglas operativas viven en [[AGENTS]], que es el contrato normativo.** Este documento explica el criterio: qué es esto, por qué está armado así y cómo se usa. Si los dos se contradicen, gana `AGENTS.md`.

### El nombre

En neurociencia, un **engrama** es la traza o huella biológica que deja un recuerdo en el cerebro. **Mi-Engrama** traslada ese concepto al ámbito digital: una red viva de notas interconectadas mediante enlaces bidireccionales donde cada nueva fuente de información fortalece y expande tu mapa de conocimiento.

---

## El problema que resuelve

No es falta de información. Es falta de **fuente**.

Leer algo, entenderlo, y a los meses volver a buscar lo mismo porque nada quedó guardado en un lugar recuperable. El conocimiento vive en la cabeza hasta que se diluye: sin respaldo, sin enlace, sin forma de mostrárselo a nadie.

La historia completa de por qué existe este repositorio está en [[Construir mi segundo cerebro]].

---

## Las dos ideas

### El Método PARA (Tiago Forte)

La estructura raíz de la bóveda sigue el método **PARA** de Tiago Forte, diseñado para organizar la información según su **nivel de accionabilidad** en cuatro categorías principales:

1. **Projects (Proyectos)**: Esfuerzos a corto plazo con un objetivo concreto y una fecha límite definida (ej. *Rediseñar sitio web*, *Comprar computadora*).
2. **Areas (Áreas)**: Responsabilidades continuas que requieren mantenimiento constante a lo largo del tiempo sin fecha de finalización (ej. *Finanzas*, *Salud*, *Marketing*).
3. **Resources (Recursos)**: Temas o materias de interés e investigación activa en el presente (ej. *Inteligencia Artificial*, *Productividad*, *Programación*).
4. **Archives (Archivos)**: Elementos inactivos procedentes de las tres categorías anteriores conservados para consulta futura.

El desarrollo del método está sintetizado en [[PARA]].

### El Patrón LLM Wiki (Arquitectura de Karpathy)

En lugar de búsquedas tradicionales tipo RAG (donde la IA relee documentos brutos y redescubre el conocimiento desde cero en cada consulta), este repositorio implementa la **arquitectura de 3 capas propuesta por Andrej Karpathy** para construir una wiki acumulativa y persistente:

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
│  Archivo AGENTS.md con instrucciones del agente           │
└─────────────────────────────▲─────────────────────────────┘
```

- **Raw Sources (Fuentes Brutas)**: Colección inmutable de documentos primarios. El modelo lee de aquí pero nunca los modifica.
- **The Wiki (La Wiki)**: Carpeta de archivos Markdown generada y mantenida por la IA (síntesis, páginas de conceptos, relaciones cruzadas, `_index.md` como mapa de navegación y `_log.md` como registro cronológico).
- **The Schema (El Esquema)**: Archivo de instrucciones (`AGENTS.md`) que establece las pautas de síntesis, formato y rigor de citas para el modelo.

El patrón completo está sintetizado en [[Patrón LLM Wiki]], y el encastre de ambos métodos en esta bóveda en [[Arquitectura Mi-Engrama]].

---

## Cómo está organizada la bóveda

```text
Mi-Engrama/
├── AGENTS.md                    ← Contrato para el agente de IA (capa 3)
├── README.md                    ← Este documento: el criterio
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

Los prefijos numéricos fijan el orden en el explorador de archivos y lo mantienen igual entre sistemas operativos e idiomas. `04-Archivos` espeja la numeración de las carpetas activas.

Por qué esta estructura funciona:

- **Flexibilidad, con o sin IA.**
  - **Sin IA**: la bóveda funciona como un sistema **PARA** tradicional en Obsidian. Al colocar las lecturas primarias (PDFs, notas brutas) en la raíz del `[Tema]` y reservar `Síntesis/` para las notas procesadas, el material de consulta queda delimitado del conocimiento refinado sin saturar la navegación ni agregar clics innecesarios.
  - **Con IA**: la productividad se multiplica. El trabajo tedioso de "contabilidad digital" (crear notas de conceptos, actualizar enlaces `[[...]]`, mantener el `_index.md`, redactar resúmenes) se delega por completo en el modelo. El rol humano se enfoca en aportar buenas fuentes y hacer las preguntas adecuadas.
- **Archivado atómico**: si un tema o proyecto deja de ser relevante, basta con trasladar la carpeta correspondiente a su equivalente dentro de `04-Archivos/`, en un solo paso y sin dejar archivos huérfanos.

---

## Cómo se usa

El ciclo completo, en lenguaje humano:

1. **Guardar la fuente.** Una nota bruta de cualquier tipo entra a `00-Inbox/`: un artículo, un PDF, una nota escrita a mano, la transcripción de un audio, un recorte. El formato no importa. Lo único que importa es que el original quede guardado y que puedas volver a él.
2. **Clasificar.** Pregúntate qué tan accionable es hoy. Si tiene fecha de cierre, es proyecto. Si es una responsabilidad que no termina, es área. Si es un tema que estás estudiando, es recurso.
3. **Ingerir.** Pide al agente que la procese, o hazlo a mano: la fuente se mueve al tema y se convierte en páginas de concepto dentro de `Síntesis/`.
4. **Consultar.** Cuando necesites algo, abre el `_index.md` del tema y sigue el enlace. No busques en carpetas: navega por conceptos.

Una fuente nueva no se guarda al costado: **modifica las páginas que ya existen**. Si dos artículos hablan del mismo tema desde ángulos distintos, el valor no está en los dos resúmenes, está en la página que los cruza.

---

## Qué incluye la plantilla

- **Un tema de ejemplo**, `Productividad`, con dos fuentes ingeridas y tres páginas de síntesis. Sirve para ver el resultado final antes de empezar con material propio.
- **Notas introductorias** en `01-Proyectos/` y `02-Áreas/`, marcadas `estado: ejemplo` en el frontmatter. Son de la plantilla, no de tu bóveda: borralas cuando ya no te sirvan. El agente te ofrece hacerlo.
- **`.gitkeep`** en las carpetas que pueden quedar vacías, para que git las versione igual.
- **`AGENTS.md`**: el contrato que convierte a un agente genérico en un mantenedor disciplinado de esta wiki.

---

## Requisitos e integración con Obsidian

**Obsidian** es una aplicación de gestión del conocimiento personal que opera sobre una bóveda (_vault_) de archivos en formato Markdown plano almacenados localmente en tu dispositivo. A diferencia de las herramientas tradicionales que guardan la información en bases de datos propietarias, Obsidian garantiza la portabilidad y propiedad absoluta de tus datos.

Esta arquitectura requiere y aprovecha las capacidades centrales de Obsidian:

- **Enlaces bidireccionales (`[[nota]]`)**: conectan conceptos e ideas entre la wiki procesada y tus proyectos o áreas.
- **Navegación y vista de grafo**: visualiza de forma gráfica la red interconectada de engramas de conocimiento que se van acumulando.
- **Almacenamiento local y abierto**: al ser archivos `.md` estándar, cualquier modelo de lenguaje o agente de IA puede leer y actualizar la estructura sin depender de exportaciones ni intermediarios.
- **Compatibilidad con plugins**: permite la integración con herramientas como `obsidian-git` para automatizar el versionado y la copia de respaldo en GitHub.

---

## Créditos

- **[PARA](https://fortelabs.com/blog/para/)** — Tiago Forte.
- **[LLM Wiki](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f)** — Andrej Karpathy.
- Licencia: ver `LICENSE`.
