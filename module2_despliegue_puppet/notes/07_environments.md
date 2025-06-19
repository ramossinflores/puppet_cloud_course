
# 📝 Clase: Implementación segura de cambios en Puppet con entornos y despliegue por lotes

**Módulo:** 3 – Validación de configuraciones en Puppet
**Fecha:** 2025‑06‑18
**Duración:** \~9 min
**Fuente:** Curso “Configuration Management and the Cloud” – Google IT Automation

## 💡 Conceptos clave

### 🏭 ¿Qué es producción?

* **Producción** = Infraestructura real en la que se presta servicio a los usuarios.
* Ejemplos:

  * Servidores web activos
  * Servidores de autenticación corporativa

⚠️ Los errores en producción pueden afectar directamente a usuarios finales.

## 🧪 Entornos en Puppet

* Puppet permite definir **entornos separados**, como:

  * `production`
  * `testing`
  * `development`
  * `feature_X`

Cada entorno tiene su propia ruta de trabajo:

```bash
/etc/puppetlabs/code/environments/NOMBRE_ENTORNO/
```

> Cada entorno puede tener su **propio `site.pp`, manifiestos y módulos**.

## 🔄 Flujo recomendado de cambios

1. **Desarrollo**

   * Cambios se prueban de forma local o en entornos internos.

2. **Entorno de prueba (testing)**

   * Máquinas que simulan la configuración real sin afectar a usuarios.

3. **Validación automática o manual**

   * Se verifican cambios con tests o validaciones funcionales.

4. **Despliegue controlado (por lotes)**

   * Cambios se aplican gradualmente a subconjuntos de nodos.



## 🐤 Uso de nodos canarios

* Nodos **"canarios"**: primeros sistemas en recibir cambios tras las pruebas.
* Permiten detectar errores que **no aparecieron en el entorno de test**.

> Si algo falla, **solo afecta a una parte pequeña de la flota** y se puede revertir a tiempo.



## ✅ Buenas prácticas para despliegue seguro

* Implementar **cambios pequeños y aislados**:

  * Más fáciles de probar
  * Más fáciles de revertir
* Evitar agrupar múltiples cambios en una sola entrega.
* Establecer una **cadencia de publicación** (ej: cada 1–2 semanas).



## 📈 Escalado progresivo

A medida que el proyecto crece:

* Aumentar el número de **tests automatizados**.
* Expandir el **entorno de prueba** para incluir más variaciones de nodos.
* Incorporar procesos de **revisión de cambios**.
* Automatizar despliegues canarios y rollback en caso de fallo.



## 🧠 Notas para repaso

* **Nunca desplegar directamente en producción sin pruebas previas.**
* Usar entornos aislados permite:

  * Probar versiones distintas de módulos
  * Separar reglas por tipo de sistema
* El despliegue debe ser progresivo:

  * Primero en test
  * Luego en canarios
  * Finalmente en toda la flota
* Cambios pequeños son más fáciles de auditar, probar y revertir.


## 📊 Comparación rápida de testing y canarios

| Característica               | Testing                   | Canarios                            |
| ---------------------------- | ------------------------- | ----------------------------------- |
| ¿Son máquinas de producción? | ❌ No                      | ✅ Sí                                |
| ¿Atienden a usuarios reales? | ❌ No                      | ✅ Sí                                |
| ¿Qué se detecta?             | Errores técnicos          | Errores contextuales o inesperados  |
| ¿Nivel de riesgo?            | Bajo                      | Moderado (se controla por cantidad) |
| ¿Cuándo se usa?              | Antes del despliegue real | Justo antes del despliegue completo |
