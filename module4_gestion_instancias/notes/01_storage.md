
# 📝 Clase: Tipos de almacenamiento en la nube

**Módulo:** 4 – Introducción a la Computación en la Nube
**Fecha:** 2025‑06‑20
**Duración:** \~11 min
**Fuente:** Curso “Configuration Management and the Cloud” – Google IT Automation


## 💡 Conceptos clave

### 💾 Tipos de almacenamiento en la nube

#### 📘 1. Almacenamiento en bloque (Block Storage)

* Simula discos duros tradicionales conectados a una VM.
* Se gestiona como si fuera una unidad física.
* **Ejemplo:** discos persistentes en GCP o EBS en AWS.

| Tipo            | Uso habitual                                                               |
| --------------- | -------------------------------------------------------------------------- |
| **Persistente** | Datos que deben conservarse entre reinicios.                               |
| **Efímero**     | Datos temporales que se eliminan al apagar la VM. Ideal para contenedores. |

> 📌 *Ideal para servidores que necesitan un sistema de archivos local*

#### 📗 2. Sistemas de archivos compartidos

* Accesibles por múltiples instancias mediante protocolos como **NFS** o **CIFS**.
* Permiten que varias máquinas trabajen sobre los mismos datos.

> 🗂️ Útil en aplicaciones distribuidas donde se requiere acceso concurrente

#### 📙 3. Almacenamiento de objetos (Object Storage o Blob)

* Almacena objetos (fotos, vídeos, archivos binarios, JSON...) en un "bucket".
* No hay sistema de archivos: se accede por nombre único.
* Usa una API o herramientas específicas para interactuar.

| Característica | Descripción                                             |
| -------------- | ------------------------------------------------------- |
| Escalabilidad  | Altamente escalable, ideal para datos no estructurados. |
| Acceso         | Mediante API HTTP o utilidades de proveedor.            |
| Casos de uso   | Backups, contenido multimedia, logs.                    |

> 🎯 Ejemplo: **GCP Cloud Storage**, **AWS S3**, **Azure Blob Storage**


### 🗄️ Bases de datos como servicio (DBaaS)

#### 🟦 SQL (Relacionales)

* Usan estructuras de tablas.
* Lenguaje de consulta: **SQL**.
* Compatible con apps existentes.

#### 🟩 NoSQL

* Escalabilidad horizontal.
* Muy rápido para grandes volúmenes.
* Requiere reescribir la lógica de acceso a datos (API específica).


### ❄️ Clases de almacenamiento

| Clase        | Frecuencia de acceso | Costo mensual | Tecnología                 |
| ------------ | -------------------- | ------------- | -------------------------- |
| **Caliente** | Acceso frecuente     | Más caro      | SSD o discos rápidos       |
| **Frío**     | Acceso infrecuente   | Más barato    | HDD o almacenamiento lento |

> 🧊 *Ejemplo:* Archivos que solo consultas después de 1 año → pasa de caliente a frío

### ⚙️ Métricas de rendimiento en almacenamiento

| Métrica        | Significado                                                                  |
| -------------- | ---------------------------------------------------------------------------- |
| **Throughput** | Cantidad de datos transferidos por segundo (ej. 1 GB/s).                     |
| **IOPS**       | Número de operaciones de entrada/salida por segundo (no depende del tamaño). |
| **Latencia**   | Tiempo que tarda en completarse una operación (lectura o escritura).         |

> 📈 *La elección de almacenamiento impacta directamente en el rendimiento del servicio.*

## 🧠 Notas para repaso

* Hay múltiples tipos de almacenamiento en la nube: **bloque**, **objetos**, y **archivos compartidos**.
* **Bloque** → VM tradicional; **objetos** → apps modernas con blobs; **archivos compartidos** → entornos multiinstancia.
* Las **bases de datos en la nube** pueden ser SQL o NoSQL según el tipo de aplicación.
* El almacenamiento puede ser **efímero o persistente**, **caliente o frío**, según el uso.
* Las métricas clave para evaluar el rendimiento del almacenamiento son: **throughput**, **IOPS** y **latencia**.


## 📦 Almacenamiento en bloque (Block Storage)

**🧩 Qué es:**
Imita un **disco duro tradicional**. El proveedor divide el almacenamiento en bloques (secciones pequeñas de datos) que puedes formatear con el sistema de archivos que tú elijas.

**🛠 Cómo se usa:**

* Se conecta a **una máquina virtual como un disco**.
* Es gestionado por el **sistema operativo del host** (como si fuera `/dev/sda1` en Linux).
* Ideal para bases de datos, sistemas operativos, aplicaciones que necesitan acceso directo y rápido al disco.

**✅ Ejemplos de uso:**

* Montar un disco en una VM para instalar PostgreSQL o MySQL.
* Usar el disco para guardar los archivos del sistema y logs de una app.
* Crear snapshots para backup.

**📌 Ejemplos en la nube:**

* **AWS:** EBS (Elastic Block Store)
* **GCP:** Persistent Disk
* **Azure:** Managed Disks

## 🎯 Almacenamiento de objetos (Object Storage)

**🧱 Qué es:**
Diseñado para almacenar archivos completos como **objetos individuales** dentro de un sistema plano llamado **bucket (cubo)**. Cada objeto tiene:

* Un contenido (archivo binario)
* Metadatos
* Un identificador único (clave)

**🌐 Cómo se accede:**

* Usando una **API HTTP/REST** o herramientas específicas.
* No hay sistema de archivos; no se monta como un disco.
* No puedes hacer “lectura de sectores”, solo acceder o subir el objeto completo.

**✅ Ejemplos de uso:**

* Subir y servir imágenes o vídeos (como en un CDN o una web).
* Almacenar backups grandes o registros (logs).
* Guardar archivos estáticos en apps web.

**📌 Ejemplos en la nube:**

* **AWS:** S3 (Simple Storage Service)
* **GCP:** Cloud Storage
* **Azure:** Blob Storage


## 📊 Comparativa rápida

| Característica      | Almacenamiento en bloque         | Almacenamiento de objetos              |
| ------------------- | -------------------------------- | -------------------------------------- |
| Tipo de acceso      | Como disco duro (bloques)        | Mediante API / HTTP                    |
| Sistema de archivos | Lo gestiona el SO                | No hay sistema de archivos             |
| Casos de uso        | Bases de datos, SO, apps         | Backups, imágenes, vídeos              |
| Rendimiento         | Alto, acceso rápido              | Escalable, pero más lento              |
| Estructura          | Jerárquica (sistema de ficheros) | Plana (bucket + objetos)               |
| Compartición        | Difícil de compartir             | Fácil de acceder desde cualquier lugar |


## 🧠 Analogía rápida

* 🧱 **Bloque:** como un disco duro USB conectado a tu ordenador.
* 🎁 **Objeto:** como una caja en un almacén de Amazon a la que accedes por número de tracking.

## 📊 Métricas clave del uso de almacenamiento

### 1. **IOPS (Input/Output Operations Per Second)**

* **¿Qué es?**
  Número de operaciones de entrada/salida que puede manejar un disco por segundo.

* **Incluye:**
  Lecturas y escrituras de bloques pequeños, como acceder a archivos o escribir en una base de datos.

* **Ejemplo:**
  Un disco SSD puede ofrecer hasta 100.000 IOPS, mientras que un HDD ofrece típicamente entre 75 y 200.

* **¿Por qué es importante?**
  Es fundamental en sistemas con muchas operaciones pequeñas y rápidas (bases de datos, servidores web).

### 2. **Throughput (Ancho de banda)**

* **¿Qué es?**
  Cantidad total de datos que se pueden transferir hacia o desde el disco por segundo.

* **Se mide en:**
  MB/s o GB/s.

* **Ejemplo:**
  Un SSD puede alcanzar 500 MB/s, mientras que un HDD suele estar por debajo de 150 MB/s.

* **¿Por qué es importante?**
  Crucial cuando trabajas con archivos grandes (copias de seguridad, vídeos, ISO, archivos log).

### 3. **Latency (Latencia)**

* **¿Qué es?**
  Tiempo que tarda una operación de lectura o escritura en completarse.

* **Se mide en:**
  Milisegundos (ms) o microsegundos (μs).

* **Tipos comunes:**

  * Latencia de lectura
  * Latencia de escritura

* **Ejemplo:**
  Un HDD tiene una latencia típica de 5-10 ms, mientras que un SSD puede estar por debajo de 1 ms.

* **¿Por qué es importante?**
  Afecta directamente la **respuesta del sistema**. Alta latencia = lentitud perceptible, especialmente en aplicaciones interactivas.

### 4. **Read Throughput / Write Throughput**

* **¿Qué es?**
  Velocidad de lectura o escritura separadas, en MB/s o IOPS.

* **Importante para:**

  * **Lectura intensiva:** servidores web, consultas a base de datos.
  * **Escritura intensiva:** logs, backups, servidores de monitoreo.

### 5. **Read IOPS / Write IOPS**

* **¿Qué es?**
  Cuántas operaciones de lectura/escritura se realizan por segundo (por separado).

* **¿Por qué diferenciarlo?**
  Algunos discos están optimizados más para lectura (por ejemplo, cachés) o para escritura (como registros de logs o bases NoSQL).

### 6. **Disk Usage (%)**

* **¿Qué es?**
  Porcentaje de espacio usado del total disponible en el disco.

* **¿Por qué es importante?**
  Cuando el disco se llena:

  * El sistema puede volverse inestable.
  * Las escrituras pueden fallar.
  * La fragmentación puede aumentar.

### 7. **Disk Queue Length (Longitud de cola)**

* **¿Qué es?**
  Número de operaciones de I/O pendientes en espera de ser procesadas.

* **Interpretación:**

  * Baja: el disco responde bien.
  * Alta: hay cuellos de botella; el sistema espera demasiado.

## 🎯 Comparación rápida de uso

| Métrica           | Mide                          | Ideal para detectar                                   |
| ----------------- | ----------------------------- | ----------------------------------------------------- |
| IOPS              | Frecuencia de accesos         | Saturación por apps con muchas transacciones pequeñas |
| Throughput (MB/s) | Volumen de datos transferidos | Límite físico del disco o bus                         |
| Latency (ms/μs)   | Velocidad de respuesta        | Lento acceso aleatorio                                |
| Disk Usage (%)    | Espacio consumido             | Riesgo de quedarse sin espacio                        |
| Queue Length      | Cuántas operaciones esperan   | Cuellos de botella del sistema                        |

## 🧠 ¿Cómo se usan en la práctica?

* En **monitorización cloud** (Google Cloud, AWS, Azure), se usan estas métricas para:

  * Escalar recursos automáticamente.
  * Activar **alertas** si se supera cierto umbral (p. ej., >80% disk usage).
  * Tomar decisiones: ¿necesito un SSD en lugar de un HDD?

* En **infraestructura local** (Linux, VMs):

  * Puedes ver estas métricas con herramientas como:

    * `iostat`, `vmstat`, `iotop`, `df`, `du` en Linux.
    * Monitor de rendimiento en Windows.

## 🧪 Ejemplo de interpretación real

Supón que tienes una base de datos que:

* Muestra **IOPS muy altos**.
* Tiene **latencia >10 ms**.
* Cola de disco elevada.

🔍 Conclusión: el disco está saturado. Soluciones posibles:

* Migrar a un SSD.
* Separar logs y base de datos en discos distintos.
* Incrementar IOPS permitidos si estás en la nube (por ejemplo, EBS en AWS o PD en GCP).
