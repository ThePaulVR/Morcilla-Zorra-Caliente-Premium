# 🚨 ES-Alert Gran Canaria · Sala de guardia

Simulador educativo para entender las decisiones que hay detrás de un ES-Alert: **¿cuándo avisar y a quién?** Eres jefe o jefa de guardia de Emergencias de Gran Canaria durante un temporal. Interpreta el radar y los avisos, decide qué municipios alertar y defiende tu gestión ante la prensa.

> ⚠️ Juego en desarrollo. Todos los datos de lluvia, avisos y cifras son **ficticios**. No envía alertas reales ni sustituye a 112 Canarias ni a AEMET.
> Dudas o fallos: **itsnotungofa** en Discord.

Inspirado en [ES-Alert Simulator](https://esalert-simulator.com/) (Cataluña).

## Cómo se juega

1. **Elige modo** en la pantalla de inicio:
   - **Elegir episodio**: aleatorio, un aviso que se queda en nada, temporal moderado o temporal intenso.
   - **Solo redactar alertas**: editor de mensajes con vista previa, sin partida.
2. **Empieza tu turno.** Cada partida tiene un turno distinto: día de lunes a viernes, hora de inicio entre las 06:00 y las 22:00 y duración de 8 a 18 horas. Tienes que cumplirlo entero. La partida empieza en pausa.
3. **Observa la situación:**
   - El radar muestra la lluvia en mm/h sobre los 21 municipios. Con los botones de −2 h a +3 h ves el pasado y el pronóstico, que puede fallar.
   - Hay avisos ficticios de **AEMET** (cada 6 h) y de **112 Canarias** (cada 3 h, desfasado) en tres zonas: norte y medianías, cumbres, y este, sur y oeste. Los niveles son verde, amarillo, naranja y rojo, y las fuentes a veces no coinciden.
   - Puedes pausar el reloj y cambiar la velocidad (x0,5 a x3).
4. **Selecciona municipios** en el mapa y pulsa **Revisar y enviar ES-Alert**. En la ventana de revisión eliges el nivel (1 aviso, 2 alerta, 3 confinamiento), ajustas las poblaciones y lees las advertencias (horario escolar, no llueve, fuentes en desacuerdo, alerta repetida…). Si quieres, puedes ver la alerta saltar en pantalla con sonido.
5. **Mira las reacciones.** La gente opina en redes según avisaste a tiempo, tarde, sin sentido o no avisaste, y eso mueve tu **credibilidad**.
6. **Al terminar el turno** ves el resumen (puntuación, víctimas, aislados, coste, falsas alarmas, incidentes y portadas de prensa) y pasas a la **rueda de prensa**: 4 preguntas con 4 respuestas cada una. Según tu gestión y tus respuestas, **continúas, dimites o te cesan**.

### Puntuación

| Situación en un municipio inundado | Puntos |
|---|---|
| Avisado con 30 min o más de antelación | +100 |
| Entre 10 y 30 min | +60 |
| Menos de 10 min | +20 |
| Sin aviso, o aviso tardío | −100 |

- **Falsa alarma** (alerta sin inundación): −15, −30 o −50 según el nivel (1, 2 o 3).
- Un aviso de **nivel 1** cuenta como si tuviera el 40 % de la antelación.
- Si no hay inundaciones y no alertas en vano: +50.
- El resultado se multiplica según el episodio: ×0,8 (aviso que se queda en nada), ×1 (temporal localizado), ×1,15 (frente extenso).

### Modo susto 😱

En el editor puedes elegir el modo «Susto»: tras unos segundos de espera aparece de repente una alerta a pantalla completa con sonido fuerte y sacudida. Úsalo solo con quien sepa que es una broma y baja antes el volumen.

## Cómo está hecho

- **Un único `index.html`** con HTML, CSS y JavaScript sin frameworks ni dependencias (solo la tipografía Barlow de Google Fonts). Se puede abrir directamente en el navegador o alojar en cualquier servidor estático.
- **Mapa:** SVG con los límites de los 21 municipios de Gran Canaria. Cada municipio es un `<path>` clicable. Fuente del SVG: [indicar autor y licencia].
- **Radar de lluvia:** un campo continuo calculado con celdas gaussianas que se desplazan en el tiempo, más una llovizna de fondo. Se dibuja en un `<canvas>` a baja resolución, recortado a la forma de la isla con una máscara y suavizado. Los avisos, las advertencias y los municipios inundados salen del mismo campo.
- **Simulación:** cada episodio genera su turno, sus tormentas y los errores del pronóstico. Los avisos de AEMET y 112 Canarias se calculan a partir del pronóstico, con actualizaciones y desfases distintos.
- **Consecuencias:** las cifras de víctimas, aislados y coste dependen de la población aproximada de cada municipio, la intensidad de la lluvia y la antelación del aviso. Las reacciones en redes y los titulares se generan con plantillas de texto.
- **Sonido:** el MP3 de alerta va incrustado en la página y se reproduce con la API Web Audio. El modo susto lo amplifica con un limitador y le añade una sirena sintetizada.
- **Datos locales:** la mejor puntuación y la credibilidad se guardan en `localStorage`. No se recoge ningún dato.
- **Desarrollo:** creado de forma iterativa con ayuda de Claude (Anthropic) a partir de capturas y referencias del ES-Alert Simulator catalán.

## Limitaciones y próximos pasos

- Las fronteras vienen de un SVG y las poblaciones son aproximadas. Todo lo demás es ficticio.
- Pendiente: reto diario y ranking compartido, cuando el juego esté alojado en un servidor propio.

## Créditos

- Inspiración: [ES-Alert Simulator](https://esalert-simulator.com/).
