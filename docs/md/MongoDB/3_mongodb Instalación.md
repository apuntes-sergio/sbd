---
layout: default
title: 3. Instalación 
parent: MongoDB
permalink: /mongodb/Instalacion
nav_order: 3
---

<h1>Almacenamiento de datos. NoSQL</h1>

<h3>Tabla de contenidos</h3>

- [3. Instalación](#3-instalación)


# 3. Instalación

En la actualidad, *MongoDB* se como base de datos en tres productos diferentes más un conglomerado de servicios y herramientas que complementas a la base de datos.

<div align="center">
    <img src="../assets/images/MongoDB/MongoDB04.png" alt="MongoDB" width="50%" />
</div>

1. **Mongo Atlas**, como plataforma cloud, con una opción gratuita mediante un cluster de 512MB.
2. **MongoDB Enterprise Advanced**, versión de pago con soporte, herramientas avanzadas de monitorización y seguridad, y administración automatizada.
3. **MongoDB Community Edition**, versión gratuita para trabajar on-premise, con versiones para Windows, MacOS y Linux. *Nosotros de momento trabajaremos con esta versión*

Para la instalación de **MongoDB Community Edition** en un sistema Ubuntu vamos a proceder tal y como se espedifica en la propia web de **mongodb**. [Install *MongoDB* Community Edition](https://www.mongodb.com/docs/manual/tutorial/install-mongodb-on-ubuntu/#install-mongodb-community-edition) 

Realizaremos los siguientes pasos:

```bash
# Requisitos previos
sudo apt-get install gnupg curl                   # Requisitos previos

# Importar claves públicas GPG de MongoDB
curl -fsSL https://www.mongodb.org/static/pgp/server-7.0.asc | sudo gpg -o /usr/share/keyrings/mongodb-server-7.0.gpg --dearmor

# añadir las fuentes
echo "deb [ arch=amd64,arm64 signed-by=/usr/share/keyrings/mongodb-server-7.0.gpg ] https://repo.mongodb.org/apt/ubuntu jammy/mongodb-org/7.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-7.0.list

# recargar paquetes
sudo apt-get update

# e instalar
sudo apt-get install -y mongodb-org
```

Con esto ya tenemos *MongoDB* instalado en nuestro sistema.

Ahora nos falta ponerlo en marcha, para ello habilitamos e iniciamos el servicio

```bash
# recargamos los nuevos servicios
sudo systemctl daemon-reload

# Habilitamos el servicios (esto es opcional, solo si queremos que se inicie al arrancar el equipo)
sudo systemctl enable mongod

# Iniciamos el servicio
sudo systemctl start mongod

# Comprobamos que el servicio se ha iniciado correctamente
sudo systemctl status mongod
```
<div align="center">
    <img src="../assets/images/MongoDB/MongoDB08.png" alt="MongoDB" width="50%" />
</div>

Mediante el siguiente comando también verificamos que esta activa y su versión. 

```bash
mongod --version                                  # Comprobamos la versión
```

<div align="center">
    <img src="../assets/images/MongoDB/MongoDB09.png" alt="MongoDB" width="50%" />
</div>



> **Nota**: *MongoDB* también lo podemos instalar descargando el paquete .deb desde la web de *MongoDB*, pero suele dar mas problemas que con la instalación presentada

Independientemente de nuestro sistema operativo, por defecto, el demonio se lanza sobre el puerto 27017. Una vez instalado, si accedemos a [http://localhost:27017](http://localhost:27017) podremos ver que nos indica cómo estamos intentando acceder mediante HTTP a *MongoDB* mediante el puerto reservado al driver nativo.

<div align="center">
    <img src="../assets/images/MongoDB/MongoDB06.png" alt="MongoDB" width="50%" />
</div>

En vez de instalarlo como un servicio en nuestra máquina, a día de hoy, es mucho más cómodo hacer uso de contenedores Docker o utilizar una solución cloud, aunque nosotros por simplicidad, de momento, realizaremos una instalación tradicional.

Al versión de **Mongo Atlas** nos ofrece de manera gratuita un cluster compartido de servidores con 3 nodos y 512 MB para datos. Si queremos una solución serverless o un servidor dedicado, ya tendremos que pasar por caja.
