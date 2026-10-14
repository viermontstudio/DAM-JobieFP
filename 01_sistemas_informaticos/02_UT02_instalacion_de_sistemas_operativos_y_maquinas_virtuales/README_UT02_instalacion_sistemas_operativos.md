# 💻 UT02 — Instalación de Sistemas Operativos y Máquinas Virtuales

## 1. Concepto y Funciones del Sistema Operativo [Concepto]
* **Sistema Operativo (SO) [Concepto]:** Componente fundamental de software que actúa como intermediario ("director de orquesta") entre el hardware del equipo, las aplicaciones y el usuario. Administra los recursos del sistema y coordina el funcionamiento de todos sus componentes físicos.
* **El Tríptico Fundamental y Características Clave [Concepto]:**
  * **Adaptabilidad:** Capacidad de ajustarse a la evolución continua del hardware y del software.
  * **Facilidad de uso:** Busca un equilibrio entre la comodidad para el usuario y la eficiencia en el consumo de recursos.
  * **Eficiencia:** Optimiza el acceso a recursos limitados priorizando su uso de forma efectiva.
* **Gestores Principales del Sistema Operativo [Técnica]:**
  1. **Gestión de Procesos:** Controla la ejecución de las aplicaciones organizándolas en procesos e hilos. Asigna tiempos de microprocesador y prioridades según políticas orientadas al usuario o al sistema.
  2. **Gestión de Memoria RAM y Virtual:** Asigna y libera espacio de memoria dinámica. Cuando la memoria RAM física es insuficiente, utiliza memoria virtual en disco mediante paginación y segmentación (*swapping*).
  3. **Gestión de Entradas/Salidas (E/S):** Regula la comunicación con periféricos y tarjetas de red mediante controladores (*drivers*), búferes (*spooling*) y colas para evitar bloquear la interacción del usuario.
  4. **Gestión de Almacenamiento Secundario:** Organiza la información en unidades lógicas (particiones, carpetas y archivos) utilizando sistemas de archivos (NTFS, ext4, APFS) manteniendo metadatos y permisos.
  5. **Gestión de Seguridad:** Controla los permisos de acceso, autentica usuarios y garantiza la disponibilidad, confidencialidad e integridad del sistema.
  6. **Gestión de Errores:** Detecta, aísla, registra en *logs* y notifica fallos de hardware o software, empleando sistemas de archivos con *journaling* para recuperar la coherencia tras un apagado imprevisto.
  7. **Gestión de la Interfaz de Usuario:** Proporciona el entorno de interacción, que puede ser textual (Línea de Comandos / CLI) o gráfico (Interfaz Gráfica de Usuario / GUI).

---

## 2. Clasificación de los Sistemas Operativos [Concepto]
* **Según la Cantidad de Procesos Simultáneos:**
  * **Monotarea / Monoprogramado [Concepto]:** Solo permite ejecutar un proceso a la vez (ej. MS-DOS).
  * **Multitarea / Multiprogramado [Concepto]:** Mantiene y ejecuta múltiples procesos e hilos simultáneamente en memoria.
* **Según el Número de Usuarios Simultáneos:**
  * **Monousuario [Concepto]:** Diseñado para que un único usuario aproveche la totalidad de los recursos del equipo.
  * **Multiusuario [Concepto]:** Permite sesiones concurrentes compartiendo y gestionando los recursos entre varios usuarios mediante control de permisos (ej. Windows Server, Debian).
* **Según el Tipo de Procesamiento:**
  * **Tiempo Real [Concepto]:** Cumple plazos de respuesta estrictos y comportamiento predecible (ej. aviación, centrales nucleares, sistemas de alarmas).
  * **Interactivo / Tiempo Compartido [Concepto]:** Requiere la participación constante del usuario (ej. procesadores de texto, juegos, SO de escritorio).
  * **Por Lotes (Batch) [Concepto]:** Agrupa tareas similares sin intervención del usuario y las ejecuta en serie.
* **Según el Tipo de Interfaz:**
  * **Textual (CLI) [Concepto]:** Funciona mediante comandos escritos en terminal. Es más potente y consume menos recursos.
  * **Gráfica (GUI) [Concepto]:** Presenta ventanas, menús e iconos. Es intuitiva, pero requiere mayor consumo de recursos hardware.
* **Según la Forma de Ofrecer Servicios:**
  * **Cliente / Escritorio [Concepto]:** Diseñado para ordenadores personales en entornos domésticos o de oficina.
  * **En Red / Servidor [Concepto]:** Administra usuarios, comunicaciones y recursos centralizados en una red corporativa.
  * **Distribuidos [Concepto]:** Hace que múltiples equipos independientes trabajen juntos como si fueran un único sistema.
  * **Embebidos / Integrados [Concepto]:** Integrados en dispositivos físicos específicos (routers, electrodomésticos, vehículos).

---

## 3. Arquitectura del Sistema Operativo y Hardware de Apoyo [Técnica]
* **Modelos Arquitectura de Kernel [Concepto]:**
  * **Monolítico [Técnica]:** Todos los servicios del sistema (procesos, memoria, archivos, drivers) ejecutan en el mismo espacio de memoria del kernel. Ofrece máxima velocidad, pero un fallo en cualquier módulo puede colapsar todo el sistema.
  * **Microkernel [Técnica]:** Reduce el núcleo a las funciones mínimas indispensables, trasladando servicios no críticos a procesos independientes en espacio de usuario. Aumenta la estabilidad y aislamiento ante fallos.
  * **Kernel Híbrido [Técnica]:** Combina la estructura modular del microkernel con componentes monolíticos para optimizar rendimiento sin perder estabilidad.
* **Arquitectura de Memoria Caché de la CPU [Técnica]:**
  * **Niveles L1, L2 y L3:** La memoria caché está integrada físicamente dentro del chip del procesador. Se divide en L1 (ultrarrápida y pequeña), L2 (capacidad intermedia) y L3 (mayor capacidad, ligeramente más lenta).
  * **Algoritmos de Predicción:** El procesador utiliza algoritmos internos de predicción por hardware para determinar qué datos cargar preventivamente en la caché.
* **Placa Base y Bus de Comunicación [Técnica]:**
  * **NorthBridge vs. SouthBridge:** El *NorthBridge* interconecta la CPU con componentes de alta velocidad (RAM, PCIe gráfico). El *SouthBridge* gestiona periféricos e interfaces más lentos (SATA, USB, audio, BIOS).
  * **Módulos RAM SIMM vs. DIMM:** Los módulos *SIMM* disponen de contactos en una sola cara. Los módulos *DIMM* poseen contactos independientes en ambas caras, permitiendo transferencias Dual-Channel.
* **Ensamblaje Físico y Gestión Térmica [Técnica]:**
  * **Sensibilidad del Socket:** Los pines del zócalo (*socket*) y de la CPU son frágiles. Alinear mal el procesador dobla los pines, provocando un daño irreversible.
  * **Pasta Térmica:** Compuesto que rellena imperfecciones microscópicas entre la CPU y el disipador para maximizar la transferencia de calor.

---

## 4. Planificación de la Instalación y Copias de Seguridad [Técnica]
* **Criterios de Selección del Sistema Operativo [Técnica]:** Análisis de TCO (*Total Cost of Ownership* / Coste Total de Propiedad), estabilidad, compatibilidad con software/hardware y licencias.
* **Requisitos Mínimos de Hardware [Técnica]:**
  * **Windows 10 / 11 (64 bits):** CPU 1 GHz (2 o más núcleos), 4 GB RAM, 64 GB de disco duro, UEFI + TPM 2.0.
  * **Debian GNU/Linux:**
    * *Sin Interfaz Gráfica (CLI):* CPU 1 GHz, 256 MB RAM, 2 GB de disco duro.
    * *Con Interfaz Gráfica (GUI):* CPU 1 GHz, 1 GB RAM, 10 GB de disco duro.
* **Copias de Seguridad Previas [Técnica]:** Medida imprescindible previa a la instalación para evitar la pérdida de información durante el formateo.
  * **Herramientas Recomendadas:** CloneApp (Windows) y Aptik (Debian).

---

## 5. Proceso de Instalación de Sistemas Operativos [Técnica]
* **Secuencia General de Instalación [Técnica]:** Preparación del medio de instalación (USB/ISO grabado con *Rufus*), configuración del orden de arranque en BIOS/UEFI, particionado y formateo del disco, copia del núcleo y archivos base e instalación de controladores esenciales.
* **Secuencia Paso a Paso en Windows 10/11 [Técnica]:**
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
  4. Particionado de discos (opción guiada *Todos los ficheros en la misma partición*).
  5. Configuración del gestor de paquetes conectando a la réplica de repositorios (`deb.debian.org`).
  6. Selección de colecciones de programas y entorno de escritorio (GNOME, Xfce, KDE Plasma).
  7. Instalación del cargador de arranque GRUB en el registro principal del disco.

---

## 6. Instalaciones Desatendidas y Automatización [Concepto]
* **Instalación Desatendida [Concepto]:** Despliegue automatizado de un sistema operativo sin intervención manual del usuario, mediante un archivo de respuestas preconfigurado.
* **Ventajas Profesionales [Técnica]:** Ahorro de tiempo, eliminación de errores de configuración e implantación de parámetros homogéneos en despliegues masivos.
* **Herramientas en Entornos Windows:**
  * **Windows System Image Manager (Windows SIM) [Técnica]:** Herramienta incluida en **Windows ADK** (*Windows Assessment and Deployment Kit*) para crear archivos de respuesta XML (`autounattend.xml`).
* **Herramientas en Entornos Debian/Linux:**
  * **Preseed (`preseed.cfg`) [Técnica]:** Archivo de configuración que responde automáticamente a las preguntas del instalador de Debian.
  * **FAI (Fully Automatic Installation) [Técnica]:** Aplicación que simplifica la generación de archivos de respuestas para preinstalación, instalación y postinstalación.
  * **Kickstart [Técnica]:** Plantilla de automatización para distribuciones derivadas de Red Hat.

---

## 7. Proceso de Arranque, Firmware y Particionado [Técnica]
* **Proceso de Arranque y POST [Técnica]:** Encendido de la PSU -> ejecución del firmware (BIOS/UEFI) -> test autocomprobación POST -> lectura del orden de arranque -> transferencia del control al cargador de arranque (*bootloader*).
* **Estándares de Particionado de Disco:**
  * **MBR (Master Boot Record) [Técnica]:** Estándar tradicional en BIOS Legacy. Ubicado en el primer sector del disco. Permite hasta 4 particiones primarias (o 3 primarias + 1 extendida). Límite de 2 TB por unidad.
  * **GPT (GUID Partition Table) [Técnica]:** Estándar moderno asociado a UEFI. Ofrece cabecera redundante, admite hasta 128 particiones primarias y hasta 8 ZB de capacidad.
* **Esquema de Particiones Creado por Windows en UEFI [Técnica]:**
  1. **ESP (EFI System Partition):** Partición formateada en FAT32 que contiene los ejecutables EFI para el arranque del sistema.
  2. **MSR (Microsoft Reserved Partition):** Reservada para la gestión interna del disco GPT.
  3. **Windows Partition:** Contiene el sistema operativo y archivos de usuario en formato NTFS.
  4. **Recovery Partition:** Aloja las herramientas del entorno de recuperación (WinRE).
* **Gestores de Arranque (Bootloaders) [Técnica]:**
  * **Windows Boot Manager [Técnica]:** Integrado por el ejecutable `bootmgr` y la base de datos BCD (*Boot Configuration Data*). Se administra mediante `bcdedit` en consola, `msconfig` en interfaz gráfica o herramientas como EasyBCD.
  * **GRUB (GRand Unified Bootloader) [Técnica]:** Gestor de arranque estándar en GNU/Linux que permite seleccionar e iniciar múltiples sistemas operativos en la misma máquina (*Dual-Boot*).

---

## 8. Diagnóstico Práctico del Entorno de Arranque y Almacenamiento en Windows [Técnica]

Procedimiento de inspección no destructivo mediante herramientas nativas integradas en Windows (`Windows + R`) para diagnosticar el estado del firmware, el esquema de particionado y la configuración de arranque sin modificar parámetros del sistema:

### 8.1. Inspección del Modo de Firmware (`msinfo32`) [Técnica]
* **Comando de Ejecución:** Abrir la ventana Ejecutar (`Windows + R`), escribir `msinfo32` y pulsar *Intro*.
* **Herramienta:** *Información del Sistema* (muestra resumen del procesador, memoria RAM, versión de Windows y firmware).
* **Parámetro Clave:** Buscar la línea **Modo de BIOS**.
* **Interpretación:**
  * **UEFI:** Indica que el equipo arranca mediante el estándar de firmware moderno.
  * **BIOS Heredado / Legacy:** Indica que el sistema utiliza la arquitectura de arranque tradicional.

### 8.2. Inspección del Esquema de Particionado y Estructura del Disco (`diskmgmt.msc`) [Técnica]
* **Comando de Ejecución:** Abrir Ejecutar (`Windows + R`), escribir `diskmgmt.msc` y pulsar *Intro*.
* **Herramienta:** *Administrador de Discos* (consola gráfica para visualizar unidades físicas, volúmenes y particiones).
* **Verificación de Estilo de Partición (GPT vs. MBR):**
  1. Hacer clic derecho sobre el conector del disco físico (ej. *Disco 0*) -> Seleccionar **Propiedades**.
  2. Acceder a la pestaña **Volúmenes** -> Consultar el apartado **Estilo de partición**.
* **Relación Técnica de Coherencia:**
  * **Modo UEFI $\leftrightarrow$ Tabla GPT:** Estándar moderno de arranque con soporte para más de 4 particiones primarias y discos > 2 TB.
  * **Modo Legacy / BIOS $\leftrightarrow$ Tabla MBR:** Estándar tradicional con límite de 4 particiones primarias y 2 TB.
* **Análisis de ParticionesReservadas:** Muestra la partición principal (letra `C:`) y particiones pequeñas de sistema (ESP, MSR y Entorno de Recuperación).
* **⚠️ Criterio de Soporte Técnico [Técnica]:** No se deben eliminar ni modificar las particiones pequeñas de sistema en equipos en producción, ya que contienen archivos críticos para el arranque y la recuperación del sistema operativo.

### 8.3. Inspección del Gestor de Arranque (`msconfig`) [Técnica]
* **Comando de Ejecución:** Abrir Ejecutar (`Windows + R`), escribir `msconfig` y pulsar *Intro*.
* **Herramienta:** *Configuración del Sistema*.
* **Inspección de Arranque:** En la pestaña **Arranque**, permite consultar la lista de sistemas operativos registrados en el gestor de arranque (Windows Boot Manager / BCD).
* **Cadena del Proceso de Encendido:** Pulsar botón encendido -> Pruebas POST de la PSU/Placa -> Carga del firmware (BIOS/UEFI) -> Lectura del orden de arranque -> Transferencia del control a Windows Boot Manager -> Inicio del Kernel de Windows.

---

## 9. Mantenimiento y Actualización del Sistema Operativo [Técnica]
* **Objetivos de las Actualizaciones [Técnica]:** Corregir vulnerabilidades de seguridad, solucionar errores, aumentar la compatibilidad y optimizar el rendimiento.
* **Planificación y Políticas Operativas [Técnica]:** Se deben configurar ventanas de mantenimiento fuera del horario crítico de producción para evitar saturación de ancho de banda o caídas de servicio.
* **Gestión por Sistema Operativo [Técnica]:**
  * **Windows:** Administrado a través del servicio integrado **Windows Update**.
  * **Debian / Linux:** Gestión mediante repositorios con comandos `apt update && apt upgrade` o mediante tareas programadas automatizadas con `cron` y `unattended-upgrades`.

---

## 10. Gestión de Aplicaciones y Características [Técnica]
* **Administración en Windows [Técnica]:**
  * Accesible desde *Configuración -> Aplicaciones y características* y *Programas y características*.
  * Permite la instalación mediante ejecutables (`.exe`, `.msi`), desinstalación limpia y la activación/desactivación de características opcionales del sistema.
* **Administración en Debian / Linux [Técnica]:**
  * **Línea de Comandos (CLI):** Uso de gestores `apt`, `apt-get` y `aptitude` para instalar paquetes `.deb`.
  * **Interfaz Gráfica (GUI):** **Synaptic** (*Package Manager*), que ofrece un índice temático, organiza paquetes por categorías y gestiona dependencias de software automáticamente.

---

## 11. Virtualización y Entornos de Pruebas con Oracle VM VirtualBox [Técnica]
* **Arquitectura de Virtualización [Concepto]:**
  * **Anfitrión (Host):** Equipo físico real que aporta el hardware (CPU, RAM, disco).
  * **Invitado (Guest):** Sistema operativo que se ejecuta dentro de la máquina virtual.
  * **Hipervisor Tipo 2 (Hosted):** Software como VirtualBox que corre sobre el sistema operativo anfitrión.
* **Selección de Imágenes ISO y Arquitectura CPU [Técnica]:**
  * **x64 vs. ARM64:** Al descargar imágenes ISO para la VM (Windows 11, Ubuntu), es crítico seleccionar la ISO correspondiente a la arquitectura del procesador del Host (**x64** para Intel/AMD tradicional o **ARM64** para procesadores ARM o Apple Silicon).
* **Herramientas y Buenas Prácticas [Técnica]:**
  * **Instalación Desatendida:** Se recomienda desmarcar la casilla de instalación desatendida (*Skip Unattended Installation*) en VirtualBox si se desea realizar el proceso de instalación manual e interactivo paso a paso.
  * **Instantáneas (Snapshots):** Captura del estado exacto de la VM para regresar a él tras realizar pruebas.
  * **Guest Additions:** Paquete de controladores especiales dentro del sistema invitado para pantalla completa, ratón integrado y carpetas compartidas.
  * **Liberación de Cursor (`Ctrl` Derecho):** La tecla host predeterminada en VirtualBox es `Ctrl` derecho, que libera el ratón atrapado dentro de la VM invitada.
  * **Regla del 50% de RAM:** No asignar a las VMs más del 50% de la memoria RAM física del Host para evitar *swapping* excesivo y congelación del sistema anfitrión.
