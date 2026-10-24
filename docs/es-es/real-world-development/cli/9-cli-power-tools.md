---
title: "Lección 9: Comandos de barra de GitHub Copilot CLI"
description: "Explora los comandos de barra para gestionar el contexto, seleccionar modelos, compartir sesiones y delegar trabajo opcionalmente al agente en la nube."
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

Como muchas otras herramientas de CLI, GitHub Copilot CLI incluye numerosos comandos de barra. Permiten acceder a funciones avanzadas, consultar información interna y cambiar opciones de configuración. Ya has utilizado comandos como `/diff`, `/mcp`, `/skills`, `/agent` y `/pr`. Ahora explorarás otros comandos útiles.

En esta lección:

- Utilizarás `/context` y `/compact` para explorar cómo gestiona Copilot el contexto de la conversación.
- Utilizarás `/model` para explorar los modelos disponibles.
- Aprenderás cómo `/share` permite exportar o compartir una sesión.
- Explorarás comandos opcionales para trabajar en paralelo, crear árboles de trabajo y delegar tareas al agente en la nube.

## Escenario

Ya has completado el flujo de trabajo principal de CLI. Ahora explorarás otras capacidades: gestionar el contexto, cambiar de modelo, compartir sesiones y delegar tareas opcionalmente al [agente en la nube de Copilot][about-cloud-agent].

## Explora el contexto de Copilot CLI

Al trabajar en tareas grandes o complejas, puede que alcances el límite de contexto del modelo. Copilot CLI compacta automáticamente la conversación cuando es necesario, pero también puedes inspeccionar o compactar el contexto mediante comandos de barra.

1. Vuelve al codespace e inicia Copilot CLI desde la raíz del repositorio si todavía no está abierto.
2. Introduce:

   ```plaintext
   /context
   ```

3. Observa el modelo, el uso actual de tokens y cómo se distribuye el contexto entre las instrucciones del sistema, las herramientas, los mensajes y el espacio libre.
4. Compacta la conversación:

   ```plaintext
   /compact
   ```

5. Vuelve a introducir `/context` y compara el resultado. Si la conversación ya era breve, puede que no haya cambiado mucho.

> [!NOTE]
> Copilot CLI compacta automáticamente el contexto a medida que se llena la ventana. Utiliza `/compact` para elegir cuándo hacerlo. Usa `/clear` o `/new` al cambiar a una tarea no relacionada y empezar una conversación nueva.

## Elige un modelo

Los modelos tienen distintas capacidades y cada desarrollador puede tener preferencias diferentes. Copilot CLI permite ver los modelos disponibles y seleccionar uno.

1. Introduce:

   ```plaintext
   /model
   ```

2. Explora los modelos disponibles y la información sobre su uso.
3. Mantén el modelo actual, selecciona otro o pulsa <kbd>Esc</kbd> para cerrar la lista.

## Comparte una sesión

Compartir lo aprendido ayuda al equipo a mejorar el uso de las herramientas de inteligencia artificial (IA). El comando `/share` puede exportar una sesión a un archivo Markdown o de lenguaje de marcado de hipertexto (HTML), crear un enlace para compartirla o publicar un gist de GitHub.

1. Introduce `/help` y revisa las opciones de `/share` en la versión instalada.
2. Si quieres compartir la sesión, elige el destino que mejor se adapte a tus necesidades, por ejemplo, `/share file` para exportarla a un archivo Markdown local.
3. Revisa el contenido exportado antes de enviarlo o publicarlo. Las exportaciones pueden incluir mensajes, respuestas e información del proyecto.

Publicar un enlace o un gist es opcional. No publiques contenido del repositorio ni de la conversación que el equipo no haya decidido compartir.

## Opcional: ampliar el trabajo o delegarlo

Ya has completado el taller principal. Copilot CLI también ofrece comandos para tareas mayores:

- `/fleet` puede repartir tareas independientes entre subagentes y ejecutarlas en paralelo.
- `/worktree` puede crear un árbol de trabajo de Git aislado para otra tarea.
- `/delegate` puede enviar una tarea al agente en la nube de Copilot, que trabaja de forma asíncrona y puede crear una solicitud de incorporación de cambios.

Estos comandos son opcionales porque pueden crear árboles de trabajo o tareas remotas adicionales. Antes de probarlos, inicia una tarea nueva y acotada y revisa el resultado con el flujo de trabajo habitual. Para profundizar en el trabajo con agentes asíncronos, continúa con el [taller del agente en la nube][cloud-workshop].

## Resumen y pasos siguientes

Los comandos de barra de Copilot CLI permiten configurar la herramienta, compartir sesiones y consultar qué ocurre en segundo plano. En esta lección:

- Has utilizado `/context` y `/compact` para explorar cómo gestiona Copilot el contexto.
- Has utilizado `/model` para explorar los modelos disponibles.
- Has aprendido cómo `/share` permite exportar o compartir una sesión.
- Has explorado comandos opcionales para trabajar en paralelo, crear árboles de trabajo y delegar tareas al agente en la nube.

Copilot CLI incluye más comandos de barra que puedes explorar. Para cerrar el recorrido, [repasarás lo aprendido][next-lesson] y los siguientes pasos.

## Recursos

- [Referencia de comandos de Copilot CLI][cli-reference]
- [Gestión del contexto en Copilot CLI][context-management]
- [Acerca del agente en la nube de Copilot][about-cloud-agent]

[previous-lesson]: ../8-create-pull-request/
[next-lesson]: ../10-review/
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
[context-management]: https://docs.github.com/copilot/concepts/agents/copilot-cli/context-management
[about-cloud-agent]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[cloud-workshop]: ../../cloud/
