---
title: "Ejercicio 5: Supervisar y gestionar agentes"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

| [← Lección anterior: Agentes personalizados][previous-lesson] |
|:--|

En el modo agente, GitHub Copilot trabaja de forma autónoma: explora el código, propone cambios, edita archivos y ejecuta comandos. Como trabaja en el equipo en tiempo real, Copilot Chat en VS Code muestra las llamadas a herramientas y las ediciones de archivos a medida que ocurren. Puedes revisar las diferencias, aceptar o rechazar cambios y orientar la conversación con mensajes de seguimiento sin salir del editor.

En este ejercicio:

- Supervisarás en tiempo real el trabajo del agente de accesibilidad.
- Revisarás y aceptarás las ediciones propuestas.
- Orientarás la sesión para añadir un selector de modo claro junto al modo de alto contraste.

## Escenario

El agente personalizado de accesibilidad del [ejercicio 4][previous-lesson] está implementando el modo de alto contraste. Mientras trabaja, el equipo de diseño solicita también un selector de modo claro para los usuarios a quienes les resulta demasiado oscuro el tema predeterminado. En lugar de iniciar una conversación desde cero, orientarás la sesión existente para ampliar el trabajo.

## Supervisa el progreso de Copilot

La vista Copilot Chat muestra cada paso del agente: los archivos que explora, los comandos que ejecuta y las ediciones que propone. Cada cambio aparece en el chat con las diferencias y los controles **Keep** y **Undo**.

1. Vuelve a la vista Copilot Chat del ejercicio 4.
2. Mientras trabaja el agente, desplázate por el chat para ver las llamadas a herramientas. Aparecerán lecturas y ediciones de archivos, además de los comandos de terminal que solicite ejecutar.
3. Cuando el agente proponga una edición, aparecerán las diferencias en el chat:
   - Selecciona **Keep** para aceptar el cambio.
   - Selecciona **Undo** para deshacerlo y permitir que el agente lo intente de nuevo.
4. También puedes abrir el indicador **Files changed** de la parte superior del chat para consultar todos los archivos que el agente ha modificado durante la sesión.

> [!NOTE]
> Si una llamada a una herramienta requiere permiso, por ejemplo para ejecutar un comando de terminal, el agente se detendrá y mostrará una solicitud **Allow**. Aprueba solo los comandos que consideres seguros.

5. Espera a que el agente termine de implementar el modo de alto contraste. Debería mostrar un mensaje final con un resumen de los cambios.

## Pide al agente que añada el modo claro

Ahora que está implementado el modo de alto contraste, ampliarás la misma conversación para añadir un selector de modo claro. Como continúas en la misma sesión, el agente conserva el contexto: los componentes que ha modificado, el enfoque de estilo y el patrón de almacenamiento local.

1. Envía este mensaje de seguimiento en el campo de entrada de Copilot Chat:

    ```plaintext
    Buen trabajo. Ahora añade un selector de modo claro junto al selector de alto contraste. El modo claro debe seguir el mismo patrón: conservarse en el almacenamiento local y estar disponible en la misma zona de la interfaz. Los usuarios deben poder activar el alto contraste y el modo claro de forma independiente.
    ```

2. El agente retomará el trabajo, revisará los cambios que ya ha realizado y propondrá cambios para añadir el modo claro.
3. Revisa cada nueva edición cuando aparezca, como hiciste con el modo de alto contraste. Utiliza **Keep** o **Undo** para cada diferencia.
4. Si el agente sigue un enfoque que no quieres, por ejemplo, si intenta reorganizar la interfaz de los selectores, detenlo con el botón **Stop** junto al campo de entrada y envía un mensaje aclaratorio.

> [!TIP]
> Orientar una sesión en curso es más rápido que empezar de nuevo. Utiliza mensajes de seguimiento para pedir ajustes («simplifica el CSS: utiliza variables CSS en lugar de duplicar selectores»), corregir el enfoque («no añadas un tercer selector; integra el modo claro en el panel de configuración existente») o ampliar el alcance («añade también métodos abreviados de teclado para ambos selectores»).

## Revisa los cambios

Antes de confirmar el trabajo, revisa brevemente todos los archivos que ha modificado el agente.

1. Abre la vista **Source Control** de VS Code.
2. Revisa la lista completa de archivos modificados. Deberías ver cambios en componentes Astro, estilos y pruebas relacionadas.
3. Abre algunos archivos modificados y revisa las diferencias. Confirma que se apliquen los patrones de accesibilidad del agente: atributos ARIA, navegación mediante teclado, HTML semántico y persistencia en el almacenamiento local.
4. Cuando estés conforme, prepara y confirma los cambios desde el panel Source Control. Los publicarás en [la siguiente lección][next-lesson].

## Resumen y pasos siguientes

Has utilizado el modo agente de Copilot Chat para supervisar y orientar una sesión en curso: has revisado cada edición, aceptado o rechazado cambios y enviado mensajes de seguimiento para ampliar el trabajo sin perder el contexto.

En este ejercicio:

- Has supervisado el trabajo del agente en tiempo real.
- Has aceptado y rechazado ediciones de archivos.
- Has orientado una sesión en curso con mensajes de seguimiento.

En la [siguiente lección][next-lesson], publicarás el trabajo de accesibilidad en una solicitud de incorporación de cambios y revisarás los cambios generados por el agente personalizado local.

## Recursos

- [Copilot Chat en VS Code][copilot-chat-vscode]
- [Uso del modo agente][agent-mode]

---

| [← Lección anterior: Agentes personalizados][previous-lesson] | [Siguiente lección: Iterar sobre el trabajo de Copilot →][next-lesson] |
|:--|--:|

[previous-lesson]: ../4-custom-agents/
[next-lesson]: ../6-iterating/
[copilot-chat-vscode]: https://code.visualstudio.com/docs/copilot/chat/copilot-chat
[agent-mode]: https://code.visualstudio.com/docs/copilot/chat/chat-agent-mode
