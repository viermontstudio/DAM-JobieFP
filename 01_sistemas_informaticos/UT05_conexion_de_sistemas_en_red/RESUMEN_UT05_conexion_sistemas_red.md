🏠 **[Volver al Índice Principal](../../README.md)** | 📐 **[Ir al Esquema Resumen](./ESQUEMA_UT05_conexion_sistemas_red.md)**

---

# 🌐 GUÍA TEÓRICA Y RESUMEN — UT05: Conexión de Sistemas en Red
**Asignatura:** Sistemas Informáticos (1º DAM/DAW)  
**Marco Metodológico:** Protocolo PEM-4 & Metodología Interna DAM

---

## 1. Clasificación de Redes y Topologías
* **Por Alcance Geográfico:**
  * **PAN (*Personal Area Network*):** Cobertura personal reducida (pocos metros, ej. Bluetooth, NFC).
  * **LAN (*Local Area Network*):** Red de área local dentro de un edificio o vivienda (Ethernet / Wi-Fi).
  * **MAN (*Metropolitan Area Network*):** Cobertura a nivel de ciudad o campus extenso.
  * **WAN (*Wide Area Network*):** Red de área amplia que interconecta países o continentes (ej. Internet).
* **Por Topología Física:**
  * **Estrella:** Todos los nodos se conectan a un dispositivo central (**Switch**). Si falla un nodo, la red sigue funcionando.
  * **Malla / Malla Total:** Conexiones punto a punto redundantes entre nodos. Utilizado en entornos de alta disponibilidad.
  * **Bus / Anillo / Árbol:** Topologías tradicionales o jerárquicas.

---

## 2. Medios Físicos de Transmisión y Conectores
* **Cables de Par Trenzado de Cobre:**
  * **UTP (*Unshielded Twisted Pair*):** Sin blindaje individual ni global. Económico y flexible. Conector **RJ45**.
  * **STP (*Shielded Twisted Pair*):** Malla metálica protectora alrededor de cada par individual contra interferencias electromagnéticas. Conector **RJ49** metálico con toma a tierra.
  * **FTP (*Foiled Twisted Pair*):** Pantalla global de aluminio que envuelve a todos los pares conjuntamente.
* **Fibra Óptica:**
  * **Monomodo (SMF):** Núcleo muy fino (~9 µm), luz emitida por láser en trayectoria recta. Cubre **decenas de kilómetros** sin repetidores.
  * **Multimodo (MMF):** Núcleo más grueso (~50-62.5 µm), luz emitida por LED en múltiples modos/ángulos de rebote. Para **distancias cortas** dentro de edificios o CPDs (<2 km).
  * **Conectores de Fibra:** **SC** (cuadrado / *push-pull*), **LC** (pequeño con pestaña, estándar en racks modernos) y **ST** (cilíndrico de bayoneta).

---

## 3. Modelos de Referencia: OSI vs. TCP/IP
| Capa OSI (7 Capas) | Capa TCP/IP (4 Capas) | Protocolos / Elementos Representativos |
| :--- | :--- | :--- |
| **7. Aplicación**<br>**6. Presentación**<br>**5. Sesión** | **4. Aplicación** | HTTP, HTTPS, DNS, DHCP, SSH, FTP, SMTP |
| **4. Transporte** | **3. Transporte** | TCP, UDP (Puertos de origen y destino) |
| **3. Red** | **2. Internet** | IP (IPv4 / IPv6), ICMP, ARP, Routers |
| **2. Enlace de Datos**<br>**1. Física** | **1. Acceso a la Red** | MAC, Ethernet, Wi-Fi, Switches, Cables, Conectores |

---

## 4. Capa de Red y Direccionamiento IP
* **Dirección IP (Lógica):** Identificador temporal único en la red.
  * **IPv4:** 32 bits expresados en 4 octetos decimales (ej. `192.168.1.50`).
  * **IPv6:** 128 bits expresados en hexadecimal (ej. `2001:db8::1`). Cabecera fija optimizada de 40 bytes.
* **Máscara de Subred:** Define qué parte de la dirección IP identifica a la red y qué parte identifica al host (ej. `/24` o `255.255.255.0`).
* **Dirección MAC (Física):** Identificador permanente grabado de fábrica en la tarjeta de red (NIC) de 48 bits expresado en hexadecimal (ej. `00:1A:2B:3C:4D:5E`).

---

## 5. Protocolos Fundamentales
* **ARP (*Address Resolution Protocol*):** Traduce una dirección **IP conocida a la dirección MAC física** de destino en la red local.
* **DNS (*Domain Name System*):** Traduce nombres de dominio legibles (`google.es`) a direcciones IP numéricas. Puerto **53 (UDP/TCP)**.
* **DHCP (*Dynamic Host Configuration Protocol*):** Asigna de forma automática direcciones IP, máscaras, puertas de enlace y DNS a los clientes de la red.
  * **Rango APIPA (`169.254.X.X`):** Dirección asignada automáticamente por el S.O. cuando el servidor DHCP no responde.
* **ICMP (*Internet Control Message Protocol*):** Protocolo de diagnóstico para reporte de errores en red, utilizado por el comando **`ping`**.

---

## 6. Capa de Transporte y Puertos
* **TCP (*Transmission Control Protocol*):** Orientado a conexión (saludo a 3 vías: SYN \(\rightarrow\) SYN-ACK \(\rightarrow\) ACK), fiable, garantiza la entrega ordenada mediante acuse de recibo.
* **UDP (*User Datagram Protocol*):** No orientado a conexión, rápido, sin garantía de entrega ni control de flujo (ideal para streaming, llamadas VoIP y juegos online).
* **Puertos Esenciales:**
  * `20 / 21` : FTP (Transferencia de archivos)
  * `22` : SSH (Consola remota segura)
  * `53` : DNS (Consultas de nombres)
  * `80` : HTTP (Navegación web plana)
  * `443` : HTTPS (Navegación web cifrada TLS/SSL)

---

## 7. Dispositivos de Interconexión
* **Switch (Conmutador - Capa 2):** Conecta equipos dentro de la misma red LAN. Utiliza la **tabla MAC** para enviar los marcos de datos únicamente al puerto del destinatario.
* **Router (Enrutador - Capa 3):** Interconecta redes diferentes y determina la mejor ruta para enviar paquetes mediante la **tabla de rutas** e IP.

---

## 8. Comandos CLI de Diagnóstico en Windows y Linux

| Función | Comandos en Windows | Comandos en Linux |
| :--- | :--- | :--- |
| **Configuración IP y MAC** | `ipconfig` / `ipconfig /all` | `ip a` / `ip addr` |
| **Tabla de Rutas** | `route print` | `ip route` |
| **Conexiones y Puertos Abiertos** | `netstat -an` | `ss -tln` / `netstat -ltup` |
| **Diagnóstico de Conectividad** | `ping <IP_o_Host>` | `ping <IP_o_Host>` |
| **Trazado de Ruta por Saltos** | `tracert <IP>` | `traceroute <IP>` |

---

## 9. Seguridad en Redes: Modelo CIAA
* **C — Confidencialidad:** Garantizar que la información solo sea accesible por personal o procesos autorizados (mediante cifrado).
* **I — Integridad:** Asegurar que los datos no hayan sido alterados o corrompidos durante el tránsito (mediante funciones hash).
* **A — Disponibilidad (*Availability*):** Garantizar que los sistemas y servicios estén operativos cuando los usuarios los necesiten.
* **A — Autenticación / No Repudio:** Confirmar la identidad legítima del emisor e impedir que pueda negar la autoría del mensaje.

---

🏠 **[Volver al Índice Principal](../../README.md)** | 📐 **[Ir al Esquema Resumen](./ESQUEMA_UT05_conexion_sistemas_red.md)**
