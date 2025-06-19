
# 📝 Clase: Definición de nodos en Puppet (`node`, `site.pp` y clases específicas)

**Módulo:** 2 – Despliegue de Puppet
**Fecha:** 2025‑06‑18
**Duración:** \~6 min
**Fuente:** Curso “Configuration Management and the Cloud” – Google IT Automation

## 💡 Conceptos clave

### 🖥️ ¿Qué es un nodo en Puppet?

* En Puppet, un **nodo** es cualquier sistema que ejecuta un **agente de Puppet**.
* Puede tratarse de un servidor físico, máquina virtual, estación de trabajo o incluso routers, siempre que puedan ejecutar el agente y recibir configuraciones.

### 🧾 Definición de nodos en Puppet

Puppet permite **aplicar reglas diferentes a distintos sistemas**. Esto se realiza mediante **definiciones de nodos**.

#### 🔧 Ejemplo básico:

```puppet
node default {
  include sudo
  class { 'ntp':
    servers => ['ntp.example.com'],
  }
}
```

* `node default` se aplica a **todos los nodos que no tengan una definición específica**.
* En este caso, todos los nodos:

  * Incluirán la clase `sudo`
  * Incluirán la clase `ntp` con el parámetro `servers` definido



### 🎯 Nodo específico por FQDN

Para establecer configuraciones distintas en ciertos sistemas:

```puppet
node 'webserver.example.com' {
  include apache
  include sudo
  class { 'ntp':
    servers => ['ntp.example.com'],
  }
}
```

* Aquí solo **`webserver.example.com`** recibirá la clase `apache`.
* Aunque `sudo` y `ntp` también están presentes, **se deben repetir** porque:

  > Las clases del nodo `default` **no se heredan automáticamente** si existe una definición específica para el nodo.



### 🧠 Optimización: clase base común

Para evitar duplicar reglas comunes:

```puppet
class base {
  include sudo
  include ntp
}

node default {
  include base
}

node 'webserver.example.com' {
  include base
  include apache
}
```

> Se centralizan las configuraciones comunes en una clase `base` y se reutiliza en todos los nodos.

## 📁 ¿Dónde se definen los nodos?

Las definiciones de nodos se colocan en el archivo especial:

```
/etc/puppetlabs/code/environments/production/manifests/site.pp
```

* **`site.pp`** no forma parte de ningún módulo.
* Es el **punto de entrada principal** para el compilador de Puppet.
* Allí se define qué clases se aplican a cada nodo.

## 🧠 Notas para repaso

* Un nodo es cualquier sistema gestionado por Puppet.
* Se puede asignar una configuración específica a un nodo mediante su FQDN.
* `default` es el nodo por defecto: se usa si no hay una definición específica.
* Las definiciones de nodo no son heredables entre sí.
* La clase `base` es una buena práctica para evitar duplicaciones.
* Toda esta lógica se centraliza en `site.pp`.
