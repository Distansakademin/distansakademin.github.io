# Python för nybörjare

Del 4 av 4: Bygga ett Projekt och Sammanfattning av Python för Nybörjare

**1. Projektidé: En Enkel Väderapplikation**

- Målet är att skapa en enkel konsolbaserad väderapplikation som hämtar väderinformation baserat på en stad.
- För detta projekt kommer vi att använda en extern API, till exempel OpenWeatherMap (notera att du kan behöva registrera dig för en gratis API-nyckel).

**2. Förbereda Projektet**

- Skapa en ny mapp för projektet och en Python-fil, till exempel `weather_app.py`.
- Använd `venv` för att skapa en virtuell miljö och installera nödvändiga paket. Ett paket du behöver är `requests` för att göra HTTP-förfrågningar.

**3. Kodstruktur och API-Anrop**

- Importera nödvändiga moduler och definiera en funktion för att göra API-anrop till väderservicen.
- Använda API-nyckeln och staden som parametrar för att bygga förfrågan.

     ```python
     import requests

     def get_weather(city, api_key):
         url = f"http://api.openweathermap.org/data/2.5/weather?q={city}&appid={api_key}&units=metric"
         response = requests.get(url)
         return response.json()
     ```

**4. Hantera Användarinmatning och Visa Väderdata**

- Läs in stadens namn från användaren.
- Anropa `get_weather`-funktionen och visa relevant väderinformation.

     ```python
     def display_weather(data):
         temp = data['main']['temp']
         description = data['weather'][0]['description']
         print(f"Temperatur: {temp}°C, Väder: {description}")

     city = input("Ange stad: ")
     api_key = "DIN_API_NYCKEL"
     weather_data = get_weather(city, api_key)
     display_weather(weather_data)
     ```

**5. Felhantering**

- Lägg till felhantering för att hantera scenarier som ogiltig stad eller nätverksproblem.

     ```python
     try:
         weather_data = get_weather(city, api_key)
         if weather_data.get('main'):
             display_weather(weather_data)
         else:
             print("Kunde inte hämta väderdata.")
     except Exception as e:
         print(f"Ett fel uppstod: {e}")
     ```

**6. Testa och Förbättra Applikationen**

- Kör applikationen och testa med olika städer.
- Försök förbättra koden genom att lägga till ytterligare funktionalitet, som att visa vindhastighet eller väderprognoser.

**7. Sammanfattning och Nästa Steg**

- Du har nu byggt en enkel, men funktionell, Python-applikation som använder externa API-anrop, felhantering, och användarinmatning.
- Detta projekt exemplifierar många av de koncept vi har gått igenom i guiden, som variabler, datatyper, kontrollstrukturer, funktioner, och moduler.

**Fortsätt Utvecklas**

- Utforska andra API:er och tänk på andra små projekt du kan bygga.
- Öva genom att lägga till nya funktioner till dina projekt eller förbättra deras design och kodstruktur.
- Tänk på att gå vidare till mer avancerade ämnen som databasintegration, webbapplikationsutveckling med Flask eller Django, eller dataanalys med Pandas.

**Kom ihåg, det bästa sättet att lära sig programmera är genom praktisk erfarenhet. Fortsätt koda, experimentera och bygga!**

## Övningar

1. Skapa en funktion som tar en lista med tal som argument och returnerar summan av alla tal i listan.
2. Skapa en funktion som tar en lista med tal som argument och returnerar det största talet i listan.
3. Modifiera väderapplikationen så att den visar en väderprognos för de kommande 5 dagarna.
4. Modifiera väderapplikationen så att den sparar väderdata till en fil och läser in den från filen om användaren söker efter samma stad igen.

## Navigering

- [Del 1](./guide-del-1.md)
- [Del 2](./guide-del-2.md)
- [Del 3](./guide-del-3.md)
- [Del 4](./guide-del-4.md) <-- Du är här