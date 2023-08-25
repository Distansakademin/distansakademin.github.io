# Avancerad HTML

Låt oss fortsätta med en avancerad del av guiden om HTML. Här kommer vi att utforska mer komplexa koncept och element i HTML.

**Steg 6: Tabeller**

Tabeller används för att strukturera data i rader och kolumner. Du kan använda `<table>` för att skapa en tabell, `<tr>` för att definiera en rad och `<td>` för att lägga till celler (data) i tabellen.

```html
<table>
    <tr>
        <td>Cell 1,1</td>
        <td>Cell 1,2</td>
    </tr>
    <tr>
        <td>Cell 2,1</td>
        <td>Cell 2,2</td>
    </tr>
</table>
```

**Steg 7: Formulär**

HTML-formulär används för att samla in användarinformation. Du kan använda `<form>` för att skapa ett formulär och olika inmatningselement som `<input>`, `<textarea>` och `<select>` för att samla in data.

```html
<form action="/skicka" method="post">
    <label for="namn">Namn:</label>
    <input type="text" id="namn" name="namn" required>
    
    <label for="email">E-post:</label>
    <input type="email" id="email" name="email" required>
    
    <label for="meddelande">Meddelande:</label>
    <textarea id="meddelande" name="meddelande" rows="4" required></textarea>
    
    <input type="submit" value="Skicka">
</form>
```

**Steg 8: Multimedia och inbäddning**

Du kan bädda in multimediaelement som ljud, video och interaktiva kartor med hjälp av HTML.

- Ljud och video med `<audio>` och `<video>`:

```html
<audio controls>
    <source src="ljud.mp3" type="audio/mpeg">
    Din webbläsare stöder inte ljudet.
</audio>

<video controls width="400">
    <source src="video.mp4" type="video/mp4">
    Din webbläsare stödjer inte videon.
</video>
```

- Inbäddning av kartor med Google Maps:

```html
<iframe src="https://www.google.com/maps/embed?pb=!1m18!1m12!1m3..."></iframe>
```

**Steg 9: Semantisk HTML**

Semantisk HTML hjälper till att beskriva innehållet och dess struktur på ett meningsfullt sätt, vilket är viktigt för tillgänglighet och sökmotoroptimering. Använd semantiska element som `<header>`, `<nav>`, `<main>`, `<article>` och `<footer>`.

```html
<header>
    <h1>Min Webbplats</h1>
    <nav>
        <ul>
            <li><a href="#">Hem</a></li>
            <li><a href="#">Om oss</a></li>
            <li><a href="#">Kontakt</a></li>
        </ul>
    </nav>
</header>

<main>
    <article>
        <h2>Vår Historia</h2>
        <p>...</p>
    </article>
</main>

<footer>
    <p>&copy; 2023 Min Webbplats. Alla rättigheter förbehållna.</p>
</footer>
```

Det här är en fördjupad guide om avancerad HTML. Genom att använda dessa koncept kan du skapa mer strukturerade, interaktiva och användarvänliga webbsidor. Kom ihåg att kombinera detta med CSS och kanske JavaScript för att skapa ännu mer imponerande webbupplevelser.

[<< Tillbaka till startsidan](../README.md) | [Nästa: HTML-exempel >>](3-html-exempel.md)