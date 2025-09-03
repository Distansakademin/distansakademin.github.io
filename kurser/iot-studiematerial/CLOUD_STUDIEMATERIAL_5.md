# Datakällor för IoT

- **Sensorer/edge**: Små enheter skickar tidserie-data; välj lämplig transport och format.
- **MQTT**: Låg-latens pub/sub för IoT — se Eclipse Paho och Mosquitto (https://mqtt.org).
- **REST/API**: Vanligt för konfig och batchhämtning; hantera paginering och rate limits.
- **Filer (CSV/JSON)**: Vanligt vid batch; spara alltid en råkopie i lake för reproducerbarhet.
- **Meddelandeköer**: Kafka eller AWS Kinesis för hög genomströmning och persistens.
- **Praktiskt tips**: Logga `device_id` + `timestamp` som naturlig nyckel och spara metadata om enheter i referenstabell.