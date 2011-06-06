# Tema 2

## Telefonía celular

Celdas hexagonales

En el centro de cada celda hay una antena (torre
con antena y edificio con el equipo de radio).

Dimensiones de la
celda: 100 m^2^ - 30/40 km^2^ 

La torre se sitúa en el centro
geométrico (donde está la estación base) 

Las celdas se agrupan en
siete grupos, donde cada uno maneja un conjunto de frecuencias
diferente. Es decir, cada grupo de siete celdas tiene una
configuración idéntica, donde cada celda tiene una configuración
diferente, de manera que no se hagan interferencias entre una celda
y otra contigua. 

Cuando los altavoces de un aparato hacen un ruido
por la cercanía de un terminal móvil, se debe a que éste está
cambiando de celda.

Cuando los terminales móviles se desplazan entre celdas, se cede el
control de la comunicación entre las estaciones base vecinas.

Un proveedor (PSC) utiliza 832 radiofrecuencias. 

Cada teléfono
tiene 2 fecuencias. Hay 395 canales de voz. 395 \* 2 = 790
frecuencias. 

Las 42 frecuencias restantes se usan para funciones de
control. Cada celda utiliza 1/7 de los canales, dando lugar a una
capacidad de 56 canales por celda, luego 56 usuarios por celda.

Agrupamiento de celdas en clusters de 7 celdas para no repetir
frecuencias en celdas vecinas.

## Telefonía celular analógica

Comenzó en los años 1980 mediante sistemas AMPS advanced mobile
phone systems. En Europa dio lugar al TACS (Total? Access Control
Communication System). Es la llamada 1G, que sólo permite envío de
voz. Los canales se multiplexaban por división de frecuencias FDM,
30KHz.

## Telefonía celular digital

1990 GSM (Global System Mobile) $\rightarrow$ 2G Permitía voz y datos, por
tanto surgieron los SMS.

2.5G $\rightarrow$ GPRS (General Packet Radio System) voz y datos con accesso
inalámbrico a internet.

3G $\rightarrow$ UMTS (Universal Mobile Telecommunications System).

GSM: 2 bandas de frecuencia de 25MHz Cada banda se divide en 125
canales (FDM) y cada canal tiene un ancho de banda de 200kHz.
Realmente se utilizan 124, el primero está reservado.

En cada canal de 200kHz se modula una única señal portadora.
270.833 Kbps (GMSK $\rightarrow$ Gaussina Minimum Shift keying)

Cada canal se divide en slots o ranuras

La secuencia de bits transmite una secuencia a ráfagas, se divide
por TDM en 8 ranuras o slots. Cada ranura transporta 22.8 Kbps (se
puede enviar tanto voz como datos)

Codificación mediante un código de voz predictivo (RPE/PLC):
muestrea generando muestras de 260 bits cada 20 mseg. Tenemos
124\*8 = 992 canales teóricos, donde muchos no se pueden usar por
solapamiento de frecuencias.

# Tema 3: Capa de enlace de datos

La capa de enlace se encarga de hacer fiable la comunicación física
a través de los medios de transmisión entre 2 máquinas adyacentes.

**Hacer fiable una comunicación:** Los bits se entregan en la capa de
enlace del receptor en el mismo orden en que se transmitieron y sin
errores.

El diseño de protocolos es diferente según trabajemos con redes LAN
o WAN

Necesario esta capa por las limitaciones en las características de
los medios de transmisión (errores vel. de transferencia finita,
retardo de propagación, etc)

Funciones de la capa de enlace:

1. Suministrar servicios a la capa de red. A través de una interfaz bien
definida. Su principal servicio es transmitir información entre las máquinas
origen y destino. La comunicación con la capa de red: solicitud, respuesta,
indicación y confirmación. Tres tipos de servicios:

    a) Servicio sin conexión y sin confirmación.

        * No se establece (ni libera) una conexión.
        * Si una trama se pierde, no se realiza ningún intento de recuperación.
        * Se usan en redes con baja tasa de error, con datos en tiempo real. P.e
          voz digitalizada en trama relay y atm.

    b) Servicios sin conexión y con confirmación:

        * Las tramas son confirmadas de forma individual
        * Se usan temporizadores para el reenvío de tramas.
        * Las tramas que llegan dañadas se envían bajo petición del receptor.
        * Se utiliza en canales que no son fiables, por ejemplo sistemas
          inalámbricos.

    c) Servicios con conexión:

        * Se realiza una conexión al principio de la transmisión y se libera al
          final.
        * las tramas se enumeran y deben entregarse todas y sin duplicados y en
          el mismo orden que se han generado en el emisor.

2. Entramado (y desentramado) de la información que llega de la capa de red.

     * Se divide la información en paquetes más pequeños (tramas) para hacer
       mejor uso del ancho de banda (más eficiencia).
     * Se debe buscar un compromiso entre el tamaño de la trama y la frecuencia
       de reenvíos en función de la tasa de errores media.
     * Las tramas se delimitan marcando el inicio y el final.

        a) Inclusión de intervalos de tiempo entre tramas (no es adecuada, el
           comportamiento de la red es impredecible)
        b) Poniendo en la cabecera el número de caracteres que mide la trama. El
           problema es si se corrompe la trama y se pierde un carácter, y se 
           estropea todo.
        c) Caracteres de inicio y fin de trama. En ascii son DLE STX  y DLE ETX.
           Sólo funciona con códigos que permiten caracteres de control. El 
           problema es si en la información tenemos esta misma secuencia, por 
           ejemplo, que se soluciona con técnicas de inserción de caracteres de
           control.
        d) Banderas de inicio y fin: Consiste en el uso de secuencias especiales
           para delimitar tramas (flags) 01111110 Tenemos aún el problema de si 
           la secuencia existe dentro de los datos. Para evitar que la bandera se
           confunda con alguna secuencia de datos, se utilizan técnicas de 
           inserción de bits. Se utiliza en el protocolo HDLC.
        e) Mediante violaciones de código en la capa física. Es decir, introducir
           códigos no válidos para el tipo de codificación que estamos utilizando. 
           Se usa en aquellas redes en la que exise algún tipo de codificación 
           en la capa física (Manchester). No se requieren técnicas de inserción
           de bits
        f) Combinación de algunas técnicas anteriores.

3. Control de errores

   Implica 2 actividades: detección y corrección de errores.

   Detección de errores:

   i. Control de paridad

     * Vertical: Par o impar
     * Horizontal
  ii. CRC: Códigos de redundancia cíclica.

   Tanto Control de paridad horizontal como CRC se hacen a nivel de Mensaje,
   mientras que Control de paridad vertical se hace a nivel de carácter.

Correción de errores:

1. Códigos autocorrectores (Hamming): Utiliza información redundante, luego
   tiene overhead.
2. Utilización de petición automática de retransmisión (ARQ)

    * ARQs simples (parada y espera)
    * ARQs continuos

       - Selectivo
       - No selectivo (Retroceso-N)

Protocolos a diseñar en la capa de enlace deben corregir las siguientes
situaciones:

a) Errores en el contenido de la información $\rightarrow$ CRC
b) Pérdida de tramas $\rightarrow$ se utiliza temporizadores y retransmisión o reenvío.
c) Pérdida de confirmaciones que conlleva presencia de I-tramas duplicadas $\rightarrow$
se soluciona usando nºs de secuencia a las tramas.


CRC (SVT secuencia de verificacion de trama o FCS frame checking sequence)

- Se utiliza para detectar errores en la transmisión de mensajes
- CRC lo calcula el emisor y lo añade a la cola del mensaje transmitido. En
  recepción se calcula el CRC del mensaje recibido y se compara.


Calcular el CRC de la secuencia 1101011011 con un polinimio generador G(x) =
X^4^+x+1

1. M(x) = X^9^+X^8^+X^6^+X^4^+X^3^+X+1
2. M(X) * X^4^ = X^13^+X^12^+X^10^+X^8^+X^7^+X^5^+X^4^ = 11010110110000 (hace hueco
para el CRC)
3. Divide X^4^ * M(X) / G(X)

   10011 | 11010110110000 se va haciendo XOR y bajando uno a uno todos los dígitos
   el resto da 1110.

4. La trama a transmitir es 11010110111110


## ARQ

Una trama llega mal, el receptor lo detecta y pide la retransmisión
de esa trama.

Existe el RQ simple que no es muy eficiente, y el RQ continuo, que
a su vez se categoriza entre selectivas y no selectivas (o
retroceso-N).

### RQ Simple

Trabaja en modo semiduplex. Cuando un emisor envía una trama, se
espera a recibir del receptor el ACK.

En la figura 1.23 del libro (página 53) vemos que el Primario
(emisor) tiene un temporizador, dentro del tiempo en que recibe el
ACK de la trama. 

Las tramas van numeradas, y el emisor no envía la
trama N+1 hasta que no recibe el ACK de la trama N.

En el apartado
b) vemos qué sucede cuando la trama llega errónea (NAK). 

Entonces
el emisor envía de nuevo esa trama, y así hasta recibir el ACK de
la trama. 

En el apartado c) se pierde el ACK, y para ello nos sirve
el temporizador, que al finalizar el tiempo de espera, el emisor
detecta que la trama no ha llegado y lo que hace es retransmitir de
nuevo la trama. 

En ese caso, el receptor obtiene un duplicado de la
trama, y se da cuenta de ello por el nº de secuencia; al recibirla
envía de nuevo el ACK.

La eficiencia es el tiempo de retransmisión de una trama dividido
entre el tiempo total (desde que se activa hasta que finaliza el
temporizador).

En la figura 1.24 del libro (página 55) se pueden observar los
tiempos de retransmisión y retardos en este protocolo.

La eficiencia se mide como $$ U = \frac{T_{ix}}{T_t}$$

en este caso: $$ U = \frac{T_{ix}}{T_{ix}}+2T_p$$

Caso:

Un canal T1 = 1.544 Mbps

A — 3000 km — B

Tramas de 64 octetos = 64 \* 8 = 512 bits

V~p~ = 6 $\mu$s / km = $\frac{10^6}{6}$ km/seg

$T_{ix}$ = $\frac{\text{longitud trama}}{V_t}$ = $\frac{512}{1.544 \times 10^6}$= 0.33
mseg

$T_p$ = $\frac{\text{distancia entre A y B}}{V_p}$ =
$\frac{310^3}{\frac{10^6}{6}}$ = 18
mseg

U = $\frac{0.33}{0.33 + (2 \times 18)}$= $\frac{0.33}{36.33}$ = 0.00908 < 1\%

nº mensajes = $\frac{36.33}{0.33}$ = 110 mensajes

### ARQ Continuo

Necesita bufferes (listas FIFO)

A medida que van llegando las confirmaciones, va quitando los
paquetes de la lista y pasandolo a la capa superior.

Requiere Full-Duplex

En la página 59, fig. 1.26 vemos el esquema de cómo funciona.


## Control de flujo

Permite controlar la tasa de transmisión de tramas a través de un
enlace. Es decir, cuando los bufferes están llenos, pide que se
deje de transmitir, etc. El receptor debe tener siempre recursos
suficientes en su buffer para aceptar tramas. Para controlar ésto
se utiliza la ventana deslizante. Esta ventana deslizante lo que
hace es establecer un límite al numeros de i-tramas que puede
enviar el emisor (p) ((p de primario)) antes de recibir una
confirmación.

Cuando el receptor no puede asumir más tramas deja de enviar ACKs
al emisor.

En RQ simple la ventana deslizante es 1. Enviamos una trama,
esperamos un ACK.

El límite de tramas a enviar se denomina ventana de transmisión K.

Entre las tramas confirmadas y las tramas por transmitir, tenemos
como máximo K tramas que esperan confirmación, si se llega al
límite tenemos que parar (se bloquea el emisor). La recepción de un
ACK hace que el límite inferior incremente en uno.

Por último, el nº máx. de bufferes de tramas requeridos en
S(receptor) se conoce como ventana de recepción.

## Números de secuencia

Nº de secuencia que P inserta en la trama $\rightarrow$ N + 1

Definir un límite máximo para el nº de i-tramas.

- Permite limitar el tamaño de las listas de transmisión y
  recepción.
 
- Permite limitar el rango de nºs requerido para poder identificar
  cada trama de forma única.

RQ Simple

-   Siempre hay como máximo una i-trama pendiente de confirmación.

-   Podemos limitar el nº a 0 ó 1.


Con retroceso-N, y una ventana K

-   el nº de identificadores debe ser al menos k+1


Con repetición selectiva y una ventana igual que k, necesitamos que
el número de identificadores sea al menos 2k.

Resumiendo:

-   RQ simple $\rightarrow$ 2

-   RQ retroceso N $\rightarrow$ K+1

-   RQ repetición selectiva $\rightarrow$ 2K


## HDLC

Protocolo más importante dentro de la capa de enlace.

Control de enlace de datos a alto nivel.

Estación primaria: Manda i-tramas. Controla el almacenamiento del
enlace. Tramas = Ordenes. Inicializa la comunicación, establece
parámetros de transmisión, etc. Estación secundaria: Manda
contestación a las tramas. Tramas = Respuestas (a la estación
primaria) Estación combinada: Mezcla de primaria y secundaria.

Tipos de configuraciones (de una conexión):

-   Configuración no balanceada: Primaria + Secundaria

-   Configuración balanceada: Dos estaciones combinadas.


Ambas son full-duplex o semiduplex.

Tenemos tres formas de realizar una transferencia:

1.  Modo repuesta normal: Estación primaria inicia la transmisión
    de datos a la secundaria. La sec. solo puede enviar respuestas.

2.  Modo balanceado asíncrono: Cualquier estación puede iniciar la
    transmisión.

3.  Modo de respuesta asíncrono: La estación secundaria sí que
    puede iniciar la transmisión.


Trama HDLC: [Delimitador | Dirección | Control | Información | FCS
| Delimitador]

Los tres primeros campos se denominan cabecera, y los dos últimos
cola.

Delimitador: 8 bits: 01111110 // Puede usarse también para marcar a
la vez fin e inicio de la siguiente trama. Si tenemos esta cadena
en el campo información, puede darse una desincronización. Esto se
soluciona con la técnica de inserción de bits, si se tiene una
secuencia: "011111" se inserta un 0 extra antes del 10.

El algoritmo para identificar el delimitador de inicio es:

Si aparece una combinación de 5 unos:

-   El sexto bit = 0 se elimina

-   El sexto bit = 1 y septimo = 0 delimitador fin

-   El sexto bit = 1 y septimo = 1 indicación de cierre generada
    por el emisor.


El problema de esta técnica es que algún bit se flipe en la
transmisión.

Dirección: 8 bits // también pueden ser 16

Se utiliza para identificar al receptor Se puede utilizar un
formato extendido. En este caso el bit menos significativo: - 1 es
el último octeto - 0 no es el último octeto 11111111 Es el
broadcast

Control: 8 ó 16 bits

I-tramas:
  ~ Transportan datos del usuario, también pueden llevar
    información del ARQ utilizado y de flujo. 

S-tramas: 
  ~ Tramas de
    supervisión: Transportan la información de ARQ cuando no se puede
    incluir en las I-tramas. 

N-tramas (no numeradas): 
  ~ Envía información
    complementaria de control de enlace.

El campo de control incluye un bit (P/F "poll/final") tramas de
órdenes P=1 solicitud de respuesta. tramas de respuesta F=1
identifica a la trama de tipo respuesta.

Información: Variable

Sólo en I-tramas y N-tramas.

La restricción es que el nº de bits tiene que ser un múltiplo
entero de 8.

FCS: 16 ó 32 bits

Campo de comprobación de trama, que lleva un CRC. Incluye un código
de detección de errores, elaborado teniendo en cuenta la trama sin
los delimitadores.

El estándar más típico que se utiliza es el CRC-CCITT de 16 bits.

HDLC, usa una transmisión síncrona. Su funcionamiento es un
intercambio de tramas I, S y N. Su funcionamiento se realiza en
tres pasos:

1.  Inicialización de la comunicación. La puede solicitar
    cualquiera de los dos extremos. Se negocia el modo de transmisión
    que se va a utilizar:

    -   Se avisa al otro extremo.

    -   Se especifica uno de los modos.

    -   Se especifica si se utilizan 3 ó 7 bits para los nºs de
        secuencia.


    El otro extremo envía:

    -   UA confirmación no numerada

    -   DM modo desconectado


2.  Transferencia de información:

    -   Envio de datos mediante I-tramas

    -   N(S) y N(R)

    -   Las tramas de supervisión también hacen control de flujo de la
        información y control de errores.

    -   RR: Receptor ready: Implica que el receptor envía tramas de
        este estilo cuando no le lleguen tramas de información, avisando
        que no se ha caído.

    -   RNR: Receptor not ready: El receptor no está preparado y sirven
        para confirmar las I-tramas. Pide que no se retransmite hasta que
        no llegue una trama RR.


3.  Desconexión:

    -   Cualquiera de los dos extremos

    -   Por iniciativa propia o solicitada por capas superiores

    -   Trama DISC (disconnect)

    -   El otro extremo puede aceptar la desconexión UA



El formato de trama es único.

Como subconjunto del HDLC tenemos los protocolos: LAP, LAPB, LAPD,
LLC, LAPX

## LAPB

- ABM
- Desarrollado por la UIT-T como una parte del X25
- Interfaz
  a redes de conmutación de paquetes. 
- Subconjunto de HDLC 
- Diseñado como interfaz para enlaces punto a punto. 
- Formato de las
  tramas = HDLC

## LAPD

- Procedimiento de acceso al enlace sobre el canal D 
- Desarrollado
  por la UIT-T como parte de la recomendación para la RDSI 
- Igual
  que HDLC el acceso es mediante ABM 
- Sin embargo el nº de bits para
  formar los nºs de secuencia (que en HDLC eran 3 o 7 bits) son
  siempre 7 bits. 
- El campo FCS donde está incluido el CRC es
  siempre de 16 bits.

## LLC

- Control de Enlace Lógico. 
- Pertenece a la familia IEEE802.2 para
  controlar el funcionamiento de las LAN (redes de área local). 
- En
  este caso ni el LLC tiene todas las características del LLC, sino
  que además tiene algunas características diferentes. 
- Principalmente las diferencias están en el formato de las tramas. 
- De hecho en este caso, las funciones de control de la capa de
  enlace está dividida en LLC y capa MAC, luego cada subcapa añade
  sus cabeceras a la trama.


        Trama LLC
        ——————————————--------------
        [DSAP(*1)|SSAP(*2)|control LLC|Informacion]
        ——————-------------- ^ 
        Puntos de acceso misma que 
        al servicio         HDLC

        *1) Destino
        *2) Source

La capa MAC añade una cabecera y una cola:

       [Control MAC | Direccion destino MAC | Dir. Origen MAC | Trama LLC | FCS]
        ^            ———————————— 
        Funciones    Todas las maquinas comparten
el medio CRC \* de control no hay primario/secundario

\*) Errata en los apuntes: En la trama MAC/LLC pone que el código
es de 16 bits pero en la literatura pone que es de 32 bits, en el
examen no lo preguntará.


     [Control MAC | Direccion destino MAC | Dir. Origen MAC | Trama LLC | FCS]
      ^             ----------------------------------------              ^
     Funciones      Todas las maquinas comparten el medio                 CRC *
     de control     no hay primario/secundario
     
     *) Errata en los apuntes: En la trama MAC/LLC pone que el código es de 16 bits
       pero en la literatura pone que es de 32 bits, en el examen no lo preguntará.

## Protocolo PPP (point to point)

- Las comunicaciones pp se establecen:

1.  Cuando interconectamos LANs a través de routers

2.  Cuando hacemos conexiones usuario-proveedor


- Cuando nacieron estas redes punto a punto, dicho protocolo no
  existía, lo que existía era el SLIP (Serial Line Internet Protocol)
  RFC 1055.

  Tenía muchos problemas, entre otros:

1.  No hace detección ni corrección de errores. Las capas
    superiores debían hacer la detección y corrección de errores

2.  Sólo soporta el protocolo IP en la capa de red.

3.  Las direcciones IP debían ser asignadas de antemano.

4.  No proporciona ningún mecanismo para hacer autenticación

5.  No es un estándar.


Como tenía tantos problemas definieron el PPP (RFCs 1661, 1662 y
1663).

-   En este protocolo sí que las tramas tienen delimitadores de
    inicio y fin

-   Detección de errores en cada trama

-   LCP (P. control de enlace), negocia los parámetros del
    establecimiento de la conexión, mantenimiento y posterior
    liberación.

-   NCP (P. control de red), negocia las opciones de la capa de
    red. Independencia del protocolo de red usado.

-   PPP es un protocolo orientado a carácter, frente al HDLC, que
    es orientado a bit.


### Trama

      [Delimitador Inicio | Address | Control | Protocolo | Datos | CRC | Delimitador Fin] 
       01111110             11111111                                      01111110 
                            (Broadcast)


**Control**: Puede ser

-   No fiable(por defecto): 00000011 (no usa nºs de secuencia, y no
    espera ACKs)

-   Fiable: Sí se usan los nºs de secuencia (RFC 1663)


**Protocolo**: indica el tipo de protocolo de capa de red que lleva
esta trama. Puede ser 1 o 2 bytes. Puede ser protocolo IP, NCP,
IPX...

**Datos**, o carga, de longitud variable, aunque por defecto son 1500
caracteres

**CRC**: Normalmente 2 bytes, pero se pueden negociar 4 bytes.

Más o menos su funcionamiento es:

Estado de reposo (dead) y cuando se detecta una portadora,
intentamos una conexión, si dicha conexión falla, volvemos al
estado de reposo. si no falla, pasamos a un estado de
autenticación. En éste es donde se negocian parámetros entre origen
y destino. Si la autenticación falla, termina la conexión. y del
estado termnate, volvemos al estado inicial (dead). Si la
autenticación tiene éxito, se negocian los parámetros de red, en el
protocolo siguiente que es el NCP. Una vez establecidos los
parámetros de red, comienza la comunicación (open). Cuando la
comunicación termina pasamos al estado terminate.

## Congestión

El caudal depende del tipo de red y tiene un valor máximo que no
podemos superar.

La red no ofrece el mismo caudal real si se le ofrece poco tráfico
o mucho.

La congestión se produce cuando la carga del tráfico del canal, es
mayor que los recursos disponibles.

Tenemos dos opciones:

1.  Disminuir la carga

    -   Denegando espacio a algunos usuarios.

    -   Degradar espacio a todos.

    -   Planificar las demandas de los usuarios en función de la
        carga.


2.  Aumentar los recursos


### Por qué se produce la congestión

1.  Capacidad de las líneas de salida está desbordada. Es decir,
    cuando los búferes están llenos. Formación de colas en los
    routers:

    -   Las líneas de salida tienen (menor?)\*\*\*\* capacidad que las
        de entrada.

    -   Muchos paquetes por la misma línea de salida


2.  Procesadores lentos en los routers / líneas de comunicación
    lentas. En este caso se producen colas a pesar de que la línea de
    salida tiene suficiente capacidad. En el segundo caso, hay que
    esperar a que la línea esté libre.


Tenemos que distinguir entre:

-   Control de flujo. Técnica que permite sincronizar el envío de
    inf. entre 2 entidades que producen/procesan información a
    distintas velocidades. Se refiere al traico en una conexión punto a
    punto entre emisor y receptor. Por ejemplo una conexión entre un
    servidor con una capacidad de procesamiento muy grande conectado
    punto a punto con un sobremesa de menor capacidad. Si estos
    dispositivos se comunican a distintas velocidades, hay un problema.
    En este caso, el sobremesa tiene que indicar al servidor la
    velocidad que puede aceptar.

-   Control de congestión. Es un concepto más global, se refiere a
    toda la red. Es un conjunto de técnicas para detectar y corregir
    problemas cuando no todo el tráfico ofrecido puede ser cursado.


En una situación ideal, los paquetes entregados o cursados y los
paquetes enviados u ofrecidos son los mismos, es decir, siguen una
progresión lineal, hasta llegar al punto de saturaciín de la red
(capacidad máx. real) donde los paquetes enviados crecen, pero los
entregados se mantienen.

El comportamiento típico es que al llegar a la zona de saturación,
cuanto más tráfico se ofrece, menos se cursa, luego es una curva
que crece linealmente y luego se curva y baja.

Por último, la situación deseable es que se introduce algún
algoritmo de control de congestión para aproximar el comportamiento
de la red a la situación ideal.

## Principios generales del control de congestión

Aplicar la teoría de control para sistemas complejos (red de
comunicaciones)

Varias soluciones agrupadas en:

1.  Bucle abierto (solución pasiva) intenta resolver el problema
    hacieno un buen diseño inicial de los sistemas. En cualquier
    momento tenemos conocimiento sobre el estado de la red, nos
    permite:

    -   decidir cuando se acepta nuevo tráfico.

    -   decidir cuando descartar tráfico y cual.¿?

    -   planificar decisiones en distintos puntos de la red


2.  Bucle cerrado (solución activa): actúa sólo cuando se detectan
    problemas. Basadas en el concepto de retroalimentación.

    1.  Monitorizar el sistema para detectar dónde y cuando ocurre la
        congestión. Medir el % de paquetes descartados por falta de memoria
        en los nodos. Longitud media de las colas. El nº de paquetes
        retransmitidos por timeout y el retardo medio de paquetes.

    2.  Pasar esta información a los puntos donde se toman decisiones,
        mediante paquetes especiales, que no están sometidos al control de
        gestión, se saltan todas las colas, no esperan porque tienen que
        tener prioridad para avisar de la congestión. Los envía el nodo que
        detecta la congestión. Se indica que es especial modificando bits
        en la cabecera del paquete, que llevan información acerca de la
        existencia de congestión.

        -   Informan a las fuente del estado del tráfico.

        -   Aumentan el tráfico en el moemnto por tanto aumenta la carga.


    3.  Ajustar la forma en la que está operando el sistema para
        corregir el problema.

        -   Reduciendo la velocidad de envío a la red.

        -   Controlando el acceso al sistema, en este caso la red,
            prohibiendo más conexiones.

        -   Descartando paquetes.




## tipos de algoritmos

- Bucles abiertos

    a) Actúan en la fuente 
    b) Actúan en el destino

- Bucles cerrados 
  
    a) Retroalimentación explícita, envío de paquetes
       desde el punto de congestión para prevenir a la fuente.
    b) Retroalimentación implícita, la fuente reduce la existencia de
       congestión haciendo observaciones locales.
  
        - Ausencia de ACK.
        - Controlar el tiempo que tarda en llegar ACK.

Políticas que afectan a la congestión:

- Enlace

  - Política de retransmisiones:

    - Timeout pequeño más retransmisiones más tráfico mayor
      probabilidad de congestión.
    - Timeout grande mayor retardo

  - Política de caching fuera de orden (almacenamiento de
    paquetes):

    - Política simple: Descartar desordenados. El emisor tiene que
      reenviar todos los paquetes que el receptor está descartando, luego
      al final genera más tráfico. 
    - Política compleja: Disminuyen las
      retransmisiones a costa de tener un número de secuencia y memoria
      en los bufferes para almacenar todos los paquetes que llegan
      desordenados entregándolos ordenados.

  - Política de confirmaciones:

    - Confirmación para cada una de las tramas más tráfico. 
    - Confirmación sólo para algunas de las tramas o incluso sólo de la
      última. Esto disminuye el tráfico pero es viable sólo en redes que
      son seguras.

- Políticas de control de flujo, ventanas de retransmisión.
  Cuanto más pequeña la ventana mejor funcionamiento desde el punto
  de vista de la congestión.


Red

-   Corcuitos virtuales versus datagramas en la subred, en los
    datagramas es más difícil controlar la congestión.

-   Política de servicio y "encolamiento" de paquetes, cómo
    organizar las colas de entrada/salida en los nodos.

-   Política de descarte de paquetes, cuando un paquete llega a un
    nodo y no lo puede procesar, el nodo decide cuál descartar, de
    manera que disminuya la congestión.

-   Algoritmos de encaminamiento, una buena práctica es elaborar
    algoritmos que saquen tráfico por todas las líneas de salida,
    balancear la carga detectando y evitando la congestión en una de
    las líneas de salida.

-   Gestión del tiempo de vida de los paquetes. En los paquetes hay
    un campo edad, donde modificándolo podemos disminuir la congestión,
    o al menos que no influya negativamente. Si el campo edad es muy
    grande, más tiempo está el paquete dando vueltas por la red,
    entonces aunque llegue a destino, ese paquete sigue pululando por
    la red hasta que su edad llegue a 0. Si la edad es muy grande, nos
    aseguramos que llegue a destino con más probabilidad, pero también
    más probabilidad de congestión. Si el campo edad es muy pequeño
    corremos el riesgo de que el paquete se caduque antes de llegar al
    destino.


Transporte

-   Politica de retransmisiones

-   politica de caching fuera de orden

-   politica de confirmaciones

-   politica de control de flujo

-   determinación del timeout, en el nivel de enlace el tiempo de
    transmisión es como siempre el mismo. En el nivel de transporte
    depende de lo que ocurra en la red.


Tecnologías de la capa de red

Redes X25

Interfaz entre la estación y red de comunicaciones, conmutación de
paquetes, funciona mediante circuitos virtuales.

La mayoría a 64 kbps.

Capas:

-   Física $\rightarrow$ X21

-   LAPB subproductos del HDLC

-   Paquete $\Rightarrow$ cabecera de control sobre los datos de usuario
    $\rightarrow$ paquete X25


Formato del paquete X.25: cabecera | inf (128)

cabecera = c.v . mediante un numero | nº seciencia para control de
flujo y control de errores. Diferentes formatos de paquete x25.

Retransmisión de tramas en Frame relay

-   servicio anterior a ATM

-   Pretende una comunicación entre dos hosts de forma sencilla

-   orientado a conexión, lo que le facilita no tener que hacer
    demasiada gestión (hay cierta garantía de entrega)

-   confía en las altas capacidades de los dos hosts que se están
    comunicando, pasa las labores de control a los dos hosts.

-   viable en redes de alta fiabilidad.

-   lineas virtuales alquiladas. Tiene que competir con líneas
    alquiladas fijas, por ejemplo las líneas telefónicas, y además
    compite con X25, pero a pesar de eso consigue velocidades de entre
    1.5 y 2 Mbps.

-   Los servicios de frame relay son básicamente detectar inicio y
    fin de trama y detección de errores trama con error descartarla


Diferencias entre FR y X25:

1.  FR, señalización por un canal lógico distinto al de datos

2.  La multiplexación y la conmutación de conexiones lógicas se
    hace en la capa 2 en FR y en X.25 en la capa 3.

3.  En FR no hay intercambio de información entre nodos (routers
    por los que circule la información), solo extremo a extremo,
    mientras que en X25 cada router establece comunicación con el
    siguiente. Por lo tanto el control de flujo, congestión y errores
    en FR se realiza extremo a extremo, mientras que en X25 se realiza
    en cada salto


En FR se pierde el control enlace a enlace pero como los enlaces
son muy fiables, la probabilidad de perdida de tramas es muy baja.

Arquitecturas de protocolos de FR.

Dos planos: 

1. Plano de control, relacion terminal-red. Protocolo
LAPD, suele ir por un canal diferente al de datos. Se encarga del
establecimiento y liberación de la conexión virtual.
2. Plano de
usuario. Se encarga de la transmisión de datos entre dos hosts
(dispositivos finales). La relación ya no es terminal-red sino
terminal-terminal, o extremo a extremo. El protocolo que se utiliza
es el LAPF. No hay control ni de flujo ni de errores. Orientado a
conexión: 

  - Entrega en orden en destino de las tramas 
  - Pequeña
    probabilidad de pérdida de tramas.


### ATM Variación del retardo de celdas

$D(i)$ retardo extremo a extremo de la celda $i$ 

$t_0$ instante q en
el que el destino recibe la 1ª celda 

$V_0$ retardo antes de pasar
la celda a la aplicación

Siguientes celdas se retardan para llegar a la aplicacion a una
tasa constante R (1/R = tiempo entre tramas)

*Ejercicio*
 Red de conmutacion de paquetes SPC 

4 conmutadores: A,B,C,D 

3 oficinas en diferentes ciudades 

La empresa solicita C V
permanentes(1 entre cada oficina) y conmutadas

Contenido de las tablas de conexiones para los 4 conmutadores

  **Conmutador D**

         Le LCIe Ls LCIs               
         d  19   a  248  <- CVP
         d  20   a  225  <- CVP
         d  30   a  485
         d  31   a  496
         a  225  d  20  <- CVP
         a  248  d  19  <- CVP
         a  485  d  30
         a  496  d  31

b) Contenido de las tablas de encaminamiento?

         Conmutador A
         Destino Enlace
         111111  b
         222222  c
         333333  d
  
         Conmutador B
         111111  d
         222222  a
         333333  a

         Conmutador C
         111111  a
         222222  c
         333333  a

         Conmutador D
         111111  a
         222222  a
         333333  d


c) CVC entre la of 1 y of 3 lo ha solicitado la of 1 ¿Qué entradas
 de las tablas de encaminamiento han sido tenidos en cuenta para
 establecer este CVC? 

         B a
         A d
         D d


d) Of 3 solicita nuevo CVC hacia la of 1. ¿Qué entradas se usan?
  
         En el D la primera 111111 a, en el A b y en el B b





# Tecnologías de interconexión de redes

Internet: Maraña de redes interconectadas y que no todas utilizan
el mismo protocolo.

## Protocolo IP

Especificado RFC 791

 Tareas principales

-   Direccionamiento, direccionar dentro de la subred de
    comunicaciones

-   Fragmentación


Características

1.  Protocolo no orientado a conexión $\rightarrow$ datagramas

2.  Fragmentación si fuera necesario

3.  Direccionamiento mediante direcciones de 32 bits (4 bytes) IPv4
    $\rightarrow$ 4 grupos de 8 bits

4.  Tamaño máximo de un datagrama es de 65.535 bytes. Tamaño min =
    576 bytes

5.  Checksum solo de la cabecera, no de los datos

6.  Campos opcionales (no requeridos)

7.  Tiempo de vida de los datagramas finito

8.  Entrega siguiendo la ley del mínimo esfuerzo


Formato de la cabecera de un datagrama (IPv4)


       <--------------------- 8 bits ----------------------->

       -----------------------------------------------------
       |       Version = 4       |   Tamaño de cabecera IP  |01
       |                Tipo de servicio                    |02
       |             Tamaño total del datagrama             |03
       |             Tamaño total del datagrama             |04
       |                   Identificación                   |05
       |                   Identificación                   |06
       |           Numeración segmentos datagrama           |07
       |           Numeración segmentos datagrama           |08
       |               Tiempo de supervivencia              |09
       |                       Protocolo                    |10
       |                 Checksum de la cabecera            |11
       |                 Checksum de la cabecera            |12
       |                   Dirección origen                 |13
       |                   Dirección origen                 |14
       |                   Dirección origen                 |15
       |                   Dirección origen                 |16
       |                   Dirección destino                |17
       |                   Dirección destino                |18
       |                   Dirección destino                |19
       |                   Dirección destino                |20
       |                       Opcionales                   |21
       |                       Opcionales                   |22
       |                       Opcionales                   |23
       |                        Relleno                     |24
       ------------------------------------------------------
       Tipo de servicio
       - - -
       Primeros 3 bits: Prioridades (hasta 8 niveles)
             - - -
             Retardo (D: Delay)
               Rendimiento (T: throughput)
                 Fiabilidad (R: Reliability)
                   - -
                   No se usan

**Tamaño total de cabecera:**
576 bytes=60 cabecera + 516 datos
2^16^ - 1 bytes = 65.535 tam max cabecera + datos


**Numeración segmentos datagrama:** identificador + offset

Identificación + Numeracion segmentos datagrama = **Fragmentación**

**Tiempo de supervivencia:** 2^8^ - 1 = 255 seg tp máx.
cuando t = 0 se destruye el fragmento

**Protocolo:** Protocolo de nivel superior = capa de transporte (TCP \& UDP)

**Checksum de la cabecera:** Se recalcula en cada salto



### Direccionamiento IP

- Redes de tipo A

         [0| Red | Host | Host | Host]
          ------- ------ ------ -----
            8        8      8     8
- Redes de tipo B 

         [10| Red | Red | Host | Host]
          -------- ----- ------ -----
              8      8      8     8
- Redes de tipo C 

         [110| Red | Red | Red | Host]
          --------- ----- ----- -----
              8       8     8     8

Clase A: 1 + 7 bits (red) + 24 bit (host) 

Clase B: 2 + 14 bits
(red) + 16 bit (host) 

Clase C: 3 + 21 bits (red) + 8 bit (host)

Dirección de un host = Dirección subred + host local Máscara de
subred, permite crear subedes cogiendo bits de host como bits de
red. Dentro de la máscara de subred todos los 1s van a indicar red
y todos los 0s indican host.

Para las redes de clase a, los bits que se utilizanpara la red son
7, para las redes de clase b, son 14 y para la clase c son 21.

El nº de bits para las máquinas, son respectivamente 24, 16 y 8.

Para la clase a, la dirección más baja es 1.0.0.1, y la más alta es
126.255.255.254

Para la clase b, la dirección más baja es 128.0.0.1, y la más alta
es 191.255.255.254

Para la clase c, la más baja es la 192.0.0.1, y la más alta es la
223.255.255.254

La 127.x.x.x es la dirección de bucle local, se usa para pruebas, y
por tanto no se puede direccionar ningún host.

El nº de redes para la clase a son : 2^7^ - 2 = 126, clase b: 2^14^
- 2, clase c : 2^21^ - 2.

El nº de hosts para la clase a son: 2^24^ - 2, clase b: 2^16^ - 2
=65534, clase c : 2^8^ - 2 = 254.


### Rangos de direcciones privadas (RFC 1918)

Para la clase A: 10.0.0.0 - 10.255.255.255 $\rightarrow$ 1 red posible

Para
la clase B: 172.16.0.0 - 172.31.255.255 $\rightarrow$ 16 redes disponibles


Para la clase C: 192.168.0.0 - 192.168.255.255 $\rightarrow$ 256 redes
disponibles

Cómo hacemos subredes desde una red? Máscaras

Por ejemplo para una red de clase A: red host host host 

La máscara
por defecto es: 255.0.0.0 

11111111.00000000.00000000.00000000

Máscara B: 255.255.0.0 

Máscara C: 255.255.255.0

En nuestro ejemplo tenemos una red cuya dirección es 192.146.46.0

Es una red de clase C.

Nos dicen que queremos dividirla en 2 subredes.

La máscara por defecto es 255.255.255.0

Pero la manipulamos para obtener dos redes.

Se utilizan siempre de izquierda a derecha.

No podemos utilizar un sólo bit, porque las direcciones
255.255.255.255 ni 255.255.255.0 no se pueden usar ¿? 

Porque no se
pueden utilizar las todo uno ni todo 0, es decir, 00 y 11 no se
pueden utilizar con máscara 11, 000 ni 111 se pueden utilizar con
máscara 111, etc.

Entonces usamos dos bits: la mascara que empieza por 10 y por 01.

Luego en la mascara añadimos los dos primeros bits del campo host:
255.255.255.192

Las primeras 64 direcciones: 192.146.46.0 - 192.146.46.64, empiezan
por 00, y no son válidas.

La primera dirección válida empieza en la 65, y está en la misma
subred que todo el rango hasta la 126. La 127 es la dirección de
broadcast para esta subred.

Otro ejemplo: Dir IP: 192.228.17.57 Máscara: 255.255.255.224

11100000

57= 00111001

¿Cuál es la dirección de subred? 00010000 = 32 ¿A qué nº de host
corresponde dentro de la subred? 25 Nº de subred: 1

Red 2, host 1 \Rightarrow 01000001 = 65 

Red 3, host 1 \Rightarrow 01100001 = 65+32
= 97

Ejemplo: Cuantas subredes podemos direccionar con una dir de tipo B
y una máscara 255.255.255.252? 

11111111.11111100 (2^14^)-2 = 16384
subredes

Cuantos hosts/subred? (2^2^) - 2 = 2 hosts/subred

Para la dirección 172.18.\_.\_ indicar la direccion más alta y la
mas baja de host. 172.18.255.250 172.18.0.5

Ejemplo: Cual es la máscara más apropiada para direccionar 3 redes
LAN con una dir de tipo B?

255.255.0.0

Para direccionar 3 redes se necesitan 3 bits: 000 y 111 no se
pueden usar: 255.255.224.0
