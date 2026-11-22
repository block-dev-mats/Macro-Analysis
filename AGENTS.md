# Macro Analysis

Projektets repo är `block-dev-mats/Macro-Analysis`. [GitHub](https://github.com/block-dev-mats/Macro-Analysis)

Börja med tillämpliga överordnade instruktioner och använd följande läsordning.

1. [Arbetsstandard](docs/WORKFLOW.md) för upptäckt, verifiering och leverans.
2. [Nuläge](docs/STATUS.md) som ingång till aktuell uppgift. Kontrollera läget mot repot.
3. [Projektbeskrivning](docs/PROJECT_BRIEF.md) för produktmål och scope.
4. [Måttdefinitioner](docs/METRICS.md) för databeroenden och statistisk metod.

## Teknik och data

- Pine Script v6, en TradingView-indikator för den aktuella symbolen.
- Dagliga prisstängningar styr beräkningarna. `200D` betyder 200 dagliga barer. Utgå från 1D och tydliggör stöd för övriga chartintervall.
- Använd bekräftade dagliga barer för avslutade resultat utan framtidsläckage eller repainting. Bevara samtliga relevanta dagsobservationer vid eventuell visning på andra chartintervall.
- Följ projektets datagränser. [Data och granskningsunderlag](docs/WORKFLOW.md#data-och-granskningsunderlag)
