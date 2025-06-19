# 🧪 Lab 01 – Depuración de la instalación de Puppet

**Fecha de realización:** 2025-06-19
**Curso:** Google IT Automation with Python – Módulo 1
**Tema:** Automatización con herramientas de configuración (Puppet)
**Duración:** 90 minutos (Qwiklabs)



## 🎯 Objetivo general

El objetivo de este laboratorio es **diagnosticar y corregir un error** en la configuración de Puppet que está provocando que la variable de entorno `$PATH` se sobrescriba incorrectamente, impidiendo la ejecución normal de comandos en Linux.

También sirve como una introducción práctica a:

* Cómo funcionan las variables de entorno
* Cómo manipularlas correctamente
* Cómo Puppet automatiza tareas como la creación de archivos de configuración del sistema



## 🔍 Introducción teórica

### ¿Qué es `$PATH`?

Es una **variable de entorno** que contiene una lista de carpetas donde el sistema **busca los ejecutables** cuando escribes comandos como `ls`, `nano`, `python`, etc.

Ejemplo típico de `$PATH`:

```
/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
```

Cada carpeta se separa por `:`. Cuando escribes `ls`, el sistema busca ese comando dentro de cada carpeta del `$PATH`, en orden.


### ¿Qué hace Puppet en este escenario?

El sistema Puppet tiene una clase llamada `profile` que estaba creando un archivo en `/etc/profile.d/` con el siguiente contenido:

```bash
PATH=/java/bin
```

Esto **sobrescribe todo el contenido del `$PATH`**, eliminando rutas esenciales del sistema.



## ❌ Problema detectado

Cuando ejecutamos:

```bash
echo $PATH
```

El resultado era:

```
/java/bin:/snap/bin
```

⚠️ Esto es un gran problema porque **las rutas estándar del sistema han desaparecido**, lo que impide que funcionen comandos básicos como `ls`, `cat`, `sudo`, etc.



## 🧪 Diagnóstico manual

Para poder continuar con el lab, restauramos temporalmente el PATH original:

```bash
export PATH=/bin:/usr/bin
```

Esto **restablece el entorno mínimo funcional** para poder trabajar.



## 🧭 Investigación del manifiesto en Puppet

Ruta del manifiesto:

```bash
/etc/puppet/code/environments/production/modules/profile/manifests/init.pp
```

Contenido problemático encontrado:

```puppet
class profile {
  file { '/etc/profile.d/append-path.sh':
    owner   => 'root',
    group   => 'root',
    mode    => '0646',
    content => "PATH=/java/bin\n",
  }
}
```


## 🧠 Análisis detallado de este bloque Puppet

| Atributo  | Explicación                                                                 |
| --------- | --------------------------------------------------------------------------- |
| `file`    | Declara un recurso tipo archivo                                             |
| `owner`   | Propietario: `root` (correcto)                                              |
| `group`   | Grupo: `root` (correcto)                                                    |
| `mode`    | Permisos: `0646` es incorrecto (da escritura a otros usuarios)              |
| `content` | Aquí es donde está el error más crítico: se reemplaza el PATH completamente |



## 🛠️ Corrección aplicada

### ✔️ Contenido corregido (content)

```puppet
content => "export PATH=\\\$PATH:/java/bin\n",
```

📌 Aquí usamos:

* `export PATH=...` para asegurarnos de que la variable se actualice correctamente en el entorno del usuario
* `\\\$PATH` para **escapar el `$`**, ya que Puppet interpreta `$` como variable suya si no se escapa

### ✔️ Permisos corregidos (mode)

```puppet
mode => '0644',
```

* Esto significa:

  * Root: lectura y escritura
  * Grupo y otros: solo lectura
* Es el permiso correcto para archivos de configuración del sistema


## 💻 Ejecución del agente Puppet

Después de corregir el archivo `init.pp`, aplicamos los cambios manualmente:

```bash
sudo puppet agent -v --test
```

Esto fuerza a Puppet a re-evaluar las configuraciones y aplicar los cambios detectados.



## ✅ Verificación final

Comprobamos que el `$PATH` está bien construido:

```bash
echo $PATH
```

Resultado esperado (y obtenido):

```
/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/snap/bin:/java/bin
```

📌 `/java/bin` está **al final**, sin haber eliminado las rutas esenciales del sistema. Todo funciona correctamente.

## 🧠 Conceptos fundamentales aprendidos

| Concepto               | Explicación                                                                                             |
| ---------------------- | ------------------------------------------------------------------------------------------------------- |
| `$PATH`                | Lista de rutas donde Linux busca comandos                                                               |
| Puppet `file` resource | Sirve para crear archivos desde Puppet y definir contenido, permisos, dueño, etc.                       |
| Idempotencia           | Puppet ejecuta solo lo necesario; si algo ya está bien, no lo repite                                    |
| Variables en Puppet    | Se escapan con `\\$` si deben escribirse literalmente en un archivo                                     |
| `/etc/profile.d/`      | Carpeta especial donde se colocan scripts de configuración de entorno que se cargan al inicio de sesión |
| Modo `0644`            | Seguridad mínima recomendada para archivos de configuración del sistema                                 |
