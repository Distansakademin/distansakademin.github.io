# Grunderna i HTML

<!-- markdownlint-disable MD036 -->

Här är en detaljerad guide om hur du kommer igång med HTML. HTML (Hypertext Markup Language) är grunden för att skapa webbsidor. Genom att använda HTML kan du strukturera och formatera innehåll på webbsidor.

**Steg 1: Skapa en grundläggande HTML-struktur**

Börja med att skapa en enkel HTML-struktur genom att följa detta exempel:

```html
<!DOCTYPE html>
<html>
<head>
    <title>Min första webbsida</title>
</head>
<body>
    <h1>Välkommen till min webbsida</h1>
    <p>Detta är en paragraf på min webbsida.</p>
</body>
</html>
```

- `<!DOCTYPE html>`: Denna rad definierar vilken version av HTML som används (HTML5 i detta fall).
- `<html>`: Huvudtaggen som innesluter allt innehåll på webbsidan.
- `<head>`: Här placeras metadata och länkar till externa filer (t.ex. stilmallar och scripts).
- `<title>`: Titeln på webbsidan som visas i webbläsarens flik.
- `<body>`: Här placeras själva innehållet som visas på webbsidan.

**Steg 2: Lägg till text och element**

För att lägga till text och olika element på din webbsida, kan du använda HTML-taggar. Här är några grundläggande exempel:

- Rubriker: Använd `<h1>`, `<h2>`, `<h3>` osv. för rubriker med olika nivåer.

```html
<h1>Detta är en huvudrubrik</h1>
<h2>Detta är en underrubrik</h2>
```

- Paragrafer: Använd `<p>` för att skapa paragrafer.

```html
<p>Detta är en paragraf med text.</p>
```

- Länkar: Använd `<a>` för att skapa länkar till andra sidor.

```html
<a href="https://www.example.com">Besök Example.com</a>
```

- Bilder: Använd `<img>` för att infoga bilder.

```html
<img src="bild.jpg" alt="En bild" width="300" height="200">
```

**Steg 3: Skapa listor**

Du kan skapa både ordbokslistor (`<ul>`) och numrerade listor (`<ol>`), samt lista ut element med `<li>`.

```html
<ul>
    <li>Äpple</li>
    <li>Banan</li>
    <li>Apelsin</li>
</ul>

<ol>
    <li>Första punkt</li>
    <li>Andra punkt</li>
    <li>Tredje punkt</li>
</ol>
```

**Steg 4: Formatera text och layout**

För att ändra textens utseende och layout kan du använda CSS (Cascading Style Sheets), men du kan också använda enklare HTML-attribut.

- Fetstil: Använd `<strong>` eller `<b>` för att göra texten fet.

```html
<strong>Detta är fetstil text</strong>
```

- Kursiv: Använd `<em>` eller `<i>` för att göra texten kursiv.

```html
<em>Detta är kursiv text</em>
```

- Radbrytning: Använd `<br>` för att infoga en radbrytning.

```html
<p>Denna text<br>är på två rader.</p>
```

**Steg 5: Kommentarer**

Du kan lägga till kommentarer i koden för att förklara vad olika delar gör. Kommentarer syns inte på webbsidan och påverkar inte dess utseende.

```html
<!-- Detta är en kommentar -->
```

Det här är en grundläggande introduktion till HTML. För mer avancerade funktioner och strukturer, inklusive formulär och inbäddning av multimedia, rekommenderas att du fördjupar dig i dokumentationen för HTML och CSS. Lycka till med din webbutvecklingsresa!

[<< Tillbaka till startsidan](../README.md) | [Nästa: Avancerad HTML >>](2-avancerad-html.md)
