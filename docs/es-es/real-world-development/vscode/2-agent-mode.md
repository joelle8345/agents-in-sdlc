---
title: "Ejercicio 2: Añadir funcionalidad con el modo agente de Copilot"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

Incluso los cambios más sencillos suelen requerir modificar varios archivos y ejecutar tareas como las pruebas. El flujo de trabajo habitual consiste en localizar los archivos necesarios, hacer los cambios, ejecutar las pruebas, depurar, averiguar qué archivo falta y volver a modificar el código. El modo agente de Copilot puede ayudarte a coordinar ese trabajo.

El modo agente trabaja de forma más autónoma en el IDE. Explora la estructura del proyecto, realiza los cambios necesarios, ejecuta tareas como las pruebas y corrige los errores que detecta. En este ejercicio lo utilizarás para añadir funcionalidad al sitio.

> [!NOTE]
> Aunque los nombres sean parecidos, el modo agente y el agente en la nube ofrecen experiencias distintas. El modo agente trabaja en el IDE y permite iterar rápidamente e interactuar con Copilot. El agente en la nube trabaja de forma asíncrona, como un miembro del equipo, mediante incidencias y solicitudes de incorporación de cambios.

En este ejercicio:

- Utilizarás el modo agente de Copilot para explorar el proyecto, identificar archivos relevantes y coordinar cambios.
- Implementarás una funcionalidad en la interfaz y la capa de datos.
- Revisarás los cambios y las pruebas generados por Copilot antes de integrarlos en el código.

## Escenario

A medida que crece la lista de juegos, quieres que los usuarios puedan filtrarlos por categoría y editorial. En el ejercicio anterior ya añadiste un método auxiliar para obtener editoriales. Ahora completarás el trabajo restante en la capa de datos, la interfaz y las pruebas con el modo agente de Copilot.

## Ejecuta el sitio Tailspin Toys

Antes de hacer cambios, explora el sitio Tailspin Toys para conocer su funcionamiento actual.

El sitio es una plataforma de financiación colectiva de juegos de mesa con temática de desarrollo. Permite mostrar juegos y sus detalles. Es una única aplicación Astro que genera páginas HTML estáticas durante la compilación. Las páginas consultan directamente una base de datos SQLite local desde sus metadatos mediante Drizzle ORM; no hay una API de backend independiente ni un framework de interfaz del lado del cliente. Los métodos de acceso a datos reutilizables se encuentran en `src/lib/`, y la interactividad se implementa con un pequeño `<script>` de Astro que utiliza las API estándar del DOM.

### Inicia el sitio web

El comando `npm run dev` inicia el único servidor de desarrollo Astro. Ejecútalo en GitHub Codespaces.

1. Vuelve al codespace. Deberías estar en `main` tras el ejercicio anterior.
2. Abre un terminal nuevo en el codespace pulsando <kbd>Control</kbd>+<kbd>`</kbd> (Mac) o <kbd>Ctrl</kbd>+<kbd>`</kbd> (Windows/Linux).
3. Actualiza `main` y crea una rama para el filtrado:

   ```bash
   git checkout main
   git pull
   git checkout -b filtering-vscode
   ```

4. Inicia el sitio:

   ```bash
   npm run dev
   ```

   Cuando el servidor de desarrollo Astro esté listo, debería aparecer un mensaje con la URL, parecido a este:

   ```bash
   🚀 Tailspin Toys is ready!
      Astro server: http://localhost:4321
      Press Ctrl-C to stop.
   ```

> [!NOTE]
> Si aparece un cuadro de diálogo que te pregunta si quieres abrir `http://localhost:4321` en un navegador, ciérralo seleccionando **x**.

5. Mantén pulsada la tecla <kbd>Command</kbd> (Mac) o <kbd>Ctrl</kbd> (Windows/Linux) y selecciona en el terminal la dirección del servidor Astro `http://localhost:4321`.

> [!NOTE]
> En un codespace, al seleccionar el enlace localhost en el terminal se te redirigirá automáticamente a `https://<your-codespace-name>-4321.app.github.dev/`. Es un túnel privado al codespace, que ahora aloja el servidor web.

### Explora el sitio web

Con el sitio en ejecución, explora sus funciones principales:

- **Página principal**: muestra una lista de juegos de mesa con sus títulos, imágenes y descripciones.
- **Página de detalles del juego**: al seleccionar un juego, se abre una página con más información, como el título, la descripción, la editorial y la categoría.

## Explora el backlog con Copilot

> [!TIP]
> **Abre Copilot Chat**
>
> Antes de empezar, vuelve al codespace, abre el panel Copilot Chat y selecciona **New Chat** para iniciar una conversación nueva. La selección de modo y modelo varía según el ejercicio; cada paso indicará cuándo cambiarla.

La implementación inicial del sitio funciona, pero quieres añadir nuevas capacidades. Empezarás revisando el backlog de incidencias que se creó al preparar el proyecto.

1. En la vista Chat, selecciona **Agent** en el selector de agentes. El modo agente puede planificar e implementar cambios en varios archivos, ejecutar comandos de terminal e invocar herramientas.

   ![Selector del agente en la vista Chat](../../../_images/shared-chat-mode-selector.png)

2. Selecciona **Claude Sonnet 4.5** en la lista de modelos disponibles.

> [!CAUTION]
> Los autores de este taller no recomiendan un modelo sobre otro. Utilizamos Claude Sonnet 4.5 para crear el taller y lo mencionamos para procurar que las sugerencias sean coherentes. Sin embargo, como los modelos de lenguaje grandes (LLM) ofrecen resultados probabilísticos, las sugerencias pueden diferir de los ejemplos. Es normal y esperable.

> [!NOTE]
> Debido a la naturaleza probabilística de los LLM, Copilot puede utilizar un comando MCP distinto, pero debería poder completar la tarea.

3. Envía este mensaje para pedir a Copilot que muestre las incidencias pendientes:

   ```plaintext
   Muéstrame el backlog de incidencias de mi repositorio de GitHub. Ayúdame a priorizarlas según su utilidad para los usuarios.
   ```

4. Selecciona **Continue** para ejecutar el comando que muestra todas las incidencias.
5. Revisa la lista generada.

Observa que Copilot también ha priorizado las incidencias según las que considera más útiles para los usuarios.

## Revisa los archivos de instrucciones

Antes de pedir al agente que genere código, revisa el archivo de instrucciones que proporcionará contexto. Utilizarás el archivo de [instrucciones de interfaz de usuario (UI)](https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/ui.instructions.md), que contiene indicaciones para añadir funcionalidad al sitio.

1. En el codespace, abre `.github/instructions/ui.instructions.md`.
2. Revisa las directrices generales para añadir funcionalidad. Incluyen:
   - Una descripción de la arquitectura.
   - Principios para el diseño de componentes, la capacidad de prueba y la accesibilidad.
   - Enlaces a instrucciones específicas para distintos tipos de archivo, entre ellos:
     - Astro
     - Tailwind CSS
     - Drizzle

> [!TIP]
> Los archivos de instrucciones pueden enlazar a otros archivos de instrucciones y a archivos del proyecto. Las rutas son relativas al archivo de instrucciones. Así puedes reutilizar directrices, dividir conjuntos complejos en archivos más pequeños y proporcionar ejemplos y plantillas.

## Implementa la funcionalidad de filtrado

Para completar el filtrado, tendrás que realizar al menos tres cambios en la aplicación:

- Añadir o ajustar la lógica de filtrado restante en la capa de datos (`src/lib/`).
- Añadir o actualizar las pruebas del comportamiento del filtrado.
- Actualizar la página de lista de juegos para incorporar la interfaz de filtrado.

Además, las pruebas deben ejecutarse y superarse antes de integrar los cambios. El modo agente de Copilot puede realizar estas tareas.

1. Continúa en la conversación actual de Copilot o selecciona **New Chat** para iniciar otra.
2. Selecciona **Add Context**, **Instructions** y **ui** para añadir el archivo de instrucciones.

   ![Seleccionar el archivo de instrucciones de interfaz de usuario](../../../_images/ex3-select-instructions-file.png)

3. Confirma que **Agent** sigue seleccionado en el selector de agentes de la vista Chat.

   ![Selector del agente en la vista Chat](../../../_images/shared-chat-mode-selector.png)

4. Confirma que sigue seleccionado el modelo **Claude Sonnet 4.5**.
5. Envía este mensaje para pedir a Copilot que implemente la funcionalidad según la incidencia relacionada del backlog:

   ```plaintext
   Actualiza el sitio para incluir el filtrado por editorial y categoría según los requisitos de la incidencia relacionada del backlog de GitHub. Ya existe un método auxiliar para obtener editoriales del ejercicio anterior; conserva y mejora ese trabajo según sea necesario mientras completas los cambios restantes en la capa de datos, la interfaz y las pruebas. Asegúrate de que todas las pruebas se superen antes de terminar. El servidor ya está en ejecución, así que no hace falta que lo inicies.
   ```

6. Observa cómo Copilot explora el proyecto y localiza los archivos relacionados con la funcionalidad. Debería encontrar métodos auxiliares de la capa de datos, la interfaz y las pruebas. Después, modificará los archivos y ejecutará las pruebas.

   ![Copilot explora los archivos del proyecto](../../../_images/ex3-agent-mode-explores.png)

> [!NOTE]
> Copilot realizará varias tareas, como explorar el proyecto, modificar archivos y ejecutar pruebas. El proceso puede tardar unos minutos, según la complejidad de la tarea y del código. Mientras trabaja, pueden aparecer los botones **Keep** y **Undo** en el editor. Al terminar, habrá un botón **Keep** o **Undo** para cada cambio; no hace falta seleccionarlos mientras el agente siga trabajando.

7. Cuando Copilot te lo solicite, selecciona **Continue** para ejecutar las pruebas.

   ![Cuadro de diálogo de Copilot Chat que solicita permiso para ejecutar las pruebas](../../../_images/ex3-agent-mode-run-tests.png)

8. Puede haber pausas y algunas pruebas pueden fallar durante el proceso. Copilot alterna entre generar código y ejecutar pruebas hasta terminar la tarea y dejar de detectar errores.

   ![Sesión completa de Copilot en modo agente](../../../_images/ex3-agent-mode-proposed-changes.png)

9. Revisa el código generado para detectar posibles problemas.

> [!CAUTION]
> Revisa siempre el código generado por Copilot y otras herramientas de IA.

10. Vuelve al navegador con el sitio en ejecución y prueba la nueva funcionalidad.
11. Cuando hayas confirmado que funciona y revisado el código, selecciona **Keep** en la ventana de Copilot Chat.

## Resumen y pasos siguientes

Has explorado cómo utilizar el modo agente de GitHub Copilot para añadir funciones al sitio de Tailspin Toys. En concreto:

- Has utilizado el modo agente de GitHub Copilot para implementar una funcionalidad en la interfaz y la capa de datos.
- Has explorado cómo el modo agente inspecciona el proyecto, identifica los archivos pertinentes y coordina los cambios.
- Has revisado los cambios y las pruebas generados por Copilot antes de integrarlos en el código.

A continuación, [probarás la funcionalidad con el servidor Playwright MCP][next-lesson] y crearás una solicitud de incorporación de cambios.

### Ejercicio de exploración adicional: implementar la paginación

A medida que crezca la lista de juegos, será necesario añadir paginación. Utiliza lo aprendido en este ejercicio y pide a Copilot que la implemente. Ten en cuenta estas decisiones:

- Sigue las prácticas recomendadas existentes, incluidos los archivos de instrucciones.
- Decide cómo funcionará la paginación: por ejemplo, si los usuarios podrán elegir el tamaño de página o si será fijo.
- Incluye en el mensaje las directrices necesarias para obtener la implementación que quieres.
- Puede que tengas que iterar con GitHub Copilot, solicitar cambios y aportar contexto. Es normal al trabajar con Copilot.

## Recursos

- [Modos ask, edit y agent de Copilot: qué hacen y cuándo utilizarlos][choose-mode]
- [Modo agente en VS Code][vs-code-agent-mode]

[previous-lesson]: ../1-custom-instructions/
[next-lesson]: ../3-mcp/
[choose-mode]: https://github.blog/ai-and-ml/github-copilot/copilot-ask-edit-and-agent-modes-what-they-do-and-when-to-use-them/
[vs-code-agent-mode]: https://code.visualstudio.com/docs/copilot/chat/chat-agent-mode
