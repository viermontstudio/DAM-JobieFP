[🏠 Volver al Índice Principal](../../README.md) | [📐 Ir al Esquema Resumen](./SI-UT01-ESQUEMA-explotacion-sistemas.md)

# 📖 GUÍA TEÓRICA DE ESTUDIO — UT01: Desarrollo de Software
**Asignatura:** Entornos de Desarrollo (1º DAM/DAW)  
**Código de Módulo:** ED | **Unidad de Trabajo:** UT01  
**Marco Metodológico:** Protocolo PEM-4 & Metodología Interna DAM v5.1  

---

## 🏛️ Nivel 1: Conceptos Clave (Fundamentos Didácticos)

### 1.1. ¿Qué es un Programa Informático?
Un **programa informático** es una secuencia ordenada de instrucciones escritas en un lenguaje interpretable o compilable que un ordenador ejecuta de forma secuencial o condicional para realizar una tarea concreta.
* **Ejemplo Canónico:** El clásico `"Hello World"` (*"Hola Mundo"*), cuyo objetivo es afianzar la sintaxis del lenguaje y verificar la correcta instalación del Entorno de Desarrollo (IDE).
* **Diferencia Fundamental con un Documento:** Mientras que un documento pasivo (como un archivo PDF o TXT) almacena únicamente datos estáticos, un programa contiene **instrucciones ejecutables** que manipulan registros de memoria, procesan entradas y producen salidas en el procesador.

### 1.2. ¿Qué es una Aplicación Informática?
Una **aplicación informática** es un sistema o ecosistema complejo compuesto por múltiples programas coordinados, librerías compartidas, interfaces de usuario y componentes de persistencia (bases de datos) que colaboran para resolver necesidades del mundo real.
* **Ecosistema / Suites:** Microsoft Office o SAP no son programas aislados, sino suites o aplicaciones compuestas por programas interconectados (Word, Excel, módulos de facturación e inventario).

### 1.3. Clasificación del Software: A Medida vs. Estándar

| Criterio | Software a Medida (Custom) | Software Estándar (Enlatado / ERP) |
| :--- | :--- | :--- |
| **Definición** | Desarrollo exclusivo ajustado a los procesos únicos de un cliente. | Producto genérico comercializado para múltiples empresas (ej. SAP, Odoo). |
| **Coste Inicial** | Elevado (el cliente asume el 100% del desarrollo). | Económico (el coste se amortiza por economía de escala). |
| **Tiempo de Despliegue** | Largo (requiere ciclo completo de desarrollo). | Inmediato / Corto (requiere instalación y parametrización). |
| **Ajuste Funcional** | 100% adaptado a reglas de negocio particulares. | Puede incluir funciones superfluas o carecer de reglas específicas. |
| **Mantenimiento** | Continuo, adaptativo y costoso tras la implantación. | Soportado por el fabricante mediante parches globales. |

### 1.4. Evolución de los Lenguajes de Programación
1. **Lenguaje Máquina (1ª Generación):** Cadenas binarias (`0` y `1`). Directamente ejecutable por la CPU pero incomprensible e ineficiente para seres humanos.
2. **Lenguaje Ensamblador (2ª Generación):** Introducción de palabras mnemotécnicas (`MOV`, `ADD`, `PUSH`). Próximo al hardware y dependiente de la arquitectura de la CPU.
3. **Lenguajes de Alto Nivel (3ª Generación y posteriores):** Sintaxis cercana al lenguaje humano (`Python`, `Java`, `JavaScript`, `C++`). Incorporan abstracciones como la **Programación Orientada a Objetos (POO)**.

---

## 🎯 Nivel 2: Claves de Examen (Repaso Crítico para Evaluación ISFP / DAM)

### 2.1. Compilación vs. Interpretación vs. Máquina Virtual

| Característica | Lenguajes Compilados (C/C++) | Lenguajes Interpretados (Python/JS) |
| :--- | :--- | :--- |
| **Traductor** | Compilador (g++, clang) | Intérprete (Python V8 / Node.js) |
| **Momento de Trad.** | Todo el código de golpe previo | Línea a línea en tiempo de ejec. |
| **Artefacto Generado** | Ejecutable binario nativo (.exe) | Ninguno (ejecución directa) |
| **Rendimiento** | Máxima velocidad y optimización | Menor velocidad, overhead en RAM |
| **Portabilidad** | Requiere recompilar por SO/CPU | Alta portabilidad (depende interpr) |

* **Modelo Híbrido / Virtual (Java):** Java compila el código fuente (`.java`) a un código intermedio ejecutable llamado **Bytecode** (`.class`). La **Máquina Virtual de Java (JVM)** interpreta o compila mediante JIT (*Just-In-Time*) dicho bytecode en cualquier sistema operativo, logrando el hito: *"Escribe una vez, ejecuta en cualquier lugar"*.

### 2.2. Pipeline de Compilación en C/C++
Es un punto crítico de examen memorizar el orden secuencial estricto de las 4 etapas del pipeline:

1. **Preprocesado:** Expansión de directivas (`#include`, `#define`), eliminación de comentarios.
2. **Compilación:** Traducción del código fuente preprocesado a código ensamblador (`.s`).
3. **Ensamblado:** Conversión de ensamblador a **Código Objeto** binario relocalizable (`.o` / `.obj`).
4. **Enlazado (Linking):** Combinación de archivos de código objeto y librerías estáticas/dinámicas para generar el **Código Ejecutable** final.

### 2.3. Ciclo de Vida del Software (SDLC)
1. **Fase Inicial / Planificación:** Definición de objetivos, viabilidad económica y tecnológica.
2. **Análisis:** Obtención y documentación de los **requisitos funcionales y no funcionales** del cliente.
3. **Diseño:** Planificación de la arquitectura (diseño genérico y detallado, diagramas UML, esquemas de BD).
4. **Codificación / Implementación:** Construcción del código fuente siguiendo estándares.
5. **Pruebas (QA):** Pruebas funcionales (validan requisitos con el cliente) y estructurales (rendimiento, seguridad).
6. **Explotación / Despliegue:** Puesta en producción en el servidor/hosting para usuarios finales.
7. **Mantenimiento:** Fase más larga y costosa del ciclo de vida (correctivo, adaptativo y perfectivo).

### 2.4. Roles en un Equipo de Desarrollo
* 📐 **Arquitecto de Software:** Diseña la estructura global, patrones arquitectónicos y tecnologías base.
* 🎼 **Jefe de Proyecto (Project Manager / Scrum Master):** Coordina plazos, recursos y relación con el cliente.
* 🔍 **Analista de Sistemas:** Traduce necesidades de negocio del cliente en especificaciones técnicas.
* 🔨 **Programador / Desarrollador:** Implementa la lógica escribiendo código limpio y documentado.

---

## 🛠️ Nivel 3: Profundización Técnica y Empleabilidad

### 3.1. Ecosistema de Lenguajes y Salidas Profesionales

* **JavaScript & Node.js:** Rey indiscutible del desarrollo web Full Stack. Permite usar el mismo lenguaje en Frontend (`React`, `Angular`, `Vue`) y Backend (`Node.js`, `Express`).
* **Java & Spring Boot:** Estándar corporativo dominante en banca, seguros y grandes sistemas empresariales backend gracias a la solidez de la JVM y su arquitectura orientada a objetos.
* **Python:** Lenguaje de referencia para Inteligencia Artificial, Data Science, Scripting y backend ágil (`Django`, `Flask`).
* **C / C++:** Dominio absoluto en programación de bajo nivel, controladores (drivers), sistemas embebidos (IoT), motores de videojuegos (`Unreal Engine`) y aplicaciones de alto rendimiento.
* **PHP:** Impulsa más del 70% de la web mundial mediante CMSs tradicionales (`WordPress`) y frameworks de desarrollo profesional como `Laravel`.

### 3.2. Buenas Prácticas de Documentación y Control de Versiones
1. **Manuales Obligatorios del Software:**
   * **Manual de Usuario:** Explicación funcional en lenguaje sencillo para el operador final.
   * **Manual Técnico:** Detalle del código, arquitectura, diagramas e APIs para desarrolladores.
   * **Manual de Instalación:** Procedimientos de despliegue, variables de entorno y dependencias.
2. **Control de Versiones con Git & Metodologías Ágiles:**
   * El trabajo en equipo moderno exige el uso diario de `Git` (commits atómicos, ramas, *Pull Requests* / *Code Reviews*) combinado con marcos de trabajo ágiles como **Scrum** o **Kanban**.