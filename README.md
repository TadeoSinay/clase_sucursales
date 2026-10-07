# Bóvedas: del pronóstico a la decisión

Material de clase interactivo para **Investigación Operativa (I4051 · UTN FRBA)**.
Toma un problema real de un banco (proyectar el efectivo de cada sucursal y decidir
cuánto mover, cuándo y por dónde) y lo conecta con las **clases 15 a 20** del repo
[invo.py](https://github.com/TadeoSinay/invo.py): LP, Simplex, Flujo de Mínimo Costo,
Dijkstra, transporte, supply chain, planificación y programación entera.

> ⚠ **Todo es ficticio.** Montos, tarifas, coberturas, clientes y la serie del gráfico
> son inventados con fines didácticos. El gráfico conserva la forma de una proyección
> real, pero la escala es arbitraria y **los montos están tapados**. Los nombres de las
> transportadoras se usan solo como ejemplo, con tarifas inventadas.

## Cómo se usa

Abrí [`index.html`](index.html) en el navegador. Es un único archivo y no necesita
servidor. Funciona sin conexión salvo la tipografía, que se baja de Google Fonts.

## Qué hay en cada solapa

| Solapa | Qué muestra |
|---|---|
| **1 · La lógica** | **La bóveda animada.** Un cliente comercial (marca ficticia) trae bolsos y los deposita por ventanilla; la plata sale por caja, por ATM y por el camión de caudales. Cada uno tiene su **palanca**. Se ven en vivo el saldo, el stock de seguridad (1,10 × mínimo histórico), el tope y el **costo ocioso** (saldo × TNA/365). <br>**Mapa AMBA por comuna:** envíos desde el Tesoro Central con o sin **abono** (el costo del viaje se imputa a la sucursal). <br>**Mapa de provincias:** camión, avión o combinado, con Brinks, Prosegur o Transportadora del Interior. Muestra costo básico, variable (camión: monto × v × km; avión: % del monto) y sobrecargo por **octopacks** que exceden la franquicia. El ranking de rutas es **Dijkstra**. <br>**¿Y si no lo muevo?** Despliega una **cadena de Markov** (bóveda → tránsito → destino) que compara el costo ocioso de dejar la plata parada con el costo de moverla y calcula el día de equilibrio. |
| **2 · La proyección y el simulador** | El gráfico del **Transformer cuantílico** (historia y zoom de la proyección con banda) para la **Sucursal X**, con los montos tapados. Al costado está el **simulador**: con el percentil de cobertura elegido, decide **cuánto mover, cuándo y hacia dónde** (mini mapa). Resuelve exacto el problema de lote dinámico con costo fijo, compara contra “remesa diaria”, “una sola remesa” y “no mover”, y permite ver cómo le hubiera ido al plan **con lo que pasó en realidad**. |
| **3 · ¿Qué tiene que ver con la materia?** | Una tarjeta por clase (15 a 20) con dónde aparece cada tema, una pregunta para disparar la discusión y los links al material de *invo.py*. También tiene el **MILP completo**, el código **PuLP** escrito con el estilo de las notebooks del curso y una **red de transporte con transbordo** interactiva (Flujo de Mínimo Costo) entre varias sucursales. |

## Relación con las clases 15–20

| Clase | Tema en *invo.py* | Dónde aparece en la bóveda |
|---|---|---|
| 15 | Intro a optimización, LP por método gráfico, PuLP | Variables de decisión (remesas), FO (ocioso + movimiento), restricciones (SS ≤ saldo ≤ tope) |
| 16 | Casos particulares en método gráfico, Simplex con tablas | Empates de rutas = óptimos múltiples |
| 17 | Variables ficticias, casos particulares en Simplex | `saldo ≥ SS` necesita variable artificial. Tope insuficiente da un problema **no factible**, y el simulador lo muestra |
| 18 | Flujo de Mínimo Costo: camino más corto | Cada envío es un camino Tesoro → aeropuerto → sucursal |
| 19 | Dijkstra, transporte | Ranking de rutas (Dijkstra); red de sucursales que sobran y que faltan (transporte) |
| 20 | Supply chain, planificación de la producción, programación entera | Balance de bóveda = balance de stock; Tesoro como nodo de transbordo; básico y abono como costo fijo (x ≤ M·y); octopacks enteros; cobertura de transportadoras como set cover |

## Guion sugerido

1. Bóveda: romper el stock de seguridad con las palancas. ¿Cuál es la única palanca que decidimos nosotros?
2. AMBA: prender y apagar el abono. ¿Por qué con abono conviene ir todos los días?
3. Provincias: Salta con Brinks (no llega) y Orán (sin aeropuerto), donde aparece el combinado con Transportadora del Interior.
4. “¿Y si no lo muevo?”: cadena de Markov y día de equilibrio `d* = costo de mover / (monto × TNA/365)`.
5. Proyección: pasar de P50 a P95 y discutir cuánto cuesta la cobertura. Ver “qué pasó con lo real”.
6. Cierre: escribir entre todos el MILP y resolver la red del día.
