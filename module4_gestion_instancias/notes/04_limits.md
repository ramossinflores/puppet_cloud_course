# 📝 Clase: Retos de Desplegar Software en la Nube

**Módulo:** 4 – Introducción a la Computación en la Nube
**Fecha:** 2025‑06‑20
**Duración:** \~8–10 min
**Fuente:** Curso “Configuration Management and the Cloud” – Google IT Automation

## 💡 Conceptos clave

### ⚠️ La nube no es infalible

Aunque la nube es altamente disponible, **no está exenta de errores o límites**. Como desarrolladora, debes considerar:

* **Fallas de instancias individuales**
* **Límites de uso o cuotas**
* **Dependencias externas (servicios gestionados)**
* **Escalado descontrolado**
* **Costes ocultos o imprevisibles**

## 🔁 Tolerancia a errores

> Un servicio bien diseñado en la nube debe seguir funcionando **aunque falle una instancia individual**

### 🔧 Buenas prácticas

* **Uso de múltiples instancias** en grupo (cluster)
* **Escalado automático** con límites
* **Persistencia externa (bases de datos, almacenamiento de objetos)** para no depender del estado local

## 📊 Límites (quotas) en la nube

Los proveedores imponen **límites de uso** para proteger su infraestructura y evitar abusos:

| Tipo de límite              | Ejemplo                                   | Solución                          |
| --------------------------- | ----------------------------------------- | --------------------------------- |
| **Límites de operación**    | 1000 escrituras/segundo en el mismo blob  | Agrupar en bloques o ralentizar   |
| **Límites de llamadas API** | 1 llamada/segundo a una API costosa       | Reducir frecuencia, usar caché    |
| **Límites de recursos**     | 20 instancias máximas en una región       | Solicitar aumento o reestructurar |
| **Límites presupuestarios** | Escalado automático que consume demasiado | Establecer umbrales y alertas     |

🔔 **Configura alertas** para no quedarte sin recursos de forma inesperada.

## 🧮 Costes y presupuestos

* En muchos servicios, **pagarás según uso**:

  * Número de llamadas a API
  * Tiempo de computación
  * Almacenamiento ocupado

💰 Si tu servicio se vuelve viral, puedes **agotar presupuesto o cuota** si no lo has limitado.

🎯 **Recomendación:** Establece **límites de escalado**, usa **presupuestos** y **monitorea el uso**.

## 🔗 Dependencias gestionadas (PaaS/SaaS)

> Cuando usas servicios gestionados (base de datos, CDN, CI/CD...), **delegas mantenimiento y actualizaciones** al proveedor

### Pros

✅ No necesitas mantener infraestructura
✅ Parcheos y seguridad gestionados automáticamente

### Contras

❌ No puedes controlar cuándo se actualizan
❌ Puede haber incompatibilidades o cambios inesperados
❌ Algunas versiones pueden tardar en desplegarse o desaparecer

🧪 Puedes usar **versiones beta en entornos de prueba** para anticiparte a cambios de producción.

## 📌 Ideas clave para llevarte

* **Diseña con tolerancia a fallos**: tu servicio debe resistir fallos de instancias individuales.
* **Conoce las cuotas**: tanto técnicas como financieras. Úsalas a tu favor.
* **Automatiza, pero con control**: el escalado automático sin límites puede causar gastos innecesarios.
* **Monitoriza todo**: estado de instancias, uso de recursos, llamadas a API, costes.
* **Aprovecha servicios gestionados**, pero con entornos de prueba que te permitan reaccionar antes de que el cambio llegue a producción.
