
# 📝 Clase: Capacidad y escalado en la nube

**Módulo:** 3 – Introducción a la Computación en la Nube
**Fecha:** 2025‑06‑20
**Duración:** \~7 min
**Fuente:** Curso “Configuration Management and the Cloud” – Google IT Automation

## 💡 Conceptos clave

### 📏 ¿Qué es capacidad?

* La **capacidad** es cuánto puede manejar tu sistema (almacenamiento, tráfico, procesamiento).
* Se puede medir como:

  * Espacio en disco
  * QPS (queries per second)
  * Ancho de banda, memoria usada, etc.

### 📈 ¿Qué es escalar?

* **Escalar** = aumentar o disminuir la capacidad del sistema.
* Tipos de escalado:

| Tipo           | Descripción                      | Ejemplo                  |
| -------------- | -------------------------------- | ------------------------ |
| **Horizontal** | Añadir más máquinas              | De 1 a 10 servidores web |
| **Vertical**   | Aumentar recursos en una máquina | Agregar más RAM o CPU    |

### ⚙️ Escalado manual vs automático

| Tipo           | ¿Quién decide cuándo escalar?       | Ventajas                                 | Riesgos                                            |
| -------------- | ----------------------------------- | ---------------------------------------- | -------------------------------------------------- |
| **Manual**     | Tú decides                          | Simple, apropiado para entornos pequeños | Puede no reaccionar a tiempo                       |
| **Automático** | Lo decide el sistema según métricas | Rápido y eficiente                       | Riesgo de costos altos si no se configuran límites |

> Ejemplo divertido: si se viraliza un video de gatos, el sistema escalará automáticamente. Pero si no hay cuotas, podrías recibir una factura enorme 🐈

### 🔄 Cómo se escala en la nube

* No hace falta agregar servidores físicos: se hace desde la interfaz web o scripts.
* El proveedor despliega los recursos extra por ti.
* Puedes escalar:

  * **Por demanda** (respuesta a carga actual)
  * **Planificado** (cuando sabes que aumentará el tráfico)

## 🧠 Notas para repaso

* **Capacidad** = qué tanto puede manejar el sistema (disco, CPU, QPS, etc.).
* **Escalar horizontalmente** = más máquinas; **verticalmente** = máquinas más potentes.
* El **escalado automático** usa métricas para adaptarse en tiempo real.
* En la nube, **escalar es fácil y rápido**, comparado con entornos físicos.
