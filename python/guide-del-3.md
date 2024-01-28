# Python för nybörjare

Del 3 av 4: Avancerade Koncept och Praktiska Tillämpningar i Python

**1. Felhantering**

- **Try-Except Block**: Används för att hantera potentiella fel i Python-kod. Detta gör ditt program mer robust och användarvänligt.
- Exempel på felhantering:

     ```python
     try:
         result = 10 / 0
     except ZeroDivisionError:
         print("Fel: Delning med noll.")
     ```

**2. Filhantering**

- Python gör det enkelt att läsa från och skriva till filer.
- Använd `open()` för att öppna en fil, och glöm inte att stänga filen när du är klar.
- Använd `with`-statement för att automatisera stängningen av filen.

     ```python
     with open('exempel.txt', 'r') as file:
         innehall = file.read()
     print(innehall)
     ```

**3. List Comprehensions**

- En kortare syntax för att skapa listor baserat på befintliga listor.
- Används ofta för att göra koden mer lättläst och koncis.

     ```python
     kvadrater = [x * x for x in range(10)]
     ```

**4. Funktioner: Lambda, Map och Filter**

- **Lambda**: Anonyma funktioner definierade med `lambda`-nyckelordet.
- **Map**: Används för att tillämpa en funktion på varje element i en lista.
- **Filter**: Används för att filtrera element i en lista baserat på ett villkor.

     ```python
     dubbla = map(lambda x: x * 2, [1, 2, 3, 4])
     jämna = filter(lambda x: x % 2 == 0, [1, 2, 3, 4])
     ```

**5. Objektorienterad Programmering (OOP)**

- Python stödjer OOP, som hjälper till att organisera och strukturera större program.
- Definiera klasser och skapa objekt för att representera verkliga koncept.
- Exempel på en enkel klass:

     ```python
     class Bil:
         def __init__(self, modell, färg):
             self.modell = modell
             self.färg = färg

         def visa_info(self):
             print(f"Modell: {self.modell}, Färg: {self.färg}")

     min_bil = Bil("Volvo", "Blå")
     min_bil.visa_info()
     ```

**6. Moduler och Paket**

- Moduler är Python-filer som innehåller definitioner och uttalanden.
- Paket är samlingar av moduler.
- Använd `import` för att inkludera modulens funktionalitet i ditt program.
- Skapa egna moduler genom att spara dina Python-skript och importera dem i andra Python-filer.

**7. Virtuella Miljöer**

- Virtuella miljöer i Python används för att hantera beroenden och Python-paket för olika projekt.
- Använd `venv` för att skapa en isolerad miljö för varje projekt.
- Detta håller dina projekt organiserade och förhindrar konflikter mellan paket.

**8. Sammanfattning**
I den här delen har vi utforskat några av de mer avancerade funktionerna i Python, inklusive felhantering, filhantering, list comprehension, lambda-funktioner, OOP, moduler och paket, samt virtuella miljöer. Dessa koncept är viktiga för att skapa effektiva och välorganiserade Python-program.

**I nästa och sista del kommer vi att fokusera på att använda dessa koncept för att bygga ett litet projekt, vilket ger en praktisk tillämpning av det du har lärt dig. Fortsätt att experimentera och bygga små projekt för att förbättra dina färdigheter i Python.**

## Övningar

1. Skapa en funktion som tar in en lista som argument och returnerar en ny lista med alla element i den ursprungliga listan som är delbara med 3.
2. Skapa en funktion som tar in en lista som argument och returnerar en ny lista med alla element i den ursprungliga listan som är delbara med ett tal som anges av användaren.
3. Skapa en klass som representarar en bok. En bok har följande attribut: titel, författare, sidor och ISBN. Skapa en metod som skriver ut bokens information till konsolen.

## Navigering

- [Del 1](./guide-del-1.md)
- [Del 2](./guide-del-2.md)
- [Del 3](./guide-del-3.md) <-- Du är här
- [Del 4](./guide-del-4.md)
