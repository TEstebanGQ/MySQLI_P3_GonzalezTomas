# Resumen General del Proceso 

## Contexto General

Durante los **primeros cuatro días de trabajo**, se realizaron ejercicios prácticos y un proyecto aplicado que combinan el uso de **MySQL**, **conexión remota a servidor**, **creación y gestión de bases de datos**, y finalmente un **análisis de muertes accidentales en Colombia entre 2015 y 2024**.  
El proceso se estructuró en cuatro etapas progresivas:

---

## Día 1 — Configuración y conexión al servidor MySQL

### Objetivo:

Aprender a conectarse a un servidor MySQL remoto mediante SSH y configurar correctamente el entorno.

### Pasos realizados:

1. **Conexión SSH al servidor:**

   ```bash
   ssh p4student@172.16.101.117
   ```

2. **Cambio de contraseña de usuario del sistema (`passwd`).**

3. **Actualización del sistema:**

   ```bash
   sudo apt-get update
   ```

4. **Verificación del estado de MySQL:**

   ```bash
   sudo systemctl status mysql.service
   ```

5. **Reinicio del servicio MySQL.**

6. **Acceso como root:**

   ```bash
   sudo mysql
   ```

7. **Ejecución del asistente de seguridad:**

   ```bash
   sudo mysql_secure_installation
   ```

8. **Creación del usuario principal:**

   ```sql
   CREATE USER 'tomas'@'%' IDENTIFIED WITH mysql_native_password BY 'tomas';
   ```

9. **Asignación de permisos:**

   ```sql
   GRANT ALL PRIVILEGES ON *.* TO 'tomas'@'%' WITH GRANT OPTION;
   FLUSH PRIVILEGES;
   ```

### Resultado:

Usuario `tomas` creado y con privilegios totales para acceder desde cualquier host.  
Servidor configurado y listo para trabajar con bases de datos.

---

## Día 2 — Práctica MySQL “Explicación Día 1”

### Objetivo:

Aplicar los comandos básicos de creación y manipulación de bases de datos.

### Ejercicios realizados:

1. **Conexión al servidor remoto:**

   ```bash
   mysql -u tomas -h 172.16.101.117 -p
   ```

2. **Creación de una base de datos:**

   ```sql
   CREATE DATABASE explicacionDia1;
   USE explicacionDia1;
   ```

3. **Creación de tablas:**

   ```sql
   CREATE TABLE Persona (
       idPersona INT PRIMARY KEY AUTO_INCREMENT,
       nombre VARCHAR(50),
       apellido VARCHAR(50)
   );
   ```

4. **Inserción de registros:**

   ```sql
   INSERT INTO Persona (nombre, apellido) VALUES ("Henry", "Duran");
   ```

5. **Visualización de datos:**

   ```sql
   SELECT * FROM Persona;
   ```

6. **Creación de tabla relacionada:**

   ```sql
   CREATE TABLE Casa (
       idCasa INT PRIMARY KEY AUTO_INCREMENT,
       direccion VARCHAR(250),
       idPersona INT,
       FOREIGN KEY (idPersona) REFERENCES Persona(idPersona)
   );
   ```

7. **Inserción de datos con relación:**

   ```sql
   INSERT INTO Casa (direccion, idPersona) VALUES ("Zona Franca", 1);
   ```

### Resultado:

Comprensión de la creación de bases de datos y relaciones entre tablas.  
Identificación y corrección de errores comunes (como `foreign` mal escrito o falta de coincidencia en claves foráneas).

---

## Días 3 y 4 — Proyecto: Análisis de Muertes Accidentales (2015–2024)

**Enlace del trabajo:**  
[Google Drive - Proyecto de análisis](https://drive.google.com/drive/folders/1Ei4o36naXrIhR-2Z3VLkmsOwCMPz0_DW?usp=sharing)

### Objetivo:

Aplicar los conocimientos adquiridos para desarrollar un **proyecto de análisis de datos reales** sobre muertes accidentales en Colombia, con enfoque en la organización, limpieza y presentación de información.

### Contenido trabajado:

- **Título del proyecto:**  
  `Análisis de Muertes Accidentales en Colombia durante el período 2015–2024`

- **Estructura del documento:**
  1. **Introducción:** Contexto general y justificación del estudio.  
  2. **Caso de estudio:** Descripción de las fuentes y el tipo de accidentes.  
  3. **Planificación:** Definición de objetivos, metodología y herramientas.  
  4. **Modelado de datos:** Tablas y relaciones diseñadas según el esquema E-R.  
  5. **Resultados:** Análisis cuantitativo de los registros.  
  6. **Conclusiones:** Observaciones finales sobre patrones y tendencias.

### Herramientas utilizadas:

- MySQL (para la base de datos y consultas analíticas)
- Google Sheets / Drive (para documentación y gráficos)
- Diagramas E-R y modelo lógico (para la estructura del sistema)

### Resultado:

Proyecto de análisis funcional con enfoque en **bases de datos relacionales y análisis estadístico**.  
Entrega organizada y publicada en Google Drive con evidencias del proceso.

---

**Autor:**  
*Tomas Esteban González Quintero*  
*Campuslands – Ruta Java*  
*Bucaramanga, Noviembre 2025*
