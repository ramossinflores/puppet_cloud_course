
# 📝 Clase: Creación de una máquina virtual en Google Cloud Platform (GCP)

**Módulo:** 3 – Introducción a la Computación en la Nube
**Fecha:** 2025‑06‑20
**Duración:** \~7 min
**Fuente:** Curso “Configuration Management and the Cloud” – Google IT Automation

---

## 💡 Conceptos clave

### ☁️ Creación de un proyecto en GCP

* Accede a la consola: [console.cloud.google.com](https://console.cloud.google.com).
* Lo primero que debes hacer es **crear un proyecto**: todas las máquinas virtuales estarán asociadas a ese proyecto.
* Ejemplo de nombre: `First Cloud Steps`.


### 🖥️ Creación de una VM desde Compute Engine

Ruta:
**Menú principal → Compute Engine → Instancias de VM → Crear instancia**

Allí podrás configurar:

1. **Nombre de la instancia:**

   * Ejemplo: `linux-instance`.

2. **Región y zona:**

   * Selecciona la más cercana a tus usuarios para reducir la latencia.
   * En el ejemplo se usan los valores por defecto.

3. **Tipo de máquina:**

   * Uso general o memoria optimizada.
   * Se puede elegir número de vCPUs y memoria RAM.
   * En el ejemplo se mantiene la configuración predeterminada.

4. **Disco de arranque:**

   * Selección de sistema operativo (Debian, Ubuntu, etc.).
   * Ejemplo: Ubuntu.
   * Tipo de disco: estándar (más barato) o SSD (más rápido).
   * Se puede ajustar el tamaño si necesitas más almacenamiento.

### 🔐 Configuración de acceso y firewall

* **Acceso SSH:** se activa por defecto, permite conectarse a la máquina remotamente.
* **Reglas de firewall:**

  * Puedes permitir tráfico **HTTP** y/o **HTTPS** al crear la instancia.
  * En este ejemplo se activa HTTP para uso posterior con un servidor web.



### 📜 Opción avanzada: comando equivalente en CLI

* Antes de crear la VM, puedes hacer clic en “**Línea de comandos**” para ver el comando `gcloud` equivalente.
* Esto permite:

  * Automatizar la creación.
  * Reutilizar el comando para crear múltiples VMs idénticas.

> Aunque es un comando largo, no necesitas entenderlo todo de inmediato. Es útil para scripting y replicación

### 🖧 Proceso de creación y conexión

* Tras hacer clic en **Crear**, la instancia se prepara:

  * Se asignan recursos.
  * Se aplica la imagen del SO.
  * Se conectan redes y claves SSH.
* Luego puedes conectarte a la instancia mediante SSH desde el navegador.


## 🧪 Prueba básica: conexión SSH y uso del sistema

Una vez dentro de la VM (como si fuera una máquina Linux cualquiera):

```bash
curl wttr.in
```

Este comando consulta el clima en formato texto, como demostración de acceso a Internet desde la VM.


## 🧠 Notas para repaso

* **Todo en GCP gira en torno a proyectos:** las VMs deben estar asociadas a uno.
* Al crear una VM debes configurar:

  * Nombre, región, tipo de máquina, SO, disco, acceso, reglas de red.
* La **GUI (interfaz web)** es intuitiva y muestra estimaciones de coste.
* Puedes **ver el comando CLI equivalente (`gcloud`)** para replicar instancias automáticamente.
* El acceso por **SSH** se configura automáticamente desde el navegador.
* Una vez dentro, la máquina se comporta como un **Linux normal**: puedes instalar paquetes, ejecutar scripts, etc