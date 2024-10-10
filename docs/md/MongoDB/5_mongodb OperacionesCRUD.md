---
title: 5. Operaciones con datos CRUD
parent: MongoDB
permalink: /mongodb/crud
nav_order: 5
---

<h1>Almacenamiento de datos. NoSQL</h1>

<h3>Tabla de contenidos</h3>

- [5. Operaciones con datos CRUD](#5-operaciones-con-datos-crud)
  - [5.1. Insertar :](#51-insertar-)
  - [5.2. Leer:](#52-leer)
  - [5.3. Actualizar:](#53-actualizar)
  - [5.4. Eliminar:](#54-eliminar)


# 5. Operaciones con datos CRUD

En *MongoDB* , las operaciones **CRUD** (*Crear*, *Leer*, *Actualizar*, *Eliminar*) se realizan utilizando métodos específicos. Aquí te muestro cómo realizar cada una de estas operaciones.

Antes de comenzar a trabajar, debemos entrar en una de las bases de datos con `use` y en todo momento podemos ver las colecciones que tenemos en esta base de datos con `use collections` 

## 5.1. Insertar :

Para insertar documentos en una colección, se utiliza el método `insertOne()` o `insertMany()`.

- `db.collectionName.insertOne(<json>);`: Inserta un solo documentos


Ejemplos

```javascript
// Insertar un solo documento en la colección "usuarios"
db.usuarios.insertOne({
    nombre: "Juan",
    edad: 30,
    ciudad: "Barcelona"
});

// En un única línea, y con comillas dobles, también... 
db.usuarios.insertOne({ nombre: "Toni", edad: 15, ciudad: "Valencia"});

// Insertar un solo documento en la colección "usuarios"
db.usuarios.insertOne({
    nombre: "Juan",
    edad: 30,
    ciudad: "Barcelona",
    intereses: ["fútbol", "música"],
    direccion: { calle: "Calle Mayor", numero: 123 },
    fechaRegistro: new Date(),
    activo: true
});


// Insertar un documento con la fecha actual. Ojo con el último campo
db.usuarios.insertOne({
    nombre: "Dorotea",
    fecha: new Date(),
    lugar: "Xàtiva"
});

// Insertar un documento con una fecha específica 
// con campos que antes no estaban 
// poniendo los campos entre comillas, que es totalmente indiferente
// pero si ponemos los número entre comillas se convierten en texto
db.usuarios.insertOne({
    "nombre": "Filiberto",
    "edad" : "33",
    "fechaNacimiento": new Date("2004-03-15"),
    "ciudad": "Alacant"
});
```

Cuando hacemos una inserción, nos devuelve el resultado del tipo

```js
{
  acknowledged: true,
  insertedId: ObjectId('65e818360ad094ed2ab24245')
}
```


- `db.collectionName.insertMany(<json>);`. Inserción de varios elementos.
Como se trata de una inserción de un conjunto de documentos, lo que hacemos en pasar un **array** y esto se hace mediante el uso de ***corchetes*** : `[]`.

Ejemplos: 

```javascript
// Insertar varios documentos en la colección "usuarios"
db.usuarios.insertMany([
    { nombre: "Ana", edad: 25, ciudad: "Madrid" },
    { nombre: "Carlos", edad: 35, ciudad: "Valencia" }
]);

// Insertar varios documentos en la colección "usuarios"
db.usuarios.insertMany([
    { nombre: "Ana", edad: 25, ciudad: "Madrid", intereses: ["viajes"], fechaRegistro: new Date(), activo: false },
    { nombre: "Carlos", edad: 35, ciudad: "Valencia", intereses: ["lectura"], fechaRegistro: new Date(), activo: true }
]);
```
Observar cómo trabajar con fechas

## 5.2. Leer:

Uno de los aspectos más interesantes de las bases de datos es la capacidad para realizar consultas, por lo que ahora vamos a ver de forma muy breve como leer datos, pero más adelante profundizaremos en la realización de consultas más elaboradas.

Para leer datos de una colección, se utiliza el método `find()`.

```javascript
// Leer todos los documentos de la colección "usuarios"
db.usuarios.find();

// Leer todos los documentos de la colección "usuarios" y formatear la salida json
db.usuarios.find().pretty();

// Leer documentos que coincidan con un criterio específico
db.usuarios.find({ ciudad: "Barcelona" });

// Leer documentos que coincidan con un criterio específico (por ejemplo, ciudad igual a "Barcelona" y activo igual a true)
db.usuarios.find({ ciudad: "Barcelona", activo: true });

// Leer documentos con proyección (seleccionar campos específicos)
db.usuarios.find({}, { nombre: 1, edad: 1 });

// Leer documentos con proyección (seleccionar campos específicos)
db.usuarios.find({}, { nombre: 1, edad: 1, _id: 0 });

// Leer todos los eventos que ocurrieron después de una fecha específica
db.eventos.find({ fecha: { $gt: new Date("2024-01-01") } });

// Leer eventos que ocurrieron en un rango de fechas
db.eventos.find({ fecha: { $gte: new Date("2024-01-01"), $lte: new Date("2024-12-31") } });
```

> **Nota**: No profundizamos más en las búsquedas porque más adelante dedicaremos un punto completo a explicar las búsquedas en más profundidad.

## 5.3. Actualizar:

Para actualizar documentos en una colección, se utiliza el método `updateOne()` o `updateMany()`.

- `db.collection.updateOne(<filter>, <update>)`

El método `updateOne()` se utiliza para actualizar un solo documento que coincida con un criterio específico. Si hay varios documentos que coinciden con el criterio, solo se actualizará el primero que se encuentre.

En la clausula de actualización tenemos el comando `$set`. Además debemos tener en cuenta que tanto el `<filter>` como la `<update>` son json por lo que deben estar comprendidos entre corchetes:

```js
db.collection.updateOne({}, {$set:{}});
```

Veamos algunos ejemplos

```javascript
// Ejemplo de updateOne()
db.usuarios.updateOne(
    { nombre: "Juan" },
    { $set: { edad: 31 } }
);

// Cambiamos más de un valor
db.usuarios.updateOne(
    { nombre: "Juan" },
    { $set: { edad: 31, ciudad: 'Albacete' } }
);

// Actualizar la fecha de un evento específico
db.usuarios.updateOne(
    { nombre: "Alberto" },
    { $set: { fechaRegistro: new Date("2024-03-20") } }
);
```
En el primer ejemplo, se actualizará el primer documento de la colección "usuarios" que tenga el campo `nombre` igual a "Juan". Si hay varios documentos con ese nombre, solo se actualizará uno.

Una vez realizada la actualización, *MongoDB* avisa: 

```js
{
  acknowledged: true,
  insertedId: null,
  matchedCount: 1,
  modifiedCount: 1,
  upsertedCount: 0
}
```

- `db.collection.updateMany(<filter>, <update)`

Por otro lado, el método `updateMany()` se utiliza para actualizar múltiples documentos que coincidan con un criterio específico. Todos los documentos que cumplan el criterio serán actualizados.

```javascript
// Ejemplo de updateMany()
db.usuarios.updateMany(
    { ciudad: "Játiva" },
    { $set: { ciudad: "Xàtiva" } }
);
```

En este ejemplo, se actualizarán todos los documentos de la colección "usuarios" que tengan el campo `ciudad` igual a "Játiva", estableciendo su valor a "Xàtiva".

O sea, `updateOne()` es útil cuando solo quieres actualizar un único documento, mientras que `updateMany()` es útil cuando necesitas actualizar múltiples documentos que cumplan un criterio específico.


- `db.collection.replaceOne(<filter>, <update>)`

Reemplazo completo de un documento. En este caso, al reemplazar el documento que encontramos por una nuevo, no necesitamos el comando `$set`

Ejemplos

```js
db.usuarios.replaceOne(
    { nombre: "Alberto" },
    {     
        nombre: "Alberto D.",
        edad: 18,
        ciudad: "Xàtiva",
        intereses: ["Baloncesto", "Informática"],
        fechaRegistro: new Date(),
        activo: true 
    }
);
```

En este caso, vamos a ver su ejecución, donde veremos incluso que al cambiar el nombre, este campo también cambia aunque se el utilizado para hacer la búsqueda:

<div align="center">
    <img src="docs/img/MongoDB/MongoDB20.png" alt="MongoDB" width="50%" />
</div>

## 5.4. Eliminar:

Para eliminar documentos de una colección, se utiliza el método `deleteOne()` o `deleteMany()`.

En *MongoDB*, tanto `deleteOne()` como `deleteMany()` son métodos utilizados para eliminar documentos de una colección. Aquí tienes las diferencias entre ellos:

- `deleteOne()`

El método `deleteOne()` se utiliza para eliminar un solo documento que coincida con un criterio específico. **Si hay varios documentos** que coinciden con el criterio, **solo se eliminará el primero** que se encuentre.

```javascript
// Ejemplo de deleteOne()
db.usuarios.deleteOne({ nombre: "Juan" });
```

En este ejemplo, se eliminará el primer documento de la colección "usuarios" que tenga el campo `nombre` igual a "Juan". Si hay varios documentos con ese nombre, solo se eliminará uno.

`deleteMany()`

Por otro lado, el método `deleteMany()` se utiliza para eliminar varios documentos que coincidan con un criterio específico. Todos los documentos que cumplan el criterio serán eliminados.

```javascript
// Ejemplo de deleteMany()
db.usuarios.deleteMany({ activo: false });
```
En este ejemplo, se eliminarán todos los documentos de la colección "usuarios" que tengan el campo `activo` igual a false.

Otros ejemplos

```javascript
// Eliminar varios documentos que cumplan el criterio especificado
db.usuarios.deleteMany({ ciudad: "Xàtiva" });

// Eliminar eventos que ocurrieron antes de una fecha específica
db.eventos.deleteMany({ fecha: { $lt: new Date("2024-03-01") } });

```

**Cuidado**. Como siempre debemos tener cuidad a la hora de borrar, de echo si hacemos 

```js
db.usuarios.deleteMany({});
```
Nos borrará **todos** los documentos de la colección.

> **Nota**: Siempre se debe pasar un json dentro de la condición, o sea, dentro de los paréntesis deben haber llaves:
> ```js
> db.usuarios.deleteMany();     //error
> db.usuarios.deleteMany({});   //correcto: json vacío
> ```



Ahora que ya tenemos más herramientas y hemos visto las operaciones básicas de *MongoDB* vamos a profundizar sobre las consultas de los datos, aunque ya las hemos visto brevemente con anterioridad.

Aprovechamos para introducir una base de datos con una colección con datos de prueba. En el siguiente [enlace](https://www.w3resource.com/mongodb-exercises/mongodb-sample-dataset/sample_mflix/movies.zip) tenemos una base de datos de películas que podemos introducir en *MongoDB* por ejemplo usando en *MongoDB* Compass. Para ello creamos una base de datos llamada **consultas** e importamos el fichero descargado.

El comando básico es `.find()`

```js
db.collection.find()            // devuelve todos los documentos
db.collection.find(<filter>)    // devuelve los documentos que cumplen el filtro
```

