# Användning av Funktioner och Objekt i JavaScript

## Funktioner

Funktioner är en grundläggande byggsten i JavaScript och används för att definiera återanvändbar kod. De tillåter dig att gruppera en uppsättning instruktioner och utföra dem när funktionen anropas. Här är hur du definierar och använder funktioner:

```javascript
// Funktion som lägger ihop två tal
function add(a, b) {
    return a + b;
}

const result = add(5, 3); // Anropar funktionen och sparar resultatet i "result"
console.log(result); // Resultatet (8) loggas i konsolen
```

Du kan också använda anonyma funktioner eller lambda-funktioner:

```javascript
// Anonym funktion (utan namn) som multiplicerar två tal
const multiply = function(x, y) {
    return x * y;
};

const product = multiply(4, 7);
console.log(product); // Resultatet (28) loggas i konsolen
```

## Objekt

Objekt tillåter dig att organisera data och funktionalitet tillsammans. De består av egenskaper (variabler) och metoder (funktioner). Objekt skapas med hjälp av en mall kallad konstruktor eller med objektliteralnotation.

### Objektliteralnotation

```javascript
const person = {
    firstName: "Alice",
    lastName: "Johnson",
    age: 30,
    greet: function() {
        console.log("Hej, jag är " + this.firstName + " " + this.lastName + ".");
    }
};

console.log(person.firstName); // "Alice"
person.greet(); // "Hej, jag är Alice Johnson."
```

### Konstruktorfunktioner

Konstruktorfunktioner används för att skapa flera liknande objekt med gemensamma egenskaper och metoder.

```javascript
function Person(firstName, lastName, age) {
    this.firstName = firstName;
    this.lastName = lastName;
    this.age = age;
    this.greet = function() {
        console.log("Hej, jag är " + this.firstName + " " + this.lastName + ".");
    };
}

const person1 = new Person("Eva", "Smith", 28);
const person2 = new Person("Bob", "Johnson", 35);

console.log(person1.firstName); // "Eva"
person2.greet(); // "Hej, jag är Bob Johnson."
```

## Prototyper och Objektorienterad Programmering

JavaScript använder en prototypbaserad objektorienterad programmeringsmodell. Det innebär att objekt kan ärva egenskaper och metoder från andra objekt, så kallade prototyper. Här är en översiktlig introduktion:

```javascript
// Skapa en prototyp
function Animal(name) {
    this.name = name;
}

Animal.prototype.makeSound = function() {
    console.log("Ljudet av ett djur.");
};

// Skapa ett nytt objekt baserat på prototypen
const cat = new Animal("Katt");

console.log(cat.name); // "Katt"
cat.makeSound(); // "Ljudet av ett djur."
```

## 'this' Nyckelordet

I JavaScript representerar `this` nyckelordet det aktuella objektet som kod körs i. Det kan variera beroende på hur en funktion anropas.

```javascript
const person = {
    firstName: "Alice",
    sayHello: function() {
        console.log("Hej, jag är " + this.firstName + ".");
    }
};

person.sayHello(); // "Hej, jag är Alice."
```

## Sammanfattning

Funktioner och objekt är grundläggande byggstenar i JavaScript-programmering. Funktioner låter dig organisera kod i återanvändbara block, medan objekt låter dig organisera data och funktionalitet tillsammans. Genom att använda objektorienterad programmering och förståelse av `this` nyckelordet kan du bygga mer strukturerad och effektiv kod.

---

[<< Tillbaka till startsidan](../README.md) | [Nästa: Övningar >>](./6-local-storage.md)
