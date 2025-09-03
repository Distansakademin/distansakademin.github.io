# Lagring och databasval

- **Filer vs DB**: Objektlagring (`S3`) för rådata, relations- eller kolumnlager för analys och API-svar.
- **NoSQL**: `MongoDB`/`DynamoDB` för flexibla dokument och snabb lookup.
- **Relational**: `PostgreSQL`/`MySQL` för transaktionell logik och kompletta SQL-möjligheter.
- **Databas i containers**: Kör testinstanser lokalt med `docker-compose` men planera för managed-tjänster i produktion.
- **Integration**: Använd connection pooling och bulk-inserts/upserts för prestanda.