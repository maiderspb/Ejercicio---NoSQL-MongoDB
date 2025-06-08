![banner](../images/The Bridge.png)

---

## 📌 Introducción

MongoDB es un sistema de gestión de bases de datos (DBMS) de código abierto que utiliza un modelo de base de datos orientado a documentos que admite numerosos tipos de datos. 

En lugar de usar tablas y filas como en las bases de datos relacionales, la arquitectura MongoDB está formada por colecciones y documentos. 

MongoDB almacena datos en documentos similares a JSON que pueden variar en estructura.
--- 

## 🧩 Objetivos del Proyecto

- Comprender qué es una base de datos no relacional.

- Comprender cómo se realizan las consultas a una base de datos no relacional.

- Analizar y diseñar bases de datos con sus correspondientes colecciones.

- Comprender cómo interactuar con los datos almacenados en la base de datos.

## 🛠️ Tecnologías utilizadas

-   Node.js
-   Express
-   MySQL
-   Sequelize
-   Bcrypt
-   JWT (JSON Web Tokens)
-   Multer (para imágenes)
-   Git y GitHub

---
# Consultas MongoDB - Base de Datos SocialMediaDB

## 1. Insertar datos

### Insertar publicaciones con comentarios

db.Posts.insertOne({
  title: "Viaje a la montaña",
  body: "Experiencia increíble en la montaña.",
  username: "user8",
  comments: [
    { username: "user9", body: "¡Increíble experiencia!" },
    { username: "user10", body: "Quiero hacer ese viaje." }
  ]
});

### Insertar usuarios 

db.Users.insertOne({
  username: "user1",
  email: "user1@email.com",
  age: 25
});

### Actualizar datos

Actualizar todos los campos de una publicación

db.Posts.updateOne(
  { title: "Viaje a la montaña" },
  {
    $set: {
      title: "Aventura en el Amazonas",
      body: "Una travesía inolvidable por la selva.",
      username: "user8",
      comments: [
        { username: "user9", body: "¡Increíble experiencia!" },
        { username: "user10", body: "Quiero hacer ese viaje." }
      ]
    }
  }
);

Cambiar solo el body de una publicación

db.Posts.updateOne(
  { title: "Aventura en el Amazonas" },
  { $set: { body: "Exploración intensa llena de desafíos y paisajes increíbles." } }
);

Actualizar un comentario específico en una publicación

db.Posts.updateOne(
  { title: "Aventura en el Amazonas", "comments.username": "user9" },
  { $set: { "comments.$.body": "¡Un viaje realmente inolvidable!" } }
);

Actualizar todos los campos de un usuario

db.Users.updateOne(
  { username: "user3" },
  {
    $set: {
      username: "nuevo_user3",
      email: "nuevo_user3@email.com",
      age: 27
    }
  }
);

Cambiar el email de dos usuarios

db.Users.updateOne(
  { username: "user1" },
  { $set: { email: "nuevo_email_user1@email.com" } }
);

db.Users.updateOne(
  { username: "user2" },
  { $set: { email: "nuevo_email_user2@email.com" } }
);

Aumentar en 5 años la edad de un usuario

db.Users.updateOne(
  { username: "user3" },
  { $inc: { age: 5 } }
);


### Obtener datos

Seleccionar todas las publicaciones

db.Posts.find().pretty();

Seleccionar publicaciones por username

db.Posts.find({ username: "user2" }).pretty();

Seleccionar usuarios con edad mayor a 20

db.Users.find({ age: { $gt: 20 } }).pretty();

Seleccionar usuarios con edad menor a 23

db.Users.find({ age: { $lt: 23 } }).pretty();

Seleccionar usuarios con edad entre 25 y 30 inclusive

db.Users.find({ age: { $gte: 25, $lte: 30 } }).pretty();

Mostrar usuarios ordenados por edad menor a mayor

db.Users.find().sort({ age: 1 }).pretty();

Mostrar usuarios ordenados por edad mayor a menor

db.Users.find().sort({ age: -1 }).pretty();

Contar número total de usuarios

db.Users.countDocuments();

Mostrar publicaciones con formato personalizado del título

db.Posts.find().forEach(post => {
  print(`Título de la publicación: "${post.title}"`);
});

Seleccionar solo 2 usuarios

db.Users.find().limit(2).pretty();

Buscar dos publicaciones por título específico

db.Posts.find({ title: "Receta de lasaña" }).limit(2).pretty();

### Borrar datos

Eliminar usuarios con edad mayor a 30

db.Users.deleteMany({ age: { $gt: 30 } });

### Seleccionar y filtrar

Contar publicaciones con más de un comentario

db.Posts.countDocuments({ $expr: { $gt: [{ $size: "$comments" }, 1] } });

Seleccionar la última publicación creada 

db.Posts.find().sort({ _id: -1 }).limit(1);

Seleccionar las últimas 5 publicaciones creadas

db.Posts.find().sort({ _id: -1 }).limit(5).pretty();

Eliminar publicaciones que tengan más de un comentario

db.Posts.deleteMany({ $expr: { $gt: [{ $size: "$comments" }, 1] } });