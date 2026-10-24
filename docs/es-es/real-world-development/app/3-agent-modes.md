---
title: "Lección 3: Modos de agente: Plan y Autopilot"
description: "Explora los modos de agente: utiliza Plan para acordar un enfoque, Autopilot para implementar el filtrado desde una incidencia e Interactive para revisar y verificar el resultado."
authors:
  - geektrainer
lastUpdated: 2026-10-22
---

Empezamos añadiendo una pequeña funcionalidad al proyecto, pero los cambios más amplios requieren un proceso más sólido. La aplicación GitHub Copilot está diseñada para adaptarse al flujo de trabajo de una organización y ayudar a desarrollar las funcionalidades adecuadas de la forma correcta. En esta lección y las siguientes seguirás un proceso habitual de desarrollo con agentes: partirás de una incidencia para crear una funcionalidad, comprobarás que el código es válido y que la funcionalidad se comporta como se espera y, por último, la integrarás en el proyecto.

> [!NOTE]
> Utilizarás la misma sesión durante todo el flujo de trabajo de la funcionalidad. Normalmente usarías sesiones o solicitudes de incorporación de cambios (PR) distintas para diferentes tipos de archivo, pero simplificaremos el proceso para centrarnos en los conceptos principales.

En esta lección:

- Iniciarás una sesión de agente nueva desde una incidencia de GitHub.
- Definirás los requisitos en modo **Plan**.
- Implementarás la nueva funcionalidad con **Autopilot**.
- Revisarás el código.
- Validarás manualmente la funcionalidad en un lienzo de navegador.

Mientras continúas con esta funcionalidad, actualizarás las instrucciones del repositorio, personalizarás la habilidad `quality-checks`, añadirás validación del Model Context Protocol (MCP), crearás un agente de control de calidad (QA) y abrirás la PR de la funcionalidad.

## Escenario

El catálogo de Tailspin Toys crece y sus visitantes necesitan filtrar los juegos por categoría y editorial. La incidencia del backlog describe la funcionalidad, pero hay que acordar detalles como la combinación de categorías antes de programar. Utilizarás el modo Plan para resolver esas decisiones y, después, autorizarás una implementación acotada con Autopilot.

## Información de contexto

Incorporar agentes de programación basados en inteligencia artificial (IA) al flujo de desarrollo no cambia los fundamentos. De hecho, los hace aún más importantes. La mayoría de los desarrolladores siguen un proceso parecido:

1. Abrir una incidencia registrada que describa el trabajo pendiente.
2. Crear un plan de lo que debe desarrollarse.
3. Desarrollar y revisar el código.
4. Ejecutar las pruebas para validar el código.
5. Validar manualmente la nueva funcionalidad.
6. Crear una solicitud de incorporación de cambios (PR).
7. Integrar el código cuando se haya revisado y el proceso de integración continua se haya completado correctamente.

> [!NOTE]
> Los detalles concretos varían según el equipo y la organización, pero muchos procesos son una variante del flujo anterior.

Si sigues este enfoque estándar, te aseguras de que el código generado por IA cumpla los requisitos y pase por el mismo proceso de revisión que el código escrito manualmente.

## Modos de sesión

El **modo de sesión** determina el nivel de autonomía del agente. Puedes seleccionarlo en el menú desplegable situado debajo del campo de mensaje y cambiarlo en cualquier momento:

- **Interactive**: trabajas con el agente. Propone cambios y espera tus indicaciones antes de continuar.
- **Plan**: el agente crea primero un plan. Lo revisas y apruebas antes de que el agente lo ejecute.
- **Autopilot**: el agente trabaja de forma totalmente autónoma: escribe código, ejecuta pruebas e itera sin esperar indicaciones.

Empieza en modo Plan, revisa el plan y, después, utiliza Autopilot para implementarlo.

## Inicia una sesión desde la incidencia

Antes de empezar, confirma que la PR de valoraciones por estrellas se ha integrado y que tu rama local `main` está actualizada.

1. En **Sessions**, selecciona la carpeta del repositorio Tailspin Toys y, en la navegación superior del repositorio, selecciona **Issues**. Abre **Allow users to filter games by category and publisher**. Es una incidencia existente de la plantilla; no tienes que crear otra.
2. Selecciona **New session** y elige un **new working tree** basado en la rama `main` actualizada.

    ![Vista de una incidencia en la aplicación GitHub Copilot con una flecha que señala el botón New session](../../../_images/app-new-session-from-issue.png)

3. Confirma que la incidencia está adjunta a la sesión y selecciona **Plan** en el selector de modo.

> [!NOTE]
> Si no se encuentra Node.js o npm, pide al agente que ejecute `node --version` y `npm --version`. Si funcionan en el terminal pero no en la sesión, comprueba la configuración de `PATH` o del gestor de versiones de la aplicación y ciérrala y vuelve a abrirla por completo. Repite la operación y las comprobaciones que fallaron. No reinstales npm solo porque el agente no lo encuentre.

## Planifica la funcionalidad de filtrado

La planificación permite revisar el enfoque antes de que Copilot escriba código. Como has iniciado la sesión desde la incidencia, Copilot ya tiene la solicitud como contexto. Envía:

```plaintext
Implementa esta funcionalidad.
```

Responde a las preguntas de Copilot y compara el plan con los criterios de aceptación de la incidencia. Comprueba que abarque el filtrado por categoría y editorial, los controles accesibles, los cambios en el acceso a datos y las pruebas. Aclara cualquier comportamiento poco definido, como la combinación de varias categorías o qué ocurre cuando ningún juego coincide.

El plan debe incluir lint, pruebas unitarias, pruebas de extremo a extremo (E2E) y comprobaciones de tipos con las herramientas existentes del proyecto. Céntralo en implementar y probar el filtrado; crearás la PR después de completar el flujo de calidad. Pide cambios en el plan antes de aprobarlo y conserva la URL de la incidencia y las aclaraciones acordadas para la validación posterior.

## Aprueba Autopilot explícitamente

Cuando estés conforme con el plan, selecciona **Approve and implement this plan** o la opción equivalente de tu versión. Comprueba el modo activo en lugar de dar por hecho que la aprobación lo cambia. Confirma que el indicador muestre **Autopilot**.

Copilot empezará a implementar la funcionalidad. Observa cómo sigue el plan acordado, genera código y ejecuta pruebas.

> [!NOTE]
> La aprobación puede iniciar la implementación inmediatamente, así que revisa el plan primero. Si Copilot informa de dependencias ausentes o de un conflicto de puertos, resuelve el problema de configuración antes de dar las comprobaciones por completadas. Detén solo los servidores que hayas iniciado.

## Revisa y verifica la implementación

Como cualquier otro código, el código generado debe revisarse antes de integrarlo. Revisarás los cambios y ejecutarás el sitio para comprobar que todo funcione.

1. Abre **Changes** y revisa la implementación del filtrado y sus pruebas.
2. Compara el resultado con la incidencia y las aclaraciones aprobadas, incluidas las combinaciones de categorías y editoriales. Comprueba que los cambios respeten las instrucciones existentes del repositorio.
3. Revisa los resultados de lint, las pruebas unitarias, las pruebas E2E y las comprobaciones de tipos. Una comprobación omitida no cuenta como superada.
4. Resuelve los fallos y repite las comprobaciones afectadas antes de aceptar la implementación. La configuración de pruebas E2E de Playwright compila y sirve una vista previa y puede reutilizar un servidor local. Comprueba que el servidor probado pertenezca a este árbol de trabajo y no a una lección anterior.

## Explora la nueva funcionalidad

El código parece correcto, pero ¿se ejecuta? Inicia la aplicación como antes y abre el sitio en un lienzo de navegador.

1. Envía este mensaje para pedir a Copilot que inicie la aplicación y abra la página en el lienzo de navegador:

    ```plaintext
    Inicia la aplicación y ábrela en el lienzo de navegador.
    ```

2. En unos instantes, se iniciará la aplicación y se abrirá una ventana del navegador dentro de la aplicación Copilot.
3. Selecciona una categoría y confirma que los resultados coinciden. Quita el filtro, selecciona una editorial y confirma que los resultados corresponden a esa editorial.
4. Combina filtros de categoría y editorial y compara los resultados con la incidencia y el plan aprobado. Si se admiten varias categorías, comprueba el comportamiento acordado.
5. Prueba una combinación sin juegos coincidentes y comprueba el estado vacío. Quita o restablece los filtros y confirma que vuelve a aparecer la lista completa.
6. Cuando termines, pide a Copilot que detenga el servidor de desarrollo que ha iniciado para esta sesión y cierre el lienzo del navegador:

    ```plaintext
    Detén el servidor de desarrollo y cierra el lienzo del navegador.
    ```

## Conserva esta sesión para las lecciones siguientes

Todavía no crees ni integres la PR del filtrado. Conserva esta sesión, este árbol de trabajo y esta rama para las lecciones 4 a 8. A continuación, aplicarás instrucciones personalizadas al código de filtrado y añadirás mejoras a la habilidad y al agente de QA antes de crear e integrar la PR combinada en la lección 8. Puedes dejar la sesión inactiva después de detener el servidor de desarrollo y volver a ella en la siguiente lección.

## Resumen y pasos siguientes

Has utilizado distintos modos de agente para desarrollar y revisar una funcionalidad. En esta lección:

- Has iniciado una sesión de agente nueva desde una incidencia de GitHub.
- Has definido los requisitos en modo **Plan**.
- Has implementado la nueva funcionalidad con **Autopilot**.
- Has revisado el código.
- Has validado manualmente la funcionalidad en un lienzo de navegador.

A continuación, profundizarás en cómo se genera el código y comprobarás que sigue las prácticas documentadas mediante el [uso de instrucciones personalizadas][next-lesson].

## Recursos

- [Trabajar con sesiones de agente en la aplicación GitHub Copilot][agent-sessions]

[next-lesson]: ../4-custom-instructions/
[agent-sessions]: https://docs.github.com/copilot/how-tos/github-copilot-app/agent-sessions
