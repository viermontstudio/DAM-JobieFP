🏠 **[Volver al Índice Principal](../../README.md)** | 📖 **[Ir a la Guía Teórica (Resumen)](./RESUMEN_UT01_explotacion_sistemas.md)**

---

---

# 🖥️ ESQUEMA DE ESTUDIO — UT01: Explotación de Sistemas Microinformáticos
**Asignatura:** Sistemas Informáticos (1º DAM/DAW)  
**Marco Metodológico:** Protocolo PEM-4 & Metodología Interna DAM

---

### 🗺️ El Gran Mapa Estructural: Componentes y Flujo de Trabajo

```text
┌────────────────────────────────────────────────────────────────────────┐
│ 1. TRÍPTICO FUNDAMENTAL                                                │
│ HARDWARE (Físico/Tangible) <──> SOFTWARE (Lógico/SO) <──> USUARIOS    │
└───────────────────────────────────┬────────────────────────────────────┘
                                    ▼
┌────────────────────────────────────────────────────────────────────────┐
│ 2. ARQUITECTURA DE COMPUTADORES (CPU Y BUSES)                           │
│ Von Neumann (Bus compartido: Datos + Instrucciones -> Cuello botella)   │
│ Harvard     (Buses separados: Procesa Datos e Instrucciones en paralelo)│
└───────────────────────────────────┬────────────────────────────────────┘
                                    ▼
┌────────────────────────────────────────────────────────────────────────┐
│ 3. JERARQUÍA DE MEMORIA (Velocidad vs Capacidad)                       │
│ Registros (CPU) -> Caché L1/L2/L3 (SRAM) -> RAM (DRAM) -> SSD/HDD      │
└───────────────────────────────────┬────────────────────────────────────┘
                                    ▼
┌────────────────────────────────────────────────────────────────────────┐
│ 4. SECUENCIA DE ARRANQUE Y DIAGNÓSTICO (POST)                           │
│ Alimentación (PSU 12V) -> BIOS/UEFI -> POST (Beep codes) -> Bootloader │
└────────────────────────────────────────────────────────────────────────┘
```

---

### 🧱 Bloques Lógicos Funcionales

#### 1. El Tríptico Fundamental y Funciones del Sistema Operativo
* **Tríptico:** Hardware (máquina), Software (instrucciones) y Usuarios (operadores). Ningún vértice funciona de forma aislada.
* **El Sistema Operativo (SO):** Director de orquesta que abstrae el hardware mediante APIs y administra 5 recursos críticos:
  1. **Gestión de Procesos:** Asigna tiempos de CPU y evita conflictos entre programas en ejecución.
  2. **Gestión de Memoria RAM:** Asigna espacio volátil dinámico a cada aplicación.
  3. **Gestión de Archivos:** Estructura de almacenamiento en disco.
  4. **Gestión de E/S:** Traduce órdenes bidireccionales mediante controladores (*drivers*).
  5. **Gestión de Seguridad:** Autentica usuarios y controla permisos de acceso.

---

#### 2. Arquitecturas de Computadores
* **Modelo Von Neumann:** Diseñado en los años 40. Usa **un único bus compartido** para datos e instrucciones. Genera el *Cuello de Botella de Von Neumann* al no poder leer datos e instrucciones simultáneamente.
* **Modelo Harvard:** Dispone de **buses y memorias físicas independientes** para datos e instrucciones, permitiendo procesamiento en paralelo.

---

#### 3. Componentes Hardware del Sistema
* **Microprocesador (CPU):**
  * **Unidad de Control (UC):** Coordina y dirige el flujo de instrucciones.
  * **Unidad Aritmético-Lógica (UAL):** Realiza operaciones matemáticas y comparaciones lógicas.
  * **Registros:** Memorias temporales ultrarrápidas de 32 o 64 bits dentro del chip.
  * **TDP (*Thermal Design Power*):** Potencia de diseño térmico en vatios (W) que el sistema de refrigeración debe disipar.
* **Memoria Principal (RAM):**
  * **Volátil:** Pierde la información al cortar la corriente eléctrica.
  * **Módulos:** **DIMM** (sobremesa) y **SO-DIMM** (portátiles/mini-PCs).
  * **Latencia (CL):** Ciclos de reloj de retardo; a menor latencia, mejor rendimiento.
* **Placa Base (*Motherboard*):**
  * **Chipset:** Centro de control de tráfico que conecta CPU, RAM, buses PCIe y puertos E/S.
  * **Socket (Zócalo):** Matriz de contactos (**LGA** con pines en placa / **PGA** con pines en CPU).
  * **Batería RTC (Pila CR2032):** Mantiene la hora del sistema y la configuración CMOS al apagar la corriente.

---

#### 4. Proceso de Arranque y Diagnóstico POST
* **Secuencia de Boot:** Encendido de la PSU (+12V para CPU/GPU) $
ightarrow$ Carga de firmware BIOS/UEFI $
ightarrow$ Test de autocomprobación **POST** (*Power-On Self-Test*) $
ightarrow$ Búsqueda de dispositivo en la **Boot Sequence** $
ightarrow$ Transferencia al *Bootloader*.
* **Diagnóstico de Pitidos (*Beep Codes*):** 
  * **3 pitidos cortos continuos:** Fallo de lectura/escritura en la memoria RAM.
  * **Solución de soporte:** Procedimiento de *reseat* (extraer, limpiar contactos dorados y reinsertar módulos en la ranura DIMM).

---

#### 5. Virtualización y Entornos de Pruebas
* **Hipervisores:**
  * **Tipo 1 (*Bare Metal*):** Corre directamente sobre el hardware (KVM, Xen, Hyper-V Server).
  * **Tipo 2 (*Hosted*):** Corre como aplicación sobre un SO anfitrión (VirtualBox, VMware Workstation).
* **Conceptos Clave:**
  * **Anfitrión (*Host*):** PC físico real.
  * **Invitado (*Guest*):** Máquina virtual aislada.
  * **Instantáneas (*Snapshots*):** Fotografía del estado exacto de la VM para revertir cambios tras pruebas de riesgo.
  * **Regla de la RAM:** Nunca asignar a las VMs más del 50% de la RAM física real del Host.

---

### 📖 Glosario de Siglas — UT01

| Sigla | Nombre Completo en Inglés | Traducción / Función en 5 Palabras |
| :--- | :--- | :--- |
| **CPU** | *Central Processing Unit* | Procesador central del sistema informático. |
| **TDP** | *Thermal Design Power* | Calor máximo en vatios a disipar. |
| **POST** | *Power-On Self-Test* | Autocomprobación hardware inicial del arranque. |
| **RTC** | *Real-Time Clock* | Reloj interno alimentado por pila CR2032. |
| **DCH** | *Declarative Componentized Hardware* | Estándar oficial moderno de drivers Windows. |
| **API** | *Application Programming Interface* | Funciones del SO para las aplicaciones. |
| **DIMM** | *Dual In-line Memory Module* | Módulo de RAM para PCs sobremesa. |
| **SO-DIMM** | *Small Outline DIMM* | Módulo compacto RAM para portátiles. |
| **SSD** | *Solid State Drive* | Almacenamiento rápido en memoria flash NAND. |
| **GPU** | *Graphics Processing Unit* | Procesador gráfico y cómputo masivo. |

---

🏠 **[Volver al Índice Principal](../../README.md)** | 📖 **[Ir a la Guía Teórica (Resumen)](./RESUMEN_UT01_explotacion_sistemas.md)**
