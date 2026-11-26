[🏠 Volver al Índice Principal](../../README.md) | [📖 Ir a la Guía Teórica (Resumen)](./ED-UT01-RESUMEN-desarrollo-de-software.md)

# 💻 ESQUEMA DE ESTUDIO — UT01: Desarrollo de Software
**Asignatura:** Entornos de Desarrollo (1º DAM/DAW)  
**Código de Módulo:** ED | **Unidad de Trabajo:** UT01  
**Marco Metodológico:** Protocolo PEM-4 & Metodología Interna DAM v5.1  

---

## 🗺️ Mapa Conceptual 1: Taxonomía y Visión Global del Software

```text
+--------------------------------------------------------------------------------+
| 1. CONCEPTO DE PROGRAMA vs. APLICACIÓN INFORMÁTICA                             |
| Programa: Secuencia de instrucciones para tarea concreta (ej. Hello World)     |
| Aplicación: Ecosistema complejo de programas, librerías y BD (ej. Office)      |
+--------------------------------------------------------------------------------+
                                        v                                         
+--------------------------------------------------------------------------------+
| 2. CLASIFICACIÓN DEL SOFTWARE: A MEDIDA vs. ESTÁNDAR                           |
| A Medida: Adaptación 100% a procesos | Alto coste inicial y mantenimiento      |
| Estándar: Producto genérico (SAP/Odoo) | Económico por economía de escala      |
+--------------------------------------------------------------------------------+
                                        v                                         
+--------------------------------------------------------------------------------+
| 3. LENGUAJES DE PROGRAMACIÓN Y PARADIGMAS                                      |
| 1ª Gen: Lenguaje Máquina (Binario 0/1 ejecutable directo en CPU)               |
| 2ª Gen: Lenguaje Ensamblador (Mnemónicos MOV, ADD, PUSH)                       |
| 3ª Gen+: Alto Nivel (Java, Python, JS, C++) con Objetos (POO)                  |
+--------------------------------------------------------------------------------+
                                        v                                         
+--------------------------------------------------------------------------------+
| 4. MODELOS DE TRADUCCIÓN Y EJECUCIÓN                                           |
| Compilados (C/C++): Traducción previa total a binario nativo (.exe)            |
| Interpretados (Python/JS): Traducción línea a línea en tiempo real             |
| Híbridos (Java): Compilación a Bytecode (.class) ejecutado en la JVM           |
+--------------------------------------------------------------------------------+
                                        v                                         
+--------------------------------------------------------------------------------+
| 5. ROLES TÉCNICOS EN EL EQUIPO DE DESARROLLO                                   |
| Arquitecto (MVC) | Jefe de Proyecto (Scrum) | Analista (ERS) | Programador      |
+--------------------------------------------------------------------------------+
```

---

## ⚙️ Diagrama ASCII 2: Pipeline de Compilación en C/C++ (4 Etapas)

```text
+--------------------------------------------------------------------------------+
| PIPELINE DE COMPILACIÓN EN C / C++ (4 ETAPAS SECUENCIALES)                     |
+--------------------------------------------------------------------------------+
| CÓDIGO FUENTE (.cpp / .c) - Código escrito por el desarrollador                |
                                        |                                         
                                        v                                         
| [ETAPA 1: PREPROCESADOR]  ---> Genera Código Expandido (.i)                    |
|   Sustituye directivas #include, expande macros y quita comentarios            |
                                        |                                         
                                        v                                         
| [ETAPA 2: COMPILADOR]     ---> Genera Código Ensamblador (.s / .asm)           |
|   Traduce la sintaxis C/C++ a instrucciones mnemotécnicas de la CPU            |
                                        |                                         
                                        v                                         
| [ETAPA 3: ENSAMBLADOR]    ---> Genera Código Objeto Binario (.o / .obj)        |
|   Convierte mnemónicos a lenguaje máquina relocalizable                        |
                                        |                                         
                                        v                                         
| [ETAPA 4: ENLAZADOR / LINKER] ---> Genera CÓDIGO EJECUTABLE (.exe / ELF)       |
|   Combina objetos binarios y librerías del sistema en ejecutable final         |
+--------------------------------------------------------------------------------+
```

---

## ☕ Diagrama ASCII 3: Modelo Híbrido de Ejecución Java (JVM)

```text
+--------------------------------------------------------------------------------+
| ARQUITECTURA DE PORTABILIDAD JAVA (JVM)                                        |
+--------------------------------------------------------------------------------+
| CÓDIGO FUENTE JAVA (.java)                                                     |
                                        |                                         
                                        v                                         
| COMPILADOR JAVA (javac) ---> Genera Bytecode Intermedio (.class)               |
                                        |                                         
| Lema: 'Escribe una vez, ejecuta en cualquier lugar' (WORA)                     |
                                        |                                         
                +-----------------------+-----------------------+                 
                |                       |                       |                 
                v                       v                       v                 
| JVM Windows             JVM Linux               JVM macOS                      |
                |                       |                       |                 
                v                       v                       v                 
| Nativo Win x64          Nativo Linux x64        Nativo macOS ARM               |
+--------------------------------------------------------------------------------+
```

---

## 🏗️ Diagrama ASCII 4: Arquitectura Patrón MVC (Modelo-Vista-Controlador)

```text
+--------------------------------------------------------------------------------+
| PATRÓN ARQUITECTÓNICO MODELO-VISTA-CONTROLADOR (MVC)                          |
+--------------------------------------------------------------------------------+
|                                                                                |
|  [VISTA / View] ------------ (1) Petición / Evento ---------> [CONTROLADOR]    |
|  Interfaz de Usuario                                          Lógica Negocio   |
|  (Formularios, HTML, App) <--- (4) Renderizado / Datos ------- (Controller)    |
|                                                                    |           |
|                                                               (2) Invoca /     |
|                                                               Actualiza        |
|                                                                    v           |
|                                                                [MODELO]        |
|                                                               Persistencia /   |
|                                                               Entidades / BD   |
|                                                                                |
+--------------------------------------------------------------------------------+
| Clave: Desacoplamiento total entre Presentación (Vista) y Datos (Modelo).     |
+--------------------------------------------------------------------------------+
```

---

## 🔄 Diagrama ASCII 5: Ciclo de Vida del Software (SDLC - 7 Fases)

```text
+--------------------------------------------------------------------------------+
| CICLO DE VIDA DEL SOFTWARE (SDLC - 7 FASES)                                    |
+--------------------------------------------------------------------------------+
| 1. PLANIFICACIÓN   ---> Requisitos iniciales, viabilidad y presupuesto         |
                                        |                                         
                                        v                                         
| 2. ANÁLISIS        ---> Criterios de Aceptación y Firma ERS/SRS (Scope Frozen) |
                                        |                                         
                                        v                                         
| 3. DISEÑO         ---> Arquitectura MVC, Modelado de Datos y Diagramas UML     |
                                        |                                         
                                        v                                         
| 4. CODIFICACIÓN   ---> Implementación en IDE, estándares de código y Git       |
                                        |                                         
                                        v                                         
| 5. PRUEBAS (QA)    ---> Pruebas Unitarias (clases) y de Integración (sistema)  |
                                        |                                         
                                        v                                         
| 6. EXPLOTACIÓN     ---> Despliegue en Servidores / Puesta en Producción        |
                                        |                                         
                                        v                                         
| 7. MANTENIMIENTO   ---> Fase más larga y costosa (>60% presupuesto total)      |
+--------------------------------------------------------------------------------+
```

---

## ⏱️ Diagrama ASCII 6: Modelos de Desarrollo (Cascada vs. Sprints Ágiles)

```text
+--------------------------------------------------------------------------------+
| MODELO EN CASCADA (WATERFALL) - Secuencial y Rígido                            |
| [Análisis] ---> [Diseño] ---> [Codificación] ---> [Pruebas] ---> [Entrega]    |
| (El cliente solo ve el resultado al final del proyecto)                        |
+--------------------------------------------------------------------------------+

+--------------------------------------------------------------------------------+
| METODOLOGÍA ÁGIL (SCRUM / SPRINTS) - Iterativo e Incremental                   |
| [Sprint 1: 2-4 sem] ---> Incremento 1 Funcional ---> Validación Cliente        |
| [Sprint 2: 2-4 sem] ---> Incremento 2 Funcional ---> Validación Cliente        |
| [Sprint N: 2-4 sem] ---> Producto Final Entregado                              |
+--------------------------------------------------------------------------------+
```

---

## 📊 Tabla Comparativa de Repaso Rápido

| Lenguaje | Tipo de Ejecución | Paradigma Principal | Ecosistema / Uso Destacado |
| :--- | :--- | :--- | :--- |
| **Java** | Híbrido (Bytecode + JVM) | POO Pura | Backend Bancario, Android, Big Data (Spring Boot) |
| **Python** | Interpretado | Multiparadigma | IA, Machine Learning, Data Science, Scripting |
| **JavaScript** | Interpretado (JIT V8) | Event-Driven / POO | Frontend Web (React/Angular), Backend (Node.js) |
| **C / C++** | Compilado Nativo | Estructurado / POO | Bajo Nivel, Embebidos, Motores Gráficos |
| **PHP** | Interpretado | Imperativo / POO | Servidores Web, CMSs (WordPress, Laravel) |
