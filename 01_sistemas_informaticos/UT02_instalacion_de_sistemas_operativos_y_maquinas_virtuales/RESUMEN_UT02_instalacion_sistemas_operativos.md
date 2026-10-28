🏠 **[Volver al Índice Principal](../../README.md)** | 📐 **[Ir al Esquema Resumen](./ESQUEMA_UT02_instalacion_sistemas_operativos.md)**

---

# 💿 GUÍA TEÓRICA Y RESUMEN — UT02: Instalación de Sistemas Operativos y Máquinas Virtuales
**Asignatura:** Sistemas Informáticos (1º DAM/DAW)  
**Marco Metodológico:** Protocolo PEM-4 & Metodología Interna DAM

---

## 1. Concepto y Funciones del Sistema Operativo
Un Sistema Operativo (S.O.) es el software de sistema fundamental que administra los recursos de hardware del equipo, abstrae la complejidad física y ofrece una interfaz de ejecución para las aplicaciones del usuario.
* **Funciones Clave:** Gestión del procesador, administración de memoria RAM, abstracción del sistema de archivos, gestión de I/O y control de seguridad/privilegios.

---

## 2. Arquitectura del Kernel y Anillos de Protección
* **Kernel (Núcleo):** El componente del S.O. que se ejecuta en el nivel más privilegiado del procesador.
* **Tipos de Kernel:**
  * **Monolítico:** Todos los servicios (gestión de memoria, drivers, red, sistema de archivos) se ejecutan dentro del espacio del kernel en Ring 0 (ej. Linux, BSD).
  * **Microkernel:** Solo las funciones mínimas indispensables residen en Ring 0 (IPC, memoria básica, hilos); el resto de drivers y servicios corren como procesos de usuario en Ring 3 (ej. QNX, MINIX).
  * **Híbrido:** Estructura monolítica modularizada (ej. Windows NT, macOS X).
* **Anillos de Protección (Rings):**
  * **Ring 0 (Modo Kernel):** Acceso total y sin restricciones al hardware y las instrucciones de la CPU.
  * **Ring 3 (Modo Usuario):** Entorno restringido donde corren las aplicaciones para evitar que un fallo cuelgue el sistema.

---

## 3. Firmware y Estructuras de Partición
* **MBR (*Master Boot Record*):**
  * Estructura clásica situada en el primer sector del disco (LBA 0, 512 bytes).
  * Admite un máximo de **4 particiones primarias** (o 3 primarias + 1 extendida con múltiples unidades lógicas).
  * Tamaño máximo de disco direccionable: **2 TB**.
* **GPT (*GUID Partition Table*):**
  * Estándar moderno vinculado a firmware **UEFI**.
  * Soporta hasta **128 particiones primarias** de forma nativa sin necesidad de particiones extendidas.
  * Tamaño máximo por volumen: **9.4 Zettabytes**.
  * Incluye copia de seguridad de la tabla de particiones al final del disco (*Protective MBR* al inicio).
* **Esquema Quad-Partition Estándar en Windows/UEFI:**
  1. `ESP` (EFI System Partition - FAT32, contiene los cargadores de arranque `.efi`).
  2. `MSR` (Microsoft Reserved Partition).
  3. Partición de Sistema / Datos (NTFS).
  4. Partición de Recuperación (Recovery Environment).

---

## 4. Métodos de Instalación y Despliegue
* **Instalación Limpia (*Clean Install*):** Formateo completo de la partición de destino y despliegue desde cero.
* **Actualización (*Upgrade*):** Mantiene archivos de usuario y aplicaciones sobre una versión previa del S.O.
* **Arranque Dual / Múltiple (*Dual Boot*):** Coexistencia de dos o más S.O. en particiones independientes (ej. Windows 11 + Ubuntu Linux) controlados por un gestor de arranque.
* **Despliegue Desatendido / Automatizado:**
  * **Windows:** Uso de archivos de respuesta `autounattend.xml` mediante WIM / Sysprep.
  * **Linux:** Archivos de automatización `preseed.cfg` (Debian/Ubuntu) o `kickstart.ks` (RedHat/Fedora).

---

## 5. Gestores de Arranque
* **GRUB2 (*Grand Unified Bootloader*):** Gestor de arranque multietapa estándar en distribuciones Linux. Configurable a través de `/etc/default/grub` y `/boot/grub/grub.cfg` (actualizable con `update-grub`).
* **Windows Boot Manager (BOOTMGR) y BCD:** Utiliza la base de datos **BCD (*Boot Configuration Data*)**, administrable desde la consola con la herramienta CLI `bcdedit`.

---

## 6. Consolas de Administración y Diagnóstico
* **`msinfo32`:** Información del sistema (versión de BIOS/UEFI, modo de arranque, memoria física, componentes).
* **`diskmgmt.msc`:** Administración visual de discos, particiones y volúmenes en Windows.
* **`msconfig`:** Configuración del sistema (arranque seguro, servicios de inicio, diagnósticos).
* **`dxdiag`:** Herramienta de diagnóstico de DirectX, componentes gráficos y de sonido.
* **`sysdm.cpl`:** Propiedades del sistema (variables de entorno, rendimiento, perfil de usuario).

---

## 7. Virtualización e Hipervisores
* **Hipervisor Tipo 1 (Bare-Metal):** Corre sobre el hardware desnudo (ej. VMware ESXi, Proxmox VE, Microsoft Hyper-VServer). Alta eficiencia y rendimiento empresarial.
* **Hipervisor Tipo 2 (Hosted):** Aplicación que corre sobre un S.O. anfitrión (ej. Oracle VM VirtualBox, VMware Workstation).
* **Herramientas de Integración (Guest Additions / VMware Tools):** Controladores y servicios instalados dentro de la VM invitada para habilitar carpetas compartidas, portapapeles bidireccional y aceleración gráfica.

---

🏠 **[Volver al Índice Principal](../../README.md)** | 📐 **[Ir al Esquema Resumen](./ESQUEMA_UT02_instalacion_sistemas_operativos.md)**
