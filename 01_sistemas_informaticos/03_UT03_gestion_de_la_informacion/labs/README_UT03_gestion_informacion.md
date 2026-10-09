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
* **FAT / FAT32 [Técnica]:** Sistema de archivos desarrollado originalmente por Microsoft basado en una tabla de asignación de archivos que vincula clústeres contiguos o dispersos.
  * **Características:** Simplicidad extrema y compatibilidad universal (televisores, consolas, equipos antiguos, sistemas embebidos).
  * **Limitaciones Críticas de FAT32:** 
    * Tamaño máximo por archivo individual: **4 GB**.
    * Tamaño máximo de partición/volumen: **2 TB**.
    * Cero soporte nativo para permisos de seguridad a nivel de archivo (ACL), cifrado o compresión.

### 2.2. exFAT (Extended File Allocation Table) [Concepto]
* **exFAT [Técnica]:** Evolución moderna de FAT diseñada por Microsoft para optimizar memorias flash, tarjetas SD/microSD y discos portátiles.
  * **Características:** Elimina la barrera de los 4 GB por archivo y los 2 TB por partición manteniendo una sobrecarga de estructura muy baja.
  * **Interoperabilidad Multiplataforma:** Es el estándar *de facto* para compartir archivos de gran tamaño (como vídeos 4K sin comprimir o imágenes ISO) entre Windows, macOS y GNU/Linux sin necesidad de controladores adicionales.

### 2.3. NTFS (New Technology File System) [Concepto]
* **NTFS [Técnica]:** Sistema de archivos nativo y estándar en los sistemas operativos Microsoft Windows desde Windows NT.
  * **Características Avanzadas:**
    * **Journaling (Registro de Transacciones):** Registra los cambios pendientes en un diario antes de escribirlos en disco, permitiendo una rápida recuperación e integridad tras apagados imprevistos o cortes eléctricos.
    * **Seguridad y Permisos:** Soporta Listas de Control de Acceso (ACL) por usuario y grupo.
    * **Funciones Integradas:** Cifrado nativo (EFS), compresión transparente de archivos, cuotas de disco para usuarios y sombras de volumen (Shadow Copies).

### 2.4. ext4 (Fourth Extended Filesystem) [Concepto]
* **ext4 [Técnica]:** Sistema de archivos nativo estándar en distribuciones GNU/Linux modernas.
  * **Características Avanzadas:**
    * **Capacidad:** Soporta archivos individuales de hasta **16 TB** y volúmenes de hasta **1 EB** (Exabyte).
    * **Extents:** Sustituye el mapeo de bloques tradicionales por rangos contiguos de clústeres (*extents*), reduciendo drásticamente la fragmentación.
    * **Journaling:** Ofrece tres niveles de registro (*journal*, *ordered*, *writeback*) para garantizar la máxima seguridad o velocidad según las necesidades del servidor.

### 2.5. APFS (Apple File System) [Concepto]
* **APFS [Técnica]:** Sistema de archivos optimizado para unidades de estado sólido (SSD) y memoria flash en dispositivos Apple (macOS, iOS).
  * **Características Avanzadas:** Arquitectura de 64 bits, clonación instantánea de archivos, *snapshots* (instantáneas) en segundo plano, cifrado nativo fuerte (simple o multi-clave) y compartición dinámica del espacio entre volúmenes.

### 📊 Tabla Comparativa de Sistemas de Archivos

| Sistema de Archivos | Sistema Operativo Principal | Tamaño Máx. Archivo | Tamaño Máx. Volumen | Journaling | Uso Recomendado / Escenario |
| :--- | :--- | :--- | :--- | :---: | :--- |
| **FAT32** | Universal / Legacy | 4 GB | 2 TB | ❌ No | Unidades USB antiguas, dispositivos multimedia básicos. |
| **exFAT** | Multiplataforma | 16 EB | 128 PB | ❌ No | Tarjetas SD/microSD (cámaras 4K), discos externos compartidos. |
| **NTFS** | Microsoft Windows | 8 PB | 8 PB | ✅ Sí | Partición de sistema en Windows, servidores de archivos Windows. |
| **ext4** | GNU / Linux | 16 TB | 1 EB | ✅ Sí | Partición de sistema en Linux, servidores corporativos, BD. |
| **APFS** | Apple macOS / iOS | Sin límite práctico | 8 EB | ✅ Sí | Unidades SSD en ordenadores Mac y dispositivos Apple. |

---

## 3. Jerarquía y Estructura de Directorios [Concepto]

* **Estructura en Árbol Invertido [Concepto]:** Modelo jerárquico donde la información se organiza partiendo de un nodo raíz (*root*) del cual ramifican directorios (carpetas) y subdirectorios hasta llegar a los archivos finales (hojas del árbol).
* **Rutas Absolutas vs. Rutas Relativas [Técnica]:**
  * **Ruta Absoluta:** Especifica la ubicación exacta de un archivo o directorio desde la raíz del sistema de archivos. Siempre empieza por la raíz (`/` en Linux, `C:\` en Windows).
    * *Ejemplo Linux:* `/home/usuario/documentos/informe.pdf`
    * *Ejemplo Windows:* `C:\Usuarios\usuario\documentos\informe.pdf`
  * **Ruta Relativa:** Especifica la ubicación partiendo del directorio de trabajo actual. Utiliza los símbolos especiales:
    * `.` : Representa el directorio actual.
    * `..` : Representa el directorio padre (un nivel superior).
    * *Ejemplo:* `cd ../imagenes`

### 3.1. Estructura de Directorios en GNU/Linux (FHS - Filesystem Hierarchy Standard) [Concepto]
En GNU/Linux no existen letras de unidad (`C:`, `D:`). Toda la estructura depende de un único directorio raíz representado por la barra diagonal `/`.

```text
/ (Directorio Raíz)
├── bin/      --> Ejecutables esenciales del sistema para todos los usuarios (ls, cp, cat)
├── boot/     --> Archivos del cargador de arranque (GRUB) y núcleo (vmlinuz)
├── dev/      --> Ficheros especiales que representan dispositivos físicos (sda, tty, null)
├── etc/      --> Archivos de configuración global del sistema y servicios
├── home/     --> Directorios personales de usuarios estándar (/home/usuario)
├── lib/      --> Bibliotecas compartidas esenciales para los ejecutables de /bin y /sbin
├── media/    --> Puntos de montaje automáticos para medios extraíbles (USB, CD-ROM)
├── mnt/      --> Punto de montaje temporal para sistemas de archivos externos montados manualmente
├── opt/      --> Paquetes de software de aplicación opcionales de terceros
├── proc/     --> Sistema de archivos virtual de información del kernel y procesos (CPU, RAM)
├── root/     --> Directorio personal del superusuario Administrador (root)
├── sbin/     --> Ejecutables de administración del sistema exclusivos para root (fdisk, mkfs)
├── sys/      --> Sistema de archivos virtual con información sobre el hardware y drivers
├── tmp/      --> Archivos temporales borrados habitualmente al reiniciar
├── usr/      --> Programas y datos de lectura compartidos por usuarios (/usr/bin, /usr/lib)
└── var/      --> Archivos de contenido variable (logs del sistema en /var/log, bases de datos)
```

### 3.2. Estructura de Directorios en Microsoft Windows [Concepto]
Windows organiza la información asignando letras de unidad a cada volumen lógico o partición (`C:`, `D:`).

```text
C:\ (Unidad de Sistema Principal)
├── Archivos de programa/         --> Aplicaciones de 64 bits (en SO de 64 bits) o 32 bits (en SO de 32 bits)
├── Archivos de programa (x86)/   --> Aplicaciones de 32 bits ejecutándose en un sistema de 64 bits
├── PerfLogs/                     --> Registros e informes de rendimiento del sistema
├── ProgramData/                  --> Carpeta oculta con datos de configuración compartidos por programas
├── Usuarios/ (Users)             --> Carpetas personales de cada cuenta de usuario (Escritorio, Documentos)
└── Windows/                      --> Ficheros del sistema operativo
    ├── System32/                 --> Librerías DLL críticas, controladores y ejecutables del sistema (cmd, calc)
    └── SysWOW64/                 --> Subsystem para ejecutar aplicaciones de 32 bits en Windows de 64 bits
```

---

## 4. Gestión de Archivos por Línea de Comandos en Linux (CLI) [Técnica]

* **Sintaxis Estándar de Comandos en Linux [Técnica]:**
  ```bash
  comando [opciones] [argumentos]
  ```
  * **Comando:** La orden o programa a ejecutar (ej. `ls`, `cp`).
  * **Opciones:** Modificadores de comportamiento que suelen empezar por un guion `-` (formato corto) o dos guiones `--` (formato largo).
  * **Argumentos:** Los objetos sobre los que recae la acción (ficheros, directorios, rutas).

### 4.1. Tipos de Ficheros en Linux (`ls -l`) [Concepto]
En Linux sigue la filosofía de que **"todo es un archivo"**. Al ejecutar `ls -l`, el primer carácter de cada línea identifica la naturaleza del elemento:

```text
drwxr-xr-x 2 alumno alumno 4096 oct  5 10:00 Documentos
-rw-r--r-- 1 alumno alumno  512 oct  5 10:05 notas.txt
lrwxrwxrwx 1 alumno alumno    9 oct  5 10:10 acceso -> notas.txt
```

* `-` : Fichero regular (texto, binario, imagen, ejecutable).
* `d` : Directorio (carpeta que contiene referencias a otros i-nodos).
* `l` : Enlace simbólico (*symbolic link* o acceso directo).
* `b` : Dispositivo de bloques (almacenamiento como discos duros `/dev/sda`).
* `c` : Dispositivo de caracteres (transmisión flujo a flujo como teclados o puertos serie).
* `s` : Socket de red local (comunicación entre procesos).
* `p` : Tubería nombrada (*named pipe* / FIFO).

* **Diferenciación por Colores (`ls --color=auto`) [Técnica]:**
  * **Blanco / Gris:** Fichero regular sin permisos de ejecución.
  * **Verde:** Fichero ejecutable.
  * **Azul:** Directorio.
  * **Cian:** Enlace simbólico válido.
  * **Rojo / Parpadeante:** Enlace simbólico roto o archivo comprimido corrupto.

### 4.2. Comandos de Listado (`ls`) [Técnica]
```bash
ls [opciones] [ruta]
```
* **Parámetros Clave:**
  * `-l` : Formato largo (muestra permisos, enlaces, propietario, grupo, tamaño, fecha de modificación y nombre).
  * `-a` : Muestra todos los ficheros, incluidos los ocultos (aquellos cuyo nombre empieza por `.`).
  * `-h` : Muestra los tamaños en formato legible por humanos (*Human Readable*: KB, MB, GB).
  * `-t` : Ordena los ficheros por fecha de modificación (los más recientes primero).
  * `-r` : Invierte el orden de salida.
  * `-R` : Listado recursivo de todos los subdirectorios.
  * `-S` : Ordena los ficheros por tamaño.

### 4.3. Operaciones Básicas de Ficheros y Directorios [Técnica]
* **Ubicación y Navegación:**
  ```bash
  pwd                 # Print Working Directory: muestra la ruta absoluta del directorio actual
  cd /var/log         # Cambia al directorio especificado (Ruta absoluta)
  cd ..               # Sube un nivel en la jerarquía
  cd ~                # Cambia al directorio personal del usuario ($HOME)
  ```
* **Creación de Directorios:**
  ```bash
  mkdir dirprueba               # Crea un directorio
  mkdir -p proyectos/2026/ut03  # Crea toda la ruta de subdirectorios padres si no existen
  ```
* **Copia de Elementos (`cp`):**
  ```bash
  cp origen.txt destino.txt     # Copia un fichero
  cp -r /origen /destino        # Copia recursiva de un directorio entero y su contenido
  cp -i foto.jpg /imagenes/     # Pide confirmación interactiva antes de sobrescribir
  ```
* **Movimiento y Renombrado (`mv`):**
  ```bash
  mv archivo.txt nuevo.txt      # Renombra el archivo en el mismo directorio
  mv /tmp/script.sh /usr/bin/   # Mueve el archivo a otra ruta
  mv -u *.txt /respaldos/       # Mueve solo los archivos más recientes que los del destino
  ```
* **Eliminación (`rm` y `rmdir`):**
  ```bash
  rm notas.txt                  # Elimina un fichero
  rm -i importante.doc          # Pide confirmación antes de borrar
  rm -r dirprueba/              # Elimina recursivamente un directorio no vacío y sus ficheros
  rm -rf /tmp/basura/           # Fuerza la eliminación recursiva sin pedir confirmación (¡Usar con precaución!)
  rmdir carpeta_vacia/          # Elimina exclusivamente un directorio que esté completamente vacío
  ```

### 4.4. Visualización, Estadísticas y Ordenación de Texto [Técnica]
* **Visualización:**
  ```bash
  cat archivo.txt               # Muestra todo el contenido del fichero en pantalla
  cat f1.txt f2.txt > f3.txt    # Concatena varios ficheros en uno nuevo
  more largo.txt                # Paginador básico (Avanza con Espacio, baja con Enter, sale con q)
  less largo.txt                # Paginador avanzado (Permite desplazarse arriba/abajo con flechas y buscar con /texto)
  ```
* **Conteo de Ficheros (`wc`):**
  ```bash
  wc -lwcL archivo.txt
  ```
  * `-l` : Cuenta el número de líneas.
  * `-w` : Cuenta el número de palabras.
  * `-c` : Cuenta el número de bytes/caracteres.
  * `-L` : Muestra la longitud de la línea más larga.
* **Ordenación de Ficheros (`sort`):**
  ```bash
  sort datos.txt                # Ordena las líneas en orden alfabético
  sort -n numeros.txt           # Ordena numéricamente
  sort -r datos.txt             # Ordena en orden inverso
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
  * `0` : `stdin` (Entrada estándar — por defecto el teclado).
  * `1` : `stdout` (Salida estándar — por defecto la pantalla).
  * `2` : `stderr` (Salida de errores estándar — por defecto la pantalla).

* **Operadores de Redirección:**
  ```bash
  cmd > fichero.txt             # Redirige stdout creando/sobrescribiendo el fichero
  cmd >> fichero.txt            # Redirige stdout añadiendo contenido al final del fichero
  cmd < entrada.txt             # Redirige stdin para leer los datos desde un fichero
  cmd 2> errores.log            # Redirige únicamente los errores (stderr) a un archivo
  cmd 2>> errores.log           # Añade los errores al final del archivo de logs
  cmd > todo.log 2>&1           # Redirige tanto stdout como stderr al mismo archivo (Método universal)
  cmd &> todo.log               # Redirige stdout y stderr al mismo archivo (Sintaxis rápida de Bash)
  ```

* **Here-Doc (`<<`):** Permite inyectar múltiples líneas de texto como entrada estándar hasta encontrar un delimitador:
  ```bash
  cat <<FIN > nota.txt
  Hola equipo,
  Esta es una nota generada automáticamente.
  FIN
  ```

* **Tuberías / Pipes (`|`):** Conecta directamente la salida estándar (`stdout`) del primer comando con la entrada estándar (`stdin`) del segundo comando:
  ```bash
  cat /etc/passwd | grep "bash" | wc -l
  ls -la /etc | tee archivo_lista.txt | less   # 'tee' duplica la salida: la guarda en fichero y la pasa a 'less'
  ```

### 4.6. Procesamiento de Textos (`cut`, `grep` y Expresiones Regulares) [Técnica]

* **Recorte de Columnas con `cut`:**
  ```bash
  cut -c1-5 notas.txt           # Recorta del carácter 1 al 5 de cada línea
  cut -d: -f1,3 /etc/passwd     # Delimitador ':' y extrae los campos 1 (usuario) y 3 (UID)
  ```

* **Filtrado de Líneas con `grep`:**
  ```bash
  grep "ERROR" /var/log/syslog              # Muestra líneas que contienen la palabra ERROR
  grep -i "error" app.log                   # Ignora mayúsculas y minúsculas
  grep -v "DEBUG" app.log                   # Muestra todas las líneas EXCEPTO las que contengan DEBUG
  grep -n "fail" /var/log/auth.log          # Muestra el número de línea junto a la coincidencia
  grep -c "200 OK" access.log               # Muestra el recuento total de líneas que coinciden
  grep -w "root" /etc/passwd                # Busca la palabra completa 'root'
  ```

* **Expresiones Regulares (RegEx / `-E`):**
  * `.` : Cualquier carácter individual.
  * `*` : Cero o más repeticiones del carácter anterior.
  * `^` : Inicio de línea (`^root` -> líneas que empiezan por root).
  * `$` : Fin de línea (`bash$` -> líneas que terminan en bash).
  * `[abc]` : Cualquier carácter contenido entre corchetes.
  * `[^abc]` : Cualquier carácter que NO esté entre corchetes.
  * `[a-z]` : Rango de caracteres.
  * `\` : Escapa un carácter especial para tratarlo como literal.
  ```bash
  grep -E "^(WARN|ERROR)" server.log        # Busca líneas que empiecen por WARN o ERROR (Expresión extendida)
  grep -E "GET|POST" access.log             # Muestra peticiones HTTP GET o POST
  ```

---

## 5. Gestión de Archivos por Interfaz Gráfica en Windows (GUI) [Técnica]

* **Explorador de Archivos de Windows [Técnica]:** Entorno gráfico intuitivo para la navegación, búsqueda y administración de carpetas y volúmenes.
* **Componentes Principales de la Ventana:**
  1. Barra de herramientas de acceso rápido.
  2. Cinta de opciones (*Ribbon*).
  3. Botones de navegación (Atrás, Adelante, Arriba).
  4. Barra de direcciones interactivas.
  5. Caja de búsqueda integrada.
  6. Panel de navegación lateral.
  7. Ventana principal de ficheros y detalles.

### ⌨️ Atajos de Teclado Imprescindibles [Técnica]
* `Ctrl + X` : Cortar elementos seleccionados.
* `Ctrl + C` : Copiar elementos seleccionados.
* `Ctrl + V` : Pegar elementos cortados/copiados.
* `Ctrl + Z` : Deshacer la última acción.
* `F2` : Renombrar rápidamente el elemento seleccionado.
* `Ctrl + E` : Seleccionar todos los elementos del directorio actual.
* `Ctrl + D` / `Supr` : Eliminar y enviar elementos a la Papelera de reciclaje.
* `Shift + Supr` : Eliminar permanentemente sin pasar por la Papelera.
* `Ctrl + Clic` : Seleccionar múltiples elementos no contiguos.
* `Shift + Clic` : Seleccionar un rango de elementos contiguos.

---

## 6. Gestión de Almacenamiento por Línea de Comandos en Linux [Técnica]

### Identificación de Dispositivos en `/dev/` [Concepto]
En Linux, los dispositivos de almacenamiento físico se representan mediante archivos especiales en el directorio `/dev/`:

* Discos IDE/PATA antiguos: `/dev/hda`, `/dev/hdb`.
* Discos SCSI, SATA, SAS, USB y SSD SATA: `/dev/sda`, `/dev/sdb`, `/dev/sdc`.
* Unidades NVMe modernas: `/dev/nvme0n1`, `/dev/nvme0n2`.
* Unidades CD/DVD ópticas: `/dev/sr0`, `/dev/cdrom`.

* **Nomenclatura de Particiones (MBR / GPT):**
  * La letra final indica el identificador de disco físico (`a` para el primer disco, `b` para el segundo).
  * El número posterior indica el número de partición:
    * *Sistemas MBR:* Particiones primarias etiquetadas del `1` al `4`. Particiones lógicas numeradas siempre a partir del `5` (ej. `/dev/sda5`).
    * *Ejemplo:* `/dev/sdb2` representa la segunda partición del segundo disco SATA/USB.

### 6.1. Montaje y Desmontaje de Unidades (`mount`, `umount`, `/etc/fstab`) [Técnica]

Para que una partición sea accesible en el árbol de directorios de Linux, debe vincularse a una carpeta llamada **Punto de Montaje**.

```bash
# Montar una partición en una carpeta existente:
mount /dev/sdb1 /mnt/disco_externo

# Opciones avanzadas de montaje:
mount -t ext4 -o ro /dev/sdc1 /media/lectura   # Monta como solo lectura (-r / -o ro)
mount -o rw /dev/sdb1 /mnt/datos               # Monta con permisos de lectura y escritura (-w / -o rw)
mount -a                                       # Monta todos los sistemas de archivos definidos en /etc/fstab

# Desmontar una unidad:
umount /dev/sdb1                               # Desmonta especificando el dispositivo
umount /mnt/disco_externo                      # Desmonta especificando el punto de montaje
```

* **Fichero `/etc/fstab` [Técnica]:** Archivo de configuración que contiene la lista de particiones y dispositivos que se montan automáticamente durante la secuencia de arranque del sistema.

### 6.2. Particionado Interactivo con `fdisk` y `partprobe` [Técnica]

`fdisk` es la herramienta de consola tradicional para gestionar tablas de particiones MBR/DOS.

```bash
sudo fdisk -l                   # Lista todos los discos físicos, particiones y tamaños conectados
sudo fdisk /dev/sdb             # Inicia la consola interactiva sobre el segundo disco
```

* **Comandos Clave dentro de la Consola Interactiva de `fdisk`:**
  * `m` : Muestra la lista de ayuda y comandos disponibles.
  * `p` : Imprime la tabla de particiones actual del disco.
  * `n` : Añade y crea una nueva partición (pregunta si será Primaria `p` o Extendida `e`).
  * `d` : Elimina una partición existente.
  * `t` : Cambia el tipo/sistema de ID de una partición (ej. `83` para Linux, `82` para Swap, `7` para NTFS/exFAT).
  * `v` : Verifica la tabla de particiones.
  * `w` : Escribe los cambios permanentemente en la tabla del disco y sale.
  * `q` : Sale de `fdisk` sin guardar ninguna modificación realizada en la sesión.

```bash
sudo partprobe                  # Informa al kernel de Linux de los cambios en las particiones sin reiniciar
```

### 6.3. Formateo de Particiones (`mkfs`) [Técnica]

Una vez creada la partición, debe aplicársele un sistema de archivos (formatearla) para poder almacenar datos. **La partición debe estar desmontada.**

```bash
sudo mkfs -t ext4 /dev/sdb1     # Formatea la partición con el sistema de archivos ext4
sudo mkfs.vfat -F 32 /dev/sdc1  # Formatea una memoria USB en FAT32
sudo mkfs.exfat /dev/sdc2       # Formatea en exFAT
```

### 6.4. Mantenimiento y Desfragmentación (`e4defrag`) [Técnica]

* **Fragmentación [Concepto]:** Fenómeno en el que los bloques de datos de un mismo archivo quedan dispersos en sectores distantes del disco. Afecta negativamente el tiempo de lectura en discos duros mecánicos (HDD).
* **Desfragmentación en ext4 [Técnica]:** Los sistemas de archivos en Linux previenen la fragmentación mediante la asignación inteligente por *extents*. No obstante, en discos muy llenos (>85%), se puede evaluar y desfragmentar con `e4defrag`:
  ```bash
  sudo e4defrag -c /home/usuario/   # Evalúa el nivel de fragmentación (-c) del directorio
  sudo e4defrag /dev/sda1           # Desfragmenta la partición especificada
  ```

### 6.5. Chequeo e Integridad del Sistema de Archivos (`fsck`, `e2fsck`, S.M.A.R.T.) [Técnica]

* **S.M.A.R.T. (Self-Monitoring, Analysis and Reporting Technology) [Técnica]:** Sistema de diagnóstico integrado en discos duros y SSD que monitoriza temperatura, sectores reasignados y tasa de errores de lectura.
* **Comandos de Chequeo y Reparación (`fsck` / `e2fsck`):**
  **IMPORTANTE:** Nunca se debe ejecutar `fsck` sobre una partición montada, ya que podría causar la pérdida irreversible de datos.
  ```bash
  sudo umount /dev/sdb1
  sudo fsck /dev/sdb1           # Chequea y repara errores interactivos en la partición
  sudo e2fsck -p /dev/sdb1      # Repara automáticamente sin hacer preguntas (-p / preen)
  sudo e2fsck -c /dev/sdb1      # Busca bloques defectuosos (bad blocks) y los añade a la lista negra
  sudo e2fsck -y /dev/sdb1      # Responde 'sí' automáticamente a todas las correcciones
  ```

---

## 7. Sistemas de Almacenamiento Redundante (RAID) [Concepto]

* **RAID (Redundant Array of Independent Disks) [Concepto]:** Tecnología que combina múltiples unidades de disco duro físicas en una o varias unidades lógicas para mejorar el rendimiento de lectura/escritura, aumentar la tolerancia a fallos mediante redundancia, o ambas cosas.
* **RAID por Hardware vs. RAID por Software [Técnica]:**
  * **RAID por Hardware:** Gestionado por una tarjeta controladora dedicada montada en la placa base con su propio procesador y memoria caché.
    * *Ventajas:* Máximo rendimiento, cero sobrecarga en la CPU del sistema anfitrión, transparencia total para el SO.
    * *Desventajas:* Coste económico elevado.
  * **RAID por Software:** Gestionado por el propio sistema operativo (ej. módulo `mdadm` en Linux, volúmenes dinámicos en Windows Server).
    * *Ventajas:* Económico, no requiere hardware especial.
    * *Desventajas:* Consume ciclos de procesador y memoria del equipo anfitrión.
  * **Fake RAID / RAID Integrado:** Controladoras de gama baja en placas base de consumo que procesan la paridad por software. Se desaconseja totalmente en entornos profesionales.

> **💡 Regla de Oro Profesional:** Un RAID **NO** sustituye a una copia de seguridad (*backup*). Un borrado accidental o un ataque de *ransomware* se replicará instantáneamente en todos los discos del conjunto RAID.

### 7.1. Niveles RAID Principales [Concepto]

#### 1. RAID 0 (Striping / Distribución en Tiras) [Concepto]
* **Mínimo de Discos:** 2 discos.
* **Funcionamiento:** Divide los datos en bloques y los escribe alternadamente entre todos los discos del array.
* **Capacidad Útil:** 100% de la capacidad combinada de todos los discos `(N * Capacidad)`.
* **Ventajas:** Máxima velocidad de lectura y escritura.
* **Desventajas:** **Cero tolerancia a fallos.** Si falla un solo disco, se pierde la totalidad de los datos.

#### 2. RAID 1 (Mirroring / Espejo) [Concepto]
* **Mínimo de Discos:** 2 discos.
* **Funcionamiento:** Duplica exactamente la misma información en dos o más discos de forma simultánea.
* **Capacidad Útil:** 50% de la capacidad total (Capacidad de 1 disco).
* **Ventajas:** Alta seguridad y tolerancia a fallos. Si falla un disco, el sistema sigue funcionando normalmente sin interrupciones.
* **Desventajas:** Alta sobrecarga económica (se duplica el coste por GB almacenable).

#### 3. RAID 5 (Paridad Distribuida) [Concepto]
* **Mínimo de Discos:** 3 discos.
* **Funcionamiento:** Divide los datos entre los discos y calcula un bloque de **paridad** que distribuye rotativamente entre todas las unidades.
* **Capacidad Útil:** `(N - 1) * Capacidad`.
* **Ventajas:** Excelente equilibrio entre rendimiento, capacidad utilizable y tolerancia a fallos. **Soporta el fallo de 1 disco simultáneo.**
* **Desventajas:** La velocidad de escritura es ligeramente más lenta debido al cálculo en tiempo real de los bloques de paridad.

#### 4. RAID 6 (Doble Paridad Distribuida) [Concepto]
* **Mínimo de Discos:** 4 discos.
* **Funcionamiento:** Similar a RAID 5, pero genera y distribuye dos bloques independientes de paridad (P y Q).
* **Capacidad Útil:** `(N - 2) * Capacidad`.
* **Ventajas:** Alta resiliencia. **Soporta el fallo simultáneo de hasta 2 discos sin perder datos.** Ideal para conjuntos de almacenamiento con discos de gran capacidad donde la reconstrucción requiere muchas horas.
* **Desventajas:** Escritura más lenta que RAID 5 y mayor penalización de espacio.

### 7.2. Niveles RAID Anidados / Combinados [Concepto]

* **RAID 0+1 (RAID 01):** Crea primero dos conjuntos en RAID 0 (striping) y luego aplica un espejo RAID 1 entre ellos. Requiere mínimo 4 discos. Si falla un disco en cada sub-array, todo el conjunto puede colapsar.
* **RAID 10 (RAID 1+0):** Crea primero parejas de discos en espejo RAID 1 y sobre ellas aplica una distribución RAID 0. Mínimo 4 discos. Es mucho más seguro y tolerante a fallos que RAID 0+1, convirtiéndose en el estándar para servidores de bases de datos.
* **RAID 50 (RAID 5+0):** Combina varios grupos de RAID 5 unidos mediante un stripe RAID 0. Ofrece gran velocidad, capacidad utilizable y alta protección para centros de datos.

### 📊 Tabla Resumen de Niveles RAID

| Nivel RAID | Nombre Comercial | Mínimo Discos | Tolerancia a Fallos | Capacidad Útil | Rendimiento Lectura | Rendimiento Escritura |
| :---: | :--- | :---: | :---: | :---: | :---: | :---: |
| **RAID 0** | Striping | 2 | **0 discos** (Ninguno) | `(N * C)` (100%) | 🚀 Muy Alto | 🚀 Muy Alto |
| **RAID 1** | Mirroring | 2 | **1 disco** | `(1 * C)` (50%) | 🟢 Alto | 🟡 Medio |
| **RAID 5** | Paridad Distribuida | 3 | **1 disco** | `(N - 1) * C` | 🟢 Alto | 🟡 Medio |
| **RAID 6** | Doble Paridad | 4 | **2 discos** | `(N - 2) * C` | 🟢 Alto | 🔴 Lento (Cálculo) |
| **RAID 10**| Mirroring + Striping | 4 | **1 disco por pareja** | `(N / 2) * C` (50%) | 🚀 Muy Alto | 🚀 Muy Alto |

---

## 8. Gestión de Almacenamiento por Interfaz Gráfica en Windows [Técnica]

* **Administrador de Discos de Windows (`diskmgmt.msc`) [Técnica]:** Herramienta gráfica integrada en el panel de administración que permite consultar, inicializar, particionar, formatear y cambiar la estructura de almacenamiento del sistema.
* **Inicialización de Discos (MBR vs. GPT):**
  * Al conectar un disco nuevo, el Administrador solicita elegir la tabla de particiones: **MBR** (para BIOS heredada o discos < 2 TB) o **GPT** (para sistemas UEFI modernos y discos > 2 TB).

### Discos Básicos vs. Discos Dinámicos [Concepto]
Windows permite gestionar los discos físicos en dos modos operativos:

1. **Discos Básicos [Técnica]:** Modo por defecto. Utilizan tablas de particiones MBR o GPT estándar compuestas por particiones primarias, extendidas y lógicas.
2. **Discos Dinámicos [Técnica]:** Permiten dividir el disco en **volúmenes dinámicos** no contiguos que se pueden extender entre varios discos físicos sin necesidad de reiniciar el sistema.

* **Tipos de Volúmenes Dinámicos en Windows:**
  * **Volumen Simple:** Ocupa espacio dentro de un único disco físico.
  * **Volumen Distribuido:** Une el espacio no asignado de múltiples discos físicos (de 2 a 32 discos) para formar una única letra de unidad de mayor capacidad. No ofrece redundancia.
  * **Volumen Seccionado:** Equivale a **RAID 0** por software. Distribuye los datos entre varios discos aumentando la velocidad.
  * **Volumen Reflejado:** Equivale a **RAID 1** por software. Mantiene dos copias idénticas en dos discos distintos.
  * **Volumen RAID-5:** Equivale a **RAID 5** por software (requiere mínimo 3 discos; disponible en ediciones Windows Server).

> **⚠️ Advertencia de Conversión:** Convertir un disco básico a dinámico es un proceso no destructivo que conserva los datos. Sin embargo, realizar el proceso inverso (convertir de dinámico a básico) **borra permanentemente todos los volúmenes y datos** del disco.

---

## 9. Búsqueda Avanzada de Información [Técnica]

### 9.1. Búsquedas por Línea de Comandos en Linux (`find`, `locate`, `grep`) [Técnica]

#### 1. Comando `find` [Técnica]
El comando `find` busca archivos en tiempo real recorriendo directamente la estructura de directorios del sistema de archivos.

```bash
find [ruta_inicio] [criterio_busqueda] [accion]
```

* **Criterios por Nombre:**
  ```bash
  find /home/usuario -name "informe.pdf"         # Busca un nombre exacto (sensible a mayúsculas)
  find /home/usuario -iname "*.pdf"              # Busca por extensión sin distinguir mayúsculas/minúsculas
  ```

* **Criterios por Profundidad de Directorio:**
  ```bash
  find /etc -maxdepth 2 -iname "network"         # Limita la búsqueda a un máximo de 2 subniveles
  find /var -mindepth 3 -iname "*.log"           # Comienza a buscar a partir del nivel 3 de profundidad
  ```

* **Criterios por Tipo de Fichero (`-type`):**
  ```bash
  find /var/log -type f -name "*.log"            # Muestra solo ficheros regulares (f)
  find /home -type d -name "fotos"               # Muestra solo directorios (d)
  find /dev -type b                              # Muestra solo dispositivos de bloque (b)
  find /lib -type l                              # Muestra solo enlaces simbólicos (l)
  ```

* **Criterios por Tamaño (`-size`):**
  * `+n` : Mayor que n.
  * `-n` : Menor que n.
  * Unidades: `c` (bytes), `k` (KB), `M` (MB), `G` (GB).
  ```bash
  find /var/log -size +100M                      # Busca archivos con un tamaño mayor a 100 MB
  find /tmp -size -10k                           # Busca archivos menores de 10 KB
  ```

* **Criterios por Tiempo y Modificación:**
  * `-mtime -n/+n` : Modificación del contenido del fichero en los últimos n días (o hace más de n días).
  * `-atime -n/+n` : Último acceso al fichero.
  * `-ctime -n/+n` : Último cambio en el i-nodo o permisos.
  ```bash
  find /home -mtime -7                           # Modificados en los últimos 7 días
  ```

* **Criterios por Permisos y Propietario:**
  ```bash
  find /home -user alumno                        # Ficheros pertenecientes al usuario 'alumno'
  find /var/www -perm 777                        # Ficheros con permisos exactos 777 (rwxrwxrwx)
  ```

#### 2. Comando `locate` [Técnica]
Busca nombres de archivos consultando una base de datos indexada en segundo plano (`/var/lib/mlocate/mlocate.db`), ofreciendo una velocidad de respuesta instantánea.

```bash
sudo updatedb                                    # Actualiza la base de datos del sistema manualmente
locate "informe.pdf"                             # Busca rápidamente el archivo en el índice
```

### 9.2. Búsquedas en Windows GUI [Técnica]
El Explorador de archivos de Windows ofrece un cuadro de búsqueda que utiliza el servicio de **Indexación de Windows** (*Windows Search*).
* **Sintaxis de Filtros de Búsqueda Avanzada:**
  * `nombre:informe` : Busca archivos cuyo nombre contenga "informe".
  * `tipo:documento` o `ext:.docx` : Filtra por formato de archivo.
  * `fechamodificacion:ayer` o `fechamodificacion:este mes` : Filtra por rango de fechas.
  * `tamaño:gigante` (>128 MB) o `tamaño:>500MB` : Filtra por peso.
  * **Carpetas Virtuales de Búsqueda:** Permite guardar una búsqueda configurada con múltiples filtros como un acceso directo dinámico que se actualiza automáticamente.

---

## 10. Práctica y Laboratorios (Lab UT03) [Técnica]

### Despliegue Práctico de Entorno Virtualizado (Oracle VM VirtualBox) [Técnica]

Como parte de las actividades prácticas de la asignatura, el alumno debe desplegar una máquina virtual de pruebas con Windows 10/11 o Ubuntu siguiendo las especificaciones del módulo:

1. **Selección e Instalación del Hipervisor:**
   * Descargar e instalar la versión más reciente de **Oracle VM VirtualBox** para el sistema operativo anfitrión (*Host*).

2. **Verificación de Arquitectura CPU e Imagen ISO:**
   * **x64 vs. ARM64:** Verificar en las propiedades del sistema Host si la arquitectura del procesador es **x64** (Intel/AMD tradicional) o **ARM64** (Apple Silicon M1/M2/M3, procesadores Qualcomm/ARM). Descargar exactamente la imagen ISO correspondiente a dicha arquitectura para evitar incompatibilidades durante el arranque.

3. **Configuración de la Máquina Virtual (Guest) y Proceso de Instalación:**
   * **Instalación Desatendida (*Unattended Installation*):** Al crear la máquina virtual en VirtualBox, se recomienda **desmarcar la casilla de instalación desatendida** (*Skip Unattended Installation*) si se desea realizar el proceso de instalación guiado paso a paso y observar la configuración manual completa del sistema operativo.
   * **RAM Asignada:** Aplicar la **Regla del 50% de RAM** (ej. asignar 4096 MB si el Host dispone de 8 u 16 GB), evitando comprometer el rendimiento del sistema anfitrión.
   * **Disco Duro Virtual:**
     * Seleccionar el formato **VDI (VirtualBox Disk Image)**.
     * Tipo de almacenamiento: Reservado dinámicamente.
     * Tamaño asignado: Al menos **80 GB** de espacio para el disco virtual.

4. **Configuración Avanzada de Red en VirtualBox [Técnica]:**
   * **Adaptador Puente (*Bridged Adapter*):** Vincula la interfaz de red virtual directamente a la tarjeta de red física (*NIC*) del equipo anfitrión (*Host*). La máquina virtual obtiene una dirección IP propia dentro de la misma subred local física y funciona como un equipo independiente en la red, disponiendo de acceso directo e inmediato a Internet sin necesidad de configuraciones intermedias.
   * **Red Interna (*Internal Network*):** Crea una red local virtual totalmente aislada entre varias máquinas virtuales alojadas sobre el mismo hipervisor. No tiene acceso a la red física ni a Internet, siendo la opción óptima para simular topologías LAN de laboratorio, realizar pruebas de conectividad entre sistemas invitados o desplegar servicios locales (DHCP/DNS) de forma segura.
   * **Modo NAT (*Network Address Translation*):** Modo predeterminado donde VirtualBox actúa como router con DHCP propio para otorgar salida a Internet a la VM a través del Host, manteniéndola oculta de la red exterior.

5. **Capturas de Evidencias e Interacción con el Cursor:**
   * **Liberación de Cursor (`Ctrl Derecho`):** En VirtualBox, la tecla Host predeterminada es la tecla **`Ctrl` derecho**. Pulsarla permite liberar el ratón atrapado dentro del sistema invitado (*Guest*) para regresar al sistema *Host* y tomar capturas de pantalla limpias del proceso mediante la herramienta *Recortes* de Windows.

6. **Cuestionario de Evaluación Teórico-Práctico del Laboratorio:**
   * **¿Qué es un sistema operativo y cuál es su función principal?** Software que actúa como intermediario entre el hardware y las aplicaciones, gestionando de forma eficiente los recursos del equipo (CPU, RAM, disco, E/S).
   * **¿Qué es la virtualización?** Creación por software de un entorno informático simulado que permite ejecutar múltiples sistemas operativos independientes sobre un único ordenador físico.
   * **Ventajas de instalar un sistema operativo en una VM frente a un equipo físico:**
     1. Pruebas y experimentación seguras sin riesgo de dañar el sistema operativo principal.
     2. Ahorro de costes en hardware adicional.
     3. Portabilidad y capacidad de rollback instantáneo mediante **Instantáneas (Snapshots)**.
