# 📝 Clase: Recursos en Puppet – `package` y `file`

**Módulo:** 2 – Despliegue de Puppet  
**Fecha:** 2025‑06‑18  
**Duración:** ~5 min  
**Fuente:** Vídeo sobre recursos básicos en Puppet

## 💡 Conceptos clave

# 📝 Clase: Recursos en Puppet – `package` y `file`

**Módulo:** 2 – Despliegue de Puppet  
**Fecha:** 2025‑06‑18  
**Duración:** ~5 min  
**Fuente:** Vídeo sobre recursos básicos en Puppet

---

## 🎯 Objetivos

- Comprender qué es un recurso en Puppet.
- Aprender a declarar recursos tipo `package` y `file`.
- Entender cómo Puppet aplica los cambios usando proveedores.

---

## 💡 Conceptos clave

- **Recurso:** unidad básica de configuración en Puppet, la más pequeña. 

> 🔧 Ejemplo de recursos: un paquete instalado, un archivo con cierto contenido, un servicio que debe estar activo.

- **Declaración de recursos:** se realiza con el tipo (`package`, `file`, etc.), un título (nombre), y atributos definidos entre llaves.

### 📦 Recurso tipo `package`

Sirve para **instalar, actualizar o eliminar un paquete de software**.

```puppet
package { 'apache2':
  ensure => 'present',
}
```

* `"apache2"` es el nombre del paquete (en Ubuntu/Debian).
* `ensure => 'present'` significa: asegúrate de que esté instalado.
* Otros valores posibles: `'absent'` (desinstalar), `'latest'` (actualizar al último).


### 📁 Recurso tipo `file`

Se usa para **gestionar archivos y directorios**. Por ejemplo, crear un archivo, escribir su contenido, o asegurarse de que un directorio exista.

```puppet
file { '/etc/sysctl.d':
  ensure => 'directory',
}
```

Este bloque indica que `/etc/sysctl.d` debe existir y ser un directorio.

- **Proveedor**: componente que Puppet utiliza para aplicar el cambio real en el sistema (como: apt, yum, file).

Puppet usa una **sintaxis muy clara y estructurada**:

```puppet
tipo_de_recurso { 'título':
  atributo1 => valor1,
  atributo2 => valor2,
}
```

### ✏️ Crear y modificar un archivo con contenido

```puppet
file { '/etc/timezone':
  ensure  => 'file',
  content => 'UTC',
  replace => true,
}
```

Aquí le decimos a Puppet:

* Que `/etc/timezone` debe ser un archivo.
* Que su contenido debe ser `"UTC"`.
* Que **reemplace el contenido** si ya existe.


### 🧠 Notas para mi cerebro

*Puppet **no ejecuta acciones como un script bash** que hace cosas paso a paso
*Puppet **declara cómo debería estar el sistema**… y **lo lleva a ese estado**
* Puppet **no es imperativo** (“haz esto, luego esto y aquello”), sino **declarativo** (“quiero que esto esté así o asao”)
* Un recurso es **una promesa de estado**
* Puedes tener **muchos recursos en un solo manifiesto**
