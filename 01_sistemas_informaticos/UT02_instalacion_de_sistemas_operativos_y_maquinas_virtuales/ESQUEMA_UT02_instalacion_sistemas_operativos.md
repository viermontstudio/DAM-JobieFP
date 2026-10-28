🏠 **[Volver al Índice Principal](../../README.md)** | 📖 **[Ir a la Guía Teórica (Resumen)](./RESUMEN_UT02_instalacion_sistemas_operativos.md)**

---

---

# 💻 ESQUEMA DE ESTUDIO — UT02: Instalación de Sistemas Operativos y Máquinas Virtuales
**Asignatura:** Sistemas Informáticos (1º DAM/DAW)  
**Marco Metodológico:** Protocolo PEM-4 & Metodología Interna DAM

---

### 🗺️ El Gran Mapa Estructural: Capas del SO y Particionado de Arranque

```text
┌────────────────────────────────────────────────────────────────────────┐
│ 1. ANILLOS DE PROTECCIÓN Y KERNEL                                      │
│ Anillo 0 (Kernel & HAL) <──> Anillos 1/2 (Drivers/Servicios) <──> Anillo 3 (Apps/UI) │
└───────────────────────────────────┬────────────────────────────────────┘
                                    ▼
┌────────────────────────────────────────────────────────────────────────┐
│ 2. ARQUITECTURA DE KERNEL                                              │
│ Monolítico (Todo en Kernel, ultra rápido) vs Microkernel (Módulos aislados en Modo User) │
└───────────────────────────────────┬────────────────────────────────────┘
                                    ▼
┌────────────────────────────────────────────────────────────────────────┐
│ 3. FIRMWARE Y PARTICIONADO DE DISCO                                    │
│ BIOS Heredado + MBR (Máx 4 particiones primarias / Límite 2 TB)        │
│ UEFI Moderno  + GPT (Hasta 128 particiones primarias / Redundancia)    │
└───────────────────────────────────┬────────────────────────────────────┘
                                    ▼
┌────────────────────────────────────────────────────────────────────────┐
│ 4. ESTRUCTURA OBLIGATORIA GPT EN WINDOWS 10/11 (UEFI)                   │
│ [ 1. ESP (FAT32) ] ──> [ 2. MSR ] ──> [ 3. Windows (NTFS) ] ──> [ 4. Recovery ] │
└────────────────────────────────────────────────────────────────────────┘
```

---

### 🧱 Bloques Lógicos Funcionales

#### 1. Concepto y Arquitecturas de Kernel
* **Kernel (Núcleo):** Parte central del SO que ejecuta en Ring 0 (*Modo Protegido*) e interactúa con el hardware a través de la **HAL** (*Hardware Abstraction Layer*).
* **Modelos de Kernel:**
  * **Monolítico:** Todos los servicios (procesos, archivos, drivers) corren en el espacio del kernel. Máxima velocidad, pero un fallo en un driver provoca caída total (*Kernel Panic* / Pantalla Azul).
  * **Microkernel:** Mantiene en el núcleo solo lo mínimo vital (interrupciones, IPC). Drivers y sistemas de archivos corren en Modo Usuario (Ring 3), facilitando aislar fallos.
  * **Kernel Híbrido:** Estructura modular estilo microkernel pero ejecuta servicios clave en espacio de kernel por rendimiento (ej. Windows NT, macOS).

---

#### 2. Firmware y Particionado de Disco
* **BIOS Legacy vs UEFI Moderno:**
  * **BIOS:** Antiguo firmware de 16 bits. Lee el primer sector del disco (**MBR**).
  * **UEFI:** Firmware moderno modular de 32/64 bits. Soporta interfaz gráfica, ratón, *Secure Boot* y tablas **GPT**.
* **MBR vs GPT:**
  * **MBR (*Master Boot Record*):** Máximo 4 particiones primarias (o 3 primarias + 1 extendida). Límite de 2 TB por disco.
  * **GPT (*GUID Partition Table*):** Hasta 128 particiones primarias. Límite de 8 ZB. Mantiene copia de seguridad redundante al final del disco (*Header GPT secundario*).
* **Particiones Obligatorias Windows UEFI/GPT:**
  1. **ESP (*EFI System Partition*):** Formateada en **FAT32**, contiene los ejecutables EFI de arranque.
  2. **MSR (*Microsoft Reserved*):** Reservada para la gestión interna de metadatos GPT.
  3. **Partición de Windows:** Sistema y datos en NTFS.
  4. **Recovery:** Herramientas del entorno de recuperación (WinRE).

---

#### 3. Criterios de Selección e Instalación
* **TCO (*Total Cost of Ownership*):** Evaluación del coste total de propiedad (licencias, migración, formación y mantenimiento).
* **Requisitos Mínimos de Instalación:**
  * **Windows 10/11 (64 bits):** CPU 1 GHz (2+ núcleos), 4 GB RAM, 64 GB disco, UEFI + TPM 2.0.
  * **Debian GNU/Linux CLI (Consola):** CPU 1 GHz, 256 MB RAM, 2 GB disco.
  * **Debian GNU/Linux GUI (Escritorio):** CPU 1 GHz, 1 GB RAM, 10 GB disco.

---

#### 4. Automatización y Despliegue Desatendido
* **Instalación Desatendida:** Despliegue automatizado sin intervención humana mediante archivos de respuestas preconfigurados.
* **Herramientas Windows:** **Windows SIM** (*System Image Manager*) dentro de **Windows ADK** para generar archivos `autounattend.xml`.
* **Herramientas Linux:** Archivos `preseed.cfg` en Debian, **FAI** (*Fully Automatic Installation*) y **Kickstart** en derivados de Red Hat.

---

#### 5. Diagnóstico de Arranque y Almacenamiento en Windows
* **`msinfo32`:** Muestra la línea **Modo de BIOS** (**UEFI** vs **Heredado/Legacy**).
* **`diskmgmt.msc`:** Administrador de discos gráfico. Botón derecho en Disco $
ightarrow$ Propiedades $
ightarrow$ Volúmenes $
ightarrow$ Estilo de partición (**GPT** vs **MBR**).
* **`msconfig`:** Pestaña *Arranque* para gestionar visualmente sistemas de arranque múltiple respaldado por la base de datos **BCD** (*Boot Configuration Data*).
* **GRUB:** Gestor de arranque múltiple estándar en GNU/Linux (*Dual-Boot*).

---

### 📖 Glosario de Siglas — UT02

| Sigla | Nombre Completo en Inglés | Traducción / Función en 5 Palabras |
| :--- | :--- | :--- |
| **ESP** | *EFI System Partition* | Partición FAT32 con ejecutables EFI. |
| **MSR** | *Microsoft Reserved Partition* | Partición reservada metadatos GPT Windows. |
| **BCD** | *Boot Configuration Data* | Base de datos de opciones de arranque. |
| **HAL** | *Hardware Abstraction Layer* | Capa que aisla kernel del hardware. |
| **GPT** | *GUID Partition Table* | Tabla particiones UEFI hasta 128 primarias. |
| **MBR** | *Master Boot Record* | Registro de arranque clásico máx 4 primarias. |
| **SIM** | *System Image Manager* | Creador de archivos XML desatendidos. |
| **TCO** | *Total Cost of Ownership* | Coste total de propiedad del sistema. |
| **WinRE** | *Windows Recovery Environment* | Entorno de reparación de inicio Windows. |
| **GRUB** | *GRand Unified Bootloader* | Cargador de arranque múltiple en Linux. |

---

🏠 **[Volver al Índice Principal](../../README.md)** | 📖 **[Ir a la Guía Teórica (Resumen)](./RESUMEN_UT02_instalacion_sistemas_operativos.md)**
