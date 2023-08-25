# Introduktion till CSS

Låt oss gå vidare med en introduktion till CSS (Cascading Style Sheets). CSS används för att styla och formatera HTML-element på webbsidor. Det gör det möjligt att ändra färger, typsnitt, layout och mycket mer. Här är en grundläggande guide om hur du kommer igång med CSS.

**Steg 10: Vad är CSS?**

CSS, eller Cascading Style Sheets, är ett stilarksspråk som används för att definiera utseendet och layouten av HTML-element. Istället för att inkludera all stilinformation direkt i HTML-koden kan du använda CSS för att separera stil från struktur.

**Steg 11: Ansluta CSS till HTML**

Du kan inkludera CSS i din HTML genom att använda `<link>`-elementet i HTML-headern eller genom att inkludera det direkt i HTML-filen med hjälp av `<style>`-taggen.

Exempel på att ansluta en extern CSS-fil:

```html
<!DOCTYPE html>
<html>
<head>
    <title>Min Webbplats</title>
    <link rel="stylesheet" type="text/css" href="style.css">
</head>
<body>
    <h1>Välkommen till Min Webbplats</h1>
    <p>Detta är en paragraf.</p>
</body>
</html>
```

**Steg 12: Grundläggande CSS-syntax**

CSS-regler består av en selektor och en deklaration. Selektorn pekar på vilket HTML-element som ska stilas och deklarationen definierar vilka egenskaper som ska ändras.

```css
/* Välj alla <p>-element och ändra färgen till blå */
p {
    color: blue;
}

/* Välj alla <h1>-element och ändra typsnittet till Arial */
h1 {
    font-family: Arial, sans-serif;
}
```

**Steg 13: Stylingsmöjligheter**

Med CSS kan du göra mycket mer än att bara ändra färger och typsnitt. Här är några exempel på vad du kan göra:

- Ändra färger och bakgrundsfärger:

```css
/* Ändra bakgrundsfärgen på <body> till ljusgrå */
body {
    background-color: lightgray;
}

/* Ändra textfärgen på <p> till grön */
p {
    color: green;
}
```

- Justera text och layout:

```css
/* Centrera texten i <h1> */
h1 {
    text-align: center;
}

/* Skapa en vit kant runt <img> */
img {
    border: 1px solid white;
}
```

- Skapa responsiv design:

```css
/* Anpassa storlek och färg på text beroende på skärmstorlek */
@media screen and (max-width: 600px) {
    p {
        font-size: 14px;
        color: red;
    }
}
```

Det här är bara en introduktion till CSS, och det finns mycket mer att utforska. Genom att använda CSS kan du anpassa och förbättra utseendet på dina webbsidor på ett kraftfullt sätt.

[<< Tillbaka till startsidan](../README.md) | [Nästa: Avancerad CSS >>](5-avancerad-css.md)
