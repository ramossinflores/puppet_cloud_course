
# 📝 Clase: Creación y automatización de máquinas virtuales en la nube

**Módulo:** 3 – Introducción a la Computación en la Nube
**Fecha:** 2025‑06‑20
**Duración:** \~9 min
**Fuente:** Curso “Configuration Management and the Cloud” – Google IT Automation



## 💡 Conceptos clave

### 🧭 Exploración inicial de una plataforma cloud

* Los proveedores de nube ofrecen una **consola de gestión** para visualizar y administrar sus servicios.
* Aunque los nombres pueden variar entre proveedores (AWS, Azure, Google Cloud…), los **conceptos son comunes**.
* Recomendación: familiarízate con los menús antes de crear recursos.



### ⚙️ Creación de una instancia de máquina virtual (VM)

Al crear una VM en la nube, debes definir varios **parámetros clave**:

1. **Nombre de la instancia**: te permitirá identificarla para conectarte, modificarla o eliminarla.
2. **Región y zona**: selecciona una ubicación **cercana a los usuarios** para reducir la latencia.
3. **Tipo de máquina**: define el número de **vCPU y RAM**.

   * Cuanto más potente, mayor el coste.
   * Empieza con una configuración **pequeña y escala** si es necesario.
4. **Disco de arranque**:

   * Incluye el **sistema operativo** y espacio de almacenamiento.
   * Puedes seleccionar el **tamaño del disco** y el tipo de SO (Linux, Windows, etc.).

### 🖥️ Interfaces para crear recursos

| Interfaz                    | Características                                                     | Cuándo usar                                         |
| --------------------------- | ------------------------------------------------------------------- | --------------------------------------------------- |
| **Web (GUI)**               | Visual, muestra comparativas de opciones y coste estimado           | Ideal para experimentar o tareas puntuales          |
| **Línea de comandos (CLI)** | Requiere escribir comandos, permite **automatización y repetición** | Útil para entornos con múltiples máquinas o scripts |

## 🛠️ Automatización de despliegues: Imágenes y plantillas

### 📸 Imagen de disco

* Es una **instantánea** del disco de una VM en un momento determinado.
* Incluye sistema operativo, software y configuraciones.

### 🧱 Plantilla de VM

* Permite capturar una configuración y **reutilizarla para crear múltiples VMs idénticas**.
* No incluye elementos únicos como hostname o IP.
* Muy útil para entornos con **escalado masivo** (ej. desplegar 10.000 VMs con el mismo software).

> Las imágenes y plantillas permiten automatizar la creación de máquinas virtuales **de forma fiable y consistente**

## 🧠 Notas para repaso

* Los **proveedores cloud** ofrecen consolas y CLI para gestionar recursos; Google Cloud es usado como ejemplo en este curso.
* Al crear una VM, seleccionas: nombre, región/zona, tipo de máquina, disco y sistema operativo.
* Es recomendable iniciar con una configuración **básica** y luego escalar según la demanda.
* La interfaz web es intuitiva; la CLI permite **automatizar**.
* Las **imágenes de disco** son instantáneas reutilizables de máquinas configuradas.
* Las **plantillas** te permiten replicar configuraciones para múltiples VMs.
* La **automatización del despliegue** ahorra tiempo, asegura consistencia y facilita la gestión a gran escala.
