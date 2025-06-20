
# 📝 Clase: Infraestructura como código y orquestación con Terraform

**Módulo:** 3 – Introducción a la Computación en la Nube
**Fecha:** 2025‑06‑20
**Duración:** \~8 min
**Fuente:** Curso “Configuration Management and the Cloud” – Google IT Automation

## 💡 Conceptos clave

### 🧾 Infraestructura como código (IaC)

* IaC = describir y gestionar la infraestructura **usando archivos de configuración similares a código**.
* Beneficios:

  * **Repetibilidad**: puedes desplegar el mismo entorno múltiples veces.
  * **Historial y control de versiones**: puedes ver qué cambió, cuándo y por qué.
  * **Deshacer errores fácilmente**.
  * Escalar con **equipos pequeños**.

> Esto aplica tanto a servidores locales como a la infraestructura en la nube

### 🏗 Herramientas nativas de cada proveedor (IaC específica)

| Proveedor           | Herramienta de IaC           |
| ------------------- | ---------------------------- |
| Amazon Web Services | CloudFormation               |
| Google Cloud        | Deployment Manager           |
| Microsoft Azure     | Azure Resource Manager       |
| OpenStack           | Heat Orchestration Templates |

* Problema: **solo funcionan con su propio ecosistema**, lo que dificulta:

  * La migración entre proveedores.
  * El uso de entornos híbridos.


### 🌍 Terraform: IaC independiente del proveedor

* Terraform es una herramienta de IaC **open source y multiplataforma**.
* Usa su propio lenguaje (HCL – HashiCorp Configuration Language).
* Interactúa con múltiples proveedores a través de **sus APIs**.

  * AWS, Azure, GCP, Kubernetes, Docker, VMware, etc.
* Te permite:

  * Diseñar infraestructuras **portables y reutilizables**.
  * Gestionar tanto nubes públicas como servicios locales (**híbridos**).
  * Declarar qué necesitas (VM, red, firewall, almacenamiento...) y Terraform se encarga de ejecutarlo.

> 🔄 Similar a cómo Puppet define un estado deseado y el agente lo aplica, Terraform compara el estado actual vs deseado y realiza cambios.


### 🖥 ¿Qué se puede definir con Terraform?

Ejemplos de recursos:

* Máquinas virtuales
* Redes y subredes
* Reglas de firewall
* Volúmenes persistentes
* Clústeres de contenedores
* DNS, balanceadores, funciones lambda...


### 🧱 Instancias de larga vs corta duración

| Tipo               | Ejemplo                               | Mantenimiento                                      | Uso de Puppet                                      |
| ------------------ | ------------------------------------- | -------------------------------------------------- | -------------------------------------------------- |
| **Larga duración** | Servidor de correo, archivos, LDAP... | Se **mantienen actualizadas** durante su vida útil | Puppet ejecuta cambios periódicamente              |
| **Corta duración** | VMs en autoescalado, nodos efímeros   | Se **reemplazan** en lugar de actualizarse         | Puppet solo se usa **al inicio**, no continuamente |

> En nubes modernas, **la mayoría de las instancias son de corta duración**, por lo que la configuración inicial es clave

### 🔁 Puppet vs Terraform (y complementarios)

| Puppet                                       | Terraform                                                   |
| -------------------------------------------- | ----------------------------------------------------------- |
| Administra **el contenido interno** del nodo | Crea y destruye **infraestructura externa**                 |
| Se ejecuta dentro del nodo (agente)          | Se ejecuta desde un cliente externo                         |
| Ideal para servidores vivos (larga duración) | Ideal para despliegues declarativos y repetibles            |
| Puede usarse con módulos cloud               | Puede usar scripts de configuración (Puppet, Ansible, etc.) |

> **Ambas herramientas se pueden combinar** para cubrir todo el ciclo de vida de una infraestructura

## 🧠 Notas para repaso

* La **infraestructura como código** permite diseñar, desplegar y versionar entornos cloud como si fueran código.
* Herramientas como **Terraform** permiten gestionar infraestructuras en varios proveedores con el mismo lenguaje.
* Puedes tener **configuraciones híbridas** (parte en la nube, parte en local) y gestionarlas de forma unificada.
* Las instancias **cortas** se regeneran con nuevas versiones; las **largas** se mantienen actualizadas en producción.
* **Terraform ≠ Puppet**, pero se complementan muy bien:

  * Terraform = crea el terreno
  * Puppet = decora la casa
