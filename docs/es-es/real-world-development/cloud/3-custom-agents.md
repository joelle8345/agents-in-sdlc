---
title: "Ejercicio 3: Agentes personalizados"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

## ¿Qué son los agentes personalizados?

Los [agentes personalizados][custom-agents-concept] de GitHub Copilot son asistentes de inteligencia artificial (IA) especializados que puedes adaptar a tareas o ámbitos concretos del flujo de desarrollo. Se definen mediante archivos Markdown en la carpeta `.github/agents` del repositorio. Puedes proporcionar al agente instrucciones específicas, prácticas recomendadas, patrones de código y conocimientos del dominio para que realice determinados tipos de trabajo con mayor eficacia. Los equipos pueden convertir su experiencia en agentes reutilizables, como un agente de accesibilidad que compruebe el cumplimiento de las Pautas de Accesibilidad para el Contenido Web (WCAG), uno de seguridad que siga prácticas de programación segura o uno de pruebas que mantenga patrones de prueba coherentes.

Los agentes personalizados se definen en archivos Markdown dentro de `.github/agents` en el proyecto o, de forma global, en `~/.copilot/agents`. Cada archivo contiene metadatos YAML con, como mínimo, los campos `name` y `description`, seguidos de una instrucción en Markdown que define el comportamiento, la experiencia y las directrices del agente.

### Diferencias entre los agentes personalizados y las habilidades de agente

Los agentes personalizados y las [habilidades de agente][agent-skills-concept] tienen algunas similitudes. Ambos se definen principalmente en archivos Markdown y explican a una IA cómo realizar tareas. La diferencia más sencilla es que un **agente personalizado** realiza el trabajo y las **habilidades** son herramientas.

Los agentes personalizados tienen su propia ventana de contexto y coordinan habilidades e incluso otros agentes para completar el trabajo. En este taller, el agente personalizado de accesibilidad revisará y actualizará el sitio de acuerdo con las directrices de accesibilidad. Como parte de la tarea, podría utilizar habilidades como una para gestionar el flujo de trabajo de las solicitudes de incorporación de cambios o para ejecutar y gestionar pruebas.

> [!NOTE]
> No existe una única manera correcta de crear un agente personalizado. Como ocurre con cualquier herramienta de IA, prueba y ajusta el agente para adaptarlo a tu entorno y a tus escenarios.

[custom-agents-concept]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
[agent-skills-concept]: https://docs.github.com/copilot/concepts/agents/about-agent-skills
[wcag]: https://www.w3.org/WAI/standards-guidelines/wcag/

En este ejercicio explorarás:

- Cómo se definen los agentes personalizados.
- Cómo asignarles tareas.

## Escenario

Tailspin Toys quiere que su plataforma de financiación colectiva sea accesible para todas las personas, independientemente de sus capacidades visuales o preferencias. Algunos usuarios han indicado que el tema oscuro actual es difícil de leer porque el contraste entre el texto y el fondo es insuficiente. Para resolver este problema de accesibilidad, el equipo de diseño ha solicitado un modo de alto contraste que se pueda activar y desactivar.

Como la accesibilidad es prioritaria, utilizarás un agente personalizado para generar esta funcionalidad cuanto antes.

## Revisa el agente personalizado de accesibilidad

Ya se ha creado un agente personalizado para las tareas de accesibilidad. Revisa su contenido para saber cómo orientará a Copilot.

Vuelve al codespace y abre el archivo del agente de accesibilidad:

1. Abre `.github/agents/accessibility.md`.
2. Revisa los campos `name` y `description` de los metadatos YAML.

> [!CAUTION]
> Los campos `name` y `description` son obligatorios en los metadatos de un agente personalizado.

3. Revisa las secciones siguientes, que describen:
   - Las responsabilidades principales al generar código para un sitio web accesible.
   - Las prácticas recomendadas de accesibilidad.
   - Ejemplos del lenguaje de marcado de hipertexto (HTML), hojas de estilo en cascada (CSS) y JavaScript.
   - Errores frecuentes y cómo evitarlos.

## Crea y asigna una incidencia

El panel de agentes es el espacio central desde el que puedes asignar tareas al agente en la nube de Copilot, supervisar su progreso y orientarlo. Primero, asígnale la tarea de crear el modo de alto contraste.

1. Ve al repositorio.
2. Selecciona la pestaña **Issues**.
3. Selecciona **New issue** para abrir el cuadro de diálogo de creación de incidencias.
4. Selecciona **Blank issue**.
5. Escribe `Add high contrast mode to website` en el campo **Title**.
6. Escribe lo siguiente en **Description**:

    ```plaintext
    We need a high contrast mode for the site. There should be a toggle for high contrast which the user can set. It should store the setting in local storage on the browser.
    ```

7. Selecciona **Create** para crear la incidencia.
8. En el lado derecho, selecciona **Assign to Copilot** para abrir el cuadro de asignación.
9. Selecciona **Accessibility agent** en la lista de agentes personalizados.

    ![Asignación del agente en la nube con el agente de accesibilidad seleccionado](../../../_images/ex5-select-custom-agent.png)

10. Selecciona **Assign**.
11. Copilot empezará a trabajar en segundo plano.

## Resumen y pasos siguientes

Has explorado los [agentes personalizados][custom-agents], asistentes de IA especializados en tareas y ámbitos concretos. Te permiten convertir los conocimientos y estándares del equipo en agentes reutilizables que orientan el trabajo de Copilot.

Has explorado estos conceptos:

- Cómo se definen los agentes personalizados.
- Cómo asignarles tareas.

Mientras Copilot implementa el modo de alto contraste, a continuación aprenderás a [supervisar y orientar la sesión del agente][next-lesson] desde el panel de agentes.

## Recursos

- [Acerca de los agentes personalizados][custom-agents]
- [Preparar la organización para usar agentes personalizados][org-custom-agents]
- [Preparar la empresa para usar agentes personalizados][enterprise-custom-agents]

---

| [← Lección anterior: Agente en la nube de GitHub Copilot][previous-lesson] | [Siguiente lección: Supervisar y gestionar agentes →][next-lesson] |
|:--|--:|

[previous-lesson]: ../2-cloud-agent/
[next-lesson]: ../4-managing-agents/
[custom-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
[org-custom-agents]: https://docs.github.com/copilot/how-tos/administer-copilot/manage-for-organization/prepare-for-custom-agents
[enterprise-custom-agents]: https://docs.github.com/copilot/how-tos/administer-copilot/manage-for-enterprise/manage-agents/prepare-for-custom-agents
