---
title: "Lección 10: Repaso y pasos siguientes"
description: "Repasa el flujo de trabajo de Copilot CLI, las dos solicitudes de incorporación de cambios, las personalizaciones reutilizables y otros recursos."
authors:
  - geektrainer
lastUpdated: 2026-09-29
---

Has utilizado GitHub Copilot CLI durante un flujo de trabajo continuo en Tailspin Toys. En concreto:

- Has preparado un codespace, instalado Copilot CLI, explorado el proyecto y localizado la incidencia de filtrado del backlog.
- Has añadido las valoraciones por estrellas, revisado el resultado en un navegador reenviado e integrado manualmente tu primera solicitud de incorporación de cambios (PR).
- Has partido de la incidencia de filtrado, definido el enfoque en modo Plan, implementado la funcionalidad en modo Autopilot y revisado el resultado en modo Interactive.
- Has orientado al agente con instrucciones personalizadas, personalizado la habilidad `quality-checks` y utilizado la habilidad para ejecutar pruebas unitarias, lint y comprobaciones de tipos.
- Has añadido el servidor Playwright del Model Context Protocol (MCP) y lo has utilizado para explorar el filtrado en un navegador real.
- Has creado y seleccionado un agente personalizado de control de calidad (QA) para evaluar los requisitos, la cobertura, los resultados de la habilidad y las pruebas del navegador.
- Has revisado todo el cambio de filtrado y autorizado Agent Merge para integrar la PR.
- Has explorado comandos de barra para gestionar el contexto, los modelos, compartir sesiones y delegar trabajo opcionalmente al agente en la nube.

## Lo que has entregado

El taller tiene dos hitos de PR, cada uno en su propia rama creada a partir de `main` actualizado:

1. **Valoraciones por estrellas:** muestra la propiedad `starRating` existente y un estado explícito para los juegos sin valoración en las tarjetas.
2. **Filtrado y flujo de calidad:** implementa el filtrado, actualiza las instrucciones y las aplica a la funcionalidad, personaliza el informe de `quality-checks`, crea un perfil de QA e incluye las pruebas correspondientes.

Has utilizado la misma conversación y rama desde la planificación del filtrado hasta la creación de su PR. Hemos agrupado ese trabajo en una sola PR para simplificar el taller.

## Distintos tipos de verificación

Has comprobado el código de varias maneras: mediante pruebas automatizadas, una inspección manual en el navegador y la exploración del navegador por parte de Copilot con MCP. La habilidad `quality-checks` ha ejecutado pruebas unitarias, lint y comprobaciones de tipos y ha informado de los resultados con el nuevo formato. QA ha combinado esos resultados con la revisión de los requisitos y la cobertura de pruebas antes de crear la PR.

Las pruebas nuevas deben cubrir carencias reales. Si la revisión de QA concluye que no hace falta añadir pruebas, puede ser correcto. Revisa el código y las pruebas antes de autorizar la integración y actualiza las pruebas afectadas después de hacer cambios.

## Prácticas recomendadas

El contexto y las herramientas que proporcionas a Copilot influyen en su trabajo. En este taller has actualizado instrucciones, personalizado una habilidad, creado un perfil de QA y configurado un servidor MCP. Puedes reutilizar estas personalizaciones en distintas conversaciones y adaptarlas cuando cambien las necesidades del equipo. Las instrucciones establecen estándares, las habilidades describen tareas repetibles, los agentes personalizados definen perfiles especializados y los servidores MCP conectan herramientas externas. Revisa los cambios y los resultados reales de las herramientas, no solo el resumen del agente.

Adapta el **modo y el modelo** a la tarea. Utiliza **Plan** para definir el enfoque antes de implementar, **Interactive** para participar en los cambios acotados y **Autopilot** para tareas con un alcance claro. Elige un modelo más rápido para los cambios habituales y otro más capaz para tareas complejas.

El contexto sigue siendo tan importante como la infraestructura. Describir con claridad *qué* quieres desarrollar, *por qué* y *cómo* influye de forma significativa en el resultado.

## Más opciones para explorar

Ya has completado el flujo de trabajo principal. También puedes explorar estas funciones de CLI:

- `/review` para pedir al agente de revisión de código que analice los cambios.
- `/rubber-duck` para explicar un problema y obtener otro punto de vista.
- `/fleet` para coordinar tareas independientes en paralelo.
- `/worktree` para aislar otra tarea.
- `/delegate` para enviar una tarea al agente en la nube de Copilot.

## Pasos siguientes

La mejor forma de mejorar con cualquier herramienta es seguir utilizándola. Aplícala a código de producción, proyectos personales o esa pequeña aplicación que llevas años pensando en crear. Comparte lo que aprendas con el equipo, aprende de sus experiencias y consulta la documentación.

Si quieres ampliar Tailspin Toys desde el terminal, continúa con la serie opcional [Foundry Backer Concierge][foundry]. Para comparar otros entornos, explora el [taller de VS Code][vscode], el [taller de la aplicación GitHub Copilot][app] o el [taller del agente en la nube de Copilot][cloud].

## Recursos

- [Acerca de GitHub Copilot CLI][about-cli]
- [Referencia de comandos de Copilot CLI][cli-reference]
- [Personalizar Copilot CLI][customize-cli]
- [Gestionar solicitudes de incorporación de cambios con Copilot CLI][manage-prs]

[previous-lesson]: ../9-cli-power-tools/
[foundry]: ../8-foundry-agent/
[vscode]: ../../vscode/
[app]: ../../app/
[cloud]: ../../cloud/
[about-cli]: https://docs.github.com/copilot/concepts/agents/about-copilot-cli
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
[customize-cli]: https://docs.github.com/copilot/how-tos/copilot-cli/customize-copilot
[manage-prs]: https://docs.github.com/copilot/how-tos/copilot-cli/use-copilot-cli/manage-pull-requests
