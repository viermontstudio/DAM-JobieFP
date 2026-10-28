🏠 **[Volver al Índice Principal](../../README.md)** | 📐 **[Ir al Esquema Resumen](./ESQUEMA_UT01_explotacion_sistemas.md)**

---

# 🖥️ GUÍA TEÓRICA Y RESUMEN — UT01: Explotación de Sistemas Microinformáticos
**Asignatura:** Sistemas Informáticos (1º DAM/DAW)  
**Marco Metodológico:** Protocolo PEM-4 & Metodología Interna DAM

---

## 1. El Tríptico Fundamental de un Sistema Informático
Un sistema informático es el conjunto integrado de elementos físicos, lógicos y humanos orientados al tratamiento automático de la información:
* **Hardware:** La arquitectura física e intangible de componentes electrónicos, circuitos y periféricos.
* **Software:** El soporte lógico intangible (sistemas operativos, firmware, aplicaciones y utilidades).
* **Humanware:** Los usuarios, administradores y desarrolladores que interactúan con el sistema.

---

## 2. Arquitectura de Ordenadores: Von Neumann vs. Harvard
* **Modelo Von Neumann:** Estructura clásica donde **datos e instrucciones comparten la misma memoria principal** y los mismos buses del sistema. Consta de:
  * **Unidad Central de Proceso (CPU):** Formada por la **ALU** (*Arithmetic Logic Unit* - cálculos matemáticos y lógicos), la **UC** (*Control Unit* - decodificación de instrucciones y sincronización) y los **Registros** (celdas de memoria de ultra-alta velocidad para operandos inmediatos).
  * **Memoria Principal (RAM):** Almacena programas y datos en ejecución.
  * **Buses de Comunicación:** Bus de Datos (bidireccional), Bus de Direcciones (unidireccional) y Bus de Control.
* **Modelo Harvard:** Separa físicamente la memoria de código/instrucciones de la memoria de datos, permitiendo accesos simultáneos (utilizado en procesadores modernos a nivel de caché L1).

---

## 3. Parámetros Técnicos del Procesador (CPU)
* **Núcleos y Hilos:** Núcleos físicos independientes (*Cores*) y tecnología de multihilo simétrico (*Hyper-Threading* / SMT) para ejecutar múltiples hilos lógicos por núcleo.
* **Frecuencia de Reloj:** Medida en Gigahertzios (GHz); velocidad base y frecuencia Turbo/Boost.
* **Memoria Caché:** Jerarquía L1 (ultra-rápida, dividida en datos/instrucciones), L2 (por núcleo) y L3 (compartida entre todos los núcleos).
* **TDP (*Thermal Design Power*):** Potencia de diseño térmico expresada en vatios (W), indicando la cantidad de calor que el sistema de refrigeración debe disipar.
* **Sockets de CPU:**
  * **LGA (*Land Grid Array*):** Los pines están integrados en el zócalo de la placa base (estándar Intel y AMD moderno).
  * **PGA (*Pin Grid Array*):** Los pines sobresalen de la parte inferior de la CPU.

---

## 4. Jerarquía de Memorias
El equilibrio del sistema se basa en la velocidad, capacidad y coste por bit:
1. **Registros de la CPU:** Velocidad máxima (sub-nanosegundo), capacidad extremadamente reducida (Bytes/KB).
2. **Caché (L1, L2, L3):** Memoria SRAM estática, integrada en el encapsulado del procesador.
3. **Memoria Principal (RAM):** DRAM dinámica volátil (DDR4 / DDR5) con tecnología *Dual-Channel* para duplicar el ancho de banda.
4. **Memoria No Volátil (Firmware):** ROM, PROM, EPROM y Flash (donde reside la BIOS/UEFI).
5. **Almacenamiento Secundario:** Unidades de Estado Sólido (SSD NVMe PCIe / SATA) y Discos Duros Mecánicos (HDD SATA).

---

## 5. Placa Base, Chipset y Buses de Expansión
* **Placa Base (Motherboard):** El circuito impreso principal que interconecta todos los componentes.
* **Chipset:**
  * **Northbridge (Puente Norte):** Historicamente gestionaba la comunicación rápida entre CPU, RAM y tarjeta gráfica (actualmente integrado en la propia CPU).
  * **Southbridge (Puente Sur / PCH):** Controla periféricos lentos, discos SATA, puertos USB, audio y red.
* **Buses de Expansión:** Ranuras **PCIe (*PCI Express*)** x1, x4, x8, x16 y conectores **M.2 NVMe** para almacenamiento de alta velocidad.

---

## 6. Controladores (Drivers) y Periféricos
* **Periféricos de Entrada:** Teclado, ratón, escáner, micrófonos.
* **Periféricos de Salida:** Monitores, impresoras, altavoces.
* **Periféricos de Almacenamiento y Comunicaciones:** Unidades externas, tarjetas de red Ethernet/Wi-Fi.
* **Controladores (*Drivers*):** Módulos de software específicos del sistema operativo que traducen las órdenes genéricas del S.O. a instrucciones comprensibles por el hardware específico.

---

## 7. Secuencia de Arranque, Firmware y Diagnóstico
* **BIOS (*Basic Input/Output System*):** Firmware tradicional almacenado en chip Flash ROM con limitación de particiones MBR (máx 2TB).
* **UEFI (*Unified Extensible Firmware Interface*):** Sustituto moderno de BIOS; soporta discos GPT (>2TB), interfaz gráfica, arranque seguro (*Secure Boot*) y ejecución en 32/64 bits.
* **Secuencia POST (*Power-On Self-Test*):** Comprobación inicial de hardware al encender la máquina.
  * **Beep Codes (Códigos de pitidos):** Diagnosticador acústico de fallos graves cuando la gráfica no puede inicializarse (e.g., pitidos continuos indica fallo en la RAM o gráfica).

---

## 8. Virtualización Básica
* **Hipervisor Tipo 1 (Bare-Metal):** Se ejecuta directamente sobre el hardware (ej. VMware ESXi, Proxmox VE).
* **Hipervisor Tipo 2 (Hosted):** Se ejecuta sobre un sistema operativo anfitrión (ej. VirtualBox, VMware Workstation). Permite aislar entornos de pruebas y desarrollar aplicaciones de forma segura.

---

## 9. Ergonomía, Prevención de Riesgos Laborales y Medio Ambiente
* **Ergonomía:** Posición de la pantalla a la altura de los ojos (40-75 cm), ángulo de codos a 90°, reposapiés y sillas regulables.
* **Normativa Medioambiental:** Cumplimiento de la directiva **RoHS** (restricción de sustancias peligrosas) y certificación **ISO 14001** para el reciclaje de residuos informáticos (*e-waste*).

---

🏠 **[Volver al Índice Principal](../../README.md)** | 📐 **[Ir al Esquema Resumen](./ESQUEMA_UT01_explotacion_sistemas.md)**
