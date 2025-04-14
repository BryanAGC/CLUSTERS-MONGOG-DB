# 🛠️ Configuración de Clusters de BD en Mongo DB con docker compose en React

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

```
> 📝 **Nota:** El archivo generado en **PC1** debe ser enviado a **PC2**.  
> Una vez copiado, en **PC2** ejecuta el siguiente comando para otorgar los permisos adecuados:

```bash
chmod 400 mongodb-keyfile
```
### 🧩 2. Configurar el `docker-compose.yml` en PC1 y PC2

En ambas computadoras, debes agregar la configuración del **Replica Set** y el archivo **keyFile** en el archivo `docker-compose.yml`.

#### 📦 En **PC1**:

```yaml
services:
  mongo:
    image: mongo:6
    container_name: mongo1
    ports:
      - "27019:27017"
    volumes:
      - ./mongodb-keyfile:/data/configdb/mongodb-keyfile
    command: ["mongod", "--replSet", "rs0", "--keyFile", "/data/configdb/mongodb-keyfile"]
```
#### 📦 En **PC2**:

```yaml
services:
  mongo:
    image: mongo:6
    container_name: mongo2
    ports:
      - "27019:27017"
    volumes:
      - ./mongodb-keyfile:/data/configdb/mongodb-keyfile
    command: ["mongod", "--replSet", "rs0", "--keyFile", "/data/configdb/mongodb-keyfile"]
```
