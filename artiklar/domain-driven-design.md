# Domain Driven Design

## Introduktion till Domain Driven Design i C\#

### Vad är Domain Driven Design (DDD)?

Domain Driven Design är en metodik för att designa och strukturera programvara baserat på domänens komplexitet. Istället för att fokusera på tekniska aspekter fokuserar DDD på affärsdomänen, dess entiteter, värdeobjekt, aggregeringar och domäntjänster.

- **Domain**: Det är problemområdet som programvaran ska lösa. Det kan vara bank, e-handel, sjukvård etc.
  
- **Entities**: Dessa är objekt som har en beständig identitet genom deras livscykel. Exempel: Användare, Order, Produkt.
  
- **Value objects**: Dessa representerar deskriptiva aspekter av domänen med ingen konceptuell identitet. Exempel: Pengar, Adress, Datumintervall.
  
- **Aggregates**: Kluster av entiteter och värdeobjekt som behandlas som en enhet för datamodifikation. De har en rotentitet, kallad aggregeringsrot, genom vilken alla externa interaktioner måste ske.
  
- **Services**: Om en viss funktionalitet inte naturligt tillhör en entitet eller ett värdeobjekt, kan den modelleras som en domäntjänst.

### Börja med Ubiquitous Language

Innan du börjar koda är det viktigt att samarbeta med de som driver affären för att skapa en "ubiquitous language" - ett gemensamt språk som används av både utvecklare och icke-utvecklare. Detta säkerställer att alla har en klar förståelse för domänen och dess terminologi.

### Exempel: E-handelsdomän i C\#

Nedan följer ett enkelt exempel på hur man kan modellera en e-handelsdomän med DDD i C#.

```csharp
// Entitet
public class Product
{
    public Guid Id { get; private set; }
    public string Name { get; private set; }
    public Money Price { get; private set; }
    // ... andra metoder och egenskaper
}

// Värdeobjekt
public struct Money
{
    public decimal Amount { get; private set; }
    public string Currency { get; private set; }
    // ... andra metoder och egenskaper
}

// Aggregering
public class Order
{
    public Guid Id { get; private set; }
    private List<OrderLine> _orderLines = new List<OrderLine>();
    public IReadOnlyList<OrderLine> OrderLines => _orderLines.AsReadOnly(); // 
    // ... andra metoder och egenskaper
}

public class OrderLine
{
    public Product Product { get; private set; }
    public int Quantity { get; private set; }
    // ... andra metoder och egenskaper
}
```

Koden ovan definierar flera klasser och en struktur i C#:

1. **Entitet - `Product`**:
    - Detta är en klass som representerar en produkt.
    - `Id` är en unik identifierare för produkten av typen `Guid`.
    - `Name` representerar produktens namn.
    - `Price` är av typen `Money`, vilket är ett värdeobjekt (förklaras nedan).

2. **Värdeobjekt - `Money`**:
    - Detta är en struktur som representerar en summa pengar.
    - `Amount` är den faktiska summan av pengar.
    - `Currency` representerar valutan för den angivna summan, t.ex. "SEK", "USD" etc.
    - Eftersom det är en struktur (och inte en klass), är det ett värdeobjekt, vilket innebär att det jämförs baserat på dess värde snarare än dess identitet, alltså `Amount` och `Currency` istället för exempelvis `Id`.

3. **Aggregering - `Order`**:
    - Detta är en klass som representerar en order.
    - `Id` är en unik identifierare för ordern av typen `Guid`.
    - `_orderLines` är en privat lista som innehåller orderlinjer. Varje orderlinje representerar en produkt och dess kvantitet i ordern.
    - `OrderLines` är en egenskap som returnerar en skrivskyddad version av `_orderLines`-listan. Detta garanterar att listan inte kan ändras direkt utifrån, vilket hjälper till att upprätthålla inkapsling.

4. **`OrderLine`**:
    - Detta är en klass som representerar en rad i en order.
    - `Product` representerar den produkt som beställts.
    - `Quantity` representerar hur många av den produkten som beställts.

## Del 2: Design och Implementering med DDD i C\#

### Aggregeringar och Aggregeringsrötter

En av de viktigaste delarna av DDD är att korrekt identifiera dina aggregeringar och deras rötter. En aggregeringsrot är den primära entiteten genom vilken externa objekt interagerar med aggregeringen.

Aggregering innebär att vi behandlar flera objekt som en enhet. Detta innebär att vi inte kan ändra ett objekt i en aggregering utan att ändra alla andra objekt i samma aggregering. Detta är anledningen till att vi inte kan ändra en `OrderLine` utan att ändra `Order`-objektet som den tillhör.

Exempel: I vårt e-handelssystem kan en `Order` vara en aggregeringsrot, medan `OrderLine` är en del av aggregeringen men inte roten.

```csharp
public class Order
{
    public Guid Id { get; private set; }
    private List<OrderLine> _orderLines = new List<OrderLine>();

    public void AddOrderLine(Product product, int quantity)
    {
        _orderLines.Add(new OrderLine(product, quantity));
    }

    // ... andra metoder och egenskaper
}
```

### Repositories

För att hämta och lagra aggregeringar använder vi ofta ett mönster som kallas för Repository. Ett repository är en källa för att hämta och lagra aggregeringar. Det är en abstraktion som isolerar domänlagret från det yttersta lagret (t.ex. en webbapplikation eller ett API).

```csharp
public interface IOrderRepository
{
    Order GetById(Guid id);
    void Save(Order order);
}
```

### Services (Applikationstjänster)

Applikationstjänster fungerar som en bro mellan din domän och det yttersta lagret (t.ex. en webbapplikation eller en API). De orkestrerar hur domänen används.

```csharp
public class OrderService
{
    private readonly IOrderRepository _orderRepository;
    private readonly DiscountService _discountService;

    public OrderService(IOrderRepository orderRepository, DiscountService discountService)
    {
        _orderRepository = orderRepository;
        _discountService = discountService;
    }

    public void PlaceOrder(Guid orderId)
    {
        var order = _orderRepository.GetById(orderId);
        var discount = _discountService.CalculateDiscount(order);
        order.ApplyDiscount(discount);
        _orderRepository.Save(order);
    }
}
```

## Bokningssystem för hotell

Här är en DDD-baserad klass-struktur för ett enkelt bokningssystem för hotell med beskrivningar för varje klass och dess syfte inom systemet.

### `Models`

#### `Guest` (Entitet)

- **Syfte**: Representerar en gäst som kan boka ett rum.
- **Egenskaper**: `Id`, `Name`, `Email`.
- **Metoder**: `UpdateContactDetails(string name, string email)`.

#### `Room` (Entitet)

- **Syfte**: Representerar ett hotellrum.
- **Egenskaper**: `Id`, `Number`, `Type` (t.ex. enkelrum, dubbelrum).
- **Metoder**: `ChangeType(string type)`.

#### `Booking` (Aggregeringsrot)

- **Syfte**: Hanterar bokningsinformation.
- **Egenskaper**: `Id`, `Guest`, `Room`, `StartDate`, `EndDate`.
- **Metoder**: `UpdateDates(DateTime start, DateTime end)`, `AssignRoom(Room room)`.

#### `BookingPeriod` (Värdeobjekt)

- **Syfte**: Representerar en tidsperiod för en bokning.
- **Egenskaper**: `StartDate`, `EndDate`.

#### `BookingService`

- **Syfte**: Orkestrerar bokningsprocessen.
- **Metoder**: `CreateBooking(Guest guest, BookingPeriod period)`, `ChangeBookingDates(Guid bookingId, BookingPeriod newPeriod)`.

#### `BookingPolicyService`

- **Syfte**: Avgör om en bokning kan göras baserat på vissa affärsregler.
- **Metoder**: `CanBook(Guest guest, BookingPeriod period)`.

### Repositories

#### `IBookingRepository`

- **Syfte**: Ger åtkomst till bokningsaggregeringar.
- **Metoder**: `GetById(Guid id)`, `Save(Booking booking)`, `FindAllByGuest(Guest guest)`.

#### `IRoomRepository`

- **Syfte**: Ger åtkomst till rum-entiteter.
- **Metoder**: `GetAvailableRooms(BookingPeriod period)`, `GetById(Guid id)`.

### Data Access Layer (DAL)

#### `DatabaseConnection`

- **Syfte**: Hanterar datakällor.
- **Metoder**: `OnConfiguring(DbContextOptionsBuilder optionsBuilder)`.

## Sammanfattning

DDD Går alltså en nivå djupare än Services-Repositories-mönstret genom att använda Repositories för att hämta och lagra aggregeringar och Services för att orkestrera domänen. Data Access Layer (DAL) blir istället det lager som hanterar databasanslutningen och är inte en del av domänen.
