# Training_Big_Data
Entrenamiento Big Data 
#TALLER 2: 

Modelamiento de las ventas por sus clientes y articulos en sus diferentes paises

"GRAFICA RESULTADO DEL TALLER AVANZADO 2"
https://github.com/cahupara/Training_Big_Data/issues/1#issue-438581693

##1.Creación de premisas a nivel de datos y de metadatos

__1.1.Cambiar Nombres a las tablas__ 
Esto se hace en modo __diseño__, donde se visualizan las tablas al costado derecho de la heraamienta, alli se da clic derecho sobre cada una de las tablas, clic en __Renombrar__, se colocan nombres como: Clientes, Productos, Ventas, Promociones, Paises y Fechas

__1.2.Crear relación entre las tablas__
Se da clic en la pestaña de relaciones y se eliminan las lineas que realizan las uniones entre las  tablas, luego el modelo que se crea es un modelo estrella, en donde la tabla Ventas, queda rodeada de las otras tablas y se unen con su llave unica, es decir, Productos y Ventas se unen por el campo __Llave del producto__, Clientes y Ventas se unen por el campo __llave del clientes__, Paises y Ventas se unen por el campo __Llave del territorio de ventas__, Promociones y Ventas se unen por el campo __llave de Promociones__ y por ultimo se une la tabla de Fechas con Ventas por el campo __llave de fecha__

__1.3.Integrar el nombre y el apellido del cliente__
Para esto se ingresa a la opción de edición de consultas, se da clic en la tabla de los clientes que se encuentra en el listado de la parte izquierda, luego de los datos que se visualicen se resaltan las columnas correspondientes a __Primer Nombre__ y __Apellido__, luego se da clic en la parte superior en __Agregar Columnas__, para finalizar clic en __Mezclar columnas__. De esta forma se observa una columna al final con los valores integrados. Para que los cambios se guarden, se debe dar clic en __inicio__ luego en __Cerrar y Aplicar__; de esta forma la columna queda lista para usarse en la construnnión de los reportes

__1.4.Creación de tabla Indicadores__
Esta se crea dando clic en __Modelando__ luego clic en __Agregar Tabla__, esta tabla se visualizará en modo diseño, en la parte derecha, con las tablas previamente cargadas, su objetivo es tener almacenadas las formulaciones requeridas

__1.5. Creación de formulas__ 
Para sumar las cantidades vendidas, se da clic derecho sobre la tabla Indicadores y clic en __nueva metrica__, aqui se coloca como nombre __quantity__ y su opeacion es __sum(Ventas[OrderQuantity])__, enter
Para sumar las ventas valorizadas, mismo proceso de __nueva metrica__, el nombre es __sales__ y su operacion es __sum(Ventas[SalesAmount])__, enter
Para sumar los costos, __nueva metrica__, el nombre es __cost__ y su operacion es sum(Ventas[TotalProductCost]), enter
Para calcular el margen, __nueva metrica__, el nombre es __margin__ y su operacion es ([sales]-[cost]) / [sales]

__1.6. Formato de las formulas__
Cantidad, venta y costo se parametrizan como numero entero, para esto se debe resaltar cada una de esta formulas, clic en __Modelando__ del menu, luego clic en la opcion de Formato, se escoge __número entero__, sin decimales y clic en el separador de miles.
Margen se parametriza como un decimal, misma ruta, se selecciona __porcentaje__ y se coloca un decimal

__1.7.Filtro de Promociones__ 
En modo diseño, se arrastra el visualizador __Slicer__ al lienzo en blanco, luego de la tabla de Promociones, se arrastra el campo llamado __nombre promocion en ingles__, a la opción celda de los parametros que se encuentran en la parte inferior de los visualizadores

__1.8.Filtro de Años__
Mismo proceso anterior con el __Slicer__, el campo que se arrastra es el de la __fecha de la orden__ de la tabla Ventas __(Ventas[orderdate])__

__1.9.Filtro de Estado Civil__
Mismo proceso con el __Slicer__, el campo que se arrastra es __(Clientes[maritalstatus])__, de la tabla Clientes

__1.10.Filtro de Numero de Hijos__
Mismo proceso con el __Slicer__, el campo que se arrastra es __(Clientes[totalchildren])__, de la tabla Clientes

__1.11.Tacómetro para el Análisis del Margen__
Se arrastra al lienzo, el visualizador llamado __Gauge__, luego de la tabla Indicadores se arrastra la formula del Margen al campo Valor de los parametros

__1.12.Gráfico de Lineas para Analizar la demanda de las bicicletas por color y el género de los clientes__
Se arrastra al lienzo, el visualizador llamado __Line chart__, parametrizandose asi: Axis=(productos[color]), Legend=(clientes[gender]) y en Values=(indicadores[sales])

__1.13.Gráfico de Dispersión para evaluar la venta por pais, haciendo relación entre el costo, la venta y el margen__
Se arrastra al lienzo, el visualizador llamado __Scatter chart__, parametrizandose de la siguiente forma: Legend=(paises[salesterritorycountry]), X Axis= (indicadores[margin]), Y Axis= (indicadores[sales]) y en Size=(indicadores[cost])
En la opción de __Analitica__, se habilita una linea constante con un valor de 0.409 para el eje X (valor porcentaje mínimo de rentabilidad); se habilita una linea constante en el eje Y con un valor de 1500000 (valor de venta minima)

__1.14.Gráfico de Concentración de las ventas por nivel de Educación y Ocupación de los clientes__
Se arrastra al lienzo, el visualizador llamado __Treemap__, parametrizandose asi: group=(clientes[englisheducation]) y debajo de este campo se arrastra (clientes[englishoccupation]); Value=(indicadores[sales])
Este grafico permite hacer drill down, primero sobre el nivel educativo y dentro de este que ocupacion tienen los clientes

__1.15.Gráfico de Torta para analizar las ventas por ocupación__
Se arrastra al lienzo, el visualizador llamado __pie char__, parametrizandose asi: (clientes[englishoccupation]) y Value=(indicadores[sales])

__1.16.Gráfico de barras para anaizar la tendencia del margen periodicamente__
Se arrastra al lienzo, el visualizador llamado __lined and clustered column chart__, parametrizandose asi: Shared Axis:(ventas(dateorder)), Column Values=(indicadores[sales]) y Line Values=(indicadores[margin])

__1.17.Matriz Navegable para analizar las ventas y su margen desde el pais hasta el articulo vendido__
Se arrastra al lienzo, el visualizador llamado __matrix__, parametrizandose asi: Rows=(paises[salesterritorycountry]), (clientes[name full]) y (productos[englishproductname]); Values=(indicadores[quantity]),(indicadores[sales]),(indicadores[cost]) y (indicadores[margin])
Esta matriz en la parte superior tiene las opciones de navegacion desde el pais, cliente llegando al producto o viceversa

__1.18.Gráfico para analizar el centro y la dispersión de la venta por paises, de acuerdo al numero de hijos de los clientes__
Se arrastra al lienzo, el visualizador llamado __box and whisker__, parametrizandose asi: Axis=(paises[salesterritorycountry]) ; Axis Category I=(clientes[totalchildren]) y Values=(indicadores[ventas]) 


*Nota: Cada visualizador permite configurar sus fuentes, sus formatos y sus colores, en la pestaña de parametrizacion llamada __Formato__*
