# Transformation och analys (utan kodexempel)

- **Rensning och typsättning**: Säkerställ datatyper, tidszoner och rimlighetskontroller (t.ex. temperaturintervall).
- **Normalisering**: Standardisera kolumnnamn och formater (t.ex. `device_id`, `ts`).
- **Aggrering & resampling**: Sammanfatta tidserier per minut/timme enligt affärsbehov.
- **Feature engineering**: Skapa rullande fönster, differenser eller flaggor för saknade värden.
- **Verktyg & resurser**: `pandas` docs (https://pandas.pydata.org), Parquet-format (https://parquet.apache.org)