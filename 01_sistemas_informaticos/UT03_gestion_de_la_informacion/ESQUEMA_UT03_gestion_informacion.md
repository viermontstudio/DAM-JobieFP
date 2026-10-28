🏠 **[Volver al Índice Principal](../../README.md)** | 📖 **[Ir a la Guía Teórica (Resumen)](./RESUMEN_UT03_gestion_informacion.md)**

---

---

# 📁 ESQUEMA DE ESTUDIO — UT03: Gestión de la Información
**Asignatura:** Sistemas Informáticos (1º DAM/DAW)  
**Marco Metodológico:** Protocolo PEM-4 & Metodología Interna DAM

---

### 🗺️ El Gran Mapa Estructural: Árbol FHS y Sistemas de Archivos

```text
┌────────────────────────────────────────────────────────────────────────┐
│ 1. SISTEMAS DE ARCHIVOS Y COMPATIBILIDAD                               │
│ FAT32 (Límite 4 GB/archivo) | exFAT (Multiplataforma 4K)               │
│ NTFS  (Windows: ACLs, Journaling, EFS) | ext4 (Linux: Extents, 16 TB/1 EB)│
└───────────────────────────────────┬────────────────────────────────────┘
                                    ▼
┌────────────────────────────────────────────────────────────────────────┐
│ 2. ESTRUCTURA FHS DE LINUX (Filesystem Hierarchy Standard)             │
│ / (Raíz / Root)                                                         │
│ ├── /bin (Binaries)  ├── /etc (Config global) ├── /home (Usuarios)      │
│ ├── /dev (Devices)   ├── /var (Logs/Variable) ├── /usr (Resources)      │
└───────────────────────────────────┬────────────────────────────────────┘
                                    ▼
┌────────────────────────────────────────────────────────────────────────┐
│ 3. FLUJO DE TRABAJO DE ALMACENAMIENTO EN LINUX                         │
│ Disco Físico (/dev/sdb) ──> Particionar (fdisk) ──> Formatear (mkfs) ──> Montar (mount) │
└───────────────────────────────────┬────────────────────────────────────┘
                                    ▼
┌────────────────────────────────────────────────────────────────────────┐
│ 4. NIVELES DE RAID (Redundancia y Velocidad)                            │
│ RAID 0 (Striping) -> Velocidad pura (Sin tolerancia a fallos)          │
│ RAID 1 (Mirroring)-> Espejo 50% capacidad (1 fallo tolerado)            │
│ RAID 5 (Paridad)   -> Paridad distribuida (Mín 3 discos / 1 fallo)     │
└────────────────────────────────────────────────────────────────────────┘
```

---

### 🧱 Bloques Lógicos Funcionales

#### 1. Comparativa de Sistemas de Archivos
* **FAT32:** Compatible con todo pero con **límite de 4 GB por archivo** e inútil para permisos.
* **exFAT:** Evolución de FAT. Estándar *de facto* para pendrives y SDs compartidas entre Windows y Mac sin límite de 4 GB.
* **NTFS:** Nativo de Windows. Incluye **Journaling** (diario de transacciones anti-corrupción), **ACLs** (permisos por usuario) y cifrado **EFS**.
* **ext4:** Nativo de Linux. Usa **extents** (asignación de bloques contiguos) que eliminan casi toda la fragmentación. Admite archivos de hasta 16 TB y volúmenes de 1 EB.

---

#### 2. Estructura FHS de Linux y Directorios Críticos
* **/ (Raíz):** Origen del árbol único de directorios.
* **/bin** (*Binaries*): Ejecutables fundamentales para todos los usuarios (`ls`, `cp`, `cat`).
* **/etc** (*Editable Text Configuration*): Archivos de configuración global del sistema y servicios.
* **/dev** (*Devices*): Archivos especiales que representan dispositivos físicos (`sda`, `sdb`, `null`).
* **/home**: Carpetas personales de usuarios estándar (`/home/usuario`).
* **/var** (*Variable*): Archivos de contenido dinámico y logs (`/var/log/syslog`).
* **/tmp** (*Temporary*): Archivos temporales borrados al reiniciar.

---

#### 3. Comandos CLI Esenciales de Manipulación y Búsqueda
* **Listado y Navegación:**
  * `ls -lth`: Formato largo (**L**ong), ordenado por fecha (**T**ime) y tamaño legible (**H**uman-readable).
  * `mkdir -p dir1/dir2`: Crea la ruta completa de subcarpetas (**P**arents).
  * `pwd` (*Print Working Directory*): Muestra la ruta absoluta actual.
* **Procesamiento de Texto y Filtros:**
  * `cut -d: -f1,3 /etc/passwd`: Recorta campos especificando delimitador (**D**elimiter) y columnas (**F**ields).
  * `grep -i -v "error"`: Busca texto ignorando mayúsculas (**I**gnore-case) e invirtiendo la búsqueda (**V**ert-match).
  * `more` / `less` / `tee`: `tee` permite enviar la salida a la pantalla y guardarla en archivo simultáneamente.
* **Búsqueda en Disco:**
  * `find /ruta -name "*.pdf" -mtime -2`: Busca archivos en tiempo real por nombre y fecha de modificación.
  * `find /var/www -type d -maxdepth 1`: Busca exclusivamente directorios (**T**ype d) limitando la profundidad a 1 nivel.
  * `locate` / `updatedb`: Búsqueda instantánea indexada en base de datos.

---

#### 4. Particionado, Formateo y Montaje
* **Identificación de Dispositivos:** Discos SATA/SSD como `/dev/sda`, `/dev/sdb`; unidades NVMe como `/dev/nvme0n1`.
* **Particionado interactivo:** `sudo fdisk /dev/sdb`
  * `p` (*Print*), `n` (*New*), `t` (*Type*), `w` (*Write* - guarda cambios permanentemente en disco).
* **Formateo:** `sudo mkfs -t ext4 /dev/sdb1` (Aplica sistema de archivos `ext4`).
* **Montaje:** `sudo mount /dev/sdb1 /mnt/disco` | Desmontaje seguro: `sudo umount /mnt/disco` (*atención: sin 'o'*).
* **Montaje Permanente:** `mount -a` lee el fichero `/etc/fstab` y monta todas las unidades declaradas.
* **Reparación:** `sudo fsck /dev/sdb1` (*File System Check* - reparar siempre desmontado).

---

#### 5. Almacenamiento Redundante (RAID)
* **RAID 0 (*Striping*):** Fragmentación de datos entre 2+ discos. Velocidad máxima, 0 redundancia (si falla 1 disco, se pierde todo).
* **RAID 1 (*Mirroring*):** Espejo idéntico entre 2 discos. Tolerancia a 1 fallo, capacidad útil del 50%.
* **RAID 5 (Paridad Distribuida):** Requiere **mínimo 3 discos**. Tolera el fallo de 1 disco calculando paridad de bloques.
* **Regla de Oro:** Un RAID **NO** sustituye a una copia de seguridad (*backup*).

---

### 📖 Glosario de Siglas — UT03

| Sigla | Nombre Completo en Inglés | Traducción / Función en 5 Palabras |
| :--- | :--- | :--- |
| **FHS** | *Filesystem Hierarchy Standard* | Estándar de árbol directorios Linux. |
| **FAT32** | *File Allocation Table 32-bit* | Formato antiguo máx 4GB por archivo. |
| **exFAT** | *Extended File Allocation Table* | Formato SD/USB libre de 4GB multiplataforma. |
| **NTFS** | *New Technology File System* | Formato nativo Windows con ACLs y Journaling. |
| **ext4** | *Fourth Extended Filesystem* | Formato nativo Linux con extents y 16TB. |
| **ACL** | *Access Control List* | Permisos de seguridad detallados por usuario. |
| **RAID** | *Redundant Array of Independent Disks* | Matriz redundante de discos para velocidad/fallos. |
| **NVMe** | *Non-Volatile Memory Express* | Interfaz ultrarrápida SSD PCIe. |
| **VDI** | *VirtualBox Disk Image* | Disco duro virtual dinámico VirtualBox. |

---

🏠 **[Volver al Índice Principal](../../README.md)** | 📖 **[Ir a la Guía Teórica (Resumen)](./RESUMEN_UT03_gestion_informacion.md)**
