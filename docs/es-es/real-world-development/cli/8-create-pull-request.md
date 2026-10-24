---
title: "Lección 8: Crear e integrar la solicitud de incorporación de cambios (PR) de la funcionalidad"
description: "Revisa juntos el filtrado, las instrucciones, la actualización de la habilidad, el perfil de control de calidad (QA) y las pruebas; después, crea una PR y utiliza Agent Merge."
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

La implementación del filtrado, las actualizaciones de instrucciones, los cambios en la habilidad, el perfil de QA y las pruebas están guardados en una misma rama. Ahora los revisarás en conjunto y crearás una PR. Integraste manualmente la PR de las valoraciones por estrellas; esta vez, **Agent Merge** gestionará el proceso.

> [!NOTE]
> Normalmente, dividirías la funcionalidad, las actualizaciones de instrucciones, los cambios en la habilidad y el agente de QA en varias PR. Para simplificar el taller, has mantenido todo el flujo de filtrado y calidad en una conversación y rama, y lo integrarás en una sola PR.

En esta lección:

- Aprenderás qué es Agent Merge y cómo automatiza el ciclo de integración de una PR.
- Revisarás todos los cambios de la funcionalidad y las pruebas de verificación.
- Crearás la PR de filtrado.
- Habilitarás Agent Merge solo después de la revisión y confirmarás que la PR se ha integrado.

## Escenario

Durante el flujo de trabajo del filtrado, has utilizado Copilot para planificar, implementar y verificar una funcionalidad. Ahora Tailspin Toys quiere automatizar el trabajo pendiente de la PR, pero el desarrollador seguirá controlando la autorización de integración.

## Presentación de Agent Merge

**Agent Merge** automatiza el trabajo restante para integrar una solicitud de incorporación de cambios. Cuando lo habilitas, Copilot resuelve los problemas que bloquean la PR, como fallos de integración continua (CI), comentarios de revisión o la necesidad de actualizar la rama base. Después, habilita la integración automática de GitHub si el repositorio lo permite.

Hasta ahora has seleccionado **Merge pull request** manualmente. Agent Merge puede encargarse de esa responsabilidad. Revisa el trabajo y comprueba que está listo antes de habilitarlo.

## Utiliza Agent Merge para gestionar la PR

Ya has creado todo el código. Ahora lo revisarás en conjunto, crearás la PR y dejarás que Agent Merge gestione el resto del proceso.

1. Vuelve al codespace.
2. Abre el cuadro de diálogo del agente introduciendo `/agent`.
3. Selecciona **Default** en la lista y pulsa <kbd>Enter</kbd>.
4. Crea una PR con el comando `/pr create`.
5. Activa Agent Merge con `/pr agentmerge`.
6. Copilot supervisará el proceso de integración continua de la PR. Cuando termine correctamente, integrará los cambios.
7. Comprueba que Copilot muestre un mensaje parecido a «PR #14 was squash-merged successfully».

> [!IMPORTANT]
> Agent Merge no omite las aprobaciones obligatorias, la protección de ramas, las colas de integración, la configuración del repositorio ni los permisos que falten. Si el proceso se bloquea, lee el motivo indicado y completa manualmente la integración revisada cuando el repositorio lo permita.

## Resumen y pasos siguientes

Has automatizado varias partes del desarrollo: la generación de código, las pruebas y la validación, y ahora el proceso de la PR. En esta lección:

- Has aprendido qué es Agent Merge y cómo automatiza el ciclo de integración de una PR.
- Has revisado todos los cambios de la funcionalidad y las pruebas de verificación.
- Has creado la PR de filtrado.
- Has habilitado Agent Merge solo después de revisar los cambios y has confirmado que la PR se ha integrado.

A continuación, [explorarás otros comandos de barra útiles de Copilot CLI][next-lesson] para gestionar el contexto y los modelos, compartir sesiones y delegar trabajo opcionalmente en la nube.

## Recursos

- [Gestionar solicitudes de incorporación de cambios con Copilot CLI][manage-prs]
- [Referencia de comandos de Copilot CLI][cli-reference]

[previous-lesson]: ../7-qa-agent/
[next-lesson]: ../9-cli-power-tools/
[manage-prs]: https://docs.github.com/copilot/how-tos/copilot-cli/use-copilot-cli/manage-pull-requests
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
