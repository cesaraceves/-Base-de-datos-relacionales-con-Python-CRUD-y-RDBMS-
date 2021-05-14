## **Base de datos con SQLite y Python**
 
 Este es un repositorio en donde conectamos una base de datos utilizando SQLite el lenguaje de Python. En esta práctica se creó una tabla en donde se agregaron varios registros con sus respectivos comandos.
 
 Para iniciar cómo se creó la base de datos, es necesario instalar primero SQLite y Python.
 
 ### Importar base de datos
 >import sqlite 3
 
 ### Conectar base de datos
 Para crear una tabla se utilizó este código:
 > conn = sqlite3.connect('customer.db')

 ### Crear cursor
 > c = conn.cursor()

 ### Crear Tabla 
 
 Para crear una tabla se utilizó este código:
 >c.execute("""CREATE TABLE customers (
		first_name text,
		last_name text,
		email text
		)""")
>

### Insertar registros en una tabla

>c.execute("INSERT INTO customers VALUES ('John', 'Elder','john@codemy.com')")


### Insertar varios registros en una tabla

>many_customers = [
					('Wes', 'Brown', 'wes@brown.com'),
					('Steph', 'Kuewa', 'steph@kuewa.com'),
					('Dan', 'Pas', 'dan@pas.com'),
				]
				c.executemany("INSERT INTO customers VALUES (?,?,?)", many_customers)
print("Command executed succesfully...")

### Llave primaria
>c.execute("SELECT rowid, * customers)")



### Where Clause
>c.execute("SELECT rowid, * customers)")

