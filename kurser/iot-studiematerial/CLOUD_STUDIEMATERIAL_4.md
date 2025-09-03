# Dataintegration & ETL/ELT

- **ETL vs ELT**: `ETL` = Transformera före lagring; `ELT` = ladda först, transformera i lagret (vanligt i moln-warehouse).
- **Idempotens**: Designa processer så att omkörning inte ger dubbletter — använd nycklar och upserts.
- **Incremental loads**: Hämta bara nya/ändrade rader med `updated_at` eller watermark-state.
- **Schema drift**: Validera och hantera förändrade fält — använd schema registry eller valideringssteg.
- **Felhantering**: Retrier, backoff, dead-letter för felaktiga rader och tydlig loggning för spårbarhet.
- **Verktyg**: dbt (https://www.getdbt.com), Airflow (https://airflow.apache.org), Prefect (https://www.prefect.io) — jämför utifrån behov.