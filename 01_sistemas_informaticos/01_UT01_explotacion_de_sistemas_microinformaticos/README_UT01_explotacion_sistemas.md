# UT01 — Explotación de Sistemas Microinformáticos

## 1. Introducción a los Sistemas Informáticos y el Sistema Operativo

* **Sistema Informático [Concepto]:** Conjunto de elementos físicos, lógicos y humanos que trabajan coordinadamente para recibir datos, procesarlos, almacenarlos y entregar información útil.
* **El Tríptico Fundamental [Concepto]:**
  * **Hardware:** La parte física, tangible y material del sistema (procesador, memoria RAM, discos, placas, cables, periféricos).
  * **Software:** La parte lógica e intangible formada por los programas, instrucciones y datos.
  * **Usuarios:** Las personas que interactúan con el sistema (desde usuarios finales hasta programadores y administradores). Ningún vértice del tríptico funciona de forma independiente.
* **Sistema Operativo (SO) [Concepto]:** Es la pieza de software más importante del sistema informático. Actúa como el **director de orquesta** o puente intermediario entre el hardware y las aplicaciones/usuarios, traduciendo órdenes a lenguaje máquina y gestionando los recursos.
* **Funciones Clave del Sistema Operativo [Técnica]:**
  1. **Gestión de Procesos:** Controla el inicio, pausa, reanudación y finalización de los programas, asignando tiempos de CPU y evitando conflictos.
  2. **Gestión de Memoria Principal (RAM):** Organiza el espacio en memoria para cada aplicación, garantizando que dispongan de la cantidad necesaria sin interferir entre sí.
  3. **Gestión de Archivos y Almacenamiento:** Organiza la estructura en disco, permitiendo crear, leer, modificar y eliminar archivos.
  4. **Gestión de Dispositivos (E/S):** Controla los componentes físicos de entrada y salida a través de controladores o drivers.
  5. **Gestión de Seguridad y Usuarios:** Autentica identidades, gestiona permisos de acceso y protege el sistema ante accesos no autorizados.

---

## 2. Arquitecturas de Computadores

* **Modelo Von Neumann [Concepto]:**
  * Diseñado en los años 40. Se caracteriza por utilizar **una única memoria compartida** para almacenar tanto las instrucciones de los programas como los datos a procesar.
  * Los componentes (CPU, memoria y periféricos) se comunican a través de un sistema de buses: **bus de datos, bus de direcciones y bus de control**.
  * **Cuello de Botella de Von Neumann [Técnica]:** Al compartir el mismo bus para transferir datos e instrucciones, la CPU debe realizar accesos secuenciales obligatorios, lo que limita el rendimiento máximo del sistema.
* **Modelo Harvard [Concepto]:**
  * Separa físicamente la memoria de datos y la memoria de instrucciones, disponiendo de **buses independientes** para cada una.
  * Permite a la CPU acceder simultáneamente a las instrucciones y a los datos, reduciendo el cuello de botella y aumentando significativamente la velocidad de procesamiento.

---

## 3. Componentes Hardware del Sistema Informático

### A. El Microprocesador (CPU)
* **CPU [Concepto]:** Circuito integrado que actúa como el corazón o cerebro del sistema informático.
* **Estructura Interna de la CPU [Técnica]:**
  * **Unidad de Control (UC):** Interpreta y ejecuta las instrucciones, coordinando el flujo de trabajo de todo el sistema.
  * **Unidad Aritmético-Lógica (UAL):** Realiza las operaciones matemáticas (sumas, restas) y lógicas (comparaciones booleanas).
  * **Registros:** Memorias temporales ultrarrápidas ubicadas dentro del propio chip de la CPU. Su tamaño de palabra (32 bits o 64 bits) determina la arquitectura del sistema.
  * **Núcleos e Hilos (Threads):** Los núcleos son unidades físicas de procesamiento en paralelo. Los hilos son los flujos de tareas que se ejecutan simultáneamente.
  * **Controladores Integrados:** Incluye el controlador de memoria RAM integrado y, en muchos modelos, el controlador gráfico (GPU integrada).
* **Parámetros de Rendimiento de la CPU [Técnica]:**
  1. **Frecuencia / Velocidad de Reloj (GHz):** Número de ciclos de instrucción por segundo.
  2. **Número de Hilos (Threads):** Capacidad de procesamiento paralelo de tareas.
  3. **Nivel de Integración (nm):** Grado de miniaturización de los transistores en la litografía del chip.
  4. **Consumo Eléctrico (W):** Cantidad de energía consumida.
  5. **TDP (Thermal Design Power) [Técnica]:** Potencia de diseño térmico expresada en vatios (W), que indica la cantidad máxima de calor que genera el chip y que el sistema de refrigeración debe disipar.

### B. Jerarquía de Memoria
1. **Registros [Concepto]:** Integrados en la propia CPU. Son las memorias de menor capacidad pero de mayor velocidad de todo el sistema.
2. **Memoria Caché (L1, L2, L3) [Técnica]:** Memoria rápida situada entre los registros y la RAM. La nivel 1 (L1) es la más rápida y cercana a los núcleos; L2 y L3 son progresivamente mayores en capacidad pero ligeramente más lentas.
3. **Memoria RAM (Random Access Memory) [Concepto]:** Memoria principal de trabajo. Es **volátil** (pierde toda la información al cortar el suministro eléctrico).
   * **Parámetros de Evaluación:** Capacidad (GB), Frecuencia de trabajo (GHz) y Latencia (**CL**, medida en ciclos de reloj; a menor latencia, mejor rendimiento).
   * **Módulos Físicos:** **DIMM** (para equipos de sobremesa) y **SO-DIMM** (para ordenadores portátiles).
   * **Tecnología:** **DDR4** (tecnología estándar tratada en la unidad, con mayor rendimiento y eficiencia energética que DDR3).

### C. Placa Base (Motherboard) y Chipset
* **Placa Base [Concepto]:** Circuito impreso principal donde se conectan e interconectan todos los componentes del sistema.
* **Factores de Forma Estandarizados [Técnica]:** **ATX**, **Micro-ATX** y **Mini-ITX**. Definen las dimensiones físicas, la distribución de tornillos y la compatibilidad con las cajas/chasis.
* **Componentes Principales de la Placa Base [Técnica]:**
  * **Chipset:** Circuito integrado que actúa como el administrador de tráfico interno de la placa base, regulando las comunicaciones entre la CPU, la RAM, las ranuras de expansión, el almacenamiento y los puertos. Determina la compatibilidad con los procesadores.
  * **Zócalo del Microprocesador (Socket):** Conector donde se inserta la CPU. Tipos principales: **ZIF/PGA** (pines en el procesador) y **LGA** (pines situados en el propio zócalo de la placa).
  * **Ranuras de Expansión (PCIe):** Zócalos para conectar tarjetas adicionales (gráficas, de red, de sonido) en formatos x1, x4 y x16 según el ancho de banda.
  * **BIOS / UEFI [Técnica]:** Firmware grabado en un chip de memoria ROM de la placa que gestiona el arranque inicial y permite configurar parámetros básicos del hardware.
  * **Conectores Internos y Externos:** Internos (SATA, M.2, conectores de fuente de alimentación) y externos (USB, HDMI, DisplayPort, Ethernet RJ-45, conectores de audio, PS/2).

### D. Dispositivos de Almacenamiento No Volátil
Son memorias a largo plazo que conservan la información aunque el equipo se apague.
1. **Almacenamiento Flash (NAND) [Técnica]:**
   * **SSD (Unidades de Estado Sólido):** Extremadamente rápidas y sin partes móviles; la tecnología dominante en la actualidad.
   * **Tarjetas de memoria y memorias USB:** Unidades portátiles no volátiles.
2. **Almacenamiento Magnético [Técnica]:**
   * **HDD (Discos Duros Mecánicos):** Utilizan platos metálicos que giran a alta velocidad y cabezales magnéticos de lectura/escritura.
   * **Cintas Magnéticas:** Utilizadas en entornos corporativos para copias de seguridad masivas y almacenamiento a largo plazo.
3. **Almacenamiento Óptico [Técnica]:** Basado en lectura/escritura mediante láser. CD (700 MB), DVD (4,7 a 17 GB) y Blu-ray (25 a 128 GB).

### E. Fuente de Alimentación (PSU) y Baterías
* **Fuente de Alimentación (PSU) [Concepto]:** Componente que transforma la Corriente Alterna (CA) de la red eléctrica en Corriente Continua (CC) estable.
* **Tres Misiones Principales [Técnica]:**
  1. Distribuir energía en tres raíles de voltaje principales: **3,3 V** (lógica de baja potencia de chips), **5 V** (periféricos y puertos USB) y **12 V** (motores, ventiladores y tarjeta gráfica/GPU).
  2. Servir de escudo protector contra variaciones de la red eléctrica.
  3. Colaborar en la extracción del aire caliente interno del chasis.
* **Baterías [Concepto]:** Fuente de alimentación acumulativa utilizada en dispositivos portátiles.

### F. Periféricos y Adaptadores
* **Dispositivos de Entrada:** Transmiten datos hacia el equipo (teclado, ratón).
* **Dispositivos de Salida:** Muestran resultados al usuario (pantalla, altavoces).
* **Dispositivos de Entrada/Salida:** Comunicación bidireccional (discos duros externos, adaptadores Wi-Fi).
* **Adaptadores [Técnica]:** Dispositivos que permiten interconectar interfaces físicas distintas (ejemplo: adaptadores de VGA a HDMI).

---

## 4. Clasificación del Software

1. **Software de Sistema [Concepto]:** Programas que interactúan directamente con el hardware, actuando como intermediarios con el usuario. Incluye el Sistema Operativo y los firmwares (BIOS/UEFI).
2. **Software de Aplicación [Concepto]:** Programas diseñados para realizar tareas específicas de usuario final (suites ofimáticas, navegadores web, reproductores, juegos).
3. **Software de Desarrollo [Concepto]:** Herramientas utilizadas por los programadores para crear nuevo software (editores de código, compiladores, depuradores e IDEs).

---

## 5. Controladores de Dispositivos (Drivers)

* **Driver [Concepto]:** Pequeño programa informático que actúa como **intérprete o traductor bidireccional** entre el Sistema Operativo y un componente hardware específico (tarjeta gráfica, red, impresora).
* **Necesidad de los Drivers [Técnica]:** El SO no conoce las instrucciones específicas de cada modelo de hardware; el driver traduce las órdenes genéricas del SO en comandos que el dispositivo comprende.
* **Drivers Genéricos vs. Oficiales [Técnica]:**
  * Los SO incluyen drivers genéricos para permitir un funcionamiento básico.
  * Se recomienda instalar siempre los **drivers oficiales del fabricante** (descargados de su web) para habilitar todas las funciones avanzadas (ej. aceleración 3D en tarjetas gráficas NVIDIA/AMD, gestión multimonitor, estabilidad y parches de seguridad).
* **Administración de Drivers por Sistema Operativo [Técnica]:**
  * **Microsoft Windows:** Se gestionan desde el **Administrador de dispositivos** (accesible con clic derecho en Inicio). Muestra las categorías de hardware (GPU integrada vs. dedicada, adaptadores de red, almacenamiento, etc.).
  * **Ubuntu Desktop (Linux):** La mayoría de controladores están integrados en el propio *kernel* como módulos (cargados automáticamente mediante `udev`/`modprobe`). Se pueden consultar en consola con `lshw` y gestionar gráficamente desde la aplicación *Software y Actualizaciones*.
* **Propiedades del Dispositivo [Técnica]:** Al acceder a un componente en el Administrador de dispositivos:
  * **Pestaña General:** Muestra el fabricante y el estado de funcionamiento.
  * **Pestaña Controlador:** Muestra el proveedor del driver, la fecha de emisión y la versión exacta instalada.
* **Opciones de Actualización [Técnica]:** Permite la búsqueda automática a través del sistema o la localización manual de archivos de controladores en el equipo.
* **Dispositivo Desconocido e Iconos de Advertencia [Técnica]:** El sistema muestra un icono de advertencia (exclamación amarilla) o la etiqueta "dispositivo desconocido" cuando falta el controlador o el componente tiene un fallo de comunicación.
* **Criterio de Seguridad de Instalación [Técnica]:** Se debe priorizar la descarga manual directa desde la web oficial del fabricante frente al uso de herramientas automatizadas de terceros (ej. Driver Booster) o sitios no verificados.

---

## 6. Proceso de Arranque y POST (Power-On Self-Test)

* **Secuencia de Arranque (Boot Sequence) [Técnica]:**
  1. **Energización:** Pulsar el botón de encendido hace que la PSU entregue corriente estable (3,3V, 5V, 12V) a la placa base.
  2. **Toma de Control:** El procesador empieza a ejecutar las instrucciones del firmware alojado en la **BIOS/UEFI**.
  3. **Fase POST (Power-On Self-Test) [Técnica]:** Test de autocomprobación inicial donde la BIOS/UEFI verifica que la CPU, la memoria RAM, la tarjeta gráfica y los discos estén presentes y funcionen.
     * **Diagnóstico de Averías:** Si un componente falla antes de inicializar la pantalla, la placa emite **códigos de pitidos (beeps)** mediante el zumbador interno o muestra códigos LED.
  4. **Carga del Sistema Operativo:** Tras superar el POST, la BIOS/UEFI busca el dispositivo de arranque según la prioridad configurada (NVMe, SATA, USB) y transfiere el control al cargador de arranque (*bootloader*).
* **Caso Práctico de Diagnóstico del Temario:** Un equipo no da imagen y emite **3 pitidos cortos continuos**. El manual de la placa indica error de memoria RAM. Tras apagar, desconectar y realizar un *reseat* (extracción, limpieza y reasentamiento de los módulos DDR4), el POST finaliza con éxito y el equipo arranca.

---

## 7. Virtualización y Máquinas Virtuales

* **Máquina Virtual (VM) [Concepto]:** Entorno informático simulado por software que funciona de forma completamente aislada dentro de un ordenador físico real.
* **Componentes y Arquitectura de Virtualización [Técnica]:**
  * **Anfitrión (Host) [Concepto]:** El ordenador físico real que aporta los recursos de hardware (CPU, RAM, disco).
  * **Invitado (Guest) [Concepto]:** El sistema operativo que se ejecuta dentro de la máquina virtual.
  * **Hipervisor / VMM (Virtual Machine Monitor) [Técnica]:** Software encargado de gestionar y reservar recursos del Host para las VMs.
    * **Tipo 1 (Bare Metal):** Se ejecuta directamente sobre el hardware físico del servidor (ej. XenServer, Hyper-V Server, KVM).
    * **Tipo 2 (Hosted):** Se ejecuta como una aplicación sobre el sistema operativo anfitrión (ej. VirtualBox, VMware Workstation Pro/Player).
* **Herramientas Clave en Virtualización [Técnica]:**
  * **Instantáneas (Snapshots) [Técnica]:** Captura del estado exacto de una VM (configuración, memoria y disco) en un momento dado. Permite regresar a dicho estado en caso de fallos o tras realizar pruebas peligrosas.
  * **Guest Additions / VMware Tools [Técnica]:** Paquete de controladores especiales que se instalan dentro del sistema invitado (Guest) para permitir pantalla completa, integración fluida del ratón y carpetas compartidas con el Host.
  * **Regla de Asignación de Recursos:** Nunca se debe asignar al sistema invitado más del 50 % de la memoria RAM física real del equipo anfitrión para evitar bloquear el sistema operativo host.
* **Pasos Estándar para Crear una VM (Ejemplo VirtualBox) [Técnica]:**
  1. Asignar un nombre descriptivo (ej. `Windows 10` o `Ubuntu Server`).
  2. Seleccionar el tipo y versión de sistema operativo.
  3. Reservar hardware inicial (ej. 4 GiB de RAM y 50 GB de disco duro virtual).
  4. Montar la imagen ISO oficial descargada en la unidad óptica virtual.
  5. Completar la instalación del SO, instalar las *Guest Additions* y tomar una instantánea (*Snapshot*) en estado limpio.

---

## 8. Prevención de Riesgos Laborales (PRL) y Ergonomía

* **Marco Legal [Concepto]:** Regulado en España por la **Ley 31/1995 de Prevención de Riesgos Laborales**, que garantiza el derecho de los trabajadores a la protección de su salud y seguridad en el trabajo.
* **Medidas de Seguridad Física y Eléctrica [Técnica]:**
  * Apagar y desconectar siempre el equipo de la red eléctrica antes de abrir la torre o manipular componentes internos.
  * Descargar la electricidad estática tocando una superficie metálica sin pintar o utilizando una **pulsera antiestática** conectada a toma de tierra.
  * Mantener libres las rejillas de ventilación de los equipos para evitar el sobrecalentamiento y el ahogamiento térmico (*thermal throttling*).
  * No mover ni transportar nunca equipos mientras estén encendidos.
* **Ergonomía en el Puesto de Trabajo [Técnica]:**
  * **Pantalla:** Colocada a la altura de los ojos, a una distancia de 50 a 70 cm y orientada de forma que evite reflejos de luz.
  * **Postura:** Espalda bien apoyada en el respaldo lumbar, brazos relajados formando un ángulo de 90° con el teclado y pies apoyados en el suelo.
  * **Iluminación:** Se recomienda trabajar con luz natural indirecta, complementada con luz artificial uniforme.
  * **Descansos Periodicos:** Realizar pausas breves cada hora para estirar las extremidades y descansar la vista de la pantalla.
