🏠 **[Volver al Índice Principal](../../README.md)** | 📐 **[Ir al Esquema Resumen](./ESQUEMA_UT06_gestion_recursos_red.md)**

---

### 🛡️ GUÍA TEÓRICA Y RESUMEN — UT06: Gestión de Recursos en una Red
**Asignatura:** Sistemas Informáticos (1º DAM/DAW)  
**Marco Metodológico:** Protocolo PEM-4 & Metodología Interna DAM  

---

#### 1. Permisos y Acreditación de Usuarios en Windows
En la administración de sistemas corporativos, la gestión del acceso garantiza que cada usuario disponga de los niveles de autorización requeridos sin comprometer la seguridad ni la integridad del sistema.

##### Acreditación y Token de Seguridad (SAT)
* **Security Access Token (SAT):** Identificador único y "pase" de seguridad generado por el sistema operativo cuando un usuario autentica su inicio de sesión en Windows.
* **Componentes del SAT:**
  * **SID (Security Identifier) de Usuario:** Identificador alfanumérico único asociado a la cuenta.
  * **SIDs de Grupos:** Lista de identificadores de todos los grupos de seguridad a los que pertenece el usuario.
  * **Lista de Privilegios:** Permisos y derechos asignados directamente o heredados.
* **Inmutabilidad de la Sesión:** El token se vincula al proceso en el momento del inicio de sesión. Si se modifican los grupos de un usuario, los cambios no surtirán efecto hasta que el usuario cierre y vuelva a iniciar sesión.

##### Permisos de Recurso Compartido vs. Permisos NTFS
* **Permisos de Recurso Compartido:** Regulan el acceso remoto a través de la red local (SMB/CIFS). Se aplican de forma global a la carpeta compartida y sus subcarpetas.
* **Permisos NTFS:** Permisos granulares aplicados directamente en el sistema de archivos local. Controlan el acceso tanto local como por red a archivos y carpetas individuales.
* **Regla de Combinación (El más restrictivo gana):** Cuando un usuario accede a un recurso por red, el sistema operativo evalúa los permisos compartidos y los permisos NTFS. El permiso efectivo final es siempre **el más restrictivo** entre ambos.

---

#### 2. Herencia de Permisos y Listas de Control de Acceso (ACL)
Los volúmenes NTFS organizan la seguridad de los archivos y carpetas mediante estructuras jerárquicas de control de acceso.

##### Herencia de Permisos NTFS
* **Propagación Automática:** Por defecto, los archivos y subcarpetas heredan automáticamente los permisos definidos en la carpeta contenedora superior (carpeta padre).
* **Ruptura de Herencia:** Cuando una subcarpeta requiere restricciones especiales, la herencia puede deshabilitarse en la pestaña *Seguridad → Opciones Avanzadas*:
  * **Convertir permisos heredados en explícitos:** Copia la lista actual permitiendo modificarla individualmente.
  * **Quitar todos los permisos heredados:** Elimina las entradas dejando la lista en blanco para definir accesos desde cero.

##### Estructura de las Listas de Control de Acceso (ACL)
Cada objeto en NTFS posee un propietario (SID) y una **ACL (Access Control List)** compuesta por entradas **ACE (Access Control Entries)**:
* **DACL (Discretionary Access Control List):** Define qué usuarios o grupos tienen permisos de lectura, escritura, modificación o control total sobre el recurso.
* **SACL (System Access Control List):** Define qué acciones (lectura, modificación, borrado) deben ser auditadas en el visor de eventos del sistema para registrar accesos o intentos fallidos.

---

#### 3. Derechos de Usuario y Privilegios
Es fundamental diferenciar entre permisos (que se aplican a recursos) y derechos/privilegios (que afectan a capacidades globales del sistema operativo).

##### Clasificación de Derechos y Privilegios
* **Derechos de Conexión:** Regulan las vías de entrada al equipo (ej. *Permitir/Denegar inicio de sesión local*, *Permitir/Denegar acceso desde la red*).
* **Privilegios del Sistema:** Autorizan a ejecutar acciones administrativas e internas del sistema (ej. *Apagar el sistema*, *Realizar/Restaurar copias de seguridad*, *Cargar/Desinstalar controladores*, *Unir equipos al dominio*).
* **Prioridad Inflexible:** Si existe un conflicto directo entre un permiso de recurso y un derecho de sistema, **el derecho prevalece siempre** sobre el permiso.

---

#### 4. Directivas de Seguridad Locales y de Dominio
Las directivas de seguridad establecen el comportamiento normativo y la configuración de seguridad centralizada de los equipos.

##### Ámbito de Aplicación de Directivas
* **Directivas de Seguridad Local (`secpol.msc`):** Se aplican individualmente en equipos Windows sin entorno de dominio Active Directory. Se gestionan desde *Herramientas Administrativas → Directivas de Seguridad Local*.
* **Directivas de Grupo en Dominio / GPO (`gpmc.msc`):** En redes corporativas con Active Directory (Windows Server), las GPO (*Group Policy Objects*) se aplican de forma centralizada a dominios, sitios o Unidades Organizativas (OU), distribuyendo configuraciones de seguridad a miles de clientes automáticamente.

---

#### 5. Servidores de Ficheros e Impresión
Los servidores centralizan los recursos de la red para garantizar su disponibilidad, escalabilidad y mantenimiento continuo.

##### Servidores de Ficheros (FTP / FTPS / SFTP)
* **Principios de Servidores:** Disponibilidad (operatividad continua), Escalabilidad (capacidad de crecimiento) y Mantenimiento preventivo.
* **Servidor FTP (Internet Information Services - IIS):**
  * **FTP estándar (Puerto 21/TCP):** Transfiere archivos en texto plano sin cifrado.
  * **FTPS (FTP Secure):** Añade capa de cifrado mediante certificados TLS/SSL.
  * **SFTP (SSH File Transfer Protocol):** Corre sobre el protocolo **SSH (Puerto 22/TCP)**; es un protocolo completamente distinto y altamente seguro.
* **Instalación en Windows Server:** Se agrega el rol *Servidor Web (IIS)* e incluye el servicio *Servidor FTP*. Se asignan directorios físicos y grupos de autorización de Active Directory.

##### Servidores de Impresión
* **Tipos:** Servidor externo (equipo dedicado que gestiona colas de impresión para varias impresoras) o servidor interno (tarjeta de red integrada en la propia impresora).
* **Administración de Impresión (`printmanagement.msc`):** Centraliza controladores, puertos de red IP y colas de spooler (*Print Spooler*), distribuyendo la carga de trabajo entre impresoras de red.

---

#### 6. Conexión Remota y Administración Centralizada
La administración remota permite gestionar servidores e infraestructura sin presencia física, reduciendo costes y tiempos de respuesta.

##### Herramientas Nativas de Conexión Remota
* **RDP (Remote Desktop Protocol - Puerto 3389/TCP):** Permite tomar el control completo de la sesión gráfica de un servidor o equipo cliente con credenciales autorizadas.
* **Servicios de Escritorio Remoto (RDS):** Permite a múltiples usuarios ejecutar sesiones virtuales concurrentes en un servidor corporativo.
* **Asistencia Remota (Quick Assist / Asistencia Rápida):** Permite compartir pantalla en tiempo real con un usuario para soporte técnico.

##### Arquitectura Segura de Acceso Remoto
* **Jump Servers / Bastion Hosts:** Servidores intermedios fuertemente acorazados que actúan como único punto de entrada a la red interna corporativa.
* **MFA (Multifactor Authentication):** Exige un segundo factor de verificación (OTP, app autenticadora) para autorizar accesos remotos.

---

#### 7. Criptografía, Cortafuegos y Seguridad Perimetral
La protección en profundidad combina cifrado de datos y filtrado de tráfico perimetral.

##### Algoritmos Criptográficos
* **Cifrado Simétrico (Una sola clave compartida):**
  * **DES:** Clave de 56 bits (obsoleto/vulnerable).
  * **TDES (Triple DES):** 192 bits (aplica 3 pasadas DES).
  * **AES (Advanced Encryption Standard):** Claves de 128, 192 o 256 bits. Es el estándar global actual por su velocidad y máxima seguridad.
  * **IDEA / Blowfish / RC2:** Algoritmos simétricos adicionales.
* **Cifrado Asimétrico (Par de claves Pública y Privada):**
  * **RSA / DSA / ECC (Criptografía de Curva Elíptica):** La clave pública cifra/verifica y la clave privada descifra/firma.
* **Cifrado Híbrido:** Utiliza cifrado asimétrico para intercambiar de forma segura una clave simétrica temporal (de sesión), que luego cifra el volumen masivo de tráfico (mecanismo base de TLS/HTTPS).

##### Cortafuegos (Firewalls)
* **Mecanismo:** Inspecciona paquetes de datos entrantes, salientes y reenviados (*Forward*), aplicando reglas de paso o bloqueo basadas en IP, puerto y protocolo.
* **Software vs. Hardware:** Windows Defender Firewall con seguridad avanzada (software local) vs. Routers/Appliance dedicados como **pfSense** o **MikroTik**.
* **Defensa en Profundidad:** Combinación de Firewall perimetral, WAF (*Web Application Firewall*), sistemas IDS/IPS (*Detección y Prevención de Intrusiones*) y segmentación de red.

---

🏠 **[Volver al Índice Principal](../../README.md)** | 📐 **[Ir al Esquema Resumen](./ESQUEMA_UT06_gestion_recursos_red.md)**
