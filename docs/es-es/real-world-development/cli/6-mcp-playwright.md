---
title: "Lección 6: Validar la funcionalidad con Playwright MCP"
description: "Inspecciona o configura Playwright MCP en Copilot CLI y utilízalo para explorar la funcionalidad de filtrado en un navegador."
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

Como ya has visto, desarrollar código implica algo más que escribirlo. También hay que trabajar con datos y servicios externos y proporcionar a Copilot automatizaciones adicionales. Para ello se utilizan los servidores del Model Context Protocol (MCP). Los servidores MCP amplían las funciones integradas en Copilot CLI con más herramientas y servicios.

En esta lección:

- Aprenderás qué es MCP y cómo lo utiliza Copilot CLI.
- Añadirás el servidor Playwright MCP si todavía no está disponible.
- Pedirás al agente que controle un navegador y explore la funcionalidad de filtrado.

## Escenario

Las pruebas unitarias y de extremo a extremo son importantes, pero para validar los cambios de la interfaz de usuario hay que interactuar con ella. Quieres que Copilot utilice el sitio web como lo haría un usuario y automatice más comprobaciones para tener mayor confianza en que los cambios funcionan como se espera.

## ¿Qué es el Model Context Protocol (MCP)?

El [Model Context Protocol (MCP)][mcp-blog-post] permite que los agentes de inteligencia artificial (IA) se comuniquen con herramientas y servicios externos en tiempo real. De este modo, pueden acceder a información actualizada y realizar acciones en tu nombre.

Los agentes acceden a estas herramientas y recursos mediante servidores MCP, que actúan como puente entre el agente y las herramientas y servicios externos. Cada servidor proporciona un conjunto distinto de herramientas y recursos.

Algunos servidores MCP conocidos:

- **[Servidor MCP de GitHub][github-mcp]**: proporciona acceso a las interfaces de programación de aplicaciones (API) para gestionar repositorios, incidencias y solicitudes de incorporación de cambios de GitHub.
- **[Servidor Playwright MCP][playwright-mcp-server]**: ofrece funciones de automatización del navegador mediante Playwright.

Hay muchos otros servidores MCP. GitHub aloja un [registro de MCP][mcp-registry] para facilitar su descubrimiento y las contribuciones al ecosistema.

> [!CAUTION]
> Trata los servidores MCP como cualquier otra dependencia del proyecto. Antes de utilizar uno, revisa su código fuente, comprueba quién lo publica y considera las implicaciones de seguridad.

## Añade el servidor Playwright MCP

Si el servidor Playwright MCP todavía no está disponible, añádelo para que Copilot pueda interactuar con el sitio web como lo haría un usuario.

> [!NOTE]
> Si Playwright MCP ya está configurado en Copilot CLI, omite estos pasos de configuración y continúa con la sección siguiente.

1. Vuelve al codespace.
2. En Copilot CLI, introduce este comando para abrir el cuadro de diálogo de incorporación de servidores MCP:

   ```plaintext
   /mcp add
   ```

3. Escribe `playwright` como nombre y pulsa <kbd>Tab</kbd>.
4. Confirma que el tipo de servidor es **STDIO** pulsando <kbd>Enter</kbd> y, después, pulsa <kbd>Tab</kbd>.
5. Pega este comando en el cuadro **Command**:

   ```plaintext
   npx -y @playwright/mcp@latest --headless --no-sandbox
   ```

6. Pulsa <kbd>Control</kbd>+<kbd>S</kbd> (Mac) o <kbd>Ctrl</kbd>+<kbd>S</kbd> (Windows/Linux) para guardar el servidor MCP.
7. Pulsa <kbd>Esc</kbd> para salir del cuadro de diálogo de MCP.

## Pide a Copilot que explore la funcionalidad con Playwright

Ya has comprobado manualmente que la funcionalidad se comporta como esperas. Ahora pedirás a Copilot que haga lo mismo mediante el servidor Playwright MCP.

1. Envía este mensaje para pedirle a Copilot que utilice Playwright MCP y valide la funcionalidad:

   ```plaintext
   Inicia la aplicación y utiliza Playwright MCP para comprobar el filtrado según la incidencia y el plan acordado. Indícame qué funciona y qué no, sin hacer cambios. Cuando termines, detén el servidor que has iniciado.
   ```

> [!NOTE]
> No hace falta que indiques a Copilot que utilice el servidor MCP, ya que normalmente lo detectará por sí solo. Sin embargo, como sabes qué herramienta debe utilizar, puedes especificarla para obtener resultados más coherentes y ahorrar tokens.

2. Observa cómo Copilot describe los distintos pasos que realiza en el navegador para comprobar la funcionalidad.
3. Lee el informe y confirma que todo se comporta como se espera.

Copilot iniciará el servidor, utilizará Playwright para interactuar con el sitio web, detendrá el servidor y te proporcionará un informe.

## Resumen y pasos siguientes

Has utilizado el servidor Playwright MCP para explorar la funcionalidad en un navegador real desde Copilot CLI. En esta lección:

- Has aprendido qué es MCP y cómo lo utiliza Copilot CLI.
- Has añadido el servidor Playwright MCP si todavía no estaba disponible.
- Has pedido al agente que controle un navegador y explore la funcionalidad de filtrado.

A continuación, [crearás un agente personalizado de control de calidad (QA)][next-lesson] que combinará la habilidad y las herramientas del navegador en un perfil especializado.

## Recursos

- [¿Qué es MCP y por qué habla todo el mundo de él?][mcp-blog-post]
- [Servidor Microsoft Playwright MCP][playwright-mcp-server]
- [Añadir servidores MCP a Copilot CLI][add-mcp]

[previous-lesson]: ../5-agent-skills/
[next-lesson]: ../7-qa-agent/
[mcp-blog-post]: https://github.blog/ai-and-ml/llms/what-the-heck-is-mcp-and-why-is-everyone-talking-about-it/
[playwright-mcp-server]: https://github.com/microsoft/playwright-mcp
[github-mcp]: https://github.com/github/github-mcp-server
[mcp-registry]: https://github.com/mcp
[add-mcp]: https://docs.github.com/copilot/how-tos/copilot-cli/customize-copilot/add-mcp-servers
