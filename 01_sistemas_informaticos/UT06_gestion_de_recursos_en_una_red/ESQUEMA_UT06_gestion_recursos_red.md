🏠 **[Volver al Índice Principal](../../README.md)** | 📖 **[Ir a la Guía Teórica (Resumen)](./RESUMEN_UT06_gestion_recursos_red.md)**

---

### 🛡️ ESQUEMA DE ESTUDIO — UT06: Gestión de Recursos en una Red
**Asignatura:** Sistemas Informáticos (1º DAM/DAW)  
**Marco Metodológico:** Protocolo PEM-4 & Metodología Interna DAM  

---

##### 🗺️ El Gran Mapa Estructural: Seguridad, Servicios y Control de Acceso
```text
┌────────────────────────────────────────────────────────────────────────┐
│ 1. ACREDITACIÓN Y CONTROL DE ACCESO WINDOWS                            │
│ Inicio de Sesión ──> Security Access Token (SAT) [SID User + SIDs Grupos] │
│                      ├──> Permisos Recurso Compartido (Red)            │
│                      └──> Permisos NTFS (Local / DACL)                 │
│                      ⚠️ Acceso por Red = COMBINACIÓN MÁS RESTRICTIVA    │
└───────────────────────────────────┬────────────────────────────────────┘
                                    ▼
┌────────────────────────────────────────────────────────────────────────┐
│ 2. ESTRUCTURA ACL Y HERENCIA EN NTFS                                   │
│ Objeto NTFS ──> Propietario (SID) + ACL                                │
│                 ├──> DACL (Discretionary ACL): ACEs Permisos (Permitir/Denegar) │
│                 └──> SACL (System ACL): Eventos de Auditoría             │
│ Herencia: Padre ──> Subcarpetas (Deshabilitable / Convertir en explícitos)│
└───────────────────────────────────┬────────────────────────────────────┘
                                    ▼
┌────────────────────────────────────────────────────────────────────────┐
│ 3. SERVIDORES Y SERVICIOS EN RED                                       │
│ Ficheros: IIS + FTP (Port 21) | FTPS (TLS) | SFTP (SSH Port 22)         │
│ Impresión: Print Spooler + printmanagement.msc (Servidor Interno/Externo)│
│ Remoto:   RDP (Port 3389) | Quick Assist | Bastion Host + MFA         │
└───────────────────────────────────┬────────────────────────────────────┘
                                    ▼
┌────────────────────────────────────────────────────────────────────────┐
│ 4. CRIPTOGRAFÍA Y CORTAFUEGOS                                          │
│ Simétrico (AES-256) + Asimétrico (RSA/ECC) ──> Cifrado Híbrido (TLS)   │
│ Cortafuegos: Filtrado por Paquetes (pfSense / MikroTik / secpol.msc)   │
└────────────────────────────────────────────────────────────────────────┘
```

---

##### 🧱 Bloques Lógicos Funcionales

###### 1. Tríptico de Control de Acceso en Windows
* **Permisos:** Reglas sobre recursos concretos (archivos/carpetas).
* **Derechos / Privilegios:** Atributos del sistema sobre la cuenta (ej. apagar equipo, backups). **Los derechos prevalecen sobre los permisos.**
* **Directivas de Seguridad:** Reglas globales (`secpol.msc` para equipos locales; `gpmc.msc` para GPOs en Active Directory).

###### 2. Reglas Prácticas de Permisos y Combinaciones
* **Permisos Acumulativos:** Se suman los permisos del usuario y de sus grupos.
* **Denegar Explícito:** Prevalece siempre sobre el Permitir explícito o heredado.
* **Fórmula de Red + NTFS:**
  * *Permiso Compartido (Lectura)* + *Permiso NTFS (Control Total)* = **Lectura Efectiva por Red**.

###### 3. Cifrado y Cortafuegos
* **Cifrado Simétrico:** Misma clave para cifrar y descifrar (AES-128/192/256 es el estándar actual).
* **Cifrado Asimétrico:** Clave pública (cifra) y clave privada (descifra).
* **Cifrado Híbrido:** Asimétrico para intercambiar la clave de sesión simétrica (modelo TLS/HTTPS).

---

##### 📖 Glosario de Siglas — UT06
| Sigla | Nombre Completo en Inglés | Traducción / Función en 5 Palabras |
| ------ | ------ | ------ |
| **SAT** | *Security Access Token* | Token de seguridad con SIDs de usuario/grupos. |
| **SID** | *Security Identifier* | Identificador único de seguridad de cuenta/grupo. |
| **ACL** | *Access Control List* | Lista de control de acceso a un recurso. |
| **DACL** | *Discretionary Access Control List* | Lista de permisos explícitos e heredados. |
| **SACL** | *System Access Control List* | Lista de auditoría de eventos de seguridad. |
| **ACE** | *Access Control Entry* | Entrada individual de permiso dentro de una ACL. |
| **GPO** | *Group Policy Object* | Directiva de grupo centralizada en Active Directory. |
| **OU** | *Organizational Unit* | Unidad Organizativa en Active Directory. |
| **IIS** | *Internet Information Services* | Servidor Web y FTP nativo de Windows Server. |
| **SFTP** | *SSH File Transfer Protocol* | Transferencia segura sobre SSH (Puerto 22). |
| **FTPS** | *FTP Secure* | Protocolo FTP cifrado con TLS/SSL (Puerto 21/990). |
| **RDP** | *Remote Desktop Protocol* | Protocolo de escritorio remoto (Puerto 3389). |
| **MFA** | *Multifactor Authentication* | Autenticación de doble o múltiple factor. |
| **AES** | *Advanced Encryption Standard* | Algoritmo simétrico estándar de alta seguridad. |
| **RSA** | *Rivest-Shamir-Adleman* | Algoritmo asimétrico clave pública/privada. |
| **WAF** | *Web Application Firewall* | Cortafuegos especializado en aplicaciones web. |
| **IDS/IPS** | *Intrusion Detection/Prevention System* | Sistema de detección/prevención de intrusos. |

---

🏠 **[Volver al Índice Principal](../../README.md)** | 📖 **[Ir a la Guía Teórica (Resumen)](./RESUMEN_UT06_gestion_recursos_red.md)**
