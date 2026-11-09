🏠 **[Volver al Índice Principal](../../README.md)** | 📖 **[Ir a la Guía Teórica (Resumen)](./RESUMEN-UT07-explotacion-aplicaciones.md)**

---

# ⚙️ UT07 — Explotación de Aplicaciones Informáticas de Propósito General
## 📖 Esquema Maestro Integrado de Estudio

> **Asignatura:** Sistemas Informáticos (1º DAM/DAW)  
> **Marco Metodológico:** Protocolo PEM-4 & Metodología Interna DAM  

---

## 🗺️ 1. Mapa Arquitectónico Visual (Clonación de Sistemas & Requisitos)

```text
┌────────────────────────────────────────────────────────────────────────────────┐
│ 1. PREPARACIÓN MEDIA: Rufus (ISO Clonezilla -> USB Booteable GPT / UEFI)       │
└────────────────────────────────────────────────────────────────────────────────┘
                                         ▼
┌────────────────────────────────────────────────────────────────────────────────┐
│ 2. AJUSTE FIRMWARE: Desactivar Secure Boot / Fast Startup (shutdown /r /fw /t 0)│
└────────────────────────────────────────────────────────────────────────────────┘
                                         ▼
┌────────────────────────────────────────────────────────────────────────────────┐
│ 3. SISTEMA PARADO: Arrancar medio USB externo (Disco Origen Inactivo)          │
└────────────────────────────────────────────────────────────────────────────────┘
                                         ▼
┌────────────────────────────────────────────────────────────────────────────────┐
│ 4. SELECCIÓN DISCOS: Clonezilla device-device (sda: Origen -> sdb: Destino)     │
└────────────────────────────────────────────────────────────────────────────────┘
                                         ▼
┌────────────────────────────────────────────────────────────────────────────────┐
│ 5. REPLICACIÓN & SUSTITUCIÓN: Copia sector a sector y ajuste proporcional      │
└────────────────────────────────────────────────────────────────────────────────┘
```

---

## 🧱 2. Desglose Estructurado por Bloques Lógicos

### 📜 1. Clasificación del Software y Licenciamiento

| Tipo de Licencia | Código Fuente | Modificación / Redistribución | Rederivación / Integración | Ejemplo Típico |
| :--- | :--- | :--- | :--- | :--- |
| **Propietaria / Comercial** | Cerrado / Privado | Prohibida sin pago/autorización | Restringida (Pago de licencias) | Windows, MS Office |
| **Copyleft (GPL)** | Abierto (Público) | Permitida libremente | **Obligatoria GPL** (Hereditaria) | Linux Kernel, GNU Tools |
| **Permisiva (MIT / Apache)** | Abierto (Público) | Permitida libremente | **Libre** (Permite código propietario) | React, VS Code Core |
| **Creative Commons (CC)** | N/A (Contenidos) | Según módulos (BY, NC, ND, SA) | Según cláusula de módulo | Fotos, Música, Textos |

* **Diferenciador Clave:**
  * **GPL (Copyleft estricto):** Exige que cualquier trabajo derivado mantenga la misma licencia libre GPL (*efecto viral*).
  * **MIT (Permisiva):** Permite reutilizar el código fuente dentro de software comercial cerrado sin liberar el código fuente modificado.

---

### 💾 2. Herramientas de Desarrollo y Requisitos de Hardware

* **Requisitos del Sistema:**
  * **Mínimos de supervivencia:** CPU básica, 4 GB RAM, almacenamiento estándar.
  * **Recomendados profesional (DevOps / IA):** CPU multi-núcleo, **16 GB a 32 GB RAM**, SSD NVMe.
* **Ecosistema de Aplicaciones de Desarrollo:**
  * **Entornos & Editores:** Visual Studio Code, IntelliJ IDEA, Eclipse.
  * **Contenedores & Orquestación:** **Docker** (empaquetado de apps con dependencias) y **Kubernetes** (orquestación).
  * **Clientes de API & BD:** **Postman** (pruebas HTTP/REST), **DBeaver** / **pgAdmin** / **MySQL Workbench** (gestión de datos).

---

### 🌐 3. Servicios de Internet, Correo y Transferencia

* **Correo Electrónico Corporativo:**
  * **SMTP Autenticado:** Envío automatizado de notificaciones (puertos 587/465 con cifrado TLS/SSL).
  * **Seguridad Antisuplantación DNS:**
    * **SPF (*Sender Policy Framework*):** Publica IPs autorizadas para emitir correo del dominio.
    * **DKIM (*DomainKeys Identified Mail*):** Firma digitalmente el mensaje para evitar alteración.
    * **DMARC:** Define la política de validación conjunta SPF/DKIM y emite reportes de fallos.
* **Transferencia de Archivos:**
  * **FTP (Puerto 21/TCP):** Texto plano (inseguro).
  * **SFTP (Puerto 22/TCP):** Transferencia cifrada sobre SSH.
  * **Almacenamiento en Nube:** AWS S3, Azure Blob Storage (repositorios de objetos).

---

### 💿 4. Procedimiento de Clonación de Sistemas (Clonezilla & Rufus)

1. **Preparación del USB de Arranque:**
   * Utilizar **Rufus** para grabar la imagen ISO de **Clonezilla**.
   * Seleccionar esquema de particionado **GPT** y sistema de destino **UEFI**.
2. **Configuración del Firmware BIOS/UEFI:**
   * Desactivar **Secure Boot** y **Fast Startup / Fast Boot** en Windows.
   * Ejecutar en consola Windows como Administrador: `shutdown /r /fw /t 0` para forzar reinicio directo al firmware UEFI.
3. **Arranque en Estado Parado:**
   * Iniciar la máquina desde la unidad USB externa.
   * **Regla de Oro:** El disco de origen debe estar completamente inactivo (sistema operativo desmontado) para evitar archivos bloqueados.
4. **Ejecución en Clonezilla (`device-device`):**
   * Seleccionar el modo `disk_to_local_disk`.
   * **Identificación Unix:** Identificar origen (`sda` - disco antiguo) y destino (`sdb` - disco nuevo).
   * **¡Atención!** Verificar las capacidades antes de confirmar para evitar sobrescribir el disco de origen.
5. **Reconstrucción y Sustitución:**
   * Seleccionar ajuste proporcional de particiones para aprovechar el espacio extra si el disco destino es mayor.
   * Apagar el equipo, sustituir físicamente el disco e iniciar el sistema clonado.

---

### 🛡️ 5. Estrategias de Backup, Restauración y Seguridad

* **Matriz Comparativa de Copias de Seguridad:**

| Tipo de Backup | Datos Copiados | Marcador de Archivo (Flag) | Tiempo de Copia | Tiempo de Restauración |
| :--- | :--- | :--- | :--- | :--- |
| **Completo (Full)** | 100% de la información | Se activa / marca | Largo | **Mínimo** (1 sola copia) |
| **Incremental** | Solo cambios desde última copia (Full o Inc) | Se limpia / desactiva | **Mínimo** | Largo (Full + **todas** las incrementales) |
| **Diferencial** | Cambios acumulados desde última copia Full | No se modifica | Medio | Medio (Full + **última** diferencial) |

* **Secuencia de Restauración:**
  * **Incremental:** `[Backup Completo]` → `[Inc 1]` → `[Inc 2]` → ... → `[Inc N]` (Orden cronológico estricto).
  * **Diferencial:** `[Backup Completo]` → `[Última Diferencial]` (Solo requiere 2 archivos).
* **Métricas de Recuperación y Reglas:**
  * **Regla 3-2-1:** 3 copias de seguridad, 2 soportes distintos, 1 copia fuera del centro (*offsite* / nube).
  * **RTO (*Recovery Time Objective*):** Tiempo máximo aceptable de inactividad del servicio.
  * **RPO (*Recovery Point Objective*):** Cantidad máxima aceptable de pérdida de datos medida en tiempo.

---

## 📚 6. Glosario Mnemotécnico de Siglas — UT07

| Sigla | Nombre Completo en Inglés | Traducción al Español | Función Clave |
| :--- | :--- | :--- | :--- |
| **GPL** | *General Public License* | Licencia Pública General | Licencia copyleft obligatoria de rederivación libre |
| **MIT** | *Massachusetts Institute of Technology* | Licencia MIT | Licencia libre permisiva para integración comercial |
| **SCA** | *Software Composition Analysis* | Análisis de Composición de Software | Detecta vulnerabilidades en librerías y dependencias |
| **SFTP** | *SSH File Transfer Protocol* | Protocolo de Transferencia Segura SSH | Transferencia de archivos cifrada sobre puerto 22 |
| **SMTP** | *Simple Mail Transfer Protocol* | Protocolo de Transferencia Simple de Correo | Envío automatizado de correos salientes |
| **SPF** | *Sender Policy Framework* | Convenio de Emisores del Sender | Registro DNS que valida servidores de correo autorizados |
| **DKIM** | *DomainKeys Identified Mail* | Correo Identificado por Claves de Dominio | Firma digital en cabeceras para prevenir alteración |
| **DMARC** | *Domain-based Message Authentication* | Autenticación de Mensajes por Dominio | Política DNS de reporte y cumplimiento SPF/DKIM |
| **RTO** | *Recovery Time Objective* | Objetivo de Tiempo de Recuperación | Tiempo máximo aceptable de parada del servicio |
| **RPO** | *Recovery Point Objective* | Objetivo de Punto de Recuperación | Pérdida máxima aceptable de datos medida en tiempo |
| **FHS** | *Filesystem Hierarchy Standard* | Estándar de Jerarquía del Sistema de Archivos | Estructura estándar de directorios en Linux |

---

🏠 **[Volver al Índice Principal](../../README.md)** | 📖 **[Ir a la Guía Teórica (Resumen)](./RESUMEN-UT07-explotacion-aplicaciones.md)**
