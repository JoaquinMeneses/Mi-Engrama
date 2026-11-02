---
tipo: sintesis
tema: Productividad
estado: ejemplo
fuentes:
  - "[[Método PARA]]"
  - "[[LLM Wiki]]"
actualizado: 2026-11-02
---
> Nota introductoria de la plantilla. Explica de dónde viene este repositorio y qué busca resolver. Si ya entendiste el sistema, puedes borrarla o reescribirla con tu propio motivo.
# Arquitectura Mi-Engrama

Cómo se combinan [[PARA]] y el [[Patrón LLM Wiki]] en esta bóveda. PARA responde **dónde** vive cada cosa; el patrón LLM Wiki responde **quién** la mantiene y **cómo** crece.

## El encastre

| Pregunta | La responde | Implementada en |
|---|---|---|
| ¿Dónde guardo esto? | PARA | `00-Inbox` → `01`..`04` |
| ¿Quién escribe la síntesis? | LLM Wiki | El agente, sobre `Síntesis/` |
| ¿Cómo sé qué existe? | LLM Wiki | `_index.md` |
| ¿Qué pasó y cuándo? | LLM Wiki | `_log.md` |
| ¿Cómo debe comportarse el agente? | Ambos | `AGENTS.md` y `README.md` |

Ninguno de los dos alcanza solo:

- **PARA sin agente** es un sistema de carpetas que hay que mantener a mano. Funciona, y se abandona.
- **LLM Wiki sin PARA** produce una wiki sin jerarquía de accionabilidad: todo pesa lo mismo y nada está donde se necesita.

## El recorrido de una fuente

```text
00-Inbox/   →   03-Recursos/[Tema]/   →   Síntesis/   →   _index + _log
  llega            fuente inmutable         wiki          navegación
```

1. La fuente entra a `00-Inbox/`.
2. Se clasifica con la pregunta de accionabilidad y se mueve a `03-Recursos/[Tema]/`.
3. El agente la lee y la discute con el humano.
4. Se crean o actualizan páginas en `Síntesis/`.
5. Se actualiza `_index.md`.
6. Se agrega la entrada en `_log.md`.
7. Se verifican los enlaces.

El detalle operativo está en el `README.md` de la bóveda.

## Propiedades que se buscan

| Propiedad | De dónde viene | Cómo se verifica |
|---|---|---|
| Reutilización | PARA | Un mismo concepto sirve a varios proyectos sin copiarse |
| Acumulación | LLM Wiki | Una fuente nueva modifica páginas viejas |
| Navegabilidad | Ambos | Se llega a cualquier página en dos saltos desde el índice |
| Portabilidad | Obsidian | Todo es Markdown plano versionado en git |

## Límites y riesgos

- **El esquema envejece.** Si `AGENTS.md` o el `README.md` describen una estructura que el filesystem ya no tiene, el agente escribe en el lugar equivocado y la bóveda se duplica. El esquema es código: se versiona y se actualiza.
- **La síntesis puede inventar.** El agente redacta prosa convincente. Cada afirmación de una página de síntesis debe poder rastrearse hasta su fuente.
- **Acumular no es comprender.** Una wiki que crece sin que el humano la lea es un cementerio ordenado. Leer el índice y las páginas nuevas es parte del método, no un extra.
- **El costo cero no es gratis.** Baja el costo de mantener y sube el de revisar. El lint mensual existe por eso.
- **Un título repetido rompe los enlaces.** Obsidian resuelve `[[...]]` por nombre de archivo; dos notas con el mismo título hacen ambiguo el enlace. De ahí la regla de títulos únicos.

## Fuentes

- [[Método PARA]]
- [[LLM Wiki]]
