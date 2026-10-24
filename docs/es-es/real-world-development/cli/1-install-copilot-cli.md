---
title: "Lección 1: Instalar GitHub Copilot CLI"
description: "Instala y autentica Copilot CLI en tu codespace, familiarízate con el entorno y localiza la incidencia de filtrado."
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

[GitHub Copilot CLI][about-copilot-cli] es un potente asistente de programación agéntico que se ejecuta en el terminal. Te permite explorar bases de código, generar código, ejecutar comandos e interactuar con herramientas externas, todo desde la línea de comandos. Puedes delegar tareas, solicitar cambios y mantener la concentración. El primer paso es instalar la herramienta, algo que puedes hacer con herramientas que ya conoces.

En esta lección:

- Instalarás GitHub Copilot CLI con npm.
- Te autenticarás con tu cuenta de GitHub.
- Confiarás en el repositorio del taller y probarás una conversación breve.
- Localizarás la incidencia de filtrado mediante el servidor GitHub MCP integrado.

## Escenario

Tu equipo empieza a utilizar agentes de IA para gestionar un backlog cada vez mayor. Copilot CLI incorpora esa capacidad al terminal, donde muchos desarrolladores ya trabajan. En esta lección lo instalarás y autenticarás para poder utilizarlo durante el resto del taller.

## Instala Copilot CLI

Puedes instalar Copilot CLI con [npm][install-cli], WinGet o Homebrew. GitHub Codespaces ya incluye Node.js, así que utilizarás npm.

1. Vuelve al codespace y abre un terminal.
2. Comprueba que Node.js está instalado y cumple el requisito de versión:

   ```bash
   node --version
   ```

   Deberías ver la versión 24 o posterior.

3. Instala Copilot CLI de forma global:

   ```bash
   npm install -g @github/copilot
   ```

4. Comprueba la instalación:

   ```bash
   copilot --version
   ```

   Deberías ver el número de versión.

## Autentícate con GitHub

La primera vez que inicies Copilot CLI, te pedirá que te autentiques con tu cuenta de GitHub.

1. Inicia Copilot CLI:

   ```bash
   copilot
   ```

2. Si se te solicita, sigue las instrucciones de autenticación mediante código de dispositivo y autoriza Copilot CLI.
3. Copilot CLI muestra este mensaje:

   ```plaintext
   Copilot can read files in this folder and, with your permission, edit them or run code and shell commands. It will remember your permissions for the rest of this session.

   Do you trust the files in this folder?
   ```

4. Comprueba que la ruta corresponde al repositorio Tailspin Toys y responde que sí seleccionando **Yes, and remember this folder for future sessions**.

> [!NOTE]
> Es posible que ya estés autenticado mediante tu sesión de GitHub en el codespace. Si Copilot CLI se inicia sin pedirte que te autentiques, ya está listo.

## Familiarízate con el entorno

Los comandos que escribas en el terminal normal se ejecutan directamente en el codespace. Una vez iniciado Copilot CLI, el lenguaje natural se envía al agente y los comandos de barra controlan la conversación.

1. Introduce `/model`, utiliza las teclas de flecha para seleccionar **Auto**, pulsa <kbd>Enter</kbd> y, después, vuelve a pulsar <kbd>Enter</kbd> para confirmar.
2. Introduce `/help` para consultar los comandos disponibles en la versión instalada y pulsa <kbd>Esc</kbd> para cerrar la ayuda.
3. Haz una pregunta sencilla a Copilot para comprobar que todo funciona:

   ```plaintext
   ¿Cuáles son los archivos principales de este proyecto?
   ```

4. Lee la respuesta y observa cómo Copilot explora el repositorio antes de contestar.
5. Introduce `/mcp list` y confirma que está disponible el servidor GitHub MCP integrado.
6. Pide a Copilot que localice la incidencia de filtrado:

   ```plaintext
   Utiliza GitHub MCP para buscar en este repositorio la incidencia titulada "Allow users to filter games by category and publisher". Indícame su URL y un breve resumen. No hagas ningún cambio.
   ```

7. Abre la URL y lee la incidencia. La utilizarás después de realizar un primer cambio rápido.

> [!TIP]
> Una sesión normal de Copilot CLI trabaja en la rama seleccionada en el terminal; no crea automáticamente un árbol de trabajo. Crearás una rama de funcionalidad antes de cada cambio.

## Utiliza el atajo del taller

Normalmente, Copilot CLI pide permiso antes de utilizar herramientas fuera de los permisos establecidos. En este taller, lo volverás a iniciar con `--yolo`, un atajo que has autorizado para eliminar esas solicitudes de aprobación dentro del codespace y centrarte en los ejercicios.

> [!CAUTION]
> `--yolo` habilita permisos automáticos completos (`--allow-all-tools`, `--allow-all-paths` y `--allow-all-urls`). Utilízalo solo en un entorno aislado, como un codespace o una máquina virtual (VM), y nunca lo configures como alias predeterminado para el desarrollo cotidiano. Consulta [Permitir y denegar el uso de herramientas][allow-all-warning] para obtener más información.

En este taller, `--enable-all-github-mcp-tools` habilita las herramientas de lectura y escritura de GitHub MCP que utilizarás en lecciones posteriores para trabajar con incidencias y solicitudes de incorporación de cambios. El codespace limita el acceso al equipo local, pero los recursos de GitHub autenticados siguen siendo reales. Revisa los cambios antes de publicarlos o integrarlos.

1. Sal de Copilot CLI con `/exit`.
2. Vuelve a iniciarlo desde la raíz del repositorio:

   ```bash
   copilot --yolo --enable-all-github-mcp-tools
   ```

3. Haz otra pregunta breve sobre el proyecto para comprobar que la conversación funciona y, después, sal con `/exit`.

Copilot guarda las conversaciones automáticamente. Más adelante, después de cambiar las instrucciones o añadir un agente, utilizarás `copilot --resume` para volver a la misma conversación y rama de funcionalidad.

## Resumen y pasos siguientes

Has instalado GitHub Copilot CLI y te has autenticado. En concreto:

- Has instalado GitHub Copilot CLI con npm.
- Te has autenticado con tu cuenta de GitHub.
- Has confiado en el repositorio del taller y has probado una conversación breve.
- Has localizado la incidencia de filtrado mediante el servidor GitHub MCP integrado.

A continuación, [realizarás tu primer cambio específico][next-lesson] y utilizarás Copilot CLI para mostrar una valoración por estrellas en las tarjetas de juegos.

## Recursos

- [Instalar GitHub Copilot CLI][install-cli]
- [Acerca de GitHub Copilot CLI][about-copilot-cli]
- [Referencia de comandos de Copilot CLI][cli-reference]

[previous-lesson]: ../0-prerequisites/
[next-lesson]: ../2-add-star-rating/
[install-cli]: https://docs.github.com/copilot/how-tos/copilot-cli/set-up-copilot-cli/install-copilot-cli
[about-copilot-cli]: https://docs.github.com/copilot/concepts/agents/about-copilot-cli
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
[allow-all-warning]: https://docs.github.com/copilot/concepts/agents/about-copilot-cli#allowing-and-denying-tool-use
