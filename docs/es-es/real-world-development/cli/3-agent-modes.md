---
title: "Lección 3: Modos de agente: Plan y Autopilot"
description: "Utiliza Plan para acordar un enfoque, Autopilot para implementar el filtrado a partir de una incidencia e Interactive para revisar el resultado."
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

Has añadido una pequeña funcionalidad al proyecto. Los cambios mayores requieren un proceso más completo. GitHub Copilot CLI permite trabajar con el flujo de tu organización para desarrollar las funcionalidades adecuadas de la forma correcta. En esta lección y las siguientes seguirás un proceso habitual de desarrollo con agentes: partirás de una incidencia para crear una funcionalidad, comprobarás que el código es válido y que la funcionalidad se comporta como se espera y, por último, la integrarás en el proyecto.

> [!NOTE]
> Utilizarás la misma conversación y rama durante todo el flujo de trabajo de esta funcionalidad. Normalmente crearías ramas o PR distintas para los diferentes tipos de archivo, pero en este taller simplificaremos el proceso para centrarnos en los conceptos principales.

En esta lección:

- Iniciarás una conversación nueva de Copilot a partir de una incidencia de GitHub.
- Definirás los requisitos en el modo Plan.
- Implementarás la nueva funcionalidad con el modo Autopilot.
- Revisarás el código.
- Validarás manualmente la funcionalidad en un navegador reenviado.

Mientras sigues trabajando en esta funcionalidad, actualizarás las instrucciones del repositorio, personalizarás la habilidad `quality-checks`, añadirás la validación del Model Context Protocol (MCP), crearás un agente de control de calidad (QA) y abrirás la PR de la funcionalidad.

## Escenario

El catálogo de Tailspin Toys crece y sus visitantes necesitan filtrar juegos por categoría y editorial. La incidencia del backlog describe la funcionalidad, pero hay decisiones pendientes, como si se pueden combinar categorías. Utilizarás el modo Plan para acordar el enfoque y, después, autorizarás una implementación acotada con Autopilot.

## Información de contexto

Incorporar agentes de programación basados en inteligencia artificial (IA) al flujo de desarrollo no cambia los fundamentos; de hecho, los hace aún más importantes. La mayoría de los desarrolladores siguen un proceso parecido a este:

1. Partir de una incidencia que describa el trabajo pendiente.
2. Crear un plan de implementación.
3. Desarrollar y revisar el código.
4. Ejecutar las pruebas para validar el código.
5. Validar manualmente la nueva funcionalidad.
6. Crear una solicitud de incorporación de cambios (PR).
7. Integrar el código cuando se haya revisado y el proceso de integración continua se haya completado correctamente.

> [!NOTE]
> Los detalles varían según el equipo y la organización, pero muchos flujos de trabajo se basan en estos pasos.

Si sigues este enfoque habitual, te aseguras de que el código generado por IA cumpla los requisitos y pase por el mismo proceso de revisión que el código escrito manualmente.

## Modos de conversación

El **modo de conversación** determina el nivel de autonomía del agente. Pulsa <kbd>Shift</kbd>+<kbd>Tab</kbd> para cambiar de modo:

- **Interactive**: trabajas con el agente. Propone cambios y espera a que respondas antes de continuar.
- **Plan**: el agente crea primero un plan y no puede editar los archivos del proyecto.
- **Autopilot**: el agente trabaja de forma autónoma: escribe código, ejecuta pruebas e itera hasta completar la tarea.

Empieza en modo Plan, revisa el plan y, después, utiliza Autopilot para implementarlo.

## Empieza por la incidencia

Antes de trabajar en el filtrado, vuelve al codespace y comprueba que el repositorio y el terminal estén preparados.

1. Vuelve al codespace. Si está detenido, reinícialo.
2. Confirma que la PR de las valoraciones por estrellas se ha integrado.
3. Si el terminal no está abierto, pulsa <kbd>Control</kbd>+<kbd>\`</kbd> (Mac) o <kbd>Ctrl</kbd>+<kbd>\`</kbd> (Windows/Linux).
4. Actualiza `main` y crea una rama para el filtrado:

   ```bash
   git checkout main
   git pull --ff-only
   git checkout -b game-filters-cli
   ```

5. Inicia Copilot CLI:

   ```bash
   copilot --yolo
   ```

6. Pulsa <kbd>Tab</kbd> dos veces para abrir la pestaña **Issues**.
7. Pulsa <kbd>A</kbd> para mostrar todas las incidencias.
8. Utiliza las teclas de flecha para seleccionar la incidencia titulada **Allow users to filter games by category and publisher**.
9. Pulsa <kbd>C</kbd> para añadir la incidencia al mensaje y volver a la pestaña **Session**.

El mensaje empezará ahora por `#7` (o un número parecido). El prefijo `#` permite añadir al contexto una incidencia o una solicitud de incorporación de cambios (PR) de GitHub.

## Planifica la funcionalidad de filtrado

La planificación permite definir cómo implementar una funcionalidad o realizar una tarea antes de asignársela a Copilot. Es recomendable dedicar tiempo a planificar las tareas complejas. Cambia al modo Plan y pide a Copilot que cree el plan.

1. Pulsa <kbd>Shift</kbd>+<kbd>Tab</kbd> para cambiar al modo Plan. Comprueba que el indicador situado debajo del mensaje muestre **Plan**.
2. Después de la referencia a la incidencia que has añadido en el paso anterior, escribe:

   ```plaintext
   Crea un plan para implementar esta funcionalidad.
   ```

Copilot empezará a crear el plan. Primero explorará el proyecto y después determinará el mejor enfoque.

3. Durante el proceso, Copilot puede preguntarte cómo debería funcionar el filtrado. Responde según tus preferencias; no hay una única respuesta correcta.
4. Cuando termine el plan, pulsa <kbd>Control</kbd>+<kbd>E</kbd> (Mac) o <kbd>Ctrl</kbd>+<kbd>E</kbd> (Windows/Linux) para ampliarlo.
5. Desplázate por el plan y revísalo.
6. Pide a Copilot que modifique las partes del plan que no se ajusten a tus decisiones.

## Aprueba Autopilot

Ya has creado y revisado el plan. Ahora lo implementarás con Autopilot, que permite a Copilot iterar sobre el problema hasta considerar que está resuelto.

1. Selecciona **Accept plan and build on autopilot (recommended)** o la opción equivalente en la versión instalada.
2. Comprueba que el indicador situado debajo del mensaje muestre **Autopilot**.
3. Observa cómo Copilot sigue el plan acordado, genera código y ejecuta pruebas.

> [!NOTE]
> Al aprobar el plan, la implementación puede empezar inmediatamente. Revísalo antes de aprobarlo. Si Copilot informa de dependencias ausentes o de un conflicto de puertos, resuelve el problema de configuración antes de dar las comprobaciones por completadas.

## Revisa y verifica la implementación

Como con cualquier otro código, revisa el código generado antes de integrarlo. También ejecutarás el sitio para comprobar que todo funciona.

1. Pulsa <kbd>Shift</kbd>+<kbd>Tab</kbd> para cambiar al modo Interactive. Comprueba que el indicador ya no muestre **Plan** ni **Autopilot**.
2. Introduce `/diff` y revisa la implementación del filtrado y sus pruebas.
3. Compara el resultado con la incidencia y las decisiones tomadas durante la planificación.
4. Cuando hayas revisado el código, pulsa <kbd>Esc</kbd> para salir de la vista de diferencias.
5. Revisa los resultados de las comprobaciones del proyecto y pide a Copilot que corrija los fallos.

## Explora la nueva funcionalidad

El código parece correcto, pero ¿funciona? Inicia la aplicación como antes y abre el sitio desde el puerto reenviado de Codespaces.

1. Pide a Copilot que inicie la aplicación:

   ```plaintext
   Inicia la aplicación para que pueda probar la funcionalidad de filtrado en el navegador. Indícame la URL y deja el servidor en ejecución.
   ```

2. Cuando Codespaces indique que el puerto `4321` está disponible, selecciona **Open in Browser**.
3. Prueba el filtrado por categoría, el filtrado por editorial y las combinaciones acordadas en el plan.
4. Confirma que el restablecimiento de filtros y los resultados vacíos se comportan según la incidencia y tus decisiones.
5. Vuelve al codespace y pide a Copilot que detenga el servidor de desarrollo que ha iniciado.

## Resumen y pasos siguientes

Has utilizado distintos modos de conversación para desarrollar y revisar una funcionalidad. En esta lección:

- Has iniciado una conversación nueva de Copilot a partir de una incidencia de GitHub.
- Has definido los requisitos en modo Plan.
- Has implementado la funcionalidad con Autopilot.
- Has revisado el código.
- Has validado manualmente la funcionalidad en un navegador reenviado.

A continuación, [utilizarás instrucciones personalizadas][next-lesson] para profundizar en cómo se genera el código y asegurarte de que sigue las prácticas documentadas.

## Recursos

- [Autopilot en GitHub Copilot CLI][autopilot]
- [Referencia de comandos de Copilot CLI][cli-reference]

[autopilot]: https://docs.github.com/copilot/concepts/agents/copilot-cli/autopilot
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
[previous-lesson]: ../2-add-star-rating/
[next-lesson]: ../4-custom-instructions/
