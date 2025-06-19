
# 📝 Clase: Pruebas de cambios en Puppet (validación, noop, entornos de prueba y RSpec)

**Módulo:** 3 – Validación de configuraciones en Puppet
**Fecha:** 2025‑06‑18
**Duración:** \~6 min
**Fuente:** Curso “Configuration Management and the Cloud” – Google IT Automation

## 💡 Conceptos clave

### 🛠️ Cambios en manifiestos Puppet

Cuando se modifica un manifiesto, Puppet:

* **Detecta el nuevo estado deseado**
* Aplica los cambios necesarios en los nodos

Esto permite realizar **cambios masivos de forma centralizada**, pero también implica riesgo si los cambios no se prueban correctamente.



## ✅ Estrategias de prueba recomendadas

### 1. Validación de sintaxis

```bash
puppet parser validate archivo.pp
```

* Comprueba que la sintaxis del manifiesto `.pp` sea correcta.
* **No ejecuta el manifiesto**, solo valida la forma.



### 2. Ejecución simulada con `--noop`

```bash
puppet apply archivo.pp --noop
```

* Simula la ejecución de Puppet.
* Muestra **qué acciones tomaría**, pero no realiza cambios.
* Útil para revisar el impacto de los cambios antes de aplicarlos.



### 3. Uso de máquinas de prueba

* Se pueden mantener **nodos separados exclusivamente para pruebas**.
* Permite aplicar el catálogo completo de Puppet y observar el comportamiento.
* Limitación: requiere **verificación manual posterior**, puede dejar pasar errores sutiles.



## 🧪 Automatización de pruebas: **RSpec-Puppet**

RSpec es un framework que permite **escribir pruebas unitarias** sobre los manifiestos.

### 📄 ¿Qué se prueba?

* El resultado del catálogo generado.
* Que ciertos recursos estén presentes, ausentes o configurados con valores específicos.

### 📋 Ejemplo

```ruby
it { is_expected.to contain_package('gksu').with_ensure('latest') }
```

En este caso, la prueba comprueba que:

* Si el nodo **no es virtual**, Puppet debe **instalar el paquete `gksu`** y asegurarse de que esté en su versión más reciente.

> Se puede simular el valor de **facts** (como `virtual => false`) y verificar el resultado del catálogo.



### 🧩 Ventajas de RSpec-Puppet

* Permite ejecutar pruebas **automáticamente** tras cada cambio.
* Detecta errores de lógica y regresiones.
* No requiere aplicar el manifiesto sobre una máquina real.
* Es útil cuando el manifiesto usa **muchas variables, condicionales o datos externos**.



## 🧰 Pruebas funcionales automatizadas (entorno completo)

* Se pueden automatizar pruebas de extremo a extremo:

  1. Aplicar el manifiesto en una máquina de prueba
  2. Ejecutar scripts que verifiquen el resultado:

     * ¿El sitio web se cargó?
     * ¿El firewall bloquea el tráfico?
     * ¿El servicio está activo?

> Este enfoque combina **Puppet + scripts de verificación personalizados**.



## 🧠 Notas para repaso

* **Validar sintaxis** evita errores básicos antes de ejecutar Puppet.
* El parámetro `--noop` es una forma **segura de previsualizar los efectos**.
* Los **tests unitarios con RSpec-Puppet** aseguran que el catálogo contiene lo esperado.
* Se recomienda tener **máquinas de prueba** o entornos controlados antes de aplicar en producción.
* Automatizar las pruebas permite ganar **confianza y velocidad** en la entrega de cambios.
