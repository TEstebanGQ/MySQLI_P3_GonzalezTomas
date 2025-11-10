# 💻 Instalación, Configuración y Conexión a MySQL en un Servidor Remoto Linux

##  1. Conexión al servidor remoto

Primero se realiza la conexión al servidor remoto mediante SSH.  
Esto permite acceder a la terminal del servidor Linux donde está instalado MySQL.

```bash
ssh p4student@172.16.101.117
```

> Luego se ingresa la contraseña asignada al usuario remoto.

---

## 2. Cambio de contraseña del usuario del sistema

Una vez dentro del servidor, se cambia la contraseña del usuario del sistema operativo para mayor seguridad:

```bash
passwd
```

Se ingresan los siguientes datos:

- Contraseña actual
- Nueva contraseña
- Confirmación de la nueva contraseña

> Mensaje esperado: `password updated successfully`

---

## 3. Actualizar los repositorios del sistema

Antes de trabajar con MySQL, se recomienda actualizar los paquetes del sistema operativo:

```bash
sudo apt-get update
```

> Esto garantiza que los paquetes estén en su versión más reciente y evita errores en futuras instalaciones.

---

## 🧰 4. Verificar estado de MySQL

Se comprueba si el servicio de MySQL está instalado y corriendo:

```bash
sudo systemctl status mysql.service
```

Si aparece `active (running)` significa que el servicio está funcionando correctamente.

---

## ▶️ 5. Controlar el servicio MySQL

Para asegurarse de que el servicio funcione bien, se pueden ejecutar los siguientes comandos:

```bash
sudo systemctl stop mysql.service     # Detiene el servicio
sudo systemctl start mysql.service    # Inicia el servicio
sudo systemctl restart mysql.service  # Reinicia el servicio
```

---

## 6. Entrar como usuario root a MySQL

Para tener acceso administrativo dentro de MySQL, se ingresa con el usuario `root`:

```bash
sudo mysql
```

> Esto abre la consola de MySQL con permisos administrativos.

---

## 7. Configurar MySQL (Seguridad básica)

MySQL incluye una herramienta interactiva llamada `mysql_secure_installation` que permite fortalecer la seguridad.

Se ejecuta así:

```bash
sudo mysql_secure_installation
```

Durante la ejecución:

- Se elimina el usuario anónimo
- Se elimina la base de datos `test`
- Se bloquea el acceso remoto del root
- Se recarga la tabla de privilegios

> Al finalizar, se muestra el mensaje:  
> `All done! If you've completed all of the above steps, your MySQL installation should now be secure.`

---

## 8. Crear un nuevo usuario MySQL

Desde la consola de MySQL (como root), se crea un usuario personalizado llamado **`tomas`** con contraseña **`tomas`**.

```sql
CREATE USER 'tomas'@'%' IDENTIFIED WITH mysql_native_password BY 'tomas';
```

> `%` significa que el usuario podrá conectarse desde **cualquier dirección IP**.

---

## 9. Otorgar privilegios al usuario

Por defecto, el usuario nuevo no tiene permisos.  
Por eso, se le otorgan privilegios globales para administrar bases de datos:

```sql
GRANT ALL PRIVILEGES ON *.* TO 'tomas'@'%' WITH GRANT OPTION;
FLUSH PRIVILEGES;
EXIT;
```

Explicación:

- `GRANT ALL PRIVILEGES`: concede todos los permisos.
- `ON *.*`: sobre todas las bases de datos y tablas.
- `WITH GRANT OPTION`: permite que este usuario también otorgue permisos a otros.
- `FLUSH PRIVILEGES`: aplica los cambios inmediatamente.
- `EXIT`: salir del entorno MySQL.

---

## 10. Conectarse con el nuevo usuario

Ahora se puede ingresar a MySQL usando el usuario `tomas`:

```bash
mysql -u tomas -p
```

(Se ingresa la contraseña `tomas` cuando la pida.)

---

## 11. Verificar acceso y privilegios

Una vez dentro de MySQL, se comprueba que el usuario tenga acceso:

```sql
SHOW DATABASES;
```

Si aparecen bases como `mysql`, `information_schema`, `sys`, etc., significa que el usuario tiene permisos correctos.

---

## 12. (Opcional) Crear base de datos de prueba

Para verificar el correcto funcionamiento del usuario:

```sql
CREATE DATABASE prueba;
USE prueba;

CREATE TABLE ejemplo (
  id INT AUTO_INCREMENT PRIMARY KEY,
  nombre VARCHAR(50)
);

INSERT INTO ejemplo (nombre) VALUES ('Conexión exitosa');
SELECT * FROM ejemplo;
```

---

## 🧾 13. Resumen general del proceso

| Paso | Acción                       | Resultado esperado               |
| ---- | ---------------------------- | -------------------------------- |
| 1    | Conexión SSH                 | Acceso al servidor remoto        |
| 2    | Cambio de contraseña         | Seguridad del usuario            |
| 3    | Actualización del sistema    | Repositorios actualizados        |
| 4    | Verificar servicio MySQL     | Servicio activo                  |
| 5    | Controlar servicio           | Arranque correcto                |
| 6    | Acceder como root            | Permisos administrativos         |
| 7    | Configurar seguridad         | Eliminación de accesos inseguros |
| 8    | Crear usuario nuevo          | Usuario `tomas` creado           |
| 9    | Otorgar permisos             | Usuario con privilegios          |
| 10   | Conectarse con nuevo usuario | Acceso exitoso                   |
| 11   | Verificar bases              | Visualización correcta           |
| 12   | Crear base y tabla           | Prueba de funcionamiento exitosa |

---

## Resultado final

El servidor MySQL quedó configurado con:

- Un usuario personalizado (`tomas`)
- Acceso remoto permitido (`'%'`)
- Seguridad básica configurada
- Servicio activo y funcional

Sistema listo para desarrollar, conectar aplicaciones o gestionar bases de datos.

---

📅 **Autor:** Tomás Esteban González Quintero  
🧠 **DIA 1:** Configuración de entorno MySQL remoto  
 **Campuslands – Ruta Java**
