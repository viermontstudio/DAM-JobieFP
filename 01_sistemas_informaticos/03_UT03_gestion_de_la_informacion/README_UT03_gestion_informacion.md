# 📁 UT03 — Gestión de la Información

## 1. Introducción y Concepto de Gestión de la Información [Concepto]

* **Gestión de la Información [Concepto]:** Conjunto de estructuras, normas, herramientas y procedimientos mediante los cuales un sistema operativo organiza, almacena, procesa, protege y recupera los datos contenidos en dispositivos de almacenamiento físico o virtual.
* **El Recurso Crítico Organizacional [Concepto]:** En cualquier entidad o empresa, la información (documentos, bases de datos, archivos de configuración, registros del sistema) constituye el activo más valioso. La eficiencia de un administrador de sistemas se mide por la velocidad de acceso, la integridad de los datos y la resiliencia ante fallos.
* **Principios de Rendimiento y Organización [Técnica]:**
  * Un equipo con hardware de alto rendimiento (CPU avanzada, gran cantidad de RAM) se vuelve ineficiente si el sistema de archivos está fragmentado, corrupto o mal estructurado.
  * La gestión de almacenamiento combina dos capas complementarias: la **Capa Lógica** (directorios, permisos, rutas) y la **Capa Física** (bloques de disco, sectores, particiones y arrays redundantes).

---

## 2. Sistemas de Archivos (File Systems) [Concepto]

* **Sistema de Archivos [Concepto]:** Estructura lógica y conjunto de algoritmos mediante los cuales el sistema operativo asigna espacio en los dispositivos de almacenamiento, gestiona la tabla de contenido, controla los permisos de acceso y organiza los datos en archivos y carpetas.
* **Analogía de la Estantería Inteligente [Concepto]:** Si el disco físico es un almacén vacío, el sistema de archivos es el sistema de estanterías etiquetadas, el índice de localización y el libro de registro que indica dónde empieza y termina exactamente cada documento.

### 2.1. FAT y FAT32 (File Allocation Table) [Concepto]
* **FAT / FAT32 [Técnica]:** Sistema de archivos desarrollado originalmente por Microsoft basado en una tabla de asignación de archivos (*File Allocation Table*) que vincula clústeres contiguos o dispersos.
  * **Características:** Simplicidad extrema y compatibilidad universal (televisores, consolas, equipos antiguos, sistemas embebidos).
  * **Limitaciones Críticas de FAT32:** 
    * Tamaño máximo por archivo individual: **4 GB** (32 bits de direccionamiento).
    * Tamaño máximo de partición/volumen: **2 TB**.
    * Cero soporte nativo para permisos de seguridad a nivel de archivo (ACL), cifrado o compresión.

### 2.2. exFAT (Extended File Allocation Table) [Concepto]
* **exFAT [Técnica]:** Evolución moderna de FAT (*Extended File Allocation Table*) diseñada por Microsoft para optimizar memorias flash, tarjetas SD/microSD y discos portátiles.
  * **Características:** Elimina la barrera de los 4 GB por archivo y los 2 TB por partición manteniendo una sobrecarga de estructura muy baja.
  * **Interoperabilidad Multiplataforma:** Es el estándar *de facto* para compartir archivos de gran tamaño (como vídeos 4K sin comprimir o imágenes ISO) entre Windows, macOS y GNU/Linux sin necesidad de controladores adicionales.

### 2.3. NTFS (New Technology File System) [Concepto]
* **NTFS [Técnica]:** Sistema de archivos nativo y estándar en los sistemas operativos Microsoft Windows desde Windows NT (*New Technology File System*).
  * **Características Avanzadas:**
    * **Journaling (Registro de Transacciones):** Registra los cambios pendientes en un diario antes de escribirlos en disco, permitiendo una rápida recuperación e integridad tras apagados imprevistos o cortes eléctricos.
    * **Seguridad y Permisos:** Soporta Listas de Control de Acceso (ACL - *Access Control List*) por usuario y grupo.
    * **Funciones Integradas:** Cifrado nativo (EFS - *Encrypting File System*), compresión transparente de archivos, cuotas de disco para usuarios y sombras de volumen (*Shadow Copies*).

### 2.4. ext4 (Fourth Extended Filesystem) [Concepto]
* **ext4 [Técnica]:** Sistema de archivos nativo estándar en distribuciones GNU/Linux modernas (*Fourth Extended Filesystem*).
  * **Características Avanzadas:**
    * **Capacidad:** Soporta archivos individuales de hasta **16 TB** y volúmenes de hasta **1 EB** (Exabyte).
    * **Extents:** Sustituye el mapeo de bloques tradicionales por rangos contiguos de clústeres (*extents*), reduciendo drásticamente la fragmentación.
    * **Journaling:** Ofrece tres niveles de registro (*journal*, *ordered*, *writeback*) para garantizar la máxima seguridad o velocidad según las necesidades del servidor.

### 2.5. APFS (Apple File System) [Concepto]
* **APFS [Técnica]:** Sistema de archivos optimizado para unidades de estado sólido (SSD) y memoria flash en dispositivos Apple (*Apple File System*).
  * **Características Avanzadas:** Arquitectura de 64 bits, clonación instantánea de archivos, *snapshots* (instantáneas) en segundo plano, cifrado nativo fuerte (simple o multi-clave) y compartición dinámica del espacio entre volúmenes.

### 📊 Tabla Comparativa de Sistemas de Archivos

| Sistema de Archivos | Origen del Nombre | Sistema Operativo Principal | Tamaño Máx. Archivo | Tamaño Máx. Volumen | Journaling | Uso Recomendado / Escenario |
| :--- | :--- | :--- | :--- | :--- | :---: | :--- |
| **FAT32** | **F**ile **A**llocation **T**able (32-bit) | Universal / Legacy | 4 GB | 2 TB | ❌ No | Unidades USB antiguas, dispositivos multimedia básicos. |
| **exFAT** | **Ex**tended **F**ile **A**llocation **T**able | Multiplataforma | 16 EB | 128 PB | ❌ No | Tarjetas SD/microSD (cámaras 4K), discos externos compartidos (Windows/Mac). |
| **NTFS** | **N**ew **T**echnology **F**ile **S**ystem | Microsoft Windows | 8 PB | 8 PB | ✅ Sí | Partición de sistema en Windows, servidores de archivos Windows con permisos ACL. |
| **ext4** | **Ex**tended **F**ilesystem (v4) | GNU / Linux | 16 TB | 1 EB | ✅ Sí | Partición de sistema en Linux, servidores corporativos, BD. |
| **APFS** | **A**pple **P**erformance / **F**ile **S**ystem | Apple macOS / iOS | Sin límite práctico | 8 EB | ✅ Sí | Unidades SSD en ordenadores Mac y dispositivos Apple. |

---

## 3. Jerarquía y Estructura de Directorios [Concepto]

* **Estructura en Árbol Invertido [Concepto]:** Modelo jerárquico donde la información se organiza partiendo de un nodo raíz (*root*) del cual ramifican directorios (carpetas) y subdirectorios hasta llegar a los archivos finales (hojas del árbol).
* **Rutas Absolutas vs. Rutas Relativas [Técnica]:**
  * **Ruta Absoluta:** Especifica la ubicación exacta de un archivo o directorio desde la raíz del sistema de archivos. Siempre empieza por la raíz (`/` en Linux, `C:\` en Windows).
    * *Ejemplo Linux:* `/home/usuario/documentos/informe.pdf`
    * *Ejemplo Windows:* `C:\Usuarios\usuario\documentos\informe.pdf`
  * **Ruta Relativa:** Especifica la ubicación partiendo del directorio de trabajo actual. Utiliza los símbolos especiales:
    * `.` : Representa el directorio actual (*current directory*).
    * `..` : Representa el directorio padre (*parent directory* - un nivel superior).
    * *Ejemplo:* `cd ../imagenes`

### 3.1. Estructura de Directorios en GNU/Linux (FHS - Filesystem Hierarchy Standard) [Concepto]
En GNU/Linux no existen letras de unidad (`C:`, `D:`). Toda la estructura depende de un único directorio raíz representado por la barra diagonal `/` (*root*).

```text
/ (Directorio Raíz / Root)
├── bin/      --> Binaries: Ejecutables esenciales del sistema para todos los usuarios (ls, cp, cat)
├── boot/     --> Bootstrap / Boot: Archivos del cargador de arranque (GRUB) y núcleo (vmlinuz)
├── dev/      --> Devices: Ficheros especiales que representan dispositivos físicos (sda, tty, null)
├── etc/      --> Editable Text Configuration / Etcetera: Archivos de configuración global del sistema y servicios
├── home/     --> Home: Directorios personales ("hogar") de usuarios estándar (/home/usuario)
├── lib/      --> Libraries: Bibliotecas compartidas esenciales para los ejecutables de /bin y /sbin
├── media/    --> Media: Puntos de montaje automáticos para medios extraíbles (USB, CD-ROM)
├── mnt/      --> Mount: Punto de montaje temporal para sistemas de archivos externos montados manualmente
├── opt/      --> Optional: Paquetes de software de aplicación opcionales de terceros
├── proc/     --> Processes: Sistema de archivos virtual con información del kernel y procesos activos (CPU, RAM)
├── root/     --> Root: Directorio personal del superusuario Administrador (root)
├── sbin/     --> System Binaries: Ejecutables de administración del sistema exclusivos para root (fdisk, mkfs)
├── sys/      --> System: Sistema de archivos virtual con información detallada sobre el hardware y drivers
├── tmp/      --> Temporary: Archivos temporales borrados habitualmente al reiniciar
├── usr/      --> User System Resources: Programas y datos de lectura compartidos por usuarios (/usr/bin, /usr/lib)
└── var/      --> Variable: Archivos de contenido variable (logs del sistema en /var/log, colas de impresión, BD)
```

### 3.2. Estructura de Directorios en Microsoft Windows [Concepto]
Windows organiza la información asignando letras de unidad a cada volumen lógico o partición (`C:`, `D:`).

```text
C:\ (Unidad de Sistema Principal)
├── Archivos de programa/         --> Program Files: Aplicaciones de 64 bits (en SO de 64 bits)
├── Archivos de programa (x86)/   --> Program Files (x86): Aplicaciones de 32 bits ejecutándose en SO de 64 bits
├── PerfLogs/                     --> Performance Logs: Registros e informes de rendimiento del sistema
├── ProgramData/                  --> Program Data: Carpeta oculta con datos de configuración compartidos por programas
├── Usuarios/ (Users)             --> Users: Carpetas personales de cada cuenta de usuario (Escritorio, Documentos)
└── Windows/                      --> Windows OS: Ficheros del sistema operativo
    ├── System32/                 --> System 32-bit: Librerías DLL críticas, controladores y ejecutables (cmd, calc)
    └── SysWOW64/                 --> Windows on Windows 64-bit: Subsystem para ejecutar aplicaciones de 32 bits en SO de 64 bits
```

---

## 4. Gestión de Archivos por Línea de Comandos en Linux (CLI) [Técnica]

* **Sintaxis Estándar de Comandos en Linux [Técnica]:**
  ```bash
  comando [opciones] [argumentos]  # Sintaxis estándar de ejecución en la CLI de Linux
  ```
  * **Comando:** La orden o programa a ejecutar (ej. `ls`, `cp`).
  * **Opciones:** Modificadores de comportamiento que suelen empezar por un guion `-` (formato corto) o dos guiones `--` (formato largo).
  * **Argumentos:** Los objetos sobre los que recae la acción (ficheros, directorios, rutas).

### 4.1. Tipos de Ficheros en Linux (`ls -l`) [Concepto]
En Linux sigue la filosofía de que **"todo es un archivo"**. Al ejecutar `ls -l` (*list long*), el primer carácter de cada línea identifica la naturaleza del elemento:

```text
drwxr-xr-x 2 alumno alumno 4096 oct  5 10:00 Documentos
-rw-r--r-- 1 alumno alumno  512 oct  5 10:05 notas.txt
lrwxrwxrwx 1 alumno alumno    9 oct  5 10:10 acceso -> notas.txt
```

* `-` : Fichero regular (*regular file* — texto, binario, imagen, ejecutable).
* `d` : Directorio (*directory* — carpeta que contiene referencias a otros i-nodos).
* `l` : Enlace simbólico (*symbolic link* — acceso directo a otra ruta).
* `b` : Dispositivo de bloques (*block device* — almacenamiento como discos duros `/dev/sda`).
* `c` : Dispositivo de caracteres (*character device* — flujo a flujo como teclados o puertos serie).
* `s` : Socket de red local (*socket* — comunicación IPC entre procesos).
* `p` : Tubería nombrada (*named pipe* / FIFO).

### 4.2. Comandos de Listado (`ls` - List) [Técnica]
```bash
ls [opciones] [ruta]             # Sintaxis general para listar el contenido de un directorio
```
* **Parámetros Clave (Mnemotécnicos):**
  * `-l` (**L**ong): Formato largo (muestra permisos, enlaces, propietario, grupo, tamaño, fecha y nombre).
  * `-a` (**A**ll): Muestra todos los ficheros, incluidos los ocultos (aquellos cuyo nombre empieza por `.`).
  * `-h` (**H**uman-readable): Muestra los tamaños en formato legible por humanos (KB, MB, GB).
  * `-t` (**T**ime): Ordena los ficheros por fecha de modificación (los más recientes primero).
  * `-r` (**R**everse): Invierte el orden de salida.
  * `-R` (**R**ecursive): Listado recursivo descendiendo por todos los subdirectorios.
  * `-S` (**S**ize): Ordena los ficheros por tamaño.
  * *Ejemplo combinado:* `ls -lah` (Lista con formato **L**ong, **A**ll ocultos y **H**uman-readable).

### 4.3. Operaciones Básicas de Ficheros y Directorios [Técnica]
* **Ubicación y Navegación:**
  ```bash
  pwd                 # Print Working Directory: muestra la ruta absoluta del directorio actual
  cd /var/log         # Change Directory: cambia al directorio especificado (Ruta absoluta)
  cd ..               # Cambia al directorio padre (parent directory)
  cd ~                # Cambia al directorio personal del usuario ($HOME)
  ```
* **Creación de Directorios (`mkdir` - Make Directory):**
  ```bash
  mkdir dirprueba               # Crea un directorio
  mkdir -p proyectos/2026/ut03  # -p (Parents): crea toda la ruta de subdirectorios padres si no existen
  ```
* **Copia de Elementos (`cp` - Copy):**
  ```bash
  cp origen.txt destino.txt     # Copia un fichero
  cp -r /origen /destino        # -r (Recursive): copia recursiva de un directorio entero y su contenido
  cp -i foto.jpg /imagenes/     # -i (Interactive): pide confirmación interactiva antes de sobrescribir
  ```
* **Movimiento y Renombrado (`mv` - Move):**
  ```bash
  mv archivo.txt nuevo.txt      # Renombra el archivo en el mismo directorio
  mv /tmp/script.sh /usr/bin/   # Mueve el archivo a otra ruta
  mv -u *.txt /respaldos/       # -u (Update): mueve solo si los archivos son más recientes que el destino
  ```
* **Eliminación (`rm` - Remove y `rmdir` - Remove Directory):**
  ```bash
  rm notas.txt                  # Elimina un fichero
  rm -i importante.doc          # -i (Interactive): pide confirmación antes de borrar
  rm -r dirprueba/              # -r (Recursive): elimina recursivamente un directorio y sus ficheros
  rm -rf /tmp/basura/           # -f (Force): fuerza la eliminación recursiva sin pedir confirmación (¡Peligro!)
  rmdir carpeta_vacia/          # Remove Directory: elimina exclusivamente un directorio que esté vacío
  ```

### 4.4. Visualización, Estadísticas y Ordenación de Texto [Técnica]
* **Visualización:**
  ```bash
  cat archivo.txt               # Concatenate: muestra todo el contenido del fichero en pantalla
  cat f1.txt f2.txt > f3.txt    # Concatena varios ficheros en uno nuevo
  more largo.txt                # Paginador básico (Avanza con Espacio, baja con Enter, sale con q)
  less largo.txt                # Paginador avanzado ("Less is More": permite desplazarse arriba/abajo con flechas)
  ```
* **Conteo de Ficheros (`wc` - Word Count):**
  ```bash
  wc -lwcL archivo.txt            # Muestra el recuento de líneas (-l), palabras (-w), caracteres (-c) y longitud máxima (-L)
  ```
  * `-l` (**L**ines): Cuenta el número de líneas.
  * `-w` (**W**ords): Cuenta el número de palabras.
  * `-c` (**C**haracters / bytes): Cuenta el número de bytes/caracteres.
  * `-L` (**L**ongest-line): Muestra la longitud de la línea más larga.
* **Ordenación de Ficheros (`sort` - Sort):**
  ```bash
  sort datos.txt                # Ordena las líneas en orden alfabético
  sort -n numeros.txt           # -n (Numeric): ordena numéricamente
  sort -r datos.txt             # -r (Reverse): ordena en orden inverso
  ```

### 4.5. Flujos Estándar y Redirecciones [Técnica]

Todo proceso en Linux dispone de tres canales o descriptores de archivos estándar abiertos:

```text
          ┌─────────────┐  ---> 1: Standard Output (stdout)  [Pantalla]
[Teclado] │  Comando /  │
0: stdin  │  Proceso    │  ---> 2: Standard Error (stderr)   [Pantalla]
          └─────────────┘
```

* **Descriptores Estándar:**
  * `0` : `stdin` (**St**andar**d** **In**put — por defecto el teclado).
  * `1` : `stdout` (**St**andar**d** **Out**put — por defecto la pantalla).
  * `2` : `stderr` (**St**andar**d** **Err**or — por defecto la pantalla).

* **Operadores de Redirección:**
  ```bash
  cmd > fichero.txt             # Redirige stdout (canal 1) creando/sobrescribiendo el fichero
  cmd >> fichero.txt            # Redirige stdout (canal 1) añadiendo (append) contenido al final del fichero
  cmd < entrada.txt             # Redirige stdin (canal 0) para leer los datos desde un fichero
  cmd 2> errores.log            # 2> : Redirige únicamente los errores (stderr - canal 2) a un archivo
  cmd 2>> errores.log           # 2>> : Añade los errores al final del archivo de logs
  cmd > todo.log 2>&1           # Redirige tanto stdout como stderr al mismo archivo (Método universal)
  cmd &> todo.log               # Redirige stdout y stderr al mismo archivo (Sintaxis rápida de Bash)
  ```

* **Tuberías / Pipes (`|`) y Duplicador (`tee`):**
  * `|` (Pipe): Conecta directamente la salida estándar (`stdout`) del primer comando con la entrada estándar (`stdin`) del segundo.
  * `tee` (Tee / "T" de fontanería): Duplica el flujo de datos; muestra la salida por pantalla (`stdout`) y la guarda simultáneamente en un archivo.
  ```bash
  cat /etc/passwd | grep "bash" | wc -l  # Cuenta el total de usuarios del sistema con shell /bin/bash
  cat log.txt | tee copia.txt            # Muestra el contenido en pantalla y lo guarda a la vez en copia.txt
  ```

### 4.6. Procesamiento de Textos (`cut`, `grep` y Expresiones Regulares) [Técnica]

* **Recorte de Columnas con `cut` (Cut):**
  * `-d` (**D**elimiter): Define el carácter separador de campos (ej. `-d,` para comas o `-d:` para `/etc/passwd`).
  * `-f` (**F**ields): Especifica los campos/columnas a extraer (ej. `-f1,3` para col. 1 y 3; `-f1-3` para rango 1 a 3).
  * `-c` (**C**haracters): Recorta posiciones fijas de caracteres (ej. `cut -c1-5`). *Incompatible con `-d` y `-f`.*
  ```bash
  cut -d: -f1,3 /etc/passwd     # Delimitador ':' y extrae los campos 1 (usuario) y 3 (UID)
  cut -d, -f1-3 datos.csv       # Delimitador ',' y extrae las columnas continuas de la 1 a la 3
  ```

* **Filtrado de Líneas con `grep` (Global Regular Expression Print):**
  * `-i` (**I**gnore-case): Ignora la diferencia entre mayúsculas y minúsculas.
  * `-v` (In**v**ert-match): Invierte la búsqueda (muestra todas las líneas que **NO** coinciden).
  * `-n` (**N**umber): Muestra el número de línea junto a cada coincidencia.
  * `-c` (**C**ount): Muestra exclusivamente el recuento total de líneas coincidentes.
  * `-w` (**W**ord): Coincidencia de palabra completa.
  * `-E` (**E**xtended): Habilita expresiones regulares extendidas (permite el operador OR `|`).
  ```bash
  grep -i "error" /var/log/syslog           # Muestra líneas con 'error', 'ERROR', 'Error'
  grep -v "DEBUG" app.log                # Muestra todas las líneas EXCEPTO las que contengan 'DEBUG'
  grep -E "WARN|ERROR" server.log        # Busca líneas que contengan WARN o ERROR (-E para Extended)
  ```

---

## 5. Gestión de Archivos por Interfaz Gráfica en Windows (GUI) [Técnica]

* **Explorador de Archivos de Windows [Técnica]:** Entorno gráfico intuitivo para la navegación, búsqueda y administración de carpetas y volúmenes.

### ⌨️ Atajos de Teclado Imprescindibles [Técnica]
* `Ctrl + X` : Cortar elementos seleccionados (X simula la forma de unas tijeras).
* `Ctrl + C` : **C**opiar elementos seleccionados (**C**opy).
* `Ctrl + V` : Pegar elementos cortados/copiados (situada junto a C y X en el teclado).
* `Ctrl + Z` : Deshacer la última acción (**Z**ero/Undo).
* `F2` : **F**unction 2: Renombrar rápidamente el elemento seleccionado.
* `Ctrl + E` : Seleccionar todo (**E**legir todo en español) / `Ctrl + A` (**A**ll en inglés).
* `Ctrl + D` / `Supr` : **D**elete / Suprimir: Eliminar y enviar a la Papelera de reciclaje.
* `Shift + Supr` : Eliminar permanentemente sin pasar por la Papelera.

---

## 6. Gestión de Almacenamiento por Línea de Comandos en Linux [Técnica]

### Identificación de Dispositivos en `/dev/` (**Dev**ices) [Concepto]
En Linux, los dispositivos de almacenamiento físico se representan mediante archivos especiales en el directorio `/dev/`:
* Discos SCSI, SATA, SAS, USB y SSD SATA: `/dev/sda`, `/dev/sdb`, `/dev/sdc` (`sd` = **S**CSI **D**isk; `a`, `b`, `c` = disco 1, 2, 3).
* Unidades NVMe modernas: `/dev/nvme0n1`, `/dev/nvme0n2` (**N**on-**V**olatile **M**emory **e**xpress).

### 6.1. Montaje y Desmontaje de Unidades (`mount`, `umount`, `/etc/fstab`) [Técnica]
* `mount` (**Mount**): Vincula una partición física a una carpeta o punto de montaje.
* `umount` (**Unmount** - *atención: sin 'o'*): Desvincula/desmonta la partición del sistema de archivos.
  ```bash
  mount /dev/sdb1 /mnt/disco_externo   # Monta la partición en el punto de montaje
  umount /mnt/disco_externo            # Desmonta especificando la carpeta o dispositivo
  mount -a                             # -a (All): Monta todas las unidades descritas en /etc/fstab
  ```

### 6.2. Particionado Interactivo con `fdisk` (**F**ormat / **F**ixed **D**isk) [Técnica]
Consola interactiva para administrar tablas de particiones MBR/GPT:
```bash
sudo fdisk /dev/sdb             # Inicia fdisk sobre el segundo disco
```
* **Comandos Clave de `fdisk`:**
  * `m` (**M**enu): Muestra la lista de ayuda y comandos.
  * `p` (**P**rint): Imprime la tabla de particiones actual del disco.
  * `n` (**N**ew): Crea una nueva partición (Primaria `p` o Extendida `e`).
  * `d` (**D**elete): Elimina una partición existente.
  * `t` (**T**ype): Cambia el tipo/sistema de ID de una partición (ej. `83` Linux, `82` Swap, `7` NTFS/exFAT).
  * `w` (**W**rite): Escribe los cambios permanentemente en el disco y sale.
  * `q` (**Q**uit): Sale sin guardar ninguna modificación.

### 6.3. Formateo de Particiones (`mkfs` - **M**a**k**e **F**ile **S**ystem) [Técnica]
Aplica un sistema de archivos a una partición desmontada:
```bash
sudo mkfs -t ext4 /dev/sdb1     # -t (Type): Formatea la partición con el sistema de archivos ext4
sudo mkfs.vfat -F 32 /dev/sdc1  # Formatea una memoria USB en FAT32
sudo mkfs.exfat /dev/sdc2       # Formatea en exFAT para compatibilidad Windows/Mac
```

### 6.4. Chequeo e Integridad del Sistema de Archivos (`fsck` - **F**ile **S**ystem **C**hec**k**) [Técnica]
Verifica y repara la consistencia lógica de particiones desmontadas tras apagados imprevistos:
```bash
sudo umount /dev/sdb1           # IMPORTANTE: Desmontar siempre antes de chequear
sudo fsck /dev/sdb1             # File System Check: Chequea y repara errores interactivos
sudo e2fsck -p /dev/sdb1        # -p (Preen/Automatic): Repara automáticamente sin hacer preguntas
```

---

## 7. Sistemas de Almacenamiento Redundante (RAID) [Concepto]

* **RAID (**R**edundant **A**rray of **I**ndependent **D**isks) [Concepto]:** Tecnología que combina múltiples unidades físicas en una o varias unidades lógicas para ganar velocidad, tolerancia a fallos o ambas.
* **RAID Hardware vs. Software:**
  * **Hardware:** Controladora dedicada con procesador y caché propia. Cero consumo de CPU en el Host.
  * **Software:** Gestionado por el propio SO (módulo `mdadm` en Linux, volúmenes dinámicos en Windows). Consume CPU y RAM.
* **Regla de Oro:** Un RAID **NO** es una copia de seguridad (*backup*). Un borrado accidental o virus se replica al instante en todos los discos del array.

### 📊 Resumen Simplificado de Niveles RAID para Examen

| Nivel RAID | Nombre Comercial | Mín. Discos | Tolerancia a Fallos | Capacidad Útil | Rendimiento Lectura | Rendimiento Escritura |
| :---: | :--- | :---: | :---: | :---: | :---: | :---: |
| **RAID 0** | **Striping** (Distribución en Tiras) | 2 | **0 discos** (Ninguno) | 100% `(N * C)` | 🚀 Máximo | 🚀 Máximo |
| **RAID 1** | **Mirroring** (Espejo) | 2 | **1 disco** | 50% `(1 * C)` | 🟢 Alto | 🟡 Medio |
| **RAID 5** | **Paridad Distribuida** | 3 | **1 disco** | `(N - 1) * C` | 🟢 Alto | 🟡 Medio |
| **RAID 6** | **Doble Paridad Distribuida** | 4 | **2 discos** | `(N - 2) * C` | 🟢 Alto | 🔴 Lento (Cálculo) |
| **RAID 10**| **Mirroring + Striping** (RAID 1+0) | 4 | **1 disco por pareja** | 50% `(N / 2) * C` | 🚀 Muy Alto | 🚀 Muy Alto |

---

## 8. Gestión de Almacenamiento por Interfaz Gráfica en Windows [Técnica]

* **Administrador de Discos de Windows (`diskmgmt.msc` - **Disk** **M**ana**g**e**m**en**t**):** Herramienta gráfica para consultar, inicializar, particionar, formatear y gestionar discos.
* **Discos Básicos vs. Dinámicos [Concepto]:**
  * **Básicos:** Estructura estándar basada en MBR o GPT.
  * **Dinámicos:** Permiten volúmenes no contiguos extendidos entre múltiples discos.
    * *Volumen Seccionado:* Equivale a **RAID 0** por software.
    * *Volumen Reflejado:* Equivale a **RAID 1** por software.
    * *Volumen RAID-5:* Equivale a **RAID 5** por software (disponible en Windows Server).

---

## 9. Búsqueda Avanzada de Información [Técnica]

### 9.1. Búsquedas por Línea de Comandos en Linux (`find` y `locate`) [Técnica]

* **Comando `find` (Find - Búsqueda en tiempo real):**
  * `-name` (**Name**): Búsqueda sensible a mayúsculas/minúsculas.
  * `-iname` (**I**gnore-case **Name**): Búsqueda insensible a mayúsculas/minúsculas.
  * `-type` (**Type**): Filtra por tipo (`f`ile = archivo regular, `d`irectory = carpeta, `l`ink = enlace).
  * `-maxdepth` (**Max**imum **Depth**): Limita la profundidad de subdirectorios a inspeccionar.
  * `-mtime` (**M**odification **Time**): Días desde la última modificación (`-7` = últimos 7 días).
  * `-size` (**Size**): Filtra por tamaño (`+100M` = mayor a 100 MB; `-10k` = menor a 10 KB).
  ```bash
  find /var/www -type d -maxdepth 1               # Busca solo directorios en el nivel actual
  find /home -iname "*.pdf" -mtime -7            # Busca PDFs modificados en la última semana
  ```

* **Comando `locate` (Locate - Búsqueda por base de datos indexada):**
  ```bash
  sudo updatedb                                    # Update Database: actualiza el índice del sistema
  locate "informe.pdf"                             # Búsqueda instantánea en el índice mlocate.db
  ```

---

## 10. Práctica y Laboratorios (Lab UT03) [Técnica]

### Despliegue Práctico de Entorno Virtualizado (Oracle VM VirtualBox) [Técnica]
1. **Regla del 50% de RAM:** No asignar más de la mitad de la RAM física del Host al Guest.
2. **Formato VDI:** **V**irtualBox **D**isk **I**mage con almacenamiento dinámico.
3. **Instalación Guiada:** Desmarcar la casilla *Skip Unattended Installation* (Omitir instalación desatendida) para realizar la instalación manual paso a paso.
