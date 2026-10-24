---
title: "Ejercicio 4: Supervisar y gestionar agentes"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

En los últimos ejercicios has asignado al agente en la nube de Copilot tres tareas distintas para mejorar la experiencia de usuario y añadir funcionalidades. Aunque el agente trabaja de forma asíncrona y autónoma, sigue siendo importante supervisar esas tareas.

Puedes gestionar las tareas asignadas al agente en la nube con distintas herramientas, como la [página de agentes][agents-page] de GitHub.com. Desde este panel puedes ver todas las tareas de los agentes que tienen solicitudes de incorporación de cambios (PR) abiertas, consultar las operaciones realizadas y orientar una sesión en curso.

En esta lección:

- Explorarás la página de agentes para supervisar las tareas del agente en la nube.
- Orientarás una sesión en curso para solicitar una funcionalidad adicional.

## Escenario

Después de asignar al agente la creación de un modo de alto contraste, el equipo decidió que también sería un buen momento para añadir un modo claro. Como ya se estaba trabajando en el estilo del sitio y en la funcionalidad para cambiar de modo, parecía lógico incluirlo. Orientarás el trabajo del agente para que añada el modo claro además del modo de alto contraste.

## Revisa las tareas del agente en la nube de Copilot

Comprueba el estado de todas las tareas asignadas al agente en la nube de Copilot.

1. Ve a la [página de agentes de Copilot](https://github.com/copilot/agents).
2. Revisa la lista de tareas en el panel principal y en el panel izquierdo. Deberías ver las tareas asignadas a Copilot, entre ellas:
   - Actualizar la documentación del código.
   - Generar interfaces de programación de aplicaciones (API) para modificar juegos.
   - Añadir un modo de alto contraste al sitio web.
3. Selecciona una tarea en curso y revisa las operaciones que ha realizado Copilot. Pueden incluir:
   - Obtener el código del repositorio.
   - Crear el entorno de trabajo de Copilot.
   - Configurar servidores del Model Context Protocol (MCP).
   - Realizar los distintos pasos para completar la tarea.

> [!NOTE]
> Los pasos concretos pueden variar según el estado del trabajo de Copilot y el enfoque que haya seguido.

4. Revisa también el panel de la PR, que aparece a la derecha. Desde allí puedes consultar la PR y los archivos modificados.

## Orienta al agente en la nube

Ahora que has revisado las tareas activas, pide a Copilot que añada el selector del modo claro mientras trabaja en el modo de alto contraste.

1. Selecciona la sesión que corresponde al modo de alto contraste. El título exacto depende del nombre que haya elegido Copilot y del estado del trabajo.

    ![Sesión de accesibilidad en el panel de agentes](../../../_images/ex6-accessibility-session.png)

2. Espera unos minutos hasta que la sesión indique que ha terminado de prepararse y ha empezado a trabajar. Lo verás cuando aparezcan mensajes parecidos a los que se muestran a continuación.
3. En el cuadro de diálogo **Steer active session while Copilot is working**, escribe este mensaje:

    ```plaintext
    While we are working on a high contrast mode, let's also add a light mode. There should be a switch for this mode as well where users can select their desired display mode.
    ```

    ![Cuadro de diálogo para orientar una sesión activa del agente en la nube](../../../_images/ex6-steer-cloud-agent-task.png)

4. Pulsa <kbd>Enter</kbd> para enviar el mensaje.
5. Comprueba que Copilot lo reconoce y lo incorpora a su flujo de trabajo.

## Deja que Copilot trabaje

Copilot abordará la tarea actualizada. Incorporará la solicitud nueva al flujo de trabajo cuando termine el paso que estaba realizando cuando enviaste el mensaje.

El proceso tardará varios minutos. Puedes aprovechar este tiempo para repasar lo que has aprendido hasta ahora.

## Resumen y pasos siguientes

Has explorado la página de agentes de Copilot, el centro desde el que se supervisan y orientan las tareas del agente en la nube de GitHub Copilot. Desde el panel puedes seguir las tareas activas y completadas, revisar el trabajo y redirigir una sesión en curso para ajustar su alcance o darle indicaciones.

Has explorado estos conceptos:

- Has utilizado el panel de agentes para supervisar las tareas del agente en la nube.
- Has orientado una sesión en curso para solicitar una funcionalidad adicional.

Mientras Copilot completa las funcionalidades de accesibilidad, a continuación aprenderás a [iterar sobre las solicitudes de incorporación de cambios creadas por Copilot][next-lesson].

## Recursos

- [Página de agentes de Copilot][agents-page]
- [Acerca de los agentes personalizados][custom-agents]

---

| [← Lección anterior: Agentes personalizados][previous-lesson] | [Siguiente lección: Iterar sobre el trabajo de Copilot →][next-lesson] |
|:--|--:|

[previous-lesson]: ../3-custom-agents/
[next-lesson]: ../5-iterating/
[agents-page]: https://github.blog/changelog/2025-07-03-agents-page-for-copilot-coding-agent-in-public-preview
[custom-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
