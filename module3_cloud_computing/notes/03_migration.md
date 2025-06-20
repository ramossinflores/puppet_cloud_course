
# 📝 Clase: Estrategias de migración y tipos de nubes

**Módulo:** 3 – Introducción a la Computación en la Nube
**Fecha:** 2025‑06‑20
**Duración:** \~10 min
**Fuente:** Curso “Configuration Management and the Cloud” – Google IT Automation


## 💡 Conceptos clave

### 🧳 ¿Qué es una migración a la nube?

* Migrar a la nube implica trasladar parte o toda la infraestructura de TI a **servidores virtuales gestionados por un proveedor de nube**.
* La estrategia dependerá del **estado actual de tu infraestructura** y del **objetivo de la migración**.
* Siempre se busca un equilibrio entre:

  * **Control** del sistema
  * **Esfuerzo de mantenimiento**

### 🪜 Lift and Shift (Levantar y trasladar)

* Estrategia donde se **replican los servidores físicos como máquinas virtuales** en la nube.
* La configuración **permanece igual**, solo cambia el entorno de ejecución.
* Ejemplo: mover físicamente un servidor a otra oficina → ahora sería migrarlo como VM a la nube.

> Ideal si ya usas herramientas de automatización de configuración (como Puppet o Ansible)

### ⚠️ Desventajas del Lift and Shift

* A pesar de migrar, **sigues gestionando**:

  * Instalación de aplicaciones
  * Actualizaciones del sistema operativo
  * Mantenimiento y parches
* Por eso, muchas empresas optan por **servicios más administrados**.


### 🧱 Alternativa: Plataforma como servicio (PaaS)

* Recomendado si **quieres mantener ciertas funcionalidades pero sin ocuparte de la administración diaria**.
* Ejemplos:

  * **Bases de datos SQL gestionadas**
  * **Aplicaciones web administradas**

#### Ejemplos de PaaS para aplicaciones web:

| Proveedor | Servicio          |
| --------- | ----------------- |
| Amazon    | Elastic Beanstalk |
| Microsoft | App Service       |
| Google    | App Engine        |

> ⚠️ Nota: no son totalmente compatibles entre sí. Migrar entre proveedores puede requerir cambios en el código.


### 📦 Contenedores (Containers)

* Aplicaciones **empaquetadas con sus configuraciones y dependencias**.
* Se ejecutan igual sin importar el entorno (local, nube pública o privada).
* Facilitan la portabilidad y **simplifican las migraciones**.



## ☁️ Tipos de nubes

| Tipo             | Definición                                                 | Características                               |
| ---------------- | ---------------------------------------------------------- | --------------------------------------------- |
| **Nube pública** | Servicios ofrecidos por un tercero al público general      | Escalable, de fácil acceso, coste compartido  |
| **Nube privada** | Infraestructura exclusiva de una empresa, in situ o remota | Mayor control y seguridad, más costosa        |
| **Nube híbrida** | Combinación de nube pública + privada                      | Flexibilidad, pero requiere buena integración |
| **Multinube**    | Uso de servicios de varios proveedores                     | Alta disponibilidad y tolerancia a fallos     |

> 🔁 Una **nube híbrida** puede ser una forma de **nube múltiple**, pero la nube múltiple siempre implica **más de un proveedor**

## 🧠 Notas para repaso

* **Lift and Shift** permite migrar servidores sin cambiar su configuración, pero sigues gestionando todo.
* **PaaS** delega la administración de la plataforma al proveedor, lo que acelera el desarrollo.
* **Contenedores** permiten ejecutar aplicaciones de forma **consistente** en distintos entornos.
* Hay varios **tipos de nubes**:

  * Pública (accesible)
  * Privada (dedicada)
  * Híbrida (mezcla)
  * Multinube (varios proveedores)
* Usar **multinube** puede prevenir caídas, aunque implica mayor coste y complejidad