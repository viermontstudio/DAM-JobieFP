🏠 **[Volver al Índice Principal](../../README.md)** | 📖 **[Ir a la Guía Teórica (Resumen)](./RESUMEN-UT07-explotacion-aplicaciones.md)**

---

### ⚙️ ESQUEMA DE ESTUDIO — UT07: Explotación de Aplicaciones Informáticas de Propósito General
**Asignatura:** Sistemas Informáticos (1º DAM/DAW)  
**Marco Metodológico:** Protocolo PEM-4 & Metodología Interna DAM  

---

#### 🧱 Bloques Lógicos Funcionales

###### 1. Clasificación del Software y Licenciamiento
┌──────────────────────────────────────────────────────────────────────────────────┐
│                      MATRIZ DE LICENCIAMIENTO DE SOFTWARE                        │
├──────────────────┬───────────────────────┬───────────────────┬───────────────────┤
│ Tipo Licencia    │ Acceso a Código       │ Modificación      │ Rederivación      │
├──────────────────┼───────────────────────┼───────────────────┼───────────────────┤
│ Propietaria      │ Privado / Cerrado     │ Prohibida         │ Restringida (Pago)│
│ Copyleft (GPL)   │ Abierto (Público)     │ Permitida         │ Obligatoria GPL   │
│ Permisiva (MIT)  │ Abierto (Público)     │ Permitida         │ Libre (Propietario│
│ Creative Commons │ Variable (Contenidos) │ Según módulo (ND) │ Según módulo (SA) │
└──────────────────┴───────────────────────┴───────────────────┴───────────────────┘

###### 2. Flujo de Trabajo en Clonación de Sistemas (`device-device`)
┌──────────────────────────────────────────────────────────────────────────────────┐
│              ARQUITECTURA DE CLONACIÓN CON CLONEZILLA & RUFUS                    │
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
│                                ¡VITAL! Verificar tamaños para evitar borrado     │
│                                                                                  │
│   [ 5. Ejecución Copy   ] ──> Copia Sector a Sector / Proporcional de Tabla      │
│                                Apagar equipo al finalizar y sustituir disco      │
│                                                                                  │
└──────────────────────────────────────────────────────────────────────────────────┘

###### 3. Comparativa de Estrategias de Backup y Restauración
┌──────────────────────────────────────────────────────────────────────────────────┐
│                 TIPOS DE BACKUP Y SECUENCIA DE RESTAURACIÓN                      │
├───────────────┬───────────────────────────┬──────────────────────┬───────────────┤
│ Tipo Backup   │ Datos Copiados            │ Flag Modificado      │ Tiempo Rest.  │
├───────────────┼───────────────────────────┼──────────────────────┼───────────────┤
│ Completo      │ 100% de la información    │ Se activa / marca    │ Mínimo (1)    │
│ Incremental   │ Cambios desde última copia│ Se desactiva / limpia│ Largo (N)     │
│ Diferencial   │ Cambios desde últ. Full   │ No se modifica       │ Medio (2)     │
└───────────────┴───────────────────────────┴──────────────────────┴───────────────┘

┌──────────────────────────────────────────────────────────────────────────────────┐
│                        ORDEN DE RESTAURACIÓN DE BACKUPS                          │
├──────────────────────────────────────────────────────────────────────────────────┤
│                                                                                  │
│  Estrategia Incremental:  [Backup Completo] ➔ [Inc 1] ➔ [Inc 2] ➔ ... ➔ [Inc N]  │
│  (Se deben aplicar TODAS las copias en orden cronológico estricto)               │
│                                                                                  │
│  Estrategia Diferencial:  [Backup Completo] ➔ [Última Copia Diferencial]         │
│  (Solo requiere el archivo base y el bloque acumulado más reciente)              │
│                                                                                  │
└──────────────────────────────────────────────────────────────────────────────────┘

---

#### 📖 Glosario de Siglas — UT07
| Sigla | Nombre Completo en Inglés | Traducción / Función en 5 Palabras |
| :--- | :--- | :--- |
| **GPL** | *General Public License* | Licencia copyleft obligatoria rederivación libre. |
| **MIT** | *Massachusetts Institute of Technology* | Licencia libre permisiva para integración comercial. |
| **SCA** | *Software Composition Analysis* | Análisis de vulnerabilidades en dependencias. |
| **P2P** | *Peer-to-Peer* | Red descentralizada entre nodos iguales. |
| **SFTP** | *SSH File Transfer Protocol* | Transferencia cifrada sobre puerto 22 SSH. |
| **SMTP** | *Simple Mail Transfer Protocol* | Protocolo de envío de correo electrónico. |
| **SPF** | *Sender Policy Framework* | Registro DNS que valida servidores emisores. |
| **DKIM** | *DomainKeys Identified Mail* | Firma digital de autenticación de correo. |
| **DMARC** | *Domain-based Message Authentication* | Política DNS de alineación SPF/DKIM y reporte. |
| **RTO** | *Recovery Time Objective* | Tiempo máximo aceptable de parada del servicio. |
| **RPO** | *Recovery Point Objective* | Pérdida máxima aceptable de datos medido en tiempo. |
| **FHS** | *Filesystem Hierarchy Standard* | Jerarquía oficial de directorios en Linux. |

---

🏠 **[Volver al Índice Principal](../../README.md)** | 📖 **[Ir a la Guía Teórica (Resumen)](./RESUMEN-UT07-explotacion-aplicaciones.md)**
