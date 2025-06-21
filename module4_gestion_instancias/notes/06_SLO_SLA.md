
# 📝 Clase: SLO, SLA y Presupuestos de Error

**Módulo:** 4 – Gestión de la fiabilidad en la nube
**Duración:** \~7–10 min
**Fuente:** Curso “Configuration Management and the Cloud” – Google IT Automation

## 📌 Conceptos clave

| Término                           | Definición                                                                                                             |
| --------------------------------- | ---------------------------------------------------------------------------------------------------------------------- |
| **SLO (Service Level Objective)** | Objetivo técnico interno que define qué tan bien debe funcionar un servicio. Ej: "99% de disponibilidad"               |
| **SLA (Service Level Agreement)** | Acuerdo formal entre proveedor y cliente. Su incumplimiento puede tener consecuencias legales o económicas.            |
| **Presupuesto de error**          | Cantidad de tiempo (o fallos) que se puede tolerar sin incumplir el SLO. Se usa para gestionar riesgos y lanzamientos. |

## 💡 ¿Por qué no todo debe tener "cinco nueves"?

| Nivel             | Disponibilidad (%)  | Tiempo máximo de inactividad por año |
| ----------------- | ------------------- | ------------------------------------ |
| Dos 9 (99%)       | 3 días, 15 horas    |                                      |
| Tres 9 (99.9%)    | 8 horas, 45 minutos |                                      |
| Cinco 9 (99.999%) | 5 minutos           |                                      |

🎯 **Cinco nueves = muy costoso + alto equipo técnico**
✅ **Dos o tres nueves** suelen ser suficientes para muchos servicios no críticos.

## 🎯 Ejemplo práctico de SLO

> "90% de las peticiones deben responder en menos de 5 segundos."

### Alertas recomendadas

* 📧 **No paginación**: si <95% responde rápido → crear ticket o email.
* 📱 **Paginación**: si <90% → alerta urgente.

## 🧮 Cómo calcular la disponibilidad

**Fórmula:**

$$
\text{Disponibilidad} = \left(1 - \frac{\text{Tiempo de inactividad}}{\text{Tiempo total}}\right) \times 100
$$

Ejemplo con 99%:

* 1% de inactividad permitido.
* En un año:

  $$
  365 \times 24 \text{h} \times 1\% = 3.65 \text{ días de inactividad posibles}
  $$

## 📉 ¿Por qué fallan los SLO?

> Casi siempre: **algo cambió** en el sistema.

⚠️ Cambios recientes (código, configuración, despliegues) suelen ser la causa de desvíos del SLO.

## 🔄 Presupuesto de error

### ¿Qué es?

Cantidad de "fallos permitidos" según el SLO.

### ¿Para qué sirve?

* Controlar cuánto margen tienes antes de incumplir.
* **Ejemplo**: con 99.9% de disponibilidad mensual → se permiten hasta **43 minutos de caída** al mes.
* Si te acercas al límite:

  * ⛔ **Congelas nuevos cambios.**
  * 🛠️ Te enfocas en corregir incidentes.

## ✔️ Buenas prácticas para SLO/SLA

1. **Empieza por lo básico**: define objetivos alcanzables y medibles.
2. **Haz seguimiento del comportamiento** del sistema antes de establecer SLO agresivos.
3. Usa las métricas para:

   * Crear alertas apropiadas.
   * Tomar decisiones sobre despliegues.
   * Priorizar mantenimiento frente a desarrollo.
4. Si usas proveedores de nube:

   * 🧾 Consulta los SLA que ofrecen.
   * ⚖️ Evalúa si cumplen tus necesidades de fiabilidad.

## 🧠 Resumen final

* No todos los sistemas requieren el mismo nivel de disponibilidad.
* Establecer SLO realistas mejora la planificación y comunicación.
* El SLA es un contrato, el SLO es una meta técnica.
* El presupuesto de error te ayuda a equilibrar estabilidad vs innovación.
* Las alertas deben estar alineadas con los SLO para ser útiles y procesables.
