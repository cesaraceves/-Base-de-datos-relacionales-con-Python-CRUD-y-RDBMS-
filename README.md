## **Base de datos con SQLite y Python**
 
 Este es un repositorio en donde conectamos una base de datos utilizando SQLite el lenguaje de Python. En esta práctica se creó una tabla en donde se agregaron varios registros con sus respectivos comandos.
 
 Para iniciar cómo se creó la base de datos, es necesario instalar primero SQLite y Python.
 
 ### Importar base de datos
 ```
 import sqlite 3
 ```
 
 ### Conectar base de datos
 Para crear una tabla se utilizó este código:
 ```
 conn = sqlite3.connect('customer.db')
 ```
 ### Crear cursor
 ```
 c = conn.cursor()
```
 ### Crear Tabla 
 
 Para crear una tabla se utilizó este código:
 ```
 c.execute("""CREATE TABLE customers (
		first_name text,
		last_name text,
		email text
		)""")
```

### Insertar registros en una tabla
```
c.execute("INSERT INTO customers VALUES ('John', 'Elder','john@codemy.com')")
```

### Insertar varios registros en una tabla
```
many_customers = [
					('Wes', 'Brown', 'wes@brown.com'),
					('Steph', 'Kuewa', 'steph@kuewa.com'),
					('Dan', 'Pas', 'dan@pas.com'),
				]
				c.executemany("INSERT INTO customers VALUES (?,?,?)", many_customers)
print("Command executed succesfully...")
```
## Consultas

### Consulta llave primaria
>c.execute("SELECT rowid, * customers)")

### Consulta utilizando el apellido de la persona
En esta consulta vamos a buscar las personas que tengan de apellido Elder
>c.execute("SELECT * FROM customers WHERE last_name = 'Elder')")

### Consulta utilizando el apellido específico de una persona usando LIKE
En esta consulta vamos a buscar las personas que tengan de apellido Brown
>c.execute("SELECT * FROM customers WHERE last_name LIKE 'Br%')")

### Ordenar de manera ascendente
c.execute("SELECT rowid, * FROM customers ORBER BY rowid ASC")

### Ordenar de manera descendente
c.execute("SELECT rowid, * FROM customers ORBER BY rowid DESC")

### Actualizar un registro
>c.execute("""UPDATE customers SET first_name = "Bob" 
             WHERE last_name = "Elder" 
             """)
             conn.commit()
             
### Eliminar un registro
>c.execute("DELETE from customers WHERE rowid = '6' ")
conn.commit()

### Our App
En esta parte se utilizó un código para mandar a llamar otro código utilizando import
>import database

En este caso, así se llamaba el otro archivo de python donde se encuentra guardado los otros 
comandos para utilizarlo en este archivo llamado our_app.py

El código de database.py se estructuró de esta manera para que se puedan hacer
las consultas.

>import sqlite3
def show_all():
	#Connect to database
	conn = sqlite3.connect('customer.db')
	#Create a cursor
	c = conn.cursor()
	#Query The Database
	c.execute("SELECT rowid, * FROM customers")
	items = c.fetchall()
	for item in items:
		print (item)
	# Commit our command
	conn.commit()
	#Close our connection
	conn.close()
	
	
	
Para ejecutarlo en el otro archivo, se utilizó este código:
>database.show_all()

### Agregar registro 
En database.py se tiene que agregar este código
>def add_one(first,last,email):
	conn = sqlite3.connect('customer.db')
	c = conn.cursor()
	c.execute("INSERT INTO customers VALUES (?,?,?)", (first, last, email))
	# Commit our command
	conn.commit()
	#Close our connection
	conn.close()

Para ejecutarlo en el our_app.py
>add a record to the database
database.add_one("Laura","Smith","laura@smith.com")

### Eliminar registro 
En database.py se tiene que agregar este código:
>def delete_one(id):
	conn = sqlite3.connect('customer.db')
	c = conn.cursor()
	c.execute("DELETE from customers WHERE rowid = (?)", id)
	# Commit our command and Close connection
	conn.commit()
	conn.close()

Para ejecutarlo en el our_app.py se utiliza este código:
>Delete Record use rowid as string
database.delete_one('6')

### Agregar varios registros
En database.py se tiene que agregar este código:
>def add_many(list):
	conn = sqlite3.connect('customer.db')
	c = conn.cursor()
	c.executemany("INSERT INTO customers VALUES (?,?,?)", (list))
	# Commit our command and Close connection
	conn.commit()
	conn.close()

Para ejecutarlo en el our_app.py se utiliza este código:
>stuff = [
		('Brenda', 'Smitherton', 'brenda@smitherton.com'),
		('Joshua', 'Raintree', 'josh@raintree.com')
		]
database.add_many(stuff)	

### Consultas Registros
En database.py se tiene que agregar este código:
>def email_lookup(email):
	conn = sqlite3.connect('customer.db')
	c = conn.cursor()
	c.execute("SELECT rowid, * from customers WHERE email = (?)", (email,))
	items = c.fetchall()
	for item in items:
		print (item)
		
Para ejecutarlo en el our_app.py se utiliza este código:
>database.email_lookup("john@codemy.com")


