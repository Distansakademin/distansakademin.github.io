# Dataplattformens grund

- **Dataplattform**: Samling komponenter för att ta data från källor till konsumenter: ingest, lagring, bearbetning och servering.
- **Ingest**: Tekniker för att ta in data (batch eller stream) — exempel `MQTT`, `Kafka`, HTTP-API.
- **Lagring**: Skillnad mellan data lake (objektlagring såsom `S3`/`ADLS`/`GCS`) och data warehouse (`Redshift`/`BigQuery`/`Synapse`).
- **Bearbetning**: Batch (t.ex. Spark) kontra stream (t.ex. Kafka Streams, Flink) — välj efter SLA och latenskrav.
- **Servering**: API:er, dashboards och modellserving som levererar värde till användare/applikationer.
- **Skalbarhet & governance**: Designera för skalning, säker åtkomst, metadata och spårbarhet.
- **Vidare läsning**: AWS architecture (https://aws.amazon.com/architecture/), Google Cloud architecture (https://cloud.google.com/architecture)