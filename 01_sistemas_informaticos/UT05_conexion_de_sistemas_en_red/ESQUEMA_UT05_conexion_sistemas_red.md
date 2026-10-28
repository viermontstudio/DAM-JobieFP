🏠 **[Volver al Índice Principal](../../README.md)** | 📖 **[Ir a la Guía Teórica (Resumen)](./RESUMEN_UT05_conexion_sistemas_red.md)**

---

---

# 🌐 UT05 — Conexión de Sistemas en Red
## 📖 Esquema Maestro Integrado de Estudio

> **Módulo:** Sistemas Informáticos (1º DAM/DAW)  
> **Propósito:** Documento de síntesis estructurado por capas para el estudio activo y preparación de exámenes técnicos.

---

## 🗺️ 1. Mapa Arquitectónico Visual (Modelo TCP/IP por Plantas)

```text
┌────────────────────────────────────────────────────────────────────────┐
│ PLANTA 4: APLICACIÓN (Lo que tú ves y pides)                           │
│ DNS (Agenda telefónica) | DHCP (Recepcionista) | HTTP/HTTPS | SSH      │
└───────────────────────────────────┬────────────────────────────────────┘
                                    ▼
┌────────────────────────────────────────────────────────────────────────┐
│ PLANTA 3: TRANSPORTE (¿Cómo viaja la caja?)                            │
│ TCP (Burofax certificado) vs UDP (Megáfono sin acuse) | Puertos        │
└───────────────────────────────────┬────────────────────────────────────┘
                                    ▼
┌────────────────────────────────────────────────────────────────────────┐
│ PLANTA 2: RED / INTERNET (El cartero y la dirección postal)            │
│ IP (Dirección lógica) | ARP (Traduce IP a MAC) | ICMP (Ping / Sonar)   │
└───────────────────────────────────┬────────────────────────────────────┘
                                    ▼
┌────────────────────────────────────────────────────────────────────────┐
│ PLANTA 1: ACCESO AL MEDIO Y FÍSICO (El asfalto y el hardware)          │
│ MAC (DNI físico) | Switch (Filtra por MAC) | Cobre (UTP/STP) | Fibra   │
└────────────────────────────────────────────────────────────────────────┘
```

---

## 🧱 2. Desglose Estructurado por Capas y Componentes

### 🛣️ Planta 1: Acceso al Medio y Nivel Físico (El Hardware Local)
En esta capa no existen programas ni direcciones IP. Únicamente circulan impulsos eléctricos, destellos de luz y señales de radio.

* **Medios de Cobre (Par Trenzado):**
  * **UTP (*Unshielded Twisted Pair*):** Par trenzado **sin apantallar**. Económico y flexible. Utiliza conectores de plástico **RJ45**.
  * **STP (*Shielded Twisted Pair*):** Par trenzado **apantallado individualmente** (malla metálica en cada par de hilos). Protege contra interferencias graves. Utiliza conectores metálicos **RJ49** conectados a masa.
  * **FTP (*Foiled Twisted Pair*):** Pantalla de aluminio global que envuelve a los 4 pares a la vez.
* **Medios de Fibra Óptica (Transmisión por Luz):**
  * **Monomodo (SMF):** Núcleo muy estrecho (~9 µm). El haz láser viaja recto sin rebotar. Diseñado para **largas distancias** (decenas de kilómetros).
  * **Multimodo (MMF):** Núcleo más ancho (~50-62.5 µm). La luz LED viaja rebotando en zigzag. Diseñado para **distancias cortas** dentro de edificios o CPDs.
  * **Conectores habituales:** **SC** (cuadrado / *push-pull*), **LC** (compacto con pestaña, estándar en racks) y **ST** (cilíndrico con fijación por bayoneta).
* **Identificación Física y Dispositivos:**
  * **Dirección MAC (*Media Access Control*):** Identificador físico único de 48 bits (representado en hexadecimal) grabado de fábrica en la NIC (*Network Interface Card*).
  * **Switch (Conmutador):** Dispositivo de Capa 2. Mantiene una tabla MAC-Puerto para reenviar tramas exclusivamente al destinatario correcto.

---

### 📮 Planta 2: Red / Internet (El Enrutamiento y Direccionamiento)
Gestiona el viaje del paquete entre distintas redes independientes a través de routers.

* **Protocolo IP (*Internet Protocol*):** Asigna direcciones lógicas a los dispositivos.
  * **IPv4:** 32 bits expresados en 4 octetos decimales (ej. `192.168.1.10`).
  * **IPv6:** 128 bits expresados en hexadecimal. Posee una cabecera fija de 40 bytes para optimizar el procesamiento en routers.
* **Protocolos Clave de Capa de Red (Las Trampas de Examen):**
  * **ARP (*Address Resolution Protocol*):** Traduce **IP lógica \(
ightarrow\) MAC física**. Permite que un equipo averigüe la dirección MAC del destinatario dentro de la misma red local.
  * **DNS (*Domain Name System*):** Traduce **Nombre de dominio \(
ightarrow\) IP lógica** (ej. `google.es` \(
ightarrow\) `142.250.184.195`). Funciona como la agenda telefónica de Internet.
  * **ICMP (*Internet Control Message Protocol*):** Protocolo de diagnóstico y reporte de errores. Es la base del comando `ping`.

---

### 🚚 Planta 3: Transporte y Puertos
Se encarga de la comunicación extremo a extremo entre aplicaciones mediante **puertos de red**.

* **TCP (*Transmission Control Protocol*):** Orientado a conexión. Realiza el saludo a tres vías (*3-way handshake*). Garantiza la entrega ordenada y sin errores de los datos (retransmite si hay pérdidas). Usado en Web, Email, SSH, FTP.
* **UDP (*User Datagram Protocol*):** No orientado a conexión. Envía datagramas a máxima velocidad sin confirmación de recepción. Usado en streaming, VoIP, juegos online y consultas DNS.
* **Tabla de Puertos Estándar Críticos:**

| Puerto | Protocolo | Descripción / Servicio |
| :---: | :---: | :--- |
| **20 / 21** | TCP | **FTP** (*File Transfer Protocol*) — Transferencia de archivos |
| **22** | TCP | **SSH** (*Secure Shell*) — Terminal remota cifrada |
| **53** | UDP/TCP | **DNS** (*Domain Name System*) — Sonda y resolución de nombres |
| **67 / 68** | UDP | **DHCP** (*Dynamic Host Configuration Protocol*) — Configuración IP automática |
| **80** | TCP | **HTTP** (*Hypertext Transfer Protocol*) — Web no cifrada |
| **443** | TCP | **HTTPS** (*HTTP Secure*) — Web cifrada con TLS/SSL |

---

### 💻 Planta 4: Aplicación y Diagnóstico del Sistema
Soporta los programas que interactúan con el usuario y las herramientas de administración del sistema operativo.

* **Direccionamiento Especial / Salvavidas:**
  * **APIPA (*Automatic Private IP Addressing*):** Rango `169.254.0.0/16`. Se asigna automáticamente cuando un cliente DHCP no logra contactar con ningún servidor DHCP.
  * **Loopback (Realimentación Local):** `127.0.0.1` (IPv4) / `::1` (IPv6). Permite probar la pila de red local sin salir a la red.

---

## 🛠️ 3. Comandos de Diagnóstico: Tabla Comparativa Windows vs. Linux

| Función de Diagnóstico | Comando en Windows | Comando en Linux |
| :--- | :--- | :--- |
| **Consultar IP, máscara y puerta de enlace** | `ipconfig` (añadir `/all` para MAC y DHCP) | `ip a` / `ip addr` (antiguo: `ifconfig`) |
| **Ver conexiones activas y puertos abiertos** | `netstat -an` / `netstat -ab` (Administrador) | `ss -tln` / `netstat -ltup` |
| **Ver tabla de enrutamiento** | `route print` | `ip route` (antiguo: `route -n`) |
| **Prueba de conectividad y latencia** | `ping <IP_Destino>` (envía 4 paquetes) | `ping <IP_Destino>` (continuo hasta `Ctrl+C`) |
| **Trazar la ruta salto a salto** | `tracert <IP_Destino>` | `traceroute <IP_Destino>` / `tracepath` |

---

## 🛡️ 4. Modelo de Seguridad CIAA

Son los cuatro pilares fundamentales para evaluar la seguridad de un sistema o comunicación en red:

1. **Confidencialidad:** Garantiza que la información solo sea accesible por usuarios o procesos autorizados (mecanismos: cifrado, HTTPS, permisos).
2. **Integridad:** Asegura que los datos no hayan sido alterados o corrompidos durante su almacenamiento o transmisión (mecanismos: funciones Hash, sumas de verificación).
3. **Disponibilidad:** Garantiza que los servicios e información estén accesibles cuando los usuarios legítimos los necesiten (mecanismos: redundancia, balanceo de carga, mitigación anti-DDoS).
4. **Autenticación y No Repudio:** Confirma la identidad del emisor y evita que este pueda negar la autoría o envío de una transacción realizada.

---

## 📚 5. Glosario Mnemotécnico de Siglas

| Sigla | Nombre Completo en Inglés | Traducción al Español | Función Clave |
| :--- | :--- | :--- | :--- |
| **ARP** | *Address Resolution Protocol* | Protocolo de Resolución de Direcciones | Traduce dirección IP a dirección MAC |
| **DHCP** | *Dynamic Host Configuration Protocol* | Protocolo de Configuración Dinámica de Host | Asigna IP, máscara y DNS de forma automática |
| **DNS** | *Domain Name System* | Sistema de Nombres de Dominio | Traduce nombres de dominio a direcciones IP |
| **ICMP** | *Internet Control Message Protocol* | Protocolo de Mensajes de Control de Internet | Mensajes de diagnóstico y errores (base de `ping`) |
| **MAC** | *Media Access Control* | Control de Acceso al Medio | Identificador físico grabado en la tarjeta de red |
| **UTP** | *Unshielded Twisted Pair* | Par Trenzado No Apantallado | Cable de red estándar sin malla metálica protectora |
| **STP** | *Shielded Twisted Pair* | Par Trenzado Apantallado | Cable con pantalla metálica individual por par |
| **FTP** | *Foiled Twisted Pair* | Par Trenzado con Pantalla de Aluminio | Cable con lámina de aluminio global sobre todos los pares |

---

🏠 **[Volver al Índice Principal](../../README.md)** | 📖 **[Ir a la Guía Teórica (Resumen)](./RESUMEN_UT05_conexion_sistemas_red.md)**
