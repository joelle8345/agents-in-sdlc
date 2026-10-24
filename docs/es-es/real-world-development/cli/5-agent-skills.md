---
title: "Lección 5: Personalizar y utilizar la habilidad quality-checks"
description: "Explora la habilidad quality-checks existente, personaliza el formato de su informe y utilízala para validar el filtrado."
authors:
  - geektrainer
lastUpdated: 2026-09-29
---

Desarrollar código implica algo más que escribirlo. Ya has comprobado manualmente que funciona y has utilizado archivos de instrucciones para asegurarte de que respeta los estándares. Ahora verás cómo se ejecutan las pruebas, el lint y otras partes de la integración continua (CI).

Las **habilidades de agente** son adecuadas para estas tareas. Ayudan a Copilot a comprender cómo ejecutar operaciones repetibles.

En esta lección:

- Explorarás la habilidad `quality-checks` existente.
- Personalizarás el formato de los resultados.
- Volverás a cargar y ejecutar la habilidad.

## Escenario

Tailspin Toys utiliza la habilidad `quality-checks` para las pruebas unitarias, el lint y las comprobaciones de tipos. El equipo quiere mejorar el informe para que los resultados sean más fáciles de leer.

## Instrucciones, scripts y recursos

Las habilidades de agente reúnen instrucciones reutilizables para tareas, scripts ejecutables y recursos auxiliares que el agente carga cuando los necesita. En esencia, son carpetas que contienen un archivo Markdown llamado `SKILL.md`. El archivo incluye metadatos con el nombre y la descripción de la habilidad, una descripción general y directrices sobre cuándo debe utilizarse. La carpeta también puede incluir scripts y otros recursos.

> [!NOTE]
> No es obligatorio añadir carpetas ni archivos adicionales. La habilidad `quality-checks` de Tailspin Toys solo contiene `SKILL.md`, porque utiliza los comandos existentes del proyecto.

Las habilidades pueden guardarse en `.github/skills` para que sean recursos compartidos y reutilizables del repositorio, o en la carpeta de habilidades del usuario, `~/.copilot/skills`.

## Explora la habilidad

Explora la habilidad `quality-checks` que el equipo de Tailspin Toys ha creado para ejecutar pruebas unitarias, lint y comprobaciones de tipos.

1. Vuelve al codespace. En el editor de Codespaces, abre `.github/skills/quality-checks/SKILL.md`.
2. Lee los campos `name` y `description` de la parte superior. La descripción ayuda a Copilot a decidir cuándo utilizar la habilidad.
3. Lee las instrucciones y fíjate en cómo guían a Copilot durante las pruebas y el lint.
4. Observa que todavía no hay ninguna sección **Results output formatting**.

## Ejecuta la habilidad antes de hacer cambios

Las habilidades se pueden invocar directamente desde Copilot CLI o mediante lenguaje natural. Pide a Copilot que ejecute las tres comprobaciones de la habilidad.

1. Vuelve a la conversación de filtrado en modo Interactive.
2. Envía este mensaje:

   ```plaintext
   Ejecuta la habilidad quality-checks para las pruebas unitarias, el lint y las comprobaciones de tipos.
   ```

3. Revisa el informe final.

## Personaliza el informe

Mejorarás el informe para que indique qué se ha ejecutado, si se ha completado correctamente y qué resultados han proporcionado las herramientas.

1. Vuelve a `.github/skills/quality-checks/SKILL.md`.
2. Añade esta sección al final del archivo:

   ```markdown
   ## Results output formatting

   Upon completion, report each command that ran and whether it passed, failed, or was blocked. Include test counts, durations, errors, warnings, and other metrics only when the tool reports them. Identify the next action for any failure or blocker, and never describe a skipped or incomplete check as passed.
   ```

3. El archivo se guarda automáticamente.

## Ejecuta la habilidad actualizada

Copilot CLI puede volver a cargar las habilidades editadas sin reiniciar la conversación. Comprueba el nuevo formato del informe.

1. Introduce:

   ```plaintext
   /skills reload
   ```

2. Envía el mismo mensaje que antes:

   ```plaintext
   Ejecuta la habilidad quality-checks para las pruebas unitarias, el lint y las comprobaciones de tipos.
   ```

3. Revisa el informe final y compáralo con el primero.

## Resumen y pasos siguientes

Has personalizado y utilizado una habilidad de agente existente. En esta lección:

- Has explorado la habilidad `quality-checks` para las pruebas unitarias, el lint y las comprobaciones de tipos.
- Has personalizado el formato de los resultados.
- Has vuelto a cargar y ejecutado la habilidad.

Este cambio acompañará al filtrado en la PR de la funcionalidad. A continuación, permitirás que Copilot interactúe directamente con el sitio mediante el servidor Playwright del Model Context Protocol (MCP) en la [lección siguiente][next-lesson].

## Más ejemplos de habilidades

Estos ejemplos de la comunidad son referencias, no tareas adicionales:

- [Especificación de Agent Skills][skill-spec]
- [Flujo de contribución: `make-repo-contribution`][contribution-example]
- [Documentos de requisitos: `prd`][prd-example]
- [Diagramas y script de exportación incluido: `drawio`][drawio-example]
- [Pruebas en el navegador: `webapp-testing`][browser-example]

[previous-lesson]: ../4-custom-instructions/
[next-lesson]: ../6-mcp-playwright/
[skill-spec]: https://agentskills.io/specification
[contribution-example]: https://github.com/github/awesome-copilot/tree/main/skills/make-repo-contribution
[prd-example]: https://github.com/github/awesome-copilot/tree/main/skills/prd
[drawio-example]: https://github.com/github/awesome-copilot/tree/main/skills/drawio
[browser-example]: https://github.com/github/awesome-copilot/tree/main/skills/webapp-testing
