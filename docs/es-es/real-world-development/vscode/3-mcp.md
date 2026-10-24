---
title: "Ejercicio 3: Probar la funcionalidad con el servidor Playwright MCP"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

[← Lección anterior: Modo agente][previous-lesson] · [Siguiente lección: Agentes personalizados →][next-lesson]

Acabas de crear la funcionalidad de filtrado con el modo agente. Antes de abrir una solicitud de incorporación de cambios, comprueba que funciona en el navegador. En lugar de probar la aplicación manualmente, conectarás el **servidor Playwright MCP** y dejarás que Copilot utilice un navegador real para probar la funcionalidad. Después, publicarás la rama y crearás la PR.

En este ejercicio:

- Aprenderás qué es el Model Context Protocol (MCP) y cómo amplían los servidores MCP las herramientas disponibles para Copilot.
- Añadirás el servidor Playwright MCP al espacio de trabajo.
- Pedirás a Copilot que lo utilice para probar manualmente la funcionalidad de filtrado en un navegador.
- Publicarás la rama y crearás una solicitud de incorporación de cambios para el filtrado.

## ¿Qué es el Model Context Protocol (MCP)?

El modo agente resulta mucho más útil cuando puede acceder a herramientas externas al editor. El Model Context Protocol (MCP) es un estándar que permite a Copilot comunicarse con esas herramientas y servicios.

![Diagrama de la interacción del modo agente con el contexto, el LLM y las herramientas, incluidas las aportadas por servidores MCP y extensiones de VS Code](../../../_images/ex1-mcp-diagram.png)

El [Model Context Protocol (MCP)](https://github.blog/ai-and-ml/llms/what-the-heck-is-mcp-and-why-is-everyone-talking-about-it/) permite que los agentes de IA se comuniquen con herramientas y servicios externos en tiempo real. Así pueden acceder a información actualizada mediante recursos y realizar acciones en tu nombre mediante herramientas.

Los agentes acceden a estas herramientas y recursos a través de un servidor MCP, que actúa como puente entre el agente y las herramientas y servicios externos. El servidor gestiona la comunicación entre el agente de IA y herramientas externas, como API existentes o herramientas locales en paquetes de npm. Cada servidor MCP proporciona un conjunto distinto de herramientas y recursos.

Algunos servidores MCP conocidos:

- **[Servidor MCP de GitHub](https://github.com/github/github-mcp-server)**: proporciona acceso a API para gestionar repositorios de GitHub, incluidas acciones como crear repositorios, actualizar los existentes y gestionar incidencias y solicitudes de incorporación de cambios.
- **[Servidor Playwright MCP](https://github.com/microsoft/playwright-mcp)**: ofrece funciones de automatización del navegador mediante Playwright, como abrir páginas, rellenar formularios y seleccionar botones.

Hay muchos otros servidores MCP que proporcionan herramientas y recursos distintos. GitHub aloja un [registro de MCP](https://github.com/mcp) para facilitar su descubrimiento y las contribuciones al ecosistema.

> [!CAUTION]
> Trata los servidores MCP como cualquier otra dependencia del proyecto. Antes de utilizar uno, revisa su código fuente, comprueba quién lo publica y considera las implicaciones de seguridad. Utiliza solo servidores de confianza y ten cuidado al conceder acceso a recursos u operaciones sensibles.

## Revisa la configuración de MCP

El archivo `.vscode/mcp.json` configura los servidores MCP disponibles en este espacio de trabajo de VS Code.

1. Abre `.vscode/mcp.json` en el codespace.
2. Comprueba que ya esté configurado el servidor `github`:

    ```json
    {
      "servers": {
        "github": {
          "type": "http",
          "url": "https://api.githubcopilot.com/mcp/"
        }
      }
    }
    ```

La plantilla del proyecto ya incluye la entrada `github`; por eso Copilot pudo leer el backlog de incidencias en el ejercicio anterior. Utiliza el [servidor MCP remoto de GitHub][remote-github-mcp-server], así que no tienes que instalarlo localmente. VS Code se conecta mediante HTTP y, la primera vez que Copilot utiliza una herramienta, te autenticas con GitHub.

## Añade el servidor Playwright MCP

Ahora añadirás un segundo servidor. El [servidor Playwright MCP][playwright-mcp-server] proporciona a Copilot un navegador que puede controlar, justo lo que necesitas para probar la funcionalidad.

1. En `.vscode/mcp.json`, añade una entrada `playwright` junto a `github` para que el archivo quede así:

    ```json
    {
      "servers": {
        "github": {
          "type": "http",
          "url": "https://api.githubcopilot.com/mcp/"
        },
        "playwright": {
          "command": "npx",
          "args": ["@playwright/mcp@latest", "--headless"]
        }
      }
    }
    ```

2. Guarda el archivo.

A diferencia del servidor remoto `github`, `playwright` se ejecuta localmente: VS Code lo inicia en el equipo con `npx @playwright/mcp@latest`. La opción `--headless` ejecuta el navegador sin mostrar una ventana. Es necesario en un codespace, que no tiene un escritorio donde mostrarla.

> [!NOTE]
> Tailspin Toys ya utiliza Playwright para las pruebas de extremo a extremo, por lo que normalmente el navegador necesario ya estará instalado. Si Copilot indica que falta un navegador, pídele que ejecute `npx playwright install chromium` y vuelva a intentarlo.

## Inicia y confía en el servidor

VS Code inicia los servidores MCP **cuando se necesitan**. La primera vez que Copilot utiliza las herramientas de un servidor, VS Code lo inicia y te pide que confirmes que confías en él.

1. En `.vscode/mcp.json`, aparecerá una acción **Start** encima de la entrada `playwright`. Selecciónala para iniciar el servidor y confirmar que la configuración es correcta.
2. Si VS Code te pregunta si confías en el servidor, revisa la configuración y confirma que confías en él para que pueda iniciarse.

Iniciarlo manualmente es opcional. Si omites estos pasos, VS Code iniciará el servidor y te pedirá que confirmes que confías en él la primera vez que Copilot necesite sus herramientas.

## Prueba la funcionalidad de filtrado

El [servidor Playwright MCP][playwright-mcp-server] proporciona a Copilot un navegador real que puede controlar. En lugar de probar la aplicación manualmente, el agente puede abrir una página, aplicar filtros y consultar los resultados. Después, resumirá lo que ha observado. Es una forma rápida de comprobar el comportamiento sin salir de la conversación.

El servidor Playwright MCP utiliza el [árbol de accesibilidad][playwright-mcp-server] de la página, no capturas de pantalla. El agente razona sobre elementos estructurados y etiquetados, como botones, enlaces y elementos de lista, igual que las tecnologías de asistencia. Así, una comprobación funcional rápida también permite hacer una revisión básica de accesibilidad.

Con el servidor conectado y la aplicación en ejecución, pide a Copilot que pruebe la funcionalidad de filtrado:

```text
Utiliza el servidor Playwright MCP, abre un navegador en la aplicación que se está ejecutando en http://localhost:4321 y verifica la nueva funcionalidad de filtrado de juegos:

1. Ve a la página de juegos e indica cuántos aparecen.
2. Aplica un filtro de categoría y confirma que la lista solo muestra juegos de esa categoría.
3. Quita ese filtro, aplica uno de editorial y confirma que la lista solo muestra juegos de esa editorial.
4. Combina un filtro de categoría y uno de editorial y confirma que los resultados respetan ambos.

Describe lo que observas en cada paso e indica si algo no se comporta como se esperaba.
```

Copilot abrirá un navegador mediante el servidor Playwright MCP, seguirá los pasos y te comunicará los resultados. Compara el informe con los criterios de aceptación de la incidencia. Si algo no parece correcto, pide más información o solicita que corrija el código antes de crear una solicitud de incorporación de cambios.

> [!NOTE]
> La aplicación debe estar en ejecución en `http://localhost:4321` para esta prueba. Si has detenido el servidor de desarrollo, vuelve a iniciarlo antes de enviar el mensaje. La primera vez que Copilot utilice Playwright MCP, puede que tenga que descargar un navegador. Si informa de que falta, pídele que ejecute `npx playwright install chromium` y vuelva a intentarlo.

[playwright-mcp-server]: https://github.com/microsoft/playwright-mcp

## Publica la rama y crea una solicitud de incorporación de cambios

Ya has comprobado que la funcionalidad funciona. Ahora crearás una solicitud de incorporación de cambios (PR) para que el equipo la revise. Primero, publicarás la rama `filtering-vscode`.

1. Abre el panel **Source Control** del codespace y revisa los cambios realizados por Copilot.
2. Prepara los cambios seleccionando el icono **+**.
3. Genera un mensaje de commit con el botón **Sparkle**.

   ![Panel Source Control con los cambios realizados](../../../_images/ex3-source-control-changes.png)

4. Selecciona **Publish** para publicar la rama en el repositorio.

## Crea la solicitud de incorporación de cambios

Puedes crear una solicitud de incorporación de cambios en github.com o con la interfaz de línea de comandos de GitHub (CLI). Como ya estás trabajando con GitHub Copilot, puedes pedirle que cree la PR y la vincule a la incidencia pertinente.

1. Abre el panel Copilot Chat y selecciona **New Chat** para iniciar una sesión nueva.
2. En el selector de agentes, confirma que está seleccionado **Agent** para que Copilot pueda utilizar las herramientas de GitHub.
3. Pide a Copilot que cree una PR:

   ```plaintext
   Busca en el repositorio la incidencia relacionada con el filtrado por categoría y editorial. Crea una solicitud de incorporación de cambios para la rama actual y vincúlala a la incidencia correspondiente.
   ```

4. Cuando sea necesario, selecciona **Continue** para permitir que Copilot recopile información y realice las operaciones. La primera vez que utilice una herramienta de GitHub, puede que tengas que autenticarte. Sigue las indicaciones para autorizarlo.
5. Observa cómo Copilot busca entre las incidencias, encuentra la correcta y crea la PR.
6. Selecciona el enlace que genera Copilot para revisar la solicitud, pero **no la integres todavía**.

## Resumen y pasos siguientes

En este ejercicio:

- Has aprendido qué es MCP y cómo amplían los servidores MCP las herramientas disponibles para Copilot.
- Has añadido el servidor Playwright MCP al espacio de trabajo.
- Lo has utilizado para probar manualmente la funcionalidad de filtrado en un navegador antes de publicarla.
- Has publicado la rama y creado una solicitud de incorporación de cambios para el filtrado.

Has utilizado un servidor MCP para *probar* una funcionalidad, pero MCP es solo una de las maneras de ampliar Copilot. A continuación, [crearás un agente personalizado][next-lesson] para agilizar tareas específicas, como las revisiones de accesibilidad.

## Recursos

- [¿Qué es MCP y por qué habla todo el mundo de él?][mcp-blog-post]
- [Servidor Microsoft Playwright MCP][playwright-mcp-server]
- [Servidor MCP de GitHub][github-mcp-server]
- [Registro de MCP de GitHub][mcp-registry]
- [Servidores MCP en VS Code][vscode-mcp-config]

[previous-lesson]: ../2-agent-mode/
[next-lesson]: ../4-custom-agents/
[mcp-blog-post]: https://github.blog/ai-and-ml/llms/what-the-heck-is-mcp-and-why-is-everyone-talking-about-it/
[github-mcp-server]: https://github.com/github/github-mcp-server
[mcp-registry]: https://github.com/mcp
[remote-github-mcp-server]: https://github.blog/changelog/2025-06-12-remote-github-mcp-server-is-now-available-in-public-preview/
[vscode-mcp-config]: https://code.visualstudio.com/docs/agents/reference/mcp-configuration
