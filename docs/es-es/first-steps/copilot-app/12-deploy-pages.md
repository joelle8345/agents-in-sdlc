---
title: "Lección 12: Publica el sitio con GitHub Pages"
description: "Utiliza la aplicación GitHub Copilot para configurar un flujo de trabajo de Pages, revisar su solicitud de incorporación de cambios y verificar el Space Quiz publicado."
authors:
  - jamesmontemagno
lastUpdated: 2026-10-12
---

Publica el Space Quiz con GitHub Pages para que tenga un localizador uniforme de recursos (URL) público. Copilot puede preparar el flujo de trabajo y guiar la publicación, pero tú eres responsable de revisar los cambios y confirmar que el sitio está disponible.

En esta lección:

- Pedirás a Copilot que configure una publicación con GitHub Pages.
- Revisarás el flujo de trabajo y la solicitud de incorporación de cambios antes de integrarlos.
- Supervisarás la publicación y verificarás el sitio publicado.

## Escenario

El Space Quiz ya está en un repositorio de GitHub, pero quienes quieran probarlo necesitan una forma sencilla de acceder. Publicar el sitio de un solo archivo con GitHub Pages permite ofrecerlo mediante una URL pública sin añadir un servidor ni dependencias de ejecución.

## Pide a Copilot que publique el sitio

En la sesión de la aplicación Copilot para `space-quiz`, envía este mensaje:

```plaintext
Habilita GitHub Pages para este repositorio. Crea un flujo de trabajo de GitHub Actions que compile el sitio si es necesario y lo publique en GitHub Pages. Añade un archivo README que describa la aplicación y cómo ejecutarla localmente si todavía no existe. Crea una solicitud de incorporación de cambios con estos cambios e intégrala cuando se superen las comprobaciones obligatorias. Supervisa la publicación hasta que se complete correctamente y, después, indica la URL final del sitio. Si no tienes permiso para habilitar Pages o integrar la solicitud, dime exactamente qué tengo que aprobar o hacer. No indiques que se ha publicado correctamente hasta que el sitio esté disponible.
```

![Diagrama de tres etapas: una solicitud de incorporación de cambios de space-quiz integrada; una ejecución correcta de Deploy website en GitHub Actions con los pasos Build website, Upload artifact y Deploy to Pages; y el Space Quiz publicado en tu-dominio.github.io/space-quiz/.](../../../_images/first-steps-app-pages-deploy.svg)

> [!WARNING]
> Este mensaje pide al agente que cree e integre una solicitud de incorporación de cambios y modifique la configuración de Pages del repositorio. Revisa las diferencias, los permisos de publicación y cualquier solicitud de aprobación de GitHub antes de continuar.

## Revisa el flujo de trabajo y verifica la publicación

1. Confirma que el archivo README solo se añada si el repositorio todavía no tiene uno.
2. Revisa los cambios de la solicitud de incorporación, incluidos los pasos de compilación y publicación del flujo de trabajo.
3. Integra los cambios solo cuando se superen las comprobaciones obligatorias de la solicitud.
4. Sigue la ejecución de publicación de GitHub Actions hasta que se complete correctamente.
5. Abre la URL indicada y confirma que se carga el Space Quiz.

Si el agente no puede habilitar Pages ni integrar la solicitud de incorporación de cambios, sigue las instrucciones concretas que te proporcione. No des la tarea por completada hasta que la publicación se complete correctamente y el sitio esté disponible.

## Resumen y pasos siguientes

El Space Quiz ya está disponible como sitio publicado y has verificado la publicación en lugar de confiar únicamente en lo que indica el agente. Continúa con [Lección 13: Repaso y pasos siguientes][next-lesson].

[next-lesson]: ../13-review/
