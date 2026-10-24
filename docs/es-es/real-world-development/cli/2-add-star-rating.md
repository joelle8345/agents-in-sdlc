---
title: "Lección 2: Añadir valoraciones por estrellas, una mejora rápida"
description: "Utiliza Copilot CLI para hacer un pequeño cambio en las tarjetas de juegos, revísalo en un navegador reenviado e intégralo en tu primera solicitud de incorporación de cambios."
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

Ya has instalado Copilot CLI y probado una conversación. Ahora realizarás tu primer cambio en el proyecto. Será pequeño: los datos de los juegos ya incluyen una valoración por estrellas, pero las tarjetas de la página principal todavía no la muestran. Pedirás al agente que la muestre, revisarás el cambio y lo integrarás en tu primera solicitud de incorporación de cambios.

En esta lección:

- Iniciarás una conversación específica de Copilot en una rama de funcionalidad.
- Pedirás al agente que realice un pequeño cambio en el proyecto.
- Revisarás el cambio con `/diff`.
- Ejecutarás la aplicación y comprobarás el cambio en un navegador reenviado.
- Crearás e integrarás tu primera solicitud de incorporación de cambios.

## Escenario

Cada juego de Tailspin Toys puede tener una valoración por estrellas, que ya aparece en la página de detalles del juego. Sin embargo, las tarjetas de la página principal solo muestran el título, la categoría, la editorial y la descripción. Como ejercicio inicial, pedirás al agente que muestre en cada tarjeta la valoración existente. Es un cambio pequeño e independiente, ideal para tu primera sesión.

## Partes de una conversación

Una **conversación** es el espacio donde trabajas con Copilot CLI en una tarea. A diferencia de la aplicación Copilot, una conversación normal de CLI utiliza el repositorio y la rama de Git seleccionados en el terminal, en lugar de crear un árbol de trabajo dedicado. Las conversaciones guardadas te permiten volver al mismo diálogo, mientras que los archivos y la rama siguen siendo el estado habitual de Git en el disco.

En una conversación verás tus mensajes y las respuestas del agente, la actividad de las herramientas que utiliza para explorar y editar archivos, y los cambios que puedes inspeccionar con `/diff`.

## Inicia una conversación y solicita el cambio

Inicia una conversación nueva para empezar a implementar la funcionalidad.

1. Vuelve al codespace.
2. Si el terminal no está abierto, pulsa <kbd>Control</kbd>+<kbd>\`</kbd> (Mac) o <kbd>Ctrl</kbd>+<kbd>\`</kbd> (Windows/Linux).
3. Si Copilot CLI todavía no está abierto, ejecuta este comando:

   ```bash
   copilot --yolo
   ```

4. Inicia una sesión nueva con el comando de barra `/new` y pulsa <kbd>Enter</kbd>.
5. Envía este mensaje para solicitar el cambio:

   ```plaintext
   Muestra en las tarjetas de juegos de la página de lista la propiedad starRating de cada juego sobre 5. Si la valoración es null, muestra "No rating yet". Mantén el diseño de las tarjetas, añade pruebas y ejecuta las comprobaciones pertinentes.
   ```

Copilot explorará el proyecto, localizará los archivos que muestran los detalles de los juegos y creará el código necesario. Ya has añadido una funcionalidad con Copilot CLI.

## Revisa las diferencias

Revisa todos los cambios generados por IA antes de integrarlos, por pequeños que sean. Inspecciónalos directamente en Copilot CLI.

1. Introduce `/diff` y revisa todos los archivos modificados.
2. Confirma que la tarjeta del juego muestra la valoración numérica cuando existe y `No rating yet` cuando `starRating` es `null`.
3. Confirma que las pruebas cubren ambos casos.
4. Revisa los resultados de las comprobaciones ejecutadas por Copilot y pídele que corrija los fallos.
5. Cuando termines la revisión, pulsa <kbd>Esc</kbd> para salir de la vista de diferencias.

> [!NOTE]
> Como todas las herramientas de inteligencia artificial (IA) generativa, Copilot ofrece resultados probabilísticos, no deterministas. El código exacto puede variar. Revisa el comportamiento en lugar de esperar una implementación concreta.

## Comprueba los cambios

No basta con leer el código y dar por hecho que funciona. Pide a Copilot que inicie el sitio para que puedas examinar la interfaz de usuario (UI) actualizada en el navegador reenviado por Codespaces.

1. Pide a Copilot que inicie la aplicación:

   ```plaintext
   Inicia la aplicación para que pueda revisar en el navegador el cambio de la valoración por estrellas. Indícame la URL y deja el servidor en ejecución.
   ```

2. Cuando Codespaces indique que el puerto `4321` está disponible, selecciona **Open in Browser**.
3. Confirma que las tarjetas de juegos muestran sus valoraciones sobre cinco.
4. Vuelve a Copilot y pídele que detenga el servidor que ha iniciado:

   ```plaintext
   Detén el servidor de desarrollo que has iniciado.
   ```

## Crea e integra tu primera solicitud de incorporación de cambios

Ya has creado la funcionalidad. Ahora crearás una solicitud de incorporación de cambios (PR) para integrar el código nuevo en el proyecto.

1. Pide al agente predeterminado que confirme el cambio:

   ```plaintext
   Confirma los cambios revisados de las valoraciones por estrellas con un mensaje de commit adecuado.
   ```

2. Introduce `/pr create`. Copilot CLI publicará el commit existente al crear la PR y mostrará su URL.
3. Para abrir la PR, mantén pulsada la tecla <kbd>Command</kbd> (Mac) o <kbd>Ctrl</kbd> (Windows/Linux) y selecciona la URL que muestra Copilot CLI.
4. Revisa los archivos modificados y las comprobaciones.
5. Cuando esté todo listo, selecciona **Merge pull request** y confirma la integración.
6. Vuelve al codespace y cierra Copilot CLI con `/exit`.
7. Actualiza la copia local de `main`:

   ```bash
   git checkout main
   git pull
   ```

## Resumen y pasos siguientes

Has publicado tu primer cambio con GitHub Copilot CLI. En concreto:

- Has iniciado una conversación específica de Copilot en una rama de funcionalidad.
- Has indicado al agente que realice un pequeño cambio en las tarjetas de juegos.
- Has revisado el cambio con `/diff`.
- Has ejecutado la aplicación para comprobar la valoración por estrellas en un navegador reenviado.
- Has creado e integrado tu primera solicitud de incorporación de cambios.

A continuación, [partirás de la incidencia de filtrado y utilizarás los modos Plan y Autopilot][next-lesson] para implementar una funcionalidad mayor.

## Recursos

- [Acerca de GitHub Copilot CLI][about-copilot-cli]
- [Referencia de comandos de Copilot CLI][cli-reference]

[previous-lesson]: ../1-install-copilot-cli/
[next-lesson]: ../3-agent-modes/
[about-copilot-cli]: https://docs.github.com/copilot/concepts/agents/about-copilot-cli
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
