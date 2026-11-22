# Status

## P01

[Macro Analysis i Pine Script v6](../indicators/macro-analysis.pine) visar prisavkastning, CAGR, mätperiod, aktuell och maximal drawdown, distans till SMA 200D samt andel och antal jämförbara dagar. SMA-linjen kan döljas i indikatorns inställningar. P01 stöder standardgrafer på exakt 1D. [Måttdefinitioner](METRICS.md#beslutat)

### Verifiering

Indikatorn kompilerades och kördes i TradingView Desktop. På SXR8 växlade **Show SMA 200D** linjen medan panelen behöll sina värden. Observationerna avser laddad historik den 22 november 2026.

| Chart | Observerat |
| --- | --- |
| `XETR_DLY:SXR8` · 1D · SEK | 2010-09-21 till 2026-11-20, 5 904 kalenderdagar. Prisavkastning 797,60 %, CAGR 14,54 %, aktuell DD −8,26 %, max DD −31,66 %. SMA 200D 7 564,29 i datafönstret, 2,51 % över SMA och 85,28 % av 3 865 jämförbara dagar över SMA. Utdelningsjustering var av. |
| `XETR_DLY:SXR8` · 1W | Panelen visade **Use a 1D chart**. Macro Analysis visade inga mått och ingen SMA-linje. |
| `BINANCE:PUMPU` · 1D | 2026-08-26 till 2026-11-21, 87 kalenderdagar. Prisavkastning −51,80 %. Båda SMA-måtten visade `N/A` och ingen SMA-linje ritades. Dagsbaren den 22 november var öppen. |
| `BINANCE:BTCUSDT` · 1D | Panelen slutade 2026-11-21 och behöll sina värden när livepriset rörde sig från 60 355,44 till 60 302,97 USDT. Andel dagar över SMA var 52,75 % av 3 185 jämförbara dagar. |

En tillfällig Pine-testvariant matade indikatorns beräkningslogik med [syntetiska stängningar och sessionsdatum](METRICS.md#deterministiska-p01-exempel). Kontrollerna passerade för 46,41 % prisavkastning och 10,00 % CAGR, återhämtning med 0 % aktuell DD och −25 % max-DD, SMA-värdena 100, 100,05 och 100 samt en andel dagar över SMA på 1/3. Kontrollen omfattade även enstaka och sammanfallande datum, `na`, noll och negativa stängningar, 199 och 200 giltiga barer i rad, lika stängning och SMA vid decimalpriser samt en simulerad öppen bar. Ett ogiltigt senaste pris visade `N/A` för aktuella mått och lämnade de historiska värdena tillgängliga.

En verklig övergång från öppen till stängd dagsbar följdes inte. Täckningen är begränsad till den laddade prisserien. Luckor där datakällan saknar en hel bar kan påverka resultaten.

### Nästa steg

Minsta P02 är prisavkastning för **1 år** på 1D, med faktiska referensdatum och `N/A` när ettårsunderlaget saknas. Verifiera referensval runt helger och skottdagar. Övriga fasta perioder, veckovis visning, episodmått och avancerad SMA-statistik ligger kvar som metodförslag. [Öppna måttförslag](METRICS.md#förslag)

## P00 · 22 november 2026

Projektgrund med arbetsregler, produktmål, måttförslag och lokal mätlogg. [P00 på GitHub](https://github.com/block-dev-mats/Macro-Analysis/commit/38bf755704f9281827d9c34d84cc5523684f13e1)
