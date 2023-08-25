# Kontrollstrukturer

Kontrollsstrukturer används för att styra flödet i ett program. De gör det möjligt att utföra olika uppgifter beroende på olika villkor. I detta avsnitt kommer vi att titta på några av de vanligaste kontrollstrukturerna i JavaScript.

## If-satsen

`if`-satsen används för att utföra en viss handling om ett visst villkor är sant. Om villkoret inte är sant, hoppas programmet över den delen av koden.

```javascript
let age = 18;

if (age >= 18) {
    console.log("Du är myndig.");
} else {
    console.log("Du är inte myndig än.");
}
```

## Else-if-satsen

Om du behöver hantera fler än två fall kan du använda `else if`-satsen.

```javascript
let score = 85;

if (score >= 90) {
    console.log("Betyg A");
} else if (score >= 80) {
    console.log("Betyg B");
} else if (score >= 70) {
    console.log("Betyg C");
} else {
    console.log("Betyg F");
}
```

## For-loop

En `for`-loop används för att upprepa en kodblock ett visst antal gånger.

```javascript
for (let i = 1; i <= 5; i++) {
    console.log("Iteration " + i);
}
```

## While-loop

En `while`-loop används för att upprepa en kodblock så länge ett visst villkor är sant.

```javascript
let count = 0;

while (count < 5) {
    console.log("Count: " + count);
    count++;
}
```

## Do-while-loop

En `do-while`-loop fungerar liknande som en `while`-loop, men kodblocket utförs åtminstone en gång även om villkoret inte är sant från början.

```javascript
let x = 5;

do {
    console.log("x är: " + x);
    x--;
} while (x > 0);
```

# Exempel: FizzBuzz

Här är ett klassiskt exempel på hur du kan använda kontrollstrukturer. Programmet ska skriva ut tal från 1 till 100, men om talet är delbart med 3 ska det skriva "Fizz" istället, om det är delbart med 5 ska det skriva "Buzz", och om det är delbart med både 3 och 5 ska det skriva "FizzBuzz".

```javascript
for (let i = 1; i <= 100; i++) {
    if (i % 3 === 0 && i % 5 === 0) {
        console.log("FizzBuzz");
    } else if (i % 3 === 0) {
        console.log("Fizz");
    } else if (i % 5 === 0) {
        console.log("Buzz");
    } else {
        console.log(i);
    }
}
```

Detta är en översikt över några av de grundläggande kontrollstrukturerna i JavaScript. Genom att använda dessa kan du skapa program som tar beslut och utför upprepande uppgifter på ett effektivt sätt. Kom ihåg att övning är nyckeln till att bemästra dessa koncept!

---

[<< Tillbaka till förstasidan](../README.md) | [Nästa: Eventhantering >>](3-eventhantering.md)
