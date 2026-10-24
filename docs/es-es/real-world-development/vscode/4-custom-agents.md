---
title: "Ejercicio 4: Agentes personalizados"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

## ¿Qué son los agentes personalizados?

Los [agentes personalizados][custom-agents-concept] de GitHub Copilot son asistentes de IA especializados que puedes adaptar a tareas o ámbitos concretos del flujo de desarrollo. Se definen mediante archivos Markdown en la carpeta `.github/agents` del repositorio. Puedes proporcionar al agente instrucciones específicas, prácticas recomendadas, patrones de código y conocimientos del dominio para que realice determinados tipos de trabajo con mayor eficacia. Los equipos pueden convertir su experiencia en agentes reutilizables, como un agente de accesibilidad que compruebe el cumplimiento de [WCAG][wcag], uno de seguridad que siga prácticas de programación segura o uno de pruebas que mantenga patrones de prueba coherentes.

Los agentes personalizados se definen en archivos Markdown dentro de `.github/agents` en el proyecto o, de forma global, en `~/.copilot/agents`. Cada archivo incluye metadatos YAML con, como mínimo, los campos `name` y `description`, seguidos de instrucciones en Markdown que definen el comportamiento, la experiencia y las directrices del agente.

### Diferencias entre los agentes personalizados y las habilidades de agente

Los agentes personalizados y las [habilidades de agente][agent-skills-concept] tienen algunas similitudes: ambos se definen principalmente en archivos Markdown e indican a una IA cómo realizar tareas. Una forma sencilla de distinguirlos es que un **agente personalizado** realiza el trabajo y las **habilidades** son herramientas.

Los agentes personalizados tienen su propia ventana de contexto y coordinan habilidades, e incluso otros agentes, para completar el trabajo. En este taller, el agente personalizado de accesibilidad revisa y actualiza el sitio de acuerdo con las directrices de accesibilidad. Como parte de esa tarea, podría utilizar habilidades para gestionar solicitudes de incorporación de cambios o para ejecutar y gestionar pruebas.

> [!NOTE]
> No existe una única manera correcta de crear un agente personalizado. Como ocurre con cualquier herramienta de IA, prueba y ajusta el agente para adaptarlo a tu entorno y tus escenarios.

[custom-agents-concept]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
[agent-skills-concept]: https://docs.github.com/copilot/concepts/agents/about-agent-skills
[wcag]: https://www.w3.org/WAI/standards-guidelines/wcag/

## Escenario

Tailspin Toys quiere que su plataforma de financiación colectiva sea accesible para todas las personas, independientemente de sus capacidades visuales o preferencias. Algunos usuarios han indicado que el tema oscuro actual es difícil de leer porque el contraste entre el texto y el fondo es insuficiente. Para resolverlo, el equipo de diseño ha solicitado un modo de alto contraste que se pueda activar y desactivar.

En este ejercicio:

- Revisarás un agente personalizado de accesibilidad existente.
- Utilizarás el agente de accesibilidad en Copilot Chat para implementar un modo de alto contraste.

## Revisa el agente personalizado de accesibilidad

Ya se ha creado un agente personalizado para las tareas de accesibilidad. Revisarás su contenido para saber cómo orientará a Copilot. Vuelve al codespace, abre un terminal y crea una rama nueva a partir de `main` para separar el trabajo de accesibilidad de la PR de filtrado del ejercicio 3:

```bash
git checkout main
git pull
git checkout -b accessibility-vscode
```

1. Abre `.github/agents/accessibility.md`.
2. Revisa los campos `name` y `description` de los metadatos YAML.

> [!CAUTION]
> Los campos `name` y `description` son obligatorios en los metadatos de un agente personalizado.

3. Revisa las secciones siguientes, que describen:
   - Las responsabilidades principales al generar código para un sitio web accesible.
   - Las prácticas recomendadas de accesibilidad.
   - Ejemplos de código HTML, CSS y JavaScript.
   - Errores frecuentes y cómo evitarlos.

## Utiliza el agente personalizado en Copilot Chat

VS Code muestra todos los agentes personalizados definidos en `.github/agents` en el selector de agentes situado en la parte inferior de la vista Copilot Chat. Puedes seleccionar uno para que sus instrucciones y herramientas rijan la sesión.

> [!TIP]
> **Abre Copilot Chat**
>
> Antes de empezar, vuelve al codespace, abre el panel Copilot Chat y selecciona **New Chat** para iniciar una conversación nueva. La selección de modo y modelo varía según el ejercicio; cada paso indicará cuándo cambiarla.

1. Si todavía no está seleccionado, selecciona **Agent** en el selector de agentes de la vista Chat.

   ![Selector del agente en la vista Chat](../../../_images/shared-chat-mode-selector.png)

2. Selecciona el selector de agentes situado en la parte inferior de la vista Chat. Muestra el agente activo; de forma predeterminada, es **default**.
3. Selecciona **Accessibility agent** en la lista de agentes disponibles.
4. Envía este mensaje al agente de accesibilidad:

    ```plaintext
    Añade al sitio un modo de alto contraste. Debe haber un selector para que los usuarios puedan activar el alto contraste, y la opción debe conservarse al volver a cargar la página mediante el almacenamiento local del navegador.
    ```

5. Copilot Chat explorará el código, propondrá cambios y editará los archivos del proyecto. Cada edición aparecerá en el chat con la ruta del archivo y las diferencias para que puedas revisarlas.
6. A medida que se apliquen cambios, el indicador **Files changed** mostrará los archivos modificados durante la sesión.

> [!NOTE]
> El proceso puede tardar unos minutos. Copilot realizará cambios en el repositorio: modificará componentes Astro, CSS y pruebas relacionadas, según sea necesario.

En el siguiente ejercicio revisarás y orientarás el trabajo en curso.

## Resumen y pasos siguientes

Has explorado los [agentes personalizados][custom-agents], asistentes de IA especializados en tareas y ámbitos concretos. Te permiten convertir los conocimientos y estándares del equipo en agentes reutilizables que orientan el trabajo de Copilot.

Has explorado estos conceptos:

- Cómo se definen los agentes personalizados.
- Cómo utilizar un agente personalizado en el modo agente de Copilot Chat.

A continuación, [supervisarás y orientarás el trabajo del agente][next-lesson], revisarás los cambios mientras se producen y añadirás un selector de modo claro a la misma sesión.

## Recursos

- [Acerca de los agentes personalizados][custom-agents]
- [Crear agentes personalizados en el IDE][creating-custom-agents-ide]
- [Agentes personalizados en VS Code][custom-agents-vscode]
- [Configuración de agentes personalizados][custom-agents-config]
- [Agentes personalizados en awesome-copilot][awesome-copilot-agents]

---

| [← Lección anterior: Probar la funcionalidad con el servidor Playwright MCP][previous-lesson] | [Siguiente lección: Supervisar y gestionar agentes →][next-lesson] |
|:--|--:|

[previous-lesson]: ../3-mcp/
[next-lesson]: ../5-managing-agents/
[custom-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
[creating-custom-agents-ide]: https://docs.github.com/copilot/how-tos/use-copilot-agents/cloud-agent/create-custom-agents-in-your-ide
[custom-agents-vscode]: https://code.visualstudio.com/docs/copilot/customization/custom-agents
[custom-agents-config]: https://docs.github.com/copilot/reference/custom-agents-configuration
[awesome-copilot-agents]: https://github.com/github/awesome-copilot/tree/main/agents
