---
title: "Ejercicio 5: Iterar sobre el trabajo de GitHub Copilot"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

| [← Lección anterior: Gestión de agentes][previous-lesson] |
|:--|

## Revisa el trabajo

Durante este taller, has trabajado con GitHub Copilot en varias tareas para mejorar la experiencia de usuario y añadir funcionalidades. Le has pedido que añada documentación al código, cree una sección de juegos relacionados para el equipo de diseño e implemente funcionalidades de accesibilidad, como los modos de alto contraste y claro. Ahora revisarás los cambios y, si es necesario, darás indicaciones a Copilot para que los mejore.

### Escenario

Los fundamentos del diseño de software y DevOps no cambian por añadir inteligencia artificial generativa. Siempre hay que revisar el código generado y seguir el proceso DevOps habitual. Revisarás las sugerencias de GitHub Copilot para la documentación, los juegos relacionados y las funcionalidades de accesibilidad antes de habilitar la revisión para el resto del equipo.

## Seguridad y agente en la nube de GitHub Copilot

Como el agente en la nube de Copilot realiza tareas de forma asíncrona y sin supervisión, se aplican algunas medidas de seguridad:

- Copilot solo tiene acceso de lectura al repositorio y acceso de escritura **únicamente** a la rama que utilizará para el código.
- El agente se ejecuta en GitHub Actions y crea un entorno aislado y temporal para trabajar.
- Una persona debe aprobar los flujos de trabajo de GitHub Actions antes de que puedan ejecutarse.
- [El acceso a recursos externos está limitado de forma predeterminada](https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-firewall), incluidos los servidores del Model Context Protocol (MCP).

## Revisa la documentación generada

Empieza por revisar la primera solicitud de incorporación de cambios (PR) creada por el agente en la nube de GitHub Copilot: la que añade documentación al código. Utilizarás la interfaz habitual de PR de GitHub.com.

> [!NOTE]
> Al abrir la PR, puede que veas un aviso que indica que un cortafuegos ha bloqueado a GitHub Copilot. Es lo esperado: Copilot tiene acceso limitado a recursos externos, incluidas las llamadas a servidores MCP externos. Si lo necesitas, puedes [personalizar o deshabilitar el cortafuegos del agente en la nube][agent-firewall].

1. Vuelve al repositorio en github.com.
2. Selecciona **Pull Requests** para abrir la lista de solicitudes.
3. Abre la PR cuyo título sea parecido a **Add missing documentation**.

> [!NOTE]
> Si Copilot todavía está trabajando, la PR mostrará la etiqueta **[WIP]**. Espera a que termine. Puede tardar unos minutos; mientras tanto, puedes descansar o repasar lo que has aprendido.

4. Cuando la PR esté lista, selecciona la pestaña **Files changed** y revisa los cambios.

    ![Pestaña Files changed](../../../_images/shared-pr-files-changed.png)

5. Revisa el código actualizado, incluidos los comentarios de TypeScript Documentation (TSDoc) y el resto de la documentación. Los cambios exactos pueden variar.

   Fíjate en los comentarios TSDoc, las convenciones de TypeScript y los comentarios al principio de los archivos. Estas directrices proceden de los archivos de instrucciones personalizadas que revisaste al principio del ejercicio 2.

6. Cuando hayas revisado los cambios, vuelve a la pestaña **Conversation** y desplázate hacia abajo.
7. Comprueba si hay una indicación de que algunos flujos de trabajo esperan aprobación.
8. Si hay flujos de trabajo pendientes, selecciona **Approve and run workflows**.

   ![Aprobar y ejecutar los flujos de trabajo](../../../_images/shared-approve-workflows.png)

9. Comprueba que los flujos de trabajo se hayan puesto en cola en la sección de comprobaciones de la PR. Si todo va bien, las comprobaciones del proyecto para la aplicación Astro deberían superarse. El proceso puede tardar unos minutos.

## Solicita cambios a GitHub Copilot

La colaboración con Copilot no termina cuando crea una PR. Puedes mencionarlo en comentarios de la PR o en comentarios insertados en el código, igual que harías con otro miembro del equipo. Copilot puede iniciar otra sesión para atender esos comentarios. Como el resultado no es determinista, no hay una frase única que debas utilizar. Por ejemplo, puedes pedirle que:

- Añada comentarios al principio de cada archivo de código con una breve descripción de su propósito.
- Añada comentarios de TypeScript Documentation (TSDoc) a los archivos TypeScript y Astro.
- Cree un archivo README que describa la estructura de la aplicación Astro.

1. Añade un comentario en el que solicites un cambio en la documentación generada y menciona a **@copilot**, como harías con cualquier otro usuario. Utiliza una de las ideas anteriores u otra sugerencia de documentación que quieras incluir en el código.
2. Selecciona **View Session** para ver el trabajo de Copilot. Observa que inicia una sesión nueva para realizar los cambios.
3. Selecciona **Back to pull request** para volver a la PR.

    ![Volver a la solicitud de incorporación de cambios](../../../_images/ex7-back-to-pr.png)

4. Cuando Copilot haya terminado, debería aparecer un nuevo commit en la PR.
5. Selecciona **Files changed** para revisar los cambios.

Puedes seguir iterando hasta que el resultado te convenza. Después, puedes marcar la PR como lista para revisión e integrarla en la rama principal.

![Marcar la PR como lista para revisión](../../../_images/ex7-ready-for-review.png)

## Revisa la funcionalidad de juegos relacionados

Ahora revisarás la PR que Copilot ha creado para mostrar juegos relacionados en la página de detalles de cada juego.

1. Vuelve al repositorio en GitHub.com.
2. Selecciona la pestaña **Pull Requests**.
3. Abre la PR cuyo título sea parecido a **Show related games on the game details page**.
4. Selecciona la pestaña **Files changed** para revisar el código generado.
5. Cuando hayas revisado los cambios, vuelve a la pestaña **Conversation** y desplázate hacia abajo.
6. Comprueba si hay una indicación de que algunos flujos de trabajo esperan aprobación.
7. Si hay flujos de trabajo pendientes, selecciona **Approve and run workflows**.

   ![Aprobar y ejecutar los flujos de trabajo](../../../_images/shared-approve-workflows.png)

8. Comprueba que los flujos de trabajo se hayan puesto en cola en la sección de comprobaciones de la PR. Si todo va bien, las comprobaciones del proyecto para la aplicación Astro deberían superarse. El proceso puede tardar unos minutos.
9. **Opcional:** Puedes cambiar a esta rama en el codespace para probar manualmente la funcionalidad de juegos relacionados. Ve al codespace, abre el terminal y ejecuta estos comandos. Sustituye `<branch-name>` por el nombre de la rama creada por Copilot, por ejemplo, `copilot/fix-8`:

    ```bash
    git fetch origin
    git checkout <branch-name>
    ```

Copilot ha creado la funcionalidad de juegos relacionados. Como antes, puedes pedirle cambios de forma iterativa, por ejemplo, para modificar la cantidad de juegos relacionados o para añadir comentarios al principio de los archivos y comentarios TSDoc. Recuerda que esta incidencia se asignó **antes** de actualizar las instrucciones personalizadas. Para pedir cambios, añade un comentario nuevo en la pestaña **Conversation**. Copilot lo utilizará para iniciar otra sesión.

## Revisa las funcionalidades de accesibilidad

Por último, revisarás las funcionalidades de accesibilidad implementadas con el agente personalizado. Esta PR debe incluir el modo de alto contraste que solicitaste en el ejercicio 3 y el modo claro que pediste desde el panel de agentes en el ejercicio 4.

1. Vuelve al repositorio en GitHub.com.
2. Selecciona la pestaña **Pull Requests**.
3. Abre la PR cuyo título sea parecido a **Add high contrast mode to website**.

> [!NOTE]
> Si Copilot todavía está trabajando, la PR mostrará la etiqueta **[WIP]**. Espera a que termine. Puede tardar unos minutos.

4. Selecciona la pestaña **Files changed** para revisar el código generado.
5. Revisa la implementación y presta atención a estos aspectos:
   - Los componentes de interfaz para cambiar de modo.
   - El uso del almacenamiento local para guardar las preferencias.
   - Los cambios en las hojas de estilo en cascada (CSS) para los modos de alto contraste y claro.
   - Los atributos de Accessible Rich Internet Applications (ARIA) y la navegación mediante teclado.
   - El código JavaScript o TypeScript que gestiona el cambio de modo.

6. Cuando hayas revisado los cambios, vuelve a la pestaña **Conversation** y desplázate hacia abajo.
7. Comprueba si hay una indicación de que algunos flujos de trabajo esperan aprobación.
8. Si hay flujos de trabajo pendientes, selecciona **Approve and run workflows**.

   ![Aprobar y ejecutar los flujos de trabajo](../../../_images/shared-approve-workflows.png)

9. Comprueba que los flujos de trabajo se hayan puesto en cola en la sección de comprobaciones de la PR. Si todo va bien, las comprobaciones del proyecto para la aplicación Astro deberían superarse. El proceso puede tardar unos minutos.
10. **Opcional:** Puedes cambiar a esta rama en el codespace para probar manualmente las funcionalidades de accesibilidad. Ve al codespace, abre el terminal y ejecuta estos comandos. Sustituye `<branch-name>` por el nombre de la rama creada por Copilot:

    ```bash
    git fetch origin
    git checkout <branch-name>
    ```

    Después, inicia la aplicación y prueba los selectores de los modos de alto contraste y claro en el navegador. Comprueba que funcionan y que las preferencias se conservan al volver a cargar la página.

El agente personalizado de accesibilidad ha orientado a Copilot para que implemente estas funcionalidades siguiendo prácticas recomendadas de accesibilidad. Si detectas algún problema de accesibilidad o una posible mejora, puedes mencionar a **@copilot** en un comentario y pedirle que lo corrija, como hiciste con las PR anteriores.

## Ejercicio opcional: sigue delegando

El agente en la nube resulta especialmente útil cuando puedes asignarle tareas reales del backlog y ocuparte de otras cosas. Para practicar, crea algunas incidencias más en tu repositorio y asígnaselas a Copilot. Por ejemplo:

- Crear un formulario para que los usuarios expresen su interés en un juego.
- Implementar la paginación de la lista de juegos.
- Añadir validación de entradas y gestión de errores a los métodos de acceso a los datos.

## Resumen

Has completado el recorrido del agente en la nube. En estas lecciones:

- **Has revisado los archivos de instrucciones personalizadas del repositorio** para comprobar cómo influyen en el trabajo del agente.
- **Has asignado incidencias al agente en la nube de Copilot** y has observado cómo prepara el entorno, planifica y trabaja de forma asíncrona.
- **Has creado y utilizado un agente personalizado** para mejorar la accesibilidad con modos de alto contraste y claro.
- **Has utilizado la página de agentes de Copilot como panel de control** para supervisar y orientar la sesión de accesibilidad.
- **Has revisado las PR del agente en la nube y has iterado sobre ellas**, mencionando a `@copilot` para solicitar cambios y aprobando los flujos de trabajo.

## Repaso y pasos siguientes

Has completado el recorrido del agente en la nube. Si quieres seguir explorando, estos otros recorridos complementan lo que has practicado:

- 🖥️ **[Recorrido de VS Code](../../vscode/)**: explora el modo de agente de Copilot Chat y la integración de MCP directamente en el IDE.
- 💻 **[Recorrido de CLI](../../cli/)**: entrega dos cambios revisados desde el terminal con los modos Plan y Autopilot, las habilidades de agente, un agente personalizado de QA, Playwright MCP, Agent Merge y el puente opcional `/delegate` al agente en la nube.

En tu propio repositorio, prueba estas ideas:

- Asigna al agente en la nube una incidencia de refactorización o de cobertura de pruebas.
- Crea un agente personalizado para otro ámbito.
- Configura `copilot-setup-steps.yml` para otra pila tecnológica.

## Recursos

- [GitHub Copilot][github-copilot]
- [Acerca de los agentes de Copilot][copilot-agents]
- [Asignar incidencias de GitHub a Copilot][assign-issue]
- [Prácticas recomendadas para el flujo de configuración del agente en la nube][cloud-agent-best-practices]
- [Configurar el cortafuegos del agente en la nube][agent-firewall]

---

| [← Lección anterior: Gestión de agentes][previous-lesson] |
|:--|

[github-copilot]: https://github.com/features/copilot
[cloud-agent-overview]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[assign-issue]: https://docs.github.com/copilot/how-tos/use-copilot-agents/cloud-agent/start-copilot-sessions
[setup-workflow]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[copilot-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[cloud-agent-best-practices]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[agent-firewall]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-firewall

[previous-lesson]: ../4-managing-agents/
