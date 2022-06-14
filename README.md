#  -DESAFIO 8 - MONGO DB 

### Consigna: Utilizando Mongo Shell, crear una base de datos llamada ecommerce que contenga dos colecciones: mensajes y productos.

```
>use ecommerce
>db.createCollection("mensajes")
>db.createCollection("productos")
```

### 1 - Agregar 10 documentos con valores distintos a las colecciones mensajes y productos. El formato de los documentos debe estar en correspondencia con el que venimos utilizando en el entregable con base de datos MariaDB.
## 2 -Definir las claves de los documentos en relación a los campos de las tablas de esa base. En el caso de los productos, poner valores al campo precio entre los 100 y 5000 pesos(eligiendo valores intermedios, ej: 120, 580, 900, 1280, 1700, 2300, 2860, 3350, 4320, 4990). 
```
>db.mensajes.insertMany([{"user":"Lau", "msg":"Hola a todos"}, {"user":"Lucas", "msg":"Hola Lau"}, {"user":"Mica", "msg":"Buen día"},{"user":"Rodrigo", "msg":"Buen día gente"},{"user":"Noe", "msg":"Buen día"}, {"user":"Pablo", "msg":"Que genial es mi tutora"}, {"user":"Dani", "msg":"Le voy a dejar un mensaje copado en la valoracion"},{"user":"Rober", "msg":"Creo que la tutora se copió mi readme"},{"user":"German", "msg":"Aguante Boquita"}])

>db.productos.insertMany([{"name": "Remera","description": "Talle 2","code": 24567,"thumbnail": "htttt/jkljkhj","price": 120,"stock": 23}, {"name": "Pantalon","description": "Talle 2","code": 24767,"thumbnail": "htttt/jkljkhj","price": 580,"stock": 23},{"name": "Vestido","description": "Talle 4","code": 94569,"thumbnail": "htttt/jkljkhj","price": 900,"stock": 23},{"name": "Zapatilla","description": "Talle 2","code": 24567,"thumbnail": "htttt/jkljkhj","price": 1280,"stock": 23},{"name": "Remera","description": "Talle 2","code": 24567,"thumbnail": "htttt/jkljkhj","price":1700,"stock": 23},{"name": "Medias","description": "Talle 2","code": 24567,"thumbnail": "htttt/jkljkhj","price": 2300,"stock": 23},{"name": "Gorra","description": "Talle 2","code": 24567,"thumbnail": "htttt/jkljkhj","price": 2860,"stock": 23},{"name": "Campera","description": "Talle 2","code": 24567,"thumbnail": "htttt/jkljkhj","price": 3350,"stock": 23},{"name": "Short","description": "Talle 2","code": 24567,"thumbnail": "htttt/jkljkhj","price": 4320,"stock": 23},{"name": "Buzo","description": "Talle 2","code": 24567,"thumbnail": "htttt/jkljkhj","price": 4990,"stock": 23}])

```

### 3 - Listar todos los documentos en cada colección
```
>db.mensajes.find().pretty()
>db.productos.find().pretty()
```
### 4 - Mostrar la cantidad de documentos almacenados en cada una de ellas.
```
>db.mensajes.find().count()
>db.productos.find().count()
```
### 5 - Realizar un CRUD sobre la colección de productos:
### a) Agregar un producto más en la colección de productos.
```
>db.productos.insertOne({"name": "Remera","description": "Talle 2","code": 24567,"thumbnail": "htttt/jkljkhj","price": 4500,"stock": 23})
```

### b) Realizar una consulta por nombre de producto específico:
```
>db.productos.findOne({"name": "Buzo"})
``` 
####   i) Listar los productos con precio menor a 1000 pesos.
```     
>db.productos.find({"price": {$lt: 1000} } ).pretty()
``` 
####   ii) Listar los productos con precio entre los 1000 a 3000 pesos.
```
>db.productos.find( { $and: [ {"price": {$gte: 1000 } } , {"price":  { $lte: 3000}  } ] } ).pretty()
```
####  iii) Listar los productos con precio mayor a 3000 pesos
```
>db.productos.find({"price": {$gt: 3000  } } ).pretty()
```
####  iv) Realizar una consulta que traiga solo el nombre del tercer producto más barato
```	
>db.productos.find().sort({price: 1})[2]
```
### c) Hacer una actualización sobre todos los productos con precios  mayores a 4000 pesos.
### d) Cambiar el stock a cero de los productos con precios mayores a 4000 pesos
```
>db.productos.updateMany({ price: { $gt: 4000 } },{ $set: { "stock" : 0 } })
```	
### e) Borrar los productos con precio menor a 1000 pesos
```	
>db.productos.deleteMany({ price: { $gt: 4000 } })
```
### 6) Crear un usuario 'pepe' clave: 'asd456' que sólo pueda leer la base de datos ecommerce

Verificar que pepe no pueda cambiar información. CREAR UN  USUARIO LECTOR
```
> db.createUser( { user: "pepe", pwd: "asd456", roles: [ { role: "read", db:"ecommerce"} ]  } )
```
