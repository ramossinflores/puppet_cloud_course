
# 📦 Gestión de la Configuración y la Nube (Puppet + GCP)

Este repo documenta el progreso, las prácticas, manifiestos `.pp`, notas técnicas y desafíos realizados en el curso **Gestión de la Configuración y la Nube**, perteneciente al programa **Google IT Automation with Python**, cursado gracias a una **beca del SEPE (Servicio Público de Empleo Estatal)**.

## 🎯 Objetivo del curso

El curso tiene como finalidad introducir los fundamentos de la **administración de configuraciones**, el uso de herramientas como **Puppet** y conceptos clave de **infraestructura como código** en entornos cloud, especialmente Google Cloud Platform (GCP).



## 🧱 Estructura del repositorio

```

puppet-cloud-course/
├── module1_automatizacion_config/
│   └── notes/
│       └── 01_intro.md
├── module2_despliegue_puppet/
│   ├── manifests/
│   ├── notes/
│   ├── labs/
├── module3_automatizacion_nube/
│   ├── notes/
│   ├── cloud/
├── module4_gestion_nube_escala/
│   ├── notes/
│   ├── cloud/
├── .gitignore
└── README.md

````

## 📚 Módulos del curso

| Módulo | Contenido principal |
|--------|---------------------|
| **1** | Automatización con administración de configuraciones |
| **2** | Despliegue y aplicación local de Puppet |
| **3** | Automatización y despliegue de recursos en GCP |
| **4** | Supervisión, gestión a escala y solución de problemas en la nube |

---

## 🧪 Cómo utilizar este repositorio

- Los **manifiestos Puppet** se encuentran en la carpeta `manifests/` del módulo 2.
- Las **notas técnicas** en Markdown están dentro de cada carpeta `notes/`.
- Los **laboratorios prácticos (Qwiklabs)** se documentan en `labs/`.
- La carpeta `cloud/` contiene archivos y plantillas utilizadas en despliegues sobre Google Cloud.

---

## ▶️ Requisitos para reproducir los ejemplos localmente

Para ejecutar los manifiestos Puppet en un entorno de prueba:

- Visual Studio Code
- [Vagrant](https://www.vagrantup.com/)
- [VirtualBox](https://www.virtualbox.org/)
- Una máquina base con Puppet.

Ejemplo de uso:

```bash
vagrant up
vagrant ssh
sudo puppet apply /vagrant/module2_despliegue_puppet/manifests/01_aplicacion_local.pp
````


## ✍️ Autora

**Laura Ramos Granados**
Administradora de Sistemas en formación.
Este repositorio forma parte del programa oficial **Google IT Automation with Python**, cursado con el apoyo de una **beca del SEPE**, como parte de mi desarrollo profesional en automatización, sistemas, infraestructura cloud y tecnologías DevOps 🩷
