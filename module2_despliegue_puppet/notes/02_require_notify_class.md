
# 📝 Clase: Relaciones entre recursos y clases en Puppet – `require`, `notify`, `class`

**Módulo:** 2 – Despliegue de Puppet
**Fecha:** 2025‑06‑18
**Duración:** \~6 min
**Fuente:** Curso “Configuration Management and the Cloud” – Google IT Automation



## 🎯 Objetivos

* Entender cómo **relacionar recursos** en Puppet para controlar el orden de aplicación.
* Conocer el uso de `require` y `notify` para **dependencias y acciones automáticas**.
* Aprender a **agrupar recursos en clases** y usarlas en manifiestos.
* Aplicar buenas prácticas de organización en manifiestos Puppet.

## 💡 Conceptos clave

### 🔗 Relaciones entre recursos

Puppet permite definir **dependencias** entre recursos. Esto garantiza que se apliquen en el orden correcto.

#### ✅ Ejemplo

```puppet
file { '/etc/ntp.conf':
  ensure  => 'file',
  content => template('ntp/ntp.conf.erb'),
  require => Package['ntp'],
  notify  => Service['ntp'],
}

package { 'ntp':
  ensure => 'present',
}

service { 'ntp':
  ensure => 'running',
  enable => true,
  require => File['/etc/ntp.conf'],
}
```

### 🧠 ¿Qué significa esto?

* El archivo de configuración **requiere** que el paquete `ntp` esté instalado antes.
* El servicio `ntp` **requiere** que el archivo de configuración esté presente.
* Si el archivo cambia, se **notifica** al servicio `ntp`, que se reinicia automáticamente.



### ✍️ Detalle importante de sintaxis

* Cuando declaras tipos de recursos:
  → `package`, `file`, `service` → en minúsculas.
* Cuando los **nombras dentro de relaciones** (`require`, `notify`):
  → `Package['ntp']`, `File['/etc/ntp.conf']` → con la **primera letra en mayúscula**.

🔔 No es un error: **así funciona la sintaxis de Puppet**.



## 🧱 Uso de `class` en Puppet

Puedes agrupar recursos relacionados en una **clase** para organizarlos mejor.

#### 📂 Ejemplo simple:

```puppet
class ntp {
  package { 'ntp': ... }
  file { '/etc/ntp.conf': ... }
  service { 'ntp': ... }
}

include ntp
```

En este ejemplo:

* Se define una clase `ntp` con todos los recursos necesarios.
* Se incluye la clase en el manifiesto con `include ntp`.

> En producción, es común tener la definición de la clase en un archivo y la inclusión en otro.



## 🧪 Prueba práctica

1. Puppet aplicó las reglas definidas:

   * Instaló el paquete `ntp`
   * Modificó el archivo `/etc/ntp.conf`
   * Reinició el servicio automáticamente gracias a `notify`

2. Editaron manualmente el archivo de configuración:

   * Cambiaron los servidores de `ntp.org` a `time1.google.com` hasta `time4.google.com`.

3. Se volvió a ejecutar:

   * Puppet detectó el cambio en el archivo.
   * Aplicó el nuevo contenido.
   * Reinició el servicio `ntp` automáticamente.



## 🧠 Notas para mi cerebro

* Puedes **encadenar recursos** para que Puppet actúe en orden.
* `require` = “esto debe hacerse antes”
* `notify` = “si esto cambia, haz algo”
* Puppet es capaz de **detectar cambios y reiniciar servicios** por sí solo.
* Agrupar recursos en clases ayuda a mantener el manifiesto **limpio y reutilizable**.
* La **mayúscula en los nombres** dentro de relaciones no es opcional: es parte de la sintaxis.

