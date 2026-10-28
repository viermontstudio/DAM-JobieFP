🏠 **[Volver al Índice Principal](../../README.md)** | 📐 **[Ir al Esquema Resumen](./ESQUEMA_UT04_configuracion_sistemas_operativos.md)**

---

# ⚙️ GUÍA TEÓRICA Y RESUMEN — UT04: Configuración de Sistemas Operativos
**Asignatura:** Sistemas Informáticos (1º DAM/DAW)  
**Marco Metodológico:** Protocolo PEM-4 & Metodología Interna DAM

---

## 1. Administración de Usuarios y Grupos en Linux
En Linux, la gestión de identidades se basa en tres archivos fundamentales de texto plano en `/etc/`:
* **`/etc/passwd`:** Almacena la lista de usuarios del sistema con la estructura:  
  `usuario:x:UID:GID:Comentario:Home:Shell` (la `x` indica que la contraseña cifrada está en `shadow`).
* **`/etc/shadow`:** Archivo legible únicamente por `root` con las contraseñas cifradas mediante **SHA-512** (prefijo `$6$`) e información de caducidad y expiración.
* **`/etc/group`:** Define los grupos del sistema y sus miembros: `nombre_grupo:x:GID:usuario1,usuario2`.

### Comandos de Gestión CLI:
* `useradd -m -s /bin/bash nuevo_usuario` : Crear usuario con directorio personal y shell por defecto.
* `usermod -aG grupo usuario` : Añadir usuario a un grupo secundario sin eliminarlo de los demás (`-a` append).
* `userdel -r usuario` : Eliminar usuario junto con su directorio personal (`-r`).
* `chage -l usuario` : Modificar o consultar los días de caducidad de contraseña del usuario.

---

## 2. Permisos POSIX y Permisos Especiales
### Estructura de Permisos (Lectura, Escritura, Ejecución)
Los permisos se aplican a tres niveles: **Propietario (*u*)**, **Grupo (*g*)** y **Otros (*o*)**.
* **Lectura (`r` / 4):** Permite ver el contenido de un archivo o listar los ficheros de una carpeta.
* **Escritura (`w` / 2):** Permite modificar o borrar el contenido de un archivo o crear/eliminar ficheros en una carpeta.
* **Ejecución (`x` / 1):** Permite ejecutar un archivo binario/script o **entrar/atravesar un directorio** (¡sin permiso `x` no se puede acceder a un directorio!).

### Comandos `chmod`, `chown` y `chgrp`:
* **Notación Octal:** `chmod 755 archivo` (Propietario=rwx/7, Grupo=r-x/5, Otros=r-x/5).
* **Notación Simbólica:** `chmod u+x,g-w script.sh`.
* **Cambio de Propietario:** `chown -R usuario:grupo /carpeta`.

### Permisos Especiales:
* **SUID (4000 / `u+s`):** Al ejecutar el archivo, el proceso adopta los privilegios del propietario del archivo (ej. `/usr/bin/passwd`).
* **SGID (2000 / `g+s`):** Los archivos creados en un directorio heredan el grupo del directorio en lugar del grupo primario del usuario.
* **Sticky Bit (1000 / `o+t`):** En un directorio compartido (como `/tmp`), solo el propietario de un archivo o `root` pueden borrarlo.

---

## 3. Control y Gestión de Procesos
Un proceso es un programa en ejecución que consume recursos de memoria y CPU, identificado por un **PID (*Process ID*)**.
* **Estados de un Proceso:**  
  * `R` (Running / Runnable) : En ejecución o listo para ejecutar.
  * `S` (Interruptible Sleep) : Esperando un evento o entrada/salida.
  * `D` (Uninterruptible Sleep) : Espera en disco/hardware I/O.
  * `T` (Stopped) : Detenido por señal.
  * `Z` (Zombie) : Proceso finalizado cuya entrada no ha sido leída por el proceso padre.

### Herramientas y Comandos de Monitorización:
* `ps aux` / `ps -ef` : Instantánea de los procesos en ejecución.
* `top` / `htop` : Monitor dinámico e interactivo de CPU, RAM y procesos en tiempo real.
* `pstree` : Árbol jerárquico de procesos (mostrando la raíz `systemd` / PID 1).
* `kill -9 <PID>` : Enviar señal `SIGKILL` (finalización inmediata no capturable).
* `killall <nombre>` : Matar todos los procesos con ese nombre.
* `bg` / `fg` / `jobs` : Control de tareas en segundo plano (*background*) y primer plano (*foreground*).

---

## 4. Automatización de Tareas (`cron` y `systemd`)
El servicio `cron` ejecuta comandos de forma programada periódicamente.
* **Sintaxis de `crontab -e` (5 campos de tiempo):**
  ```text
  ┌───────────── Minuto (0 - 59)
  │ ┌─────────── Hora (0 - 23)
  │ │ ┌───────── Día del Mes (1 - 31)
  │ │ │ ┌────── Mes (1 - 12)
  │ │ │ │ ┌──── Día de la semana (0 - 6, donde 0 es Domingo)
  │ │ │ │ │
  * * * * * comando_a_ejecutar
  ```
  * Ej. `0 2 * * 1-5 /scripts/backup.sh` (Ejecuta a las 2:00 AM de Lunes a Viernes).

---

## 5. Mantenimiento, Optimización y Rendimiento
* **Gestión de Paquetes en Linux (Debian/Ubuntu):**
  * `apt update` : Actualiza el índice local de repositorios.
  * `apt upgrade` : Actualiza los paquetes instalados a su última versión.
  * `apt autoremove` : Limpia dependencias huérfanas sin uso.
* **Análisis de Espacio en Disco:**
  * `df -h` : Muestra el espacio libre/ocupado en los sistemas de archivos montados.
  * `du -sh /var/*` : Muestra el tamaño total consumido por carpetas específicas.

---

🏠 **[Volver al Índice Principal](../../README.md)** | 📐 **[Ir al Esquema Resumen](./ESQUEMA_UT04_configuracion_sistemas_operativos.md)**
