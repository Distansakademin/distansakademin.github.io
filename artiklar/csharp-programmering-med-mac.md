# Programmera C# på en Mac med VS Code

Att komma igång med att koda C# och ASP.NET-applikationer på en Mac med Visual Studio Code (VS Code) är ett spännande projekt som öppnar upp för en värld av utvecklingsmöjligheter. Här är en enkel guide för att hjälpa dig igång steg för steg:

## Guide

### 1. Installera .NET SDK

Först och främst behöver du .NET Software Development Kit (SDK), som inkluderar allt du behöver för att utveckla och köra .NET-applikationer.

- Gå till [.NET officiella hemsida](https://dotnet.microsoft.com/download) och ladda ner .NET SDK för macOS.
- Följ installationsinstruktionerna på skärmen.

### 2. Installera Visual Studio Code

Visual Studio Code är en kraftfull och lättviktig kodeditor som stödjer C# och ASP.NET utveckling genom tillägg.

- Ladda ner och installera VS Code från [den officiella hemsidan](https://code.visualstudio.com/Download).
- Följ installationsinstruktionerna på skärmen.

### 3. Installera C#-tillägg för VS Code

För att effektivt kunna arbeta med C# i VS Code, behöver du installera C#-tillägget.

- Starta VS Code.
- Gå till Extensions-vy genom att klicka på Extensions-ikonen i sidofältet eller genom att trycka på `Cmd+Shift+X`.
- Sök efter "C#" och välj C#-tillägget från Microsoft.
- Klicka på "Install".

### 4. Skapa en ny ASP.NET Core-applikation

Nu när du har allt installerat är det dags att skapa en ny ASP.NET Core-applikation.

- Öppna terminalen.
- Navigera till mappen där du vill skapa ditt projekt.
- Kör kommandot `dotnet new webapp -o MinAspNetApp` för att skapa en ny ASP.NET Core Web Application. `MinAspNetApp` är mappnamnet för ditt nya projekt.
- Navigera in i din projektmap med `cd MinAspNetApp`.

### 5. Öppna projektet i VS Code

- Kör `code .` inuti din projektmap för att öppna VS Code med ditt projekt.
  
### 6. Utforska och kör din applikation

- När du har öppnat ditt projekt i VS Code, kan du utforska de skapade filerna.
- För att köra din applikation, öppna terminalen i VS Code (`Terminal` -> `New Terminal`) och kör kommandot `dotnet run`.
- Öppna en webbläsare och navigera till adressen som visas i terminalen (vanligtvis `http://localhost:5000`).

### 7. Utforska mer och börja koda

Nu när du har din första ASP.NET Core-applikation upp och körande, är det dags att börja utforska och lära dig mer. Använd dokumentationen på [.NETs officiella hemsida](https://docs.microsoft.com/en-us/aspnet/core/?view=aspnetcore-5.0) för att lära dig mer om ASP.NET Core och dess funktioner. Lycka till med din kodningsresa!

---

## Testa din applikation

Efter att ha fått din första ASP.NET Core-applikation att köra, är det dags att testa att allt fungerar som det ska genom att skapa en enkel webbsida som visar ett meddelande.

### Testa din applikation med en enkel webbsida

1. **Skapa en ny Razor-sida:** Razor är ett markeringsspråk för att skapa dynamiskt genererade webbsidor med C#.

   - I din projektmap, navigera till `Pages`-mappen.
   - Skapa en ny fil och namnge den `Hello.cshtml`.
   - Öppna `Hello.cshtml` i VS Code och lägg till följande kod:

     ```html
     @page
     @model MinAspNetApp.Pages.HelloModel
     @{
         ViewData["Title"] = "Hello Page";
     }

     <h2>Hello, ASP.NET!</h2>
     <p>Welcome to your first Razor page.</p>
     ```

2. **Skapa en modell för sidan:** För varje Razor-sida behövs en modell. Modellen hanterar datan som sidan visar.

   - Skapa en ny fil i `Pages`-mappen och namnge den `Hello.cshtml.cs`.
   - Öppna `Hello.cshtml.cs` i VS Code och lägg till följande C#-kod:

     ```csharp
     using Microsoft.AspNetCore.Mvc.RazorPages;

     namespace MinAspNetApp.Pages
     {
         public class HelloModel : PageModel
         {
             public void OnGet()
             {
                 
             }
         }
     }
     ```

3. **Kör din applikation igen:**

   - Använd terminalen i VS Code och kör kommandot `dotnet run` igen.
   - När applikationen är igång, öppna en webbläsare och navigera till `http://localhost:5000/Hello`.

Nu bör du se en enkel webbsida som säger "Hello, ASP.NET!" tillsammans med meddelandet "Welcome to your first Razor page." Detta bekräftar att din ASP.NET Core-applikation fungerar och kan visa dynamiskt innehåll genom Razor-sidor.

### Utforska vidare

Från denna punkt kan du börja utforska mer komplex funktionalitet, såsom att arbeta med databaser, skapa API:er, och lägga till användarautentisering. ASP.NET Core är ett kraftfullt ramverk för att bygga både webbsidor och webbapplikationer, så ta dig tid att utforska vad det har att erbjuda. Glöm inte att den officiella dokumentationen är en utmärkt resurs för att lära dig mer och lösa eventuella problem som uppstår under ditt lärande.
