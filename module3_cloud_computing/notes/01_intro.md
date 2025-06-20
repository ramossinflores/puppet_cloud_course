
# 📝 Clase: ¿Qué significa que un servicio se ejecute en la nube?

**Módulo:** 3 – Introducción a la Computación en la Nube
**Fecha:** 2025‑06‑20
**Duración:** \~8 min
**Fuente:** Curso “Configuration Management and the Cloud” – Google IT Automation

## 💡 Conceptos clave

### ☁️ ¿Qué significa que algo esté “en la nube”?

* No significa que esté en el cielo, sino que se ejecuta en **infraestructura remota** (centros de datos) accesible por Internet.
* Los servicios en la nube se ejecutan sobre **máquinas virtuales** (VMs) que pueden tener distintos niveles de rendimiento (discos SSD, almacenamiento en red, etc.).

### 🧩 Modelos de servicio en la nube

| Tipo de servicio                       | Significado                                                 | ¿Quién gestiona qué?                               | Ejemplos                                         |
| -------------------------------------- | ----------------------------------------------------------- | -------------------------------------------------- | ------------------------------------------------ |
| **SaaS** (Software as a Service)       | El proveedor entrega un software completo                   | El proveedor gestiona todo                         | Gmail, Dropbox, Office 365                       |
| **PaaS** (Platform as a Service)       | Plataforma lista para usar sin gestionar la infraestructura | El proveedor gestiona hardware y entorno           | Google App Engine, servicios de SQL gestionados  |
| **IaaS** (Infrastructure as a Service) | Infraestructura virtual básica (VMs, red)                   | Tú gestionas el SO, el software y la configuración | Amazon EC2, Google Compute Engine, Azure Compute |

### 🌍 Regiones y zonas en la nube

* Una **región** es una ubicación geográfica con varios centros de datos.
* Una **zona** es una subunidad dentro de una región (alta disponibilidad).
* Elegir bien la región:

  * **Cercanía a usuarios** (menor latencia)
  * **Requisitos legales/políticos**
  * **Ubicación de servicios dependientes** (ej. servidor de correo + base de datos)

> Ejemplo: si estás en Europa y accedes a tu banco ubicado en EE.UU., puede haber más latencia.

### 🛠️ Caso real: Qwiklabs

* Qwiklabs usa **IaaS**.
* Se aprovisionan máquinas virtuales con un sistema operativo base.
* El resto del software y configuraciones se aplican mediante automatización de laboratorios.


## 🧠 Notas para repaso

* Los servicios en la nube se ejecutan **remotamente en centros de datos**.
* Existen tres modelos: **SaaS, PaaS e IaaS**, con diferentes niveles de control.
* Las **regiones y zonas** impactan en la latencia, la legalidad y la arquitectura del sistema.
* Qwiklabs es un ejemplo práctico de uso de IaaS con automatización