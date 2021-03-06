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

$F_{mod max}$ = 2H baudios (es decir, dos baudios por Hertzio)

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


Ejemplo: Canal H = 1KHz, N = 32 estados

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

Transmisión asíncrona
  ~ uso de señales de reloj diferentes en E y R, pero
    ajustadas a la misma frecuencia.

    Se produce un evento de sincronización inicial, para conseguir la
    sincronización.

    Se da una pérdida de sincronización después de unos pocos bits, es adecuada
    sólo para la transmisión de caracteres.

Transmisión síncrona
  ~ uso de la misma señal de reloj.

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


**Codificaciones basadas en niveles**:

NRZ-L (Non Return to Zero - Level)
  ~ Sin retorno a cero.

  ~ Señal binaria, unipolar (0,V) o polar (-V,V).

  ~ No adecuada para sincronismo de bit: no hay garantía de transiciones, por
     ejemplo, si tienes muchos ceros, puedesde preder el punto en el que comienza el
     ciclo.

RZ (Return to Zero)
  ~ Bipolar, con retorno a cero antes de finalizar el periodo del bit.

  ~ Señal ternaria, tres niveles:  -V = '0', 0 = referencia, +V = '1'

  ~ Garantizadas dos transiciones por bit. Si que hay presencia de información
     de sincronismo, de donde empieza y donde acaba cada ciclo. Problema, el
     interfaz es más complicado.
  

Codificaciones basadas en transiciones:

NRZ-I (Non Return to Zero - Inversion)
  ~ Señal binaria, es un código diferencial: 0 = transición al principio del
    bit. 1 = no transición al principio del bit.

  ~ La transición es al principio del ciclo.

  ~ Se utiliza bastante como codificaciones de línea, pero no hay transiciones
    garantizadas para sincronismo de bit.

Manchester
  ~ Usada en 802.3 (ethernet)

  ~ Transición para sincronismo siempre en medio del bit.

  ~ Valor del bit: sentido de la transición del medio del bit: 0 = transición
     positiva (LH), 1 = transición negativa (HL). LL ó HH son violaciones del 
     código

  ~ Código "bifase": dos transiciones por bir: 0 = $\uparrow$ 1 = $\downarrow$

  ~ Así se garantiza la info sobre sincronismo, ala mitad del bit siempre hay
     transición.

Manchester Diferencial
  ~ Usada en 802.5 (token ring)

  ~ Es binaria, diferencial.

  ~ Separa la transición de sincronismo (medio del bit) del valor:

      - 0: Presencia de transición al principio del bit.
      - 1: Ausencia de transición al principio del bit.

  ~ Antes era necesario sincronizar todos los bits, pero eso supone reducir el
     ancho de banda a la mitad (2 transiciones por bit transmitido en el peor
     de los casos). Ahora algunas de las técnicas que se ven a continuación
     relajan estas características.


AMI (Alternate Mark Insertion)
  ~ Señal ternaria y bipolar (-V, 0 , +V)

      - 0: nivel cero
      - 1: transición de signo opuesta a la última.
    
  ~ Técnicas de sustitución de ceros consecutivos por código especial:

     - B8ZS: Sustituye grupos de 8 ceros.
     - HDB3: Sustitute grupos de 4 ceros.

MLT-3 (Multi-Level Transition)
  ~ Es una mejora de AMI.

  ~ Señal ternaria y bipolar (-V, 0, +V)

     - 0: no hay transición
     - 1: hay transición al nivel contiguo (va oscilando entre los tres
       posibles niveles: -V, 0, +V, 0, -V, 0, ...)

**Codificaciones de bloque**:

- Se codifican grupos de bits conjuntamente, y a cada grupo se le asigna un
  código (grupo de símbolos) que es el que realmente se transmite.
- Necesitan una codificación final de línea (suele ser NRZL o NRZI) para la
  transmisión del código.
- Permiten eludir las codificaciones con grupos de bits problemáticos para el
  sincronismo (p.e., sin transiciones)
- **"nBmS"**:

    - **n** : nº de bits que se codifican conjuntamente.
    - **B** : indica que los datos de partida son binarios
    - **S** : tipo de señal usada para codificar los *m* símbolos (B=binaria,
      T=ternaria, Q=cuaternaria)
    - **m** : nº de símbolos que se corresponden con los n bits

Ejemplos: 4B5B, 4B3T, 2B1Q, PAM5

4B5B
  ~ Usada en FDDI y Fast Ethernet, en combinación con NRZI.

     Objetivo:

     - Garantiza al menos una transición de sincronismo cada 4 bits.
     - Se elimina la posibilidad de transmitir más de tres 0's consecutivos.

     Cada grupo de 4 bits de datos se corresponde con un grupo de 5 símbolos
     binarios. Se eligen aquellos códigos en los que no se van a dar nunca más
     de 3 bits de código iguales concatenando cada secuencia.

     *Continuará, pag 9 de RED Tema2-1*

2B1Q
  ~ 2 bits se codifican con 1 símbolo cuaternario: -2, -1, +1, +2

PAM 5x5:
  ~ Señal de 5 niveles (-2, -1, 0, +1, +2). 4 bits se codifican con 2 símbolos
     (5^2 = 25 > 2^4 = 16)

Balance de DC
  ~ Elección de las combinaciones no sólo para sincronismo, sino también para
    equilibrado de la tensión de la línea (señales polares y bipolares).

Rendimiento
  ~ R = 100 * bits de datos / baudio

    - **NRZI, NRZL, AMI, MLT3** 100% porque en el peor de los casos hay una
      transición por cada bit.
    - **Manchester, Manchester diferencial** 50% (dos transiciones por bit)
    - **4B5B** 80%: 4 bits / 5 baudios
    - **4B3T, 8B6T**: 133%: 4 bits / 3 baudios
    - **2B1Q, PAM5x5**: 200%: 2 bits/1 baudio, 4 bits/2 baudios

Scrambling
  ~ Mezclado de los bits para convertir la secuencia original en una
    pseudoaleatoria, y minimizar la probabilidad de secuencias de 0's y 1's
    consecutivos.

Consideraciones espectrales
  ~ Mejor cuanto menos componentes de alta frecuencia tenga la señal (MLT3 o
    AMI mejores que Manchester)

## Técnicas de Modulación

Para transmitir información digital como analógica.

Modulación
  ~ Modificación de las propiedades de una señal ondulatoria (la señal
    portadora). Es decir, cambiamos algún parámetro.

Tenemos que analizar sus parámetros característicos para modificarlos. Toda
señal ondulatoria se puede representar como:

$$s(t) = A \sin (2 \pi f t + \varphi_0) $$

A
  ~ Amplitud máxima, la real viene dada por el tiempo

f
  ~ Frecuencia (1/T)

$\varphi$
  ~ Fase, es la responsable de la evolución en el tiempo de la señal.

    $$\varphi = 2 \pi f t + \varphi_0$$

    $2 \pi f$: frecuencia angular (nº de vueltas / unidad de tiempo)


Posibilidades de variar los diferentes parámetros con una frecuencia de
modulación Fmod (distinta de la frecuencia original de la onda portadora, fp):

- A y f permanecen estables
- $\varphi$ va variando con el tiempo t, puede incrementarse su valor en
  $\Delta \varphi$

Ejemplos de variaciones *ver Pág.11 RED Tema2-1.pdf*

Técnicas de modificación de parámetros:

ASK (Amplitude Shift Keying):
  ~ Modulación por desplazamiento de la amplitud, se conservan la fase y la
    frecuencia.

    Usamos una amplitud para el 0 y otra para el 1 (una de ellas podría ser
    0V).

    Dos frecuencias: la de la onda portadora f~p~ = 1/T (que debe estar en el
    rango del ancho de banda de la onda) y la de modulación (en la que cambia 
    la amplitud) F~mod~ [^2]

    Problema: muy susceptible a la atenuación, ya que como ésta ataca la
    amplitud, se podría llegar a confundir si es '0' o '1'.

[^2]: Aquí se habla de frecuencias, pero en realidad lo que se cambia es la
amplitud. Supongo una ida de pinza del ComicSansMan.

FSK (Frequency Shift Keying):
  ~ Modulación por desplazamiento de la frecuencia de la portadora, se
    conservan la amplitud y la fase.

    Se usa una frecuencia para el '0' y otra para el '1'.

    Problema: nº de frecuencias alternativas reducido, luego permite transmitir
    pocos bits por baudio. Si se usan muchas frecuencias (4 o más), la señal se
    vuelve muy débil respecto al ruido.

PSK (Phase Shift Keying):
  ~ Modulación por desplazamiento de la fase al valor asignado al nuevo estado.
    Modificar la fase es el cambio más robusto. '0' = $\varphi_0$ y
    '1'=$\varphi_1$

    Muy robusta frente a ruidos y distorsiones.

    Permite muchos estados diferentes (16, 32, etc).

    Se suele poner 1º el nº de estados: 4-PSK, 8-PSK...

    Ejemplo: dos fases: $\varphi_0$ = 0º, $\varphi_1$ = 180º.

DPSK (Differential PSK):
  ~ El estado de la constelación representa un incremento de la fase, con
    respecto al valor de la fase de la portadora en el instante de modulación:

    $$\varphi ' = \varphi + \Delta \varphi$$

    Depende del estado anterior de la portadora.

    Ejemplo: 4-DPSK tiene una "constelación" de 4 estados. Cada estado (que
    ahora represent un incremento de la fase) se asigna igualmente a un dibit
    (2 bits de datos).

    - 


## Medios de Transmisión

*Ver 'RED Tema2_2.pdf'*



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




# Capa de Enlace (Resumen)

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

Cuando se detecta una colisión se interrumpe la transmisión.

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



