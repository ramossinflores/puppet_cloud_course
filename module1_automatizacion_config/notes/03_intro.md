
## 📝 Clase: Declaración, Idempotencia y Ejecución en Puppet

**Módulo:** 2 – Comportamiento del sistema Puppet
**Fecha:** 2025-06-18
**Tema:** Declaración de estado deseado, automatización segura e idempotencia

## 💡 Conceptos clave

### 🔎 1. Puppet es **declarativo**

* No le dices *cómo* hacer las cosas, sino *cómo debe quedar* el sistema.
* Ejemplo:

  ```puppet
  package { 'ntp':
    ensure => present,
  }
  ```

  Puppet no necesita que le digas `apt install ntp` o `yum install ntp`. Solo declaras el estado deseado, y Puppet lo resuelve.

### ⚙️ 2. Procedural vs Declarativo

| Enfoque           | Ejemplo                    | Descripción                                                          |
| ----------------- | -------------------------- | -------------------------------------------------------------------- |
| **Procedimental** | Bash, Python, C            | Tú defines paso a paso cómo llegar al resultado                      |
| **Declarativo**   | Puppet, Ansible, Terraform | Tú defines el resultado deseado; la herramienta decide cómo lograrlo |

> 🧠 *Esto requiere un cambio de mentalidad, especialmente si vienes de bash o Python.*


### 🔁 3. Idempotencia

> Una acción **idempotente** se puede ejecutar muchas veces sin alterar el resultado más allá de la primera vez.

* Puppet compara el **estado actual** con el **estado deseado**.
* Solo actúa si hay diferencia.
* Si el recurso ya está como debe estar → **no hace nada**.

💡 Ejemplo:

```puppet
file { '/etc/motd':
  content => "Bienvenido a este servidor",
  mode    => '0644',
}
```

Este recurso **no se ejecuta una y otra vez** innecesariamente. Solo aplica cambios si:

* El archivo no existe
* El contenido es diferente
* Los permisos no son los correctos


### 🚨 4. Cuidado con `exec`

```puppet
exec { 'mover archivo':
  command => 'mv example.txt ~/Escritorio',
}
```

Esto **NO es idempotente**:

* La primera vez mueve el archivo
* La segunda vez falla porque el archivo ya no está

### 🛡 Solución con `onlyif` (control de ejecución)

```puppet
exec { 'mover archivo':
  command => 'mv example.txt ~/Escritorio',
  onlyif  => 'test -f example.txt',
}
```

✅ Ahora es idempotente: **solo se ejecuta si el archivo existe**


### 🧪 5. Prueba y reparación

Puppet trabaja con un modelo de:

1. **Probar** si el recurso necesita acción
2. **Reparar** solo si es necesario

> Evita repetir tareas innecesarias y acelera la ejecución.


### 🔄 6. Puppet es **sin estado**

* Cada ejecución es **independiente**
* No guarda información entre ejecuciones
* Cada vez:

  * Recoge los **facts** del sistema
  * Evalúa las reglas
  * Aplica solo lo necesario

💡 Esto permite que puedas ejecutar Puppet muchas veces sin romper el sistema, incluso tras errores anteriores

## 📌 Referencias

* [Idempotence in configuration management](https://en.wikipedia.org/wiki/Idempotence)
* [Documentación oficial de Puppet sobre recursos `exec`](https://puppet.com/docs/puppet/latest/types/exec.html)
* [Declarative vs Procedural](https://www.terraform.io/language/expressions/declarative-vs-imperative)
