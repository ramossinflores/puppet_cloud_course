## 🧪 Laboratorio: Depurar un despliegue roto en la nube (Apache2 en GCP)

### 🎯 Objetivo

Solucionar un **error 500** en un servidor web (`ws01`) causado por un **conflicto de puertos**, restaurar el servicio Apache2 y eliminar un proceso no deseado que lo bloqueaba.

## 🧭 Paso a paso detallado

### 1. 🕵️‍♀️ Verifica el error

Abre la IP pública de `ws01` → Muestra **HTTP 500 Internal Server Error**.

> Esto indica que el servidor ha tenido un problema inesperado del lado backend.

### 2. 🔧 Comprueba el estado de Apache

```bash
sudo systemctl status apache2
```

📌 Resultado: `failed (Result: exit-code)`
📌 Indica que **Apache no puede iniciar** correctamente.

### 3. 🚨 Intenta reiniciar Apache

```bash
sudo systemctl restart apache2
```

📌 Error persistente → Revisa más detalles:

```bash
sudo journalctl -xeu apache2.service
```

### 4. 🔍 Identifica la causa raíz

```bash
sudo systemctl status apache2
```

📌 Aparece:

```
(98)Address already in use: AH00072: make_sock: could not bind to address [::]:80
```

👉 El **puerto 80 ya está en uso** → Apache no puede "escuchar" en él.

### 5. 🧠 ¿Quién está usando el puerto 80?

```bash
sudo netstat -nlp
```

📌 Verás algo como:

```
tcp 0 0 0.0.0.0:80 ... LISTEN 1356/python3
```

🔎 PID del proceso que ocupa el puerto 80 → `1356` (ejemplo)

### 6. 🔍 Verifica qué script es

```bash
ps -ax | grep python3
```

📌 Resultado:

```
1371 ? Ss 0:00 python3 /usr/local/bin/jimmytest.py
```

👉 Ese script está tomando el puerto 80.

### 7. 💀 Mata el proceso

```bash
sudo kill 1371
```

Pero el proceso vuelve a iniciar... 🔁

### 8. 🧰 Verifica si es un servicio activo

```bash
sudo systemctl --type=service | grep jimmy
```

📌 Resultado:

```
jimmytest.service loaded active running Jimmy python test service
```

🛑 **Detén y desactiva el servicio**:

```bash
sudo systemctl stop jimmytest
sudo systemctl disable jimmytest
```

✅ Ahora el proceso no se volverá a iniciar.

### 9. 🔁 Confirma que el puerto 80 está libre

```bash
sudo netstat -nlp
```

Debe **no aparecer ninguna entrada con el puerto 80**.

### 10. 🚀 Reinicia Apache

```bash
sudo systemctl start apache2
```

Abre el navegador → La IP de `ws01` debe mostrar:

> ✅ Página por defecto de Apache2 Ubuntu

## 📌 Conceptos que estás aplicando

| Comando o concepto       | Qué hace / Por qué se usa                              |                                              |
| ------------------------ | ------------------------------------------------------ | -------------------------------------------- |
| `systemctl status`       | Verifica el estado de un servicio                      |                                              |
| `netstat -nlp`           | Muestra puertos y procesos que los usan                |                                              |
| \`ps -ax                 | grep\`                                                 | Busca procesos activos con una palabra clave |
| `kill`                   | Termina un proceso por su PID                          |                                              |
| `systemctl stop/disable` | Detiene y desactiva un servicio de `systemd`           |                                              |
| `journalctl -xeu`        | Muestra errores y logs detallados de servicios systemd |                                              |

## 🧠 Consejo final

Este tipo de debugging refleja lo que un **SysAdmin o SRE** hace a diario: investigar, aislar y resolver. Si lo complementas con *logs*, *scripts de monitoreo* o *alertas*, te estarás acercando mucho al trabajo profesional en producción.