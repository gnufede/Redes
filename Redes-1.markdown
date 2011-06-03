% Redes
% Federico Mon
% 2010-2011

# Capa Física

Señal
  ~ Cambio en alguna propiedad del medio, que se propaga a través de éste.

Retraso de propagación
  ~ La propagación no es instantánea, influyen la velocidad de propagación
    (fracción de la velocidad de la luz) y la longitud del medio.

    $T_{prop}(s) = \frac{long (m)}{vel_{prop}(m/s)}$

Modulación
  ~ Acción de cambiar la señal.

Frecuencia de Modulación
  ~ Frecuencia con la que cambiamos la señal. Se mide en baudios ($s^{-1}$),
    indica los cambios por segundo.

Velocidad de transmisión de datos
  ~ Depende de la frecuencia de modulacion y se mide en bits por segundo.

    $V_{datos}(bps) = F_{mod} (baudios) * B (bits/baudio)$

B
  ~ Cantidad de información transmitida con cada cambio de señal. Depende del 
    nº de estados posibles de la señal

Ancho de banda 
  ~ Mayor frecuencia de señal que se puede enviar por un medio de transmisión.

Teorema de Fourier
  ~ Aproximación de frecuencias a una señal cuadrada Se suman todos los 
    armónicos. Para tomar el valor 0 o 1 hay que tomarlo lejos de la transición.


## Teorema de Nyquist

Canales o medios de transmisión
  ~ Dejan pasar la señal, se comporta como un filtro en el dominio de la
    frecuencia, dejando pasar sólo un rango de frecuencias restringido: ancho
    de banda H del canal.

Un canal es apropiado para transmitir una señal si deja pasar el ancho de banda
efectivo d la misma.

El teorema de Nyquist relaciona el ancho de banda de un canal con la frecuencia
de modulación de la señal: "el ancho de banda H mínimo necesario para
transmitir n baudios es H~n~ = n/2"

Es decir, si tenemos F~mod~ = n bandas necesitamos un canal con $H \ge \frac
{n}{2}$ (Hz)

Puede expresarse al revés, la frecuencia máxima teórica de modulación para un
canal ideal con ancho de banda H y N posibles estados:

F~mod max~ = 2H baudios (es decir, dos baudios por Hertzio)

Esta frecuencia máxima es teórica, en la práctica llegar al límite da
problemas, es difícilmente alcanzable, se suele hacer 1 baudio por Hz.

V(bps) = F~mod~ * B = F~mod~ * log~2~N
V~max~(bps) = 2 * H * log~2~N


Ruido
  ~ Cualquier cosa que impide o dificulta la comunicación. Hay muchos tipos de 
    ruidos:

Ruido blanco
  ~ Espectro más o menos plano. Compuesto por un gran número de frecuencias. 
    Motivado por la agitación térmica de los electrones.

Diafonía
  ~ Consiste en la interferencia que provoca su canal adyacente, interferencias 
    en el teléfono.

Intermodulación
  ~ Fenómeno bastante complejo que sucede en medios no lineales. Parte de la 
    energía de su armónico se transfiere a otro armónico, luego la onda cambia.

Ruido Impulsivo
  ~ Provocado por interferencias electromagnéticas externas (rayo, fluorescente,
    instalaciones eléctricas, etc) se superponen las ondas y pueden cambiar el 
    valor de la señal.

Distorsión por atenuación
  ~ Se pierde energía por el camino, pero no se pierde por igual en todas las 
    frecuencias.

Distorsión por retardo
  ~ En los medios reales no todos los armónicos se propagan a igual velocidad.

Distorsión de camino
  ~ Se produce cuando la señal tiene el mismo camino en llegar desde el emisor 
    al receptor. Y claro, hay caminos más largos que otros.
    (*distinto camino?*)


El ruido afecta por la relación Señal/Ruido (SNR): cociente entre la potencia
de la señal y el ruido

El valor de SNR se suele proporcionar en escala logarítmica (en decibelios,
db):

SNR~dB~ = 10 * log~10~(SNR) (dB)

Ejemplo: SNR~dB~ = 30dB = SNR = 1000

Cuanto mayor sea SNR, menor será el efecto distorsionador del ruido sobre la
señal original.


## Teorema de Shannon

Capacidad máxima de transmisión de datos de un canal real (con ruido) de ancho
de banda H:
V~max~ = H * log~2~(1+SNR) (bps)

Tiene en cuenta que la cantidad de ruido aumenta al hacerlo el ancho de banda
usado.

El teorema de Shannon acota en la práctica el número de estados posibles de la
señal que podemos utilizar en el teorema de Nyquist.

$2 H log_{2}N \le Hlog_2(1+SNR)$

$log_{2}N$ son bits, habrá que bajar N hasta que se cumpla, si no, no será
viable.


Ejemplo: Canal H = 1KHz 
N = 32 estados
Canal ideal: $V_{max} = 2H*log_2 32 = 10kbps$
Canal real: $SNR_{db} = 20 dB \rightarrow SNR = 100$
$V_{max(Shannon)} = H*log_2(100+1) = 1000 log_2(101) = 6.8 kbps$

Hay que bajar N:
 
$2000 log_2(N) < 7 kbps \rightarrow log_2(N) < 3.5 \rightarrow$ por ejemplo
$log_2(N) = 3$ bits/baudio $\rightarrow$ señal de 8 estados $\rightarrow
2H*log_2(8) = 2*1000*3 = 6kbps$

## Sincronismo:

Forma de garantizar que el receptor pueda detectar la ocurrencia de sucesos
clave de la comunicación. Tres clases de sincronismo:

  - Sincronismo de bit
  - Sincronismo de byte o carácter
  - Sincronismo de trama o bloque

### Sincronismo de bit

Método usado para que el receptor R calcule correctamente cada intervalo de bit
en la señal procedente del emisor E. Hay dos alternativas:

- Transmisión asíncrona: uso de señales de reloj diferentes en E y R, pero
  ajustadas a la misma frecuencia.

    Se produce un evento de sincronización inicial, para conseguir la
    sincronización.

    Se da una pérdida de sincronización después de unos pocos bits, es adecuada
    sólo para la transmisión de caracteres.

- Transmisión síncrona: uso de la misma señal de reloj.

    Misma señal física en E y R: distancias muy cortas.
    Señal de reloj incorporada ea los datos en forma de transiciones:
    codificaciones que garanticen una transición cada uno o varios bits.

    No se pierde la sincronización nunca: orientada a la transmisión de tramas de
    miles de bits.


### Sincronismo de carácter

Usado en transmisión asíncrona (orientada a carácter):

- Detección del comienzo de un nuevo carácter mediante transmisión negativa:
  "bit de start"
*Pag 6 RED Tema2-1.pdf*

### Sincronismo de trama o bloque

Usado en transmisión síncrona (orientada al bloque): detección del comienzo de
una nueva trama mediante código de sincronización reservado:

  a) BISYNC: varios caracteres reservados "SYNC" consecutivos.

      SYNC SYNC SOH Cabecera STX Bloque datos ETX Checksum
  b) HDLC: byte reservado denominado "flag" ("01111110")

      01111110 Dirección Control Bloque datos Checksum 01111110

## Transmisión Analógico / Digital

Los datos pueden ser de naturaleza analógica o digital, al igual que las
señales, tenemos 4 combinaciones:

- Datos analógicos y señales analógicas: medio tradicional de transmisión de
  teléfono, radio o televisión.

- Datos analógicos y señales digitales: digitalización previa de los datos
  analógicos (códecs de audio y video: PCM, MPEG)

- Datos digitales y señales digitales: codificación de los bits de datos en
  señales digitales.

- Datos digitales y señales analógicas: modulación de una señal analógica: onda
  portadora (modificación de su amplitud, frecuencia, fase)

## Técnicas de codificación

Generación de la forma de onda de la señal: codificaciones de línea:

- Basadas en:
    + **Niveles**: El nivel de la señal determina el valor del bit.
    + **Transiciones**: El valor del bit va asociado a una transición.

- De acuerdo a la naturaleza de la señal:
    + **Unipolar**: niveles 0 y +V (tiene componente DC)
    + **Polar**: niveles -v y +V (no tienen componente DC)
    + **Bipolar**: niveles -V 0 y +V.

- De acuerdo al número de niveles usados:

    Binaria, ternaria, cuaternaria...

- Diferencial:

    La señal depende del nivel en el bit o baudio anterior.


Codificaciones basadas en niveles:

NRZ-L (Non Return to Zero - Level)
  ~ Sin retorno a cero.

  ~ Señal binaria, unipolar (0,V) o polar (-V,V).

  ~ No adecuada para sincronismo de bit: no hay garantía de transiciones...




## Medios de Transmisión

*Continuará*

# Capa de Enlace

Funciones:

1.  Proporcionar una **interfaz** bien definida a la capa de red
2.  Proporcionar a la capa de red un medio físico sin errores (**Gestión de 
    errores**)
3.  **Control de flujo**: consiste en que un receptor lento puede decirle a un 
    emisor lento que pare la conexión.
4.  **Enmarcado**: Agrupar el flujo continuo de bits en tramas
 
Servicios:

1. Sin conexión:
     i. Sin confirmación
    ii. Con confirmación
2. Orientado a conexión fiable.
      i. Establecimiento de conexión.
     ii. Transmisión
    iii. Cierre de conexión

SAP's único o múltipe. Primitivas tipo L. CONNECT. request

## Control de Errores

Errores de bit: aislados o ráfagas (entrelazados)

Detección

Corrección:

BEC (Backwards error correction)
  ~ Corrección de errores hacia atrás. Si hay error se vuelve a retransmitir 
     el paquete. Es útil si los errores son escasos o el retardo es bajo (los 
     paquetes tardan poco en llegar de origen a destino)

FEC (Forward error correction)
  ~ Corrección de errores hacia delante. Se transmite información redundante
     para detectar y corregir.

Detectar - corregir con códigos de bloque (distancia de Hamming, 
convolucionales o Reed Solomon)

Detección de errores:

  * Paridad: bit de paridad y checksum.
  * CRC: Códigos polinómicos


## Corrección de errores:

En BEC, directamente se retransmite el paquete con errores.

ARQ (Automatic repeat reQuest)
  ~ Solicitud de reenvío automático 

ACK
  ~ Mensaje de confirmación

Timeout
  ~ Temporizador de seguridad en emisión. Si llega al tiempo límite sin 
     respuestas reenvía la trama.


Retardo de propagación
  ~ $T_p =  \frac{distancia}{V_{propagacion}}$

Retardo de transmisión
  ~ $T_x =  \frac{tamaño trama}{V_{transmision}}$

$a = \frac{T_p}{T_x}$

ARQ Simple: Parada y espera
  ~ Transmite Trama N. Hasta que no recibe ACK(N) no pasa a transmitir la 
    trama N+1. Es sencillo y bueno si no se espera mucho al ACK.

    Rendimiento:

    $\frac{1}{1+2a}$

ARQ Continuo
  ~ No impone restricciones de parada a la espera de confirmación. Almacena las
    tramas que ha mandado en la lista de retransmisión, cuando recibe ACK las 
    saca de la lista.

    Llega un momento en el que el tamaño de la lista de retransmisión se hace 
    constante.

    Rendimiento:

    $\frac{k}{1+2a}$ siendo $k$ el nº de tramas de la lista de retransmisión.

Situaciones problemáticas en ARQ Simple:

  - **Pérdida de trama o error**: Si el receptor detecta error se descarta la 
     trama, luego no envía ACK.

     Para recuperarse: cuando se cumple el tiempo de espera máximo del ACK y
     no ha recibido ACK, se retransmite.


  - **Pérdida de ACK(N)**
       Éste es un problema de verdad:

       Receptor recibe y procesa correctamente Trama(N)

       Emisor no recibe ACK(N), luego retransmite Trama(N)

       El receptor tiene que distinguir esta Trama(N) como duplicado:
       - Detectar duplicado (nº de secuencia)
       - Descartar duplicado
       - Confirmar recepción enviando ACK(N)


Situaciones problemáticas en ARQ continuo:

* 2 técnicas: Retroceso-N y Retransmisión selectiva.
* **Retroceso-N**:

    Cuando detecta error retrocede hasta la trama que provocó el error y
    retransmite desde ahí.

    **Pérdida de trama:**
      - Receptor detecta error por pérdida de secuencia (Esperaba N+1 y recibe N+2
        porque ha habido error y ha ignorado la trama N+1)
      - Receptor envía NAK(N) = confirmación negativa
      - Emisor recibe NAK(N) y vuelve a la secuencia N+1, N+2 ...

    Pérdida de ACK(N+1):
      ~ Se usa confirmación retardada, una trama ACK(N+2) confirma todas las
        anteriores.

        Si sigue habiendo error se detecta por timeout.

    Pérdida de NAK(N):
      ~ Se soluciona mediante el temporizador del emisor, receptor envía NAK y
        no procesa el resto, cuando salta el timeout comienza a transmitir la
        secuencia.

* **Retransmisión selectiva**:
  
    Se retransmiten sólo las tramas con error, el receptor acepta las tramas
    fuera de secuencia (lista de recepción). Se confirma cada trama, no puede
    haber confirmación retardada.

    Pérdida de trama:
      ~ El emisor lo detecta por ausencia de ACK o por timeout.

    Pérdida de ACK:
      ~ Igual, emisor retransmite N+1 pero al llegar al receptor este comprueba
        que es un duplicado, no la procesa y manda ACK(N+1)

El nº de bits que se asigna para el nº de secuencia no es arbitrario, depende
de la técnica empleada.

El nº de secuencia permite distinguir tramas entre sí y que el receptor
distinga entre situaciones posibles.

* **ARQ Simple**: 2 posibles situaciones: 
    * N+1 (OK)
    * N(Duplicado)

    Se necesita $log_22 = 1$ bit para el nº de secuencia

* **ARQ Continuo con retroceso N**: K+1 situaciones:
    * N+1 (OK)
    * (N, N-1,...,N-K+1)(duplicado) hay K posibilidades

     Se necesita $log_2(K+1)$ bits para el nº de secuencia

* **ARQ Continuo con retransmisión selectiva**: 2K situaciones: 
    * (N+1,N+2,...,N-K+1)(OK, tramas nuevas)
    * (N, N-1,...,N-K+1)(duplicado) hay K posibilidades

    Se necesita $log_22K$ bits para el nº de secuencia.


Confirmación "piggyback" (incorporada)
  ~ Aprovecha que hay transmisión en ambos sentidos para incorporar la
    confirmación de las tramas recibidas en las enviadas, estas tienen que 
    tener campos para el nº de secuencia propio y el de confirmación. Debido a 
    que puede no haber transmisión en un sentido o ser esporádico sólo se usa 
    la confirmación piggyback cuando se puede.

## Control de flujo

El receptor regula la velocidad de transmisión del emisor, porque debe
almacenar y procesar las tramas. Tipos de mecanismo orientados a la trama:

Crédito
  ~ El emisor dispone de un crédito inicial. Cada vez que transmite se le resta
    del crédito el nº de bytes transmitidos. El receptor le concede créditos en
    los mensajes de confirmación.

Ventana
  ~ El receptor le impone al emisor el tamaño máximo que puede tener la lista
    de retransmisión (en nº de tramas).


## Especificación de protocolos

Formas de especificar el comportamiento de las entidades de la capa:
* Pseudocódigo / Lenguaje de alto nivel
* Diagramas de estados (diferente detalle)
* Tabla de eventos

Ejemplo: fase de establecimiento de conexión (diagrama de secuencia)

*Ver diagrama final página 3 - Resumen T3.pdf*

## Protocolos de la capa de Enlace de Datos

BSC (Binary Synchronous Control)
  ~ Protocolo orientado al carácter. Trama formada por caracteres de control.
    Syn (sincronización), soh (comienzo de cabecera).

    Ya no se utiliza, los actuales están orientados a bit.

HDLC
  ~ PPPoE está basado en HDLC (High-level Data Link Control). Proviene del SDLC
    de IBM. Ha evolucionado a LAP (LAP-B y LAP-D).

    Protocolo orientado a bit.

    Dos modos: punto a punto (ABM) y multipunto (NRM)

    El modo habitual es ABM.

    Formato de trama básico:
      - Flag: 8 bits
      - Dir: 8 bits
      - Control: 8 bits
      - Información: 0-N bits
      - F: 8 bits
      - S: 8 bits
      - Flag: 8 bits

    Flag: '01111110' indica comienzo o fin de trama. Si hay 5 unos seguidos, se
    inserta un cero, el receptor lee 5 unos y si viene un cero, lo quita, si
    viene un 1 es el flag.

    Dir: dirección

    Control: Tipos de trama / nº de secuencia

    a) Tramas de información: *Ver pág 4 de Resumen T3.pdf*

        8 bits: 0,N(S),P/F,N(R)

        N(S) = Nº secuencia (3 bits)

        N(R) = Nº secuencia ACK piggyback (3 bits)

        P/F = pregunta/final (trama comando/respuesta) (1 bit)

    b) Tramas de supervisión:

        8 bits: 1,0,S(2 bits),P/F,N(R)(3 bits)

        S = 

        - RR (receptor preparado) (ACK)
        - RNR Receptor no preparado
        - RET Rechazo (NAK)
        - RET Rechazo selectivo

    c) Tramas no numeradas:

        8 bits: 1,1,M(2 bits),P/F,M(3 bits)

        M =
        - SABM: Solicitud conexión modo ABM (campo DIR = opciones de conexión)
        - DISC: Solicitud de desconexión
        - UA: ACK no numerada

    Detalles HDLC:

    - Usa piggyback
    - Usa retroceso-N / retransmisión selectiva
    - HDLC extendido usa 16 bits para control (nº secuencia 7 bits)

    LAP-B
      ~ WAN's X.25
        Como HDLC / ABM

    LAP-D
      ~ WAN's RDSI

        Añade servicio sin conexión (no hay nº secuencia)

        Nuevo tipo de trama no numerada: UI (info no numerada)

        Nueva primitiva para este servicio

        Servicio orientado a conexión: aceptación expresa de la petición
        reconexión (L.CONNECT.Response)


    LAP-F:
      ~ Frame Relay

    LLC:
      ~ LAN's control enlace lógico IEEE 802.2

        Formato trama *Ver fin pág. 5 Resumen T3.pdf*


## Enmarcado

Se trata de traducir el flujo continuo de bits a tramas diferenciadas.

### Tamaño

Se utiliza un campo longitud donde se indica la longitud de la "carga".

Problema: si se daña el campo longitud, perdemos la cuenta de dónde termina la
trama, y a partir de ahí, perdemos todas las tramas.

### Violación de código

Se trata de violar el sincronismo de bit a nivel físico para indicar que
comienza una trama nueva.

De esa manera aunque falle el campo longitud, sabremos dónde comienza la
siguiente trama.

### Inclusión de caracteres de comienzo y fin

Para protocolos **orientados a carácter**, se añaden dos caracteres, uno al
principio y otro al final (STX y ETX).

Si lo que transmitimos es texto, no hay problema, estos caracteres son 
especiales, no son imprimibles.

Si lo que transmitimos es binario, entonces puede que aparezca la configuración
de bits STX o ETX en la trama, entonces se usa la transparencia de datos para
solucionar ésto: ponemos delante otros caracteres: DLE y DLT. Si en la
configuración de bits original apareciesen los caracteres DLE o DLT, se inserta
otro DLE extra, de manera que el receptor al detectar dos seguidos, deja uno.

Para protocolos **orientados a bit**, se usa la transparencia de datos,
insertando las cadenas '01111110' al principio y al final de la trama. Ésta
cadena no se puede dar dentro de la trama porque si el emisor detecta 5 unos
seguidos, inserta un 0, y el receptor al detectar 5 unos seguidos, quita el 0
que venga detrás.

# Tema 4: Control de Acceso al Medio (MAC)

## Introducción

En redes de difusión, bajo la capa de enlace lógico.

En un medio compartido por muchos hosts. Veremos accesos múltiples y técnicas
de protocolos MAC. Ver quién tiene derecho a transmitir y ver que las trmas
tengan información de emisor o receptor. Sobre todo redes de difusión LAN's y
MAN's.

Arquitectura IEEEE (802)

------------ -----------------
 LLC (802.2)  Enlace de datos
------------ -----------------
     MAC                       
------------ -----------------

No todas las tecnologías de medio compartido encajan dentro del std 802, pero
sí la mayoría. Por ejemplo la TV por cable tiene acceso múltiple pero no
pertenece a esta arquitectura.


Protocolos MAC
 
- Sin restricciones
- Con restricciones (libre de colisiones)

    + Control centralizado
    + Control distribuido


## Protocolo sin restricciones

### ALOHA

Diseñado para radio de Hawai. Estaciones hacia ord3enador central en una de las
islas (C), y terminales que quieren acceder (T). Si acceden al canal (UHF) 
varias estaciones a la vez se produce colisión.

No gestiona colisiones a nivel MAC, si no recibe ACK después de un tiempo, se
retransmite (tras un intervalo aleatorio).

El período de vulnerabilidad es el intervalo de tiempo durante el cual si se
inicia otra trama, se produce una colisión.

### ALOHA Ranurado

División del tiempo en ranura. Sólo se puede transmitir al inicio de la ranura,
que es de tamaño aproximado de lo que se tarda en enviar una trama. El período
de vulnerabilidad se reduce a L.

### CSMA

Acceso múltiple con detección de portadora.

Antes de transmitir se mira si hay alguien transmitiendo. Cada estación escucha
el medio. Si hay alguien transmitiendo espera a que quede libre y luego
retransmite.

Hay dos causas de colisiones:

  a) 2 estaciones esperando a que termine una 3ª.
      Se da en CSMA persistente. En CSMA no persistente al ver que el canal
      está ocupado se genera un intervalo aleatorio antes de volver a mirar.

  b) Por retardo de propagación.
      Al comprobar B si A está transmitiendo, la señal de A le llega con
      retardo. B puede empezar a transmitir cuando A ya está transmitiendo
      (aunque B no lo sabía porque no le había llegado la señal). Siempre va a
      existir este problema.

Período de vulnerabilidad: retardo de propagación entree extremos.

### CSMA/CD: CSMA con detección de colisiones

Cuando se detecta una colisión se interrumple la transmisión.

La detección de colisiones no es inmediata.

El control se hace ocupando el ancho de banda del canal (bajan las 
prestaciones)

## Protocolos libres de colisiones

### Solicitud / concesión

### Mapas de bits

### Ranuras

### Testigo

## Interconexión de Redes de Difusión

## Tecnologías estándares LAN/MAN

### Ethernet (802.3)

### Ethernet 10 Mbps

### Fast Ethernet (802.3u)

### Gigabit Ethernet

### 10 Gigabit Ethernet

### Token Bus (802.4)

### Token Ring (802.5)

### FDDI (interfaz de datos distribuido de fibra)

### DQDB (802.6)

### Wifi (802.11)

### Wifi (802.11a)

### Wifi (802.11b)

### Wifi (802.11g)

### Wifi (802.11n)

## Gestión de LLC sobre canales físicos

## Gestión de canal físico en BSS convencional

## Formato de trama MAC



\newpage

# Capa de Transporte (Cap 17 Stallings)

**Importante**: DNS y ejercicios de DNS

### Establecimiento de conexión TCP

  - Host1 envía Syn(seq=x).
  - Host2 envía Syn(seq=y, ack=x+1)
  - Host1: Syn(seq=x+1,ack=y+1)
  
  Conexión establecida


Posibles problemas:

  - Establecimiento de conexión simultáneo

    - Host1: Syn(seq=x)
    - Host2: Syn(seq=x)
    - Host2: Syn(seq=y,ack=x+1)
    - Host1: Syn(seq=y,ack=x+1)
 
    Es un acuerdo a tres vías, y la conexión se establece correctamente.

### Gestión de las ventanas en TCP

Tenemos un emisor que a lo largo del tiempo quiere enviar 2kbytes de datos a un
receptor.

Tenemos un receptor que tiene un buffer de 4kbytes que originalmente está
vacío.

El emisor envía los 2kbytes en la seq=0.

El buffer del receptor tiene ahora los dos primeros K ocupados.

El receptor le envía un ACK de la seq=0 (es decir: ACK=2048) y le dice que
quedan libres 2048 (WIN=2048)

Ahora un programa del emisor quiere enviar 3kbytes.

El emisor envía otros 2k, con seq=2048.

El buffer del receptor está ahora lleno.

El receptor envía ahora ACK=4098,WIN=0

Ahora una aplicación (en la capa de aplicación) del receptor, lee los dos
primeros Kbytes del buffer, luego borra esos dos primeros Kbytes del buffer.

Ahora el receptor envía un ACK=4096,WIN=2048.

Hasta este momento el emisor quedó bloqueado esperando.

Ahora el emisor envía el Kbyte que le queda, con seq=4096.


Entonces:
  - Los emisores no tienen que emitir los datos tan pronto como los reciben de
    la capa de aplicación.
  - Los receptores no necesitan enviar ACK's tan pronto como reciben los datos.



### Gestión de los temporizadores


En la capa de enlace se establece un temporizador para saber cuándo se ha
recibido un ACK o no, si hay que volver a emitir el paquete.

En la capa de enlace suelen llegar todos, porque funciona en una red local,
manejable.

Sin embargo en la capa de transporte no es así. La curva es diferente.

Si ponemos el temporizador demasiado corto, es muy probable que muchos ACKs se
pierdan, y provocamos que haya muchas retransmisiones de tramas. Pero si lo 
ponemos muy largos, provocamos retardos, si hay que volver a reenviar un
paquete, se tarda más en hacerlo.

Para solucionar ésto, uno de los algoritmos más utilizados para saber cuánto
debe durar un temporizador es **el algoritmo de Jacobson**.


\newpage

# Tema 7 - Capa de Aplicación - DNS y SMTP

Última capa del modelo TCP/IP, es la capa donde están todas las aplicaciones de
usuario.

Las capas por debajo ofrecen un transporte confiable.

Hay otro servicio aparte del TCP: el UDP, que es un servicio no fiable. La capa
de transporte no hace detección de errores, se lo deja a la capa de aplicación.

La capa de aplicación necesita protocolos de apoyo que permitan el
funcionamiento de las aplicaciones reales.

Hay varias áreas en las que actúan estos protocolos de apoyo:

  1. la seguridad.
  2. servicio de nombres
  3. Protocolo para la administración de la red


Las aplicaciones reales son muchas: el correo electrónico, la WWW, aplicaciones
multimedia, etc.

## DNS - Servicio de nombres de dominio

  - Los programas hacen referencia a host, buzones de correo, etc, mediante el
    uso de cadenas ASCII no mediante las direcciones binarias de red.
  - En los tiempos de ARPANET había un fichero llamado hosts.txt en todos los
    hosts conectados y ahí se listaban todos los hosts y sus direcciones IP.
    Cada noche todos los hosts obtenían este fichero de la instalación que lo
    mantenía.
  - Cuando miles de estaciones se conectaron a la red, este enfoque o podía
    permenecer y se inventó el DNS (Domain Namer System).
  - Para relacionar un nombre con una IP, un programa de aplicación llama a un
    procedimiento de la biblioteca llamado resolvedor. El resolvedor envía un
    paquete UDP a un servidor DNS local, este busca el nombre y devuelve la IP
    al resolvedor y éste al solicitante.

### El espacio de nombres DNS

La administración de un espacio de nombres muy grande y cambiante es un
problema difícil, se usa para solucionarlo un direccionamiento jerárquico.

*Ejemplo*:

  - Calle Gran Vía, Madrid, Madrid, Comunidad de Madrid
  - Calle Gran Vía, Murcia, Murcia, Región de Murcia


Internet se divide en cientos de dominio de nivel superior, cada uno abarca
muchos hosts. Cada dominio se divide en subdominios y estos subdominios
nuevamente, etc. Todos los dominios pueden representarse mediante un árbol.

Los dominios se pueden representar como un árbol.


Los nombres de dominio no  distinguen entre mayusculas y minusculas.

Los nombres de componentes pueden tener 63 caracteres y los de trayectoria
hasta 255.

Cada dominio controla todos los subdominios que tiene debajo.

Los dominios reflejan límites organizacionales no redes físicas. No están
necesariamente relacionados.

#### Registros de recursos

Cada dominio, host individual o de nivel superior, puede tener un grupo de
registros de recursos asociados a él.

En un host individual, el registro más común es simplemente su IP.

Cuando un resolvedor da un nombre a un dns lo que recibe es el registro de
recursos asociado a ese nombre.

La función real de DNS es asociar nombres a registros de recursos. Un registro
de recursos tiene 5 tuplas.

Nombre de dominio, tiempo de vida, tipo (), clase (para internet siempre es IN)
y valor (puede ser un nº, un nombre de dominio o una cadena).

Tipo:

  - SOA: Proporicioina información sobre la zona
  - A: Contiene una dirección IP
  - MX: especifica el nombre de dominio que está preparado para aceptar correo
    electrónico del dominio especificado
  - AME: Creación de alias
  - PTR: Puntero a otro nombre.
  - HINFO: Para conoocer tipo de máquina y S.O.
  - TXT: Permite a los dominios indentificarse.



Base de datos para cs.vu.nl. 86400[^1] es el contenido del campo tiempo de vida.

      cs.vu.nl       86400     SOA   IN    star boss (...)
      cs.vu.nl       86400     TXT   IN    "Facultad de informatica"
      cs.vu.nl       86400     TXT   IN     "Univ. Amsterdam"
      cs.vu.nl       86400     MX    IN     1 zephyr.cs.vu.nl
      cs.vu.nl       86400     MX    IN     2 top.cs.vu.nl
      
      flits.cs.vu.nl 86400     HINFO IN     Sun Unix
      flits.cs.vu.nl 86400     A     IN     130.37.16.112
      flits.cs.vu.nl 86400     A     IN     192.31.231.165
      flits.cs.vu.nl 86400     MX    IN     1 flits.cs.vu.nl
      flits.cs.vu.nl 86400     MX    IN     2 zephyr.cs.vu.nl
      flits.cs.vu.nl 86400     MX    IN     3 top.cs.vu.nl
      www.cs.vu.nl   86400     CNAME IN     star.cs.vu.nl
      ftp.cs.vu.nl   86400     CNAME IN     zephyr.cs.vu.nl

[^1]: Los días de 24 horas tienen 86400 segundos.


Para evitar tener problemas asociados a una sola fuente de información se
definen zonas. Cada zona contiene una parte del árbol. Cómo se establecen las
zonas es reponsabilidad del administrador.



