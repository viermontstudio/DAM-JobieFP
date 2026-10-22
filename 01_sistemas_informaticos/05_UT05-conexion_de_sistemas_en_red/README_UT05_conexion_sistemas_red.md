# 🛠️ UT05 — Conexión de Sistemas en Red

## 1. Protocolos Principales de Red y Clasificación [Concepto]

* **Concepto de Protocolo de Red [Concepto]:** Conjunto formal de reglas, sintaxis, semántica y procedimientos que definen el formato y la secuencia en que dos o más sistemas informáticos intercambian información a través de un medio de transmisión.
* **Clasificación por Propiedad y Estandarización [Concepto]:**
  * **Protocolos Abiertos:** Basados en estándares internacionales públicos y no propietarios (desarrollados por organismos como la **IETF** (**I**nternet **E**ngineering **T**ask **F**orce) o el **IEEE** (**I**nstitute of **E**lectrical and **E**lectronics **E**ngineers)). Permiten la interoperabilidad universal entre diferentes fabricantes (ej. **TCP/IP**, **Ethernet**, **HTTP**).
  * **Protocolos Cerrados / Propietarios:** Diseñados y patentados por empresas privadas. Requieren licencias comerciales para su uso o funcionan exclusivamente en hardware del mismo fabricante (ej. el antiguo **NetBEUI** de Microsoft, **AppleTalk** de Apple o versiones propietarias de protocolos de enrutamiento).
* **Clasificación por Orientación a la Conexión [Concepto]:**
  * **Orientados a la Conexión:** Exigen la negociación previa y el establecimiento de una sesión de comunicación lógica entre emisor y receptor antes del envío de datos. Garantizan alta fiabilidad, control de flujo y retransmisión de paquetes perdidos, a costa de una mayor sobrecarga (*overhead*) y menor velocidad. *(Ejemplos: **TCP**, **Frame Relay**, **ATM**).*
  * **No Orientados a la Conexión:** Envían bloques de información (datagramas) directamente al destino sin verificar previamente si el receptor está disponible o listo para recibir. Ofrecen la máxima velocidad y mínima latencia pero carecen de mecanismos integrados de confirmación o retransmisión. *(Ejemplos: **UDP**, **IP**, **ICMP**, **IPX**).*

---

## 2. Redes Cableadas e Inalámbricas (Ethernet y Wi-Fi) [Técnica]

* **Familia Ethernet (IEEE 802.3) [Técnica]:** Estándar de red local cableada desarrollado originalmente en la década de 1970 por el consorcio **DIX** (**D**igital, **I**ntel, **X**erox) y estandarizado posteriormente por el **IEEE** (**I**nstitute of **E**lectrical and **E**lectronics **E**ngineers) en 1985 bajo la norma **IEEE 802.3**.
  * **Ámbito del Modelo OSI:** Ethernet abarca la **Capa 1 (Física)** —definiendo cables, conectores y señales eléctricas u ópticas— y el **Subnivel MAC** (**M**edia **A**ccess **C**ontrol) dentro de la **Capa 2 (Enlace de Datos)**.
  * **Direccionamiento Físico (Dirección MAC):** Identificador alfanumérico único de 48 bits (12 dígitos hexadecimales, agrupados de dos en dos como `XX:XX:XX:XX:XX:XX`) grabado en la memoria ROM/Flash de la tarjeta de red (**NIC** - **N**etwork **I**nterface **C**ard). Los primeros 6 dígitos corresponden al código **OUI** (**O**rganizational **U**nique **I**dentifier) asignado al fabricante.
  * **Codificación y Señalización:** En redes LAN modernas se utilizan señales digitales con codificaciones avanzadas como **4B5B**, **8B6T** o **PAM-5** (**P**ulse-**A**mplitude **M**odulation) permitiendo comunicación **Full-Dúplex** (transmisión y recepción simultánea) en un único canal físico.
  * **Control de Acceso al Medio CSMA/CD [Técnica]:** **CSMA/CD** (**C**arrier **S**ense **M**ultiple **A**ccess with **C**ollision **D**etection) es el algoritmo utilizado en medios compartidos en bus o hubs. El equipo *escucha* el canal (**Carrier Sense**); si está libre, transmite. Si dos equipos transmiten a la vez, se produce una *colisión*, la cual es detectada (**Collision Detection**), provocando la emisión de una señal de jam y la pausa aleatoria de ambos equipos (*backoff*) antes de reintentar. En redes modernas con switches Full-Dúplex, las colisiones quedan totalmente eliminadas.
  * **Estándares e Implementaciones de Ethernet:**
    * **Ethernet Original (10 Mbps):** `10Base5` (coaxial grueso / Thicknet, 500 m), `10Base2` (coaxial fino / Thinnet, 185 m), `10BaseT` (par trenzado UTP, 100 m), `10BaseF` (fibra óptica, 2000 m).
    * **Fast Ethernet (100 Mbps - IEEE 802.3u):** `100BaseTX` (par trenzado Categ. 5/5e de 2 pares, 100 m), `100BaseFX` (fibra óptica multimodo, 2000 m).
    * **Gigabit Ethernet (1 Gbps / 1000 Mbps - IEEE 802.3ab):** `1000BaseT` (par trenzado Categ. 5e/6 de 4 pares, 100 m), `1000BaseX` (fibra óptica SC/LC).
    * **10 Gigabit Ethernet (10 Gbps - IEEE 802.3ae / 802.3an):** `10GBaseT` (par trenzado Categ. 6a/7, 100 m), `10GBaseSR` / `10GBaseLR` (fibra óptica monomodo/multimodo).
* **Tecnología Inalámbrica Wi-Fi (IEEE 802.11) [Técnica]:** Estándar de redes inalámbricas de área local (**WLAN** - **W**ireless **L**ocal **A**rea **N**etwork) que transmite información mediante ondas electromagnéticas en radiofrecuencia.
  * **Control de Acceso al Medio CSMA/CA [Técnica]:** **CSMA/CA** (**C**arrier **S**ense **M**ultiple **A**ccess with **C**ollision **A**voidance). Dado que en el aire no es posible detectar colisiones de forma fiable mientras se transmite, los equipos *escuchan* el aire y envían una trama previa de reserva (**RTS/CTS** - **R**equest **t**o **S**end / **C**lear **t**o **S**end) solicitando confirmación antes de transmitir los datos para **prevenir y evitar** colisiones.
  * **Evolución de Estándares Wi-Fi:**
    * **802.11a (1999):** Banda 5 GHz, velocidad máxima 54 Mbps.
    * **802.11b (1999):** Banda 2.4 GHz, velocidad máxima 11 Mbps.
    * **802.11g (2003):** Banda 2.4 GHz, velocidad máxima 54 Mbps (compatible con 802.11b).
    * **802.11n / Wi-Fi 4 (2009):** Bandas 2.4 GHz y 5 GHz, hasta 600 Mbps mediante tecnología **MIMO** (**M**ultiple-**I**nput **M**ultiple-**O**utput) y *Channel Bonding* (canales de 40 MHz).
    * **802.11ac / Wi-Fi 5 (2014):** Banda exclusiva de 5 GHz, hasta 6.9 Gbps (canales de 80/160 MHz y modulación **256-QAM**).
    * **802.11ax / Wi-Fi 6 (2019):** Bandas 2.4 GHz y 5 GHz (y 6 GHz en Wi-Fi 6E), hasta 9.6 Gbps mediante **OFDMA** (**O**rthogonal **F**requency-**D**ivision **M**ultiple **A**ccess).
  * **Topologías e Infraestructura Wi-Fi:**
    * **Modo Ad-hoc (IBSS - Independent Basic Service Set):** Comunicación directa punto a punto entre dos o más clientes sin necesidad de un punto de acceso central.
    * **Modo Infraestructura:**
      * **BSS (Basic Service Set):** Celda inalámbrica formada por un único punto de acceso (**AP** - **A**ccess **P**oint) y sus clientes asociados.
      * **ESS (Extended Service Set):** Red formada por múltiples puntos de acceso interconectados por un tronco de red cableado que comparten el mismo **SSID** (**S**ervice **S**et **I**dentifier), permitiendo la transición transparente (*roaming*) de los clientes entre zonas de cobertura.

---

## 3. Protocolos de Red y Transporte (IPv4, IPv6, TCP, UDP) [Técnica]

* **Capa de Red: Protocolos IPv4 e IPv6 [Técnica]:**
  * **Características del Protocolo IP:** Funciona en la **Capa 3 (Red)** del modelo OSI. Es un protocolo **no orientado a la conexión** y **no fiable** (*best-effort delivery*); no garantiza que los paquetes lleguen, ni que lo hagan ordenados o libres de errores.
  * **Datagrama IPv4:**
    * **Estructura:** Consta de una **Cabecera** de longitud variable de **20 a 60 Bytes** (20 B fijos + opciones) y un **Área de Datos** de hasta **65535 Bytes**. La longitud variable de la cabecera obliga a los routers a procesar el campo **IHL** (**I**nternet **H**eader **L**ength), pudiendo ralentizar el enrutamiento.
    * **Direccionamiento:** Utiliza direcciones numéricas de **32 bits** (4 octetos decimales separados por puntos, ej. `192.168.1.10`), permitiendo un máximo teórico de 4294967296 direcciones (agotadas a nivel global).
  * **Datagrama IPv6:**
    * **Estructura:** Diseñado para optimizar el procesamiento en routers. Consta de una **Cabecera Fija de 40 Bytes** (con campos clave: *Versión = 6*, *Traffic Class*, *Flow Label*, *Payload Length*, *Next Header*, *Hop Limit* / TTL y direcciones origen/destino), **Cabeceras de Extensión opcionales** y el **Área de Datos**.
    * **Direccionamiento:** Utiliza direcciones de **128 bits** representadas en **8 bloques de 4 dígitos hexadecimales** separados por dos puntos (ej. `2001:0db8:85a3:0000:0000:8a2e:0370:7334`), ofreciendo un espacio de direccionamiento prácticamente infinito.
* **Capa de Transporte: Protocolos TCP y UDP [Técnica]:**
  * **Protocolo TCP (RFC 793) [Técnica]:** **TCP** (**T**ransmission **C**ontrol **P**rotocol). Operación orientada a la conexión en la **Capa 4 (Transporte)**.
    * **Mecanismos de Control:** Realiza el establecimiento de conexión mediante la negociación en 3 pasos (**Three-Way Handshake**: `SYN` → `SYN-ACK` → `ACK`). Divide la información en **segmentos** (hasta 64 KB) asignando números de secuencia, y exige la confirmación mediante asentimientos (**ACK** - **A**cknowledge). Si un segmento no se confirma dentro del tiempo límite (*timeout*), se retransmite automáticamente.
    * **Uso:** Ideal para aplicaciones que requieren fiabilidad absoluta y cero pérdida de datos (navegación web **HTTP/HTTPS**, transferencia de archivos **FTP**, correo electrónico **SMTP/IMAP**, acceso remoto **SSH**).
  * **Protocolo UDP (RFC 768) [Técnica]:** **UDP** (**U**ser **D**atagram **P**rotocol). Protocolo ligero y no orientado a la conexión en la **Capa 4 (Transporte)**.
    * **Mecanismos de Control:** Transmite **datagramas** directamente sin establecer sesión previa ni requerir asentimientos de recepción (*no ACK*). No realiza retransmisiones ni control de flujo, logrando la máxima velocidad y mínima latencia.
    * **Uso:** Diseñado para transmisión en tiempo real donde la velocidad es prioritaria sobre pequeñas pérdidas esporádicas (streaming de audio/vídeo, llamadas **VoIP**, videojuegos en línea, consultas **DNS**, llamadas **DHCP**).
* **Gestión y Clasificación de Puertos de Red [Técnica]:**
  * **Concepto de Puerto:** Número entero de **16 bits** (rango entero de **0 a 65535**) situado en la cabecera de transporte que identifica el proceso o servicio de aplicación concreto dentro de un host. La combinación de una Dirección IP y un Puerto se denomina **Socket** (ej. `192.168.1.10:80`).
  * **Categorías Oficiales de Puertos (IANA):**
    * **Puertos Bien Conocidos / Sistema (0 a 1023):** Reservados para servicios esenciales del sistema operativo e infraestructura de red. Requieren privilegios de administración (*root* / *Administrator*) para abrir sockets de escucha. *(Ejemplos: **FTP** [20/21], **SSH** [22], **TELNET** [23], **SMTP** [25], **DNS** [53], **DHCP** [67/68], **HTTP** [80], **HTTPS** [443]).*
    * **Puertos Registrados (1024 a 49151):** Asignados por la **IANA** (**I**nternet **A**ssigned **N**umbers **A**uthority) a aplicaciones y servicios de usuario específicos. *(Ejemplos: **MySQL/MariaDB** [3306], **RDP Escritorio Remoto** [3389], **PostgreSQL** [5432], **Proxy HTTP** [8080]).*
    * **Puertos Dinámicos / Privados / Efímeros (49152 a 65535):** Asignados aleatoriamente por el sistema operativo de un cliente para iniciar conexiones temporales hacia un servidor. Se liberan automáticamente al cerrar la sesión TCP/UDP.

---

## 4. Configuración del Protocolo TCP/IP en Windows y Linux [Técnica]

* **Tipos y Métodos de Direccionamiento IP [Concepto]:**
  * **Direccionamiento Estático / Manual:** La Dirección IP, Máscara de Subred, Puerta de Enlace Predeterminada (*Default Gateway*) y Servidores DNS son introducidos manualmente por el administrador. Utilizado en servidores, impresoras de red y electrónica de red.
  * **Direccionamiento Dinámico (DHCP):** Obtención automática de parámetros de red mediante el protocolo **DHCP** (**D**ynamic **H**ost **C**onfiguration **P**rotocol). El cliente solicita IP al arrancar (`DHCPDISCOVER` → `DHCPOFFER` → `DHCPREQUEST` → `DHCPACK`).
  * **Direccionamiento Alternativo / APIPA [Técnica]:** **APIPA** (**A**utomatic **P**rivate **I**P **A**ddressing). Mecanismo automático de reserva activado por el sistema operativo cuando está configurado en modo DHCP pero no recibe respuesta de ningún servidor en la red. Asigna automáticamente una dirección privada aleatoria dentro del rango **169.254.0.1 a 169.254.255.254** con máscara `255.255.0.0` (/16), permitiendo la comunicación exclusiva entre equipos del mismo segmento local sin acceso a Internet.
* **Procedimiento de Configuración en Windows (GUI y CLI) [Técnica]:**
  * **Interfaz Gráfica (GUI):** `Panel de control → Centro de redes y recursos compartidos → Cambiar configuración del adaptador → Clic derecho en Adaptador (Ethernet/Wi-Fi) → Propiedades → Protocolo de Internet versión 4 (TCP/IPv4) → Propiedades`. Permite seleccionar entre obtención automática por DHCP o asignación manual de IP, Máscara, Gateway y DNS (preferido y alternativo).
  * **Inspección en CLI (CMD / PowerShell):**
    * `ipconfig` (**IP** **Config**uration): Muestra IP, Máscara y Puerta de enlace de los adaptadores activos.
    * `ipconfig /all` (**IP** **Config**uration / **All**): Muestra el desglose completo (Dirección MAC física, estado de DHCP, servidor DHCP asignador, servidores DNS, tiempo de concesión o *lease*).
    * `ipconfig /release` y `ipconfig /renew`: Libera y solicita una nueva concesión IP al servidor DHCP.
    * `ipconfig /flushdns`: Vacía la caché del resolvedor DNS local.
* **Procedimiento de Configuración en Linux (GUI y CLI) [Técnica]:**
  * **Interfaz Gráfica (GUI en Debian/Ubuntu/GNOME):** `Configuración → Red (Network) → Selección de interfaz (Wired/Wi-Fi) → Engranaje de opciones`. En la pestaña **Detalles** muestra IP, MAC, Gateway y DNS. En las pestañas **IPv4 / IPv6** permite alternar entre *Automatic (DHCP)* y *Manual* (introduciendo IP, Netmask, Gateway y DNS).
  * **Archivos Fijos de Configuración (Debian/Ubuntu Clásico):**
    * **`/etc/network/interfaces`** o subdirectorio **`/etc/network/interfaces.d/`**: Archivo fundamental donde se definen las interfaces del sistema.
      * *Ejemplo IP Estática:*
        ```text
        auto enp0s3
        iface enp0s3 inet static
            address 192.168.1.10
            netmask 255.255.255.0
            gateway 192.168.1.1
            dns-nameservers 8.8.8.8 8.8.4.4
        ```
      * *Ejemplo IP Dinámica:*
        ```text
        auto enp0s3
        iface enp0s3 inet dhcp
        ```
    * **`/etc/resolv.conf`** (**Resolv**er **Conf**iguration): Define los servidores DNS del sistema (`nameserver 8.8.8.8`).
    * **Netplan (Ubuntu Moderno):** Ficheros YAML de configuración en `/etc/netplan/*.yaml` que se aplican mediante el comando `sudo netplan apply`.

---

## 5. Dispositivos de Interconexión de Red [Técnica]

* **Dispositivos de Capa 1 (Física):**
  * **Repetidor (Repeater):** Dispositivo de 2 puertos que amplifica, regenera y limpia la señal eléctrica u óptica atenuada por la distancia antes de retransmitirla, extendiendo el alcance del medio físico.
  * **Hub / Concentrador:** Dispositivo multipuerto que actúa como un repetidor central. Todo paquete o señal que entra por un puerto se retransmite a ciegas por **todos los demás puertos** (*broadcast* físico). Genera colisiones continuas, comparte el ancho de banda entre todos los puertos y opera únicamente en modo **Half-Dúplex**.
* **Dispositivos de Capa 2 (Enlace de Datos):**
  * **Switch / Conmutador [Técnica]:** Dispositivo inteligente multipuerto que conecta equipos dentro de la misma red local (LAN).
    * **Principios de Funcionamiento:** Examina la dirección MAC de destino presente en la cabecera de la trama entrante y realiza un **reenvío selectivo** enviando la información exclusivamente al puerto donde se encuentra el equipo destinatario.
    * **Tabla de Direcciones MAC (Tabla CAM):** El switch aprende dinámicamente qué dirección MAC está conectada a cada puerto inspeccionando la MAC de origen de las tramas recibidas y guardándolas en la tabla **CAM** (**C**ontent **A**ddressable **M**emory).
    * **Componentes de Alto Rendimiento:** Utilizan chips de hardware dedicados **ASIC** (**A**pplication-**S**pecific **I**ntegrated **C**ircuit) capaces de conmutar millones de tramas por segundo a velocidad de cable (*wire-speed*). Funcionan en modo **Full-Dúplex** dedicando el ancho de banda total a cada puerto.
    * **Funcionalidades Avanzadas de Switches Gestionables:**
      * **Auto-Sensing y Auto-MDI/MDI-X:** Auto-detección de velocidad y cruce automático de cables.
      * **VLAN (** **V**irtual **L**ocal **A**rea **N**etwork **):** Segmentación lógica de la red física en múltiples redes independientes a nivel de Capa 2.
      * **PoE (** **P**ower **o**ver **E**thernet **):** Transmisión simultánea de datos y energía eléctrica sobre el cable UTP (normas IEEE 802.3af/at/bt) para alimentar teléfonos IP, cámaras o Access Points.
      * **Seguridad de Puertos (*Port Security*):** Restricción de acceso permitiendo únicamente direcciones MAC autorizadas por puerto.
      * **QoS (** **Q**uality **o**f **S**ervice **):** Priorización de tramas de voz o vídeo sobre tráfico de datos general.
      * **LACP (** **L**ink **A**ggregation **C**ontrol **P**rotocol **):** Agregación de múltiples enlaces físicos para multiplicar el ancho de banda y aportar redundancia.
  * **Punto de Acceso Inalámbrico (AP - Access Point):** Dispositivo de Capa 2 que realiza el puente de unión (*bridge*) entre la red inalámbrica Wi-Fi y la red local cableada Ethernet.
* **Dispositivos de Capa 3 (Red):**
  * **Router / Enrutador [Técnica]:** Dispositivo encargado de interconectar redes con rangos e IP totalmente diferentes y determinar la mejor ruta para enviar cada paquete hacia su destino final.
    * **Mecanismo de Enrutamiento:** Lee la dirección IP de destino presente en el paquete, consulta su **Tabla de Enrutamiento** (*Routing Table*) y toma decisiones:
      1. Si la red de destino está directamente conectada a una de sus interfaces, entrega el paquete.
      2. Si la red no está directamente conectada, reenvía el paquete al router del siguiente salto (*Next Hop*).
      3. Si no existe ruta concreta ni ruta por defecto (*Default Route*), descarta el paquete y devuelve un mensaje de error **ICMP** (**I**nternet **C**ontrol **M**essage **P**rotocol) de *destino inalcanzable*.
    * **Arquitectura Hardware de un Router:** Posee **CPU**, puertos de entrada/salida (Ethernet, Wan, Fibra, ADSL) y memoria dividida en **RAM** (almacena la tabla de enrutamiento y paquetes en tránsito), **ROM** (bootstrap de arranque), **NVRAM** (almacena la configuración de inicio `startup-config`) y **Flash** (guarda la imagen del sistema operativo de red, ej. Cisco IOS).
    * **Tipos de Routers:**
      * **Routers SOHO / Domésticos (** **S**mall **O**ffice / **H**ome **O**ffice **):** Equipos integrados todo-en-uno que incorporan en un solo chasis: Router de Capa 3, Switch Ethernet de 4 puertos, Punto de Acceso Wi-Fi, servidor **DHCP**, resolvedor **DNS**, Módem y servicio **NAT** (**N**etwork **A**ddress **T**ranslation).
      * **Routers Enterprise / WAN:** Equipos modulares de altas prestaciones instalados en armarios RACK para interconexión de sedes o acceso a la DMZ corporativa.

---

## 6. Topologías Físicas y Lógicas de Red [Concepto]

* **Concepto de Topología [Concepto]:** La **topología física** define la disposición espacial y el esquema de interconexión del cableado y los nodos. La **topología lógica** define la forma en que los datos viajan a través del medio de transmisión.
* **Clasificación de Topologías Físicas:**
  * **Topología en Bus:** Todos los equipos se conectan en paralelo a un único cable central denominado *bus* o tronco, finalizado en sus extremos por resistencias terminadoras.
    * *Ventajas:* Mínimo consumo de cableado y bajo coste.
    * *Inconvenientes:* La rotura del cable central o fallo de un terminador inutiliza la red entera. Elevado riesgo de colisiones.
  * **Topología en Estrella:** Todos los ordenadores se conectan de forma independiente mediante un cable dedicado a un dispositivo de conmutación central (Switch o Hub). Es la topología estándar utilizada en la actualidad en redes LAN.
    * *Ventajas:* Altamente segura y modular. La avería de un equipo o su cable individual no afecta al resto de la red. Fácil instalación y detección de fallos.
    * *Inconvenientes:* Requiere mayor cantidad de cableado. Un fallo catastrófico en el conmutador central deja inoperativa toda la red.
  * **Topología en Anillo:** Los nodos se conectan formando un círculo cerrado punto a punto. La información circula en un único sentido pasando de nodo en nodo. Para evitar colisiones se utiliza el paso de un token o **testigo** (tecnología *Token Ring* - IEEE 802.5).
    * *Ventajas:* No hay colisiones.
    * *Inconvenientes:* La caída de un solo ordenador o la rotura del anillo interrumpe la comunicación global.
  * **Topología en Árbol (Estrella Jerárquica):** Combinación de varias topologías en estrella organizadas en niveles jerárquicos conectadas a un switch o router principal (*root*). Utilizada para estructurar la red por plantas o departamentos.
  * **Topología en Malla (Mesh):** Cada dispositivo está conectado directamente a múltiples o a todos los demás equipos de la red (**Malla Completa** o **Malla Parcial**).
    * *Ventajas:* Máxima tolerancia a fallos y redundancia. Si un cable o nodo cae, el tráfico se encamina por rutas alternativas de forma instantánea.
    * *Inconvenientes:* Extremadamente costosa y compleja debido a la enorme cantidad de interfaces y cableado requeridos. Se utiliza principalmente en infraestructuras críticas, backbones WAN y redes militares o bancarias.

---

## 7. Tipos de Redes por Alcance y Tecnologías WAN [Concepto]

* **Clasificación de Redes por Cobertura Geográfica [Concepto]:**
  * **PAN (** **P**ersonal **A**rea **N**etwork **):** Red de área personal con alcance de pocos metros (hasta 10 m). Conecta dispositivos personales del usuario (móviles, auriculares, relojes inteligentes) mediante tecnologías como **Bluetooth** (IEEE 802.15.1) o **NFC**.
  * **LAN (** **L**ocal **A**rea **N**etwork **):** Red de área local que interconecta equipos dentro de una extensión limitada (oficina, hogar, edificio o campus educativo) utilizando Ethernet o Wi-Fi.
  * **MAN (** **M**etropolitan **A**rea **N**etwork **):** Red de área metropolitana que abarca un municipio o ciudad entera (hasta decenas de kilómetros). Utilizada por corporaciones, redes municipales de fibra o televisión por cable (HFC).
  * **WAN (** **W**ide **A**rea **N**etwork **):** Red de área amplia que cubre regiones, países o el planeta entero interconectando múltiples redes LAN a través de proveedores de servicios **ISP** (**I**nternet **S**ervice **P**rovider). El ejemplo global por excelencia es **Internet**.
* **Tecnologías y Accesos a Redes WAN [Técnica]:**
  * **Conexiones WAN Privadas:**
    * **Conmutación de Circuitos:** Establece un canal físico y dedicado entre los extremos durante el tiempo que dura la sesión (ej. telefonía básica RTC/RDSI). Ineficiente para datos discontinuos.
    * **Conmutación de Paquetes:** Los datos se dividen en paquetes independientes que viajan por una red física compartida optimizando el uso de la infraestructura (ej. **Frame Relay**, **ATM**, **MPLS**).
    * **Líneas Dedicadas / Punto a Punto:** Enlaces permanentes y reservados exclusivamente para la empresa cliente. Ofrecen la menor latencia y máxima seguridad para tráfico crítico de voz y vídeo, pero presentan los costes más elevados.
  * **Conexiones WAN Públicas y Accesos a Internet:**
    * **DSL (** **D**igital **S**ubscriber **L**ine **):** Transmisión de datos de alta velocidad sobre el par de cobre telefónico tradicional mediante modulación de frecuencias no audibles (ADSL/VDSL).
    * **FTTH (** **F**iber **t**o **t**he **H**ome **):** Conexión directa mediante hilo de fibra óptica pura desde la central del operador hasta la roseta **ONT** (**O**ptical **N**etwork **T**erminal) del domicilio. Ofrece velocidades simétricas de varios Gigabits por segundo.
    * **HFC (** **H**ybrid **F**iber-**C**oaxial **):** Infraestructura híbrida que utiliza fibra óptica en el backbone principal del operador y cable coaxial flexible en el último tramo hasta el hogar del usuario.
    * **Inalámbricas y Móviles:** Accesos mediante ondas de radio a larga distancia: telefonía móvil celular (**4G LTE / 5G**), enlaces de microondas y redes por satélite (**Starlink**).

---

## 8. Cableado Estructurado y Medios Físicos de Transmisión [Técnica]

* **Medios de Transmisión Cobre (Cable de Par Trenzado) [Técnica]:**
  * **Principios de Diseño:** Formado por pares de hilos de cobre aislados y entrelazados helicoidalmente. El trenzado cancela las interferencias electromagnéticas externas y la diafonía (*crosstalk*) entre pares adyacentes.
  * **Tipos según Blindaje:**
    * **UTP (** **U**nshielded **T**wisted **P**air **):** Par trenzado sin apantallamiento. Es el más flexible, económico y común en instalaciones interiores. Conector estándar: **RJ45** (**R**egistered **J**ack **45**).
    * **STP (** **S**hielded **T**wisted **P**air **):** Cada par de hilos dispone de una malla/pantalla metálica individual. Máxima protección contra ruido eléctrico en entornos industriales. Conector blindado: **RJ49**.
    * **FTP / F/UTP (** **F**oiled **T**wisted **P**air **):** Una pantalla de aluminio global envuelve al conjunto de los 4 pares. Excelente equilibrio entre coste y protección.
  * **Categorías de Cableado de Cobre:**
    * *Categoría 5e:* Hasta 100 MHz, soporta 1 Gbps (1000BaseT) a 100 metros.
    * *Categoría 6:* Hasta 250 MHz, soporta 1 Gbps a 100 m y 10 Gbps a distancias cortas (hasta 55 m).
    * *Categoría 6a:* Hasta 500 MHz, soporta **10 Gbps** (10GBaseT) a la distancia completa de **100 metros**.
    * *Categoría 7 / 7a:* Hasta 600/1000 MHz, totalmente apantallado (S/FTP).
    * *Categoría 8:* Hasta 2000 MHz, soporta 25/40 Gbps a 30 metros para centros de datos.
* **Cable Coaxial y Fibra Óptica [Técnica]:**
  * **Cable Coaxial:** Formado por un núcleo central de cobre (*viga*), aislante dieléctrico, malla metálica de blindaje y cubierta exterior. Utilizado en redes de televisión por cable y conectividad de antenas. Estándar de conector clásico: **RG58** / **BNC**.
  * **Fibra Óptica:** Hilo transparente ultra-fino de sílice/vidrio o plástico que transmite pulsos de luz en lugar de señales eléctricas. Totalmente inmune a interferencias electromagnéticas y de radiofrecuencia.
    * **Fibra Monomodo (SMF - Single Mode Fiber):** Núcleo muy estrecho (8-10 micras). La luz viaja en un único haz paralelo sin reflexiones. Alcanza distancias de decenas de kilómetros a enorme ancho de banda. Utiliza láseres.
    * **Fibra Multimodo (MMF - Multi Mode Fiber):** Núcleo más ancho (50-62.5 micras). La luz penetra en múltiples haces (*modos*) rebotando en el interior. Diseñada para redes LAN y distancias cortas/medias (hasta 2 km). Utiliza diodos LED.
    * *Conectores Habituales:* **SC** (**S**ubscriber **C**onnector - conector cuadrado a presión), **ST** (**S**traight **T**ip - conector cilíndrico a bayoneta), **LC** (**L**ucent **C**onnector - conector compacto dúplex).
* **Subsistemas de Cableado Estructurado e Infraestructura Física [Técnica]:**
  * **Normas Estándar:** Reglamentado internacionalmente por las especificaciones **ANSI/TIA/EIA-568** e **ISO/IEC 11801**.
  * **Espacios y Subsistemas Principales:**
    1. **Cuarto de Entrada de Servicios (EF - Entrance Facility):** Punto de la edificación donde penetran los cables de los operadores externos de telecomunicaciones (**ISP**).
    2. **CPD / Sala de Equipos (ER - Equipment Room):** Centro de Procesamiento de Datos central donde residen los servidores corporativos, matrices de almacenamiento, **SAI** (**S**istema de **A**limentación **I**ninterrumpida) y routers principales. Se exige climatización controlada y protección contra incendios.
    3. **Armarios de Comunicaciones / RACK [Técnica]:** Estructuras metálicas estandarizadas de 19 pulgadas de ancho destinadas a alojar switches, patch panels y electrónica. La altura interna útil de los armarios se mide en **Unidades U** (donde **1 U = 1,75 pulgadas = 44,45 mm**).
    4. **Paneles de Parcheo (*Patch Panels*):** Bloques de conectores RJ45/fibra hembra montados en el RACK donde terminan de forma fija todos los cables procedentes de las rosetas de la planta. Permiten realizar interconexiones y cambios de puerto mediante latiguillos cortos (*patch cords*) sin someter al cableado permanente a estrés mecánico.
    5. **Cableado Vertical / Troncal (*Backbone*):** Interconecta los armarios de comunicaciones de las distintas plantas entre sí y con el CPD. Se realiza preferentemente con fibra óptica.
    6. **Cableado Horizontal:** Discurre desde el armario de comunicaciones de la planta hasta las rosetas o **TO** (**T**elecommunications **O**utlet) en los puestos de trabajo. La longitud máxima del tramo horizontal rígido no debe superar los **90 metros** (sumando un máximo de 10 m en latiguillos flexibles para el total de 100 m de canal).
  * **Canalizaciones:** Vías físicas para el tendido protegido de cables.
    * *Por Pared:* Mediante canaletas plásticas o metálicas de superficie fijadas con tornillos.
    * *Por Techo:* Sobre falso techo utilizando bandejas de rejilla metálica, escalera o canaleta cerrada galvanizada.
    * *Por Suelo:* Mediante falso suelo técnico canalizado o canaletas pasacables reforzadas (*salvacables*).

---

## 9. Monitorización, Verificación y Diagnóstico CLI [Técnica]

* **Herramientas y Comandos CLI en Linux (Suite iproute2 y net-tools) [Técnica]:**
  * **`ip` (Comando Universal `iproute2`):**
    * `ip a` / `ip addr show` (**IP** **A**ddress **Show**): Lista todas las interfaces de red del sistema, sus estados, direcciones IPv4/IPv6 y direcciones MAC.
    * `ip link set <interfaz> down` / `up`: Deshabilita o habilita administrativamente una tarjeta de red (ej. `ip link set enp0s3 down`).
    * `ip addr add <IP/Máscara> dev <interfaz>`: Asigna temporalmente una dirección IP (ej. `ip addr add 192.168.1.10/24 dev enp0s3`).
    * `ip addr del <IP/Máscara> dev <interfaz>`: Elimina una dirección IP de la interfaz.
    * `ip route show`: Muestra la tabla de enrutamiento del kernel de Linux, identificando la puerta de enlace por defecto (*default via*).
    * `ip neighbour show`: Muestra la tabla **ARP** (**A**ddress **R**esolution **P**rotocol) con la correspondencia entre direcciones IP locales y direcciones MAC físicas asociadas.
  * **`ss` (** **S** ocket **S** tatistics) / **`netstat` [Técnica]:**
    * `ss -ltup` o `netstat -ltup` (**l**istening, **t**cp, **u**dp, **p**rograms): Muestra todos los puertos TCP y UDP en estado de escucha (*LISTEN*), identificando el **PID** y el nombre del proceso ejecutor de cada puerto.
  * **`ifconfig` (** **I** nterface **C** on **fig** uration - *Paquete net-tools*): Comando tradicional para visualizar y configurar parámetros IP (`ifconfig enp0s3 192.168.1.10 netmask 255.255.255.0`).
* **Herramientas y Comandos CLI en Windows (CMD / PowerShell) [Técnica]:**
  * **`ipconfig /all`:** Inspección completa del direccionamiento, MAC, estado de DHCP y servidores DNS.
  * **`ping <IP_Destino>`:** Envía paquetes de eco **ICMP** (**I**nternet **C**ontrol **M**essage **P**rotocol) para verificar la conectividad de Capa 3, la latencia en milisegundos (ms) y el tiempo de vida (**TTL** - **T**ime **t**o **L**ive).
  * **`tracert <IP_o_Dominio>` (** **Trac** e **R** ou **t** e): Identifica uno a uno todos los routers intermedios (saltos) que atraviesa un paquete hasta alcanzar su destino.
  * **`netstat -ab`:** (**Net**work **Stat**istics - **a**ll sockets, **b**inary executable): Muestra todas las conexiones activas y puertos en escucha asociando directamente el nombre del archivo ejecutable `.exe` responsable de cada conexión (requiere ejecutar CMD como Administrador).
  * **`nslookup <Dominio>` (** **N** ame **S** erver **Lookup**): Consulta directamente los servidores DNS para resolver nombres de dominio a direcciones IP y viceversa.

---

## 10. Resolución de Problemas y Seguridad en Comunicaciones [Técnica]

* **Metodología y Enfoques de Mantenimiento de Red [Técnica]:**
  * **Mantenimiento Predictivo:** Utilización de software de monitorización avanzada y sensores (*SNMP*, depuración de logs) para analizar tendencias de uso, variaciones de latencia y tasas de error, anticipándose a las fallas antes de que se produzca la interrupción del servicio.
  * **Mantenimiento Preventivo:** Planificación programada de tareas físicas y lógicas periódicas orientadas a prevenir averías: limpieza de polvo en armarios RACK y ventiladores, verificación de latiguillos, revisión de temperaturas en el CPD y aplicación de parches de firmware en switches y routers.
  * **Mantenimiento Correctivo:** Protocolo de actuación ejecutado tras la aparición de una incidencia o caída del sistema. Comprende el diagnóstico de la causa raíz mediante herramientas analíticas (como **Cisco Packet Tracer** o analizadores de protocolos **Wireshark**) y la sustitución o reconfiguración del componente averiado.
* **Principios Fundamentales de Seguridad en Comunicaciones (Modelo CIAA) [Concepto]:**
  * **Confidencialidad:** Garantía de que la información transmitida solo sea accesible y legible por los usuarios y procesos autorizados, impidiendo la interceptación (*eavesdropping*). Se implementa mediante protocolos de cifrado fuerte (**HTTPS / TLS**, **SSH**, **WPA3**, **VPN IPsec**).
  * **Integridad:** Garantía de que los datos no han sido alterados, truncados o manipulados voluntaria o involuntariamente durante su transporte por la red. Se asegura mediante funciones hash y firmas digitales (**SHA-256**, firmas **MAC** / **HMAC**).
  * **Disponibilidad:** Garantía de que los servicios de red, servidores y recursos permanezcan accesibles sin interrupciones para los usuarios legítimos siempre que los necesiten. Se protege mediante redundancia de enlaces, balanceo de carga, sistemas **SAI** y defensas contra ataques de denegación de servicio (**DDoS**).
  * **Autenticidad:** Verificación inequívoca de la identidad del emisor y del receptor en una comunicación, asegurando que ninguna de las partes pueda suplantar la identidad de otra (*spoofing*) ni no-reproducir la autoría de sus acciones (*No Repudio*).

---
