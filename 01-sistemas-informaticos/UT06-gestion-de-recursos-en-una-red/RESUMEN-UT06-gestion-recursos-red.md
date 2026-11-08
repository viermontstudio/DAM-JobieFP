🏠   **[Volver al Índice Principal](../../README.md)**   | 📐   **[Ir al Esquema Resumen](./ESQUEMA-UT06-gestion-recursos-red-v2.md)**

--------------------------------------------------------------------------------

###### 🛡️ GUÍA TEÓRICA Y RESUMEN — UT06: Gestión de Recursos en una Red (v2)
**Asignatura:**   Sistemas Informáticos (1º DAM/DAW)  
**Marco Metodológico:**   Protocolo PEM-4 & Metodología Interna DAM  
**Documento Actualizado:**   Incorpora transcripción del vídeo de impacto profesional (Doc 04A), procedimiento de compartición, rutas UNC y regla de la doble puerta.

--------------------------------------------------------------------------------

###### 1. Acreditación de Usuarios, Permisos y Rutas de Red
En la administración de sistemas corporativos, la gestión del acceso garantiza que cada usuario disponga de los niveles de autorización requeridos sin comprometer la seguridad ni la integridad del sistema.

###### Acreditación y Token de Seguridad (SAT)
*   **Security Access Token (SAT):**   Identificador único y "pase" de seguridad generado por el sistema operativo cuando un usuario autentica su inicio de sesión en Windows.
*   **Componentes del SAT:**
    *   **SID (Security Identifier) de Usuario:**   Identificador alfanumérico único asociado a la cuenta.
    *   **SIDs de Grupos:**   Lista de identificadores de todos los grupos de seguridad a los que pertenece el usuario.
    *   **Lista de Privilegios:**   Permisos y derechos asignados directamente o heredados.
*   **Inmutabilidad de la Sesión:**   El token se vincula al proceso en el momento del inicio de sesión. Si se modifican los grupos o privilegios de un usuario, los cambios no surtirán efecto en la sesión activa; requiere cerrar y volver a iniciar sesión.

###### Permisos de Recurso Compartido vs. Permisos NTFS (Metáfora de la Doble Puerta)
*   **Permisos de Recurso Compartido (Puerta 1 - Perímetro de Red):**   Regulan el acceso remoto a través de la red local (SMB/CIFS). Se configuran desde *Uso compartido avanzado* y ofrecen niveles de *Lectura*, *Cambio* y *Control Total*.
*   **Permisos NTFS (Puerta 2 - Disco Local):**   Permisos granulares aplicados directamente en el sistema de archivos local (pestaña *Seguridad*). Controlan el acceso tanto local como por red a archivos y carpetas individuales (*Lectura*, *Escritura*, *Modificación*, *Lectura y ejecución*, *Control Total*).
*   **Regla de Combinación (El más restrictivo gana):**   Para acceder a un archivo por red, el usuario debe atravesar ambas puertas. El permiso efectivo final es siempre **el resultado más restrictivo** entre los permisos compartidos y los permisos NTFS.
*   **Principio de Mínimo Privilegio:**   Regla de oro de seguridad que establece que cada usuario o grupo debe recibir únicamente los permisos estrictamente necesarios para realizar su trabajo (ej. si solo necesita consultar un informe, se asigna exclusivamente permiso de *Lectura*).

###### Rutas de Acceso en Red: Rutas UNC vs. URIs Samba
*   **Ruta UNC (Universal Naming Convention - Windows):**   Estructura estandarizada para acceder a recursos compartidos en redes Microsoft mediante la sintaxis `\\NombreEquipo\NombreRecurso` o `\\DireccionIP\NombreRecurso` (ej. `\\SERVIDOR01\UT6_Compartida`).
*   **Ruta URI en Linux (Samba / GVFS):**   Sintaxis utilizada en sistemas Linux/Ubuntu para conectar con servidores SMB mediante la URI `smb://<IP>/<Recurso>` (ej. `smb://10.0.0.11/UT6_Compartida`).

--------------------------------------------------------------------------------

###### 2. Herencia de Permisos, Grupos y Listas de Control de Acceso (ACL)
Los volúmenes NTFS organizan la seguridad de los archivos y carpetas mediante estructuras jerárquicas de control de acceso.

###### Permisos Múltiples por Grupos y Prevalencia de Denegar Explícito
*   **Combinación Acumulativa:**   Cuando un usuario pertenece a múltiples grupos (ej. *Empleados* y *Administración*), Windows combina de forma acumulativa los permisos concedidos a cada grupo.
*   **Botón de Pánico (Denegar Explícito):**   Si existe un conflicto entre una regla que permite (*Allow*) y una entrada que deniega explícitamente (*Explicit Deny*), **la denegación prevalece siempre**, anulando cualquier permiso positivo asignado al usuario o a sus grupos.

###### Herencia de Permisos NTFS
*   **Propagación Automática:**   Por defecto, los archivos y subcarpetas heredan automáticamente los permisos definidos en la carpeta contenedora superior (carpeta padre). Esto evita configurar manualmente cientos de archivos individuales.
*   **Ruptura de Herencia:**   Cuando una subcarpeta requiere restricciones especiales, la herencia puede deshabilitarse en *Seguridad → Opciones Avanzadas*:
    *   **Convertir permisos heredados en explícitos:**   Copia la lista actual permitiendo modificarla individualmente.
    *   **Quitar todos los permisos heredados:**   Elimina las entradas dejando la lista en blanco para definir accesos desde cero.

###### Estructura de las Listas de Control de Acceso (ACL)
Cada objeto en NTFS posee un propietario (SID) y una **ACL (Access Control List)** compuesta por entradas **ACE (Access Control Entries)**:
*   **DACL (Discretionary Access Control List):**   Define qué usuarios o grupos tienen permisos de lectura, escritura, modificación o control total sobre el recurso.
*   **SACL (System Access Control List):**   Define qué acciones (lectura, modificación, borrado) o intentos fallidos deben ser auditados en el visor de eventos de Windows para investigación forense.

--------------------------------------------------------------------------------

###### 3. Procedimiento Metodológico de Compartición de Recursos
Para evitar configurar permisos mediante "prueba y error", se aplica un protocolo sistemático de 6 pasos en la administración de redes:

1.  **Análisis de Necesidades y Usuarios:**   Identificar qué usuarios necesitan acceder y aplicar el principio de mínimo privilegio.
2.  **Configuración del Recurso Compartido:**   Habilitar *Compartir esta carpeta* en *Uso compartido avanzado*, definir el nombre de red y asignar permisos de red (ej. *Lectura*).
3.  **Configuración de Permisos NTFS Locales:**   Ajustar los permisos en la pestaña *Seguridad* asignando reglas específicas a usuarios o grupos en la DACL.
4.  **Evaluación de la Herencia:**   Verificar si los permisos se propagan correctamente a las subcarpetas o si se debe romper la herencia para aislar contenidos confidenciales.
5.  **Cálculo del Permiso Efectivo:**   Comprobar la combinación de ambos niveles de seguridad (Regla de la doble puerta: el más restrictivo prevalece).
6.  **Verificación Práctica:**   Validar la conectividad y las capacidades de edición probando el acceso desde un equipo cliente con la cuenta de un usuario real.

--------------------------------------------------------------------------------

###### 4. Derechos de Usuario y Privilegios
Es fundamental diferenciar entre permisos (que se aplican a recursos) y derechos/privilegios (que afectan a capacidades globales del sistema operativo).

###### Clasificación de Derechos y Privilegios
*   **Derechos de Conexión:**   Regulan las vías de entrada al equipo (ej. *Permitir/Denegar inicio de sesión local*, *Permitir/Denegar acceso desde la red*).
*   **Privilegios del Sistema:**   Autorizan a ejecutar acciones administrativas e internas del sistema (ej. *Apagar el sistema*, *Realizar/Restaurar copias de seguridad*, *Cargar/Desinstalar controladores*, *Unir equipos al dominio*).
*   **Prioridad Inflexible:**   Si existe un conflicto directo entre un permiso de recurso y un derecho de sistema, **el derecho prevalece siempre** sobre el permiso (ej. el derecho de backup permite copiar archivos aunque la DACL de NTFS deniegue el acceso).

--------------------------------------------------------------------------------

###### 5. Directivas de Seguridad Locales y de Dominio
Las directivas de seguridad establecen el comportamiento normativo y la configuración de seguridad centralizada de los equipos.

###### Ámbito de Aplicación de Directivas
*   **Directivas de Seguridad Local (secpol.msc):**   Se aplican individualmente en equipos Windows sin entorno de dominio Active Directory.
*   **Directivas de Grupo en Dominio / GPO (gpmc.msc):**   En redes corporativas con Active Directory (Windows Server), las GPO (*Group Policy Objects*) se aplican de forma centralizada a dominios, sitios o Unidades Organizativas (OU), distribuyendo configuraciones a miles de clientes automáticamente.

--------------------------------------------------------------------------------

###### 6. Servidores de Ficheros, Impresión e Interoperabilidad Heterogénea
Los servidores centralizan los recursos de la red para garantizar su disponibilidad, escalabilidad y mantenimiento continuo.

###### Servidores de Ficheros (FTP / FTPS / SFTP / SMB)
*   **Principios de Servidores:**   Disponibilidad (operatividad continua), Escalabilidad (capacidad de crecimiento) y Mantenimiento preventivo.
*   **Servidor FTP (Internet Information Services - IIS):**
    *   **FTP estándar (Puerto 21/TCP):**   Transfiere archivos en texto plano sin cifrado.
    *   **FTPS (FTP Secure):**   Añade capa de cifrado mediante certificados TLS/SSL.
    *   **SFTP (SSH File Transfer Protocol):**   Corre sobre el protocolo **SSH (Puerto 22/TCP)**; es un protocolo completamente distinto y altamente seguro.
*   **Protocolo SMB / CIFS (Puerto 445/TCP y 139/TCP):**   Estándar de compartición de recursos nativo en Windows para redes locales.

###### Interoperabilidad Heterogénea Windows - Linux (Práctica de Laboratorio)
1.  **Configuración Avanzada de Red en Windows:**
    *   Acceso desde *Panel de control ➔ Centro de redes y recursos compartidos ➔ Cambiar configuración de uso compartido avanzado*.
    *   **Detección de redes y uso compartido:**   Activar *Detección de redes* y *Uso compartido de archivos e impresoras*.
    *   **Protección por contraseña:**   Desactivar opcionalmente la *Protección por contraseña* para recursos públicos o exigir credenciales locales de Windows (ej. `invita2`).
2.  **Acceso e Integración desde Linux (Ubuntu / Samba):**
    *   Instalación de paquetes Samba de cliente/servidor (`sudo apt install samba`).
    *   Conexión mediante el explorador de archivos GUI (Nautilus) usando la ruta URI: `smb://<IP_Windows>/<Ruta_Recurso>` (ej. `smb://10.0.0.11/Users/eusko/Desktop/Carpeta Compartida`).
    *   Montaje dinámico en el sistema de archivos virtual GVFS de Linux (`/run/user/$UID/gvfs/smb-share:server=...`).
    *   Operatividad CLI desde la terminal mediante `ls -l`, `cat` y `touch prueba.txt` para comprobar permisos efectivos de lectura/escritura.
3.  **Auditoría de Sockets y Conectividad:**
    *   Prueba de conectividad de Capa 3 mediante `ping <IP_Windows>`.
    *   Inspección de sockets activos en Windows con `netstat -ab` desde la consola de Administrador y `sudo netstat -tulnp` en Ubuntu para confirmar el estado `LISTENING` sobre los puertos **445/TCP** (SMB) y **139/TCP** (NetBIOS).

###### Servidores de Impresión
*   **Tipos:**   Servidor externo (equipo dedicado que gestiona colas de impresión) o servidor interno (tarjeta de red integrada en la propia impresora).
*   **Administración de Impresión (printmanagement.msc):**   Centraliza controladores, puertos IP y colas de *Print Spooler*.

--------------------------------------------------------------------------------

###### 7. Conexión Remota y Administración Centralizada
La administración remota permite gestionar servidores e infraestructura sin presencia física.

###### Herramientas Nativas de Conexión Remota
*   **RDP (Remote Desktop Protocol - Puerto 3389/TCP):**   Toma el control completo de la sesión gráfica de un servidor o cliente.
*   **Servicios de Escritorio Remoto (RDS):**   Habilita múltiples sesiones virtuales concurrentes en servidores corporativos.
*   **Asistencia Remota (Quick Assist / Asistencia Rápida):**   Permite compartir pantalla en tiempo real con un usuario para soporte técnico colaborativo sin cerrar su sesión.

###### Arquitectura Segura de Acceso Remoto
*   **Jump Servers / Bastion Hosts:**   Servidores intermedios acorazados como único punto de entrada.
*   **MFA (Multifactor Authentication):**   Exige un segundo factor de verificación.

--------------------------------------------------------------------------------

###### 8. Criptografía, Cortafuegos y Seguridad Perimetral
La protección en profundidad combina cifrado de datos y filtrado de tráfico perimetral.

###### Algoritmos Criptográficos
*   **Cifrado Simétrico:**   AES (128/192/256 bits) como estándar global actual; DES y TDES (obsoletos).
*   **Cifrado Asimétrico:**   Par de claves pública (cifra) y privada (descifra) mediante RSA, DSA o ECC.
*   **Cifrado Híbrido:**   Asimétrico para intercambiar la clave simétrica de sesión (modelo TLS/HTTPS).

###### Cortafuegos (Firewalls)
*   **Mecanismo:**   Inspecciona paquetes de datos entrantes (*Input*), salientes (*Output*) y reenviados (*Forward*).
*   **Herramientas:**   Windows Defender Firewall con seguridad avanzada (`wf.msc`) vs. soluciones perimetrales dedicadas (**pfSense** / **MikroTik**).

--------------------------------------------------------------------------------

🏠   **[Volver al Índice Principal](../../README.md)**   | 📐   **[Ir al Esquema Resumen](./ESQUEMA-UT06-gestion-recursos-red-v2.md)**
