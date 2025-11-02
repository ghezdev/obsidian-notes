# 1) Camino “golden path” (evita el pantano de opciones)

- **Versionado**: instalen **Unity Hub** y usen **la última versión LTS** (estabilidad > features nuevas).
    
- **Render pipeline**: **URP** (Universal Render Pipeline). HDRP sólo si buscan gráfico AAA (más curva).
    
- **Plantilla 3D URP** + paquetes:
    
    - **New Input System**, **TextMeshPro**, **Cinemachine**, **ProBuilder**, **Post-processing** (URP), **Addressables**.
        
    - (Opcionales que aceleran): **DOTween** (tweens/animaciones UI), **NavMesh Components**, **Unity Test Framework**.
        
- **Estructura de carpetas** (desde el día 0):

```
Assets/
  Art/ (Models, Textures, Materials, Animations)
  Audio/ (SFX, Music)
  Code/
    Runtime/   (código de juego)
    Editor/    (herramientas editor)
    Tests/     (playmode/editmode)
    Shared/    (utilidades)
  Data/
    ScriptableObjects/ (balancing, catálogos, loot tables)
    Addressables/ (escenas y bundles)
  Prefabs/
  Scenes/
    Boot.unity
    MainMenu.unity
    Game.unity
  UI/
```


- **Patrones**: **ScriptableObjects** para datos configurables (balance), **Eventos** (C# events + SO), **Composición por componentes** (eviten herencias profundas), **State Machines** simples para enemigos/jugador.
    

---

# 2) Reparto de roles (y cómo no pisarse)

- **Dev A – Gameplay/Feel**: control del jugador, cámara (Cinemachine), enemigos, FX (DOTween), UI in-game.
    
- **Dev B – Tech/Infra**: Addressables, escenas, build pipeline, tests, performance budgets, integración con backend IA.
    
- **Dev C – Contenido/UX**: niveles con ProBuilder/ProGrids, menús, HUD, flujos (menu → partida → resultados).
    

> Roten **PM semanal/QA** (1 persona por semana arma el sprint, define criterios de aceptación y aprueba PRs).

---

# 3) IA en desarrollo y en gameplay (sin fricción)

**Gameplay (in-engine)**

- **NavMesh + FSM/BT** para NPCs.
    
- **Director de dificultad**: ScriptableObject con curvas; ajusta spawns/velocidad por “stress score” del jugador.
    
- **ML-Agents (cuando toque)**: primero prototipen con reglas; luego entrenan un agente para 1 comportamiento concreto (e.g., esquivar).
    

**IA “exógena” (LLM/TTS/STT)**

- **Microservicio** (Node/Fastify o Python) que expone `/npc/reply`, `/quest/generate`.
    
- Unity **NO** llama al proveedor directamente; llama a su **backend** (clave segura, cache, moderación).
    
- **Streaming**: mostrar respuestas token a token en subtítulos/diálogos; seguir el juego aunque no llegue aún la respuesta.
    

---
# 5) Productividad: cómo multiplicarla x2–x3

**A. Editor & IDE**

- Usen **Rider** (mejor integración con Unity) o VS Code con C# Dev Kit.
    
- Atajos: **Prefab Variants**, **Timeline** para secuencias rápidas, **Cinemachine** para cámaras pro sin código.
    

**B. Paquetes que ahorran tiempo**

- **DOTween**: animaciones UI, feedback (sin coroutines kilométricas).
    
- **Addressables**: carga diferida de escenas/assets, reduce tiempos de build y permite parchar contenido.
    
- **NavMesh Components**: horneado runtime si cambian geometría.
    

**C. Asset Store con criterio**

- Buscar **“template de género”** (top-down shooter, runner, platformer) para estudiar y/o partir desde ahí.
    
- Usar **kits modulares** (input, pooling, UI) en lugar de “engines” cerrados.
    
- Arte **low-poly** coherente: permite calidad aceptable con perf alta.
    

**D. Automatización**

- **GameCI / Unity Builder** en GitHub Actions: build por PR, smoke tests, export WebGL/Windows/Android.
    
- **Playmode tests**: mínimo 2–3 tests de “arranca, entra al juego, el jugador se mueve, se puede pausar”.
    

**E. Telemetría mínima**

- Logueen: FPS promedio, duración de partida, muertes por causa, abandono en tutorial.
    
- Exporten a CSV o a un endpoint propio; deciden balance con datos, no intuición.
    

**F. Design-tech**

- **ScriptableObjects + Addressables** → balancean sin recompilar.
    
- **Catálogos** (armas, enemigos, ítems) en SO y **tablas** (CSV/Google Sheets → import) para diseñar fuera del código.
    
- **Eventos** (C#) para desacoplar UI/Gameplay (HUD escucha “OnScoreChanged”).
    

---

# 6) Plan realista de 4 semanas (de cero a algo jugable)

**Semana 1 — Fundaciones**

- Proyecto URP, paquetes básicos, estructura carpetas, Escenas Boot/MainMenu/Game.
    
- Control del jugador + cámara (Cinemachine) + 1 enemigo con FSM simple.
    
- Addressables configurado. Build local estable.
    

**Semana 2 — Loop jugable**

- Spawner + DirectorConfig (curvas de dificultad).
    
- HUD (vida, score), pausa, resultados.
    
- 1 nivel con ProBuilder.
    
- Telemetría mínima (duración partida, muertes, FPS).
    

**Semana 3 — IA de valor**

- Backend IA (endpoint `/npc/reply`) + diálogo en streaming in-game.
    
- “Asistente” (hint system) con cooldown.
    
- Balance por datos (tocar ScriptableObjects, no código).
    
- Primeros tests (arranque + ganar/perder).
    

**Semana 4 — Pulido y rendimiento**

- 60 fps target: batching, LOD, texturas comprimidas.
    
- UX: tutorial de 60s, vibración/feedback, audio básico.
    
- CI/CD: build WebGL/Windows en cada release tag.
    
- Demo jugable a amigos + feedback → backlog v2.
    

---

# 7) Errores comunes que matan tiempo (y cómo evitarlos)

- **Querer “sistema perfecto” al principio** → vayan por **juego que divierta** y refactoricen.
    
- **No usar ScriptableObjects** → todo queda “horneado” en código.
    
- **Física y mallas complejas** sin necesidad → comiencen con colliders simples (capsule/box).
    
- **Cargar todo al inicio** → **Addressables** y pantallas de carga breves.
    
- **LLM en cada frame** → orquesten server-side, cacheen, usen streaming y respuestas prefetch.
    

---

# 8) Qué sí aprenderán “rápido” en Unity (y vale la pena)

- **Cinemachine/Timeline** (nivel cinematográfico sin programar cámaras).
    
- **URP + post-FX**: calidad/performances decentes.
    
- **NavMesh + FSM**: IA útil sin RL.
    
- **ScriptableObjects + Addressables**: flujo moderno de contenido.
    
- **Pipelines de build**: PC/WebGL/Android sin dolor.