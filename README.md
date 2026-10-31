
---

## **Requisitos e Integración con Obsidian**

**Obsidian** es una aplicación de gestión del conocimiento personal que opera sobre una bóveda (_vault_) de archivos en formato Markdown plano almacenados localmente en tu dispositivo. A diferencia de las herramientas tradicionales que guardan la información en bases de datos propietarias, Obsidian garantiza la portabilidad y propiedad absoluta de tus datos.

Esta arquitectura requiere y aprovecha las capacidades centrales de Obsidian:

- **Enlaces bidireccionales (`[[nota]]`)**: Permiten conectar conceptos e ideas de forma fluida entre la wiki procesada y tus proyectos o áreas.
- **Navegación y Vista de Grafo**: Permite visualizar de forma gráfica la red interconectada de engramas de conocimiento que se van acumulando.
- **Almacenamiento local y abierto**: Al ser archivos `.md` estándar, cualquier modelo de lenguaje o agente de IA puede leer y actualizar la estructura sin depender de exportaciones ni intermediarios.
- **Compatibilidad con plugins**: Permite la integración con herramientas como `obsidian-git` para automatizar el versionado y copia de respaldo en GitHub.

---

## ¿Qué es un "Engrama"?

En neurociencia, un **engrama** es la traza o huella biológica que deja un recuerdo en el cerebro. **Mi-Engrama** traslada este concepto al ámbito digital: una red viva de notas interconectadas mediante enlaces bidireccionales donde cada nueva fuente de información fortalece y expande tu mapa de conocimiento.

---

## El Método PARA (Tiago Forte)

La estructura raíz del vault sigue el método  **PARA** de Tiago Forte, diseñado para organizar la información según su **nivel de accionabilidad** en cuatro categorías principales:

1. **Projects (Proyectos)**: Esfuerzos a corto plazo con un objetivo concreto y una fecha límite definida (ej. *Rediseñar sitio web*, *Comprar computadora*).
2. **Areas (Áreas)**: Responsabilidades continuas que requieren mantenimiento constante a lo largo del tiempo sin fecha de finalización (ej. *Finanzas*, *Salud*, *Marketing*).
3. **Resources (Recursos)**: Temas o materias de interés e investigación activa en el presente (ej. *Inteligencia Artificial*, *Productividad*, *Programación*).
4. **Archives (Archivos)**: Elementos inactivos procedentes de las tres categorías anteriores conservados para consulta futura.

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
│  Conceptos [[enlazados]], index.md y log.md               │
└─────────────────────────────▲─────────────────────────────┘
                              │ Reglas y flujos
┌─────────────────────────────┴─────────────────────────────┐
│  Capa 3: The Schema (Configuración del Modelo)            │
│  Archivo CLAUDE.md / system.md con instrucciones del LLM  │
└─────────────────────────────▲─────────────────────────────┘
```

* **Raw Sources (Fuentes Brutas)**: Colección inmutable de documentos primarios. El modelo lee de aquí pero nunca los modifica.
* **The Wiki (La Wiki)**: Carpeta de archivos Markdown generada y mantenida por la IA (síntesis, páginas de conceptos, relaciones cruzadas, `index.md` como mapa de navegación y `log.md` como registro cronológico).
* **The Schema (El Esquema)**: Archivo de instrucciones (`CLAUDE.md`, `system.md` o `conventions.md`) que establece las pautas de síntesis, formato y rigor de citas para el modelo.

---
## Estructura de Carpetas y Productividad

A continuación se presenta el árbol completo de carpetas de la bóveda, integrando la estructura de **PARA** con el patrón de **LLM Wiki**:

```
Mi-Engrama/
├── AGENTS.md                   &lt;-- Esquema de reglas e instrucciones para el LLM
├── 1. Proyectos/               &lt;-- Proyectos activos con meta y fecha límite
├── 2. Áreas/                   &lt;-- Áreas de responsabilidad continua
├── 3. Recursos/                 &lt;-- Temas de interés e investigación activa
│   └── [Tema]/                 &lt;-- Estructura modular por tema que almacena Documentos brutos (notas humanas, PDFs)
│       └── Sintesis/           &lt;-- Capa Wiki de la IA (index.md, log.md, conceptos)
└── 4. Archivos/                &lt;-- Contenedor de elementos inactivos
    ├── Proyectos/              &lt;-- Proyectos completados o pausados
    ├── Áreas/                  &lt;-- Ámbitos de responsabilidad que ya no mantienes
    └── Recursos/              &lt;-- Recursos y temas que perdieron relevancia actual
        └── [Tema]/

```

---
### **¿Por qué esta estructura optimiza la productividad?**

- **Flexibilidad (Con o Sin IA)**:
    
    - **Sin IA**: Si prefieres no usar modelos de lenguaje, la bóveda funciona de forma limpia como un sistema **PARA** tradicional en Obsidian. Al colocar tus lecturas primarias (PDFs, notas brutas) en la raíz del `[Tema]` y reservar `Sintesis/` para tus propias notas procesadas o resúmenes, mantienes tu material de consulta bien delimitado del conocimiento refinado sin saturar la navegación visual ni agregar clicks innecesarios.
        
    - **Con IA (LLM Wiki)**: Al activar un agente de IA, la productividad se multiplica. El trabajo tedioso de "contabilidad digital" (crear notas de conceptos, actualizar enlaces bidireclonales `[[...]]`, mantener el `index.md` y redactar resúmenes) se delega por completo en el modelo. Tu rol se enfoca exclusivamente en aportar buenas fuentes en la raíz del tema y realizar las preguntas adecuadas.
        
- **Archivado Atómico**: Si un tema o proyecto deja de ser relevante, basta con trasladar la carpeta correspondiente (`1. Proyectos/[Proyecto]`, `2. Áreas/[Área]` o `3. Recursos/[Tema]`) a su subcarpeta equivalente dentro de `4. Archivos/` en un solo paso y sin dejar archivos huérfanos.