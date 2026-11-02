---
tipo: log
tema: Productividad
actualizado: 2026-11-02
---

# Log — Productividad

Registro cronológico, **solo agregar**. Nunca se reescribe una entrada anterior.

Formato fijo de encabezado: `## [YYYY-MM-DD] tipo | Título`
Tipos: `ingesta`, `consulta`, `lint`, `esquema`.

```bash
grep "^## \[" _log.md | tail -5   # últimas cinco operaciones del tema
```

---

## [2026-11-02] ingesta | Método PARA
- Fuente: [[Método PARA]] — Tiago Forte, *The PARA Method* (2023)
- Página creada: [[PARA]]
- Páginas actualizadas: —
- Notas: la distinción proyecto/área es el punto que el artículo desarrolla con más detalle; quedó como sección propia.

## [2026-11-02] ingesta | LLM Wiki
- Fuente: [[LLM Wiki]] — Andrej Karpathy, *llm-wiki*
- Página creada: [[Patrón LLM Wiki]]
- Páginas actualizadas: —
- Notas: el patrón se apoya sobre la organización por accionabilidad; de ese cruce sale la página de arquitectura.

## [2026-11-02] esquema | Inicialización de la capa de síntesis
- Se definió el formato de `_index.md` y `_log.md` y se documentaron las reglas en el `README.md`.
- Se creó [[Arquitectura Mi-Engrama]] como página de convergencia de las dos fuentes.
- Alcance: tema Productividad. Las notas de `01-Proyectos/`, `02-Áreas/` y el `AGENTS.md` quedan pendientes.
