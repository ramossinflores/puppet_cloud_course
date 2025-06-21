
# 📝 Clase: Balanceo de carga y distribución global de servicios

**Módulo:** 4 – Introducción a la Computación en la Nube
**Fecha:** 2025‑06‑20
**Duración:** \~10 min
**Fuente:** Curso “Configuration Management and the Cloud” – Google IT Automation

## 💡 Conceptos clave

### 🔄 Balanceo de carga (Load Balancing)

* El **balanceo de carga** permite distribuir el tráfico de usuarios entre varias instancias de un mismo servicio para:

  * Escalar horizontalmente
  * Mejorar la disponibilidad
  * Garantizar la tolerancia a fallos

### 🧠 Técnicas de balanceo de carga

#### 1. 🌀 **DNS Round Robin**

* DNS devuelve varias IPs en orden rotativo.
* Cada cliente escoge una IP diferente al resolver el nombre de dominio.

📌 Ventajas:

* Simple de configurar.

⚠️ Limitaciones:

* No puedes controlar qué IP elige el cliente.
* Los registros DNS pueden quedar en **caché**, dificultando actualizaciones rápidas.
* No detecta servidores inactivos.

#### 2. 🧭 **Balanceador de carga dedicado (Load Balancer)**

* Un servidor proxy que actúa como punto de entrada.
* Redirige las peticiones a los servidores **back-end** según reglas específicas.

📌 Características:

* **Distribuye tráfico** de forma inteligente.
* Puede **monitorear la salud** de los servidores y excluir los que fallen.
* Permite escalado fácil: solo hay que agregar/quitar instancias del pool.

### 🔒 **Sesiones fijas (Sticky Sessions)**

* El balanceador siempre dirige las solicitudes del mismo cliente al **mismo servidor back-end**.

📌 Útil si:

* El servidor necesita **mantener estado** de sesión (ej. carritos de compra).

⚠️ Problemas potenciales:

* Complica migraciones.
* Puede desbalancear la carga.

### 📈 Escalado dinámico + balanceo

* Al escalar automáticamente, las nuevas instancias pueden añadirse al balanceador de carga sin intervención manual.
* La nube permite que esto sea **dinámico** y reactivo a la carga.

### 🌍 Distribución geográfica del tráfico

#### 🌐 **GeoDNS / GeoIP**

* Configura el DNS para que responda con IPs basadas en la **ubicación del cliente**.
* Redirige usuarios al **balanceador regional más cercano**.

📌 Ejemplo: usuarios en España reciben IPs de un servidor en Europa.

### 🚀 CDN (Redes de Entrega de Contenido)

* Red de servidores distribuidos geográficamente que almacenan contenido **en caché cerca del usuario final**

📌 Funcionamiento:

* Cuando un usuario solicita un recurso (ej. vídeo), se entrega desde el servidor CDN más cercano.
* Los siguientes usuarios lo descargan aún más rápido.

📌 Beneficios:

* Reducción de latencia
* Mejora de la experiencia del usuario
* Ahorro de ancho de banda del servidor original

🧪 Ejemplo:

1. Primer usuario pide `gato.mp4`, se descarga desde el servidor de origen → se guarda en el CDN local.
2. Segundo usuario (de la misma zona) lo recibe directamente desde el CDN, casi instantáneamente.

## 🧠 Notas para repaso

* El **balanceo de carga** es clave para escalar, distribuir tráfico y evitar fallos en los servicios cloud.
* **Round Robin DNS** es fácil, pero limitado.
* Los **balanceadores dedicados** permiten:

  * Control fino sobre reglas de tráfico
  * Monitorización de salud
  * Sticky sessions
* Las **GeoDNS** y **CDN** optimizan el servicio para usuarios distribuidos globalmente
* La **automatización** del escalado y la orquestación permiten añadir instancias dinámicamente sin afectar el servicio