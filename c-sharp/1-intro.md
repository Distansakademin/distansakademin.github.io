# Guide till C# Programmering

## Variabler

Variabler används för att lagra och hantera data i C#. Här är några exempel på hur du deklarerar och använder variabler:

```csharp
// Deklarera en integer-variabel
int age = 25;

// Deklarera en sträng-variabel
string name = "John Doe";

// Deklarera en decimal-variabel
decimal price = 29.99m;

// Utskrift av variabler
Console.WriteLine("Ålder: " + age);
Console.WriteLine("Namn: " + name);
Console.WriteLine("Pris: " + price);
```

### Övning 1

Deklarera och initialisera en variabel för att lagra din ålder. Skriv ut åldern på skärmen.

### Övning 2

Deklarera och initialisera en variabel för att lagra ditt namn. Skriv ut ditt namn på skärmen.

## If-satser

If-satser används för att göra beslut i ditt program. Här är ett exempel:

```csharp
int age = 25;

if (age >= 18)
{
    Console.WriteLine("Du är myndig.");
}
else
{
    Console.WriteLine("Du är inte myndig.");
}
```

### Övning 3

Skriv en if-sats som kontrollerar om din ålder är över eller lika med 21. Om det är sant, skriv ut "Du är gammal nog att dricka alkohol", annars skriv ut "Du är för ung för att dricka alkohol."

### Övning 4

Skriv en if-sats som kontrollerar om ett nummer är jämnt eller udda. Använd modulusoperatorn (%) för att göra detta. Skriv ut "Jämnt" eller "Udda" baserat på resultatet.

## Input och Output

För att ta emot användarinput och visa resultat på skärmen kan du använda `Console.ReadLine()` och `Console.WriteLine()`:

```csharp
Console.Write("Ange ditt namn: ");
string userName = Console.ReadLine();

Console.WriteLine("Hej, " + userName + "!");
```

### Övning 5

Be användaren att ange sitt favoritdjur och spara det i en variabel. Skriv ut "Ditt favoritdjur är: " följt av användarens inmatning.

### Övning 6

Be användaren att ange två tal och spara dem som variabler. Skriv ut summan av de två talen.

## Loopar

Loopar används för att utföra en uppgift upprepade gånger. Här är ett exempel på en for-loop:

```csharp
for (int i = 1; i <= 5; i++)
{
    Console.WriteLine("Iteration " + i);
}
```

### Övning 7

Skriv en for-loop som räknar från 1 till 10 och skriver ut varje nummer på skärmen.

### Övning 8

Skriv en while-loop som frågar användaren efter deras favoritfärg tills de anger "blå". När användaren väljer "blå", skriv ut "Blå är också min favoritfärg!" och avsluta loopen.

## Funktioner

Funktioner används för att dela upp kod i mindre delar. Här är ett exempel på en funktion:

```csharp
static void Main(string[] args)
{
    string name = "John Doe";
    PrintName(name);
}

static void PrintName(string name)
{
    Console.WriteLine("Hej, " + name + "!");
}
```

### Övning 9

Skriv en funktion som tar emot ett tal som inmatning och returnerar det dubbla värdet av talet.

### Övning 10

Skriv en funktion som tar emot ett namn som inmatning och returnerar en hälsning med namnet. Anropa funktionen och skriv ut resultatet på skärmen.
