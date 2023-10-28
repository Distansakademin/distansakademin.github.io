# Bygg ett flerlagerprojekt i asp net web-api

Skriv en guide för att bygga om ett asp net web-api till ett flerlagerprojekt med `WebAPI`, `Services`, `Models`, och `Repositories`-projekt.

## Steg 1: `Models`

- Skapa ett nytt projekt i samma solution som ert web-api. Döp det till `Models`.
- Ta bort `Class1.cs`-filen.
- Flytta era modeller från web-api-projektet till `Models`-projektet.
- Lägg till nödvändiga paket för att kunna använda `Entity Framework Core`.
- Ta bort era modeller från ert web-api-projekt.
- Uppdatera er kod i web-api-projektet så att den använder modellerna från `Models`-projektet och kontrollera att allt fungerar som det ska.

## Steg 2: `Repositories`

- Skapa ett nytt projekt i samma solution som ert web-api. Döp det till `Repositories`.
- Ta bort `Class1.cs`-filen.
- Lägg till nödvändiga paket.
- Skapa en `DatabaseConnection`-klass som ärver från `DbContext`.
- Lägg till era `DbSet`-objekt i `DatabaseConnection`-klassen.
- Se till att er `DatabaseConnection`-klass har en `OnConfiguring`-metod som anropar `UseSqlite`-metoden och skickar med en connection string.
- Byt ut era databasanrop i web-api-projektet mot anrop till `DatabaseConnection`-klassen i `Repositories`-projektet och kontrollera att allt fungerar som det ska.
  - Byt alltså ut `_context.Cars` mot `var db = new DatabaseConnection();` och sedan `db.Cars`.

```csharp
public class DatabaseConnection : DbContext
{
    private const string CONNECTION_STRING = "Data Source=favoritecars2.sqlite";

    protected override void OnConfiguring(DbContextOptionsBuilder optionsBuilder)
    {
        optionsBuilder.UseSqlite(CONNECTION_STRING);
        
        base.OnConfiguring(optionsBuilder);
    }

    public DbSet<Car> Cars { get; set; }
}
```

## Steg 3: `Services`

- Skapa ett nytt projekt i samma solution som ert web-api. Döp det till `Services`.
- Ta bort `Class1.cs`-filen.
- Lägg till nödvändiga paket.
- Skapa en `CarService`-klass som har en konstruktor som tar emot en `DatabaseConnection`-instans.
- Skapa en statisk metod i `CarService`-klassen som hämtar alla bilar från databasen.
- Byt ut anropet till databasen i web-api-projektet mot ett anrop till `CarService`-klassen i `Services`-projektet och kontrollera att allt fungerar som det ska.

```csharp
public class CarService
{
    public static async Task<List<Car>> GetAllCars()
    {
        var db = new DatabaseConnection();

        var cars = await db.Cars.ToListAsync();

        return cars;
    }
}
```
