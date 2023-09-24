# Guide: Driftsätta en Java Spring Boot-applikation med Maven på AWS Elastic Beanstalk

Elastic Beanstalk (EB) är en PaaS (Platform as a Service) lösning från AWS som automatiskt hanterar distribution, skalning och drift av applikationer. Här är en steg-för-steg guide för att driftsätta en Spring Boot-applikation med Maven på EB.

## Steg 1: Förbered din applikation

1. **Spring Boot-applikation**: Se till att du har en Spring Boot-applikation byggd med Maven. Om du inte redan har en, kan du generera en med Spring Initializr eller genom att klonera ett exempel från GitHub.

2. **Packaging**: Ändra `packaging` till `jar` i din `pom.xml`:

    ```xml
    <packaging>jar</packaging>
    ```

3. **Portkonfiguration**: Elastic Beanstalk använder port 5000 som standard för Java-applikationer. För att säkerställa att din Spring Boot-applikation lyssnar på rätt port, kan du konfigurera den med följande i `src/main/resources/application.properties`:

    ```properties
    server.port=5000
    ```

## Steg 2: Bygg din applikation

Kör följande kommando i ditt projektets rotkatalog för att bygga applikationen med Maven:

```bash
mvn clean package
```

Efter byggprocessen kommer du att ha en `.jar` fil i `target` katalogen, som kan deployas till Elastic Beanstalk.

## Steg 3: Förbered AWS

1. **AWS CLI**: Installera [AWS Command Line Interface (CLI)](https://aws.amazon.com/cli/) om du inte redan har den.

2. **Konfigurera AWS CLI**: Kör följande kommando och följ instruktionerna:

    ```bash
    aws configure
    ```

    Ange dina AWS access keys, region, och önskat output format.

3. **Installera EB CLI**: Elastic Beanstalk Command Line Interface (EB CLI) är ett verktyg för att interagera med Elastic Beanstalk direkt från terminalen. Följ [officiella instruktionerna](https://docs.aws.amazon.com/elasticbeanstalk/latest/dg/eb-cli3-install.html) för att installera det.

## Steg 4: Skapa och konfigurera EB-applikation

1. **Initiera Elastic Beanstalk**:
    Gå till din applikations rotkatalog och kör:

    ```bash
    eb init
    ```

    - Välj den region där du vill deploya din applikation.
    - Välj "Java" när du blir tillfrågad om plattform.
    - Skapa en ny applikation eller använd en befintlig.

2. **Skapa en miljö**:

    ```bash
    eb create my-springboot-env
    ```

    Detta kommando kommer att skapa en ny miljö inom din EB-applikation och börja processen att driftsätta din Spring Boot-applikation.

## Steg 5: Uppdatera din applikation

När du gjort förändringar i din kod och vill uppdatera din applikation på Elastic Beanstalk:

1. Bygg din applikation igen:

    ```bash
    mvn clean package
    ```

2. Deploya uppdateringen:

    ```bash
    eb deploy
    ```

## Steg 6: Övervaka applikationen

Elastic Beanstalk erbjuder en övervakningsdashboard som innehåller information om ditt applikationstillstånd, begärandehastighet, etc.

1. För att öppna EB-konsolen direkt från din terminal, kör:

    ```bash
    eb console
    ```

2. På konsolen kan du se grafisk representation av ditt applikationstillstånd och diverse metriker.

3. Sätt upp varningar via Amazon CloudWatch för att bli meddelad om kritiska händelser.

## Steg 7: Konfigurera en databas

1. På EB-konsolen, under din applikations miljö, välj "Konfiguration".

2. Under "Databas", klicka på "Ändra" och välj önskad databas (t.ex. Amazon RDS).

3. Följ stegen för att konfigurera databasinstans, användarnamn, lösenord, etc.

4. När databasen är skapad och associerad med din Elastic Beanstalk-miljö, kommer AWS att sätta miljövariabler som din Spring Boot-applikation kan använda för att ansluta till databasen.

## Steg 8: Hantera säkerhet

1. **IAM roller**: Se till att din Elastic Beanstalk-applikation har rätt IAM-roll för att interagera med andra AWS-tjänster.

2. **Säkerhetsgrupper**: Konfigurera säkerhetsgrupper för att begränsa inkommande och utgående trafik till din applikation och databas.

3. **SSL/TLS**: Aktivera HTTPS för din applikation genom att lägga till ett SSL-certifikat. Du kan antingen använda AWS Certificate Manager eller ladda upp ditt eget certifikat.

## Steg 9: Skalning och optimering

1. Under "Konfiguration" på EB-konsolen, kan du justera inställningar för automatisk skalning, vilket gör att din applikation kan hantera fluktuerande trafik.

2. Använd Elastic Load Balancer (ELB) för att distribuera inkommande trafik till flera instanser av din applikation.

3. Aktivera instansoptimeringar baserat på dina prestandakrav och budget.

## Steg 10: Rengöring

När du är klar med din applikation eller vill avsluta testning:

1. Radera miljön:

    ```bash
    eb terminate my-springboot-env
    ```

2. Glöm inte att även rensa upp eventuella databaser, S3-buckets, etc. för att undvika extra kostnader.
