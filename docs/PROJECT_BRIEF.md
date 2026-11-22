# Projektbeskrivning

Macro Analysis ska bli ett eget analysverktyg för `block-dev-mats` vid långsiktigt investeringsurval. Indikatorn ska ge en statistisk översikt över en TradingView-symbol med tillräcklig kurshistorik, till exempel ett index, en ETF eller en fond.

Öppna symbolen på dagschart, kontrollera vilken historik som täcks och läs av utvecklingen. Byt symbol för nästa jämförelse. Ta hänsyn till skillnader i kurshistorik, sessionskalender, justeringar, datagap, valuta och prissättning när resultaten jämförs. [Datakrav](METRICS.md#beslutat)

## Produktens tre delar

- **Performance** visar prisavkastning från första giltiga mätpunkt, CAGR och avkastning över 1, 3, 5 och 10 år där underlaget räcker. Mätperiod och luckor i täckningen framgår.
- **Rallies & Drawdowns** beskriver storlek, frekvens och varaktighet för upp- och nedgångsepisoder. Drawdown från historiska toppar redovisas med aktuellt och största historiskt värde, antalet separata djupa nedgångar och tiden till botten respektive återhämtning.
- **MA Behavior** börjar med SMA 200D. Visa aktuell distans, andel dagar över och under samt typiska och extrema avstånd på vardera sidan. Objektiva stöd- och motståndstester hör till en senare fas.

## Gränssnitt och prioriteringar

Visa SMA som en diskret overlay och samla resultaten i en kompakt tabell med **Performance**, **Drawdowns** och **MA Behavior**. Använd korta måttnamn och få inställningar. Lägg definitioner som behövs vid tolkning i tooltips. Mätperiod, otillräcklig historik och begränsat chartstöd ska gå att se direkt. Håll chartytan fri från täta etiketter, stora markeringar och godtyckliga rankingpoäng i standardläget.

Grunden är en korrekt 1D-vy. Målet är en begriplig översikt även på 1W när dagsberäkningarna kan visas där med bibehållen korrekthet.

## Faser

1. **P00** etablerar projektgrunden.
2. **P01** bygger den första användbara 1D-versionen med grundmått. [P01:s avgränsning](STATUS.md#p01)
3. **Fortsättning** utökar täckningen med fler perioder, detaljerade episoder och fördelningar för SMA-distans. Veckovis visning förutsätter verifierad överensstämmelse med 1D för samma avslutade mätperiod. Stöd- och motståndsanalys förutsätter objektiva utfallskriterier.

## Icke-mål i första fasen

Portföljhantering, mäklarkoppling, orderläggning, köpsignaler och annan signalmotor, extern app och bred multi-symbol-screener ligger utanför fasen.

## Öppna beslut

- Val av swing-metod och trösklar, inklusive bekräftelse och hantering av nästlade rörelser.
- Val av robusta mått för typiska och extrema SMA-avstånd samt tolerans, testfönster och utfall för stöd och motstånd.
- Om korrekt veckovis visning kan nås inom TradingViews historik- och tidsupplösningsgränser. [Metodförslag](METRICS.md)
