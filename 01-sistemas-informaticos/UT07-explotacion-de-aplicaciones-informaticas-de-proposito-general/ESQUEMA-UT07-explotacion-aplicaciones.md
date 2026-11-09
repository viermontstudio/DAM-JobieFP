🏠 **[Volver al Índice Principal](../../README.md)** | 📖 **[Ir a la Guía Teórica (Resumen)](./RESUMEN-UT07-explotacion-aplicaciones.md)**

---

# ⚙️ ESQUEMA DE ESTUDIO — UT07: Explotación de Aplicaciones Informáticas de Propósito General
**Asignatura:** Sistemas Informáticos (1º DAM/DAW)  
**Marco Metodológico:** Protocolo PEM-4 & Metodología Interna DAM  

---

## 🗺️ 1. El Gran Mapa Estructural: Clasificación, Clonación y Backups

```text
┌──────────────────────────────────────────────────────────────────────────────────┐
│ 1. CLASIFICACIÓN DEL SOFTWARE Y LICENCIAMIENTO                                   │
├──────────────────────────────────────────────────────────────────────────────────┤
│ Software Propietario (Cerrado) vs Libre/Código Abierto (GPL, MIT, CC)            │
│ Copyleft (GPL): Obliga a liberar derivadas  |  Permisivo (MIT): Libre uso privado│
│ Licenciamiento de Contenidos: Creative Commons (Módulos BY, NC, ND, SA)          │
└──────────────────────────────────────────────────────────────────────────────────┘
                                         ▼
┌──────────────────────────────────────────────────────────────────────────────────┐
│ 2. ENTORNO DE DESARROLLO Y HERRAMIENTAS DE PRODUCTIVIDAD                         │
├──────────────────────────────────────────────────────────────────────────────────┤
│ Hardware Dev: CPU Multi-núcleo + 16-32 GB RAM + SSD NVMe                         │
│ Contenedores: Docker & Docker Compose (Empaquetan app con dependencias)          │
│ Editores & Clientes: VS Code, Postman (REST API), DBeaver / pgAdmin / Workbench  │
└──────────────────────────────────────────────────────────────────────────────────┘
                                         ▼
┌──────────────────────────────────────────────────────────────────────────────────┐
│ 3. SERVICIOS DE INTERNET, CORREO CORPORATIVO Y SEGURIDAD DNS                     │
├──────────────────────────────────────────────────────────────────────────────────┤
│ Correo Saliente: SMTP Autenticado (Puerto 587/465 TLS)                           │
│ Antisuplantación DNS: SPF (IPs autorizadas) + DKIM (Firma) + DMARC (Política)    │
│ Transferencia: SFTP (Puerto 22 SSH) | Almacenamiento Objetos (AWS S3 / Blob)     │
└──────────────────────────────────────────────────────────────────────────────────┘
                                         ▼
┌──────────────────────────────────────────────────────────────────────────────────┐
│ 4. CLONACIÓN DE SISTEMAS CON CLONEZILLA Y RUFUS (REPLICA DISCOS)                 │
├──────────────────────────────────────────────────────────────────────────────────┤
│ Preparación: Rufus (ISO Clonezilla -> USB Booteable GPT/UEFI)                    │
│ Sistema Parado (Regla de Oro): Disco inactivo | shutdown /r /fw /t 0             │
│ Ejecución Clonezilla device-device: Origen (sda) -> Destino (sdb)                │
└──────────────────────────────────────────────────────────────────────────────────┘
                                         ▼
┌──────────────────────────────────────────────────────────────────────────────────┐
│ 5. ESTRATEGIAS DE BACKUP, RECUPERACIÓN Y SEGURIDAD                               │
├──────────────────────────────────────────────────────────────────────────────────┤
│ Tipos Copia: Completa (100%), Incremental (Cambios/Limpia), Diferencial (Acum)   │
│ Seguridad DevSecOps: SCA (Análisis librerías) + Regla 3-2-1 de Respaldos         │
│ Métricas Continuidad: RTO (Tiempo máx. parada) | RPO (Pérdida máx. datos)        │
└──────────────────────────────────────────────────────────────────────────────────┘
```

---

## 🧱 2. Desglose Estructurado por Bloques Lógicos

### 📜 1. Clasificación del Software y Licenciamiento

```text
┌──────────────────────────────────────────────────────────────────────────────────┐
│                      MATRIZ DE LICENCIAMIENTO DE SOFTWARE                        │
├─────────────────┬───────────────────────┬─────────────────┬──────────────────────┤
│ Tipo Licencia   │ Acceso a Código       │ Modificación    │ Rederivación         │
├─────────────────┼───────────────────────┼─────────────────┼──────────────────────┤
│ Propietaria     │ Privado / Cerrado     │ Prohibida       │ Restringida (Pago)   │
│ Copyleft (GPL)  │ Abierto (Público)     │ Permitida       │ Obligatoria GPL      │
│ Permisiva (MIT) │ Abierto (Público)     │ Permitida       │ Libre (Propietario)  │
│ Creative Comm.  │ Variable (Contenidos) │ Según módulo ND │ Según módulo SA      │
└─────────────────┴───────────────────────┴─────────────────┴──────────────────────┘
```

* **Tríptico de Licencias:**
  * **Software Propietario:** Código privado/cerrado. Uso bajo licencia de pago o restricciones del fabricante.
  * **Copyleft (GPL - General Public License):** Código abierto. Obliga legalmente a que cualquier software derivado se distribuya bajo la misma licencia GPL (*efecto viral*).
  * **Licencias Permisivas (MIT / BSD / Apache):** Código abierto de máxima libertad. Permite integrar el código en productos comerciales sin necesidad de publicar las modificaciones.
  * **Creative Commons (CC):** Licenciamiento modular para contenidos (textos, imágenes, música): **BY** (Atribución), **NC** (No Comercial), **ND** (Sin Derivadas), **SA** (Compartir Igual).

---

### 💾 2. Herramientas de Desarrollo y Requisitos de Hardware

* **Auditoría de Requisitos de Hardware:**
  * **Mínimos de Supervivencia:** CPU básica, 4 GB RAM, almacenamiento HDD estándar.
  * **Recomendados Profesional (DevOps / IA):** CPU multi-núcleo (8+ hilos), **16 GB a 32 GB RAM**, SSD NVMe.
* **Ecosistema de Herramientas Dev:**
  * **IDEs & Editores:** Visual Studio Code, IntelliJ IDEA, Eclipse.
  * **Contenedores & Despliegue:** **Docker** y **Docker Compose** (empaquetado portátil de la aplicación con sus dependencias exactas), **Kubernetes** (orquestación).
  * **Clientes API & Bases de Datos:** **Postman** (pruebas de servicios web REST/HTTP), **DBeaver** / **pgAdmin** / **MySQL Workbench** (administración gráfica de BD).

---

### 🌐 3. Servicios de Internet, Correo Corporativo y Transferencia

* **Correo Electrónico Automatizado (Notificaciones & CI/CD):**
  * **Servicio SMTP Autenticado:** Envío mediante puertos **587/TCP** o **465/TCP** con cifrado TLS/SSL.
  * **Tríptico de Seguridad Antisuplantación DNS:**
    * **SPF (*Sender Policy Framework*):** Registro TXT en DNS que lista los servidores e IPs autorizados a enviar correo del dominio.
    * **DKIM (*DomainKeys Identified Mail*):** Firma digital en la cabecera que garantiza que el correo no ha sido alterado.
    * **DMARC:** Define la política de alineación (SPF/DKIM) y genera reportes automáticos de intentos de suplantación.
* **Protocolos de Transferencia & Nube:**
  * **SFTP (*SSH File Transfer Protocol*):** Transferencia cifrada sobre el puerto **22/TCP** (SSH).
  * **Almacenamiento de Objetos:** AWS S3, Azure Blob Storage (repositorios en la nube para activos estáticos y copias).

---

### 💿 4. Procedimiento de Clonación de Sistemas (Clonezilla & Rufus)

```text
┌──────────────────────────────────────────────────────────────────────────────────┐
│              ARQUITECTURA Y PASOS DE CLONACIÓN DEVICE-DEVICE                     │
├──────────────────────────────────────────────────────────────────────────────────┤
│                                                                                  │
│   [ 1. Preparación Media ] ──> Generar USB Booteable Clonezilla con Rufus        │
│                                (Configurar esquema GPT / Destino UEFI)           │
│                                                                                  │
│   [ 2. Ajuste Firmware  ] ──> Desactivar Secure Boot / Fast Startup              │
│                                Forzar reinicio UEFI: shutdown /r /fw /t 0        │
│                                                                                  │
│   [ 3. Sistema Parado   ] ──> Arrancar desde el USB (Disco Inactivo)             │
│                                Seleccionar modo Clonezilla: device-device        │
│                                                                                  │
│   [ 4. Selección Discos ] ──> Origen: sda (HDD 500GB)  ──> Destino: sdb (SSD 1TB)│
│                                [VITAL] Verificar tamaños para evitar borrado     │
│                                                                                  │
│   [ 5. Ejecución Copy   ] ──> Copia Sector a Sector / Proporcional de Tabla      │
│                                Apagar equipo al finalizar y sustituir disco      │
│                                                                                  │
└──────────────────────────────────────────────────────────────────────────────────┘
```

* **Reglas Clave de Examen:**
  * **Regla de Oro del Sistema Parado:** La clonación exige que el disco de origen esté **totalmente inactivo** (sistema operativo desmontado) para evitar archivos bloqueados o corruptos.
  * **Nomenclatura de Discos Unix:** Disco 1 = `sda`, Disco 2 = `sdb`.
  * **Reactivación de Licencia & Drivers:** Al clonar a una máquina con hardware distinto, Windows detecta el cambio de MAC/Hardware y solicitará clave de licencia y adaptación de controladores.

---

### 🛡️ 5. Estrategias de Backup, Restauración y Seguridad

```text
┌──────────────────────────────────────────────────────────────────────────────────┐
│                 TIPOS DE BACKUP Y SECUENCIA DE RESTAURACIÓN                      │
├───────────────┼─────────────────────────────┼─────────────────────┼──────────────┤
│ Tipo Backup   │ Datos Copiados              │ Flag Modificado     │ Tiempo Rest. │
├───────────────┼─────────────────────────────┼─────────────────────┼──────────────┤
│ Completo      │ 100% de la información      │ Se activa / marca   │ Mínimo (1)   │
│ Incremental   │ Cambios desde última copia  │ Se desactiva/limpia │ Largo (N)    │
│ Diferencial   │ Cambios desde últ. Full     │ No se modifica      │ Medio (2)    │
└───────────────┴─────────────────────────────┴─────────────────────┴──────────────┘

┌──────────────────────────────────────────────────────────────────────────────────┐
│                        ORDEN DE RESTAURACIÓN DE BACKUPS                          │
├──────────────────────────────────────────────────────────────────────────────────┤
│                                                                                  │
│  Estrategia Incremental: [Completo] -> [Inc 1] -> [Inc 2] -> ... -> [Inc N]      │
│  (Se deben aplicar TODAS las copias en orden cronológico estricto)               │
│                                                                                  │
│  Estrategia Diferencial: [Completo] -> [Última Copia Diferencial]                │
│  (Solo requiere el archivo base y el bloque acumulado más reciente)              │
│                                                                                  │
└──────────────────────────────────────────────────────────────────────────────────┘
```

* **Métricas y Políticas de Recuperación:**
  * **Regla 3-2-1:** 3 copias de los datos, 2 soportes distintos, 1 copia fuera del sitio (*offsite* / nube).
  * **RTO (*Recovery Time Objective*):** Tiempo máximo aceptable de parada del servicio.
  * **RPO (*Recovery Point Objective*):** Pérdida máxima aceptable de datos medida en tiempo.
  * **DevSecOps & SCA (*Software Composition Analysis*):** Análisis automatizado de vulnerabilidades en dependencias y librerías de código.

---

## 📚 3. Glosario Mnemotécnico de Siglas — UT07

| Sigla | Nombre Completo en Inglés | Traducción al Español | Función Clave |
| :--- | :--- | :--- | :--- |
| **GPL** | *General Public License* | Licencia Pública General | Licencia copyleft obligatoria de rederivación libre |
| **MIT** | *Massachusetts Institute of Technology* | Licencia MIT | Licencia libre permisiva para integración comercial |
| **SCA** | *Software Composition Analysis* | Análisis de Composición de Software | Detección de vulnerabilidades en dependencias |
| **SFTP** | *SSH File Transfer Protocol* | Protocolo de Transferencia Segura SSH | Transferencia cifrada de archivos sobre puerto 22 |
| **SMTP** | *Simple Mail Transfer Protocol* | Protocolo de Transferencia Simple de Correo | Envío automatizado de correos salientes |
| **SPF** | *Sender Policy Framework* | Convenio de Emisores del Sender | Registro DNS que publica IPs autorizadas a emitir correo |
| **DKIM** | *DomainKeys Identified Mail* | Correo Identificado por Claves de Dominio | Firma digital en cabecera para prevenir alteración |
| **DMARC** | *Domain-based Message Authentication* | Autenticación de Mensajes por Dominio | Política DNS de reporte y cumplimiento SPF/DKIM |
| **RTO** | *Recovery Time Objective* | Objetivo de Tiempo de Recuperación | Tiempo máximo aceptable de inactividad del servicio |
| **RPO** | *Recovery Point Objective* | Objetivo de Punto de Recuperación | Pérdida máxima aceptable de datos medida en tiempo |
| **FHS** | *Filesystem Hierarchy Standard* | Estándar de Jerarquía del Sistema de Archivos | Estructura oficial de directorios en Linux |

---

🏠 **[Volver al Índice Principal](../../README.md)** | 📖 **[Ir a la Guía Teórica (Resumen)](./RESUMEN-UT07-explotacion-aplicaciones.md)**
