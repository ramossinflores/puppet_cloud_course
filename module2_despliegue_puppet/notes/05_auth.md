
# 📝 Clase: Infraestructura de certificados en Puppet (PKI y autenticación de nodos)

**Módulo:** 2 – Despliegue de Puppet
**Fecha:** 2025‑06‑18
**Duración:** \~8 min
**Fuente:** Curso “Configuration Management and the Cloud” – Google IT Automation

## 💡 Conceptos clave

### 🔐 Seguridad en Puppet: ¿por qué es necesaria?

* Puppet administra configuraciones que pueden incluir **información sensible**.
* Es fundamental garantizar que **solo máquinas legítimas reciban configuraciones**.
* Para ello, Puppet utiliza una **infraestructura de clave pública (PKI)** basada en **SSL** (como HTTPS).

### 🔑 ¿Cómo funciona la autenticación en Puppet?

* Cada nodo y el servidor Puppet tienen:

  * Una **clave privada** (secreta, local)
  * Una **clave pública** (compartida)

* La autenticación se realiza mediante firmas:

  * El emisor **firma un mensaje con su clave privada**
  * El receptor **verifica la firma con la clave pública**



### 🏢 ¿Cómo saber si una clave pública es confiable?

* Se usa una **autoridad de certificación (CA)**:

  * La CA emite un **certificado digital** que vincula una clave pública con la identidad de la máquina.
  * Puppet incluye una CA propia, aunque también puede integrarse con una CA corporativa externa.



## 🔄 Proceso típico de autenticación en Puppet

1. 🔄 El nodo agente **envía una solicitud de certificado (CSR)** al Puppet master.
2. 🔍 El master verifica la identidad del nodo (manualmente o por script).
3. 🧾 Si es válido, el master **firma el certificado**.
4. 📬 El nodo recoge el certificado firmado.
5. 🔒 A partir de ese momento, la comunicación se realiza **de forma cifrada y autenticada**.



## 🧪 Modos de firma de certificados

| Modo                       | Descripción                                                           | Uso recomendado                        |
| -- |  | -- |
| **Manual**                 | El admin revisa y aprueba cada CSR                                    | Ideal para pruebas o entornos pequeños |
| **Automático (autofirma)** | El Puppet master firma automáticamente                                | ⚠️ No se recomienda en producción      |
| **Script personalizado**   | Automatiza la validación con claves precompartidas u otros mecanismos | Escalable y más seguro                 |



### 🛑 Riesgos de no autenticar

* Una máquina maliciosa podría:

  * Obtener configuraciones indebidas
  * Suplantar el nombre de otro nodo
  * Exponer servicios sensibles

> **Verificar la identidad del nodo es una medida de seguridad crítica.**



## 📁 ¿Dónde se almacenan las solicitudes de certificado?

* En el Puppet master, las CSR pendientes quedan en cola.
* Se pueden revisar y firmar manualmente con:

```bash
puppetserver ca list
puppetserver ca sign --certname NOMBRE_DEL_NODO
```



## 🧠 Notas para repaso

* Puppet usa **SSL** para garantizar comunicaciones seguras.
* Cada nodo tiene un par de claves (pública y privada).
* La **CA integrada de Puppet** permite gestionar certificados fácilmente.
* La autenticación protege tanto la **confidencialidad** como la **integridad** del despliegue.
* **Nunca usar autofirma en producción.**
* En entornos grandes, es preferible usar scripts con datos precompartidos para autenticar automáticamente los nodos.

