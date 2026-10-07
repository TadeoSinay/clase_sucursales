# Bóvedas: del pronóstico a la decisión

Material de clase interactivo para **Investigación Operativa (I4051 · UTN FRBA)**.
Toma un problema real de un banco (proyectar el efectivo de cada sucursal y decidir
cuánto mover, cuándo y por dónde) y lo resuelve con las herramientas de optimización
de la materia: LP, Flujo de Mínimo Costo, Dijkstra, transporte, planificación,
programación entera y cadenas de Markov.

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
| **1 · La lógica** | **La bóveda animada.** Un cliente comercial (marca ficticia) trae bolsos y los deposita por ventanilla. La plata sale por caja, por ATM y por el camión de caudales, y cada uno tiene su **palanca**. El camión lleva o trae remesas desde tres **salidas**: el **CIB** (Centro Interdepósito de Billetes, costo $0), **otra sucursal** u **otro banco**. Se ven en vivo el saldo, el stock de seguridad (1,10 × mínimo histórico), el tope, el **costo ocioso** (saldo × TNA/365) y el costo de mover. El **modo foto** congela la escena en **bóveda vacía** o **bóveda llena**, con la explicación de qué pasa, qué cuesta y qué hacer dentro de la misma imagen. <br>**Mapa AMBA por comuna:** envíos desde el Tesoro Central con o sin **abono** (el costo del viaje se imputa a la sucursal). <br>**Mapa de provincias:** camión, avión o combinado, con Brinks, Prosegur o Transportadora del Interior. Muestra costo básico, variable y sobrecargo por **octopacks**. El ranking de rutas es **Dijkstra**. <br>**¿Y si no la muevo?** Arma una **cadena de Markov absorbente** con todas las salidas (quedarse, CIB, otra sucursal, otro banco y los tránsitos). Muestra la matriz en forma canónica, π<sub>n</sub>, la matriz fundamental N = (I − Q)⁻¹, la probabilidad de terminar en cada salida, el costo esperado y el día de equilibrio. |
| **2 · La proyección y el simulador** | El gráfico del **Transformer cuantílico** (historia y zoom de la proyección con banda) para la **Sucursal X**, con los montos tapados. Al costado está el **simulador**: con el percentil de cobertura elegido, decide **cuánto mover, cuándo y hacia dónde** (mini mapa). Resuelve exacto el problema de lote dinámico con costo fijo, compara contra “remesa diaria”, “una sola remesa” y “no mover”, y permite ver cómo le hubiera ido al plan **con lo que pasó en realidad**. |
| **3 · El modelo formal** | El **MILP** de remesas completo, el código **PuLP** escrito con el estilo de las notebooks del curso y una **red de transporte con transbordo** interactiva (Flujo de Mínimo Costo) entre varias sucursales. |
