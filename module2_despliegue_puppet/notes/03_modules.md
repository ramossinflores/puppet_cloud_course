
# 📝 Clase: Organización de la configuración con módulos en Puppet

**Módulo:** 2 – Despliegue de Puppet
**Fecha:** 2025‑06‑18
**Duración:** \~7 min
**Fuente:** Curso “Configuration Management and the Cloud” – Google IT Automation




## 💡 Conceptos clave

### 🧱 ¿Qué es un módulo en Puppet?

* Un **módulo** es una **colección estructurada de manifiestos y datos** que implementa configuraciones relacionadas.
* Sirve para mantener la configuración organizada, reutilizable y mantenible a largo plazo.

> Ejemplos de módulos: configuración de red, instalación de servicios como Apache o NTP, supervisión del sistema.



### 🗂 Estructura típica de un módulo Puppet

```plaintext
mimodulo/
├── manifests/
│   └── init.pp              ← archivo principal obligatorio
├── files/                   ← archivos que se copian sin cambios
├── templates/               ← plantillas con lógica dinámica (.erb)
├── lib/                     ← funciones adicionales personalizadas (opcional)
├── metadata.json            ← metadatos del módulo (nombre, compatibilidad, etc.)
```

* **`manifests/init.pp`**: define la clase principal del módulo. Es el **punto de entrada obligatorio**.
* **`files/`**: contiene archivos que se copian directamente en el nodo (por ejemplo, `ntp.conf`).
* **`templates/`**: contiene archivos `.erb` que se procesan antes de ser aplicados.
* **`lib/`**: puede incluir funciones personalizadas para extender Puppet (no obligatorio).
* **`metadata.json`**: archivo con información sobre el módulo (por ejemplo, compatibilidad con sistemas operativos).



## 🧪 Ejemplo: Modularización de la clase `ntp`

* El archivo `init.pp` contiene la clase `ntp` y sus recursos.
* El archivo de configuración `ntp.conf` se mueve al directorio `files/`.

> Esta estructura permite mantener juntos todos los recursos relacionados y facilita la reutilización.

## 📦 Uso de módulos de terceros

* Puppet Labs y otros equipos publican **módulos preempaquetados**.
* Estos pueden instalarse con herramientas como `puppet module install`.
* Ejemplo del vídeo: instalación del módulo `puppetlabs-apache`.

### 🔍 Exploración del módulo Apache

```bash
cd /etc/puppetlabs/code/modules/apache
ls
```

Se observaron los siguientes directorios:

* `manifests/` → contiene múltiples archivos `.pp` organizados por funcionalidades
* `files/` y `templates/`
* `lib/` → añade funciones extra
* `metadata.json` → describe compatibilidad y metadatos del módulo

> El archivo `init.pp` siempre debe estar presente en `manifests/` para que el módulo sea reconocible por Puppet.

## ⚙️ Aplicación de un módulo instalado

Para usar el módulo, se crea un manifiesto nuevo que lo **incluye**:

```puppet
include ::apache
```

* El prefijo `::` indica que se trata de un módulo **global**.

Luego se aplica como cualquier manifiesto local:

```bash
sudo puppet apply archivo.pp
```

> Esto ejecuta todas las configuraciones predeterminadas del módulo, como la instalación y activación del servidor Apache.

## 🧠 Notas para repaso

* Un módulo es una **unidad organizativa** para agrupar manifiestos, archivos y plantillas.
* Todos los módulos deben tener un archivo `init.pp` en su directorio `manifests/`.
* Es posible aprovechar **módulos creados por otros** para ahorrar tiempo y evitar errores.
* Los módulos facilitan la **escalabilidad y mantenimiento** de la infraestructura.
* La organización modular es una **buena práctica esencial** en entornos de administración de sistemas a gran escala.
