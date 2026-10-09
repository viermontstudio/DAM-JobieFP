### 💻 UT02 — Instalación de Sistemas Operativos y Máquinas Virtuales

###### 1. Concepto y Funciones del Sistema Operativo
* **Sistema Operativo (SO) [Concepto]:** Componente fundamental de software que actúa como intermediario ("director de orquesta") entre el hardware del equipo, las aplicaciones y el usuario [7, 8]. Administra los recursos del sistema y coordina el funcionamiento de todos sus componentes físicos [7].
* **El Tríptico Fundamental y Características Clave [Concepto]:**
    * **Adaptabilidad:** Capacidad de ajustarse a la evolución continua del hardware y del software.
    * **Facilidad de uso:** Busca un equilibrio entre la comodidad para el usuario y la eficiencia en el consumo de recursos.
    * **Eficiencia:** Optimiza el acceso a recursos limitados priorizando su uso de forma efectiva.
* **Gestores Principales del Sistema Operativo [Técnica]:**
    1. **Gestión de Procesos:** Controla la ejecución de las aplicaciones organizándolas en procesos e hilos [10, 11]. Asigna tiempos de microprocesador y prioridades según políticas orientadas al usuario (E/S, respuesta rápida a periféricos) o al sistema (rendimiento bruto para cálculo intensivo) [11].
    2. **Gestión de Memoria RAM y Virtual:** Asigna y libera espacio de memoria dinámica [11, 12]. Cuando la memoria RAM física es insuficiente, utiliza memoria virtual en disco mediante paginación y segmentación (*swapping*) [12].
    3. **Gestión de Entradas/Salidas (E/S):** Regula la comunicación con periféricos y tarjetas de red mediante controladores (*drivers*) [13], búferes (*spooling*) y colas para evitar bloquear la interacción del usuario.
    4. **Gestión de Almacenamiento Secundario:** Organiza la información en unidades lógicas (particiones, carpetas y archivos) utilizando sistemas de archivos (NTFS, ext4, APFS) manteniendo metadatos y permisos [14].
    5. **Gestión de Seguridad:** Controla los permisos de acceso, autentica usuarios y garantiza la disponibilidad, confidencialidad e integridad del sistema [14].
    6. **Gestión de Errores:** Detecta, aísla, registra en *logs* y notifica fallos de hardware o software [15], empleando sistemas de archivos con *journaling* para recuperar la coherencia tras un apagado imprevisto.
    7. **Gestión de la Interfaz de Usuario:** Proporciona el entorno de interacción, que puede ser textual (Línea de Comandos / CLI) o gráfico (Interfaz Gráfica de Usuario / GUI) [15].

---

###### 2. Clasificación de los Sistemas Operativos
* **Según la Cantidad de Procesos Simultáneos:**
    * **Monotarea / Monoprogramado [Concepto]:** Solo permite ejecutar un proceso a la vez (ej. MS-DOS) [17].
    * **Multitarea / Multiprogramado [Concepto]:** Mantiene y ejecuta múltiples procesos e hilos simultáneamente en memoria [17, 18].
* **Según el Número de Usuarios Simultáneos:**
    * **Monousuario [Concepto]:** Diseñado para que un único usuario aproveche la totalidad de los recursos del equipo [18].
    * **Multiusuario [Concepto]:** Permite sesiones concurrentes compartiendo y gestionando los recursos entre varios usuarios mediante control de permisos (ej. Windows Server, Debian) [18, 19].
* **Según el Tipo de Procesamiento:**
    * **Tiempo Real [Concepto]:** Cumple plazos de respuesta estrictos y comportamiento predecible (ej. centrales nucleares, aviación, sistemas de alarmas) [22].
    * **Interactivo / Tiempo Compartido [Concepto]:** Requiere la participación constante del usuario (ej. procesadores de texto, juegos, SO de escritorio).
    * **Por Lotes (Batch) [Concepto]:** Agrupa tareas similares sin intervención del usuario y las ejecuta en serie; si una falla, se detiene todo el lote [20].
* **Según el Tipo de Interfaz:**
    * **Textual (CLI) [Concepto]:** Funciona mediante comandos escritos en terminal [20]. Es más potente y consume menos recursos.
    * **Gráfica (GUI) [Concepto]:** Presenta ventanas, menús e iconos [20, 21]. Es intuitiva, pero requiere mayor consumo de recursos hardware.
* **Según la Forma de Ofrecer Servicios:**
    * **Cliente / Escritorio [Concepto]:** Diseñado para ordenadores personales en entornos domésticos o de oficina.
    * **En Red / Servidor [Concepto]:** Administra usuarios, comunicaciones y recursos centralizados en una red corporativa [22].
    * **Distribuidos [Concepto]:** Hace que múltiples equipos independientes trabajen juntos como si fueran un único sistema [22, 23].
    * **Embebidos / Integrados [Concepto]:** Integrados en dispositivos físicos específicos (routers, electrodomésticos, vehículos) [23].

---

###### 3. Arquitectura del Sistema Operativo y Hardware de Apoyo
* **Modelos Arquitectura de Kernel [Concepto]:**
    * **Monolítico [Técnica]:** Todos los servicios del sistema (procesos, memoria, archivos, drivers) ejecutan en el mismo espacio de memoria del kernel [28]. Ofrece máxima velocidad, pero un fallo en cualquier módulo puede colapsar todo el sistema [28].
    * **Microkernel [Técnica]:** Reduce el núcleo a las funciones mínimas indispensables, trasladando servicios no críticos a procesos independientes en espacio de usuario [29]. Aumenta la estabilidad y aislamiento ante fallos [29].
    * **Kernel Híbrido [Técnica]:** Combina la estructura modular del microkernel con componentes monolíticos para optimizar rendimiento sin perder estabilidad.
* **Arquitectura de Memoria Caché de la CPU [Técnica]:**
    * **Niveles L1, L2 y L3:** La memoria caché está integrada físicamente dentro del chip del procesador (es volátil y ultrarrápida) [94, 97-99]. Se divide en L1 (ultrarrápida y pequeña), L2 (capacidad intermedia) y L3 (mayor capacidad, ligeramente más lenta) [98, 99].
    * **Algoritmos de Predicción:** El procesador utiliza algoritmos internos de predicción por hardware para determinar qué datos cargar preventivamente en la caché; no es gestionado ni programado por el usuario [100-102].
* **Placa Base y Bus de Comunicación [Técnica]:**
    * **NorthBridge vs. SouthBridge:** El *NorthBridge* interconecta la CPU con los componentes de alta velocidad (memoria RAM y bus gráfico/PCIe) [109, 110]. El *SouthBridge* gestiona los periféricos e interfaces más lentos (SATA, USB, audio, BIOS) [109, 110].
    * **Módulos RAM SIMM vs. DIMM:** Los módulos *SIMM* disponen de contactos en una sola cara (transmisión por un único canal) [111, 112]. Los módulos *DIMM* poseen contactos independientes en ambas caras, permitiendo transferencias de doble canal (Dual-Channel) y mayor ancho de banda [111, 112].
* **Ensamblaje Físico y Gestión Térmica [Técnica]:**
    * **Sensibilidad del Socket:** Los pines del zócalo (*socket*) y de la CPU son extremadamente frágiles [81, 84]. Forzar la colocación o alinear mal el procesador dobla los pines, provocando un daño irreversible [83, 84].
    * **Pasta Térmica:** Compuesto que rellena las imperfecciones microscópicas entre las superficies metálicas de la CPU y el disipador para maximizar la transferencia de calor hacia el sistema de refrigeración (por aire, líquida o por inmersión) [94-97, 136-139].

---

###### 4. Versiones de Sistemas Operativos Actuales
* **Sistemas Operativos de Microsoft:**
    * **Escritorio (Windows 10/11):** Ediciones *Home* (uso básico), *Pro* (pymes/entornos de trabajo), *Enterprise* (gestión corporativa avanzada), *Education* (centros académicos), *Pro for Workstations* (cargas pesadas) e *IoT* (dispositivos conectados).
    * **Servidores (Windows Server 2019/2022):** Ediciones *Essentials* (pequeños negocios), *Standard* (baja virtualización) y *Datacenter* (entornos en la nube y alta virtualización).
* **Sistemas Operativos GNU/Linux y BSD:**
    * **Distribuciones de Escritorio:** *Ubuntu* y *Linux Mint* (principiantes/uso general), *Arch Linux* y *Manjaro* (avanzados/configuración a medida), *Kali Linux* y *Tails* (seguridad, pentesting y privacidad) y *Chromium OS*.
    * **Distribuciones de Servidor:** *Red Hat Enterprise Linux (RHEL)* (soporte empresarial), *Debian* (base estable de libre distribución) [30], *Ubuntu Server*, *SUSE Linux Enterprise (SLES)*, *CentOS* y *FreeBSD*.
* **Sistemas Operativos de Apple:**
    * **macOS:** Diseñado exclusivamente para ordenadores Mac con alta optimización e integración hardware [31, 32].
    * **Sistemas Específicos:** *iOS* (iPhone), *iPadOS* (tablets) y *watchOS* (smartwatches).

---

###### 5. Planificación de la Instalación y Copias de Seguridad
* **Criterios de Selección del Sistema Operativo [Técnica]:** Análisis de TCO (*Total Cost of Ownership* / Coste Total de Propiedad), estabilidad, compatibilidad con software/hardware y licencias [33, 34].
* **Requisitos Mínimos de Hardware [Técnica]:**
    * **Windows 10 (64 bits):** CPU 1 GHz, 2 GB RAM (4 GB recomendado), 20 GB de disco duro, pantalla 800x600 y tarjeta gráfica DirectX 9.
    * **Debian GNU/Linux:**
        * *Sin Interfaz Gráfica (CLI):* CPU Pentium 4 1 GHz, 128 MB RAM (512 MB recomendado), 2 GB de disco duro.
        * *Con Interfaz Gráfica (GUI):* CPU Pentium 4 1 GHz, 256 MB RAM (1 GB recomendado), 10 GB de disco duro.
* **Copias de Seguridad Previas [Técnica]:** Medida imprescindible previa a la instalación para evitar la pérdida de información durante el formateo [37].
    * **Herramientas Recomendadas:** CloneApp (para entornos Windows) y Aptik (para entornos Debian).

---

###### 6. Proceso de Instalación de Sistemas Operativos
* **Secuencia General de Instalación [Técnica]:** Preparación del medio de instalación (USB/ISO grabado con herramientas como *Rufus*), configuración del orden de arranque en BIOS/UEFI [39], particionado y formateo del disco [40], copia del núcleo y archivos base [40], e instalación de controladores esenciales [41].
* **Secuencia Paso a Paso en Windows 10 [Técnica]:**
    1. Selección de idioma, formato de hora, moneda y mapa de teclado -> Pulsar *Siguiente* e *Instalar ahora*.
    2. Introducción de la clave de producto o selección de *No tengo clave de producto*.
    3. Selección de la versión del sistema y aceptación de términos de licencia.
    4. Elección del tipo de instalación *Personalizada* (permite particionado manual).
    5. Selección/creación de la partición de destino (el asistente crea automáticamente particiones adicionales de sistema/recuperación).
    6. Copia de archivos y reinicio del sistema.
    7. Configuración de región, cuenta de usuario (Microsoft o local), PIN de seguridad y opciones de privacidad.
* **Secuencia Paso a Paso en Debian GNU/Linux [Técnica]:**
    1. Selección del idioma de instalación, ubicación geográfica y mapa de teclado.
    2. Asignación del nombre de la máquina (*hostname*) y nombre de dominio en red.
    3. Configuración de la clave de superusuario (root) y creación de la cuenta de usuario estándar.
    4. Particionado de discos (opción guiada *Todos los ficheros en la misma partición* para estructura simple).
    5. Configuración del gestor de paquetes conectando a la réplica de repositorios (deb.debian.org).
    6. Selección de colecciones de programas y entorno de escritorio (GNOME, Xfce, KDE Plasma) [41].
    7. Instalación del cargador de arranque GRUB en el registro principal del disco.

---

###### 7. Instalaciones Desatendidas y Automatización
* **Instalación Desatendida [Concepto]:** Despliegue automatizado de un sistema operativo sin intervención manual del usuario, mediante un archivo de respuestas preconfigurado [43, 44].
* **Ventajas Profesionales [Técnica]:** Ahorro de tiempo, eliminación de errores de configuración e implantación de parámetros homogéneos en despliegues masivos [46].
* **Herramientas en Entornos Windows:**
    * **Windows System Image Manager (Windows SIM) [Técnica]:** Herramienta incluida en **Windows ADK** (*Windows Assessment and Deployment Kit*) para crear archivos de respuesta XML (autounattend.xml) [43, 64].
* **Herramientas en Entornos Debian/Linux:**
    * **Preseed (** `preseed.cfg` **) [Técnica]:** Archivo de configuración que responde automáticamente a las preguntas del instalador de Debian [43, 66].
    * **FAI (Fully Automatic Installation) [Técnica]:** Aplicación que simplifica la generación de archivos de respuestas para preinstalación, instalación y postinstalación [45, 66].
    * **Kickstart [Técnica]:** Plantilla de automatización para distribuciones derivadas de Red Hat [45].

---

###### 8. Proceso de Arranque, Firmware y Particionado
* **Proceso de Arranque y POST [Técnica]:** Encendido de la PSU -> ejecución del firmware (BIOS/UEFI) -> test autocomprobación POST [47] -> lectura del orden de arranque -> transferencia del control al cargador de arranque (*bootloader*) [48].
* **Estándares de Particionado de Disco:**
    * **MBR (Master Boot Record) [Técnica]:** Estándar tradicional en BIOS Legacy. Ubicado en el primer sector del disco. Permite hasta 4 particiones primarias (o 3 primarias + 1 extendida con particiones lógicas). Límite de 2 TB por unidad.
    * **GPT (GUID Partition Table) [Técnica]:** Estándar moderno asociado a UEFI. Ofrece cabecera redundante (primaria y secundaria), admite hasta 128 particiones primarias y hasta 8 ZB de capacidad [67].
* **Esquema de Particiones Creado por Windows en UEFI [Técnica]:**
    1. **ESP (EFI System Partition):** Partición formateada en FAT32 que contiene los ejecutables EFI para el arranque del sistema [67].
    2. **MSR (Microsoft Reserved Partition):** Reservada para la gestión interna del disco GPT [67].
    3. **Windows Partition:** Contiene el sistema operativo y archivos de usuario en formato NTFS [67].
    4. **Recovery Partition:** Aloja las herramientas del entorno de recuperación (WinRE) [67].
* **Gestores de Arranque (Bootloaders) [Técnica]:**
    * **Windows Boot Manager [Técnica]:** Integrado por el ejecutable bootmgr y la base de datos BCD (*Boot Configuration Data*) [68]. Se administra mediante bcdedit en consola, msconfig en interfaz gráfica o herramientas como EasyBCD [68].
    * **GRUB (GRand Unified Bootloader) [Técnica]:** Gestor de arranque estándar en GNU/Linux que permite seleccionar e iniciar múltiples sistemas operativos en la misma máquina (*Dual-Boot*) [48].

---

###### 9. Mantenimiento y Actualización del Sistema Operativo
* **Objetivos de las Actualizaciones [Técnica]:** Corregir vulnerabilidades de seguridad, solucionar errores, aumentar la compatibilidad y optimizar el rendimiento [50, 69].
* **Planificación y Políticas Operativas [Técnica]:** Se deben configurar ventanas de mantenimiento y políticas fuera del horario crítico de producción para evitar saturación de ancho de banda o caídas de servicio [51, 70].
* **Gestión por Sistema Operativo [Técnica]:**
    * **Windows:** Administrado a través del servicio integrado **Windows Update** [51, 70].
    * **Debian / Linux:** Gestión mediante repositorios con comandos `apt update && apt upgrade` [51] o mediante tareas programadas automatizadas con `cron` [70] y `unattended-upgrades`.

---

###### 10. Gestión de Aplicaciones y Características
* **Administración en Windows [Técnica]:**
    * Accesible desde *Configuración -> Aplicaciones y características* y *Programas y características*.
    * Permite la instalación mediante ejecutables (.exe, .msi), desinstalación limpia y la activación/desactivación de características opcionales del sistema.
* **Administración en Debian / Linux [Técnica]:**
    * **Línea de Comandos (CLI):** Uso de los gestores `apt`, `apt-get` y `aptitude` para instalar paquetes en formato .deb [51, 71].
    * **Interfaz Gráfica (GUI):** **Synaptic** (*Package Manager*), que ofrece un índice temático, organiza paquetes por categorías, muestra descripciones y gestiona dependencias de software automáticamente [71].

---

###### 11. Virtualización y Entornos de Pruebas con Oracle VM VirtualBox
* **Arquitectura de Virtualización [Concepto]:**
    * **Anfitrión (Host):** Equipo físico real que aporta el hardware (CPU, RAM, disco) [157, 159, 217, 227].
    * **Invitado (Guest):** Sistema operativo que se ejecuta dentro de la máquina virtual [157, 158, 217, 227].
    * **Hipervisor Tipo 2 (Hosted):** Software como VirtualBox que corre sobre el sistema operativo anfitrión [217, 227].
* **Selección de Imágenes ISO y Arquitectura CPU [Técnica]:**
    * **x64 vs. ARM64:** Al descargar las imágenes ISO para la máquina virtual (Windows 11, Ubuntu, etc.), es crítico seleccionar la ISO correspondiente a la arquitectura del procesador del equipo Host (**x64** para Intel/AMD tradicional o **ARM64** para procesadores de tipo ARM o Apple Silicon) [159, 160].
* **Herramientas y Buenas Prácticas [Técnica]:**
    * **Instantáneas (Snapshots):** Captura del estado exacto de la VM para regresar a él tras realizar pruebas o antes de actualizaciones críticas [193, 204, 210, 217, 227].
    * **Guest Additions:** Paquete de controladores especiales dentro del sistema invitado para pantalla completa, ratón integrado y carpetas compartidas [217, 227].
    * **Liberación de Cursor (`Ctrl` Derecho):** La tecla host predeterminada en VirtualBox es la tecla **`Ctrl` derecho**, que permite liberar el puntero del ratón atrapado dentro de la ventana de la VM invitada [167]. Esto permite usar herramientas externas como *Recortes* en Windows para tomar capturas del proceso de instalación fácilmente [168, 169].
    * **Regla del 50% de RAM:** No asignar a las VMs más del 50% de la memoria RAM física del Host para evitar *swapping* excesivo y congelación del sistema anfitrión [186, 196, 217, 227].
