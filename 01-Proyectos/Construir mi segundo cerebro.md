---
tipo: proyecto
estado: ejemplo
actualizado: 2026-11-02
---

# Construir mi segundo cerebro

> Nota introductoria de la plantilla. Explica de dónde viene este repositorio y qué busca resolver. Si ya entendiste el sistema, puedes borrarla o reescribirla con tu propio motivo.

## El problema que me trajo hasta acá

No era falta de información. Era falta de **fuente**.

Me pasaba esto: le decía a un amigo "hay un estudio que dice X". Tenía el estudio. Lo había leído. Pero no lo guardé, y en el momento de mostrarlo solo quedaba el conocimiento en mi cabeza, sin respaldo y sin forma de volver a encontrarlo.

El patrón se repetía en todo:

- Seguía usando papel para cosas que podían estar en digital.
- Lo digital vivía en la PC. Si estaba con el celular, no podía consultarlo ni anotarlo.
- Lo que aprendía en el trabajo, en el estudio o en el día a día se quedaba en la cabeza hasta diluirse.
- Cada tema arrancaba de cero: leía, entendía, y a los meses volvía a buscar exactamente lo mismo.

El problema no era la memoria. Era que no había un lugar donde las cosas **quedaran**.

## La idea

Soy programador, así que lo encaré como un problema de ingeniería: si el costo de mantener un sistema de conocimiento es mayor que el valor que entrega, el sistema se abandona. No es falta de disciplina, es diseño.

La pregunta correcta no era "¿cómo me organizo mejor?", sino "¿cómo hago que mantener esto cueste casi nada?".

Esa respuesta tiene dos partes:

1. **Una estructura de carpetas que no hay que pensar**: [[PARA]]. Cuatro categorías y una bandeja de entrada.
2. **Un agente que hace la contabilidad**: [[Patrón LLM Wiki]]. Resúmenes, enlaces cruzados, índices y registro.

El resultado es esta bóveda. Las notas no son archivos sueltos: son una red que crece con cada fuente que se agrega.

## El hábito

Lo que quiero instalar no es "tomar notas". Es **cerrar el ciclo**: cuando se aprende algo, la fuente queda guardada, la idea queda escrita y la nota queda enlazada.

Vale la pena por una razón concreta: convierte el conocimiento en algo **recuperable**. Una idea que no se puede volver a encontrar es una idea que va a tener que volver a aparecer.

## A mano o con IA

La bóveda funciona de las dos formas. Fue una decisión de diseño, no una concesión.

| | A mano | Con IA |
|---|---|---|
| **Quién escribe** | El humano | El agente, y el humano revisa |
| **Ventaja** | Control total. Se aprende al escribir. Cero dependencia | La contabilidad deja de costar tiempo |
| **Desventaja** | El mantenimiento crece más rápido que el valor | Puede inventar. Depende de un esquema bien escrito |
| **Cuándo conviene** | Pocas fuentes, tema que se quiere aprender a fondo | Muchas fuentes, muchos enlaces, tema que ya se conoce |

Sin IA, la carpeta `Síntesis/` la llena el humano. Con IA, la llena el agente y el humano se dedica a curar fuentes y hacer preguntas.

## Sobre la IA

Estuve en contra del uso de IA. Lo digo sin maquillaje: me parecía una forma de no hacer el trabajo.

Cambié de opinión con un argumento simple. Los contadores no desaparecieron cuando se inventó la calculadora. Los panaderos no desaparecieron con las máquinas de amasar. Los programadores no desaparecieron con los IDE.

Lo que cambió no fue el trabajo: cambió **qué parte del trabajo** hace cada uno. La IA no decide qué vale la pena guardar. No sabe qué te importa. No interpreta. Hace la parte que ningún humano quiere hacer: mantener actualizados los enlaces, los índices y los resúmenes.

Es una **herramienta**. Y como toda herramienta, el criterio sigue siendo humano.

## Qué no es esto

- No es una aplicación. Son archivos Markdown en una carpeta.
- No es un servicio. No hay cuenta, no hay suscripción, no hay servidor.
- No es propiedad de nadie más. El respaldo es propio: un repositorio git, donde cada uno decida.

## Por qué lo comparto

Quiero que mis amigos y conocidos tengan otra forma de ver el conocimiento que ya tienen. Que puedan tener su respaldo sin depender del correo o de un proveedor que puede cerrar, cobrar o cambiar las reglas.

Si alguien encuentra un método mejor, que lo use. Esto no es una doctrina: es una base, una puerta de entrada.

## Cómo empezar

1. Clonar el repositorio y abrirlo como bóveda en Obsidian.
2. Leer el `README.md` para entender el sistema, y el `AGENTS.md` si se va a trabajar con un agente.
3. Colocar la primera fuente en `00-Inbox/`.
4. Hacer la primera ingesta.
5. Borrar las notas de ejemplo (`estado: ejemplo`) cuando ya no sirvan.

## Criterio de cierre

Este proyecto termina cuando:

- [ ] La bóveda está documentada y `README.md` y `AGENTS.md` coinciden con la estructura real.
- [ ] La primera ingesta completa está hecha y verificada.
- [ ] El lint mensual está agendado.

Después de eso deja de ser un proyecto y pasa a ser un área: [[Segundo cerebro]].

## Enlaces

- Área que lo mantiene: [[Segundo cerebro]]
- Conceptos: [[PARA]] · [[Patrón LLM Wiki]] · [[Arquitectura Mi-Engrama]]
