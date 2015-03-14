# Ejemplos de uso #

Algunos ejemplos mas avanzados.


### Relaciones entre tablas ###

```
jDB.createDB('dbTest');
jDB.selDB = 'dbTest';
jDB.createTable('usuarios', {cols: ['nombre', 'apellido'], rel: {oneToMany: 'telefonos'}});
jDB.createTable('telefonos', {cols: ['descr', 'numero'], rel: {manyToOne: 'usuarios'}});

jDB.insert('usuarios', {nombre: 'Pepe', apellido: 'Duran'});
		
jDB.insert('telefonos', {descr: 'casa', numero: 213212, id_usuarios: 1});
jDB.insert('telefonos', {descr: 'trabajo', numero: 2112666, id_usuarios: 1});

var rows = jDB.select('usuarios')
    .where(function(row) { return row.nombre == 'Pepe' }, 
    {telefonos: function(fono) {return fono.id == 1}} );

var pepe = rows.rows[0];
```