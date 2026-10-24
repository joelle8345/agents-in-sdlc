---
title: "Lección 7: Crear y utilizar un agente de control de calidad (QA)"
description: "Crea un agente personalizado de QA que combine los requisitos de la incidencia, la habilidad quality-checks y Playwright del Model Context Protocol (MCP)."
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

Ya has utilizado la habilidad `quality-checks` para ejecutar comprobaciones automatizadas y Playwright MCP para observar la experiencia de filtrado en un navegador. Ahora combinarás esas funciones en un agente personalizado con un proceso de QA definido.

En esta lección:

- Explorarás cómo trabaja un agente personalizado con instrucciones, habilidades y herramientas MCP.
- Crearás y revisarás un perfil de QA reutilizable.
- Seleccionarás el agente de QA y revisarás sus resultados según la incidencia de filtrado.

## Escenario

Antes de crear una solicitud de incorporación de cambios (PR), Tailspin Toys quiere revisar de forma coherente los requisitos, la calidad del código, las comprobaciones automatizadas, la cobertura de las pruebas y el comportamiento en el navegador. Un agente personalizado puede coordinar el proceso de QA y proporcionar un informe reutilizable.

## ¿Qué es un agente personalizado?

Un agente personalizado es una versión especializada de Copilot, definida en un perfil de Markdown. El perfil describe su propósito, sus instrucciones y las herramientas disponibles. En este taller, definirás un perfil de QA en `.github/agents/qa.agent.md` y lo seleccionarás en Copilot CLI.

Las personalizaciones que has utilizado tienen funciones distintas. Las instrucciones del repositorio describen los estándares del equipo. La habilidad `quality-checks` reúne comprobaciones repetibles. Playwright MCP proporciona herramientas del navegador. El perfil de QA indica a Copilot cómo utilizar estas funciones para comprobar los requisitos e informar de los resultados. No las sustituye ni requiere otra conversación.

## Crea el perfil de QA

Antes de abrir la PR de la funcionalidad, pide a Copilot que cree un perfil de QA reutilizable. El perfil definirá las comprobaciones y los límites que debe respetar.

1. Vuelve al codespace y confirma que la conversación de filtrado está en modo Interactive.
2. Pide al agente predeterminado que cree el agente personalizado:

   ```plaintext
   Crea un agente personalizado llamado QA en .github/agents/qa.agent.md. Debe comprobar las funcionalidades según sus incidencias y los requisitos acordados, seguir las instrucciones del repositorio, ejecutar la habilidad quality-checks, utilizar Playwright MCP para verificar el comportamiento y añadir pruebas si falta cobertura.

   Debe informar de cada requisito como superado, fallido o bloqueado e incluir pruebas que respalden el resultado. Debe pedir permiso antes de cambiar código de implementación y no debe confirmar cambios ni crear solicitudes de incorporación de cambios.

   Por ahora, crea solo el perfil para que pueda revisarlo.
   ```

## Inspecciona el perfil

Antes de utilizar el nuevo agente, revisa su perfil para confirmar que Copilot ha incluido el flujo de QA y los límites previstos. Así evitarás que un perfil incompleto o demasiado amplio cambie la funcionalidad cuando solo quieres verificarla.

1. Introduce `/diff` y abre `.github/agents/qa.agent.md`.
2. Lee los metadatos. Se requiere `description`; `name` es opcional, pero le da al agente un nombre visible claro.
3. Lee las instrucciones del perfil y confirma que QA parte de los requisitos, sigue las instrucciones del repositorio, ejecuta la habilidad `quality-checks` y utiliza Playwright MCP.
4. Confirma que QA informa de las pruebas que respaldan los resultados, pide permiso antes de cambiar el código de implementación y no confirma cambios ni crea solicitudes de incorporación de cambios.
5. Si el perfil no incluye alguna de estas responsabilidades o límites, pide al agente predeterminado que lo revise antes de continuar.

## Ejecuta QA según la incidencia

Copilot CLI carga los agentes del proyecto cuando se inicia una conversación. Después de crear el perfil, reanuda la misma conversación de filtrado y selecciona QA para que pueda utilizar el contexto de la incidencia y las decisiones de planificación.

1. Activa el agente con este comando:

   ```plaintext
   /agent QA
   ```

> [!NOTE]
> Como acabas de crear el agente, puede que no aparezca en la lista de agentes disponibles. El comando anterior lo activará igualmente.

2. Envía este mensaje para pedir al agente de QA que revise la funcionalidad:

   ```plaintext
   Revisa la funcionalidad de filtrado según la incidencia y las decisiones del plan. ¿Está lista para crear una PR?
   ```

3. El agente de QA empezará a trabajar.
4. Cuando termine, lee el informe.

## Resumen y pasos siguientes

Has añadido un perfil especializado reutilizable al flujo de trabajo y has revisado sus resultados. En esta lección:

- Has explorado cómo trabaja un agente personalizado con instrucciones, habilidades y herramientas MCP.
- Has creado e inspeccionado un perfil de control de calidad reutilizable.
- Has seleccionado el agente de QA y revisado sus resultados según la incidencia de filtrado.

Ya tienes la implementación, la actualización de la habilidad, el perfil de QA, las pruebas y el informe de verificación listos para revisar. A continuación, [los reunirás en una PR de funcionalidad y utilizarás Agent Merge][next-lesson].

## Recursos

- [Crear agentes personalizados para Copilot CLI][create-agents]
- [Configuración de agentes personalizados][agent-config]

[previous-lesson]: ../6-mcp-playwright/
[next-lesson]: ../8-create-pull-request/
[create-agents]: https://docs.github.com/copilot/how-tos/copilot-cli/customize-copilot/create-custom-agents-for-cli
[agent-config]: https://docs.github.com/copilot/reference/custom-agents-configuration
