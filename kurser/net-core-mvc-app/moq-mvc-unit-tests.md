# Enhetstester av MVC Controller med Entity Framework och Moq

Denna guide visar hur du enhetstestar en MVC CRUD-controller som använder Entity Framework. I guiden skapar vi en mockad DbContext och lägger till några sånger i databasen.

## Steg 1: Förberedelser

Guiden förutsätter att du har ett MVC-projekt uppsatt med en DbContext och en modell. Om du inte har det kan du skapa ett nytt projekt och lägga till en modell och en DbContext. I exemplet nedan har vi en modell som heter `Song` och en DbContext som heter `ApplicationDbContext`.

### `Song.cs`

```csharp
public class Song
{
    public int Id { get; set; }
    public string Title { get; set; }
    public string Artist { get; set; }
}
```

Guiden förutsätter också att du har ett NUnit testprojekt i samma solution som MVC-projektet. Om du inte har det kan du skapa ett nytt projekt och installera paketet `NUnit` från NuGet. Du behöver också installera paketet `EntityFrameworkCore.Testing.Moq` för att kunna mocka DbContexten.

## Steg 2: TestFixture och SetUp

I testprojektet skapar vi en klass som heter `SongsControllerTests`. Vi använder attributet `TestFixture` för att indikera att klassen innehåller tester. Vi använder också attributet `SetUp` för att indikera att metoden ska köras innan varje test.

### `SongsControllerTests.cs`

```csharp
[TestFixture]
public class SongsControllerTests
{
    private ApplicationDbContext mockContext;
    private SongsController controller;

    [SetUp]
    public void SetUp()
    {
        // Skapa en mockad DbContext
        mockContext = Create.MockedDbContextFor<ApplicationDbContext>();

        // Konfigurera mockad DbSet
        var songs = new List<Song>
        {
            new Song { Id = 1, Title = "Song 1", Artist = "Artist 1" },
            new Song { Id = 2, Title = "Song 2", Artist = "Artist 2" }
        };

        // Använd SetupDbSet för att konfigurera DbSet
        mockContext.Set<Song>().AddRange(songs);
        mockContext.SaveChanges();

        mockContext.ChangeTracker.Clear();

        // Skapa controller med mockad DbContext
        controller = new SongsController(mockContext);
    }

    // ...
}
```

I denna kod skapar vi en mockad DbContext med hjälp av metoden `Create.MockedDbContextFor`. Vi använder också metoden `SetupDbSet` för att konfigurera en mockad DbSet. Vi lägger till två sånger i databasen och sparar ändringarna. Vi rensar också DbContextens ChangeTracker för att undvika problem med att entiteter är i olika states.

## Steg 3: Testa Index-metoden

I detta steg testar vi Index-metoden i SongsController. Vi använder attributet `Test` för att indikera att metoden är ett test. Vi använder också attributet `async` för att indikera att metoden är asynkron, alltså att den kan köras parallellt med andra tester.

### `SongsControllerTests.cs`

```csharp
[Test]
public async Task Index_ReturnsViewResult_WithListOfSongs()
{
      // Act
      var result = await controller.Index();

      // Assert
      Assert.That(result, Is.InstanceOf<ViewResult>());

      var viewResult = result as ViewResult;
      var model = viewResult.Model;
      Assert.That(model, Is.InstanceOf<List<Song>>());

      var songList = model as List<Song>;
      Assert.That(songList.Count, Is.EqualTo(2));
}
```

I detta test verifierar vi att Index-metoden returnerar en ViewResult med en lista av sånger. Vi använder `Is.InstanceOf` för att verifiera att result är av typen ViewResult. Vi använder också `Is.EqualTo` för att verifiera att listan innehåller två sånger. Detta test kommer att misslyckas om Index-metoden inte returnerar en ViewResult eller om listan inte innehåller två sånger.

## Steg 4: Testa Create-metoden

Create består av två metoder: en GET-metod för att visa formuläret och en POST-metod för att skapa sången. Vi börjar med att testa GET-metoden.

### `SongsControllerTests.cs`

```csharp
[Test]
public void Create_ReturnsViewResult()
{
    // Act
    var result = controller.Create();

    // Assert
    Assert.IsInstanceOf<ViewResult>(result);
}
```

Detta test verifierar att Create-metoden returnerar en ViewResult. Vi använder metoden `IsInstanceOf` för att verifiera att result är av typen ViewResult.

### `SongsControllerTests.cs`

```csharp
[Test]
public async Task Create_Post_ReturnsRedirectToActionResult_WhenModelStateIsValid()
{
    // Arrange
    var newSong = new Song { Title = "New Song", Artist = "New Artist" };

    // Act
    var result = await controller.Create(newSong);

    // Assert
    Assert.IsInstanceOf<RedirectToActionResult>(result);
    var redirectToActionResult = result as RedirectToActionResult;
    Assert.That(redirectToActionResult.ActionName, Is.EqualTo("Index"));
}

[Test]
public async Task Create_Post_ReturnsViewResult_WhenModelStateIsInvalid()
{
    // Arrange
    controller.ModelState.AddModelError("Error", "Model error");
    var newSong = new Song { Title = "New Song", Artist = "New Artist" };

    // Act
    var result = await controller.Create(newSong);

    // Assert
    Assert.IsInstanceOf<ViewResult>(result);
}
```

Detta test verifierar att Create-metoden returnerar en ViewResult när ModelState är ogiltig, alltså när sången är ogiltig så visas formuläret igen. Vi använder metoden `AddModelError` för att lägga till ett fel i ModelState.

Vi verifierar också att Create-metoden returnerar en RedirectToActionResult när ModelState är giltig. Vi använder metoden `IsInstanceOf` för att verifiera att result är av typen RedirectToActionResult. Detta betyder att Create-metoden redirectar till Index-metoden när sången har ska skapas.

## Steg 5: Testa Edit-metoden

Edit består också av två metoder: en GET-metod för att visa formuläret och en POST-metod för att uppdatera sången. Vi börjar med att testa GET-metoden.

### `SongsControllerTests.cs`

```csharp
[Test]
public async Task Edit_Get_ReturnsNotFoundResult_WhenIdIsNull()
{
      // Act
      var result = await controller.Edit(null);

      // Assert
      Assert.IsInstanceOf<NotFoundResult>(result);
}

[Test]
public async Task Edit_Get_ReturnsNotFoundResult_WhenSongDoesNotExist()
{
      // Act
      var result = await controller.Edit(99);

      // Assert
      Assert.IsInstanceOf<NotFoundResult>(result);
}

[Test]
public async Task Edit_Get_ReturnsViewResult_WithSong()
{
      // Arrange
      var song = new Song { Id = 3, Title = "Test Song", Artist = "Test Artist" };
      mockContext.Set<Song>().Add(song);
      mockContext.SaveChanges();

      // Act
      var result = await controller.Edit(1);

      // Assert
      Assert.IsInstanceOf<ViewResult>(result);
      var viewResult = result as ViewResult;
      Assert.IsInstanceOf<Song>(viewResult.Model);
      var model = viewResult.Model as Song;
      Assert.That(model.Id, Is.EqualTo(1));
}
```

Detta test verifierar att Edit-metoden returnerar en ViewResult med en sång när id är giltigt, alltså när sången finns i databasen så visas formuläret. Vi använder metoden `IsInstanceOf` för att verifiera att result är av typen ViewResult. Vi använder också `IsInstanceOf` för att verifiera att model är av typen Song. Vi använder också `Is.EqualTo` för att verifiera att sångens id är 1.

Vi verifierar också att Edit-metoden returnerar en NotFoundResult när id är null eller när sången inte finns i databasen.

### `SongsControllerTests.cs`

```csharp
[Test]
public async Task Edit_Post_ReturnsNotFoundResult_WhenIdDoesNotMatchSongId()
{
      // Arrange
      var song = new Song { Id = 1, Title = "Test Song", Artist = "Test Artist" };

      // Act
      var result = await controller.Edit(2, song);

      // Assert
      Assert.IsInstanceOf<NotFoundResult>(result);
}

[Test]
public async Task Edit_Post_ReturnsRedirectToActionResult_WhenModelStateIsValid()
{
      // Arrange
      var song = new Song { Id = 1, Title = "Updated Song", Artist = "Updated Artist" };

      // Act
      var result = await controller.Edit(1, song);

      // Assert
      Assert.IsInstanceOf<RedirectToActionResult>(result);
      var redirectToActionResult = result as RedirectToActionResult;
      Assert.That(redirectToActionResult.ActionName, Is.EqualTo("Index"));
}

[Test]
public async Task Edit_Post_ReturnsViewResult_WhenModelStateIsInvalid()
{
      // Arrange
      controller.ModelState.AddModelError("Error", "Model error");
      var song = new Song { Id = 1, Title = "Updated Song", Artist = "Updated Artist" };

      // Act
      var result = await controller.Edit(1, song);

      // Assert
      Assert.IsInstanceOf<ViewResult>(result);
}
```

Detta test verifierar att Edit-metoden returnerar en ViewResult när ModelState är ogiltig, alltså när sången är ogiltig så visas formuläret igen. Vi använder metoden `AddModelError` för att lägga till ett fel i ModelState.

Vi verifierar också att Edit-metoden returnerar en RedirectToActionResult när ModelState är giltig. Vi använder metoden `IsInstanceOf` för att verifiera att result är av typen RedirectToActionResult. Detta betyder att Edit-metoden redirectar till Index-metoden när sången har uppdaterats.

Vi verifierar också att Edit-metoden returnerar en NotFoundResult när id inte matchar sångens id.

## Steg 6: Testa Delete-metoden

Delete består också av två metoder: en GET-metod för att visa formuläret och en POST-metod för att radera sången. Vi börjar med att testa GET-metoden.

### `SongsControllerTests.cs`

```csharp
[Test]
public async Task Delete_Get_ReturnsNotFoundResult_WhenIdIsNull()
{
    // Act
    var result = await controller.Delete(null);

    // Assert
    Assert.IsInstanceOf<NotFoundResult>(result);
}

[Test]
public async Task Delete_Get_ReturnsNotFoundResult_WhenSongDoesNotExist()
{
    // Act
    var result = await controller.Delete(99);

    // Assert
    Assert.IsInstanceOf<NotFoundResult>(result);
}

[Test]
public async Task Delete_Get_ReturnsViewResult_WithSong()
{
    // Arrange
    var song = new Song { Id = 3, Title = "Test Song", Artist = "Test Artist" };
    mockContext.Set<Song>().Add(song);
    mockContext.SaveChanges();

    // Act
    var result = await controller.Delete(1);

    // Assert
    Assert.IsInstanceOf<ViewResult>(result);
    var viewResult = result as ViewResult;
    Assert.IsInstanceOf<Song>(viewResult.Model);
    var model = viewResult.Model as Song;
    Assert.That(model.Id, Is.EqualTo(1));
}
```

Detta test verifierar att Delete-metoden returnerar en ViewResult med en sång när id är giltigt, alltså när sången finns i databasen så visas formuläret. Vi använder metoden `IsInstanceOf` för att verifiera att result är av typen ViewResult. Vi använder också `IsInstanceOf` för att verifiera att model är av typen Song. Vi använder också `Is.EqualTo` för att verifiera att sångens id är 1.

Vi verifierar också att Delete-metoden returnerar en NotFoundResult när id är null eller när sången inte finns i databasen.

### `SongsControllerTests.cs`

```csharp
[Test]
public async Task DeleteConfirmed_ReturnsRedirectToActionResult()
{
    // Arrange
    var song = new Song { Id = 3, Title = "Test Song", Artist = "Test Artist" };
    mockContext.Set<Song>().Add(song);
    mockContext.SaveChanges();

    // Act
    var result = await controller.DeleteConfirmed(1);

    // Assert
    Assert.IsInstanceOf<RedirectToActionResult>(result);
    var redirectToActionResult = result as RedirectToActionResult;
    Assert.That(redirectToActionResult.ActionName, Is.EqualTo("Index"));
}
```

Detta test verifierar att DeleteConfirmed-metoden returnerar en RedirectToActionResult när sången har raderats. Vi använder metoden `IsInstanceOf` för att verifiera att result är av typen RedirectToActionResult. Detta betyder att DeleteConfirmed-metoden redirectar till Index-metoden när sången har raderats.

## Steg 7: Testa Exception Handling

I detta steg testar vi att vår controller hanterar exceptions korrekt. Vi börjar med att testa Index-metoden och testar att den kastar ett Exception när det uppstår ett fel.

### `SongsControllerTests.cs`

```csharp
[Test]
public async Task Index_ThrowsException()
{
    // Arrange
    mockContext.Dispose();

    // Act & Assert
    Assert.ThrowsAsync<ObjectDisposedException>(() => controller.Index());
}
```

Detta test verifierar att Index-metoden kastar ett Exception när DbContexten har blivit disposed. Vi använder metoden `Assert.ThrowsAsync` för att verifiera att metoden kastar ett Exception.

Vi testar också att Create-metoden kastar ett Exception när det uppstår ett fel.

### `SongsControllerTests.cs`

```csharp
[Test]
public async Task Create_ThrowsException()
{
    // Arrange
    mockContext.Dispose();
    var newSong = new Song { Title = "New Song", Artist = "New Artist" };

    // Act & Assert
    Assert.ThrowsAsync<ObjectDisposedException>(() => controller.Create(newSong));
}
```

Vi kan testa alla metoder i SongsController i ett enda test genom att använda metoden `Assert.Multiple`. Vi använder metoden `Assert.ThrowsAsync` för att verifiera att metoden kastar ett Exception.

### `SongsControllerTests.cs`

```csharp
[Test]
public void Controller_ThrowsException()
{
    // Arrange
    mockContext.Dispose();
    var newSong = new Song { Id = 1, Title = "New Song", Artist = "New Artist" };

    // Act & Assert
    Assert.Multiple(() =>
    {
        Assert.ThrowsAsync<ObjectDisposedException>(() => controller.Index());
        Assert.ThrowsAsync<ObjectDisposedException>(() => controller.Create(newSong));
        Assert.ThrowsAsync<ObjectDisposedException>(() => controller.Edit(1));
        Assert.ThrowsAsync<ObjectDisposedException>(() => controller.Edit(1, newSong));
        Assert.ThrowsAsync<TargetInvocationException>(() => controller.Delete(1));
        Assert.ThrowsAsync<ObjectDisposedException>(() => controller.DeleteConfirmed(1));
        Assert.ThrowsAsync<TargetInvocationException>(() => controller.Details(1));
    });
}
```

Detta test verifierar att alla metoder i SongsController kastar ett Exception när DbContexten har blivit disposed. Vi använder metoden `Assert.Multiple` för att köra flera assertions i ett test. Alla assertions kommer att köras även om en av dem misslyckas. Samtliga metoder i SongsController kastar ett `ObjectDisposedException` när DbContexten har blivit disposed förutom tre:

1. `Create`-metoden utan parametrar, alltså sidan som visar formuläret, kastar inte ett Exception när DbContexten har blivit disposed. Detta beror på att den inte använder DbContexten.
2. `Delete`-metoden, som visar en bekräftelsesida, kastar ett `TargetInvocationException` när DbContexten har blivit disposed.
3. `Details`-metoden, som visar detaljer om en sång, kastar ett `TargetInvocationException` när DbContexten har blivit disposed.

`Delete`- och `Details`-metoden kastar ett `TargetInvocationException` eftersom de använder en `FirstOrDefaultAsync` på DbContexten. Detta beror på att `FirstOrDefaultAsync` kastar ett `TargetInvocationException` när DbContexten har blivit disposed.
