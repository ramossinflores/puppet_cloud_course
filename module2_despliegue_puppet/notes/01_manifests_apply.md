# 📝 Clase: Ejecución local de Puppet con `puppet apply` y recurso `package`

**Módulo:** 2 – Despliegue de Puppet
**Fecha:** 2025‑06‑18
**Duración:** \~5 min
**Fuente:** Curso “Configuration Management and the Cloud” – Google IT Automation

## 💡 Conceptos clave

* **Modo local:** Puppet puede usarse sin servidor, aplicando configuraciones directamente desde la línea de comandos con `puppet apply`.
* **Manifiesto (`.pp`)**: archivo donde se escriben las reglas que Puppet aplicará.
* **Recurso `package`:** se usa para gestionar la instalación de paquetes de software.
* **Catálogo:** lista de reglas que Puppet aplicará tras evaluar condiciones y hechos del sistema.
* **Idempotencia:** Puppet no repite acciones si el sistema ya está en el estado deseado.



## ⚙️ Pasos prácticos

### 1. 🧩 Instalar Puppet (modo local en Ubuntu)

```bash
sudo apt install puppet-master
```

> Aunque instala `puppet-master`, **no necesitas un servidor** en este modo. Todo se ejecuta localmente.



### 2. 📄 Crear el manifiesto `tools.pp`

```puppet
package { 'htop':
  ensure => 'present',
}
```

Este manifiesto le dice a Puppet:
👉 “Asegúrate de que el paquete `htop` esté instalado”.



### 3. ▶️ Aplicar el manifiesto con `puppet apply`

```bash
sudo puppet apply -v tools.pp
```

* `-v` muestra salida detallada.
* Puppet:

  1. Carga los hechos del sistema
  2. Compila el catálogo
  3. Aplica las reglas
  4. Informa los cambios realizados

### 4. ❓ ¿Qué es un catálogo?

> Es el conjunto de acciones que Puppet **decide ejecutar** en una máquina, basándose en las reglas del manifiesto y los hechos recogidos.

En el ejemplo de esta clase, como no hay condiciones ni variables, el catálogo es idéntico al manifiesto.



### 5. ✅ Probar que el paquete fue instalado

```bash
htop
```



### 6. 🔁 Reaplicar el manifiesto

```bash
sudo puppet apply -v tools.pp
```

> Puppet detecta que el estado **ya está cumplido**, así que no hace nada.
> Eso es la **idempotencia**: Puppet solo actúa si hay algo que cambiar.



## 🧠 Notas para mi cerebro

* Puppet **no ejecuta pasos como Bash**. Declara cómo debe estar el sistema.
* Es un lenguaje **declarativo**, no imperativo.
* Un recurso Puppet es como una **promesa de estado** (“esto debe estar así”).
* Se puede agrupar **muchos recursos en un solo manifiesto**.
* Puppet puede trabajar sin servidor para pruebas o entornos simples.
