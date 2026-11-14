# 01 - Requerimientos

**Proyecto:** Martian Map
**Equipo:** The Cluster Devs
**Reto:** [Interplanetary Survival Guide: Martian Map](https://www.spaceappschallenge.org/2026/), NASA Space Apps Challenge 2026
**Estado:** listo (14 nov 2026)

## 1. Resumen y propuesta

Vamos a hacer una app web para planear y seguir una caminata de un astronauta (Marswalk) en el cráter Jezero, juntando en un solo mapa al menos tres tipos de datos de NASA y una ruta segura calculada sobre el terreno.

El reto pide un mapa, herramienta o interfaz que un astronauta pueda usar en una misión de superficie en Marte. Pide que se combinen datos de varias misiones, que se piense primero en la seguridad de la tripulación y, si se puede, que haya una ruta que esquive obstáculos.

Elegimos Jezero porque Perseverance lleva años ahí. Eso nos da imágenes desde órbita en alta resolución, modelos de elevación y más de un millón de fotos tomadas desde el suelo.

**Objetivo científico de la misión ficticia:** recorrer el frente del delta de Jezero para tomar muestras de rocas sedimentarias donde pudo haber agua, siguiendo puntos que Perseverance ya visitó.

## 2. Alcance

**Entra:**

- Una sola zona: el frente del delta de Jezero, de unos pocos kilómetros.
- Mapa con capas de NASA que se prenden y apagan.
- Ruta entre puntos de interés calculada con la pendiente del terreno.
- Fotos reales de Perseverance ligadas a los puntos de la ruta.
- Panel de condiciones (clima y radiación) con datos históricos o de referencia.

**No entra:**

- Datos en tiempo real desde Marte (no existen públicos con esa latencia).
- Todo el planeta o varias zonas.
- App nativa de tablet o un HUD real en un casco. Si da tiempo, se simula en el navegador.
- Cuentas de usuario e inicio de sesión.

## 3. Usuarios y escenarios

| Usuario | Dónde lo usa | Qué necesita |
| --- | --- | --- |
| Tripulación en el hábitat | Pantalla grande o laptop | Ver la zona con todas las capas, elegir puntos, revisar la ruta y aprobar la salida |
| Astronauta en campo | Tablet o vista tipo HUD | Saber dónde está, cuál es el siguiente punto, cuánto falta y si hay algún riesgo |

**Escenario A, planeación:** la tripulación abre el mapa de Jezero, activa la capa de pendiente y la de minerales, marca tres puntos de muestreo y pide la ruta. La app traza el camino evitando pendientes fuertes, muestra distancia y tiempo estimado, y deja ver la foto de Perseverance de cada punto antes de salir.

**Escenario B, en campo:** el astronauta sigue la ruta aprobada. La vista le dice el siguiente punto, la distancia y el rumbo, y le avisa si se sale del camino o si se acerca a una zona marcada como peligrosa.

## 4. Requerimientos funcionales

Los "Debe" son el mínimo para entregar; si el domingo a las 14:00 no están, se deja todo lo demás.

| ID | Requerimiento | Prioridad |
| --- | --- | --- |
| RF-01 | Mostrar el mapa base de Jezero con zoom y desplazamiento, usando el mosaico de Mars Trek | Debe |
| RF-02 | Prender y apagar al menos tres capas de datos de distinto tipo (óptica, topográfica y espectral o térmica), con opacidad ajustable | Debe |
| RF-03 | Colocar, mover y borrar puntos de interés (muestra, descanso, peligro) en el mapa | Debe |
| RF-04 | Calcular una ruta entre los puntos que evite pendientes mayores al límite configurado | Debe |
| RF-05 | Mostrar distancia total, desnivel y tiempo estimado de la ruta | Debe |
| RF-06 | Al tocar un punto, ver fotos de Perseverance tomadas cerca de ahí con su sol, cámara y fecha | Debe |
| RF-07 | Panel de condiciones: temperatura, presión y radiación de referencia para la hora de la caminata | Debería |
| RF-08 | Perfil de elevación de la ruta (gráfica de altura contra distancia) | Debería |
| RF-09 | Modo campo: siguiente punto, distancia, rumbo y alerta si se sale de la ruta | Debería |
| RF-10 | Guardar y cargar un plan de caminata (puntos y ruta) | Debería |
| RF-11 | Vista 3D del terreno para revisar la ruta desde otro ángulo | Podría |
| RF-12 | Simulación en primera persona tipo HUD siguiendo la ruta aprobada | Podría |
| RF-13 | Ruta para dos astronautas o con apoyo de un rover que cargue equipo | Podría |

## 5. Requerimientos no funcionales

| ID | Requerimiento | Cómo lo revisamos |
| --- | --- | --- |
| RNF-01 | Corre en Chrome y en una tablet sin instalar nada | Abrir la URL publicada en una laptop y en un celular |
| RNF-02 | El mapa carga en menos de 5 s con buena conexión | Pestaña Network del navegador |
| RNF-03 | El cálculo de ruta tarda menos de 3 s en la zona elegida | Medir con console.time |
| RNF-04 | Funciona si una API de NASA falla: los datos de la zona se guardan antes en el repo | Desconectar internet y abrir la demo |
| RNF-05 | Texto legible y botones grandes para usarse con guantes (mínimo 44 px de toque) | Revisión visual en celular |
| RNF-06 | Toda la interfaz en inglés, porque el demo se juzga en inglés | Revisión antes de grabar |
| RNF-07 | Cada capa dice de qué misión e instrumento viene | Revisión del panel de capas |
| RNF-08 | Publicada en una URL pública | Abrir desde un dispositivo que no sea del equipo |

## 6. Datos de NASA

El reto sugiere al menos tres tipos de datos; vamos con seis para tener margen si alguno no se puede usar a tiempo.

| Tipo | Fuente | Para qué la usamos |
| --- | --- | --- |
| Óptico | Mosaicos HiRISE y CTX de Jezero en [Mars Trek (WMTS)](https://trek.nasa.gov/tiles/apidoc/trekAPI.html?body=mars) | Mapa base |
| Topográfico | Modelos de elevación (DTM) de CTX y HiRISE de Jezero en [USGS Astrogeology STAC](https://stac.astrogeology.usgs.gov/docs/tutorials/mosaic_json) | Calcular pendiente, ruta y perfil de elevación |
| Geológico | [Mapa fotogeológico del sitio de aterrizaje de Perseverance](https://pmc.ncbi.nlm.nih.gov/articles/PMC7116714) | Elegir los puntos de muestreo del delta |
| Espectral / térmico | Mapas de minerales de CRISM e inercia térmica de THEMIS (revisar cuáles están en Mars Trek) | Ubicar rocas interesantes y zonas de arena suelta |
| Imágenes de superficie | [Galería de raw images de Perseverance](https://mars.nasa.gov/mars2020/multimedia/raw-images/) | Fotos de cada punto (Navcam, Mastcam-Z, Hazcam) |
| Atmosférico / radiación | Datos de MEDA (Perseverance) y RAD (Curiosity) en el PDS | Panel de condiciones con valores de referencia |

Notas para el equipo de datos:

- Los identificadores exactos de cada capa de Mars Trek salen de su archivo GetCapabilities; la página del API no los lista.
- Jezero está en 18.41° N, 77.69° E. Ese es el centro para recortar todo.
- Bajar y guardar en el repo un recorte pequeño del DTM y la lista de fotos, para no depender de internet en la demo (RNF-04).

## 7. Restricciones

- **Tiempo:** el hackathon es del 14 al 15 de noviembre; el envío cierra el domingo a las 23:59 hora local.
- **Datos:** solo se pueden usar datos abiertos de NASA u otras agencias espaciales. No hay datos de Marte en tiempo real.
- **Idioma:** el demo se evalúa en inglés, así que la interfaz y los textos de la app van en inglés.
- **Demo:** video de máximo 30 segundos o máximo 7 diapositivas, en un link público.
- **Costo:** todo con herramientas y servicios gratuitos.
- **Equipo:** seis personas, con las computadoras que traigamos a la sede.

## 8. Supuestos y dependencias

**Supuestos:**

- El astronauta camina con traje y con equipo encima, así que no puede subir pendientes fuertes.
- La tripulación planea la caminata con tiempo, antes de salir, y no sobre la marcha.
- Las fotos de Perseverance y los datos de órbita representan bien cómo está el terreno hoy.
- Los valores de clima y radiación son de referencia; no predicen el día real de la caminata.

**Dependencias:**

- Mars Trek debe estar en línea para mostrar las teselas del mapa.
- La galería de raw images de Perseverance debe seguir publicando sus metadatos.
- Los modelos de elevación de USGS deben poder descargarse antes del domingo.
- La sede debe tener internet estable para bajar datos y publicar la app.

## 9. Glosario

| Término | Significado |
| --- | --- |
| Marswalk | Caminata de un astronauta fuera del hábitat, en la superficie de Marte |
| Jezero | Cráter de Marte donde aterrizó Perseverance; tuvo un lago y tiene un delta de río |
| Delta | Depósito de sedimentos que dejó un río al entrar al lago |
| Sol | Un día marciano, unas 24 h 40 min |
| DTM | Modelo digital de terreno: una cuadrícula con la altura de cada punto |
| Pendiente | Qué tan inclinado está el terreno, en grados |
| Tesela | Pedazo cuadrado de imagen con el que se arma el mapa al hacer zoom |
| WMTS | Estándar para pedir teselas de un mapa por internet |
| HiRISE / CTX | Cámaras de la sonda Mars Reconnaissance Orbiter |
| CRISM | Espectrómetro de la misma sonda; detecta minerales |
| THEMIS | Cámara térmica de la sonda Mars Odyssey |
| MEDA | Estación meteorológica de Perseverance |
| RAD | Detector de radiación de Curiosity |
| HUD | Información proyectada en el visor del casco |
| Punto de interés | Lugar marcado en el mapa: muestra, descanso o peligro |

## 10. Entregables para Space Apps

El envío cierra el domingo 15 de noviembre a las 23:59 hora local; nuestra meta interna es tenerlo enviado a las 22:00.

- [ ] Página del proyecto llenada en la pestaña Project del equipo.
- [ ] Demo: video de máximo 30 segundos con subtítulos en inglés, o máximo 7 diapositivas en inglés contando la portada. ([guía de envío](https://www.spaceappschallenge.org/resources/project-submission-guide/))
- [ ] El demo va en un link público (YouTube, Drive o GitHub).
- [ ] Las diapositivas o el video dicen nombre del equipo, nombres de los integrantes y el reto elegido.
- [ ] Explicar qué datos de NASA usamos y cómo (sección 6).
- [ ] Link a la app publicada y al repo de GitHub.

## 11. Pendientes por decidir

- [x] Zona: Jezero.
- [ ] ¿Quién toma cada rol?
- [ ] ¿Pendiente máxima para la ruta? Proponemos empezar con 15° y dejarla configurable.
- [ ] ¿Demo en video o en diapositivas?
- [ ] ¿Vale la pena la vista 3D y el HUD (RF-11 y RF-12), o nos quedamos en 2D bien hecho?
