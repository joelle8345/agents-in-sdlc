---
title: "Ejercicio 1: Instrucciones personalizadas (VS Code)"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

[← Lección anterior: Requisitos previos][previous-lesson] · [Siguiente lección: Modo agente →][next-lesson]

El contexto es esencial cuando se trabaja con inteligencia artificial generativa. Si una tarea debe realizarse de una manera determinada o Copilot necesita información de contexto, asegúrate de que pueda acceder a ella. Los [archivos de instrucciones][instruction-files] proporcionan directrices sobre la generación de código.

En este ejercicio:

- Explorarás cómo llegan a Copilot el contexto específico del proyecto, las directrices de código y los estándares de documentación mediante instrucciones personalizadas del repositorio y archivos asociados a rutas.
- Generarás la primera parte de los datos del filtrado (un método auxiliar para editoriales) con las instrucciones actuales.
- Añadirás un estándar general al repositorio en `.github/copilot-instructions.md`.
- Repetirás el mismo mensaje y observarás cómo el código generado aplica el nuevo estándar.
- Confirmarás la actualización de instrucciones y la parte del filtrado en `main` para que Copilot pueda utilizar las nuevas directrices en el siguiente ejercicio.

> [!CAUTION]
> El código generado puede no cumplir algunos de los estándares definidos. Copilot no es determinista. El objetivo de este ejercicio es observar la tendencia después de actualizar las instrucciones, no obtener exactamente el mismo resultado carácter por carácter.

## Archivos de instrucciones

### Escenario

Tailspin Toys tiene directrices y requisitos para sus prácticas de desarrollo:

- La capa de datos siempre debe tener pruebas unitarias.
- La interfaz de usuario debe utilizar el modo oscuro y tener un aspecto moderno.
- El código debe incluir documentación en forma de comentarios TSDoc.
- Al principio de cada archivo debe haber un bloque de comentarios que describa su propósito.

Explorarás los archivos de instrucciones para que Copilot disponga del contexto necesario y realice las tareas de acuerdo con estas prácticas.

### Instrucciones personalizadas

Las instrucciones personalizadas proporcionan contexto y preferencias a Copilot para que pueda ofrecer sugerencias más pertinentes y código que se ajuste a tus requisitos. Puedes especificar convenciones de programación, bibliotecas y tipos de comentarios, y crear instrucciones para todo el repositorio o para tipos de archivo concretos.

Hay dos tipos de archivos de instrucciones:

- `.github/copilot-instructions.md` es un único archivo que se envía a Copilot en todas las solicitudes del repositorio. Debe contener información general, como la pila tecnológica, una descripción del proyecto, las prácticas recomendadas y otras directrices aplicables a la mayoría de las solicitudes de chat o CLI.
- Los archivos `.github/instructions/*.instructions.md` permiten definir directrices para tareas o tipos de archivo concretos, como TypeScript, Astro, componentes de interfaz o pruebas unitarias.

> [!NOTE]
> En un IDE, los archivos de instrucciones solo se utilizan para generar código en Copilot Chat, no para completar código ni para sugerencias de edición siguiente.
>
> Copilot Chat, Copilot CLI y el agente en la nube de Copilot utilizan tanto las instrucciones del repositorio como los archivos `*.instructions.md` que incluyen metadatos `applyTo`.
>
> Copilot también admite [archivos de instrucciones de otros estándares][custom-instructions-support], como AGENTS.md y CLAUDE.md.

### Prácticas recomendadas para gestionar archivos de instrucciones

El proyecto de ejemplo muestra un enfoque representativo para crear archivos de instrucciones. En general:

- Mantén `copilot-instructions.md` centrado en directrices generales del proyecto, como su descripción, su estructura y los estándares de código globales.
- Utiliza archivos `*.instructions.md` para tipos de archivo concretos, como pruebas unitarias, componentes Astro y la capa de datos, o para tareas específicas.
- Escribe directrices claras en lenguaje natural e incluye ejemplos de código correcto e incorrecto.

No existe una única manera de crear archivos de instrucciones ni de utilizar la IA. La experimentación te ayudará a encontrar el enfoque adecuado para tu proyecto.

> [!TIP]
> Todos los proyectos que utilizan GitHub Copilot deberían tener un conjunto sólido de archivos de instrucciones. Al revisar los de este proyecto, encontrarás archivos para tareas como [actualizar la interfaz de usuario][ui-instructions] y trabajar con [Astro][astro-instructions].
>
> Copilot también puede ayudarte a generar archivos de instrucciones. Cada superficie ofrece esta opción de una forma distinta (por ejemplo, **Configure Chat → Generate Agent Instructions** en VS Code o `/init` en Copilot CLI). La lección correspondiente explicará cómo utilizarla cuando sea pertinente.
>
> Para encontrar plantillas o un punto de partida, consulta [awesome-copilot][awesome-copilot], un repositorio con archivos de instrucciones, agentes personalizados y otros recursos.

[ui-instructions]: https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/ui.instructions.md
[astro-instructions]: https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/astro.instructions.md
[awesome-copilot]: https://github.com/github/awesome-copilot
[custom-instructions-support]: https://docs.github.com/copilot/reference/custom-instructions-support

## Explora los archivos de instrucciones personalizadas del proyecto

Lee los archivos de instrucciones incluidos en este repositorio antes de hacer cambios: hay un archivo principal `copilot-instructions.md` y varios archivos `*.instructions.md` para distintas tareas.

1. Abre `.github/copilot-instructions.md`.
2. Revisa la descripción breve del proyecto y secciones como **Agent notes**, **Code standards**, **Scripts** y **Repository Structure**. En **Code standards**, fíjate también en las directrices anidadas de **GitHub Actions Workflows**. Se aplican a todas las interacciones con Copilot.
3. Abre la carpeta `.github/instructions` y explórala. Encontrarás instrucciones para Astro, la capa de datos Drizzle, las pruebas y otros temas.
4. Abre `.github/instructions/unit-tests.instructions.md`. El campo `applyTo` de la parte superior define un patrón global relativo a la raíz del repositorio. En este caso, coincide con los archivos de prueba TypeScript que cumplen `**/*.test.ts`.
5. Revisa las instrucciones específicas para crear pruebas unitarias en este proyecto.
6. Abre `.github/instructions/drizzle.instructions.md` y ve al final. Observa los enlaces a otros archivos de instrucciones, como `unit-tests.instructions.md`, y a archivos existentes del proyecto. Así puedes dividir instrucciones extensas en archivos más pequeños y reutilizables y proporcionar ejemplos a Copilot. Las rutas de esos enlaces son relativas al archivo de instrucciones, no a la raíz del repositorio.

> [!NOTE]
> La sección **Code formatting requirements** de `copilot-instructions.md` describe los estándares de código del proyecto, pero todavía no exige documentación en el código. En los pasos siguientes, añadirás reglas para los comentarios TSDoc y los comentarios al principio de cada archivo.

## Crea una rama para los cambios

Crearás una rama para aislar estos cambios.

1. Vuelve al codespace del ejercicio anterior.
2. Abre un terminal nuevo pulsando <kbd>Control</kbd>+<kbd>`</kbd> (Mac) o <kbd>Ctrl</kbd>+<kbd>`</kbd> (Windows/Linux).
3. Crea una rama y cámbiate a ella:

   ```bash
   git checkout -b custom-instructions
   ```

## Utiliza Copilot Chat antes de actualizar las instrucciones

> [!TIP]
> **Abre Copilot Chat**
>
> Antes de empezar, vuelve al codespace, abre el panel Copilot Chat y selecciona **New Chat** para iniciar una conversación nueva. La selección de modo y modelo varía según el ejercicio; cada paso indicará cuándo cambiarla.

Para observar el efecto de las instrucciones personalizadas, primero enviarás un mensaje con el archivo de instrucciones actual. Después, lo actualizarás y enviarás el mismo mensaje para comparar los resultados.

1. Cierra las pestañas del editor que estén abiertas de ejercicios anteriores para que Copilot reciba solo el contexto necesario.
2. Abre `src/lib/publishers.ts` para indicar a Copilot dónde debe ubicarse el método auxiliar.
3. En la vista Chat, selecciona **Agent** en el selector de agentes para que Copilot pueda aplicar cambios a los archivos.

   ![Selector del agente en la vista Chat](../../../_images/shared-chat-mode-selector.png)

4. Envía este mensaje:

   ```plaintext
   Crea o actualiza src/lib/publishers.ts con un método de acceso a datos que devuelva una lista de todas las editoriales, con el nombre y el id de cada una. Aplica los cambios a los archivos.
   ```

5. Copilot explorará el proyecto y aplicará los cambios de código. A menudo, modificará tanto el archivo del método auxiliar como sus pruebas.
6. Observa que el método propuesto es una función tipada que recibe un cliente `db` como primer argumento y devuelve una matriz tipada de editoriales. Esto se debe a las convenciones de la capa de datos de `.github/instructions/drizzle.instructions.md`, que se aplica a `src/lib/*.ts`.
7. Comprueba que el código propuesto **no incluye** comentarios TSDoc ni un comentario al principio del archivo.

> [!CAUTION]
> Como Copilot ofrece resultados probabilísticos, puede que añada comentarios de documentación aunque no se los hayas pedido. No pasa nada: el objetivo sigue siendo observar la mejora de coherencia después de actualizar las instrucciones.

## Añade un estándar al repositorio

`.github/copilot-instructions.md` contiene información general del proyecto. Añadirás los estándares de código para mejorar las sugerencias de Copilot.

1. Vuelve a abrir `.github/copilot-instructions.md`.
2. Busca la sección **Code formatting requirements**, que debería estar cerca de la línea 27. Describe los estándares de código, pero todavía no incluye reglas de documentación en el código.
3. Añade estas líneas de Markdown justo después de los estándares existentes para pedir comentarios al principio de los archivos y comentarios TSDoc:

   ```markdown
   - Every exported function should have a TSDoc comment describing its purpose, parameters, and return value.
   - Before imports or any code, add a comment block to the file that explains its purpose.
   ```

4. Guarda `copilot-instructions.md`.

> [!TIP]
> Como has visto en la lección anterior, puedes crear archivos de instrucciones en el repositorio (`.github/copilot-instructions.md`) para directrices generales o archivos `*.instructions.md` para lenguajes, tipos de archivo o tareas concretos. El archivo del repositorio es el lugar adecuado para estándares generales, como la regla de comentarios de documentación que acabas de añadir.

## Repite el mensaje y observa el cambio

Vuelve a enviar el mismo mensaje para comprobar cómo se aplican las instrucciones actualizadas.

1. Vuelve a Copilot Chat y selecciona **New Chat** para vaciar el contexto.
2. Selecciona `src/lib/publishers.ts` para que Copilot se centre en el archivo adecuado.
3. Envía **el mismo mensaje** que antes:

   ```plaintext
   Crea o actualiza src/lib/publishers.ts con un método de acceso a datos que devuelva una lista de todas las editoriales, con el nombre y el id de cada una. Aplica los cambios a los archivos.
   ```

4. Observa que el archivo propuesto ahora empieza con un bloque de comentarios parecido a este:

   ```typescript
   /**
    * Publisher data-access helpers for the Tailspin Toys Crowd Funding platform.
    * Provides functions to retrieve publisher information from the database.
    */
   ```

5. Comprueba que la función propuesta ahora incluye un comentario TSDoc parecido a este:

   ```typescript
   /**
    * Returns a list of all publishers with their id and name.
    *
    * @param db - The Drizzle database client.
    * @returns A promise that resolves to an array of publisher objects.
    */
   ```

Has orientado a Copilot para que aplique un estándar nuevo a código real, que utilizarás en el siguiente ejercicio.

## Confirma los cambios de instrucciones y publica la rama

Los archivos de instrucciones son recursos del repositorio y se gestionan mediante el control de versiones como cualquier otro archivo. Confirmarás y publicarás la rama.

1. Abre un terminal nuevo pulsando <kbd>Control</kbd>+<kbd>`</kbd> (Mac) o <kbd>Ctrl</kbd>+<kbd>`</kbd> (Windows/Linux).
2. Comprueba que estén presentes la actualización de instrucciones y los cambios del método auxiliar:

   ```bash
   git status
   ```

3. Prepara y confirma la actualización de instrucciones y todos los archivos modificados por Copilot para el método auxiliar:

   ```bash
   git add .github/copilot-instructions.md src/lib/publishers.ts
   # If git status shows additional supporting updates (for example tests), add those files too.
   git commit -m "Add doc comment standards and publishers helper foundation"
   ```

4. Publica la rama en el repositorio:

   ```bash
   git push -u origin custom-instructions
   ```

## Crea e integra una solicitud de incorporación de cambios

Ya has publicado la rama. Ahora crearás una solicitud de incorporación de cambios y la vincularás a la incidencia del backlog sobre los estándares de documentación. Copilot puede localizar la incidencia, crear la PR vinculada y, después, integrarla.

> [!NOTE]
> Este es el primer ejercicio en el que Copilot actúa en GitHub en tu nombre. La plantilla del proyecto ya incluye las herramientas de GitHub, por lo que no tienes que configurarlas. La primera vez que Copilot utilice una herramienta, VS Code puede pedirte que inicies sesión en GitHub. Sigue las indicaciones para autorizarlo. En un ejercicio posterior aprenderás cómo funciona esta conexión mediante el Model Context Protocol.

1. Abre Copilot Chat en el codespace.
2. Pulsa <kbd>Control</kbd>+<kbd>Command</kbd>+<kbd>I</kbd> (Mac) o <kbd>Ctrl</kbd>+<kbd>Alt</kbd>+<kbd>I</kbd> (Windows/Linux) para abrir la vista Copilot Chat y confirma que **Agent** está seleccionado en el selector de agentes.
3. Pide a Copilot que encuentre la incidencia sobre la actualización de los archivos de instrucciones y cree una PR desde la rama actual, describiendo tanto las instrucciones como la base del método auxiliar para editoriales:

   ```plaintext
   Busca la incidencia relacionada con la actualización del archivo de instrucciones. Crea una nueva PR desde la rama actual, indica que la PR cierra esa incidencia y añade que también hemos creado la base del método auxiliar de editoriales para el próximo trabajo de filtrado.
   ```

4. Copilot empezará a buscar la incidencia y a crear la PR.
5. Cuando Copilot te pida permiso para realizar acciones de GitHub, revisa el comando y selecciona **Allow** según corresponda.
6. Cuando se cree la PR, pide a Copilot que la integre y vuelva a `main`:

   ```plaintext
   Integra la PR en main. Después, vuelve a main localmente y descarga el código más reciente para dejar el repositorio actualizado.
   ```

7. Cuando Copilot te pida permiso para realizar acciones de GitHub y ejecutar comandos de shell, revisa el comando y selecciona **Allow** según corresponda.

Has creado e integrado una solicitud de incorporación de cambios con la ayuda de GitHub Copilot.

## Resumen y pasos siguientes

Has explorado cómo Copilot obtiene contexto de los archivos de instrucciones del proyecto y has utilizado Copilot Chat en VS Code para:

- Enviar un mensaje de generación de código y observar el resultado con las instrucciones *existentes*.
- Añadir un estándar general al repositorio en `.github/copilot-instructions.md`.
- Repetir el mismo mensaje y observar cómo el código propuesto aplica el nuevo estándar.
- Confirmar la actualización de instrucciones y la base del método auxiliar en `main` para que el siguiente ejercicio pueda aprovecharlas.

A continuación, pondrás en práctica esas instrucciones en el [modo agente][next-lesson], donde Copilot añadirá una nueva funcionalidad en varias partes del código.

## Recursos

- [Archivos de instrucciones para personalizar GitHub Copilot][instruction-files]
- [Prácticas recomendadas para crear instrucciones personalizadas][instructions-best-practices]
- [Cinco consejos para escribir mejores instrucciones personalizadas para Copilot][copilot-instructions-five-tips]
- [Instrucciones personales para GitHub Copilot][personal-instructions]
- [Awesome Copilot: archivos de instrucciones y otros recursos][awesome-copilot]

[previous-lesson]: ../0-prerequisites/
[next-lesson]: ../2-agent-mode/
[instruction-files]: https://code.visualstudio.com/docs/copilot/copilot-customization
[instructions-best-practices]: https://docs.github.com/enterprise-cloud@latest/copilot/using-github-copilot/coding-agent/best-practices-for-using-copilot-to-work-on-tasks#adding-custom-instructions-to-your-repository
[personal-instructions]: https://docs.github.com/copilot/customizing-copilot/adding-personal-custom-instructions-for-github-copilot
[copilot-instructions-five-tips]: https://github.blog/ai-and-ml/github-copilot/5-tips-for-writing-better-custom-instructions-for-copilot/
