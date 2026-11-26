# A Dark Room: análisis de seguridad client-side de un juego web · client-side security analysis of a web game

![Type](https://img.shields.io/badge/type-personal%20project-8957e5)
![Topics](https://img.shields.io/badge/topics-reverse%20engineering%20%C2%B7%20client--side%20trust%20%C2%B7%20logic%20abuse-informational)
![Language](https://img.shields.io/badge/JavaScript-DevTools%20console-F7DF1E?logo=javascript&logoColor=black)

📄 **Artículo completo (español) · Full write-up (Spanish): [a-dark-room.md](a-dark-room.md)**

[Link to a-dark-room github page](https://github.com/doublespeakgames/adarkroom/tree/main)

---

## **ES** · Resumen

*A Dark Room* es un juego minimalista de navegador. Tras terminarlo con 3.990.770 puntos, quise entenderlo por dentro: cómo está construido, cómo gestiona su estado y hasta qué punto se puede manipular desde el navegador.

**Qué hice**

- Leí y mapeé los scripts del juego (`state-manager.js`, `world.js`, `path.js`, `events.js`, `fabricator.js`, `ship.js`, `perks.js`) para reconstruir su arquitectura.
- Encontré el **State Manager** global (`$SM`) y lo usé desde la consola de DevTools para modificar cualquier valor guardado.
- Disparé eventos narrativos a mano, eliminé los límites de peso, agua y vida en el mapa, desbloqueé la cadena de perks y automaticé las mejoras de la nave con bucles.
- Llegué a un estado de cabañas infinitas que rompió la economía del juego: puntuación final **3.263.351.856**, unas **817×** la partida original.

**Conceptos de seguridad que practiqué**

| Concepto | Cómo aparece en el juego |
|---|---|
| Confianza en el cliente | Toda la lógica y el estado viven en el navegador |
| Falta de validación | No se comprueban rangos ni tipos, así que se aceptan estados imposibles |
| API interna expuesta | Las funciones críticas se pueden llamar desde la consola |
| Ingeniería inversa ligera | Reconstruir las dependencias a partir de código ajeno |
| Desincronización DOM / estado | La interfaz lee el DOM, no el estado real |
| Explotación de la lógica | Saltarse requisitos y generar recursos ilimitados |

**Conclusión:** son los mismos patrones (confiar en el cliente, no validar en el servidor, exponer funciones) que en aplicaciones web reales generan vulnerabilidades.

---

## **EN** · Summary

*A Dark Room* is a minimalist browser game. After finishing it with a score of 3,990,770, I wanted to understand it from the inside: how it is built, how it manages its state and how far that state can be manipulated from the browser.

**What I did**

- Read and mapped the game's scripts (`state-manager.js`, `world.js`, `path.js`, `events.js`, `fabricator.js`, `ship.js`, `perks.js`) to reconstruct its architecture.
- Found the global **State Manager** (`$SM`) and used it from the DevTools console to change any stored value.
- Triggered narrative events by hand, removed weight, water and health limits on the map, unlocked the perk chain and automated the ship upgrades with loops.
- Reached an infinite-huts state that broke the game's economy: final score **3,263,351,856**, about **817×** the original run.

**Security concepts practised**

| Concept | How it shows up in the game |
|---|---|
| Client-side trust | All logic and state live in the browser |
| Missing input validation | No ranges or types are checked, so impossible states are accepted |
| Exposed internal API | Critical functions are callable from the console |
| Lightweight reverse engineering | Rebuilding dependencies from someone else's code |
| DOM / state desync | The UI reads the DOM, not the real state |
| Business-logic abuse | Skipping requirements and generating unlimited resources |

**Takeaway:** the same patterns (trusting the client, no server-side validation, exposed functions) appear in real web applications and lead to real vulnerabilities.

---

← [github.com/nievesnu](https://github.com/nievesnu)
