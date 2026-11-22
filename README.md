# Macro Analysis

Macro Analysis visar långsiktig prisutveckling, drawdowns och beteende kring SMA 200D för den aktuella symbolen i TradingView.

Öppna en vanlig prisgraf på **1D**. Klistra in [Pine v6-källan](indicators/macro-analysis.pine) i **Pine Editor** och välj **Add to chart**. Med **Show SMA 200D** kan du dölja linjen och behålla statistiken.

Panelen visar prisavkastning, CAGR och mätperiod, aktuell och maximal drawdown samt distans till SMA 200D och andel jämförbara dagar över SMA. Vecko- och intradagsintervall får ett meddelande om att 1D krävs.

Mätperioden slutar vid den senaste bekräftade dagsbaren. Resultaten bygger på den historik som TradingView har laddat och chartens prisserie, inklusive eventuella val av valuta och justeringar. [Verifiering och nästa steg](docs/STATUS.md#p01)

- Produktmål, användningsflöde och avgränsning. [Projektbeskrivning](docs/PROJECT_BRIEF.md)
- Datakrav, mått och räkneexempel. [Måttdefinitioner](docs/METRICS.md)
- Läsordning för Codex. [AGENTS.md](AGENTS.md)
- Arbetsstandard för verifiering och leverans. [WORKFLOW.md](docs/WORKFLOW.md)

[Macro Analysis på GitHub](https://github.com/block-dev-mats/Macro-Analysis)
