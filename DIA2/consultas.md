# Práctica de MySQL – Día 1  

## Conexión, creación de base de datos, tablas y relaciones

---

## 1. Conexión al servidor remoto MySQL

Desde la terminal local se establece conexión con el servidor remoto de MySQL ubicado en `172.16.101.117` utilizando el usuario `tomas`:

```bash
mysql -u tomas -h 172.16.101.117 -p
```

> Se solicita la contraseña y, si es correcta, aparece el mensaje:
>
> ```
> Welcome to the MySQL monitor.
> Server version: 8.0.43 (Ubuntu)
> ```

---

## 2. Visualizar bases de datos existentes

Se ejecuta el comando:

```sql
show databases;
```

**Resultado:**

```
+--------------------+
| Database           |
+--------------------+
| information_schema |
| performance_schema |
+--------------------+
```

---

## 3. Crear una nueva base de datos

Se crea una base de datos llamada **`explicacionDia1`**:

```sql
create database explicacionDia1;
```

> Mensaje: `Query OK, 1 row affected`

Luego se usa esa base de datos:

```sql
use explicacionDia1;
```

---

## 4. Crear la tabla `Persona`

Dentro de la base de datos se crea una tabla para almacenar personas:

```sql
create table Persona (
  idPersona int primary key auto_increment,
  nombre varchar(50),
  apellido varchar(50)
);
```

**Verificar tablas creadas:**

```sql
show tables;
```

**Resultado:**

```
+---------------------------+
| Tables_in_explicacionDia1 |
+---------------------------+
| Persona                   |
+---------------------------+
```

---

## 5. Insertar datos en la tabla Persona

Se inserta un registro:

```sql
insert into Persona (nombre, apellido) values ("Henry", "Duran");
```

Verificar los datos insertados:

```sql
select * from Persona;
```

**Resultado:**

```
+-----------+--------+----------+
| idPersona | nombre | apellido |
+-----------+--------+----------+
|         1 | Henry  | Duran    |
+-----------+--------+----------+
```

---

## 6. Crear tabla con llave foránea (`Casa`)

Inicialmente se cometió un error al escribir **`foregin`** en lugar de **`foreign`**, lo que generó el error:

```
ERROR 1064 (42000): You have an error in your SQL syntax
```

Se corrigió el comando correctamente así:

```sql
create table Casa (
  idCasa int primary key auto_increment,
  direccion varchar(250),
  idPersona int,
  foreign key (idPersona) references Persona(idPersona)
);
```

**Resultado:**

```
Query OK, 0 rows affected
```

---

## 7. Errores comunes y su solución

### Error 1: columna mal escrita

```sql
insert into Casa (dirrecion, idPersona) values ("Zona Franca", 2);
```

**Error:**

```
Unknown column 'dirrecion' in 'field list'
```

**Solución:** corregir el nombre del campo:

```sql
insert into Casa (direccion, idPersona) values ("Zona Franca", 2);
```

---

### Error 2: llave foránea no válida

Cuando se intentó insertar con `idPersona = 2` (que no existía):

```
ERROR 1452 (23000): Cannot add or update a child row: 
a foreign key constraint fails
```

**Solución:** insertar usando un `idPersona` existente:

```sql
insert into Casa (direccion, idPersona) values ("Zona Franca", 1);
```

**Resultado:**

```
Query OK, 1 row affected
```

---

## 8. Consultar datos finales

### Tabla Persona:

```sql
select * from Persona;
```

**Resultado:**

```
+-----------+--------+----------+
| idPersona | nombre | apellido |
+-----------+--------+----------+
|         1 | Henry  | Duran    |
+-----------+--------+----------+
```

### Tabla Casa:

```sql
select * from Casa;
```

**Resultado:**

```
+--------+-------------+-----------+
| idCasa | direccion   | idPersona |
+--------+-------------+-----------+
|      2 | Zona Franca |         1 |
+--------+-------------+-----------+
```

---

## 9. Conclusión de la práctica

Durante la práctica se realizaron con éxito las siguientes acciones:

| Paso | Descripción                   | Resultado                       |
| ---- | ----------------------------- | ------------------------------- |
| 1    | Conexión al servidor remoto   | Acceso correcto                 |
| 2    | Visualización de bases        | Acceso permitido                |
| 3    | Creación de base de datos     | `explicacionDia1` creada        |
| 4    | Creación de tabla Persona     | Estructura básica creada        |
| 5    | Inserción de datos            | Registro agregado               |
| 6    | Creación de tabla Casa        | Relación foránea establecida    |
| 7    | Corrección de errores         | Escritura y claves corregidas   |
| 8    | Inserción con relación válida | Registro exitoso                |
| 9    | Consulta de datos             | Tablas relacionadas consultadas |

---

## Resultado final

El usuario `tomas` logró:

- Conectarse al servidor remoto MySQL.
- Crear y usar una base de datos.
- Crear tablas relacionadas con llave foránea.
- Insertar y consultar información correctamente.
- Resolver errores de sintaxis y restricciones.

Sistema y conexión 100% funcional

---

📅 **Autor:** Tomás Esteban González Quintero  
🧩 **DIA 2:** Práctica MySQL – Explicación Día 1  
🏫 **Campuslands – Ruta Java**
