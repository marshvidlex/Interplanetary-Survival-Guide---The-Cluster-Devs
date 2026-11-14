# 02 - Historias de usuario

**Estado:** listo (14 nov 2026)

## 1. Cómo leer este documento

Son 16 historias en 4 épicas. Las 8 marcadas como "Debe" suman 29 puntos y son lo mínimo para entregar. Cada historia dice de qué requerimiento viene ([requerimientos](../01-requerimientos/README.md)).

**Formato:** Como [usuario], quiero [acción], para [beneficio]. Hay dos usuarios: la **tripulación**, que planea en el hábitat, y el **astronauta**, que camina afuera.

**Puntos:** escala 1, 2, 3, 5, 8. Miden cuánto pesa una historia comparada con las otras, no son horas exactas. Una historia de 1 punto es algo chico, como mostrar un texto. Una de 8 es lo más pesado del proyecto y conviene partirla si se puede.

**Una historia está terminada cuando:**

- Cumple todos sus criterios de aceptación.
- Funciona en Chrome de laptop y de celular.
- Está en `main` por pull request revisado por otra persona.
- Los textos que ve el usuario están en inglés.

## 2. Épica 1: mapa y capas

### HU-01 Ver el mapa de la zona

Como tripulación, quiero ver el mapa del delta de Jezero y moverme con zoom, para ubicar dónde va a ser la caminata.

RF-01 · Debe · 3 puntos

- [ ] Al abrir la app, el mapa aparece centrado en el delta de Jezero.
- [ ] El zoom y el arrastre funcionan con mouse y con el dedo.
- [ ] El mapa carga en menos de 5 segundos con buena conexión.

### HU-02 Prender y apagar capas

Como tripulación, quiero prender y apagar capas de datos y cambiar su opacidad, para ver solo la información que necesito en ese momento.

RF-02 · Debe · 5 puntos

- [ ] Hay al menos tres capas de tipos distintos: óptica, topográfica (pendiente) y espectral o térmica.
- [ ] Cada capa se activa y desactiva sin recargar la página.
- [ ] Cada capa tiene un control de opacidad de 0 a 100 %.

### HU-03 Saber de dónde viene cada capa

Como tripulación, quiero ver de qué misión e instrumento viene cada capa, para saber qué tan confiable es lo que estoy viendo.

RNF-07 · Debe · 1 punto

- [ ] Cada capa muestra la misión, el instrumento y la resolución.

## 3. Épica 2: planeación de la ruta

### HU-04 Marcar puntos de interés

Como tripulación, quiero marcar puntos en el mapa y decir de qué tipo son, para armar el plan de la caminata.

RF-03 · Debe · 3 puntos

- [ ] Al tocar el mapa se agrega un punto.
- [ ] Cada punto puede ser de muestra, descanso o peligro, y cada tipo tiene un ícono distinto.
- [ ] Un punto se puede mover arrastrándolo y se puede borrar.
- [ ] Los puntos de muestra y descanso se numeran en el orden en que se visitan.

### HU-05 Calcular una ruta segura

Como tripulación, quiero que la app calcule una ruta entre los puntos que evite pendientes peligrosas, para que el astronauta no se arriesgue con el traje y el equipo.

RF-04 · Debe · 8 puntos

- [ ] La ruta pasa por todos los puntos de muestra y descanso, en orden.
- [ ] Ningún tramo de la ruta pasa la pendiente máxima.
- [ ] La ruta no entra a las zonas marcadas como peligro.
- [ ] Si no hay camino posible, aparece un mensaje que lo dice y sugiere subir la pendiente o mover un punto.
- [ ] La ruta tarda menos de 3 segundos en calcularse.

### HU-06 Ajustar la pendiente máxima

Como tripulación, quiero cambiar la pendiente máxima permitida, para adaptar la ruta a la condición del astronauta y al equipo que lleva.

RF-04 · Debe · 2 puntos

- [ ] Hay un control de pendiente máxima que empieza en 15°.
- [ ] Al cambiar el valor, la ruta se vuelve a calcular.

### HU-07 Ver los datos de la ruta

Como tripulación, quiero ver la distancia, el desnivel y el tiempo estimado de la ruta, para decidir si la caminata cabe en el tiempo disponible.

RF-05 · Debe · 2 puntos

- [ ] Se muestra la distancia total en metros o kilómetros.
- [ ] Se muestra cuánto se sube y cuánto se baja en total.
- [ ] Se muestra el tiempo estimado según la velocidad de caminata configurada.
- [ ] Los datos se actualizan cada vez que cambia la ruta.

### HU-08 Ver el perfil de elevación

Como tripulación, quiero ver una gráfica de altura contra distancia de la ruta, para saber en qué tramos el astronauta va a subir.

RF-08 · Debería · 3 puntos

- [ ] La gráfica aparece debajo de los datos de la ruta.
- [ ] Al pasar el cursor por la gráfica se marca ese lugar en el mapa.

### HU-09 Guardar y cargar un plan

Como tripulación, quiero guardar un plan de caminata con nombre y abrirlo después, para no repetir la planeación.

RF-10 · Debería · 3 puntos

- [ ] Un plan guarda sus puntos, la pendiente máxima y la ruta.
- [ ] Hay una lista de planes guardados y al elegir uno se carga en el mapa.

## 4. Épica 3: información del sitio

### HU-10 Ver fotos de Perseverance de un punto

Como tripulación, quiero ver fotos reales que tomó Perseverance cerca de un punto, para saber cómo se ve el lugar antes de llegar.

RF-06 · Debe · 5 puntos

- [ ] Al tocar un punto se abre un panel con las fotos tomadas cerca de ahí.
- [ ] Cada foto muestra el sol, la cámara y la fecha.
- [ ] Una foto se puede ampliar.
- [ ] Si no hay fotos cerca, el panel lo dice en lugar de quedarse vacío.

### HU-11 Ver las condiciones del lugar

Como tripulación, quiero ver la temperatura, la presión y la radiación de referencia para la hora de la caminata, para decidir a qué hora conviene salir.

RF-07 · Debería · 3 puntos

- [ ] El panel muestra temperatura, presión y radiación con sus unidades.
- [ ] Al cambiar la hora de salida, los valores cambian.
- [ ] El panel dice que son valores de referencia y de qué instrumento vienen.

## 5. Épica 4: modo campo y extras

En Marte no hay GPS. En la demo, la posición del astronauta se simula avanzando sobre la ruta.

### HU-12 Saber a dónde ir

Como astronauta, quiero ver cuál es el siguiente punto, a qué distancia está y en qué dirección, para no perderme durante la caminata.

RF-09 · Debería · 5 puntos

- [ ] La vista muestra el nombre del siguiente punto, la distancia y el rumbo.
- [ ] Al llegar a un punto, la vista pasa sola al siguiente.
- [ ] Los botones miden al menos 44 px para usarse con guantes.

### HU-13 Recibir alertas

Como astronauta, quiero que la app me avise si me salgo de la ruta o me acerco a una zona de peligro, para corregir a tiempo.

RF-09 · Debería · 3 puntos

- [ ] Aparece una alerta si la posición se aleja de la ruta más de la distancia configurada.
- [ ] Aparece una alerta al acercarse a un punto de peligro.
- [ ] La alerta se ve aunque el astronauta esté en otra parte de la pantalla.

### HU-14 Ver el terreno en 3D

Como tripulación, quiero ver la ruta sobre el terreno en 3D, para entender mejor las subidas y los obstáculos.

RF-11 · Podría · 8 puntos

- [ ] La ruta se dibuja sobre el relieve real del DTM.
- [ ] La cámara se puede girar y acercar.

### HU-15 Simular la caminata en primera persona

Como tripulación, quiero ver una simulación desde el casco del astronauta siguiendo la ruta aprobada, para ensayar la caminata antes de salir.

RF-12 · Podría · 8 puntos

- [ ] La cámara avanza sobre la ruta a la altura de los ojos.
- [ ] Encima se ve el HUD con el siguiente punto, la distancia y las alertas.

### HU-16 Planear con rover o en pareja

Como tripulación, quiero planear la caminata para dos astronautas o con un rover que cargue el equipo, para hacer más ciencia en una sola salida.

RF-13 · Podría · 8 puntos

- [ ] Se puede elegir caminata sola, en pareja o con rover.
- [ ] Con rover, la pendiente máxima y el tiempo se calculan con los límites del rover.

## 6. Resumen y trazabilidad

Todos los RF tienen al menos una historia. El total es de 70 puntos: 29 Debe, 17 Debería y 24 Podría.

| ID | Historia | Viene de | Prioridad | Puntos | Estado |
| --- | --- | --- | --- | --- | --- |
| HU-01 | Ver el mapa de la zona | RF-01 | Debe | 3 | Por hacer |
| HU-02 | Prender y apagar capas | RF-02 | Debe | 5 | Por hacer |
| HU-03 | Saber de dónde viene cada capa | RNF-07 | Debe | 1 | Por hacer |
| HU-04 | Marcar puntos de interés | RF-03 | Debe | 3 | Por hacer |
| HU-05 | Calcular una ruta segura | RF-04 | Debe | 8 | Por hacer |
| HU-06 | Ajustar la pendiente máxima | RF-04 | Debe | 2 | Por hacer |
| HU-07 | Ver los datos de la ruta | RF-05 | Debe | 2 | Por hacer |
| HU-08 | Ver el perfil de elevación | RF-08 | Debería | 3 | Por hacer |
| HU-09 | Guardar y cargar un plan | RF-10 | Debería | 3 | Por hacer |
| HU-10 | Ver fotos de Perseverance | RF-06 | Debe | 5 | Por hacer |
| HU-11 | Ver las condiciones del lugar | RF-07 | Debería | 3 | Por hacer |
| HU-12 | Saber a dónde ir | RF-09 | Debería | 5 | Por hacer |
| HU-13 | Recibir alertas | RF-09 | Debería | 3 | Por hacer |
| HU-14 | Ver el terreno en 3D | RF-11 | Podría | 8 | Por hacer |
| HU-15 | Simular la caminata en primera persona | RF-12 | Podría | 8 | Por hacer |
| HU-16 | Planear con rover o en pareja | RF-13 | Podría | 8 | Por hacer |

Orden sugerido: HU-01 y HU-04 primero, porque todo lo demás se dibuja sobre el mapa y los puntos. HU-05 es la más pesada y la más importante, así que debe arrancar cuanto antes.

## 7. Pendientes

- [ ] Revisar en equipo los puntos de cada historia.
- [ ] Definir la velocidad de caminata con traje para el tiempo estimado (HU-07).
- [ ] Definir a qué distancia de la ruta se dispara la alerta de desvío (HU-13).
- [ ] Asignar un responsable a cada historia "Debe".
- [ ] Crear un issue en GitHub por historia, con sus criterios de aceptación como checklist.
