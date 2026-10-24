---
slug: es-es/real-world-development/cli
title: "GitHub Copilot CLI"
description: "Desarrolla, verifica y entrega dos cambios en Tailspin Toys mientras aprendes a utilizar los modos, las personalizaciones, las herramientas MCP y la automatización de solicitudes de incorporación de cambios de Copilot CLI."
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

**[GitHub Copilot CLI][about-copilot-cli]** lleva GitHub Copilot al terminal como asistente de programación agéntico. Explora bases de código, genera código, ejecuta comandos y se conecta a herramientas externas, todo desde la línea de comandos para que puedas seguir trabajando sin cambiar a un editor gráfico.

El taller sigue un flujo de trabajo continuo en Tailspin Toys:

1. Prepara el proyecto en GitHub Codespaces, instala Copilot CLI y familiarízate con el entorno.
2. Añade valoraciones por estrellas, revisa el cambio en el navegador e integra manualmente tu primera solicitud de incorporación de cambios (PR).
3. Parte de la incidencia de filtrado, define el enfoque en modo Plan, implementa la funcionalidad en modo Autopilot y revísala en modo Interactive.
4. Actualiza las instrucciones del repositorio y aplícalas al trabajo de filtrado.
5. Personaliza la habilidad `quality-checks` existente y úsala para ejecutar las comprobaciones del proyecto.
6. Añade el servidor Playwright del Model Context Protocol (MCP) y úsalo para explorar el filtrado en un navegador.
7. Crea un agente personalizado de control de calidad (QA) y úsalo para revisar los requisitos, la cobertura y las pruebas de verificación.
8. Revisa el cambio completo de filtrado y utiliza Agent Merge para la PR correspondiente.
9. Explora comandos de barra útiles para gestionar el contexto, los modelos, compartir sesiones y delegar trabajo opcionalmente al agente en la nube.

Para mantener el taller centrado, crearás dos PR: una para las valoraciones por estrellas y otra para el filtrado, con las actualizaciones de instrucciones y de la habilidad, el perfil QA y las pruebas. El flujo de trabajo de filtrado y calidad comparte una conversación y una rama para que puedas aprovechar el trabajo realizado mientras exploras cada herramienta.

## Lecciones

| Lección | Tema | Descripción |
| ------ | ----- | ----------- |
| [0. Requisitos previos][ex0] | Configuración | Crea tu repositorio y codespace |
| [1. Instalar Copilot CLI][ex1] | Instalación | Instala y autentica Copilot CLI y familiarízate con el entorno |
| [2. Añadir valoraciones por estrellas: una mejora rápida][ex2] | Primer cambio | Muestra las valoraciones existentes y el estado sin valoración; después, integra tu primera PR |
| [3. Modos de agente: Plan y Autopilot][ex3] | Modos de agente | Planifica la funcionalidad a partir de su incidencia, impleméntala con Autopilot y revísala en modo Interactive |
| [4. Guiar a Copilot con instrucciones personalizadas][ex4] | Contexto | Explora y actualiza las instrucciones y aplícalas al filtrado |
| [5. Personalizar y utilizar la habilidad quality-checks][ex5] | Comprobaciones repetibles | Explora la habilidad existente, cambia el formato de su informe y ejecútala |
| [6. Validar la funcionalidad con Playwright MCP][ex6] | Observación en el navegador | Configura MCP en CLI y examina el comportamiento del filtrado |
| [7. Crear y utilizar un agente de QA][ex7] | Requisitos y cobertura | Crea y selecciona un perfil especializado y reúne pruebas de verificación |
| [8. Crear e integrar la PR de la funcionalidad][ex8] | Revisión e integración | Revisa el cambio completo, crea la PR y utiliza Agent Merge |
| [9. Comandos de barra de GitHub Copilot CLI][ex9] | Funciones de CLI | Explora el contexto, los modelos, compartir sesiones y delegar trabajo al agente en la nube |
| [10. Repaso y pasos siguientes][ex10] | Resumen | Repasa el flujo de trabajo, las personalizaciones reutilizables y otros recursos |
| [Opcional: integrar Foundry][foundry] | Agentes hospedados | Prepara un modelo, implementa un agente basado en el catálogo y conéctalo al sitio web |

## Requisitos previos

Antes de asistir a este taller, asegúrate de disponer de:

- [ ] Una cuenta de GitHub con un plan **Copilot Student, Pro, Pro+, Business o Enterprise** activo
- [ ] Permiso para crear un repositorio y un codespace
- [ ] Conocimientos básicos sobre el terminal o la línea de comandos

> [!TIP]
> ¿No tienes un plan de pago? Los estudiantes verificados pueden obtener GitHub Copilot gratis mediante [GitHub Education][student-plan]. El plan **Copilot Student** incluye el agente, MCP, la revisión de código y las funciones de Copilot CLI que se utilizan en este taller.

> [!NOTE]
> Si utilizas Copilot Business o Copilot Enterprise, asegúrate de que el administrador haya habilitado Copilot CLI.

## Comenzar

**[Empieza por los requisitos previos →][ex0]**

[about-copilot-cli]: https://docs.github.com/copilot/concepts/agents/about-copilot-cli
[student-plan]: https://github.com/education/students
[ex0]: 0-prerequisites/
[ex1]: 1-install-copilot-cli/
[ex2]: 2-add-star-rating/
[ex3]: 3-agent-modes/
[ex4]: 4-custom-instructions/
[ex5]: 5-agent-skills/
[ex6]: 6-mcp-playwright/
[ex7]: 7-qa-agent/
[ex8]: 8-create-pull-request/
[ex9]: 9-cli-power-tools/
[ex10]: 10-review/
[foundry]: 8-foundry-agent/
