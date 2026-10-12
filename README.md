# Imperio Español — Nivel 1: «La Orilla»

Prototipo jugable del nivel de acción en tercera persona ambientado en el siglo XVI: un conquistador
desembarca de una chalupa en una playa caribeña y debe abrirse paso hasta asegurar el borde de la jungla
frente a los guerreros defensores de la isla (lanceros y arqueros taínos).

## Cómo ejecutarlo

Opción directa: abre `index.html` con doble clic en Chrome, Edge o Safari (requiere internet la primera
vez para cargar Three.js desde CDN).

Opción con servidor local (recomendada):

```bash
cd "Imperio Español"
python3 -m http.server 8765
# luego visita http://127.0.0.1:8765
```

## Controles

| Entrada | Acción |
|---|---|
| `W A S D` | Movimiento en 3D |
| Ratón | Cámara en tercera persona (puntero bloqueado) |
| `Shift` | Correr |
| `Espacio` | Saltar |
| Clic izquierdo | Ataque con espada ropera (combo de dos golpes) |
| Clic derecho (mantener) | Bloqueo con rodela (reduce el daño frontal ~85 %) |
| `F` | Grito de guerra **«¡¿Dónde está el oro?!»** (voz sintetizada) |
| `Esc` | Pausa |

## Mecánicas del nivel

- **Objetivo principal**: eliminar a los 10 defensores repartidos en tres grupos (playa, sendero y borde
  de la jungla) para asegurar la posición.
- **Grito de guerra (`F`)**, con 9 s de recarga:
  - Intimida a los guerreros en un radio de 14 m, que retroceden unos segundos.
  - Revela con un haz dorado los **3 tesoros enterrados** en un radio de 32 m (objetivo secundario;
  recogerlos restaura 25 puntos de vigor).
- **Combate**: la ropera encadena combo frontal en arco; la rodela bloquea ataques de lanza y flechas
  que lleguen de frente. El vigor se regenera lentamente si no recibes daño durante 6 s.
- **Enemigos**: los lanceros cargan cuerpo a cuerpo con telegrafiado de golpe; los arqueros mantienen
  la distancia y disparan flechas con trayectoria balística.

## Apartado visual

Estilo realista estilizado con iluminación de atardecer tropical: sol bajo cálido sobre el mar con
sombras largas, cielo con degradado y disco solar en shader, agua con oleaje y espuma dinámica en la
orilla más reflejo especular del sol, niebla cálida, partículas de arena al correr, hojas al golpear y
destellos dorados en los tesoros.

## Nota sobre el contenido

Es una obra de ficción histórica interactiva. Los guerreros de la isla se representan como defensores
de su territorio, que es su papel histórico real frente a las expediciones de conquista. Las figuras
son deliberadamente estilizadas y sin gore.

## Tecnología

Three.js r160 (ES modules + import map) en un único `index.html` autocontenido, sin dependencias de
compilación: terreno analítico compartido por render y física, vegetación instanciada con texturas de
lienzo generadas en tiempo de ejecución, shaders propios para cielo/agua/partículas y audio 100 %
sintetizado con WebAudio. El grito «¡¿Dónde está el oro?!» pronuncia la frase de verdad —un motor de
fonemas propio encadena DÓN-DE ES-TÁ EL O-RO con vocales por formantes, consonantes de ruido, garra
por saturación, capa demoníaca una octava abajo y sub-bajo—, con eco aterrador por reverb de
convolución y una sacudida de cámara; el mar se atenúa mientras retumba el eco.

## Hooks de depuración

La consola del navegador expone `window.__imperio` para pruebas: `start()`, `teleport(x,z)`,
`look(yaw,pitch)`, `attack()`, `shout()`, `heal()`, `state()`, `enemies()` y `near(x,z,tipo)`.

## Puente a Unity/Godot

Para llevarlo a un motor comercial, la estructura se traduce directa: la función `terrainHeight(x,z)`
define la altura del terreno, `SQUADS` la distribución de enemigos y los objetos `player`/`enemies[]`
los controladores de combate e IA.
