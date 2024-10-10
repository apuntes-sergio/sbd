---
title: 7. Herramientas visuales para interactuar con *MongoDB*
parent: MongoDB
permalink: /mongodb/herramientas
nav_order: 7
---

<h1>Almacenamiento de datos. NoSQL</h1>

<h3>Tabla de contenidos</h3>

- [7. Herramientas visuales para interactuar con *MongoDB*](#7-herramientas-visuales-para-interactuar-con-mongodb)
  - [7.1. *MongoDB* Compass](#71-mongodb-compass)
    - [7.1.1. Instalación](#711-instalación)
    - [7.1.2. Tabajando con *MongoDB* Compass](#712-tabajando-con-mongodb-compass)
  - [7.2. *MongoDB* for VSCode](#72-mongodb-for-vscode)


# 7. Herramientas visuales para interactuar con *MongoDB* 

Hemos visto cómo interactuar con *MongoDB* desde la consola que nos ofrece la base de datos, pero para interactuar de una forma más flexible e intuitiva existen herramientas visuales que nos facilitan el trabajo diario con *MongoDB*

## 7.1. *MongoDB* Compass

Una de ellas es *MongoDB* Compass, que facilita la exploración y manipulación de los datos. De una manera flexible e intuitiva, Compass ofrece visualizaciones detalladas de los esquemas, métricas de rendimiento en tiempo real así como herramientas para la creación de consultas.

Existen tres versiones de Compass, una completa con todas las características, una de sólo lectura sin posibilidad de insertar, modificar o eliminar datos (perfecta para analítica de datos) y una última versión isolated que solo permite la conexión a una instancia local.

Enlace a la documentación oficial de *MongoDB* Compass: [What is *MongoDB* Compass?](https://www.mongodb.com/docs/compass/current/)

### 7.1.1. Instalación

Siguiendo los pasos ofrecidos por la propia web de *MongoDB*, para la instalación de *MongoDB* Compass en Ubuntu seguimos los siguientes pasos:

```bash
# Download *MongoDB* Compass
wget https://downloads.mongodb.com/compass/mongodb-compass_1.40.4_amd64.deb

# Install *MongoDB* Compass
sudo dpkg -i mongodb-compass_1.40.4_amd64.deb

# Start *MongoDB* Compass
mongodb-compass
```

Si hacemos caso a lo que nos dicen en la guía, directamente instalamos la última versión estable.

<div align="center">
    <img src="docs/img/MongoDB/MongoDB21.png" alt="MongoDB" width="50%" />
</div>

### 7.1.2. Tabajando con *MongoDB* Compass

Al iniciar la aplicación, la primera vez nos ofrece conectarnos a la base de datos local. También nos podemos conectar a una base de datos remota e incluso a [Mongo Atlas](https://www.mongodb.com/es/atlas), que como se comentó es la base de datos que ofrece *MongoDB* en la nube.

Una vez conectados a la base de datos, vemos todas las bases de datos exitentes. En la parte inferior tenemos una consola donde podemos actuar de la misma forma que lo hicimos anteriormente.

<div align="center">
    <img src="docs/img/MongoDB/MongoDB22.png" alt="MongoDB" width="60%" />
</div>

Dentro de una base de datos, podemos acceder a las colecciones, listar los documentos, y realizar todo tipo de operaciones sobre los mismos:

<div align="center">
    <img src="docs/img/MongoDB/MongoDB23.png" alt="MongoDB" width="60%" />
</div>

Así como operaciones específicas sobre documentos en concreto. Si nos colocamos con el ratón sobre un documento aparecen cuatro opciones, para *editar*, *copiar,*, *duplicar* y *borrar* el documento. Haciendo doble click, también lo editamos.

Tenemos varias opciones sobre la base de datos, incluso podemos hacer consultas.

<div align="center">
    <img src="docs/img/MongoDB/MongoDB24.png" alt="MongoDB" width="60%" />
</div>

En la imagen:
1. Dentro de una colección, seleccionamos la pestaña de `schema`
2. Introducimos el filtro a buscar
3. Obtenemos el detalle de los datos de los documentos obtenidos
4. Tenemos un histórico de todas las búsquedas realizadas


## 7.2. *MongoDB* for VSCode

También podemos utilizar la extensión que lleva VSCode para trabajar con *MongoDB*.

Para su **instalación**

Si no disponemos de VSCode:
- podemos instalarlo siguiendo los pasos de la propia web de Microsoft: [Visual Studio Code on Linux](https://code.visualstudio.com/docs/setup/linux#_debian-and-ubuntu-based-distributions)
- si tenemos la versión completa de Ubuntu, la podemos instalar desde el gestor de aplicaciones:

<div align="center">
    <img src="docs/img/MongoDB/MongoDB25.png" alt="MongoDB" width="20%" />
    <img src="docs/img/MongoDB/MongoDB26.png" alt="MongoDB" width="50%" />
</div>

Una vez instalado VSCode, instalamos la extensión de *MongoDB* for VS Code, aqui seguimos los pasos de la web oficial donde tenemos cómo instalar y configurar la conexión: [VSCode: Working with MongoDB](https://code.visualstudio.com/docs/azure/mongodb). Para la conexión, pulsamos sobre el botón de *Advanced* y la conexión es sencilla

<div align="center">
    <img src="docs/img/MongoDB/MongoDB27.png" alt="MongoDB" width="40%" />    
    <img src="docs/img/MongoDB/MongoDB28.png" alt="MongoDB" width="40%" />
</div>

Una vez conectados, podremos recorrer las colecciones con los datos así como utilizar un *playground* para interactuar de manera similar al shell:

<div align="center">
    <img src="docs/img/MongoDB/MongoDB29.png" alt="MongoDB" width="40%" />    
    <img src="docs/img/MongoDB/MongoDB30.png" alt="MongoDB" width="40%" />
</div>

Realmente, esta extensión este pensada para trabajar con opciones avanzadas, como crear índices, generar código en lenguajes como *javascript*, *python* o cualquier otro para realizar todo tipo de operaciones en *MongoDB*, o crear variables con datos y estos utilizarlos en nuestras operaciones. Para más información en la web de la extension: [MongoDB for VS Code. *MongoDB* Without Leaving Your IDE](https://www.mongodb.com/products/tools/vs-code)

