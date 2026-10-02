# 💻 UT02 — Instalación de Sistemas Operativos y Máquinas Virtuales

#### 1. Concepto y Funciones del Sistema Operativo
* **Sistema Operativo (SO) [Concepto]:** Componente fundamental de software que actúa como intermediario ("director de orquesta") entre el hardware del equipo, las aplicaciones y el usuario. Administra los recursos del sistema y coordina el funcionamiento de todos sus componentes físicos.
* **El Tríptico Fundamental y Características Clave [Concepto]:**
  * **Adaptabilidad:** Capacidad de ajustarse a la evolución continua del hardware y del software.
  * **Facilidad de uso:** Busca un equilibrio entre la comodidad para el usuario y la eficiencia en el consumo de recursos.
  * **Eficiencia:** Optimiza el acceso a recursos limitados priorizando su uso de forma efectiva.
* **Gestores Principales del Sistema Operativo [Técnica]:**
  1. **Gestión de Procesos:** Controla la ejecución de las aplicaciones organizándolas en procesos e hilos. Asigna tiempos de microprocesador y prioridades según políticas orientadas al usuario (E/S, respuesta rápida a periféricos) o al sistema (rendimiento bruto para cálculo intensivo).
  2. **Gestión de Memoria RAM y Virtual:** Asigna y libera espacio de memoria dinámica. Cuando la memoria RAM física es insuficiente, utiliza memoria virtual en disco mediante paginación y segmentación (intercambio / *swapping*).
  3. **Gestión de Entradas/Salidas (E/S):** Regula la comunicación con periféricos y tarjetas de red mediante controladores (*drivers*), búferes (*spooling*) y colas para evitar bloquear la interacción del usuario.
  4. **Gestión de Almacenamiento Secundario:** Organiza la información en unidades lógicas (particiones, carpetas y archivos) utilizando sistemas de archivos (NTFS, ext4, APFS) manteniendo metadatos y permisos.
  5. **Gestión de Seguridad:** Controla los permisos de acceso, autentica usuarios y garantiza la disponibilidad, confidencialidad e integridad del sistema.
  6. **Gestión de Errores:** Detecta, aisla, registra en *logs* y notifica fallos de hardware o software, empleando sistemas de archivos con *journaling* para recuperar la coherencia tras un apagado imprevisto.
  7. **Gestión de la Interfaz de Usuario:** Proporciona el entorno de interacción, que puede ser textual (Línea de Comandos / CLI) o gráfico (Interfaz Gráfica de Usuario / GUI).

---

#### 2. Clasificación de los Sistemas Operativos
* **Según la Cantidad de Procesos Simultáneos:**
  * **Monotarea / Monoprogramado [Concepto]:** Solo permite ejecutar un proceso a la vez (ej. MS-DOS).
  * **Multitarea / Multiprogramado [Concepto]:** Mantiene y ejecuta múltiples procesos e hilos simultáneamente en memoria.
* **Según el Número de Usuarios Simultáneos:**
  * **Monousuario [Concepto]:** Diseñado para que un único usuario aproveche la totalidad de los recursos del equipo.
  * **Multiusuario [Concepto]:** Permite sesiones concurrentes compartiendo y gestionando los recursos entre varios usuarios mediante control de permisos (ej. Windows Server, Debian).
* **Según el Tipo de Procesamiento:**
  * **Tiempo Real [Concepto]:** Cumple plazos de respuesta estrictos y comportamiento predecible (ej. centrales nucleares, aviación, sistemas de alarmas).
  * **Interactivo / Tiempo Compartido [Concepto]:** Requiere la participación constante del usuario (ej. procesadores de texto, juegos, SO de escritorio).
  * **Por Lotes (Batch) [Concepto]:** Agrupa tareas similares sin intervención del usuario y las ejecuta en serie; si una falla, se detiene todo el lote (ej. facturación masiva, envío masivo de informes).
* **Según el Tipo de Interfaz:**
  * **Textual (CLI) [Concepto]:** Funciona mediante comandos escritos en terminal. Es más potente y consume menos recursos.
  * **Gráfica (GUI) [Concepto]:** Presenta ventanas, menús e iconos. Es intuitiva, pero requiere mayor consumo de recursos hardware.
* **Según la Forma de Ofrecer Servicios:**
  * **Cliente / Escritorio [Concepto]:** Diseñado para ordenadores personales en entornos domésticos o de oficina.
  * **En Red / Servidor [Concepto]:** Administra usuarios, comunicaciones y recursos centralizados en una red corporativa.
  * **Distribuidos [Concepto]:** Hace que múltiples equipos independientes trabajen juntos como si fueran un único sistema.
  * **Embebidos / Integrados [Concepto]:** Integrados en dispositivos físicos específicos (routers, electrodomésticos, vehículos).

---

#### 3. Arquitecturas del Kernel (Núcleo)
* **Arquitectura en Capas o Anillos [Concepto]:** Estructura jerárquica dividida en niveles concéntricos donde cada capa ofrece servicios a la superior y se apoya en la inferior.
  * **Partes de la Estructura [Técnica]:** Incluye el **Núcleo** (interactúa con el hardware mediante la capa *HAL* o Capa de Abstracción de Hardware), la **Capa de Servicios** (gestión de procesos, memoria, E/S) y la **Interfaz de Usuario**.
* **Arquitectura Monolítica [Concepto]:** Todos los servicios del sistema (procesos, memoria, sistema de archivos, drivers) se ejecutan dentro del mismo espacio de memoria compartiendo el núcleo. Es muy rápida, pero un fallo en cualquier módulo afecta a todo el sistema (ej. MS-DOS, kernel Linux de Debian).
* **Microkernel [Concepto]:** Reduce el núcleo a las funciones mínimas indispensables (gestión básica de memoria, hilos y comunicación IPC), ejecutando el resto de servicios en **Modo Usuario**. Aumenta la estabilidad, reduce la superficie de fallos y facilita la mantenibilidad y portabilidad.
* **Kernel Híbrido [Concepto]:** Evolución que combina la estructura modular y estable del microkernel con la rapidez de ejecución del modelo monolítico. Utilizado en Windows NT (Windows 10/11) y macOS.

---

#### 4. Versiones de Sistemas Operativos Actuales
* **Sistemas Operativos de Microsoft:**
  * **Escritorio (Windows 10/11):** Ediciones *Home* (uso básico), *Pro* (pymes/entornos de trabajo), *Enterprise* (gestión corporativa avanzada), *Education* (centros académicos), *Pro for Workstations* (cargas pesadas) e *IoT* (dispositivos conectados).
  * **Servidores (Windows Server 2019/2022):** Ediciones *Essentials* (pequeños negocios), *Standard* (baja virtualización) y *Datacenter* (entornos en la nube y alta virtualización).
* **Sistemas Operativos GNU/Linux y BSD:**
  * **Distribuciones de Escritorio:** *Ubuntu* y *Linux Mint* (principiantes/uso general), *Arch Linux* y *Manjaro* (avanzados/configuración a medida), *Kali Linux* y *Tails* (seguridad, pentesting y privacidad) y *Chromium OS*.
  * **Distribuciones de Servidor:** *Red Hat Enterprise Linux (RHEL)* (soporte empresarial), *Debian* (base estable de libre distribución), *Ubuntu Server*, *SUSE Linux Enterprise (SLES)*, *CentOS* y *FreeBSD*.
* **Sistemas Operativos de Apple:**
  * **macOS:** Diseñado exclusivamente para ordenadores Mac con alta optimización e integración hardware.
  * **Sistemas Específicos:** *iOS* (iPhone), *iPadOS* (tablets) y *watchOS* (smartwatches).

---

#### 5. Planificación de la Instalación y Copias de Seguridad
* **Criterios de Selección del Sistema Operativo [Técnica]:** Análisis de TCO (*Total Cost of Ownership* / Coste Total de Propiedad), estabilidad, compatibilidad con software/hardware y licencias.
* **Requisitos Mínimos de Hardware [Técnica]:**
  * **Windows 10 (64 bits):** CPU 1 GHz, 2 GB RAM (4 GB recomendado), 20 GB de disco duro, pantalla 800x600 y tarjeta gráfica DirectX 9.
  * **Debian GNU/Linux:**
    * *Sin Interfaz Gráfica (CLI):* CPU Pentium 4 1 GHz, 128 MB RAM (512 MB recomendado), 2 GB de disco duro.
    * *Con Interfaz Gráfica (GUI):* CPU Pentium 4 1 GHz, 256 MB RAM (1 GB recomendado), 10 GB de disco duro.
* **Copias de Seguridad Previas [Técnica]:** Medida imprescindible previa a la instalación para evitar la pérdida de información durante el formateo.
  * **Herramientas Recomendadas:** `CloneApp` (para entornos Windows) y `Aptik` (para entornos Debian).

---

#### 6. Proceso de Instalación de Sistemas Operativos
* **Secuencia General de Instalación [Técnica]:** Preparación del medio de instalación (USB/ISO grabado con herramientas como *Rufus*), configuración del orden de arranque en BIOS/UEFI, particionado y formateo del disco, copia del núcleo y archivos base, e instalación de controladores esenciales.
* **Secuencia Paso a Paso en Windows 10 [Técnica]:**
  1. Selección de idioma, formato de hora, moneda y mapa de teclado -> Pulsar *Siguiente* y *Instalar ahora*.
  2. Introducción de la clave de producto o selección de *No tengo clave de producto*.
  3. Selección de la versión del sistema y aceptación de términos de licencia.
  4. Elección del tipo de instalación *Personalizada* (permite particionado manual).
  5. Selección/creación de la partición de destino (el asistente crea automáticamente particiones adicionales de sistema/recuperación).
  6. Copia de archivos y reinicio del sistema.
  7. Configuración de región, cuenta de usuario (Microsoft o local), PIN de seguridad y opciones de privacidad.
* **Secuencia Paso a Paso en Debian GNU/Linux [Técnica]:**
  1. Selección del idioma de instalación, ubicación geográfica y mapa de teclado.
  2. Asignación del nombre de la máquina (*hostname*) y nombre de dominio en red.
  3. Configuración de la clave de superusuario (`root`) y creación de la cuenta de usuario estándar.
  4. Particionado de discos (opción guiada *Todos los ficheros en la misma partición* para estructura simple).
  5. Configuración del gestor de paquetes conectando a la réplica de repositorios (`deb.debian.org`).
  6. Selección de colecciones de programas y entorno de escritorio (GNOME, Xfce, KDE Plasma).
  7. Instalación del cargador de arranque GRUB en el registro principal del disco.

---

#### 7. Instalaciones Desatendidas y Automatización
* **Instalación Desatendida [Concepto]:** Despliegue automatizado de un sistema operativo sin intervención manual del usuario, mediante un archivo de respuestas preconfigurado.
* **Ventajas Profesionales [Técnica]:** Ahorro de tiempo, eliminación de errores de configuración e implantación de parámetros homogéneos en despliegues masivos.
* **Herramientas en Entornos Windows:**
  * **Windows System Image Manager (Windows SIM) [Técnica]:** Herramienta incluida en **Windows ADK** (*Windows Assessment and Deployment Kit*) para crear archivos de respuesta XML (`autounattend.xml`).
* **Herramientas en Entornos Debian/Linux:**
  * **Preseed (`preseed.cfg`) [Técnica]:** Archivo de configuración que responde automáticamente a las preguntas del instalador de Debian.
  * **FAI (Fully Automatic Installation) [Técnica]:** Aplicación que simplifica la generación de archivos de respuestas para preinstalación, instalación y postinstalación.
  * **Kickstart [Técnica]:** Plantilla de automatización para distribuciones derivadas de Red Hat.

---

#### 8. Proceso de Arranque, Firmware y Particionado
* **Proceso de Arranque y POST [Técnica]:** Encendido de la PSU -> ejecución del firmware (BIOS/UEFI) -> test autocomprobación POST -> lectura del orden de arranque -> transferencia del control al cargador de arranque (*bootloader*).
* **Estándares de Particionado de Disco:**
  * **MBR (Master Boot Record) [Técnica]:** Estándar tradicional en BIOS Legacy. Ubicado en el primer sector del disco. Permite hasta 4 particiones primarias (o 3 primarias + 1 extendida con particiones lógicas). Límite de 2 TB por unidad.
  * **GPT (GUID Partition Table) [Técnica]:** Estándar moderno asociado a UEFI. Ofrece cabecera redundante (primaria y secundaria), admite hasta 128 particiones primarias y hasta 8 ZB de capacidad.
* **Esquema de Particiones Creado por Windows en UEFI [Técnica]:**
  1. **ESP (EFI System Partition):** Partición formateada en FAT32 que contiene los ejecutables EFI para el arranque del sistema.
  2. **MSR (Microsoft Reserved Partition):** Reservada para la gestión interna del disco GPT.
  3. **Windows Partition:** Contiene el sistema operativo y archivos de usuario en formato NTFS.
  4. **Recovery Partition:** Aloja las herramientas del entorno de recuperación (WinRE).
* **Gestores de Arranque (Bootloaders) [Técnica]:**
  * **Windows Boot Manager [Técnica]:** Integrado por el ejecutable `bootmgr` y la base de datos BCD (*Boot Configuration Data*). Se administra mediante `bcdedit` en consola, `msconfig` en interfaz gráfica o herramientas como `EasyBCD`.
  * **GRUB (GRand Unified Bootloader) [Técnica]:** Gestor de arranque estándar en GNU/Linux que permite seleccionar e iniciar múltiples sistemas operativos en la misma máquina (*Dual-Boot*).

---

#### 9. Mantenimiento y Actualización del Sistema Operativo
* **Objetivos de las Actualizaciones [Técnica]:** Corregir vulnerabilidades de seguridad, solucionar errores, aumentar la compatibilidad y optimizar el rendimiento.
* **Planificación y Políticas Operativas [Técnica]:** Se deben configurar ventanas de mantenimiento y políticas fuera del horario crítico de producción para evitar saturación de ancho de banda o caídas de servicio.
* **Gestión por Sistema Operativo [Técnica]:**
  * **Windows:** Administrado a través del servicio integrado **Windows Update**.
  * **Debian / Linux:** Gestión mediante repositorios con comandos `apt update && apt upgrade` o mediante tareas programadas automatizadas con `cron` y `unattended-upgrades`.

---

#### 10. Gestión de Aplicaciones y Características
* **Administración en Windows [Técnica]:**
  * Accesible desde *Configuración -> Aplicaciones y características* y *Programas y características*.
  * Permite la instalación mediante ejecutables (`.exe`, `.msi`), desinstalación limpia y la activación/desactivación de características opcionales del sistema.
* **Administración en Debian / Linux [Técnica]:**
  * **Línea de Comandos (CLI):** Uso de los gestores `apt`, `apt-get` y `aptitude` para instalar paquetes en formato `.deb`.
  * **Interfaz Gráfica (GUI):** **Synaptic** (*Package Manager*), que ofrece un índice temático, organiza paquetes por categorías, muestra descripciones y gestiona dependencias de software automáticamente.

---

#### 11. Virtualización y Entornos de Pruebas con Oracle VM VirtualBox
* **Arquitectura de Virtualización [Concepto]:**
  * **Anfitrión (Host):** Equipo físico real que aporta el hardware (CPU, RAM, disco).
  * **Invitado (Guest):** Sistema operativo que se ejecuta dentro de la máquina virtual.
  * **Hipervisor Tipo 2 (Hosted):** Software como VirtualBox que corre sobre el sistema operativo anfitrión.
* **Herramientas y Buenas Prácticas [Técnica]:**
  * **Instantáneas (Snapshots):** Captura del estado exacto de la VM para regresar a él tras realizar pruebas o antes de actualizaciones críticas.
  * **Guest Additions:** Paquete de controladores especiales dentro del sistema invitado para pantalla completa, ratón integrado y carpetas compartidas.
  * **Regla del 50% de RAM:** No asignar a las VMs más del 50% de la memoria RAM física del Host para evitar *swapping* excesivo y congelación del sistema anfitrión.
