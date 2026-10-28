🏠 **[Volver al Índice Principal](../../README.md)** | 📐 **[Ir al Esquema Resumen](./ESQUEMA_UT03_gestion_informacion.md)**

---

# 📁 GUÍA TEÓRICA Y RESUMEN — UT03: Gestión de la Información
**Asignatura:** Sistemas Informáticos (1º DAM/DAW)  
**Marco Metodológico:** Protocolo PEM-4 & Metodología Interna DAM

---

## 1. Concepto de Archivo, Directorio y Enlaces
* **Archivo (Fichero):** Colección organizada de información o datos estructurados almacenados de forma permanente en un medio secundario.
* **Directorio (Carpeta):** Fichero especial que contiene un índice de entradas que apuntan a otros ficheros o subdirectorios.
* **Enlaces en Linux:**
  * **Enlace Físico (*Hard Link*):** Apunta directamente al mismo número de inodo en el disco. No puede cruzar distintos sistemas de archivos ni apuntar a directorios. Si se borra el archivo original, los datos permanecen intactos mientras quede algún enlace físico.
  * **Enlace Simbólico (*Soft/Symbolic Link* - `ln -s`):** Fichero independiente que contiene la ruta de texto hacia otro archivo o directorio. Si se borra el archivo de origen, el enlace queda roto ("huérfano").

---

## 2. Sistemas de Archivos
* **FAT32:** Compatible con casi todos los S.O. Sin permisos de seguridad ACL ni journaling. Limite máximo de archivo: **4 GB**.
* **exFAT:** Evolución de FAT optimizada para memorias flash y discos externos; elimina la limitación de 4 GB por archivo.
* **NTFS (Windows):** Sistema de archivos transaccional con **Journaling** (registro de cambios para recuperación rápida tras fallos), soporte de permisos ACL (*Access Control Lists*), cifrado EFS y compresión nativa.
* **ext4 (Linux):** Sistema de archivos basado en **inodos**, journaling, asignación diferida de bloques (*extents*) y soporte para ficheros y volúmenes gigantescos.

---

## 3. Jerarquía de Directorios en Linux (Estándar FHS)
El *Filesystem Hierarchy Standard* (FHS) define la estructura unificada en Linux comenzando desde la raíz `/`:
* `/` : Raíz del árbol de directorios.
* `/bin` y `/sbin` : Binarios esenciales del sistema para todos los usuarios (`/bin`) y para administración (`/sbin`).
* `/etc` : Archivos de configuración plana del sistema y servicios.
* `/dev` : Archivos especiales de dispositivos de hardware (ej. `/dev/sda`, `/dev/nvme0n1`).
* `/var` : Datos variables (archivos de log `/var/log`, colas de impresión, bases de datos).
* `/home` : Directorios personales de los usuarios normales (ej. `/home/usuario`).
* `/root` : Directorio personal del superusuario `root`.
* `/tmp` : Archivos temporales borrados habitualmente al reiniciar.
* `/mnt` y `/media` : Puntos de montaje temporales (`/mnt`) o automáticos de medios extraíbles (`/media`).
* `/proc` y `/sys` : Sistemas de archivos virtuales que reflejan el estado del kernel y los procesos en tiempo real.

---

## 4. Comandos CLI de Manipulación y Búsqueda de Texto
* **Navegación y Archivos:** `ls -lth` (listar con detalles, archivos ocultos y orden cronológico), `cp -r` (copia recursiva), `mv` (mover/renombrar), `rm -rf` (eliminación recursiva forzada), `mkdir -p` (crear ruta de directorios).
* **Visualización y Procesamiento:**
  * `cat` / `less` : Mostrar contenido de archivos de forma continua o paginada.
  * `head -n X` / `tail -n X` : Mostrar las primeras o últimas X líneas de un archivo (útil `tail -f` para monitorizar logs en vivo).
  * `grep -i "patron" archivo` : Filtrar líneas que coinciden con una expresión o patrón (-i ignora mayúsculas/minúsculas, -r recursivo).
  * `find /ruta -name "*.txt"` : Buscar archivos en el disco según criterios de nombre, tamaño o permisos.
  * `cut -d':' -f1 /etc/passwd` : Extraer campos delimitados de un texto.
  * `sort` / `uniq` : Ordenar líneas y eliminar duplicados consecutivos.
  * `wc -l` : Contar líneas, palabras o caracteres.
  * `tee` : Leer de la entrada estándar y escribir simultáneamente en la salida estándar y en un archivo.

---

## 5. Redirecciones y Tuberías (*Pipes*)
* `>` : Redirige la salida estándar (STDOUT) a un archivo, **sobrescribiendo** su contenido.
* `>>` : Redirige la salida estándar a un archivo, **añadiendo** al final (*append*).
* `2>` : Redirige la salida de errores estándar (STDERR).
* `|` (Tubería / *Pipe*) : Conecta la salida estándar de un comando con la entrada estándar del siguiente comando (ej. `cat /etc/passwd | grep bash | cut -d':' -f1`).

---

## 6. Almacenamiento, Particionado, Formateo y Montaje
1. **Particionado:** Creación de la estructura de tablas mediante `fdisk` o `gparted` (ej. `/dev/sdb1`).
2. **Formateo:** Creación del sistema de archivos mediante `mkfs` (ej. `mkfs.ext4 /dev/sdb1` o `mkfs.ntfs /dev/sdb1`).
3. **Montaje:** Asociación de una partición a una carpeta del árbol de directorios mediante `mount /dev/sdb1 /mnt/disco`.
4. **Montaje Automático:** Configuración en el archivo `/etc/fstab` especificando UUID de la partición, punto de montaje, sistema de archivos, opciones y valores de comprobación.

---

## 7. Tolerancia a Fallos y Redundancia (RAID)
* **RAID 0 (*Data Striping*):** Distribución de datos en bloques entre 2 o más discos. **Sin redundancia**. Máxima velocidad de lectura/escritura. Si falla 1 disco, se pierde toda la información.
* **RAID 1 (*Data Mirroring*):** Espejo idéntico entre 2 discos. **Alta redundancia**. Si falla un disco, el sistema sigue funcionando sin interrupción. Capacidad útil = 50% del total.
* **RAID 5 (*Block-Level Striping with Distributed Parity*):** Distribución de datos y bloques de paridad entre un mínimo de **3 discos**. Tolera el fallo de **1 disco simultáneo**. Capacidad útil = \((N-1) \times \text{Capacidad}\).

---

🏠 **[Volver al Índice Principal](../../README.md)** | 📐 **[Ir al Esquema Resumen](./ESQUEMA_UT03_gestion_informacion.md)**
