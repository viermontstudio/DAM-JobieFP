# 🛠️ UT04 — Configuración de Sistemas Operativos

## 1. Gestión de Usuarios y Grupos en Linux (CLI) [Concepto]

* **Identidad Digital y Filosofía FHS [Concepto]:** En Linux, toda acción o proceso es ejecutado por una identidad digital compuesta por un **UID** (**U**ser **ID**entifier) y un **GID** (**G**roup **ID**entifier). El superusuario `root` ostenta de forma reservada el **UID 0** con privilegios y control total sobre el sistema.
* **Ficheros Fundamentales de Configuración [Técnica]:**
  * **`/etc/passwd`** (**Passw**or**d**): Fichero de texto legible por todos los usuarios que almacena la información básica de las cuentas en 7 campos separados por dos puntos (`:`):
    `login:x:UID:GID:comentario:home:shell`
    *(La `x` en el campo 2 indica que la contraseña cifrada reside en `/etc/shadow`).*
  * **`/etc/shadow`** (**Shadow** Passwords): Archivo con permisos de lectura restringidos exclusivamente a `root` que almacena las contraseñas cifradas mediante *hash* (usando por defecto el algoritmo seguro **SHA-512**, el cual se identifica en el fichero con el prefijo **`$6$`** al inicio del hash) y los parámetros de caducidad y expiración de la cuenta.
  * **`/etc/group`** (**Group**): Define los grupos del sistema y sus miembros en 4 campos (`nombre:x:GID:usuarios_secundarios`).
  * **`/etc/skel`** (**Skel**eton): Directorio plantilla cuyo contenido se copia automáticamente al directorio personal (`/home/usuario`) al crear un usuario nuevo.
* **Cuentas de Sistema vs. Cuentas Humanas [Concepto]:**
  * **Cuentas de Servicio/Sistema:** Creadas automáticamente para ejecutar demonios y servicios con mínimos privilegios (`nobody`, `adm` para acceso a logs, `tty`, `lpadmin`). No inician sesión interactiva.
  * **Cuentas Humanas:** Pertenecen a usuarios reales (UID >= 1000 en sistemas Debian/Ubuntu).
* **Comandos de Administración de Cuentas y Grupos [Técnica]:**
  * **`useradd`** (**User** **Add**): `useradd -g <grupo_principal> -G <grupos_sec> -d <home> -m -s <shell> <login>`
    * `-g` (**g**roup): Asigna el grupo principal.
    * `-G` (**G**roup): Lista de grupos secundarios separados por comas.
    * `-d` (**d**irectory): Define la ruta del directorio personal (`home`).
    * `-m` (**m**ake home): Fuerza la creación del directorio personal y copia los archivos de `/etc/skel`.
    * `-s` (**s**hell): Establece el intérprete de comandos por defecto (ej. `/bin/bash`).
  * **`usermod`** (**User** **Mod**ify): Modifica parámetros de cuentas existentes:
    * `-c` (**c**omment): Modifica el campo de información personal/comentario.
    * `-e` (**e**xpiration): Establece la fecha de caducidad o expiración de la cuenta.
    * `-L` (**L**ock): Bloquea la cuenta impidiendo el acceso.
    * `-U` (**U**nlock): Desbloquea la cuenta.
    * `-l` (**l**ogin): Cambia el nombre de usuario (*login*).
  * **`userdel -r`** (**User** **Del**ete - **r**emove home): Elimina la cuenta de usuario y borra de forma recursiva su directorio personal.
  * **`groupadd -g <GID>`** (**Group** **Add**), **`groupmod -n`** (**Group** **Mod**ify **n**ame) y **`groupdel`** (**Group** **Del**ete).
  * **`who`** (**Who** is logged in): Lista los usuarios conectados en tiempo real:
    * `-u` (**u**sers info): Muestra detalles adicionales de sesión.
    * `-H` (**H**eaders): Añade cabeceras a la salida.
    * `-q` (**q**uick count): Muestra únicamente los *logins* y el recuento total.

---

## 2. Seguridad, Autenticación y Permisos Locales en Linux [Técnica]

* **Linux-PAM y Gestión de Contraseñas [Técnica]:** **Linux-PAM** (**P**luggable **A**uthentication **M**odules) centraliza y modula la autenticación.
  * **`passwd`** (**Passw**or**d**): Actualiza la contraseña cifrada en `/etc/shadow`.
  * **`chage -l`** (**Ch**ange **Age** - **l**ist): Audita los parámetros de caducidad y expiración de contraseñas.
* **Niveles y Notación de Permisos [Concepto]:**
  * Tres niveles de usuario: **Propietario/Dueño (`u` - user)**, **Grupo (`g` - group)** y **Otros (`o` - others)**.
  * Tres permisos básicos: **Lectura (`r` - read = 4)**, **Escritura (`w` - write = 2)** y **Ejecución (`x` - execute = 1)**.

```text
  -     r w -     r - -     r - -
 ───   ───────   ───────   ───────
  │       │         │         │
  │       │         │         └─ OTROS (o - others)      ──> Permiso: Solo Lectura (r--)
  │       │         └─ GRUPO (g - group)        ──> Permiso: Solo Lectura (r--)
  │       └─ PROPIETARIO / DUEÑO (u - user) ──> Permisos: Lectura y Escritura (rw-)
  └─ TIPO DE ARCHIVO (- = Fichero regular, d = Directorio, l = Enlace)
```
* **Comandos de Control de Acceso [Técnica]:**
  * **`chmod`** (**Ch**ange **Mod**e): Cambia los permisos mediante notación simbólica (`chmod go+w archivo`) o numérica octal *(donde 7=rwx, 6=rw-, 5=r-x, 4=r--; ej. `chmod 755 script.sh` otorga todos los permisos al dueño y lectura/ejecución al resto).* 
  * **`chown`** (**Ch**ange **Own**er): Modifica el usuario propietario (`chown usuario archivo`).
  * **`chgrp`** (**Ch**ange **Gr**ou**p**): Modifica el grupo propietario (`chgrp grupo archivo`).
  * **`umask`** (**U**ser **Mask**): Define la máscara de permisos por defecto al crear nuevos ficheros/directorios. Resta valores sobre la base `666` (archivos) o `777` (directorios). Una `umask 0022` asigna permisos iniciales `644` para ficheros y `755` para carpetas.
* **Entorno y Perfiles de Usuario [Técnica]:**
  * **Archivos Globales:** `/etc/profile` (shell de inicio/login) y `/etc/bash.bashrc` (shell Bash interactivo global).
  * **Archivos Locales:** `~/.bashrc` (shell interactivo de usuario) y `~/.profile`.
  * **Variables y Alias:** `export VAR=valor` (**Export** variable de entorno global), `unset VAR` (**Unset** eliminar variable), `env` (**Env**ironment list), `alias cls='clear'` y `unalias`.

---

## 3. Gestión de Usuarios y Seguridad en Windows (GUI y CLI) [Técnica]

* **Tipos de Cuentas y Perfiles [Concepto]:**
  * **Cuentas Locales:** Creadas y almacenadas exclusivamente en la base de datos SAM del equipo local.
  * **Cuentas Globales / de Dominio:** Centralizadas en Active Directory para entornos corporativos.
  * **Perfiles:** Almacenan el entorno de trabajo (`%HOMEPATH%`). Pueden ser locales, **móviles** (roaming - sincronizados en red) u **obligatorios** (read-only).
* **Grupos Locales Predeterminados [Concepto]:** `Administradores` (control total), `Usuarios` (estándar, sin permisos de instalación), `Invitados` (acceso temporal mínimo) y `Usuarios avanzados`.
* **Herramientas de Gestión en Windows [Técnica]:**
  * **GUI:** `Configuración → Cuentas → Familia y otros usuarios` y consola **`lusrmgr.msc`** (**L**ocal **Usr** / **Us**e**r** **M**ana**g**e**m**en**t** - disponible en Windows Pro).
  * **CLI (CMD / PowerShell):**
    * `net user <usuario> <contraseña> /add` (Crear cuenta local).
    * `net user <usuario> /active:no` (Deshabilitar cuenta).
    * `net user <usuario> /delete` (Eliminar cuenta).
    * `net localgroup <grupo> <usuario> /add` (Añadir usuario a grupo).
* **Seguridad y Control de Acceso:**
  * **UAC** (**U**ser **A**ccount **C**ontrol): Solicita confirmación o credenciales administrativas antes de realizar cambios críticos o instalar aplicaciones.

---

## 4. Gestión y Planificación de Procesos en Linux (CLI) [Técnica]

* **Concepto de Proceso y Estructura PCB [Concepto]:** Instancia de un programa en ejecución. Identificado por su **PID** (**P**rocess **ID**entifier) y su **PPID** (**P**arent **P**rocess **ID**entifier). Su **PCB** (**P**rocess **C**ontrol **B**lock) almacena su estado, propietario, uso de memoria y descriptores abiertos.
* **Ciclo de Vida y Estados de un Proceso [Concepto]:**
  * **Nuevo (New):** Creación e inicialización.
  * **Listo (Ready):** Preparado en cola esperando asignación de CPU.
  * **Ejecución (Running):** Instrucciones procesándose en la CPU.
  * **Espera/Bloqueado (Sleeping/Waiting):** Esperando un evento de E/S.
  * **Terminado (Terminated):** Finalizado. Si finalizó pero su padre no ha recogido su código de salida, permanece como **Zombie (Z)**.
* **Niveles de Planificadores [Técnica]:**
  * **Largo Plazo:** Controla la admisión de procesos y los envía a la cola de listos.
  * **Medio Plazo:** Suspende o reactiva procesos gestionando el intercambio (*swapping*) de memoria.
  * **Corto Plazo:** Asigna la CPU a los procesos listos según la política activa.
* **Políticas de Planificación [Concepto]:** **FIFO** (First-In, First-Out), **SJF** (Shortest Job First), **Prioridades**, **Round-Robin** (asignación por *quantum* o turno de tiempo) y **Retroalimentación multinivel**.
* **Comandos de Control de Procesos [Técnica]:**
  * **`ps`** (**P**rocess **S**tatus): Muestra el estado puntual de los procesos:
    * `ps aux`: Muestra todos los procesos (`a` = **a**ll users, `u` = **u**ser format, `x` = procesos sin terminal) con uso de CPU y RAM.
    * `ps -ef`: Lista completa con formato estructurado (`-e` = **e**very, `-f` = **f**ull).
  * **`top`** (**T**able **O**f **P**rocesses): Monitor interactivo dinámico en tiempo real.
  * **`kill`** / **`killall`**: Envía señales a procesos. *(Ejemplo: `kill -9 <PID>` envía la señal `SIGKILL` para forzar la terminación inmediata e incondicional del proceso).* 
  * **`nice`** / **`renice`**: Modifica la prioridad de ejecución (de `-20` máxima prioridad a `19` mínima).
  * **`systemctl`** (**System** **C**on**tr**o**l**): Administra servicios del sistema (`systemctl status|start|stop|restart <servicio>`).

---

## 5. Gestión de Procesos en Windows (GUI) [Técnica]

* **Administrador de Tareas (`Ctrl + Shift + Esc`) [Técnica]:** Herramienta centralizada para la monitorización gráfica de procesos.
  * **Procesos:** Muestra aplicaciones, procesos en segundo plano y servicios con su uso de CPU, RAM, Disco y Red.
  * **Rendimiento:** Gráficas en tiempo real de uso de hardware.
  * **Aplicaciones de arranque / Inicio:** Permite habilitar/deshabilitar programas que arrancan con el sistema.
  * **Detalles / Servicios:** Muestra PID, usuario ejecutor y estado de servicios del sistema.

---

## 6. Automatización de Tareas en Linux [Técnica]

* **Tareas Periódicas (`cron` / `crontab`) [Técnica]:**
  * **`cron`** (**Chron**os): Demonio de ejecución periódica.
  * **`crontab -e`** (**Cron** **Tab**le - **e**dit): Edita la tabla de tareas del usuario.
  * **Sintaxis de 5 campos:** `Minuto (0-59) Hora (0-23) Día_Mes (1-31) Mes (1-12) Día_Semana (0-6) Comando`.
* **Tareas Puntuales (`at`) [Técnica]:**
  * **`at`**: Programa la ejecución única de una tarea en un momento concreto (`at 23:30`, `at now + 2 hours`).

---

## 7. Monitorización de Recursos y Gestión de Logs [Técnica]

* **Comandos de Monitorización en Linux [Técnica]:**
  * **`free -h`**: Muestra la memoria RAM física y SWAP usada/libre en formato **h**umano legible.
  * **`df -h`** (**D**isk **F**ree): Muestra el espacio ocupado y libre en las unidades montadas.
  * **`uptime`**: Muestra el tiempo encendido del sistema y la carga media (*load average*).
  * **`vmstat`** (**V**irtual **M**emory **Stat**istics) e **`iostat`** (**I**nput/**O**utput **Stat**istics).
  * **`sar`** (**S**ystem **A**ctivity **R**eporter): Recopila y analiza informes históricos de rendimiento.
* **Gestión e Inspección de Logs [Técnica]:**
  * Directorio centralizado: **`/var/log`** (**Var**iable **Log**s).
  * Ficheros clave: `/var/log/auth.log` (autenticación y accesos), `/var/log/syslog` (eventos generales) y `/var/log/dmesg` (mensajes del kernel durante el arranque).
  * **`tail -f <log>`** (**f**ollow): Muestra las últimas líneas del archivo y se actualiza en tiempo real.
  * **`journalctl`** (**Journal** **C**on**tr**o**l**): Consulta el registro unificado del sistema mediante `systemd`.

---

## 8. Mantenimiento y Optimización del Sistema [Técnica]

* **Optimización en Windows:** Liberador de espacio en disco, Desfragmentador para discos mecánicos (HDD) vs. comando **TRIM** automático para unidades de estado sólido (**SSD**).
* **Optimización en Linux:**
  * **`fsck`** (**F**ile **S**ystem **C**hec**k**): Verificación y reparación de sistemas de archivos.
  * **`apt autoremove`**: Elimina automáticamente paquetes y dependencias obsoletas no utilizadas.
  * **`BleachBit`**: Aplicación multiplataforma para la limpieza de temporales y memoria caché.
