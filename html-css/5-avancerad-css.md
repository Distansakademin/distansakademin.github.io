# Avancerad CSS

Låt oss fortsätta med guiden om CSS genom att utforska några avancerade koncept och tekniker.

**Steg 14: Klasser och Id:n**

För att mer specifikt styra enskilda element kan du använda klasser och id:n i CSS-selektorer. Klasser används för att applicera samma stil på flera element med samma klass, medan id:n används för att identifiera och stilisera ett unikt element.

```html
<!-- HTML -->
<p class="highlight">Detta är en markerad paragraf.</p>
<p id="special">Detta är ett speciellt element.</p>
```

```css
/* CSS */
.highlight {
    background-color: yellow;
}

#special {
    font-weight: bold;
    color: blue;
}
```

**Steg 15: Pseudo-element och Pseudo-klasser**

Pseudo-element och pseudo-klasser låter dig applicera specifika stilar för särskilda tillstånd eller delar av element.

```css
/* Skapa en röd ram runt länkar när de hovras över */
a:hover {
    border: 1px solid red;
}

/* Infoga innehåll före varje <p>-element */
p::before {
    content: "»";
}
```

**Steg 16: Boxmodellen**

Boxmodellen beskriver hur innehållet i ett element är strukturerat inom dess omgivande ram. Den består av innehåll, padding, gräns och marginal.

```css
/* Ge <div> element en 10px tjock svart kant och 20px utfyllnad */
div {
    border: 10px solid black;
    padding: 20px;
    margin: 15px;
}
```

**Steg 17: Flexbox och Grid**

Flexbox och CSS Grid är layoutmodeller som låter dig bygga komplexa layouter med enkla metoder.

Flexbox:

```css
.container {
    display: flex;
    justify-content: center;
    align-items: center;
}
```

Grid:

```css
.container {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    grid-gap: 10px;
}
```

**Steg 18: Responsiv design**

Använd medier för att skapa responsiv design och anpassa stilen baserat på skärmstorlek.

```css
/* Ändra storlek på text när skärmbredden är mindre än 768px */
@media screen and (max-width: 768px) {
    p {
        font-size: 14px;
    }
}
```

Det här är några avancerade CSS-koncept som du kan utforska för att göra dina webbsidor ännu mer interaktiva och användarvänliga. Kombinera dessa koncept med HTML för att skapa dynamiska och väldesignade webbupplevelser.

[<< Tillbaka till startsidan](../README.md) | [Nästa: Avancerad CSS 2 >>](6-avancerad-css-2.md)
