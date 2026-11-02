---
tipo: sintesis
tema: Productividad
estado: ejemplo
fuentes:
  - "[[LLM Wiki]]"
actualizado: 2026-11-02
---
> Nota introductoria de la plantilla. Explica de dónde viene este repositorio y qué busca resolver. Si ya entendiste el sistema, puedes borrarla o reescribirla con tu propio motivo.
# Patrón LLM Wiki

Forma de construir una base de conocimiento personal con un LLM, propuesta por Andrej Karpathy. La idea central: en lugar de que el modelo recupere fragmentos en cada consulta, **mantiene una wiki persistente** que se acumula.

## RAG vs. wiki acumulativa

| | RAG | Wiki LLM |
|---|---|---|
| Qué hace el modelo | Recupera fragmentos y responde | Lee la fuente e **integra** lo que sabe |
| Conocimiento | Se re-descubre en cada pregunta | Se compila una vez y se mantiene |
| Al agregar una fuente | Se indexa para consulta futura | Se actualizan las páginas afectadas |
| Trabajo del humano | Subir archivos y preguntar | Curar fuentes y hacer buenas preguntas |

En RAG, una pregunta que exige sintetizar cinco documentos obliga a reencontrar los fragmentos cada vez. En la wiki, las referencias cruzadas ya están escritas y las contradicciones ya están marcadas. La diferencia se resume en una frase: **la wiki es un artefacto persistente que compone, no una búsqueda que se repite.**

## Las tres capas

| Capa | Qué es | Quién la escribe |
|---|---|---|
| **Fuentes crudas** | Documentos primarios: artículos, papers, imágenes | El humano. Inmutables |
| **Wiki** | Markdown generado: resúmenes, conceptos, comparaciones | El LLM |
| **Esquema** | Instrucciones sobre estructura, convenciones y flujos | Humano y LLM, juntos |

El esquema es la pieza que convierte al modelo en un **mantenedor disciplinado** en lugar de un chatbot genérico. Es también la pieza que envejece más rápido: si describe una estructura que ya no existe, el modelo escribe en el lugar equivocado.

## Operaciones

**Ingesta.** Llega una fuente; el modelo la lee, se discuten los puntos clave, escribe la página de resumen, actualiza el índice, toca las páginas de concepto afectadas y agrega una entrada al log. Una sola fuente puede tocar entre diez y quince páginas.

**Consulta.** Se buscan las páginas relevantes y se responde con citas. La respuesta valiosa se archiva como página nueva: las exploraciones también acumulan.

**Lint.** Chequeo periódico de contradicciones, afirmaciones que una fuente nueva superó, huérfanas, conceptos mencionados sin página propia y huecos que se podrían llenar con una búsqueda.

## Índice y log

Dos archivos con funciones distintas y complementarias:

- **`_index.md`** — orientado al contenido. Catálogo de todo lo que existe, con una línea por página. Se lee primero al responder y desde ahí se baja a las páginas. Funciona bien hasta unas cien fuentes; después hace falta un buscador.
- **`_log.md`** — cronológico y de solo agregar. Con un prefijo fijo por entrada se vuelve filtrable con herramientas comunes: `grep "^## \[" _log.md | tail -5` da las últimas cinco operaciones.

## Por qué funciona

La parte tediosa de mantener una wiki no es leer ni pensar: es la contabilidad. Actualizar referencias, sostener resúmenes, notar contradicciones, mantener consistencia entre decenas de páginas.

Los humanos abandonan wikis porque el costo de mantenimiento crece más rápido que el valor que entregan. Un LLM no se aburre, no olvida actualizar un enlace y puede tocar quince archivos en una pasada. **El costo de mantenimiento se acerca a cero, y por eso la wiki sigue viva.**

## Reparto de responsabilidades

| Humano | LLM |
|---|---|
| Curar fuentes | Resumir e integrar |
| Dirigir el análisis | Cruzar referencias |
| Hacer buenas preguntas | Mantener índices y enlaces |
| Interpretar y decidir | Contabilidad completa |

## Linaje

Conecta con el **Memex** de Vannevar Bush (1945): un archivo personal y curado, donde los senderos asociativos entre documentos valen tanto como los documentos. Lo que Bush no resolvía era **quién hace el mantenimiento**. Ese es exactamente el aporte del LLM.

## Fuente

- [[LLM Wiki]] — Andrej Karpathy, *llm-wiki* (gist). https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f
