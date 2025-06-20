# 📝 Clase: Balanceo de carga y escalabilidad en aplicaciones en la nube

**Módulo:** 3 – Introducción a la Computación en la Nube
**Fecha:** 2025‑06‑20
**Duración:** \~8 min
**Fuente:** Curso “Configuration Management and the Cloud” – Google IT Automation

## 💡 Conceptos clave

### 🚀 Escalado eficiente en la nube

* Las implementaciones cloud están diseñadas para **escalar fácilmente** (más capacidad cuando se necesita, menos cuando no).
* Esto se logra **añadiendo o quitando nodos**: VMs, contenedores o servicios.

### ⚖️ Balanceadores de carga

* Reparten las solicitudes entrantes entre varios nodos para:

  * **Optimizar el rendimiento**
  * **Evitar sobrecarga**
  * **Mejorar la disponibilidad**

#### 🔁 Estrategias de distribución

* **Round Robin**: turnos equitativos entre nodos.
* **Por origen**: misma IP → mismo nodo (persistencia).
* **Por proximidad**: el nodo más cercano geográficamente.
* **Por carga**: el nodo con menor uso actual.

> Los balanceadores de carga pueden trabajar en **capa 4 (TCP/UDP)** o **capa 7 (HTTP/HTTPS)**.


### 🔄 Escalado automático

* Escalar automáticamente según demanda = **Autoescalado**.
* Ventajas:

  * Aumenta capacidad ante alta carga.
  * Reduce instancias si baja la demanda.
  * Solo se paga por lo que se usa.


### 💾 Discos efímeros y almacenamiento persistente

* Cuando una VM se detiene por autoescalado, su **disco local se pierde**
* Para **guardar datos entre reinicios**, se debe usar **almacenamiento persistente** (volúmenes externos, buckets, bases de datos cloud, etc.)

### 🗄️ Infraestructura típica de una app web escalable

1. **Usuarios acceden vía Internet**.
2. Llegan a un **balanceador de carga**, que distribuye entre:

   * **Servidores de caché web** (como Varnish, Nginx, Cloudflare).
   * Si no está en caché → redirige al backend.
3. El backend accede a la **base de datos**:

   * Servidores de DB tras otro balanceador.
   * Puede incluir una **capa de caché de DB** (Memcached, Redis).

## 🧠 Notas para repaso

* Las aplicaciones escalables usan **varios nodos** con un balanceador de carga para repartir el tráfico.
* El **autoescalado** permite responder a cambios de carga y ahorrar costes.
* Los **discos locales son efímeros**. Usa almacenamiento persistente para datos importantes.
* El **caching** (web y de DB) mejora el rendimiento general.
* Es recomendable **preparar la arquitectura antes de escalar** para aprovechar los servicios cloud de forma óptima.
