## Mongo-queries-2
Crear una bd “libreria” y cargar los scripts adjuntos con el comando `load("nombrefichero")` desde el __mongo shell__.

Lanzar las siguientes queries:

- Obtener todos los autores
- Obtener los autores cuyo apellido sea DATE
```
db.libros.aggregate([ {$match: {"autor.apellidos":"DATE"}},{$project:{_id:0,autor:{$concat:["$autor.nombre", " ", "$autor.apellidos"]}}}])
```
- Obtener los libros editados en 1998 o en 2005
```
db.libros.find({$or:[{anyo:"1998"},{anyo:"2005"}]})
db.libros.aggregate([{$match:{$or:[{anyo:"1998"},{anyo:"2005"}]}}, {$project:{_id:0, titulo:1}}]) -> show only title
```
- Obtener el número de libros de la editorial Addison‐Wesley
```
db.libros.find({editorial:"Addison-Wesley"}).count() -> 3

db.libros.aggregate([{$match:{editorial:"Addison-Wesley"}},{$group:{_id:null, numLibros:{$sum:1}}},{$project:{_id:0}}]) -> [ { numLibros: 3 } ]
```
- Obtener el libro que ocupa la tercera posición
```
db.libros.aggregate([{$skip:2}, {$limit:1}, {$project: { _id: 0, titulo:1}}]).toArray()[0].titulo
```
- Obtener la lista de autores de cada libro junto con el título
```

```
- Obtener los títulos de libro publicados con posterioridad a 2004.
- Obtener los libros editados desde 2001 y precio mayor que 50
- Obtener los libros publicados por la editorial Addison‐Wesley después de 2005.
- Obtener el título de libro y editorial para aquellos libros que tengan un precio superior a 50€.
- Obtener los libros publicados en 1998 o a partir de 2005.
