# Python för nybörjare

Del 2 av 4: Grundläggande Python-koncept och -syntax

**1. Förståelse av Variabler och Datatyper**

- **Variabler**: I Python lagrar variabler data. De kan namnges nästan vad som helst och behöver inte deklareras med en specifik datatyp.
- **Datatyper**: De vanligaste datatyperna i Python är integers (heltal), floats (flyttal), strings (strängar), och booleans (boolska värden). Till exempel:

     ```python
     my_integer = 10
     my_float = 20.5
     my_string = "Hej Python!"
     my_boolean = True
     ```

**2. Arbeta med Strängar**

- **Skapa en sträng**: Använd enkel (`'`) eller dubbel (`"`) citationstecken.
- **Konkatenering**: Lägg ihop strängar med `+`-tecknet.
- **Formatsträngar**: Använd `.format()` eller f-strängar (från Python 3.6) för att infoga variabler i strängar.

     ```python
     name = "Världen"
     greeting = f"Hej {name}!"
     print(greeting)  # Skriver ut "Hej Världen!"
     ```

**3. Python-listor och -dictionaries**

- **Listor**: Samlingar som är ordnade och ändringsbara. Skapas med hakparenteser `[]`.
- **Dictionaries**: Nyckel-värde-par som används för att lagra data. Skapas med måsvingar `{}`.

     ```python
     my_list = [1, 2, 3]
     my_dictionary = {'nyckel1': 'värde1', 'nyckel2': 'värde2'}
     ```

**4. Kontrollstrukturer**

- **If-satser**: Används för att utföra kod baserat på ett villkor.
- **For-loopar**: Används för att iterera över en sekvens (som en lista, en tupel, en dictionary, en uppsättning, eller en sträng).
- **While-loopar**: Upprepa kod så länge som ett villkor är sant.

     ```python
     if my_integer > 5:
         print("Större än 5")
     
     for item in my_list:
         print(item)

     count = 0
     while count < 3:
         print(count)
         count += 1
     ```

**5. Funktioner**

- Funktioner är en central del av Python och används för att kapsla in kod som utför en specifik uppgift.
- Definiera en funktion med `def`-nyckelordet och anropa den med dess namn.

     ```python
     def say_hello(name):
         return f"Hej {name}!"

     print(say_hello("Världen"))  # Skriver ut "Hej Världen!"
     ```

**6. Importera Moduler**

- Python har ett stort antal inbyggda moduler och bibliotek som utökar dess funktionalitet.
- Använd `import`-nyckelordet för att inkludera moduler i ditt program.

     ```python
     import math
     print(math.sqrt(16))  # Skriver ut 4.0
     ```

**7. Sammanfattning**
I den här delen har du lärt dig om grundläggande Python-koncept som variabler, datatyper, strängar, listor, dictionaries, kontrollstrukturer, funktioner och moduler. Dessa koncept utgör grunden för all Python-programmering. I nästa del kommer vi att utforska felhantering, filhantering och mer avancerade funktioner i Python.

**Fortsätt att öva genom att skapa små program som använder dessa koncept. Experiment och praktisk erfarenhet är nyckeln till att bli en skicklig programmerare.**

## Övningar

1. Skapa en lista med dina favoritfilmer och skriv ut den till konsolen.
2. Skapa en dictionary med dina favoritfilmer och deras betyg, och skriv ut den till konsolen.
3. Skapa en funktion som tar in en lista som argument och skriver ut varje element i listan.
4. Skapa en funktion som tar in en dictionary som argument och skriver ut varje nyckel-värde-par i dictionaryn.


## Navigering

- [Del 1](./guide-del-1.md)
- [Del 2](./guide-del-2.md) <-- Du är här
- [Del 3](./guide-del-3.md)
- [Del 4](./guide-del-4.md)