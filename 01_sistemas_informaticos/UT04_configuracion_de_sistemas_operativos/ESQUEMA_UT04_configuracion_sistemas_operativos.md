🏠 **[Volver al Índice Principal](../../README.md)** | 📖 **[Ir a la Guía Teórica (Resumen)](./RESUMEN_UT04_configuracion_sistemas_operativos.md)**

---

---

# 🛠️ ESQUEMA DE ESTUDIO — UT04: Configuración de Sistemas Operativos
**Asignatura:** Sistemas Informáticos (1º DAM/DAW)  
**Marco Metodológico:** Protocolo PEM-4 & Metodología Interna DAM

---

### 🗺️ El Gran Mapa Estructural: Permisos de Seguridad y Ciclo de Vida de Procesos

```text
┌────────────────────────────────────────────────────────────────────────┐
│ 1. ESTRUCTURA DE PERMISOS LINUX (chmod / chown)                        │
│ [Tipo (-/d/l)] [ Propietario (u) ] [ Grupo (g) ] [ Otros (o) ]         │
│  Notación Octal:  Lectura (r=4) + Escritura (w=2) + Ejecución (x=1)   │
│  ⚠️ Carpetas EXIGEN ejecucion (x): chmod 770 (rwxrwx---) NO 660        │
└───────────────────────────────────┬────────────────────────────────────┘
                                    ▼
┌────────────────────────────────────────────────────────────────────────┐
│ 2. CICLO DE VIDA Y ESTADOS DE UN PROCESO LINUX                         │
│ Nuevo ──> Listo (Cola) ──> Ejecución (CPU) ──> Espera (E/S) ──> Terminado │
│                                            └──> Proceso Zombie (Z)    │
└───────────────────────────────────┬────────────────────────────────────┘
                                    ▼
┌────────────────────────────────────────────────────────────────────────┐
│ 3. GESTIÓN Y AUTOMATIZACIÓN (cron vs at)                               │
│ Tareas Periódicas: cron / crontab -e  (5 campos: Min Hora DíaM Mes DíaS)│
│ Tareas Puntuales: at 23:30 / at now + 2 hours                          │
└───────────────────────────────────┬────────────────────────────────────┘
                                    ▼
┌────────────────────────────────────────────────────────────────────────┐
│ 4. MONITORIZACIÓN Y MANTENIMIENTO                                      │
│ Procesos: top / ps aux | Recursos: free -h, df -h | Logs: /var/log/syslog │
└────────────────────────────────────────────────────────────────────────┘
```

---

### 🧱 Bloques Lógicos Funcionales

#### 1. Usuarios y Grupos en Linux (CLI)
* **Identificadores:** Todo proceso e identidad tiene un **UID** (*User ID*) y **GID** (*Group ID*). El usuario `root` tiene **UID 0**.
* **Ficheros Críticos en `/etc`:**
  * **/etc/passwd:** 7 campos (`login:x:UID:GID:comentario:home:shell`).
  * **/etc/shadow:** Contraseñas cifradas en **SHA-512** (identificado con el prefijo **`$6$`**) y parámetros de expiración. Permiso exclusivo de `root`. Significado de **`!`**: Cuenta bloqueada.
  * **/etc/group:** Define grupos y miembros secundarios.
  * **/etc/skel:** Plantilla copiada al crear el directorio `/home/usuario`.
* **Comandos de Cuentas:**
  * `useradd -m -s /bin/bash usuario1`: Crea cuenta forzando creación de `/home` (**M**ake-home) y asignando Shell.
  * `usermod -aG grupoSec usuario`: Añade usuario a grupo secundario (**A**ppend **G**roup).
  * `chage -M 90 usuario`: Modifica expiración (**M**ax-days) de contraseña en `/etc/shadow`.
  * `userdel -r usuario`: Elimina usuario y borra su `/home` (**R**emove).

---

#### 2. Permisos y Seguridad Local en Linux
* **Notación Octal de Permisos (`r=4`, `w=2`, `x=1`):**
  * `7` = `rwx` (Lectura, escritura y ejecución).
  * `6` = `rw-` (Lectura y escritura).
  * `5` = `r-x` (Lectura y ejecución).
  * `4` = `r--` (Solo lectura).
* **⚠️ Regla Inflexible de Examen (chmod 770 vs 660 en Carpetas):**
  * Las carpetas **requieren obligatoriamente la ejecución (`x=1`)** para poder entrar en ellas (`cd`), listar su contenido o navegar.
  * Asignar `660` (`rw-rw----`) a una carpeta provoca error de *Permiso denegado*. Para dar lectura y escritura funcionales a un grupo en una carpeta se exige **`chmod 770` (`rwxrwx---`)**.
* **Comandos de Acceso:**
  * `chmod 755 script.sh`: Otorga todos los permisos al dueño y lectura/ejecución al resto.
  * `chown usuario:grupo archivo`: Modifica propietario y grupo.
  * `umask 0022`: Resta permisos iniciales. Asigna por defecto 644 a archivos y 755 a carpetas.

---

#### 3. Gestión de Usuarios y Seguridad en Windows
* **Base SAM:** Almacena cuentas locales en el equipo local.
* **Herramientas de Administración:**
  * **GUI:** `lusrmgr.msc` (*Local Users and Groups*).
  * **CMD/PowerShell:** `net user usuario1 clave /add`, `net user empleado *` (cambio interactivo), `net localgroup Administradores usuario /add`.
* **UAC (*User Account Control*):** Control de cuentas que solicita confirmación antes de elevar privilegios.

---

#### 4. Gestión de Procesos y Planificación
* **Conceptos:** Proceso identificado por **PID** y su padre **PPID**.
* **Estado Zombie (Z):** Proceso que ha finalizado su ejecución pero cuyo padre no ha recogido aún su código de salida.
* **Comandos de Control:**
  * `ps aux` / `ps -ef`: Muestra instantánea de procesos activos.
  * `top`: Monitor interactivo en tiempo real ordenado por CPU/RAM.
  * `kill -9 <PID>`: Envia la señal **SIGKILL** para terminar incondicionalmente un proceso.
  * `nice` / `renice`: Ajusta prioridad (de -20 máxima prioridad a 19 mínima).
  * `systemctl status|start|stop <servicio>`: Administra demonios systemd.

---

#### 5. Automatización y Monitorización de Recursos
* **Sintaxis de 5 campos en `crontab -e`:**
  ```text
  Minuto (0-59)  Hora (0-23)  Día_Mes (1-31)  Mes (1-12)  Día_Semana (0-6)  Comando
  ```
  * *Ejemplo:* `0 2 * * * /backup.sh` (Ejecuta a las 02:00 todos los días).
* **Monitorización CLI:**
  * `free -h`: Estado de memoria RAM y SWAP en formato humano.
  * `df -h`: Espacio libre en disco por partición montada.
  * `uptime`: Tiempo de actividad y carga media (*load average*).
  * `apt autoremove`: Limpia automáticamente dependencias huérfanas en Debian/Ubuntu.
  * `BleachBit`: Herramienta gráfica multiplataforma para limpieza de temporales y privacidad.

---

### 📖 Glosario de Siglas — UT04

| Sigla | Nombre Completo en Inglés | Traducción / Función en 5 Palabras |
| :--- | :--- | :--- |
| **UID** | *User Identifier* | Número de identificación de usuario. |
| **GID** | *Group Identifier* | Número de identificación de grupo. |
| **PAM** | *Pluggable Authentication Modules* | Módulos de autenticación flexible Linux. |
| **UAC** | *User Account Control* | Control de elevación privilegios Windows. |
| **PID** | *Process Identifier* | Identificador único de proceso activo. |
| **PPID** | *Parent Process Identifier* | PID del proceso padre creador. |
| **PCB** | *Process Control Block* | Bloque de control de estado del proceso. |
| **SAM** | *Security Account Manager* | Base de datos usuarios locales Windows. |
| **SKEL** | *Skeleton* | Directorio plantilla para nuevos usuarios. |

---

🏠 **[Volver al Índice Principal](../../README.md)** | 📖 **[Ir a la Guía Teórica (Resumen)](./RESUMEN_UT04_configuracion_sistemas_operativos.md)**
