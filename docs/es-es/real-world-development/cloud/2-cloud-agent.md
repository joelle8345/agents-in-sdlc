---
title: "Ejercicio 2: Agente en la nube de GitHub Copilot"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

| [← Lección anterior: Instrucciones personalizadas][previous-lesson] |
|:--|

Muchas organizaciones tienen problemas de deuda técnica: incidencias de seguridad sin resolver, código heredado que necesita actualizarse o funcionalidades solicitadas que siguen pendientes por falta de tiempo. El agente en la nube de GitHub Copilot puede actualizar código y añadir funcionalidades de forma autónoma. Cuando termina, crea una solicitud de incorporación de cambios (PR) en borrador para que un desarrollador la revise. Así puedes delegar tareas tediosas, acelerar el desarrollo y centrarte en cuestiones de mayor alcance.

En este ejercicio explorarás cómo utilizar el agente en la nube para:

- Personalizar el entorno en el que genera código.
- Garantizar que las operaciones se realizan de forma segura.
- Comprender la importancia de definir incidencias con un alcance claro.
- Asignar incidencias a Copilot.

## Escenarios

Tailspin Toys quiere resolver parte de su deuda técnica. Los contratistas que crearon la primera versión del sitio no documentaron el código. Como primer paso, el equipo quiere añadir comentarios de TypeScript Documentation (TSDoc) a todas las funciones exportadas de la aplicación.

Además, el equipo de diseño quiere facilitar el descubrimiento de juegos. Quiere que la página de detalles de cada juego muestre otros títulos de la misma categoría para que los usuarios puedan seguir explorando. No hace falta una implementación pulida: basta con una versión que permita probar la experiencia de usuario. Aunque este trabajo bloquea al equipo, hay incidencias de mayor prioridad.

Son tareas que suelen quedar relegadas y que puedes asignar al agente en la nube de Copilot. El agente puede trabajar en segundo plano mientras tú te ocupas de otras tareas. Después, revisarás su trabajo y comprobarás que cumple los requisitos.

## Presentación del agente en la nube de GitHub Copilot

El [agente en la nube de GitHub Copilot](https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent#overview-of-copilot-cloud-agent-formerly-copilot-coding-agent) puede realizar tareas en segundo plano de forma parecida a un desarrollador. Por ejemplo, puedes [asignar una incidencia de GitHub a Copilot](https://docs.github.com/copilot/how-tos/use-copilot-agents/cloud-agent/start-copilot-sessions). Cuando se la asignas, Copilot crea una PR en borrador para mostrar el progreso, prepara un entorno y empieza a trabajar. Puedes consultar la sesión mientras trabaja o cuando haya terminado. Cuando la solución esté lista para revisión, Copilot te mencionará en la PR.

## La importancia de definir bien el alcance de las instrucciones

GitHub Copilot no hace magia: no elimina la necesidad de pensar. Incluso las tareas que parecen sencillas pueden tener cierta complejidad, así que [define con cuidado el alcance de las tareas del agente en la nube][cloud-agent-best-practices]. Trátalo como a un compañero de programación basado en IA: divide el trabajo en etapas, aprende, experimenta y adapta el enfoque. Los fundamentos del desarrollo de software no cambian al añadir inteligencia artificial generativa.

## Instrucciones personalizadas de este repositorio

En ejercicios anteriores has explorado las instrucciones personalizadas y cómo guían a Copilot. Si ya has completado un ejercicio práctico sobre instrucciones, habrás visto `.github/copilot-instructions.md` en acción. Si no, aprovecha para revisar los archivos incluidos en este repositorio antes de asignar trabajo al agente en la nube. Así podrás reconocer su efecto más adelante.

Abre estos archivos en la interfaz web de GitHub o en un codespace que ya tengas en ejecución:

- `.github/copilot-instructions.md`: revisa la sección **Code standards**, especialmente las convenciones de TypeScript y los comentarios TSDoc.
- `.github/instructions/unit-tests.instructions.md`: fíjate en los metadatos `applyTo`, que aplican estas instrucciones a los archivos `**/*.test.ts`.

Cuando asignes al agente en la nube la incidencia `Code lacks documentation` en la siguiente sección, fíjate en si la PR incluye comentarios TSDoc, convenciones de TypeScript y comentarios al principio de los archivos. Estas directrices proceden de los archivos de instrucciones que acabas de revisar. Volverás a comprobarlo al revisar las PR en un ejercicio posterior.

## Configurar el entorno de desarrollo del agente en la nube de Copilot

La creación de código suele requerir un entorno concreto y la ejecución de scripts de configuración para instalar herramientas y dependencias. Lo mismo ocurre al asignar una tarea a Copilot: el agente trabaja de forma similar a un ingeniero de software.

El agente en la nube utiliza [GitHub Actions][github-actions] para preparar su entorno. Puedes personalizarlo con un [flujo de trabajo de configuración especial][setup-workflow], definido en `.github/workflows/copilot-setup-steps.yml`, que se ejecuta antes de que el agente empiece a trabajar. Así puede acceder a las herramientas y dependencias necesarias. El taller ya incluye esta configuración para que puedas centrarte en el flujo de trabajo. Permite que Copilot instale Node.js y las dependencias del proyecto, los navegadores de las pruebas de extremo a extremo y la base de datos SQLite migrada y con datos iniciales de la aplicación Astro:

```yaml
name: "Copilot Setup Steps"

# Allows you to test the setup steps from your repository's "Actions" tab
on: workflow_dispatch

env:
  ASTRO_TELEMETRY_DISABLED: "1"

jobs:
  copilot-setup-steps:
    runs-on: ubuntu-latest
    # Set the permissions to the lowest permissions possible needed for *your steps*. Copilot will be given its own token for its operations.
    permissions:
      # If you want to clone the repository as part of your setup steps, for example to install dependencies, you'll need the `contents: read` permission. If you don't clone the repository in your setup steps, Copilot will do this for you automatically after the steps complete.
      contents: read
    steps:
      - name: Checkout code
        uses: actions/checkout@v5

      # Frontend / app setup - Node.js (the whole app is now Astro + Drizzle/libSQL)
      - name: Set up Node.js
        uses: actions/setup-node@v6
        with:
          node-version: "lts/*"
          cache: "npm"
          cache-dependency-path: "./package-lock.json"

      - name: Install JavaScript dependencies
        run: npm ci

      - name: Install Playwright browsers
        run: npx playwright install --with-deps chromium

      # Migrate + seed the local SQLite database so builds and tests have data.
      - name: Set up the database
        run: npm run db:setup
```

El archivo es similar a cualquier flujo de trabajo de GitHub, pero tiene algunos aspectos importantes:

- Contiene un único trabajo, `copilot-setup-steps`, que se ejecuta en GitHub Actions antes de que Copilot empiece a trabajar en la PR.
- El desencadenador `workflow_dispatch` permite ejecutar el flujo de trabajo manualmente desde la pestaña **Actions** del repositorio. Esto resulta útil para comprobar que funciona sin esperar a que Copilot lo ejecute.

## Añadir documentación

Aunque la documentación es importante, muchos proyectos tienen información desactualizada o carecen de ella. Esta deuda técnica ralentiza el trabajo y dificulta el mantenimiento del código o la incorporación de nuevos desarrolladores. Copilot puede ayudarte a crear documentación, por lo que esta es una buena tarea para asignar al agente en la nube. El agente trabajará en segundo plano y más adelante revisarás el resultado.

1. Abre una pestaña nueva y ve al repositorio en github.com.
2. Selecciona la pestaña **Issues**.
3. Selecciona **New issue** para abrir el cuadro de diálogo de creación de incidencias.
4. Selecciona **Blank issue**.
5. Escribe `Code lacks documentation` en el campo **Title**.
6. Escribe lo siguiente en **Description**:

    ```plaintext
    Our organization has a requirement that functions and methods include TSDoc doc comments where helpful. Unfortunately, recent updates haven't followed this standard. We need to update the existing code to ensure doc comments are included where they clarify behavior.
    ```

7. Selecciona **Create** para crear la incidencia.
8. En el lado derecho, selecciona **Assign to Copilot** para abrir el cuadro de asignación.

    ![Asignar Copilot a una incidencia](../../../_images/shared-assign-copilot.png)

9. Selecciona **Assign**.
10. Selecciona la pestaña **Pull Requests**.
11. Abre la PR nueva, que tendrá un título parecido a `[WIP]: Code lacks documentation`. Si todavía no aparece, espera un momento y actualiza la página del navegador.
12. Al cabo de unos minutos, Copilot debería crear una lista de tareas.

> [!NOTE]
> La lista puede tardar varios minutos en aparecer. Copilot está preparando el entorno mediante el flujo de trabajo anterior, analizando el proyecto y determinando cómo abordar la tarea.

13. Revisa la lista y las tareas que Copilot va a completar.
14. Desplázate por la cronología de la PR hasta ver que Copilot ha empezado a trabajar en la incidencia.
15. Selecciona el botón **View session**.

    ![Vista de la sesión de Copilot](../../../_images/ex4-view-session.png)

> [!CAUTION]
> Puede que tengas que actualizar la página para ver el indicador actualizado.

16. Recorre la sesión en directo para observar cómo Copilot explora el código, comprende el estado del proyecto, decide un plan y crea código.

El proceso puede tardar varios minutos. Una de las ventajas principales del agente en la nube es que realiza tareas de forma asíncrona, lo que te permite centrarte en otro trabajo. Aprovecharás esa función asignándole otra tarea y, mientras tanto, añadirás funcionalidades a la aplicación.

## Añadir una sección de juegos relacionados a la página de detalles

Una de las ventajas del agente en la nube es que permite repartir el trabajo: tú puedes ocuparte de unas tareas mientras el agente aborda otras. Añadir una sección de juegos relacionados para el equipo de diseño quizá no lleve mucho tiempo, pero podrías dedicarlo a otras tareas. Asígnasela al agente en la nube.

1. Vuelve al repositorio en github.com.
2. Selecciona la pestaña **Issues**.
3. Selecciona **New issue** para abrir el cuadro de diálogo de creación de incidencias.
4. Selecciona **Blank issue**.
5. Escribe `Show related games on the game details page` en el campo **Title**.
6. Escribe lo siguiente en **Description**:

    ```markdown
    We want to help people discover more games by showing related games on each game's details page. The design team wants to explore the UX and do some acceptance testing. Our requirements are:

   - Add a data-access helper in `src/lib/` that returns other games in the same category as a given game, excluding that game
   - Show a "Related games" section on the game details page that uses the helper
   - Handle the case where a game has no related games
   - There should be unit tests created for the new helper
   - Before creating the PR, ensure all tests pass
    ```

7. Selecciona **Create** para crear la incidencia.
8. En el lado derecho, selecciona **Assign to Copilot** para abrir el cuadro de asignación.

    ![Asignar Copilot a una incidencia](../../../_images/shared-assign-copilot.png)

9. Selecciona **Assign**.

Poco después, verás varios ojos 👀 en el primer comentario de la incidencia. Esto indica que Copilot está trabajando.

![Los ojos indican que Copilot está trabajando en la incidencia](../../../_images/ex4-issue-eyes-emoji.png)

Copilot ya está trabajando en la segunda tarea. El agente funciona de forma similar a un ingeniero de software, así que no necesitas supervisarlo continuamente: podrás revisar el trabajo cuando termine. Mientras tanto, crearás y utilizarás agentes personalizados.

## Resumen y pasos siguientes

Has explorado el [agente en la nube de GitHub Copilot][copilot-agents]. Puedes asignarle incidencias para que las resuelva de forma asíncrona y utilizarlo para abordar deuda técnica, crear funcionalidades o migrar código entre frameworks.

Has explorado estos conceptos:

- Personalizar el entorno para generar código.
- Garantizar que las operaciones se realizan de forma segura.
- Definir incidencias con un alcance claro.
- Asignar incidencias a Copilot.

Mientras el agente trabaja en segundo plano, a continuación crearás y utilizarás agentes personalizados. El [agente en la nube también puede utilizar servidores MCP][cloud-agent-mcp] e instrucciones personalizadas, que ya has explorado.

## Recursos

- [Acerca de los agentes de Copilot][copilot-agents]
- [Asignar incidencias de GitHub a Copilot][assign-issue]
- [Prácticas recomendadas para el flujo de configuración del agente en la nube][cloud-agent-best-practices]

| [Siguiente lección: Agentes personalizados →][next-lesson] |
|--:|

[previous-lesson]: ../1-custom-instructions/
[next-lesson]: ../3-custom-agents/
[cloud-agent-mcp]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/extend-cloud-agent-with-mcp
[assign-issue]: https://docs.github.com/copilot/how-tos/use-copilot-agents/cloud-agent/start-copilot-sessions
[setup-workflow]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[copilot-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[cloud-agent-best-practices]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[github-actions]: https://docs.github.com/actions
