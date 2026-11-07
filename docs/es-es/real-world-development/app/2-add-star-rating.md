---
title: "Lección 2 - Añade valoraciones con estrellas: una mejora rápida"
description: "Inicia tu primera sesión de agente en la aplicación GitHub Copilot, haz un pequeño cambio en las tarjetas de juegos y combínalo en tu primera solicitud de incorporación de cambios."
authors:
  - geektrainer
lastUpdated: 2026-10-22
---

Ahora que has explorado el espacio de trabajo y usado un chat rápido, es el momento de iniciar una **sesión de agente** y hacer tu primer cambio en el proyecto. Será pequeño: los juegos ya incluyen una valoración con estrellas en sus datos, pero aún no se muestra en las tarjetas de la página de inicio. Pedirás al agente que la muestre, revisarás el cambio y lo combinarás como tu primera solicitud de incorporación de cambios.

En esta lección:

- iniciarás una sesión de agente y aprenderás cómo se estructura.
- pedirás al agente que haga un cambio pequeño y acotado en el proyecto.
- revisarás el cambio en la vista de diferencias del espacio de trabajo.
- ejecutarás la aplicación localmente para confirmar el cambio en el navegador.
- abrirás y combinarás tu primera solicitud de incorporación de cambios.

## Escenario

Cada juego de Tailspin Toys puede tener una valoración con estrellas, que ya aparece en la página de detalles del juego. Sin embargo, las tarjetas de juegos de la página de inicio solo muestran el título, la categoría, la editorial y la descripción. Como ejercicio inicial, pedirás al agente que muestre en cada tarjeta la valoración existente: un cambio pequeño y autónomo, perfecto para tu primera sesión.

## Anatomía de una sesión

Una **sesión** es una conversación con un agente que se ejecuta en su propio espacio de trabajo aislado. Cada sesión tiene su propio **worktree y rama de Git**, lo que permite ejecutar varias a la vez —por ejemplo, una para añadir una función y otra para corregir un error— sin que sus cambios entren en conflicto. Las sesiones aparecen en la barra lateral, agrupadas por repositorio. Selecciona una para cambiar a ella.

En una sesión verás tres elementos: la **conversación** con el agente, la **actividad de las herramientas** que usa para explorar y editar archivos, y la lista de **archivos modificados** con sus diferencias.

## Inicia una sesión y solicita el cambio

Inicia una sesión nueva para explorar el proyecto e implementar la funcionalidad. Durante la [configuración de la aplicación][prior-lesson], añadiste el proyecto desde su repositorio de GitHub. Crea una sesión para ese repositorio y solicita el cambio.

1. Vuelve a la aplicación GitHub Copilot o ábrela.
2. Selecciona **+** en la parte superior de la barra lateral para iniciar una sesión.
3. Selecciona `tailspin-toys` como repositorio.
4. Elige un **new working tree** y el modo **Interactive** debajo del cuadro del prompt. Usa este prompt para solicitar el cambio:

   ```plaintext
   Show each game's starRating out of 5 in the game cards on the list page. If the rating is null, show "No rating yet". Keep the card layout as it is, add tests, and run the relevant checks.
   ```

5. Pulsa <kbd>Enter</kbd> para enviar el prompt a Copilot.

La aplicación Copilot empieza por crear un worktree nuevo, una copia aislada del proyecto. Después, explora el proyecto, localiza los archivos que debe actualizar para añadir la funcionalidad y crea el código necesario. ¡Ya has añadido una función con la aplicación Copilot!

## Revisa las diferencias

Todas las modificaciones generadas por IA se deben revisar antes de combinarlas, aunque sean pequeñas. Revisa los cambios aquí mismo, en la aplicación Copilot.

1. En la esquina superior derecha de la aplicación, selecciona **Toggle review panel**. En el panel que se abre, selecciona **Changes** para ver los archivos modificados y sus diferencias.

   ![Barra de herramientas superior de la aplicación GitHub Copilot con una flecha que señala el botón Toggle review panel, a la derecha de Create PR](../../../_images/app-2-review-panel.png)

2. Deberías ver código añadido a `GameCard.astro`, el archivo principal que se usa para mostrar los detalles de los juegos. Debería parecerse a este bloque, que muestra la valoración cuando existe y utiliza `No rating yet` cuando `starRating` es `null`:

   ```astro
   {game.starRating !== null ? (
       <span class="text-xs font-medium px-2.5 py-0.5 rounded bg-amber-900/60 text-amber-300" data-testid="game-rating">
           ★ {game.starRating} / 5
       </span>
   ) : (
       <span class="text-xs font-medium text-slate-500" data-testid="game-rating-empty">
           No rating yet
       </span>
   )}
   ```

> [!NOTE]
> Copilot, como todas las herramientas de IA generativa, es probabilístico, no determinista, por lo que el código exacto puede variar. Sin embargo, debería ser parecido al ejemplo.

## Comprueba los cambios

Revisa los resultados de las comprobaciones automatizadas del agente antes de abrir un navegador. Confirma que las pruebas cubren una valoración numérica de `starRating` y el caso alternativo `null`. Si falta un requisito previo o se omite una comprobación, no cuentes la tarea como superada; revisa cualquier solicitud de instalación antes de aprobarla.

No basta con leer el código y dar por hecho que funciona. Pide a Copilot que abra el sitio web para poder examinar la interfaz de usuario (UI) actualizada. Para ello, inicia el sitio y ábrelo en un lienzo de navegador.

> [!TIP]
> Un lienzo es un widget interactivo integrado en la aplicación Copilot. Más adelante explorarás lienzos personalizados e incluso crearás uno. Por ahora, usarás el lienzo de navegador integrado.

1. Usa este prompt para pedir a Copilot que inicie la aplicación y abra la página en el lienzo de navegador:

   ```plaintext
   Start the app and open it in the browser canvas.
   ```

2. En unos instantes, se iniciará la aplicación y se abrirá una ventana del navegador dentro de la aplicación Copilot.
3. Confirma que las tarjetas de juegos con valoración muestran su puntuación sobre cinco.
4. Cuando termines, pide a Copilot que detenga el servidor de desarrollo que ha iniciado para esta sesión y cierre el lienzo de navegador:

   ```plaintext
   Stop the dev server and close the browser canvas.
   ```

## Abre y combina tu primera solicitud de incorporación de cambios

Ya has creado la funcionalidad. Ahora crearás una solicitud de incorporación de cambios (PR) para combinar el código nuevo con el código existente.

1. Selecciona **Create PR** en la esquina superior derecha.
2. Si se te solicita, selecciona **Sign in with your browser** y sigue las indicaciones para autenticarte.
3. Si Copilot explica que la directiva del repositorio exige vincular una incidencia antes de crear la PR, confirma que debe seguir ese proceso.
4. Copilot empezará a crear la PR.
5. Selecciona la burbuja **PR** situada justo encima del chat para abrir la solicitud en el panel de revisión. Puedes revisar la PR desde allí.
6. Cuando esté lista, selecciona **Ready to merge**.
7. En el cuadro de diálogo nuevo, selecciona **Merge pull request** para combinarla.

## Resumen y próximos pasos

¡Enhorabuena! Has publicado tu primer cambio con la aplicación GitHub Copilot. En concreto, has:

- iniciado una sesión de agente y aprendido cómo se estructuran las sesiones.
- indicado al agente que hiciera un cambio pequeño y acotado en las tarjetas de juegos.
- revisado el cambio en la vista de diferencias del espacio de trabajo.
- ejecutado la aplicación localmente para confirmar la valoración con estrellas en el navegador.
- abierto la PR 1, revisado sus comprobaciones y autorizado explícitamente su combinación.

A continuación, [partirás de la incidencia de filtrado y usarás los modos Plan y Autopilot][next-lesson] para desarrollar una función más amplia.

## Recursos

- [Trabajar con sesiones de agente en la aplicación GitHub Copilot][agent-sessions]
- [Acerca de la aplicación GitHub Copilot][about-copilot-app]
- [Gestionar incidencias y solicitudes de incorporación de cambios con la aplicación GitHub Copilot][managing-issues-prs]

[prior-lesson]: ../1-install-copilot-app/#instala-y-configura-la-aplicación-github-copilot
[next-lesson]: ../3-agent-modes/
[agent-sessions]: https://docs.github.com/copilot/how-tos/github-copilot-app/agent-sessions
[about-copilot-app]: https://docs.github.com/copilot/concepts/agents/github-copilot-app
[managing-issues-prs]: https://docs.github.com/copilot/how-tos/github-copilot-app/managing-issues-and-pull-requests
