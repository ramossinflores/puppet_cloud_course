
# 📡 Supervisión y Alertas con Cloud Monitoring (Stackdriver)

**Módulo:** 4 Supervisión de recursos en la nube
**Duración:** \~8 min
**Fuente:** Curso “Configuration Management and the Cloud” – Google IT Automation

## 📌 ¿Qué es Cloud Monitoring?

Google Cloud Monitoring (antes Stackdriver) permite:

* Recoger métricas en tiempo real.
* Crear dashboards personalizados.
* Configurar alertas sobre condiciones críticas.
* Recibir notificaciones automáticas por canales definidos (correo, Slack, Pub/Sub, etc.).

## 🧭 Flujo general de trabajo

1. **Activar Cloud Monitoring en el proyecto.**
2. **Esperar unos minutos** hasta que se recojan las primeras métricas.
3. Personalizar paneles de control con gráficas útiles.
4. Crear políticas de alerta con:

   * Condición (ej. “CPU > 90% por 1 minuto”).
   * Canal de notificación (correo electrónico, Slack, webhook, etc.).
   * Documentación para facilitar la respuesta.

## 📊 Métricas predeterminadas por instancia

Para cada VM (instancia de GCE), Stackdriver recoge por defecto:

* **CPU usage (% de uso)**
* **Disk I/O (entrada/salida de disco)**
* **Network traffic (tráfico de red)**

Se pueden añadir:

* Métricas personalizadas.
* Logs de Stackdriver Logging (Cloud Logging).

## 🛠️ Ejemplo práctico: crear una alerta por uso de CPU

### Pasos:

| Paso | Acción                                                            |
| ---- | ----------------------------------------------------------------- |
| 1    | Entrar a "Monitoring" → "Alertas"                                 |
| 2    | Crear nueva política de alerta                                    |
| 3    | Elegir el recurso: **GCE VM Instance**                            |
| 4    | Seleccionar métrica: **CPU utilization**                          |
| 5    | Filtro: opcional por zona, nombre, etc.                           |
| 6    | Agregador: puede ser "mean", "sum", etc. (según el caso)          |
| 7    | Condición: **Si cualquier instancia > 90% durante 1 min**         |
| 8    | Canal de notificación: **Correo electrónico**                     |
| 9    | Añadir documentación útil: ej. “Ejecutar `top` y buscar procesos” |
| 10   | Asignar nombre a la alerta (ej. `HighCPU`) y guardar              |

## ⚠️ Consideraciones sobre condiciones de alerta

* El **intervalo de tiempo (ventana)** es clave:

  * Muy corto → muchas falsas alarmas.
  * Muy largo → alertas tardías.
* Puedes ajustar condiciones según:

  * Servicio (crítico o no).
  * Variabilidad natural esperada.
  * Repetición de alertas innecesarias.

## 🔥 Simulación de alerta

Se crea un proceso con alto uso de CPU:

```bash
while true; do :; done
```

✔️ Se verifica con `top` que se utiliza el 100% de la CPU.

🕑 Tras 1 minuto, se genera una alerta real en la consola de Monitoring:

* Incidente se abre automáticamente.
* Se puede inspeccionar la métrica, el umbral y los valores actuales.
* Se muestra el mensaje de ayuda (documentación de alerta).
* Puedes añadir anotaciones sobre acciones realizadas.

🧯 Se detiene el proceso con:

```bash
fg
CTRL+C
```

📉 La alerta se resuelve sola al cesar la condición.

## ✅ Buenas prácticas

* **Separar alertas para entornos distintos** (dev, staging, prod).
* **Agrupar métricas** si se desea monitoreo de todo el servicio (suma de errores, etc.).
* **Documentar cada alerta** para facilitar la intervención (scripts, comandos, enlaces).
* **Usar otros canales de alerta** (SMS, webhooks, Opsgenie, PagerDuty) conforme el sistema crece.
* **Corregir picos falsos** ajustando ventanas de tiempo.

