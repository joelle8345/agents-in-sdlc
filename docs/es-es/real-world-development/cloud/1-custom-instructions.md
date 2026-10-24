---
title: "Ejercicio 1: Instrucciones personalizadas (agente en la nube)"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

[← Lección anterior: Requisitos previos][previous-lesson] · [Siguiente lección: Agente en la nube de Copilot →][next-lesson]

El contexto es esencial cuando se trabaja con inteligencia artificial generativa. Si una tarea debe hacerse de una manera concreta o Copilot necesita información de contexto, debes asegurarte de que pueda acceder a ella. Los [archivos de instrucciones][instruction-files] proporcionan esa guía para que Copilot entienda no solo qué debe hacer, sino también cómo.

En este ejercicio:

- Explorarás cómo el contexto específico del proyecto, las directrices de programación y los estándares de documentación llegan a Copilot mediante instrucciones personalizadas del repositorio y archivos de instrucciones asociados a rutas.
- Añadirás un estándar general al repositorio en `.github/copilot-instructions.md`.

> [!NOTE]
> A diferencia de los recorridos de VS Code y CLI, aquí no compararás una instrucción antes y después de usarla. El agente en la nube de Copilot trabaja de forma asíncrona en incidencias de GitHub, por lo que resulta más difícil mostrar su efecto en tiempo real. Verás la influencia del archivo de instrucciones más adelante, al revisar las solicitudes de incorporación de cambios que cree el agente.

## Archivos de instrucciones

### Escenario

Tailspin Toys tiene directrices y requisitos para las prácticas de desarrollo:

- La capa de datos siempre debe tener pruebas unitarias.
- La interfaz de usuario debe utilizar el modo oscuro y tener un aspecto moderno.
- El código debe incluir documentación en forma de comentarios de TypeScript Documentation (TSDoc).
- Al principio de cada archivo debe haber un bloque de comentarios que describa su propósito.

Utilizarás archivos de instrucciones para que Copilot disponga del contexto necesario y realice las tareas de acuerdo con estas prácticas.

### Instrucciones personalizadas

Las instrucciones personalizadas proporcionan contexto y preferencias a Copilot para que pueda ofrecer sugerencias más pertinentes y código que se ajuste a tus requisitos. Puedes especificar convenciones de código, bibliotecas y tipos de comentarios, y crear instrucciones para todo el repositorio o para tipos de archivo concretos.

Hay dos tipos de archivos de instrucciones:

- `.github/copilot-instructions.md` es un único archivo que se envía a Copilot en todas las solicitudes del repositorio. Debe incluir información general del proyecto, como la pila tecnológica, una descripción del trabajo y directrices globales.
- Los archivos `.github/instructions/*.instructions.md` permiten definir directrices para tareas o tipos de archivo concretos, como TypeScript, Astro, componentes de interfaz o pruebas unitarias.

> [!NOTE]
> En un entorno de desarrollo integrado (IDE), los archivos de instrucciones solo se utilizan para generar código en Copilot Chat, no para completados de código ni sugerencias de edición siguiente.
>
> Copilot Chat, Copilot CLI y el agente en la nube de Copilot utilizan tanto las instrucciones del repositorio como los archivos `*.instructions.md` que incluyen metadatos `applyTo`.
>
> Copilot también admite [archivos de instrucciones de otros estándares][custom-instructions-support], como AGENTS.md y CLAUDE.md.

### Prácticas recomendadas para gestionar archivos de instrucciones

El proyecto de ejemplo muestra un enfoque representativo para crear archivos de instrucciones. En general:

- Mantén `copilot-instructions.md` centrado en directrices generales del proyecto, como su estructura, una descripción y los estándares de código globales.
- Utiliza archivos `*.instructions.md` para tipos de archivo concretos, como pruebas unitarias, componentes Astro y la capa de datos, o para tareas específicas.
- Escribe directrices claras en lenguaje natural e incluye ejemplos de código correcto e incorrecto.

No existe una única manera correcta de crear archivos de instrucciones ni de utilizar la inteligencia artificial. La experimentación te ayudará a encontrar el enfoque adecuado para tu proyecto.

> [!TIP]
> Todos los proyectos que utilizan GitHub Copilot deberían tener un conjunto sólido de archivos de instrucciones. Al revisar los de este proyecto, encontrarás archivos para tareas como [actualizar la interfaz de usuario][ui-instructions] y trabajar con [Astro][astro-instructions].
>
> Copilot también puede ayudarte a generar archivos de instrucciones. Cada interfaz ofrece esta opción de una forma distinta (por ejemplo, **Configure Chat → Generate Agent Instructions** en VS Code o `/init` en Copilot CLI). La lección correspondiente a cada interfaz explicará cómo utilizarla cuando sea pertinente.
>
> Para encontrar plantillas o un punto de partida, consulta [awesome-copilot][awesome-copilot], un repositorio con archivos de instrucciones, agentes personalizados y otros recursos.

[ui-instructions]: https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/ui.instructions.md
[astro-instructions]: https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/astro.instructions.md
[awesome-copilot]: https://github.com/github/awesome-copilot
[custom-instructions-support]: https://docs.github.com/copilot/reference/custom-instructions-support

## Explora los archivos de instrucciones personalizadas del proyecto

Lee los archivos de instrucciones incluidos en este repositorio: hay un archivo principal `copilot-instructions.md` y varios archivos `*.instructions.md` para distintas tareas. Ábrelos en el editor o en la interfaz web de GitHub.

1. Abre `.github/copilot-instructions.md`.
2. Revisa la descripción breve del proyecto y secciones como **Agent notes**, **Code standards**, **Scripts** y **Repository Structure**. Estas directrices se aplican a cualquier interacción con Copilot. En **Code standards**, fíjate también en las directrices anidadas de **GitHub Actions Workflows**.
3. Abre la carpeta `.github/instructions` y explórala. Encontrarás instrucciones para archivos Astro, la capa de datos Drizzle, las pruebas y otros temas.
4. Abre `.github/instructions/unit-tests.instructions.md`. El campo `applyTo` de la parte superior define un patrón global relativo a la raíz del repositorio que determina a qué archivos se aplican las instrucciones. En este caso, coincide con los archivos de prueba TypeScript que cumplen `**/*.test.ts`.
5. Revisa las instrucciones específicas para crear pruebas unitarias en este proyecto.
6. Abre `.github/instructions/drizzle.instructions.md` y ve al final. Observa los enlaces a otros archivos de instrucciones, como `unit-tests.instructions.md`, y a archivos existentes del proyecto. Las rutas de esos enlaces son relativas al archivo de instrucciones, no a la raíz del repositorio.

> [!NOTE]
> La sección **Code formatting requirements** de `copilot-instructions.md` describe los estándares de código del proyecto, pero todavía no exige documentación en el código. En los pasos siguientes, añadirás reglas para los comentarios TSDoc y los comentarios al principio de cada archivo.

## Añade un estándar al repositorio

Ahora añadirás una regla general del proyecto para incluir documentación en el código mediante comentarios TSDoc y un comentario al principio de cada archivo. El agente en la nube aplicará esta regla al trabajar en las incidencias que le asignes más adelante.

Antes de editar, crea una rama:

1. En el terminal del codespace, crea una rama y cámbiate a ella:

   ```bash
   git checkout -b custom-instructions-cloud
   ```

`.github/copilot-instructions.md` contiene información general del proyecto. Añade los estándares de código para que Copilot genere sugerencias mejores.

1. Vuelve a abrir `.github/copilot-instructions.md`.
2. Busca la sección **Code formatting requirements**, que debería estar cerca de la línea 27. Describe los estándares de código, pero todavía no incluye reglas de documentación en el código.
3. Añade las siguientes líneas de Markdown justo después de los estándares existentes:

   ```markdown
   - Every exported function should have a TSDoc comment describing its purpose, parameters, and return value.
   - Before imports or any code, add a comment block to the file that explains its purpose.
   ```

4. Guarda `copilot-instructions.md`.

> [!TIP]
> Como has visto en la lección anterior, puedes crear archivos de instrucciones en el repositorio (`.github/copilot-instructions.md`) para directrices generales o archivos `*.instructions.md` para lenguajes, tipos de archivo o tareas concretos. El archivo del repositorio es el lugar adecuado para estándares generales, como la regla de comentarios de documentación que acabas de añadir.

## Confirma, publica e integra la actualización de instrucciones

El agente en la nube lee los archivos de instrucciones de la rama a la que apunta la incidencia. Cuando le asignes una incidencia en el siguiente ejercicio, creará una rama a partir de `main`. Por eso, debes integrar las instrucciones en `main` para que el agente pueda utilizarlas.

1. Prepara y confirma el cambio:

   ```bash
   git add .github/copilot-instructions.md
   git commit -m "Add doc comment and file-header standards to copilot instructions"
   ```

2. Publica la rama:

   ```bash
   git push -u origin custom-instructions-cloud
   ```

3. En github.com, abre una solicitud de incorporación de cambios de `custom-instructions-cloud` a `main` e intégrala. Así, el agente en la nube podrá leer estas instrucciones cuando trabaje en las incidencias que le asignes en el siguiente ejercicio.

> [!TIP]
> Si prefieres trabajar directamente en `main` durante el taller, puedes omitir la rama y confirmar los cambios en `main`. El uso de una rama permite practicar un flujo de trabajo habitual en un proyecto real.

## Resumen y pasos siguientes

Has explorado cómo Copilot obtiene contexto de los archivos de instrucciones del proyecto y has añadido un estándar general a `.github/copilot-instructions.md`. Verás cómo se aplica en las solicitudes de incorporación de cambios del agente en la nube durante el resto de este recorrido.

A continuación, [asigna tu primera incidencia al agente en la nube de Copilot][next-lesson].

## Recursos

- [Archivos de instrucciones para personalizar GitHub Copilot][instruction-files]
- [Prácticas recomendadas para crear instrucciones personalizadas][instructions-best-practices]
- [Cinco consejos para escribir mejores instrucciones personalizadas para Copilot][copilot-instructions-five-tips]
- [Awesome Copilot: archivos de instrucciones y otros recursos][awesome-copilot]

[previous-lesson]: ../0-prerequisites/
[next-lesson]: ../2-cloud-agent/
[instruction-files]: https://docs.github.com/copilot/customizing-copilot/about-customizing-github-copilot-chat-responses
[instructions-best-practices]: https://docs.github.com/enterprise-cloud@latest/copilot/using-github-copilot/coding-agent/best-practices-for-using-copilot-to-work-on-tasks#adding-custom-instructions-to-your-repository
[copilot-instructions-five-tips]: https://github.blog/ai-and-ml/github-copilot/5-tips-for-writing-better-custom-instructions-for-copilot/
