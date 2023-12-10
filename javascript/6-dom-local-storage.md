# DOM Manipulation, Event Listeners och Local Storage

Välkommen till världen av JavaScript, det språk som ger liv till webbsidor! Som nybörjare kommer denna guide att introducera dig till tre grundläggande men kraftfulla koncept: DOM Manipulation, Event Listeners och Local Storage.

## DOM Manipulation

DOM (Document Object Model) är en programmeringsgränssnitt som låter oss ändra innehållet och strukturen på en webbsida med JavaScript.

### Välja Element

För att manipulera DOM:en måste vi först välja element vi vill manipulera. De vanligaste metoderna för detta är:

```javascript
document.getElementById('id'); // Hämtar element med specifikt ID
document.getElementsByClassName('class'); // Hämtar alla element med en specifik klass
document.getElementsByTagName('tag'); // Hämtar alla element med en specifik tagg, t.ex. 'div'
document.querySelector('selector'); // Hämtar det första elementet som matchar CSS-selektorn
document.querySelectorAll('selector'); // Hämtar alla element som matchar CSS-selektorn
```

### Ändra Element

När ett element är valt kan du ändra dess egenskaper eller innehåll:

```javascript
const h1 = document.querySelector('h1');
h1.textContent = 'Hello, World!'; // Ändrar textinnehållet i h1-elementet
h1.style.color = 'blue'; // Ändrar färgen på texten till blå
```

### Lägga till och Ta Bort Element

För att lägga till ett nytt element till DOM:

```javascript
const nyttElement = document.createElement('p'); // Skapar ett nytt p-element
nyttElement.textContent = 'Detta är ett nytt stycke.';
document.body.appendChild(nyttElement); // Lägger till det nya elementet till body i DOM
```

För att ta bort ett element från DOM:

```javascript
const gammaltElement = document.querySelector('p');
gammaltElement.remove(); // Tar bort det valda elementet från DOM
```

## Övning 1: DOM Manipulation

1. Skapa en HTML-sida med en `div`-behållare och en knapp.
2. Använd JavaScript för att lägga till en lista med tre punkter i `div`:en när användaren klickar på knappen.
3. Gör så att när man klickar på en punkt i listan förändras färgen på texten.

## Event Listeners

Event Listeners låter dig "lyssna" efter händelser (som klick, tangentnedtryckningar, etc.) och köra en funktion när händelsen inträffar.

### Lägga till en Event Listener

```javascript
const knapp = document.querySelector('button');
knapp.addEventListener('click', function() {
  alert('Knappen klickades på!');
});
```

## Övning 2: Event Listeners

1. Skapa en HTML-sida med en knapp och en tom `div`.
2. Använd `addEventListener` för att ändra texten inuti `div`:en till "Knappen trycktes!" när knappen klickas.

## Local Storage

Local Storage är en enkel nyckel-/värdelagringsfunktion i webbläsaren som låter dig spara data mellan sessioner.

### Spara Data

```javascript
localStorage.setItem('nyckel', 'värde');
```

### Hämta Data

```javascript
const varde = localStorage.getItem('nyckel');
console.log(varde); // Skriver ut 'värde'
```

### Ta Bort Data

```javascript
localStorage.removeItem('nyckel');
```

## Övning 3: Local Storage

1. Skapa en HTML-sida med ett textfält och en knapp.
2. När knappen klickas, spara texten från textfältet i Local Storage.
3. När sidan laddas, kolla om det finns sparad text i Local Storage och i så fall visa den i en `div` på sidan.

## Fördjupning i DOM Manipulation

För att skapa interaktiva gränssnitt behöver du veta hur man hanterar HTML-element och attribut. Här är några exempel:

### Ändra attribut

```javascript
const link = document.querySelector('a');
link.setAttribute('href', 'https://example.com'); // Uppdaterar länkens href-attribute
```

### Klasser och Stil

```javascript
const element = document.querySelector('.min-klass');
element.classList.add('en-annan-klass'); // Lägger till en klass
element.classList.remove('min-klass'); // Tar bort en klass

element.style.backgroundColor = 'yellow'; // Ändrar bakgrundsfärgen
```

## Övning 4: Interaktion med klasser och attribut

1. Lägg till en `<input>` för att ändra bakgrundsfärgen på en `div` när en knapp klickas.
2. Implementera en toggle-funktion för en klass varje gång användaren klickar på ett HTML-element.

## Avancerade Event Listeners

Du kan inte bara lyssna på klick, utan det finns en uppsjö av händelser som kan fångas upp, inklusive musrörelser, tangenttryckningar och formulärhändelser.

### Formulärhändelser

```javascript
const form = document.querySelector('form');
form.addEventListener('submit', function(event) {
  event.preventDefault(); // Stoppar standardbeteendet (skickar inte formuläret)
  const inputVal = form.querySelector('input').value;
  alert(`Formulärvärdet: ${inputVal}`);
});
```

## Övning 5: Hantera formulärhändelser

1. Skapa ett enkelt inloggningsformulär med två textfält (för användarnamn och lösenord) och en "Logga in"-knapp.
2. Visa en alert med användarnamn och lösenord när formuläret skickas.

## Kommunicera med Local Storage

Du kan även använda Local Storage för att hantera komplexa data genom att konvertera till och från `JSON` format:

### Spara och Hämta Komplexa Data

```javascript
const user = { name: 'Anna', age: 28 };
localStorage.setItem('user', JSON.stringify(user)); // Sparar som en sträng

const storedUser = JSON.parse(localStorage.getItem('user'));
console.log(storedUser.name); // Skriver ut 'Anna'
```

## Övning 6: Shoppinglista med Local Storage

1. Bygg en enkel app där användaren kan lägga till och ta bort saker från en shoppinglista.
2. När något läggs till eller tas bort, spara listan i Local Storage så att den behålls även när sidan uppdateras.

Genom dessa övningar och exempel borde du nu ha en stabil grund att stå på för att bygga interaktiva webbsidor med JavaScript. Ju mer du övar, desto bekvämare blir du med dessa koncept och desto mer komplexa applikationer kommer du att kunna skapa.


---

[<< Tillbaka till startsidan](../README.md) | [Nästa: Övningar >>](./7-ovningar.md)