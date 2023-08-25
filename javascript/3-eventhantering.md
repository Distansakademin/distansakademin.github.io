# Hantering av händelser med Event Listeners

Event listeners används för att lyssna efter olika händelser som inträffar på en webbsida och sedan utföra viss kod när händelsen inträffar. Detta är användbart för att interagera med användare och svara på deras åtgärder, som att klicka på en knapp, skriva in text i ett formulär eller hovra över ett element.

## Grundläggande Event Listener

Här är ett exempel på hur du kan använda en event listener för att reagera på en klickhändelse på en knapp:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Event Listener</title>
</head>
<body>
    <button id="myButton">Klicka här</button>

    <script>
        const button = document.getElementById("myButton");

        button.addEventListener("click", function() {
            alert("Knappen har klickats!");
        });
    </script>
</body>
</html>
```

## Eventobjektet

När en händelse inträffar, skickas ett eventobjekt till event listenern som innehåller information om händelsen. Du kan använda detta objekt för att få mer information om händelsen och hantera den på lämpligt sätt.

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Event Object</title>
</head>
<body>
    <button id="myButton">Klicka här</button>

    <script>
        const button = document.getElementById("myButton");

        button.addEventListener("click", function(event) {
            alert("Händelse typ: " + event.type);
            console.log("X-koordinat: " + event.clientX);
            console.log("Y-koordinat: " + event.clientY);
        });
    </script>
</body>
</html>
```

## Att ta bort Event Listeners

Om du vill ta bort en event listener kan du använda `removeEventListener`-metoden. Detta kan vara användbart om du vill sluta lyssna på händelser efter att de inte längre behövs.

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Ta bort Event Listener</title>
</head>
<body>
    <button id="myButton">Klicka här</button>

    <script>
        const button = document.getElementById("myButton");

        function clickHandler() {
            alert("Knappen har klickats!");
            button.removeEventListener("click", clickHandler);
        }

        button.addEventListener("click", clickHandler);
    </script>
</body>
</html>
```

Detta ger dig en överblick över hur du kan använda event listeners för att reagera på olika händelser på din webbsida. Event listeners är en viktig del av interaktiv webbutveckling och ger dig möjlighet att skapa användarvänliga och dynamiska användargränssnitt.

---

[<< Tillbaka till startsidan](../README.md) | [Nästa: DOM-manipulering >>](./4-dom-manipulation.md)
