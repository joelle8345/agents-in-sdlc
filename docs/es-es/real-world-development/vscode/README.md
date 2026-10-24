---
slug: es-es/real-world-development/vscode
title: "Visual Studio Code"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

**[GitHub Copilot Chat](https://code.visualstudio.com/docs/copilot/chat/copilot-chat)** en VS Code integra GitHub Copilot en el editor que ya utilizas. En Visual Studio Code y GitHub Codespaces, trabajarás con Copilot Chat en modo agente, conectarás herramientas externas mediante MCP y utilizarás agentes personalizados sin salir del IDE, donde Copilot tiene acceso a tus archivos, al terminal y a los problemas.

Empezarás añadiendo instrucciones personalizadas y comprobarás cómo las sigue Copilot. Después, utilizarás el modo agente para crear una funcionalidad de filtrado en la interfaz, la capa de datos y las pruebas. A continuación, conectarás el servidor Playwright MCP y dejarás que Copilot controle un navegador para probar la funcionalidad antes de crear una solicitud de incorporación de cambios. Por último, revisarás y utilizarás un agente personalizado para las tareas de accesibilidad, y supervisarás, orientarás e iterarás sobre los cambios de Copilot sin salir del editor.

## Ejercicios

| Ejercicio | Tema | Descripción |
|----------|-------|-------------|
| [0. Requisitos previos][ex0] | Configuración | Crea tu repositorio y codespace |
| [1. Instrucciones personalizadas][ex1] | Contexto | Añade y verifica instrucciones personalizadas en VS Code |
| [2. Modo agente][ex2] | Generación de código | Crea una funcionalidad de filtrado en modo agente |
| [3. MCP con Playwright][ex3] | Herramientas externas | Prueba la funcionalidad en un navegador con el servidor Playwright MCP |
| [4. Agentes personalizados][ex4] | Agentes especializados | Revisa y utiliza agentes personalizados |
| [5. Gestionar agentes][ex5] | Supervisión | Supervisa y orienta las sesiones del agente |
| [6. Iteración][ex6] | Revisión | Revisa localmente el trabajo de Copilot y elige los pasos siguientes |
| [Opcional: Incorporar Foundry][foundry-toolkit] | Agentes de IA | Prepara un modelo, implementa un agente y conéctalo al sitio en tres módulos con VS Code y Foundry Toolkit |

## Requisitos previos

Antes de asistir a este taller, asegúrate de disponer de:

- [ ] Una cuenta de GitHub con un plan **Copilot Student, Pro, Pro+, Business o Enterprise** activo
- [ ] Acceso a GitHub Codespaces

> [!TIP]
> ¿No tienes un plan de pago? Los estudiantes verificados pueden obtener GitHub Copilot gratis mediante [GitHub Education][callout-student-plan-education]. El plan **Copilot Student** incluye el agente, MCP, la revisión de código y las funciones de Copilot CLI que se utilizan en este taller, por lo que permite completar todos los recorridos.

[callout-student-plan-education]: https://github.com/education/students

## Comenzar

**[Empieza por el ejercicio 0: Requisitos previos →][ex0]**

[ex0]: 0-prerequisites/
[ex1]: 1-custom-instructions/
[ex2]: 2-agent-mode/
[ex3]: 3-mcp/
[ex4]: 4-custom-agents/
[ex5]: 5-managing-agents/
[ex6]: 6-iterating/
[foundry-toolkit]: 7-foundry-toolkit/
