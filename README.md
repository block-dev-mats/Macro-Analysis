# Macro Analysis

Macro Analysis visar långsiktig prisutveckling, drawdowns och beteende kring ett valbart SMA i TradingView.

Öppna en vanlig prisgraf på **1D**. Klistra in [Pine v6-källan](indicators/macro-analysis.pine) i **Pine Editor** och välj **Update on chart** för en befintlig instans eller **Add to chart** första gången. På raden **SMA** väljer du längd och **Daily**, **Weekly** eller **Monthly**. Standard är 200 dagar. Kryssrutan på samma rad döljer eller visar linjen och behåller statistiken.

För Weekly och Monthly kan du aktivera **Smooth SMA**. Linjen, **MA Distance** och **Above MA** använder då samma utjämnade värde. **Panel corner** placerar panelen i något av chartens fyra hörn.

Panelen visar prisavkastning sedan start och för 1, 3, 5 och 10 kalenderår, CAGR, drawdowns och SMA-mått. Periodvärdenas tooltips visar faktiska referensdatum. Vecko- och intradagsintervall får ett meddelande om att 1D krävs.

Med **Panel View → Dips** visas aktuell nedgång från den lokala toppen och historisk frekvens för återhämtade nedgångsepisoder. Trösklar och återhämtningskrav kan ställas in. Antal och täckning visas i tooltips.

Med **Panel View → Compare** jämför du chartsymbolen med upp till fyra extra symboler. Förvalen är ACWI, EUNL och VWCE från de andra graferna i Avanza-fliken samt XACT Norden Högutdelande (XACTHDIV). Kryssrutan på varje symbolrad styr om den visas. Kolumnernas tooltips visar valuta och faktiska sessionsdatum. [Jämförelseregler och datatäckning](docs/METRICS.md#symboljämförelse)

**Compare currency** väljer gemensam SEK eller varje symbols egen valuta (**Native**). **Opportunity** väger samman 3Y och 5Y CAGR med avståndet tillbaka till tidigare pristopp vid ett gemensamt datum per valuta. En grön stjärna visas när det finns en enda jämförbar grupp och en entydig ledare. [Beräkningsmetod](docs/METRICS.md#opportunity)

Mätperioderna bygger på bekräftade dagsstängningar i den historik TradingView tillhandahåller. [Verifiering och begränsningar](docs/STATUS.md#p07)

- Produktmål, användningsflöde och avgränsning. [Projektbeskrivning](docs/PROJECT_BRIEF.md)
- Datakrav, mått och räkneexempel. [Måttdefinitioner](docs/METRICS.md)
- Läsordning för Codex. [AGENTS.md](AGENTS.md)
- Arbetsstandard för verifiering och leverans. [WORKFLOW.md](docs/WORKFLOW.md)

[Macro Analysis på GitHub](https://github.com/block-dev-mats/Macro-Analysis)
