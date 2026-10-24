---
title: "Lección 8: Crear e integrar la solicitud de incorporación de cambios (PR) de la funcionalidad"
description: "Revisa conjuntamente el filtrado, las instrucciones, la actualización de la habilidad, el perfil de control de calidad (QA) y las pruebas; después, crea una PR y utiliza Agent Merge."
authors:
  - geektrainer
lastUpdated: 2026-10-22
---

La implementación del filtrado, las actualizaciones de instrucciones, los cambios en la habilidad, el perfil de control de calidad (QA) y las pruebas están guardados en una sola rama. Ahora los revisarás juntos y crearás una solicitud de incorporación de cambios (PR). Ya integraste personalmente la PR de las valoraciones por estrellas; esta vez permitirás que **Agent Merge** gestione el proceso.

> [!NOTE]
> Normalmente dividirías la funcionalidad, las actualizaciones de instrucciones y de la habilidad y el agente de QA en varias PR. Para simplificar el taller, has mantenido todo el flujo de filtrado y calidad en una sesión y una rama, y lo integrarás en una sola PR.

En esta lección:

- Aprenderás qué es Agent Merge y cómo automatiza el ciclo de integración de una PR.
- Revisarás la PR completa de la funcionalidad y las pruebas de verificación.
- Autorizarás Agent Merge solo después de la revisión y confirmarás que la PR se ha integrado.

## Escenario

Durante el flujo de trabajo del filtrado, has utilizado Copilot para planificar, implementar y verificar una funcionalidad. Ahora Tailspin Toys quiere automatizar el trabajo restante de la PR y mantener el control de la autorización de integración en manos del desarrollador.

## Presentación de Agent Merge

**Agent Merge** automatiza el trabajo restante para integrar una solicitud de incorporación de cambios en la aplicación GitHub Copilot. Cuando lo habilitas, la sesión de la aplicación lee la PR y resuelve lo que la bloquea: corrige las comprobaciones de integración continua (CI) que fallan, responde a comentarios de revisión y actualiza la rama base cuando sea necesario. Después, la integra en cuanto GitHub lo permite. Se ejecuta en segundo plano, continúa tras reiniciar la aplicación y se desactiva cuando se integra la PR.

Hasta ahora has seleccionado **Merge pull request** manualmente. Agent Merge puede encargarse de esa tarea, pero su capacidad de editar código e integrar cambios sigue necesitando tu autorización explícita. Revisa las acciones permitidas y el trabajo antes de conceder permiso para integrar la PR.

## Utiliza Agent Merge para gestionar la PR

Ya has creado y revisado todo el código. Ahora permitirás que Agent Merge gestione el proceso de la PR.

1. Utiliza el selector de agentes para seleccionar **Default agent**.
2. Selecciona el menú desplegable junto a **Create PR**.
3. Selecciona **Agent Merge**. El texto del botón cambiará a **Agent Merge**.
4. Selecciona el botón **Agent Merge** para iniciar el proceso. Elegir la opción del menú desplegable no inicia el proceso por sí solo.

Se iniciará el proceso de Agent Merge. Hará lo siguiente:

- Crear la solicitud de incorporación de cambios con un título y una descripción.
- Si has iniciado la sesión desde una incidencia, incluir una referencia a ella en el cuerpo de la descripción.
- Actualizar la rama base o gestionar posibles conflictos de integración.
- Supervisar el proceso de CI para comprobar que se superen todas las comprobaciones.
- Supervisar la PR para detectar comentarios de otros desarrolladores o de la revisión de código de Copilot y realizar cambios para resolverlos.
- Integrar automáticamente la PR cuando todo se haya completado correctamente, si se lo autorizas.

Permitirás que Agent Merge también integre la PR cuando se hayan superado todas las comprobaciones.

5. Revisa las diferencias de la PR y las pruebas de verificación antes de conceder permiso para integrarla.
6. Selecciona el menú desplegable junto a **Agent Merge**.
7. Comprueba que **Merge pull request** esté marcado.
8. Pide explícitamente al agente que integre la PR:

    ```plaintext
    Merge the PR once all required checks and approvals pass. Do not bypass repository protections.
    ```

9. Supervisa el progreso y resuelve los bloqueos que se indiquen. Antes de continuar, confirma que el estado de la PR sea **Merged**. Tener habilitado el permiso de integración o un agente en ejecución no confirma que la PR se haya integrado.

> [!IMPORTANT]
> Agent Merge no omite las protecciones del repositorio ni los permisos que falten. Resuelve esos bloqueos antes de continuar.

## Resumen y pasos siguientes

Has automatizado varias partes del desarrollo: la generación de código, las pruebas y la validación, y ahora también el proceso de la PR. En concreto:

- Has aprendido qué es Agent Merge y cómo automatiza el ciclo de integración de una PR.
- Has revisado la PR completa de la funcionalidad y las pruebas de verificación.
- Has autorizado Agent Merge solo después de la revisión y has confirmado que la PR se ha integrado.

A continuación, [utilizarás un lienzo existente y crearás uno de clasificación][next-lesson] para explorar una forma más completa de examinar, planificar y visualizar el trabajo con el agente.

## Recursos

- [Gestionar incidencias y solicitudes de incorporación de cambios con la aplicación GitHub Copilot][managing-issues-prs]
- [Acerca de la aplicación GitHub Copilot][about-copilot-app]

[next-lesson]: ../9-canvases/
[managing-issues-prs]: https://docs.github.com/copilot/how-tos/github-copilot-app/managing-issues-and-pull-requests
[about-copilot-app]: https://docs.github.com/copilot/concepts/agents/github-copilot-app
