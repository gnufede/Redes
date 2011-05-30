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

* BEC (Backwards error correction)
  ~ Corrección de errores hacia atrás. Si hay error se vuelve a retransmitir 
     el paquete. Es útil si los errores son escasos o el retardo es bajo (los 
     paquetes tardan poco en llegar de origen a destino)

* FEC (Forward error correction)
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

