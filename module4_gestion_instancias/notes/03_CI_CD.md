# 📝 Clase: CI/CD y Gestión del Cambio en la Nube

**Módulo:** 4 – Introducción a la Computación en la Nube
**Fecha:** 2025‑06‑20
**Duración:** \~10 min
**Fuente:** Curso “Configuration Management and the Cloud” – Google IT Automation



## 💡 Conceptos clave

### 🔁 ¿Por qué gestionar el cambio?

* En la nube, **el cambio es inevitable**: nuevas funciones, correcciones, escalabilidad...
* No cambiar puede parecer seguro, pero **bloquea la innovación**.
* La solución no es evitar el cambio, sino **gestionarlo con seguridad y control**.


### 🧪 Pruebas automatizadas

* Son la primera defensa para evitar errores:

  * **Pruebas unitarias**: verifican componentes individuales.
  * **Pruebas de integración**: validan cómo interactúan los componentes.



### ⚙️ Integración Continua (CI)

* Herramientas que **compilan y prueban automáticamente** el código con cada cambio.
* Ayudan a detectar errores **antes** de fusionar cambios en la rama principal.
* Ejemplos: **Jenkins**, **Travis CI**, **GitHub Actions**, soluciones nativas de proveedores cloud.



### 🚀 Despliegue Continuo (CD)

* Automatiza la implementación de cambios validados.
* Reglas típicas:

  * Solo desplegar si **todas las pruebas pasan**.
  * Desplegar primero en entornos intermedios.

> CI/CD permite **cambios rápidos, seguros y trazables**.



### 🏗 Entornos de despliegue

| Entorno      | Finalidad                                                                    |
| ------------ | ---------------------------------------------------------------------------- |
| **dev**      | Desarrollo y pruebas iniciales.                                              |
| **pre-prod** | Validación más estable, previa a producción.                                 |
| **prod**     | Entorno real, con usuarios reales. Debe protegerse y replicarse con cuidado. |

📌 Todos deben ser **consistentes** entre sí para que las pruebas sean válidas.



### 🧪 Pruebas A/B

* Método para probar **dos versiones distintas** (A y B) en producción.
* Requiere un **balanceador de carga** que redirija tráfico en porcentajes controlados.
* Ejemplo:

  * 99 % de usuarios → versión A (actual)
  * 1 % de usuarios → versión B (experimental)

> Aumenta progresivamente el porcentaje de tráfico hacia B si funciona correctamente.

🛑 **Es esencial tener monitoreo** activo para detectar rápidamente fallos o mejoras.



### 🔍 ¿Y si algo falla?

* Realizar una **autopsia técnica (post-mortem)**:

  * ¿Cómo lo detectaste?
  * ¿Qué falló en las pruebas o monitoreo?
  * ¿Qué mejoras puedes implementar (más pruebas, nuevas reglas, alertas)?

> El objetivo no es evitar el error, sino **aprender para no repetirlo**.



## 🧠 Notas para repaso

* **Cambiar en la nube es inevitable**, pero debe hacerse de forma controlada.
* **CI/CD** automatiza pruebas y despliegues, minimizando riesgos humanos.
* **Separar entornos** permite validar sin afectar usuarios reales.
* Las **pruebas A/B** permiten experimentar con funciones nuevas en producción.
* Una **post-mortem técnica** es parte fundamental de la mejora continua.
* Confianza ≠ ausencia de errores, sino saber **detectar, aprender y corregir rápido**.

