

# 📝 Clases: Preparación, imagen y despliegue automatizado de instancias en GCP

**Módulo:** 3 – Introducción a la Computación en la Nube
**Fecha:** 2025‑06‑20
**Duración combinada:** \~13 min
**Fuente:** Curso “Configuration Management and the Cloud” – Google IT Automation


## 💡 Conceptos clave

### 🔧 Configurar una VM como base para escalado

1. **Conectarse a la VM creada previamente**.
2. **Clonar un repositorio** con una app web escrita en Python.
3. **Ejecutar la app en el puerto 80 con privilegios:**

   ```bash
   sudo python3 app.py 80
   ```
4. La app responde con:

   * `"Hello Cloud"`
   * Nombre de host e IP pública de la VM.


### 🛠️ Hacer que la app se inicie automáticamente con systemd

1. El repositorio incluye un archivo `.service` compatible con **systemd**.
2. Pasos para configurarlo:

   ```bash
   sudo cp app.py /usr/local/bin/
   sudo cp hello.service /etc/systemd/system/
   sudo systemctl enable hello
   sudo systemctl start hello
   ```
3. Tras reiniciar la VM:

   ```bash
   ps ax | grep hello
   ```

   Verificamos que el servicio está activo.



### 🧩 Integrar Puppet para gestión futura

* La VM se prepara para integrarse con **Puppet Master**.
* Se instala el cliente con un script incluido en el repositorio:

  ```bash
  sudo ./setup_puppet.sh
  ```
* Puppet se configura para iniciarse al arrancar.


## 🖼️ Crear una imagen de disco (imagen de referencia)

1. **Apagar la VM** desde la consola.
2. Ir al menú del **disco de arranque** de la instancia.
3. Crear una **imagen nueva** desde ese disco:

   * Ejemplo de nombre: `webserver-image`.
   * Se conservará todo el contenido relevante excepto elementos únicos (hostname, IP…).


## 📐 Crear una plantilla de instancia

1. Ir a **Instance templates → Crear nueva plantilla**.
2. Configurar:

   * Nombre: `servidor-web-plantilla`.
   * Imagen: seleccionar `webserver-image` creada previamente.
   * Activar tráfico HTTP.
   * Dejar el resto en valores por defecto.

> Esta plantilla incluye toda la configuración predefinida: SO, app, reglas de red, tipo de máquina, etc

## ⚙️ Crear una instancia desde plantilla

1. Desde Compute Engine → Crear instancia.
2. Seleccionar la plantilla como base.
3. Asignar un nombre a la VM (ej: `servidor-web-uno`).
4. Resultado: la nueva VM ya tiene la app funcionando, sin configuración manual.



## 💻 Automatizar el despliegue con `gcloud`

1. Instalar y configurar el CLI:

   ```bash
   gcloud init
   ```

   * Inicia sesión con cuenta de Google.
   * Selecciona proyecto, región y zona por defecto.

2. Crear 5 VMs usando la plantilla:

   ```bash
   gcloud compute instances create ws1 ws2 ws3 ws4 ws5 \
     --source-instance-template=servidor-web-plantilla
   ```

> ✅ Esto es mucho más rápido y automatizable que usar la interfaz web manualmente


## 🧠 Notas para repaso

* Puedes convertir una VM configurada en una **imagen de disco reutilizable**.
* A partir de esa imagen, creas una **plantilla de instancia**, que predefine los valores de red, disco, SO, etc.
* Las plantillas permiten **crear VMs a gran escala** de forma consistente.
* El **CLI de Google Cloud (`gcloud`)** permite crear instancias por lotes fácilmente.
* **systemd** se usa para lanzar automáticamente servicios al arrancar la VM.
* **Puppet** permite aplicar cambios futuros a todas las VMs sin necesidad de recrearlas.

