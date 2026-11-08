🏠 **[Volver al Índice Principal](../../README.md)** | 📐 **[Ir al Esquema Resumen](./ESQUEMA-UT07-explotacion-aplicaciones.md)**

---

### 💻 GUÍA TEÓRICA Y RESUMEN — UT07: Explotación de Aplicaciones Informáticas de Propósito General
**Asignatura:** Sistemas Informáticos (1º DAM/DAW)  
**Marco Metodológico:** Protocolo PEM-4 & Metodología Interna DAM  

---

#### 1. Tipos de Software, Licencias y Clasificación
El software se clasifica según sus derechos de uso, modificación y distribución (licenciamiento) o según su propósito funcional.

##### Nivel 1: En lenguaje sencillo (La idea en 10 segundos)
Las licencias de software son contratos legales que dictan qué puedes hacer con un programa. El software propietario es un "edificio cerrado" donde no puedes ver ni alterar los cimientos; el software libre/código abierto es una "receta pública" que cualquiera puede inspeccionar, mejorar y compartir.

##### Nivel 2: De un vistazo (Claves de examen)
| Tipo de Licencia | Código Fuente | Modificación / Redistribución | Ejemplo Típico |
| :--- | :--- | :--- | :--- |
| **Propietario / Comercial** | Cerrado | Prohibida sin autorización / Pago de licencias | Windows, MS Office |
| **Copyleft / FSF (GPL)** | Abierto | Obliga a mantener la misma licencia libre en derivadas | Linux Kernel, GNU Tools |
| **Permisivo (MIT / Apache / BSD)** | Abierto | Permite integrar en código comercial cerrado | React, VS Code Core |
| **Creative Commons (CC)** | N/A (Obras) | Modular: BY (Atribución), NC (No Comercial), SA (Compartir Igual) | Música, Texto, Fotos |

##### Nivel 3: Detalle técnico
*   **Software de Propósito General:** Aplicaciones no diseñadas para una tarea única o nicho exclusivo, sino para cubrir necesidades comunes de cualquier usuario (ofimática, navegadores, multimedia, utilidades).
*   **Copyleft (GPL):** Garantiza que las versiones modificadas del software sigan siendo libres. Si modificas un componente bajo GPL y lo distribuyes, estás legalmente obligado a liberar tu código fuente con la misma licencia.
*   **Licencias Permisivas (MIT/BSD/Apache):** Otorgan máxima libertad. Permiten la reutilización del código en productos propietarios sin obligación de publicar las modificaciones.

---

#### 2. Requisitos de Instalación, Hardware y Software de Desarrollo
Antes de desplegar cualquier software en un entorno de producción o desarrollo, se deben auditar los requisitos mínimos y recomendados del sistema.

##### Nivel 1: En lenguaje sencillo (La idea en 10 segundos)
Los requisitos mínimos son la "línea de supervivencia" para que el programa abra; los requisitos recomendados son los necesarios para que el trabajo sea fluido y profesional, especialmente al usar tecnologías exigentes como contenedores o inteligencia artificial.

##### Nivel 2: De un vistazo (Claves de examen)
*   **Mínimo de Supervivencia:** CPU básica, 4 GB RAM, almacenamiento estándar.
*   **Recomendación Profesional Modern:** CPU multi-núcleo, **16 GB a 32 GB de RAM**, almacenamiento SSD NVMe para mover entornos con Docker, VS Code e Inteligencia Artificial.
*   **Herramientas de Productividad Dev:** VS Code (Editor), npm/pnpm/yarn (Gestores de paquetes), Postman (Cliente API), Docker & Docker Compose (Contenedores), Kubernetes (Orquestación).

##### Nivel 3: Detalle técnico
*   **Ecosistema DevOps:** En la explotación moderna de aplicaciones, el software de desarrollo va más allá del paquete ofimático tradicional. Los desarrolladores e ingenieros de sistemas utilizan contenedores ligeros (Docker) que empaquetan la aplicación con todas sus dependencias, asegurando un comportamiento idéntico en desarrollo, pruebas y producción.

---

#### 3. Herramientas Ofimáticas, Bases de Datos y Tratamiento de Gráficos
Las herramientas ofimáticas y de gestión permiten procesar, almacenar y presentar la información corporativa.

##### Nivel 1: En lenguaje sencillo (La idea en 10 segundos)
Involucra aplicaciones para crear documentos de texto, hojas de cálculo, presentaciones, así como clientes de bases de datos para consultar información estructurada y editores de imágenes para material visual.

##### Nivel 2: De un vistazo (Claves de examen)
*   **Procesadores de Texto & Hojas de Cálculo:** Microsoft Word/Excel, LibreOffice Writer/Calc, Google Docs/Sheets.
*   **Gestión de Bases de Datos (GUI):** MySQL Workbench, DBeaver, pgAdmin.
*   **Diseño Gráfico & Retoque:** Adobe Photoshop, GIMP (software libre), Canva.

---

#### 4. Herramientas de Internet, Transferencia de Archivos y Correo Electrónico
Comprende los protocolos y aplicaciones para la comunicación y transferencia de datos a través de redes locales e Internet.

##### Nivel 1: En lenguaje sencillo (La idea en 10 segundos)
Permite enviar correos automáticos, descargar o subir archivos de servidores de forma segura y compartir información entre equipos mediante clientes web o servicios especializados.

##### Nivel 2: De un vistazo (Claves de examen)
*   **Correo Saliente Automatizado:** Servicio **SMTP autenticado** (puerto 587/465 TLS) para notificaciones y recuperación de contraseñas.
*   **Autenticación Antisuplantación DNS:** **SPF** (valida IPs de envío), **DKIM** (firma digital de correo), **DMARC** (política de alineación y reporte).
*   **Transferencia de Archivos:** **FTP** (sin cifrado, puerto 21), **SFTP** (cifrado sobre SSH, puerto 22), **Almacenamiento de Objetos** (AWS S3, Azure Blob, GCS para despliegues CI/CD).
*   **P2P (*Peer-to-Peer*):** Redes descentralizadas o híbridas donde los recursos residen en los nodos iguales.

---

#### 5. Software Antimalware y Seguridad en Pipelines CI/CD
El software antimalware protege el sistema contra código malicioso mediante análisis en tiempo real y firmas de seguridad.

##### Nivel 1: En lenguaje sencillo (La idea en 10 segundos)
Un antivirus tradicional busca "huellas conocidas" (firmas) o "comportamientos sospechosos" (heurística) en el equipo; en el desarrollo moderno, la seguridad se automatiza también analizando las librerías y contenedores en el propio código.

##### Nivel 2: De un vistazo (Claves de examen)
*   **Análisis por Firmas:** Comparación del archivo con una base de datos de malware conocido.
*   **Análisis Heurístico:** Detección de patrones anómalos o comportamientos maliciosos no registrados.
*   **Seguridad DevSecOps:** **SCA** (*Software Composition Analysis* para detectar vulnerabilidades en dependencias), escaneo de imágenes de contenedores y *secret scanning* (evitar claves o contraseñas expuestas en Git).

---

#### 6. Clonación de Sistemas Operativos y Réplica de Discos
La clonación es la copia integral "bit a bit" o sector a sector de una unidad de almacenamiento (disco o partición), permitiendo replicar el sistema operativo, programas, configuraciones y datos.

##### Nivel 1: En lenguaje sencillo (La idea en 10 segundos)
A diferencia de copiar y pegar archivos a mano, la clonación duplica el disco entero exactamente como está. Para que la copia sea idéntica y no falle, el sistema operativo del disco original debe estar **completamente apagado (*estado parado*)**.

##### Nivel 2: De un vistazo (Claves de examen)
*   **Clonación Directa (`device-device`):** Copia directa de disco físico a disco físico (`disk_to_local_disk`). El destino debe ser de igual o mayor capacidad.
*   **Clonación por Imagen (`device-image`):** Genera un archivo comprimido encapsulado (ISO/img) para restaurar en múltiples equipos (*Golden Image*).
*   **Regla de Oro del Sistema Parado:** La clonación requiere arrancar desde un medio externo (USB con **Clonezilla**) para mantener el disco de origen desmontado y sin archivos bloqueados por el sistema operativo.
*   **Creación de USB Booteable:** Herramienta **Rufus** para grabar archivos ISO en pendrives autoarrancables (configurando esquemas GPT/MBR y destino UEFI/BIOS).
*   **Ajustes Firmware BIOS/UEFI:** Desactivar **Secure Boot** (si se usan sistemas no firmados) y **Fast Boot/Fast Startup** en Windows. En CMD/PowerShell se fuerza el reinicio a UEFI con: `shutdown /r /fw /t 0`.
*   **Identificación de Discos Unix:** Disco 1 = `sda`, Disco 2 = `sdb`. ¡Verificar siempre el tamaño antes de clonar para evitar borrar el origen!

##### Nivel 3: Detalle técnico
*   **Licenciamiento y MAC Address:** Al clonar un sistema operativo a otra máquina física diferente, Windows detecta la nueva dirección física MAC de la tarjeta de red e id del hardware, requiriendo reactivar la licencia.
*   **Drivers Hardware:** La clonación incluye los controladores instalados. Si la máquina de destino tiene piezas distintas (tarjeta gráfica, chip de sonido), el sistema requerirá instalar o adaptar los drivers tras el primer arranque.

---

#### 7. Copias de Seguridad (Backups), Restauración y Recuperación
Un backup es un respaldo planificado de datos para garantizar la continuidad del negocio ante incidentes (borrados, ataques de ransomware o fallos de disco).

##### Nivel 1: En lenguaje sencillo (La idea en 10 segundos)
Existen tres formas de guardar copias: guardar todo cada vez (completa), guardar solo lo nuevo desde el último día (incremental) o guardar lo nuevo desde la última copia completa (diferencial).

##### Nivel 2: De un vistazo (Claves de examen)
*   **Copia Completa (Full Backup):** Copia el 100% de los datos y marca el flag de modificado. Restauración más rápida (1 sola pieza), copia más lenta.
*   **Copia Incremental:** Guarda solo los cambios desde la última copia (sea completa o incremental) y limpia el flag. Ocupa poco espacio; restauración más lenta (requiere la completa + **todas** las incrementales en orden estricto).
*   **Copia Diferencial:** Guarda los cambios acumulados desde la última copia completa (sin limpiar el flag). Tamaño creciente; restauración rápida (requiere la completa + la **última** diferencial).
*   **Regla 3-2-1 de Respaldos:** 3 copias de los datos, 2 medios de almacenamiento distintos, 1 copia guardada fuera del sitio (*offsite* / nube).
*   **Métricas de Recuperación:** **RTO** (*Recovery Time Objective* - tiempo máximo de parada permitido) y **RPO** (*Recovery Point Objective* - cantidad máxima de datos que se puede tolerar perder).
*   **Runbook:** Documento técnico operativo donde se registra y prueba periódicamente el procedimiento de restauración.

---

#### 8. Caso Práctico de Laboratorio: Migración HDD a SSD
Análisis del escenario profesional de la Actividad Práctica de la UT07.

##### Contexto y Solución Técnica
*   **Escenario:** Migración del portátil de dirección en "Logística Veloz" de un disco mecánico (HDD de 500 GB) a un disco de estado sólido (SSD de 1 TB).
*   **Procedimiento Operativo:**
    1.  Preparación del pendrive de arranque con **Rufus** seleccionando la ISO de **Clonezilla**.
    2.  Conexión del nuevo SSD mediante adaptador SATA/USB o segundo puerto interno.
    3.  Acceso al firmware BIOS/UEFI para ajustar la prioridad de arranque (Boot Order) al USB.
    4.  Ejecución de Clonezilla en modo `device-device` ➔ `disk_to_local_disk`.
    5.  Selección cuidadosa de origen (`sda` - 500GB HDD) y destino (`sdb` - 1TB SSD).
    6.  Elección de reconstrucción de tabla de particiones proporcional para aprovechar el espacio extra del SSD de 1 TB.
    7.  Sustitución física del disco HDD por el nuevo SSD y verificación de arranque idéntico con rendimiento optimizado.

---

🏠 **[Volver al Índice Principal](../../README.md)** | 📐 **[Ir al Esquema Resumen](./ESQUEMA-UT07-explotacion-aplicaciones.md)**
