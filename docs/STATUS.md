# Status

## P00 · 22 november 2026

Macro Analysis fick sin första dokumenterade arbetsgrund på `main` med `origin` satt till `https://github.com/block-dev-mats/Macro-Analysis.git`. Arbetsmappen saknade Git-historik vid start och GitHub-repot svarade utan Git-referenser. Den publicerade historiken finns på GitHub. [Macro Analysis](https://github.com/block-dev-mats/Macro-Analysis)

Projektbeskrivning, måttförslag, arbetsregler och lokal mätlogg är etablerade. P00 innehåller ingen Pine-kod, testsvit eller CI-konfiguration. TradingView-kompilering och visuell verifiering börjar med indikatorn.

## Öppet

P01 behöver ta ställning till måttförslagen för kort historik och identifierade datagap. Swing-definitionen, SMA:s senare fördelnings- och stöd/motståndsmått och veckovis visning återstår att definiera eller verifiera. [Måttdefinitioner](METRICS.md)

## P01

Bygg en första kompilerbar Pine Script v6-indikator på 1D. Visa prisavkastning sedan första giltiga stängning och CAGR med mätperiod, aktuell och max drawdown samt procentuell distans till SMA 200D och andel jämförbara dagar ovanför SMA. Använd en diskret SMA-overlay och den kompakta tabellen som beskrivs i projektbeskrivningen.

Kontrollera grundmåtten mot syntetiska facit, inklusive kort historik och återhämtning från en drawdown. Kontrollera att obekräftade dagsbarer lämnar redovisade resultat oförändrade och att chartintervall utanför stödet får tydlig status. Kompilera och granska indikatorn i TradingView där åtkomst finns. [Projektbeskrivning](PROJECT_BRIEF.md)
