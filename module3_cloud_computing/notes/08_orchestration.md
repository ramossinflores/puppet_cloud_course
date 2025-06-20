
# 📝 Clase: Introducción a la orquestación en entornos en la nube

**Módulo:** 3 – Introducción a la Computación en la Nube
**Fecha:** 2025‑06‑20
**Duración:** \~7 min
**Fuente:** Curso “Configuration Management and the Cloud” – Google IT Automation

## 💡 Conceptos clave

### 🔁 ¿Qué es la automatización?

* **Automatización** = sustituir tareas manuales por procesos que se ejecutan automáticamente.
* En la nube ya hemos visto ejemplos:

  * Uso de **plantillas** para crear VMs.
  * Uso de **CLI** (`gcloud`, por ejemplo).
  * **Escalado automático** basado en demanda.

### 🧠 ¿Qué es la orquestación?

* La **orquestación** es la **coordinación automática de múltiples servicios y sistemas** que necesitan funcionar juntos.
* No solo automatiza la creación, sino también la **conexión, configuración y comportamiento** entre recursos.

> **Automatización = tareas individuales**
> **Orquestación = sistemas enteros funcionando en conjunto**

### 🧱 Ejemplo práctico

Supón que quieres replicar toda tu infraestructura web en otro centro de datos:

* Necesitas:

  * Crear todos los tipos de instancias (web, caché, base de datos…).
  * Configurar redes, accesos, reglas de firewall.
  * Asegurar que **todos los servicios se comunican entre sí correctamente**.

Esto se puede orquestar para que **todo ocurra automáticamente**, de forma repetible y coherente.

### 🔌 Uso de APIs para orquestación

* Las **herramientas de orquestación no usan la web o la CLI directamente**, sino que interactúan con la **API del proveedor cloud**.
* Las APIs permiten:

  * Crear, modificar y eliminar recursos.
  * Aplicar configuraciones complejas desde scripts.
  * Integrar con otras aplicaciones.

> **Ventaja clave:** puedes controlar toda tu infraestructura desde un **programa o script centralizado**.


### ☁️ Nube híbrida y orquestación

* Muchas empresas combinan servicios en la nube y en servidores locales: esto se llama **nube híbrida**.
* La orquestación ayuda a que **ambos entornos se comuniquen** y se configuren correctamente.

  * Red interna
  * Seguridad y firewall
  * Servicios compartidos (DNS, autenticación, base de datos…)


### 📈 Orquestar el monitoreo y alertas

* Una parte crítica de cualquier infraestructura es el **monitoreo proactivo**:

  * Qué métricas observar (CPU, RAM, errores…)
  * Qué alertas enviar y cuándo
* Configurarlo manualmente en cada nodo es costoso.
* Las herramientas de orquestación permiten:

  * **Automatizar el monitoreo**
  * Aplicar las mismas reglas en entornos completos (on-prem y nube)

## 🧠 Notas para repaso

* La **orquestación va más allá de la automatización individual**: se encarga de que todos los servicios funcionen como un sistema cohesionado.
* Usa **APIs cloud** para ejecutar tareas complejas desde scripts, no desde GUI ni terminales manuales.
* Permite **configuraciones repetibles** para diferentes entornos (por ejemplo, replicar una infraestructura completa en otra región).
* Es esencial para **escenarios híbridos** donde servicios locales y cloud deben convivir.
* Automatiza también tareas de **monitorización y alertas**, lo que mejora la fiabilidad del sistema.
