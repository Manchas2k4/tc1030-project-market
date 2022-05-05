![Tec de Monterrey](images/logotecmty.png)
# Situación problema: Simulación de un sistema de un sistema de gestión portuaria

## <span style="color: rgb(26, 99, 169);">¿Qué tengo que hacer?</span>
En este repositorio encontrarás una serie de carpetas y archivos que necesitarás para el desarrollo del proyecto.
* *test_cases*: En este directorio encontrarás los archivos de entrada (*input0.txt*, *input1.txt*, *input2.txt*, *input3.txt*, *input4.txt*) que utilizaremos para probar el sistema completo. Adicionalmente están las salida esperadas para cada uno de los archivos de entrada (*output0.txt*, *output1.txt*, *output2.txt*, *output3.txt*, *output4.txt*).
* *unit_test*: En este directorio se encuentran los archivos de pruebas de unidad para cada una de las clases que tienes que desarrollar. Estos archivos de prueba te permiten verificar si tu implementación es correcta.
* *archivos cabecera (o header)*: Archivos en los que se realiza la implementación de cada clase.
* *main.cpp*: Archivo que contiene la función *main*. En este archivo se realiza la lectura/escritura de archivos.

En estos archivos deberás desarrollar la implementación de cada una de las clases que integran la solución del problema presentado en esta actividad. En la parte superior de cada archivo coloca deberás, en comentarios, tus datos. Por ejemplo:
```
// =========================================================
// File: one_header.h
// Author: Edward Elric - A00123456
// Date: 01/01/2021
// Description: This file implements some functions.
// =========================================================
```

## <span style="color: rgb(26, 99, 169);">Introducción</span>
La economía es un hecho indispensable de nuestras vidas. En la vida real, para comprar y vender cosas, usamos algunos activos impresos o virtuales, llamados dinero. Sin embargo, los billetes en tu bolsillo no tiene ninguna diferencia con un pedazo de papel. Obtiene su valor sólo en un mercado.

En este proyecto, implementarás un modelo de mercado básico. Este modelo consta de *comerciantes*, *billeteras*, *transacciones*, *divisas* y un *mercado*. Para simplificar, tenemos dos monedas en el mercado: *dólar* y *PQoin* (Priority Queue Coin). Los comerciantes pueden dar órdenes de compra o venta al mercado si pueden pagarlas.

En nuestro modelo de mercado, hay dos filas ordenadas por prioridad para almacenar pedidos. En una fila de prioridad, los elementos que tienen la prioridad más alta estarán al frente. Las reglas de prioridad se escriben en las siguientes secciones. Con estas reglas, su implementación de mercado debería realizar transacciones si los primeros elementos de estas files de prioridad se superponen.

Ten en cuenta que no hay ninguna interacción con el usuario durante la ejecución. Tu solución tomará la entrada de un archivo de texto, realizará las operaciones e imprimirá la información necesario en un archivo de texto de salida. El nombre de ambos archivos, los tomará como argumento del programa. En otras palabras, **no habrá ninguna entrada dada con el teclado mientras se ejecuta el programa**.

Ten en cuenta que habrá varias clases. Por lo tanto, trabajarás con varios archivos cabecera (o header). Los nombres de las variables de instancia y métodos se proporcionarán en este documento, así como en el encabezado de la clase que se encuentra en cada archivo cabecera. Aunque esto no significa que no puedas agregar métodos o campos adicionales.

### <span style="color: rgb(26, 99, 169);">**Clases**</span>
Existen 6 clases interactuando entre sí en este proyecto:
* `Order`.
* `SellingOrder` (derivado de `Order`)
* `BuyingOrder` (derivado de `Order`)
* `Wallet`
* `Trader`
* `Market`.

Ten en cuenta que será necesario hacer los cálculos necesarios mediante el uso de los métodos correspondiente en las clases `Order` (o derivados), `Wallet`, `Trader` o `Market`, no en el programa principal.

#### <span style="color: rgb(26, 99, 169);">**Order**</span>
La clase `Order` cuenta con las siguientes variables de estado:
* `traderId`: Identificador del comerciante que generó la orden.
* `amount`: Cantidad a comprar.
* `price`: Precio al que se quiere comprar.
* `type`: Tipo de order (venta, compra).

La clase cuenta con los siguientes métodos:
* Constructor con cuatro parámetro (identificador, cantidad, precio, tipo de orden).
* Constructor de copia.
* Métodos de acceso para todas las variables de instancia. (Si consideras necesario agregar métodos de modificación, adelante).
* `double getDollar() const`: El costo, en dólares, de la orden. Se calcula multiplicando el precio por la cantidad a comprar.
* `bool operator==(const Order *right)`: Regresa `true`, si el tipo, identificador, cantidad y precio son los mismos.
* `bool operator==(const Order &right)`: Regresa `true`, si el tipo, identificador, cantidad y precio son los mismos.
* `virtual bool operator<(const Container *right) = 0`: Función abstracta. Se implementará en clases derivadas.
* `virtual bool operator<(const Container &right) = 0`: Función abstracta. Se implementará en clases derivadas.

#### <span style="color: rgb(26, 99, 169);">**SellingOrder**</span>
La clase `SellingOrder`, derivada de `Order`, no tiene ninguna variable de instancia propia. Sin embargo, cuenta con los siguientes métodos:
* Constructor con tres parámetro (identificador, cantidad y precio). Invoca al constructor de la clase superior, indicando el tipo de contenedor correcto.
* Constructor de copia. Invoca al constructor de la clase superior.
* Métodos de acceso para todas las variables de instancia. (Si consideras necesario agregar métodos de modificación, adelante).
* `bool operator<(const Container *right)`: Si el tipo de nuestra orden es diferente a la de `right`, regresa si nuestro tipo es **menor** o no. Si el precio de nuestra orden es diferente al de `right`, regresa si nuestro precio es **menor** o no. Si la cantidad de nuestra orden es diferente a la de `right`, regresa si nuestra cantidad es **mayor** o no. Si no fue ninguno de los casos previos, regres si nuestro identificador es **menor** o no.
* `bool operator<(const Container &right)`: Emplea la misma lógica que el método anterior.

#### <span style="color: rgb(26, 99, 169);">**BuyingOrder**</span>
La clase `BuyingOrder`, derivada de `Order`, no tiene ninguna variable de instancia propia. Sin embargo, cuenta con los siguientes métodos:
* Constructor con tres parámetro (identificador, cantidad y precio). Invoca al constructor de la clase superior, indicando el tipo de contenedor correcto.
* Constructor de copia. Invoca al constructor de la clase superior.
* Métodos de acceso para todas las variables de instancia. (Si consideras necesario agregar métodos de modificación, adelante).
* `bool operator<(const Container *right)`: Si el tipo de nuestra orden es diferente a la de `right`, regresa si nuestro tipo es **menor** o no. Si el precio de nuestra orden es diferente al de `right`, regresa si nuestro precio es **mayor** o no. Si la cantidad de nuestra orden es diferente a la de `right`, regresa si nuestra cantidad es **mayor** o no. Si no fue ninguno de los casos previos, regres si nuestro identificador es **menor** o no.
* `bool operator<(const Container &right)`: Emplea la misma lógica que el método anterior.

#### <span style="color: rgb(26, 99, 169);">**Wallet**</span>
La clase `Wallet` cuenta con las siguientes variables de estado:
* `dollars`: Dólares disponibles.
* `coins`: PQCoins disponibles.
* `blockedDollars`: Dólares bloqueados por transacciones que no se han procesado.
* `blockedCoins`: PQCoins bloqueadas por transacciones que no se han procesado.

La clase cuenta con los siguientes métodos:
* Constructor con dos parámetros (dólares y monedas).
* Constructor de copia.
* Métodos de acceso para todas las variables de instancia. (Si consideras necesario agregar métodos de modificación, adelante).
* `void depositDollars(double amount)`: Si la cantidad recibida es positiva, la agrega a la cantidad de dólares disponibles.
* `void depositCoins(double amount)`: Si la cantidad recibida es positiva, la agrega a la cantidad de PQCoins disponibles.
* `void withdrawDollars(double amount)`: Si la cantidad recibida es positiva, resta esa cantidad de los dólares disponibles.
* `void blockDollars(double amount)`: Si la cantidad recibida es positiva, elimina esa cantidad de los dólares disponibles y la agrega a los bloqueados.
* `void blockCoins(double amount)`: Si la cantidad recibida es positiva, elimina esa cantidad de las PQCoins disponibles y la agrega a las bloqueadas.
* `void returnDollars(double amount)`: Si la cantidad recibida es positiva, elimina esa cantidad de los dólares bloquedos y la agrega a los disponibles.
* `void payFromBlockedDollars(double amount)`: Si la cantidad recibida es positiva, elimina esa cantidad de los dólares bloquedos.
* `void payFromBlockedCoins(double amount)`: Si la cantidad recibida es positiva, elimina esa cantidad de las PQCoins bloquedas.
* `bool checkWithDraw(double amount)`: Si la cantidad recibida es positiva, regresa verdadero si la cantidad es menor a la cantidad de dólares disponibles.
* `bool checkSelling(double amount)`: Si la cantidad recibida es positiva, regresa verdadero si la cantidad es menor a la cantidad de PQCoins disponibles.
* `bool checkBlockedDollars(double amount)`: Si la cantidad recibida es positiva, regresa verdadero si la cantidad es menor a la cantidad de dólares bloqueados.
* `bool checkBlockedCoins(double amount)`: Si la cantidad recibida es positiva, regresa verdadero si la cantidad es menor a la cantidad de PQCoins bloquedas.
* `std::string toString() const`: Regresa un string con el siguiente formato: `<amount1>$ <amount2>PQ`, donde `amount1` es la cantida total de dólares (disponibles y bloquedos) y `amount2` es la cantidad total de PQCoins (disponibles y bloquedas).


#### <span style="color: rgb(26, 99, 169);">**Port**</span>
La clase `Port` cuenta con las siguientes variables de estado:
* `id`: Identificador del puerto.
* `x`, `y`: Posición del puerto en un plano cartesiano.
* `containers`: Lista de los contenedores que están en el puerto.
* `history`: Lista de los barcos que han estado en el puerto.
* `current`: Lista de los barcos que actualmente están en el puerto.

La clase cuenta con los siguientes métodos:
* Constructor con tres parámetros (identificador, posición en `x` y `y` del puerto).
* Constructor de copia.
* Métodos de acceso para todas las variables de instancia. (Si consideras necesario agregar métodos de modificación, adelante).
* `double getDistance(Port *port)`: Regresa la distancia euclidiana entre nuestro puerto y `port`.
* `void incomingShip(SimpleShip *ship)`: Si la nave no se encuentra ya en el puerto, la agrega a la lista de naves que actualmente están en el puerto.
* `void outgoingShip(SimpleShip *ship)`: Sólo se debe ejecutar si la nave se encuentra en el puerto. Remueva la nave de la lista de naves que actualmente están en el puerto y, si la nave no se encuentra en la lista de naves que han estado en el puerto, la agrega.
* `bool contains(Container *container)`: Regresa `true`, si el contenedor se encuentra en el puerto.
* `std::string toString() const`: Regresa un string con el siguiente formato: "Port #id : (x, y)", en seguido la lista de contendores lígeros, pesados, refrigerados y líquidos que hay en el puerto. A continuación, despliega las naves que se encuentra en el puerto (**VER LOS EJEMPLOS DE SALIDA**).

#### <span style="color: rgb(26, 99, 169);">**Ship**</span>
La clase `Ship`, derivada de `SimpleShip`, cuenta con las siguientes variables de estado propias:
* `currentWeight`, `totalWeight` : Peso actual y máximo total de los contenedores que puede llevar la nave.
* `currentNumberOfAllContainers`, `maxNumberOfAllContainers` : cantidad actual y máxima de contenedores que puede llevar la nave.
* `currentNumberOfHeavyContainers`, `maxNumberOfHeavyContainers` : cantidad actual y máxima de contenedores pesados que puede llevar la nave.
* `currentNumberOfRefrigeratedContainers`, `maxNumberOfRefrigeratedContainers` : cantidad actual y máxima de contenedores refrigerados que puede llevar la nave.
* `currentNumberOfLiquidContainers`, `maxNumberOfLiquidContainers` : cantidad actual y máxima de contenedores con líquidos que puede llevar la nave.
* `fuel` : Cantidad actual de combustible.
* `fuelConsumptionPerKM`: Consumo de combustible por kilómetro.
* `currentPort`: Puerto actual en que se encuentra la nave.
* `containers` : Una lista con los contenedores que lleva la nave actualmente.

La clase cuenta con los siguientes métodos:
* Constructor con ocho parámetro (identificador de la nave, puerto actual, peso total que puede llevar, máxima cantidad de contenedores (totales, pesados,refrigrerados y líquidos) que puede llevar la nave y el consumo por kilómetro. Debe invocar al constructor de la clase superior con los parámetros correctos. El resto de las variables de instancia se inicializan a cero.
* Constructor de copia.
* Métodos de acceso para todas las variables de instancia. (Si consideras necesario agregar métodos de modificación, adelante).
* `bool sailTo(Port *port)`: El método calcula combustible que se consumiría por ir de un puerto a otro con base al consumo que genera cada uno de los contenedores que lleva la nave en ese momento, la distancia al puerto destino y el consumo por kilómetro de esta nave. Si la cantidad de combustible es menor al combustible actual, resta la cantidad calculada al combustible actual, elmina la nave del puerto actual, agrega la nave al puerto destino, cambia el puerto actual al puerto destino y regresa `true`para indicar que si se pudo realizar el viaje.
* `void reFuel(double amount)`: Siempre la cantidad sea positiva, la aumenta al combustible actual.
* `bool load(Container *container)`: Este método deberá revisar varias condiciones. La primera, si el puerto actual no tiene el contenedor o si la cantidad actual de contenedores es mayor o igual a la cantidad máxima de contenedores o si el peso actual m+as el peso del contenedor excede el peso total que puede llevar la nave, no es posible cargar ese contenedor. A continuación, deberá verificar, de acuerdo al tipo de contenedor, que no se exceda de la cantidad máxima permitida de contenedores de un tipo determinado. En cualquier caso anterior, deberá regresar `false`. Si se puede hacer la carga, deberá remover el contenedor del puerto actual, agregar a la lista de contenedor, incrementar el número de contenedores que lleva la nave tanto en lo general, como en lo que respecta a un tipo determinado, regresando `true`para indicar que se realizó la carga del contenedor.
* `bool contains(Container *container)`: Indica si el contenedor se encuentra dentro de la lista de contenedores.
* `bool remove(Container *container)`: Remueve un contenedor determinado de la lista de contenedores.
* `bool unLoad(Container *container)`: Este método, primero, deberá revisar si lleva el contenedor indicado. Si es así, deberá remove el contenedor de la lista de contenedores agregarlo al puerto actual, reducir el número de contenedores que lleva la nave tanto en lo general, como en lo que respecta a un tipo determinado, regresando `true`para indicar que se realizó la descarga del contenedor. Si no, regresa `false`.
* `std::string toString() const`: Regresa un string con el siguiente formato: "Ship #id : fuel", en seguido "\n\t\tLight Containers: " y la lista de contenedores ligeros, a continuación "\n\t\tHeavy Containers: " y la lista de contenedores pesados; y así para el resto de los contenedores refigerados y líquidos (**VER LOS EJEMPLOS DE SALIDA**).

#### <span style="color: rgb(26, 99, 169);">**main.cpp**</span>
En el archivo *main.cpp* se realizarán las operaciones generales de entrada y salida. Leerás de un archivo de entrada las operaciones sobre la simulación, las deberás realizar e imprimirás los resultados en el archivo de salida.

Las operaciones se detallan más adelante. El nombre de los archivos de entrada y salida se darán como argumentos del programa a través de la línea de comandos. Si el archivo de entrada no existe, el programa termina.

Deberás manejar tres vectores, uno para apuntadores a objetos `Container`, otro para apuntadores de objetos `Port` y otro para apuntadores a objetos `Ship`. **Adicionalmente, deberás considerar variables que indiquen la cantidad de contenedores, puertos y naves creadas, ya el valor de estas variables se utilizarán como id de los objetos creados. Por lo mismo, deben ser inicializas a 0.**

#### <span style="color: rgb(26, 99, 169);">**Entrada**</span>
Vas a leer el archivo de entrada elemento por elemento.

La primera línea tiene cuatro números enteros, `C`, `S`, `P` y `N`. El número `C` represnta el número de contenedores que estarán en la simulación. El segundo número, `S`, indica el número de naves en la simulación. El tercer número, `P`, indica el número de puertos en la simulación. Y, por último, `N`, representa el número de eventos a simular.

Las siguientes línea `N` serán algunas de las siguientes operaciones:
1. Creando un contenedor.
2. Creando una nave.
3. Creando un puerto.
4. Cargar un contenedor a una nave.
5. Descargar un contenedor de una nave.
6. Un nave viaja del puerto actual a otro.
7. Una nave carga combustible.

##### <span style="color: rgb(26, 99, 169);">**1. Creando un contenedor**</span>
Esta línea contiene un 1, seguido id del puerto en el que está el contenedor, el peso y tipo de contenedor.
```
1 <idPort> <weight> <type>
```
Los tipos válidos son `B`, `R` y `L`. `R` indica que es un contenedor refrigerado, mientras que `L` indica que es un contenedor líquido. Caso espacial es `B`, el tipo de contenedor que se creará dependerá del peso del contenedor. Si es peso es menor o igual a 3000, se crea un contenedor ligero; si es mayo, se crea un contenedor pesado. Toma en cuenta que el identificador del contenedor será el orden de creación. Por ejemplo, el primer contenedor creado debe tener Id 0 y debe colocarse en la posición 0 del vector.

##### <span style="color: rgb(26, 99, 169);">**2. Creando una nave**</span>
Esta línea contiene un 2, seguido del identificador del puerto en que se encuentra la nave, el peso total que puede llevar la nave, en número máximo de contenedores, de contenedores pesados, refrigerados y líquidos que la nave puede llevar, así como el consumo de combustible por kilómetro.
```
2 <idPort> <totalWeight> <maxNumberOfAllContainers> <maxNumberOfHeavyContainers> <maxNumberOfRefrigeratedContainers> <maxNumberOfLiquidContainers> <fuelConsumptionPerKM>
```
Toma en cuenta que el identificador de la nave será el orden de creación. Por ejemplo, la primera nave creada debe tener Id 0 y debe colocarse en la posición 0 del vector.

##### <span style="color: rgb(26, 99, 169);">**3. Creando un puerto**</span>
Esta línea contiene un 3, seguido de la posición `x` y `y` del puerto.

```
3 <x> <y>
```
Toma en cuenta que el identificador de la nave será el orden de creación. Por ejemplo, la primera nave creada debe tener Id 0 y debe colocarse en la posición 0 del vector.

##### <span style="color: rgb(26, 99, 169);">**4. Cargar un contenedor a una nave**</span>
Esta línea contiene un 4, seguido del id de la nave y el id del contenedor.

```
4 <idShip> <idContainer>
```

##### <span style="color: rgb(26, 99, 169);">**5. Descargar un contenedor de una nave**</span>
Esta línea contiene un 5, seguido del id de la nave y el id del contenedor.

```
5 <idShip> <idContainer>
```

##### <span style="color: rgb(26, 99, 169);">**6. Un nave viaja del puerto actual a otro**</span>
Esta línea contiene un 6, seguido del id de la nave y el id del puerto.

```
6 <idShip> <idPort>
```

##### <span style="color: rgb(26, 99, 169);">**7. Una nave carga combustible**</span>
Esta línea contiene un 7, seguido del id de la nave y la cantidad de combustible.

```
7 <idShip> <amount>
```

#### <span style="color: rgb(26, 99, 169);">**Salida**</span>
Debes calcular lo siguiente e imprimirlo en el archivo de salida.

Debés imprimir la información relacionada con cada puerto (contenedores y barcos).

Por último, deberás eliminar todos los apuntadores que existan y cerrar los archivos de entrada y salida.
