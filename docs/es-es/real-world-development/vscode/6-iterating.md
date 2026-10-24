---
title: "Ejercicio 6: Iterar sobre el trabajo de GitHub Copilot"
authors:
  - geektrainer
lastUpdated: 2026-06-30
next: false
---

| [← Lección anterior: Supervisar y gestionar agentes][previous-lesson] |
| :-- |

## Revisa el trabajo

Durante este taller has trabajado con GitHub Copilot en varias tareas para mejorar la experiencia de usuario. Has utilizado el modo agente para añadir filtros en el cliente y el servidor, el servidor Playwright MCP para probar manualmente esa funcionalidad en un navegador y, después, un agente personalizado para implementar funciones de accesibilidad, como los modos de alto contraste y claro. También has orientado la sesión en curso para ampliar el trabajo. Ahora publicarás los cambios locales y los revisarás como lo haría tu equipo.

### Escenario

Los fundamentos del diseño de software y DevOps no cambian por añadir inteligencia artificial generativa. Es necesario revisar los cambios que produce Copilot. En este ejercicio publicarás desde el codespace los cambios de accesibilidad, crearás una solicitud de incorporación de cambios y revisarás las diferencias antes de involucrar al resto del equipo.

## Publica las funcionalidades de accesibilidad

Los selectores de los modos de alto contraste y claro que has implementado con el agente personalizado de accesibilidad en el [ejercicio 4][exercise-4] y el [ejercicio 5][exercise-5] están en el codespace como cambios confirmados. Los publicarás en una rama y crearás una solicitud de incorporación de cambios para que el equipo pueda revisarlos.

1. Vuelve al codespace.
2. Abre la vista **Source Control** de VS Code.
3. Confirma que los cambios de accesibilidad están confirmados. Si quedan cambios sin confirmar del ejercicio 5, prepáralos y confírmalos con un mensaje descriptivo, como `Add high-contrast and light-mode toggles`.
4. Publica la rama seleccionando **Publish Branch** o seleccionando **...** y, después, **Push**.
5. VS Code te ofrecerá abrir la nueva rama en github.com. Acepta la propuesta o ve al repositorio y selecciona **Compare & pull request** en el aviso de la rama.
6. Escribe un título claro, por ejemplo, `Add high-contrast and light-mode toggles`, y una descripción breve que resuma qué has hecho y por qué.
7. Selecciona **Create pull request**.
8. Cuando se abra la PR, selecciona **Files changed** y revisa todo el trabajo. Presta atención a:
   - Los componentes de la interfaz que permiten cambiar de modo.
   - El uso del almacenamiento local para conservar las preferencias.
   - Los cambios de CSS o de estilo para los modos de alto contraste y claro.
   - Los atributos de accesibilidad, como las etiquetas ARIA y la navegación mediante teclado.
   - El código JavaScript o TypeScript que gestiona el cambio de modo.

9. Vuelve a la pestaña **Conversation**.
10. Si hay flujos de trabajo pendientes de aprobación, selecciona **Approve and run workflows**.

    ![Aprobar y ejecutar flujos de trabajo](../../../_images/shared-approve-workflows.png)

11. Espera a que terminen los flujos de trabajo. Si todo va bien, deberían completarse correctamente.

> [!TIP]
> ¿Quieres una segunda opinión sobre el trabajo de accesibilidad? Menciona a `@copilot` en un comentario de la PR y pídele, por ejemplo, que revise posibles problemas adicionales de WCAG o sugiera mejoras para la navegación mediante teclado. Copilot iniciará una sesión nueva para atender el comentario.

## Ejercicio opcional: sigue explorando localmente

Trabajar de forma iterativa con un agente en el IDE es una habilidad que se adquiere con la práctica. Puedes probar estas ideas en otras sesiones de VS Code:

- Añadir un formulario para que los usuarios expresen su interés en un juego en la página de detalles.
- Implementar la paginación de la lista de juegos.
- Añadir validación de entradas y gestión de errores a los métodos de acceso a datos de `src/lib/`.
- Ampliar el alcance del agente de accesibilidad, por ejemplo, para auditar el orden del foco del teclado en todo el sitio.

## Resumen

Has completado el recorrido de VS Code. En este taller:

- **Has utilizado Playwright MCP para probar manualmente la funcionalidad.** Has añadido el servidor Playwright MCP y has dejado que Copilot controle un navegador para verificar el filtrado antes de crear una solicitud de incorporación de cambios.
- **Has utilizado el modo agente para coordinar cambios en varias capas.** Has añadido una funcionalidad de filtrado que afecta al cliente, al servidor y a las pruebas en una sola sesión.
- **Has utilizado un agente personalizado.** Has seleccionado el agente de accesibilidad en el selector y has observado cómo implementaba el modo de alto contraste en el repositorio.
- **Has gestionado y orientado una sesión de agente.** Has revisado los cambios propuestos en el editor, aceptado los que querías y ampliado la sesión con una solicitud para añadir el modo claro.
- **Has completado el flujo con una solicitud de incorporación de cambios.** Has publicado el trabajo local y lo has revisado de principio a fin como lo haría el equipo.

## Repaso y pasos siguientes

Aquí termina el recorrido obligatorio de VS Code. Puedes detenerte aquí: ya has completado el taller.

Si quieres ampliar tus conocimientos sobre las capacidades de los agentes de Copilot, los otros recorridos presentan escenarios relacionados en distintas interfaces:

- 💻 **[Recorrido de CLI](../../cli/)**: entrega dos cambios revisados desde el terminal con los modos Plan y Autopilot, habilidades, un agente personalizado de QA, Playwright MCP, Agent Merge y transferencias con contexto.
- ☁️ **[Recorrido del agente en la nube](../../cloud/)**: asigna incidencias al agente en la nube, supervisa sesiones desde la página de agentes e itera de forma asíncrona sobre solicitudes de incorporación de cambios.

También puedes seguir ampliando el proyecto. [awesome-copilot][awesome-copilot] incluye más archivos de instrucciones, agentes personalizados y habilidades que puedes adaptar a tus propios proyectos.

Como ampliación opcional, [Opcional: Incorporar Foundry][exercise-7] utiliza VS Code y Microsoft Foundry Toolkit para preparar un modelo, implementar Backer Concierge y conectarlo al sitio.

## Recursos

- [GitHub Copilot][github-copilot]
- [Copilot Chat en VS Code][copilot-chat-vscode]
- [Uso del modo agente][agent-mode]

---

| [← Lección anterior: Gestionar agentes][previous-lesson] |
|:--|

[previous-lesson]: ../5-managing-agents/
[exercise-4]: ../4-custom-agents/
[exercise-5]: ../5-managing-agents/
[exercise-7]: ../7-foundry-toolkit/
[github-copilot]: https://github.com/features/copilot
[copilot-chat-vscode]: https://code.visualstudio.com/docs/copilot/chat/copilot-chat
[agent-mode]: https://code.visualstudio.com/docs/copilot/chat/chat-agent-mode
[awesome-copilot]: https://github.com/github/awesome-copilot
