# 🛠️ Configuración de Replica Set de MongoDB con Docker y Keyfile

Este proyecto detalla cómo configurar un **Replica Set** de MongoDB en dos computadoras utilizando Docker y autenticación con un **keyfile**. Los pasos están diseñados para ser fáciles de seguir y asegurar que ambos nodos estén sincronizados de manera eficiente.

## 📋 Requisitos

Antes de comenzar, asegúrate de tener lo siguiente:

- Docker y Docker Compose instalados en ambas PCs.
- MongoDB versión 6 o superior.
- Acceso de red entre **PC1** y **PC2** (verifica con `ping` o `telnet`).
  
## 🚀 Pasos para la configuración

### 1. Generar y transferir el **keyFile**

Primero, generamos un archivo de clave para asegurar la autenticación entre los nodos.

#### En **PC1**:

```bash
openssl rand -base64 756 > mongodb-keyfile
chmod 400 mongodb-keyfile
