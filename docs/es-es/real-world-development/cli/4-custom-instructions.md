---
title: "Lección 4: Guiar a Copilot con instrucciones personalizadas"
description: "Explora las instrucciones del repositorio, añade un estándar de documentación y aplícalo al código de filtrado."
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

El contexto es esencial cuando se trabaja con inteligencia artificial generativa. Si una tarea debe realizarse de una manera determinada, asegúrate de que Copilot disponga de esas directrices. Los [archivos de instrucciones][instruction-files] describen no solo qué código quieres, sino también cómo debe estructurarse. Ahora que has implementado el filtrado, explorarás las instrucciones utilizadas por Copilot, añadirás un estándar de documentación y lo aplicarás al código.

En esta lección:

- Explorarás cómo llegan al agente las instrucciones del repositorio y los archivos asociados a rutas.
- Actualizarás el archivo de instrucciones para que se respeten los estándares de código.
- Comprobarás el efecto de los archivos de instrucciones en el código.

## Escenario

Tailspin Toys tiene directrices y requisitos para sus prácticas de desarrollo:

- Los comentarios deben explicar la intención y las decisiones que no resulten obvias, no repetir el código.
- Las funciones exportadas de `db/` y `src/lib/` deben documentar su propósito, parámetros y valores devueltos con TypeScript Documentation (TSDoc) o JavaScript Documentation (JSDoc), incluido el argumento `db` inyectable cuando corresponda.
- Los componentes Astro reutilizables deben documentar sus contratos `Props`, y los comentarios deben seguir actualizados cuando cambie el código relacionado.
- Deben respetarse las directrices existentes de formato y lint.

Explorarás los archivos de instrucciones para que Copilot disponga de la información necesaria para cumplir estas prácticas.

## Archivos de instrucciones

Las instrucciones personalizadas proporcionan contexto y preferencias a Copilot para que pueda ofrecer sugerencias más pertinentes y código que se ajuste a tus requisitos. Puedes especificar convenciones de código, bibliotecas y tipos de comentarios, y crear instrucciones para todo el repositorio o para tipos de archivo y tareas concretos.

Hay dos tipos de archivos de instrucciones:

- `.github/copilot-instructions.md` es un único archivo que se envía a Copilot en todas las solicitudes del repositorio. Debe incluir información general pertinente para la mayoría de las solicitudes.
- Los archivos `.github/instructions/*.instructions.md` definen directrices para lenguajes, tipos de archivo o tareas concretos.

> [!NOTE]
> Los demás formatos de instrucciones y su compatibilidad varían según el entorno. Consulta la [referencia de compatibilidad de instrucciones personalizadas][custom-instructions-support] antes de depender de un formato concreto.

## Explora los archivos de instrucciones personalizadas del proyecto

El proyecto de inicio ya incluye varios archivos de instrucciones. Antes de hacer cambios, explóralos para ver cómo influyen en el trabajo de Copilot.

1. Vuelve al codespace.
2. En el editor de Codespaces, no en el terminal, abre `.github/copilot-instructions.md`.
3. Revisa la descripción breve del proyecto y sus directrices de código. Se aplican a todas las interacciones con Copilot en este repositorio.
4. Abre la carpeta `.github/instructions` y explora sus archivos. Encontrarás instrucciones para Astro, la capa de datos Drizzle, las pruebas y otros temas.
5. Abre `.github/instructions/unit-tests.instructions.md`. El campo `applyTo` de la parte superior define un patrón global que determina a qué archivos se aplican las instrucciones.
6. Abre `.github/instructions/drizzle.instructions.md` y revisa los enlaces a otros archivos de instrucciones y a archivos del proyecto. Así puedes dividir instrucciones extensas en archivos más pequeños y reutilizables y proporcionar a Copilot ejemplos que seguir.

## Actualiza las instrucciones del equipo

Los archivos existentes son un buen punto de partida, pero todavía falta una regla. Modifica `copilot-instructions.md` para pedir que el TypeScript nuevo incluya comentarios TSDoc.

1. En `.github/copilot-instructions.md`, busca la sección **Code formatting guidance**, que debería estar cerca de la línea 35.
2. Añade como último elemento de la lista:

   ```markdown
   - All new TypeScript should contain TSDocs comments for documentation purposes.
   ```

El archivo se guardará automáticamente.

## Aplica las directrices actualizadas

Copilot CLI carga las instrucciones del repositorio al iniciar una conversación. Después de guardar las instrucciones, cerrarás y reanudarás la conversación de filtrado para que Copilot cargue las nuevas directrices sin perder el contexto de la funcionalidad.

1. Si la conversación de filtrado sigue abierta, introduce `/exit` para cerrarla. Copilot CLI guarda las conversaciones automáticamente.
2. Desde la raíz del repositorio y en la rama `game-filters-cli`, reanuda la conversación guardada:

   ```bash
   copilot --resume
   ```

   Si se te solicita, selecciona la conversación de filtrado y confirma que está seleccionada la rama `game-filters-cli`.
3. Pide a Copilot que aplique las directrices actualizadas:

   ```plaintext
   Acabamos de actualizar las instrucciones y las directrices de código. ¿Puedes actualizar el código que has generado para que las cumpla?
   ```

4. Introduce `/diff` y revisa los archivos TypeScript modificados. Comprueba que los comentarios TSDoc nuevos describan el código con precisión.

## Resumen y pasos siguientes

Has explorado cómo Copilot CLI utiliza el contexto de los archivos de instrucciones y has aplicado un estándar nuevo a la funcionalidad. En concreto:

- Has explorado cómo llegan al agente las instrucciones del repositorio y los archivos asociados a rutas.
- Has actualizado el archivo de instrucciones para exigir que se respeten los estándares de código.
- Has comprobado el efecto de los archivos de instrucciones en el código.

A continuación, [personalizarás y ejecutarás la habilidad reutilizable quality-checks][next-lesson] para que el lint y las pruebas se ejecuten de forma coherente.

## Recursos

- [Añadir instrucciones personalizadas a Copilot CLI][instruction-files]
- [Compatibilidad con instrucciones personalizadas][custom-instructions-support]
- [Prácticas recomendadas para crear instrucciones personalizadas][instructions-best-practices]
- [Awesome Copilot: archivos de instrucciones y otros recursos][awesome-copilot]

[instruction-files]: https://docs.github.com/copilot/how-tos/copilot-cli/customize-copilot/add-custom-instructions
[instructions-best-practices]: https://docs.github.com/copilot/concepts/prompting/response-customization#writing-effective-custom-instructions
[awesome-copilot]: https://awesome-copilot.github.com/
[custom-instructions-support]: https://docs.github.com/copilot/reference/custom-instructions-support
[previous-lesson]: ../3-agent-modes/
[next-lesson]: ../5-agent-skills/
