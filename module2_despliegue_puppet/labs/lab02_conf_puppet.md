# 📅 Laboratorio de Puppet con Qwiklabs

**Fecha:** 2025-06-19
**Plataforma:** Qwiklabs
**Temática:** Automatización de configuraciones con Puppet (cliente-servidor)



## 📄 Resumen del laboratorio

Durante este laboratorio se completó una implementación funcional de Puppet para automatizar la gestión de una flota de sistemas con distintos sistemas operativos (Debian, RedHat, Windows, etc.). Las tareas se realizaron en dos máquinas virtuales:

* `puppet` (servidor Puppet Master)
* `linux-instance` (cliente administrado por Puppet)

Se editaron manifiestos, se aplicaron reglas condicionales mediante *facts*, se gestionaron paquetes por familia de sistema operativo, se crearon plantillas con ERB y se construyó un módulo nuevo llamado `reboot`.



## 🔧 Tareas realizadas

### 1. **Instalación condicional de paquetes**

Ruta del módulo: `/etc/puppet/code/environments/production/modules/packages/manifests/init.pp`

* Se añadió la instalación de `golang` solo para sistemas Debian:

```puppet
if $facts[os][family] == "Debian" {
  package { 'golang':
    ensure => installed,
  }
}
```

* Se implementó también para `nodejs` en sistemas RedHat:

```puppet
if $facts[os][family] == "RedHat" {
  package { 'nodejs':
    ensure => installed,
  }
}
```

### 2. **Creación de módulo `machine_info` para recopilar información del sistema**

Ruta: `/etc/puppet/code/environments/production/modules/machine_info/`

* El manifiesto `init.pp` usa un fact para definir la ruta del archivo dependiendo del kernel:

```puppet
if $facts[kernel] == "windows" {
  $info_path = "C:\\Windows\\Temp\\Machine_Info.txt"
} else {
  $info_path = "/tmp/machine_info.txt"
}

file { 'machine_info':
  path    => $info_path,
  content => template('machine_info/info.erb'),
}
```

* Se agregó al template ERB:

```erb
Machine Information
-
Disks: <%= @disks %>
Memory: <%= @memory %>
Processors: <%= @processors %>
Network Interfaces: <%= @interfaces %>
```

### 3. **Creación del módulo `reboot`**

Ruta: `/etc/puppet/code/environments/production/modules/reboot/manifests/init.pp`

* Reinicia el sistema si el `uptime_days` es mayor a 30. Define el comando según el sistema:

```puppet
class reboot {
  if $facts[kernel] == "windows" {
    $cmd = "shutdown /r"
  } elsif $facts[kernel] == "Darwin" {
    $cmd = "shutdown -r now"
  } else {
    $cmd = "reboot"
  }

  if $facts[uptime_days] > 30 {
    exec { 'reboot':
      command => $cmd,
    }
  }
}
```

### 4. **Inclusión de clases en el archivo `site.pp`**

Ruta: `/etc/puppet/code/environments/production/manifests/site.pp`

```puppet
node default {
  class { 'packages': }
  class { 'machine_info': }
  class { 'reboot': }
}
```



## 📊 Validación y ejecución

Se usó el comando:

```bash
sudo puppet agent -v --test
```

Y se validó:

```bash
apt policy golang
cat /tmp/machine_info.txt
```



## 🎉 Conclusión

Se completó exitosamente el despliegue de Puppet:

* Se personalizó la configuración según el SO.
* Se implementó una recolección condicional de información.
* Se automatizó un reinicio controlado.
* Se aprendieron buenas prácticas como uso de facts, plantillas ERB, y entornos aislados para producción y prueba.

> 🔹 *"Automatizar es liberar tiempo. Mantenerlo ordenado es lo que hace posible escalarlo"*
