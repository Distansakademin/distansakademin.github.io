# 

För att generera slumpmässig data till en tabell i en SQLite-databas i Python, kan du använda `random` och `sqlite3` modulerna. Här är ett exempel på hur du kan göra det:

1. Börja med att importera de nödvändiga modulerna:

```python
import random
import sqlite3
```

2. Skapa en anslutning till din SQLite-databas genom att ange sökvägen till databasfilen:

```python
conn = sqlite3.connect('path/to/database.db')
```

3. Skapa en cursor för att utföra SQL-frågor:

```python
cursor = conn.cursor()
```

4. Skapa en tabell i databasen om den inte redan finns:

```python
cursor.execute('''
    CREATE TABLE IF NOT EXISTS tablename (
        id INTEGER PRIMARY KEY,
        column1 TEXT,
        column2 INTEGER
    )
''')
```

5. Generera slumpmässig data och lägg till den i tabellen. I detta exempel ska vi lägga till 10 rader:

```python
for i in range(10):
    column1 = 'Random Text ' + str(i)
    column2 = random.randint(1, 100)
    
    cursor.execute('''
        INSERT INTO tablename (column1, column2)
        VALUES (?, ?)
    ''', (column1, column2))
```

6. Kom ihåg att spara ändringarna i databasen och stänga anslutningen när du är klar:

```python
conn.commit()
conn.close()
```

Hela koden skulle se ut så här:

```python
import random
import sqlite3

conn = sqlite3.connect('path/to/database.db')
cursor = conn.cursor()

cursor.execute('''
    CREATE TABLE IF NOT EXISTS tablename (
        id INTEGER PRIMARY KEY,
        column1 TEXT,
        column2 INTEGER
    )
''')

for i in range(10):
    column1 = 'Random Text ' + str(i)
    column2 = random.randint(1, 100)
    
    cursor.execute('''
        INSERT INTO tablename (column1, column2)
        VALUES (?, ?)
    ''', (column1, column2))

conn.commit()
conn.close()
```

Kom ihåg att byta ut "tablename" mot det faktiska namnet på tabellen du vill använda och att ändra sökvägen till rätt plats för din SQLite-databasfil.