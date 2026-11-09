🏠 **[Volver al Índice Principal](../../README.md)** | 📖 **[Ir a la Guía Teórica (Resumen)](./RESUMEN-UT06-gestion-recursos-red-v2.md)**

---

### 🛡️ ESQUEMA DE ESTUDIO — UT06: Gestión de Recursos en una Red
**Asignatura:** Sistemas Informáticos (1º DAM/DAW)  
**Marco Metodológico:** Protocolo PEM-4 & Metodología Interna DAM  

---

#### 🗺️ El Gran Mapa Estructural: Seguridad, Servicios y Control de Acceso

```text
┌──────────────────────────────────────────────────────────────────────────────────┐
│ 1. ACREDITACIÓN, RUTAS UNC Y REGLA DE LA DOBLE PUERTA                            │
│ Inicio de Sesión ──> Security Access Token (SAT) [SID User + SIDs Grupos]        │
│ Ruta UNC: \\Equipo\Recurso  vs  URI Linux: smb://<IP>/<Recurso>                  │
│ PERMISO EFECTIVO DE RED = Puerta 1 (Recurso Compartido) + Puerta 2 (NTFS)        │
│ [!] Regla de Combinación: EL RESULTADO MÁS RESTRICTIVO PREVALECE                 │
└──────────────────────────────────────────────────────────────────────────────────┘
                                          ▼
┌──────────────────────────────────────────────────────────────────────────────────┐
│ 2. ESTRUCTURA ACL, HERENCIA Y DENEGAR EXPLÍCITO                                  │
│ Objeto NTFS ──> Propietario (SID) + ACL                                          │
│                 ├──> DACL (Discretionary ACL): ACEs Permisos (Permitir/Denegar)  │
│                 └──> SACL (System ACL): Eventos de Auditoría (Visor Eventos)     │
│ Grupos Múltiples: Permisos Acumulativos | [!] DENEGAR EXPLÍCITO APLASTA PERMITIR │
│ Herencia NTFS: Padre ──> Subcarpetas (Deshabilitable / Convertir en explícitos)  │
└──────────────────────────────────────────────────────────────────────────────────┘
                                          ▼
┌──────────────────────────────────────────────────────────────────────────────────┐
│ 3. PROCEDIMIENTO METODOLÓGICO DE COMPARTICIÓN (6 PASOS)                          │
│ [1. Necesidades] ──> [2. Recurso Red] ──> [3. NTFS Local] ──> [4. Herencia]      │
│                                                                                  │
│ [6. Verificación Real] <── [5. Cálculo Permiso Efectivo] <────┘                  │
└──────────────────────────────────────────────────────────────────────────────────┘
                                          ▼
┌──────────────────────────────────────────────────────────────────────────────────┐
│ 4. SERVIDORES, SERVICIOS Y LAB HETEROGÉNEO (WINDOWS - LINUX)                     │
│ Ficheros: IIS + FTP (Port 21) | FTPS (TLS) | SFTP (SSH Port 22)                  │
│ Compartición SMB: Windows (Port 445/139) <──> Linux Samba (sudo apt install)     │
│ Impresión: Print Spooler + printmanagement.msc (Servidor Interno/Externo)        │
└──────────────────────────────────────────────────────────────────────────────────┘
                                          ▼
┌──────────────────────────────────────────────────────────────────────────────────┐
│ 5. CONEXIÓN REMOTA, CRIPTOGRAFÍA Y CORTAFUEGOS                                   │
│ Remoto: RDP (Port 3389) | Quick Assist (Soporte) | Bastion Host + MFA            │
│ Cifrado: Simétrico (AES-256) + Asimétrico (RSA/ECC) ──> Cifrado Híbrido (TLS)    │
│ Cortafuegos: Filtrado Paquetes (wf.msc / pfSense / MikroTik) ──> Input/Forward   │
└──────────────────────────────────────────────────────────────────────────────────┘
```

---

#### 🧱 Bloques Lógicos Funcionales

###### 1. Tríptico de Control de Acceso y Reglas de Combinación
* **Permisos:** Reglas aplicadas sobre recursos concretos (archivos/carpetas).
* **Derechos / Privilegios:** Capacidades globales asignadas a la cuenta sobre el sistema operativo (ej. apagar equipo, realizar copias de seguridad). **Los derechos prevalecen siempre sobre los permisos NTFS.**
* **Directivas de Seguridad:** Configuración centralizada (`secpol.msc` para equipos locales; `gpmc.msc` para GPOs en Active Directory).
* **Fórmula de Permisos Acumulados:** `Permisos Usuario + Permisos Grupo 1 + Permisos Grupo 2`.
* **Fórmula del Denegar Explícito:** `Cualquier Permitir + Denegar Explícito = ACCESO BLOQUEADO`.
* **Fórmula de Acceso por Red (Doble Puerta):**
  * *Permiso Compartido (Lectura)* + *Permiso NTFS (Control Total)* = **Lectura Efectiva por Red**.

###### 2. Interoperabilidad Heterogénea y Comandos CLI
* **Rutas UNC (Windows):** `\\10.0.0.11\UT6_Compartida` (Explorer / CMD).
* **Rutas URI (Linux/Samba):** `smb://10.0.0.11/UT6_Compartida` (Nautilus / GVFS).
* **Diagnóstico de Sockets en Windows:** `netstat -ab` (Verifica estado `LISTENING` en puertos 445/TCP y 139/TCP).
* **Diagnóstico de Sockets en Linux:** `sudo netstat -tulnp` o `ss -tlpn` (Verifica procesos de Samba `smbd`).

---

#### 📖 Glosario de Siglas — UT06
| Sigla | Nombre Completo en Inglés | Traducción / Función en 5 Palabras |
| :--- | :--- | :--- |
| **SAT** | *Security Access Token* | Token de seguridad con SIDs de usuario/grupos. |
| **SID** | *Security Identifier* | Identificador único de seguridad de cuenta/grupo. |
| **UNC** | *Universal Naming Convention* | Sintaxis estandarizada de rutas de red Windows. |
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

🏠 **[Volver al Índice Principal](../../README.md)** | 📖 **[Ir a la Guía Teórica (Resumen)](./RESUMEN-UT06-gestion-recursos-red-v2.md)**
