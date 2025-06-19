# 📝 Clase: DSL de Puppet, variables y hechos (`facts`)

**Módulo:** 2 – Puppet DSL y decisiones condicionales
**Fecha:** 2025-06-18
**Tema:** Sintaxis del lenguaje de Puppet y decisiones dinámicas según el sistema


## 💡 Conceptos clave

### 🧠 ¿Qué es un DSL?

* Un **DSL** (lenguaje específico de dominio o domain specific leanguage) es un lenguaje de programación **limitado a un contexto concreto**, en este caso: **automatizar configuraciones de sistemas**.
* A diferencia de Python o Java, **Puppet DSL** no sirve para todo, sino solo para **definir el estado deseado** de un sistema.

📌 Ventaja: mucho **más fácil de aprender** que un lenguaje de propósito general.



### 🧩 Puppet DSL = recursos + variables + condicionales + funciones

Puppet DSL te permite:

* Declarar recursos (`package`, `file`, `service`, etc.).
* Usar **variables**, que empiezan con `$`.
* Aplicar **condicionales** (`if`, `else`) para tomar decisiones.
* Usar **funciones** para procesar valores.


### 📦 ¿Qué son los `facts`?

* Son **valores recopilados automáticamente** sobre cada sistema gestionado: sistema operativo, IP, RAM, si es VM, hostname, etc.
* Puppet los obtiene a través del **comando `facter`**.
* Se accede a ellos con: `$facts['nombre_del_fact']`

Ejemplo:

```puppet
if $facts['is_virtual'] {
  notice("Esto es una máquina virtual")
}
```

### 💻 Ejemplo de la clase

```puppet
if $facts['is_virtual'] {
  package { 'smartmontools':
    ensure => purged,
  }
} else {
  package { 'smartmontools':
    ensure => present,
  }
}
```

🧵 Detalle:

* `if $facts['is_virtual']` → Evalúa si la máquina es **virtual**
* Si **es virtual**, Puppet **elimina** el paquete `smartmontools`, porque no tiene sentido monitorizar discos SMART en una VM
* Si **NO es virtual** (`else`), lo **instala** para poder monitorizar discos físicos.


### 🧪 Sintaxis importante

* Variables comienzan con `$`
* `$facts` es un **hash** (diccionario en Python)
* Accedes así: `$facts['clave']`
* Las condiciones usan `{ ... }` para cada bloque.
* Los recursos tienen este formato:

```puppet
package { 'nombre':
  ensure => 'valor',
}
```

Cada atributo termina con una **coma** 👀



## 📌 Comandos útiles

```bash
facter is_virtual
facter os
puppet apply recurso.pp
```


