# Arbetsstandard

## Uppdrag och upptäckt

ChatGPT diskuterar produkten, granskar resultat och skriver Codex-prompter. Codex implementerar, testar, integrerar och rapporterar. Repot är källan till projektets faktiska nuläge.

Börja med tillämpliga instruktioner, arbetsmapp och Git-läge. Läs sedan filer och symboler som påverkar uppgiften. Samla oberoende läsningar och återanvänd resultat. Upprepa bred sökning, byggen och kontroller när ny information motiverar det.

Arbeta utifrån ett uppdragskontrakt med mål, icke-mål, beteenden som måste bevaras, acceptanskriterier och verifiering. Håll ändringar små och begripliga, återanvänd fungerande logik och undvik spekulativ abstraktion, duplicering och orelaterad refaktorering.

## Risk, session och ansvar

| Reasoning | När nivån passar |
| --- | --- |
| Low | Mekanisk ändring med liten risk. |
| Medium | Normal implementation eller felsökning. |
| High | Komplex Pine-logik eller statistik där extra analys behövs. |
| Extra High | Betydande risk för korrekthet, data eller behörigheter. |
| Max | Exceptionellt svåra problem eller särskilt kritisk granskning. |

Låt risken avgöra vilka kontroller som behövs. Återanvänd en passande Codex-session vid fortsatt arbete. En Architect-session kan samordna större uppdrag och ansvarar då för det integrerade resultatet. Använd QA eller metodgranskare när de tillför konkret värde. Använd faktiska sessions-ID:n vid hänvisning.

Låt bara en agent i taget ändra en gemensam yta. Oberoende läsningar kan köras parallellt. Parallella ändringar behöver isolerade worktrees eller skilda filer och planerad integration.

## Verifiering

- Kör diff-check och granska diffen vid små ändringar. Använd fokuserade tester för normalt ändrat beteende.
- Kontrollera drawdowns, datumgränser, historiklängd och saknad data vid riskfyllda statistikändringar. Kontrollera också 1D mot 1W när båda stöds, samt bekräftelse och framtidsläckage. Syntetiska prissekvenser ger reproducerbara facit. [Måttdefinitioner och exempel](METRICS.md)
- Redovisa TradingView-kompilering och visuella kontroller först efter faktisk körning. Om miljön saknas, ange kvarstående begränsningar och vilka manuella TradingView-steg som behövs. Använd befintlig CI som leveranskontroll när den finns.

## Data och granskningsunderlag

Offentliga marknadsdata och syntetiska kurser får användas för utveckling och granskning. Håll privata innehav, affärer, personuppgifter, API-nycklar och andra hemligheter borta från det publika GitHub-repot, loggar, fixtures och granskningsunderlag.

Skärmbilder från faktisk TradingView-körning får användas som versionsbunden evidens i en godkänd GitHub-kanal om de saknar privata data. Knyt dem till revision och relevanta körförutsättningar. Mockups är designunderlag. Lagra bara den evidens som behövs för granskningen.

## Git och rapportering

Bevara arbete utanför uppdraget. Stagea avsedda filer uttryckligen och granska staged diff. Följ uppdrags- och repopolicy för commit och push. Verifiera remote-SHA och observerat CI-läge efter push. Avstå från `git reset`, `git clean` och force-push. TradingView-publicering kräver uttryckligt uppdrag.

Använd automatisk leverans till GPT-chatten ”Macro Analysis GPT” bara för en begärd rapport och med verifierad mottagare, behörighet och fungerande kanal. Leverera annars rapporten kopieringsklar i Codex.

## Lokal mätlogg

Skriv en sanerad JSON-post per substantiellt uppdrag i den git-ignorerade `.project-local/workflow.jsonl`. Ange task-id, datum, commit när den finns, risk, antal subagenter, betydande omförsök och hinder. Uppskatta sekunder för discovery, implementation, verifiering, review och CI. Använd `0` för en fas som uteblev och `null` för okänd tidsåtgång. Håll promptinnehåll och privata data utanför loggen. Extern loggning kräver en konkret godkänd destination.

Optimera kvalitet per tid, tokens och verktygsanrop. Föreslå snävare scope efter cirka två timmar utan stabil diff. Avsluta normalt efter cirka fyra timmar med delresultat och kvarvarande hinder. Följ upp tiden inom uppdraget utan separat daemon eller timer.

Slutrapportera kort vad som ändrades, vad som verifierades, Git- och CI-läge, ungefärliga fas-tider och eventuella blockerare.
