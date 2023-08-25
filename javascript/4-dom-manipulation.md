# DOM-manipulation för att ändra HTML-innehåll och stilar dynamiskt

DOM (Document Object Model) är en representation av en webbsidas struktur och innehåll. Genom att använda JavaScript kan du dynamiskt ändra innehåll och stilar på en webbsida.

## Ändra HTML-innehåll

För att ändra innehållet i ett HTML-element kan du använda egenskapen `innerHTML`.

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>DOM-manipulation</title>
</head>
<body>
    <p id="myParagraph">Detta är en ursprunglig text.</p>
    <button id="changeButton">Ändra text</button>

    <script>
        const button = document.getElementById("changeButton");
        const paragraph = document.getElementById("myParagraph");

        button.addEventListener("click", function() {
            paragraph.innerHTML = "Texten har ändrats!";
        });
    </script>
</body>
</html>
```

## Ändra CSS-stilar

Du kan ändra ett HTML-elements stilar genom att ändra dess CSS-egenskaper med JavaScript.

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>DOM-manipulation</title>
    <style>
        .highlight {
            color: red;
            font-weight: bold;
        }
    </style>
</head>
<body>
    <p id="myParagraph">Detta är en normal text.</p>
    <button id="highlightButton">Markera text</button>

    <script>
        const button = document.getElementById("highlightButton");
        const paragraph = document.getElementById("myParagraph");

        button.addEventListener("click", function() {
            paragraph.classList.add("highlight");
        });
    </script>
</body>
</html>
```

## Lägga till och ta bort element

Du kan även lägga till och ta bort element från DOM-trädet.

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>DOM-manipulation</title>
</head>
<body>
    <ul id="myList">
        <li>Äpple</li>
        <li>Banan</li>
    </ul>
    <button id="addButton">Lägg till</button>
    <button id="removeButton">Ta bort</button>

    <script>
        const addButton = document.getElementById("addButton");
        const removeButton = document.getElementById("removeButton");
        const list = document.getElementById("myList");

        addButton.addEventListener("click", function() {
            const newItem = document.createElement("li");
            newItem.textContent = "Apelsin";
            list.appendChild(newItem);
        });

        removeButton.addEventListener("click", function() {
            const lastItem = list.lastElementChild;
            if (lastItem) {
                list.removeChild(lastItem);
            }
        });
    </script>
</body>
</html>
```

Denna del ger dig en grundläggande förståelse för hur du kan använda DOM-manipulation för att ändra innehåll och stilar på en webbsida dynamiskt. Genom att manipulera DOM kan du skapa interaktiva och responsiva användargränssnitt.

[<< Tillbaka till startsidan](../README.md) | [Nästa: Funktioner, klasser och objekt >>](./5-funktioner-klasser-objekt.md)

