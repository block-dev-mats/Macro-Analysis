# Måttdefinitioner

## Beslutat

### Data och mätperiod

- Overview, Dips och Compare använder dagsobservationer på standardgrafer med exakt intervallet `1D`. SMA-linjen, MA Behavior, extremmarkörer och extremfärger stöder standardgrafer med tidsbaserade intervall. Syntetiska charttyper som Heikin Ashi visar en instruktion i panelen.
- En giltig observation är en tillgänglig dagsstängning större än noll. `na`, noll och negativa stängningar behandlas som saknade. En explicit ogiltig bar bryter SMA-fönstret. En utebliven bar i datakällan kan vara ett planerat uppehåll eller ett datagap. Beräkningarna använder de barer som TradingView laddat.
- Panelen visar det första laddade giltiga sessionsdatumet och det senaste bekräftade sessionsdatumet. Pine anger datumen genom `time_tradingday`. CAGR använder hela kalenderdagar mellan dem, även vid sommartidsbyten.
- Historiska räknare, fördelningar och SMA-linjen uppdateras när dagsbaren bekräftas. Vid en ogiltig senaste stängning visar panelen `Missing` för bekräftade mått som behöver den. Max DD och andelen dagar över SMA använder fortfarande tidigare giltiga observationer.
- Chartens val av historik, prisserie, valuta och prisjusteringar påverkar resultat och jämförbarhet. Beteckningen *total return* kräver verifierad utdelningsbehandling, övriga justeringar, avgifter och valuta.
- En ruta med otillräckligt underlag visar **Missing**. Tooltips visar relevant mätperiod eller vilken observation som behövs. Varje mått bedöms efter sina egna datakrav.

#### Öppen dagsbar

- **Price** visar senaste tillgängliga kurs från TradingViews dagsserie. Prefixet `~` markerar preliminärt pris, Current DD och Overview-avstånd till senast bekräftad SMA. Max DD och Active Dip får prefixet när den öppna baren skulle vara djupare än det bekräftade värdet. I Close kan den preliminära botten försvinna vid en återhämtning. Wicks använder dagens hittills lägsta kurs även efter att senaste handelskurs har återhämtat sig.
- Avkastning, SMA, MA Behavior, Compare-avståndets percentil, avslutade dippar och deras frekvens använder bekräftade observationer. Dip Rarity och Opportunity använder den bekräftade gemensamma avgränsningen per valuta. En öppen bar kan förhandsvisa en lägre botten för ett aktivt ben. Vid bekräftelsen ersätts preliminära värden av den slutliga observationen.
- Kursen uppdateras med värddiagrammets tillgängliga kursuppdateringar. En extern symbol kan ligga kvar på ett äldre värde tills värddiagrammet uppdateras. Källor kan vara fördröjda. Om en identifierad preliminär session saknar giltig kurs i vald valuta används den senast bekräftade kursen med dess datum. Datum och status framgår av tooltipen.

### Performance

- **Return** är prisavkastningen i procent, `100 × (C_slut / C_start − 1)`. Utgå från första giltiga stängningen och stängningen på den senaste bekräftade dagsbaren. Kräv två giltiga priser på olika sessionsdatum. Annars visas `Missing`.
- CAGR i procent per år är `100 × ((C_slut / C_start)^(365,25 / d) − 1)`, där `d` är antalet kalenderdagar mellan sessionsdatumen med samma krav som för prisavkastning.
- **1Y, 3Y, 5Y och 10Y** använder samma bekräftade slutkurs. Flytta slutdatumet 1, 3, 5 eller 10 kalenderår bakåt. Om den 29 februari saknas i målåret används den 28 februari.
- Använd den senaste laddade sessionen på eller före måldatumet. Om måldatumet infaller under ett uppehåll kan referensen därför ligga tidigare. Visa `Missing` om historiken saknar en sådan session eller om dess stängning är explicit ogiltig. En senare giltig stängning på eller före måldatumet ersätter en tidigare ogiltig observation. Tooltipen visar referensdatumet för respektive mått.

### Drawdowns från historiska toppar

- **Drawdown prices** styr Current DD, Max DD, lokala dipmått, Dip Rarity och drawdownledet i Opportunity. Close är standard. Avkastning, Quality och samtliga SMA-serier använder stängningskurser i båda lägena.
- I **Close** är Current DD `100 × (pris / högsta pris − 1)` relativt den högsta bekräftade stängningen inklusive den senaste observationen. En preliminär ny topp ger 0 % och blir en historisk topp först vid bekräftad stängning.
- I **Wicks** används `min(0, 100 × (dagens low / tidigare dagars högsta high − 1))`. Dagens high blir tidigast referens för nästa giltiga sessions low. Samma bars high och low ger därför aldrig en ATH-baserad drawdown tillsammans. Max DD är lägsta giltiga Wick-värde. Baren behöver giltiga H/L och stängning. En ogiltig bar ger ingen ny drawdown eller topp och bevarar tidigare ATH och Max DD.
- Max DD i Close är det lägsta drawdownvärdet över de laddade stängningarna. Det kräver minst två giltiga dagsobservationer. En bekräftad återhämtning ändrar inte det historiska maximumet i djup.
- Redovisa drawdowns från historiska toppar och swing-episoder som egna mått. Redovisa avslutade respektive pågående episoder och räkna varje identifierad episod en gång inom sitt mått.

### Strukturella nedgångsepisoder och frekvens

- Frekvensen följer samma strukturella nedben som grafen. Ett ben har en bekräftad lokal pivottopp, en senare lägsta punkt och ett avslut när en tillräckligt stor uppgång bekräftar botten. **Depth** är `100 × (1 − botten / pivottopp)`. **Max Dip** visar det djupaste avslutade strukturella benet. **Max DD** visar den djupaste ATH-baserade drawdownen över laddad historik och kan använda andra referenspunkter. Tooltips visar båda måttens faktiska topp- och bottenpriser och sessionsdatum.
- Varje avslutad episod räknas en gång per uppnådd tröskel, inklusive exakt träff. Dips har fyra strikt stigande trösklar med standardvärdena 5, 10, 20 och 30 %. Compare använder den fasta tröskeln 10 %. Den tidigare reversalbaserade historiken gav andra antal.
- **Active Dip** visar djupet från toppen till den lägsta punkten i det öppna nedbenet. Tooltipen visar senaste kursens procentavstånd till samma topp och dagens low när en Wick-bar är öppen. I en uppgångsfas visas 0 % och tooltipen kan visa senaste avslutade dippen.
- En explicit ogiltig stängning eller ogiltigt OHLC-underlag i Wicks bryter det pågående avsnittet. Avbrutna öppna ben utelämnas ur episodantalen. Observerad kalendertid är summan av dagar mellan intilliggande giltiga dagsobservationer inom varje avsnitt. Normala sessionsuppehåll ingår. En helt utebliven bar kan se ut som ett sessionsuppehåll.
- Observerade år är observerade kalenderdagar dividerat med 365,25. Frekvensen per år är antalet avslutade episoder dividerat med observerade år. Genomsnittliga år per episod är det omvända vid positivt antal. Annualisering kräver att serien minst en gång fått en positiv skala från 52 avslutade veckor och att minst ett kalenderårs dagar observerats. Vid tillräcklig täckning och noll avslutade episoder visas `0`. Perioden inkluderar de dagar som bygger det initiala veckounderlaget. Tooltips visar antal och täckning.
- **Chart lines → Dip episodes** ritar avslutade dippar mellan den exakta lokala toppen och botten. Dips använder den lägsta valda tröskeln och Compare den fasta, inkluderande 10 %-tröskeln. Djup ≥10 % visas tydligare. Den streckade linjen visar Active Dip, med `~` under den öppna baren när dess botten är preliminär. Den separata inställningen **Dip Rarity reference** visar den prickade referensen mellan den historiska toppen och den faktiska slutobservation som tabellen använder. Tooltips visar referenspunkter och urval. Markeringarna gäller chartsymbolen på standard 1D.

### Längre rörelseben på grafen

- **Chart lines → Swing legs** visar upp- och nedben. **Dip episodes** visar de nedben som räknas vid den valda djuptröskeln, samt Active Dip. Valet av grafvisning påverkar inga tabellvärden.
- I Compare bestämmer tabellens prisvaluta datum, topp, botten och procent. Linjerna förankras på samma sessionsbarers high, low eller close i grafens prisserie enligt valt Close/Wicks-läge. När valutorna skiljer sig visar tooltipen både mätvärdena och grafens ankarpriser. Linjens lutning följer grafens axel och etiketten följer tabellens valuta. Samma princip gäller Dip Rarity med den bekräftade referens som tabellen använder. En linje kräver giltiga mätvärden och båda grafpriserna.
- **Swing scale** är samma multiplikator för graf och tabell, standard 2,0. Beräkna för varje avslutad vecka `ln(max(veckohögsta, föregående veckostängning) / min(veckolägsta, föregående veckostängning))`. I Close används max/min av bekräftade dagsstängningar inom veckan, i Wicks max high/min low. Skalan är multiplikatorn gånger medianen av 52 avslutade veckor i symbolens egen kalender och prisvaluta. Den först inlästa veckan kan vara partiell och bidrar endast med sin sista stängning. En explicit ogiltig bar avgränsar urvalet.
- Varje ny strikt dagsextrem sparar skalan som var tillgänglig då. Ett nedben bekräftas på en senare dag när uppgångens logaritmiska prisförändring från botten når denna gräns. Ett uppben bekräftas symmetriskt av tillräcklig nedgång från toppen. Vändningar kan därför ske under en tidigare högre topp. På en Wick-bar får en ny strikt extrem företräde framför en möjlig motrörelse samma dag. Vid lika extrem bevaras den första dagen. Startpunkten för nästa ben är den föregående ändpunkten.
- Pågående ben visas streckade. Etiketterna visar signerad procent, med `~` om den öppna dagsbaren ger en preliminär ändpunkt. Ett färdigt ben ritas mellan de exakta tidigare dagsbarerna först när vändningen bekräftats. Tooltips visar priser, pivotdagar och bekräftelsedag. Varje grafläge visar upp till de 96 senaste avslutade benen eller dipparna som korsar den synliga perioden på standard 1D. När perioden flyttas uppdateras urvalet av linjer utifrån den inlästa historiken. Tabellens mätperiod och antal är oberoende av zoom och bläddring.

### Symboljämförelse

- **Compare** visar chartsymbolen och upp till fyra valda symboler. En avstängd eller tom input utelämnas. Samma standardiserade börs- och tickersymbol visas en gång. **Compare currency** har SEK som standard samt EUR, USD och Native. Native använder respektive symbols ursprungliga prisvaluta. När grafens prisserie redan är valutaomräknad hämtar Compare chartsymbolens underliggande standardserie. Prisjusteringar följer den använda källan.
- För SEK, EUR och USD hämtas priset inklusive high/low i symbolens egen dagskontext före beräkningen. Vanliga valutor använder TradingViews omräkning via `request.security(..., currency = målvaluta)`. En serie som redan är uttryckt i målvalutan används direkt. Overview och Dips följer grafens prisserie. [TradingViews valutakonvertering](https://www.tradingview.com/pine-script-docs/concepts/other-timeframes-and-data/#currency)
- USDT och USDC använder `KRAKEN:USDTUSD` respektive `KRAKEN:USDCUSD`. Till SEK eller EUR multipliceras kursen med `FX_IDC:USDSEK` respektive `FX_IDC:USDEUR`. Använd senaste dagsstängning vid symbolens sessionsöppning, med högst två dygns ålder för stablecoin-ledet och fem för fiatledet. Det medger att senaste stängda vardagskurs används på helgen. När stablecoin-ledet saknas används 1 USD per USDT eller USDC. För SEK och EUR krävs fortfarande den giltiga kursen från USD till målvalutan. En giltig observerad avvikelse från paritet behålls. Samma faktor används för dagens close, high och low. Tooltipen visar observerade kurser med tider i UTC. [Kraken USDT/USD](https://www.tradingview.com/symbols/USDTUSD/?exchange=KRAKEN) · [Kraken USDC/USD](https://www.tradingview.com/symbols/USDCUSD/?exchange=KRAKEN) · [USD/SEK](https://www.tradingview.com/symbols/USDSEK/?exchange=FX_IDC) · [USD/EUR](https://www.tradingview.com/symbols/USDEUR/?exchange=FX_IDC)
- En saknad valutaobservation spärrar mått efter deras egna datakrav. Kalenderavkastning behöver bekräftade ändpunkter. En saknad omräknad stängning startar om CAGR:s sammanhängande period. ATH-baserade mått startar om sin täckning vid en saknad omräknad prisobservation för vald prisbas. Opportunity kräver tillräcklig sammanhängande ATH-täckning för femårsreferensen. Dip Rarity kräver giltiga dagliga observationer inom sin period. Dipfrekvensen avgränsar öppna ben vid avbrottet och summerar observerad tid i giltiga avsnitt. Preliminära priser och omräknade dagsobservationer kräver matchande sessionsdatum.
- CAGR, ATH-baserad Current DD och Max DD, strukturell Max Dip, Active Dip och historisk dipfrekvens använder samma definitioner som Overview och Dips. Compare använder en fast, inkluderande tröskel på **≥10 %**. `Missing` följer måttets ordinarie datakrav.
- **1Y**, **3Y** och **5Y** visar prisavkastning och använder dagens UTC-datum som gemensamt kalendermål för periodslut. Startmålet ligger motsvarande antal kalenderår tidigare, med samma skottdagsregel som Overview. Varje symbol använder sin senaste tillgängliga bekräftade stängning för periodslutet och senaste session på eller före startmålet för referensen. En ogiltig referensstängning ger `Missing`. Periodslutet måste ligga efter startmålet. Både måldatum och faktiska sessionsdatum visas i tooltipen, tillsammans med annualiserad avkastning för 3Y och 5Y. Overview förankrar perioderna i chartsymbolens senaste bekräftade session.
- **1Y**, **3Y** och **5Y** färgsätts vid samma prisvaluta, referens- och slutdatum. **CAGR** och **Max DD** kräver samma valuta och hela datumperiod. När visade värden skiljer sig markeras högsta i grönt och lägsta i rött, även när alla är negativa. För **Max DD** innebär det att värdet närmast noll markeras grönt. En symbol med öppen eller ännu obekräftad senare session ingår inte i färgjämförelsen för Max DD. **Active Dip** och **Dips ≥10%** visas neutralt.
- **Current DD** färgsätts efter cellernas två visade decimaler. Jämför preliminära och bekräftade värden från samma sessionsdag och prisvaluta bland symboler med positiv Quality. Endast den senaste användbara sessionsdagen per valuta inom fyra kalenderdagar från dagens UTC-datum färgsätts. Äldre värden, saknade värden och siffror från en tidigare session medan kursen väntar visas neutralt. När minst två jämförbara värden skiljer sig är djupast grönt och grundast rött.
- Varje extern symbols statistik räknas i symbolens eget dagskontext, inklusive sessioner som saknas i värddiagrammets kalender. `request.security()` med `lookahead_off` returnerar skalära mått och högst fem färska daterade resultat för Opportunity och Dip Rarity per symbol. TradingView samplar resultaten på värddiagrammets tidsaxel. På ett helgstängt värddiagram kan en kryptokolumn därför ligga kvar på fredagen. Vid övergångar och fördröjda data kan en fjärrsymbol behöva nästa uppdatering innan en stängning syns. Tooltips visar det faktiska senaste sessionsdatumet och den observerade perioden. Vyn använder den aktuella UTC-dagen och är avsedd för löpande jämförelse. [TradingViews datamodell](https://www.tradingview.com/pine-script-docs/concepts/other-timeframes-and-data/)

### Opportunity

- **Quality** är `0,70 × CAGR 3Y + 0,30 × CAGR 5Y` i procentenheter. För ett gemensamt jämförelsedatum används respektive symbols sista bekräftade stängning på eller före datumet. 3Y och 5Y har gemensamma kalenderbaserade startmål. Varje symbol använder sin sista session på eller före respektive startmål, högst fyra kalenderdagar tidigare. En explicit ogiltig referens ger `Missing`. Annualiseringen använder det faktiska antalet kalenderdagar mellan kurserna och 365,25 dagar per år.
- **Recovery Upside** är `|DD| / (100 − |DD|)`, med drawdown i procentenheter mätt från den historiska toppen till och med valutagruppens gemensamma bekräftade jämförelsedatum. **Opportunity** är positiv Quality multiplicerad med Recovery Upside. En giltig poäng kräver båda perioderna samt en bekräftad drawdown strikt mellan 0 och −100 %. Tooltipen visar datum, Quality och det drawdown-värde som faktiskt användes.
- Per prisvaluta väljs det datum som ger flest kvalificerade symboler, med senaste datum vid lika antal. Möjliga datum sträcker sig från dagens UTC-datum till fyra kalenderdagar bakåt. Symbolen måste ha ett giltigt underlag på sin senaste bekräftade session och en bekräftad serie som når jämförelsedatumet. Stängningen som används måste också ligga inom de senaste fyra kalenderdagarna. Det tillåter olika föregående sessioner vid börshelgdagar och utesluter för gamla data. Saknad valutakurs, kort historik eller övrigt ogiltigt underlag utesluter bara den berörda kandidaten.
- Opportunity visas direkt under tickerraden, i fetstil och med två decimaler. Positiva poäng som avrundas till noll visas som `<0.01`. Inom en grupp med minst två kvalificerade symboler färgas högsta visade poäng grön och lägsta röd när värdena skiljer sig. Om endast en valutagrupp går att rangordna får alla som delar högsta visade poäng en grön ticker och stjärna. En tillgänglig poäng från symbolens eget datum visas neutralt utanför den gemensamma rankningen. Vid flera rangordningsbara grupper i Native jämförs färgerna inom respektive valuta. Opportunity är en historisk heuristik.

| CAGR 3Y | CAGR 5Y | Current DD | Quality | Visad Opportunity |
| ---: | ---: | ---: | ---: | ---: |
| 30 % | 20 % | −2 % | 27 % | 0,55 |
| −10 % | 5 % | −60 % | −5,5 % | `Missing` |
| 15 % | 10 % | −25 % | 13,5 % | 4,50 |

### Dip Rarity

- **Dip Rarity** visar andelen observerade dagsstängningar med grundare ATH-baserad drawdown än vid jämförelsedatumet. Beräkna `100 × (1 − antal lika djupa eller djupare / antal jämförbara dagar)`. Med 50 av 1 000 sådana dagar blir värdet 95,0 %. Den aktuella stängningen räknas om den ligger i mätperioden. Vid en bekräftad drawdown på 0 % räknas alla jämförbara dagar som minst lika djupa och resultatet blir 0,0 %.
- Perioden omfattar de senaste fem kalenderåren till och med valutagruppens jämförelsedatum för Opportunity, med samma skottdagsregel som övriga perioder. Symbolens senast bekräftade stängning på eller före datumet ger jämförelsens drawdown. För varje tidigare dag används dess egen historiska topp i den valda prisvalutan. Toppen kan ligga före femårsperioden och beror på den laddade historiken.
- En giltig drawdownobservation krävs på eller högst fyra kalenderdagar före periodens start. Referensen ingår i urvalet om den infaller på startdatumet. I Wicks krävs en tidigare bekräftad high för den första jämförbara observationen. Kort historik, explicit ogiltig observation i perioden, otillgänglig slutobservation eller saknad SEK-omräkning ger `Missing`. Vanliga sessionsuppehåll påverkar urvalet genom sina faktiska handelsdagar. En bar som saknas helt i datakällan kan se ut som ett sessionsuppehåll.
- Om Opportunity saknar jämförelsedatum i en valuta väljs för Dip Rarity det senaste datumet med flest giltiga femårsunderlag inom samma fyradagarsfönster. En symbol utan giltigt värde vid gruppdatumet kan visa sitt eget giltiga femårsunderlag med dess faktiska datum. Raden visas med en decimal och neutrala färger. Tooltipen visar mätperiod, jämförelsedatum, faktisk slutstängningsdag när den avviker samt antal dagar.

### MA Stretch in Compare

- **MA Distance** är det signerade procentavståndet från vald SMA vid symbolens senaste bekräftade stängning på eller före valutagruppens Opportunity-datum. Om ett giltigt gemensamt SMA-värde saknas kan symbolens egen bekräftade stängning användas. Tooltipen visar datumet. En symbol behöver ingen giltig Opportunity-poäng för att få ett MA-avstånd.
- Både stängningen och SMA kommer från symbolens egen prisserie i vald valuta. **Daily** använder de valda sammanhängande dagsstängningarna. **Weekly** och **Monthly** använder P10:s bekräftade högre bars för en oförändrad källserie. När Compare använder en annan prisserie än grafen eller räknar om till tabellvalutan används den sista dagsstängningen i vald prisserie för varje avslutad vecka eller månad. Periodens värde blir tillgängligt på nästa periods första bekräftade dagsbar. **Smooth SMA** använder samma kalenderinterpolering som MA Behavior. Diagrammets SMA-linje och candle-färger följer diagrammets ordinarie prisserie.
- **MA Percentile** placerar det signerade avståndet i hela den sorterade fördelningen från **MA Statistics Period**. Kalenderfönstret räknas från symbolens faktiska stängningsdag. Startdatumet ingår och referensen slutar före stängningsdagen. Percentilen interpoleras mellan närmaste observerade värden på skalan P0–P100. Lika värden får mittpunkten av sina rangpositioner. Det måttet skiljer sig från **Current Stretch** i MA Behavior, som bara jämför absoluta avstånd på den aktuella sidan.
- En kalenderperiod kräver giltig SMA-historik tillbaka till fönstrets start eller tidigare. Percentilen kräver dessutom minst 30 tidigare avstånd på aktuell sida. Vid en exakt MA-träff används minst 30 tidigare observationer i hela fördelningen och färgen är neutral. Med giltig SMA men för lite historik visas bara avståndet. Saknad valutaomräkning, ett ogiltigt aktuellt MA eller en avsaknad bekräftad stängning ger `Missing` för den berörda symbolen.
- Båda raderna får röd text vid ett positivt avstånd som når den valda övre tröskeln och grön text vid ett negativt avstånd som når den komplementära nedre tröskeln. Gränserna beräknas med P10:s linjära interpolation i hela fördelningen och är inklusiva vid träff. Valen är gemensamma med extremfärgningen. Compare visar om det aktuella värdet ligger i svansen, även om det inträdde tidigare. Tooltips visar valutabas, jämförelsedatum, faktisk stängningsdag och de tidigare observationernas period och antal.

### MA Behavior

- SMA är det aritmetiska medelvärdet av det valda antalet på varandra följande giltiga bekräftade stängningar på **Daily**, **Weekly** eller **Monthly**. Standard är 200 dagar och minsta längd är 2 barer på det valda intervallet. En explicit ogiltig stängning på det valda intervallet bryter dess fönster.
- Daily inkluderar jämförelsedagens stängning. För Weekly och Monthly hämtas tidigare avslutade vecko- respektive månadsbarer från TradingView. Deras nya SMA tas i bruk vid den första bekräftade dagsbaren i nästa period. Det bekräftade grundvärdet är detsamma under hela perioden.
- **Smooth SMA** är valbart för Weekly och Monthly. På varje bekräftad dagsbar interpoleras linjärt från det föregående till det senast tillgängliga bekräftade SMA-värdet. Vikten är den del av den pågående veckan eller månaden som förflutit enligt barernas tidsstämplar. När ett föregående giltigt värde saknas används det tillgängliga SMA-värdet direkt. Både linjen och MA-måtten använder det utjämnade värdet. Linjen kan därför ligga efter den nya bekräftade nivån under övergången.
- **MA Distance** i Overview är senaste prisets procentavstånd från senast bekräftade SMA. Under öppen dag markeras värdet med `~`. Visa `Missing` när fönstret behöver fler giltiga stängningar.
- **Above MA** är `100 × antal dagar strikt över SMA / antal jämförbara dagar`. En jämförbar dag har en giltig bekräftad dagsstängning och en giltig SMA för den valda längden och det valda intervallet. Dagar med stängning exakt på SMA ingår i nämnaren. Tooltipen visar antalet jämförbara dagar och vid noll visas `Missing` för andelen. Kryssrutan på inställningsraden styr linjens synlighet.

#### Tidsintervall och bekräftelse

- MA-motorn kör i symbolens `1D`-kontext. `200 Daily` räknar alltid 200 dagsstängningar. Även jämförelsen med Weekly- eller Monthly-SMA och dess eventuella utjämning görs per dagsobservation. Avstånd, percentiler och varaktighet beräknas för hela tillgängliga dagssekvensen i den kontexten. `request.security()` överför senaste och föregående dagsresultat, inklusive tidpunkten för senaste extremhändelsen. Stora dagliga samlingar behöver därmed inte hämtas till värddiagrammet med `request.security_lower_tf()`. [TradingViews datamodell](https://www.tradingview.com/pine-script-docs/concepts/other-timeframes-and-data/)
- På 1D tas stängningen vid bekräftelsen. På andra tidsintervall visas senaste tillgängliga avslutade dagsresultat inom diagrammets tidpunkt. Historiskt styr värdbarens stängning avgränsningen. I realtid används ett avslutat dagsresultat eller föregående dagsresultat när dagens är preliminärt. En samtidigt bekräftad värdbar med samma stängningstid och slutkurs kan styrka dagens slutkurs. Vid fördröjd feed kan ett dagsresultat därför bli synligt först på nästa tillgängliga värdbar.
- På 1W och 1M kan pågående bars uppdateras efter varje bekräftad dagsstängning. Vid flera extremhändelser i samma värdbar visas den senaste bekräftade händelsens färg. Under 1D visas en händelse på den värdbar där dagsstängningen blir tillgänglig. När feeden lämnar bekräftelsen senare kan första efterföljande värdbar få markeringen. Bekräftelsetiden gör att upprepade värden på efterföljande intradagsbarer inte målas igen. Diagrammets laddade historik, abonnemangets datagränser och källans täckning styr hur långt tillbaka resultat kan visas. [Pines gränser för intrabardata](https://www.tradingview.com/pine-script-docs/writing/limitations/#intrabars)

#### Fördelningar och perioder

- **Panel View → MA Behavior** visar två kolumner för chartsymbolens dagsstängningar över och under samma SMA som linjen använder. **MA Statistics Period** är fem kalenderår som standard. Tio kalenderår och all laddad historik är valbara. Fönstret för varje bar slutar på dess sessionsdatum och börjar på kalenderårsdagen, inklusive gränsdatumet. Den 29 februari flyttas till den 28 februari vid behov. Ett valt kalenderfönster kräver giltiga MA-observationer tillbaka till eller före startdatumet. All Available använder all laddad giltig historik.
- **Time %** kräver minst 20 jämförbara sessioner. Lika pris och SMA ingår i nämnaren och hör till ingen sida. **Median Distance** är medianen av de absoluta procentavstånden på respektive sida. **P90 Distance** är den sorterade observationen med rang `ceil(0,90 × antal)`. Båda kräver minst 30 avstånd per sida. Medianen använder medelvärdet av de två mittersta observationerna vid jämnt antal. Avstånden i tabellen visar sidans tecken.
- **Median Duration** och **P90 Duration** använder samma definitioner på längderna hos minst tio fullständiga avslutade perioder per sida. En giltig korsning eller en exakt träff på SMA avslutar perioden. En ogiltig bar avbryter perioden och gör längden osäker. Perioden måste ha observerad start inom valt fönster och observerat avslut. Start mitt i en period vid första giltiga MA eller efter ett datagap ger en ofullständig period. Färdiga perioder som började före fönstret utesluts från fördelningen.
- **Current Duration** räknar den pågående periodens observerade handelssessioner, även om starten ligger före fönstret. `≥` markerar att den faktiska starten är okänd. **Current Stretch** är andelen av minst 30 tidigare avstånd på samma sida som är högst lika stora som den aktuella avvikelsen, uttryckt i procent. Den bedöms före dagens observation läggs till. Historikmåtten i tabellen inkluderar den senaste bekräftade dagen. En session som saknas helt i datakällan kan se ut som ett handelsuppehåll.

#### Extremfärger

- **Color Extreme Candles** och **Show Extreme Entry Markers** är separata val, båda av som standard. Standardtrösklarna är **P95** för ett positivt avstånd och **P5** för ett negativt. Extreme Percentile kan väljas från 55 till 100. Den nedre tröskeln är `100 − vald percentil`. Trösklarna interpoleras linjärt i den samlade sorterade fördelningen av signerade dagsavstånd, inklusive noll. Föregående bekräftade observationer i valt fönster används och minst 30 från den berörda sidan krävs.
- Trianglar visar P10:s inträde i en extremzon ovanför respektive nedanför baren. Vid standardvärden återställs röd zon först under P90 eller vid stängning på eller under SMA. Grön zon återställs först över P10 eller vid stängning på eller över SMA. För andra val ligger återställningspercentilen fem percentilsteg närmare medianen. Ett explicit ogiltigt pris räcker inte för att återställa zonen.
- Candle-färgen prövar dagens bekräftade avstånd mot yttertrösklarna. Högst de första två sammanhängande bekräftade dagarna per svans färgas. En neutral, ogiltig eller motsatt kvalificerad observation bryter följden. Trianglarnas inträden och återställningsband påverkas inte.
- Markerade candles använder värdbarens faktiska öppning, högsta, lägsta och stängning. Current Stretch i tabellen markeras om senaste dagsstängningen gav en händelse. Current Duration är en separat beskrivning. Ett framtida jämförande test kan dela redan bekräftade extremhändelser efter varaktighetspercentil vid inträdet och mäta hur urvalet förändras innan varaktighet får påverka markeringen.
- Färgerna beskriver historisk ovanlighet. Nyare prisrörelser påverkar bara senare bedömningar. Om TradingView laddar äldre historik eller ändrar prisdata kan en tidigare referensfördelning få annat underlag.

### Deterministiska P01-exempel

| Fall | Förväntat |
| --- | --- |
| `100` den 2 januari 2020 och `146,41` den 2 januari 2024. | `46,41 %` prisavkastning och `10,00 %` CAGR över 1 461 kalenderdagar. |
| `100 → 85 → 95 → 75 → 100`. | Aktuell drawdown `0 %` och max drawdown `−25 %`. |
| 200 stängningar på `100`, följda av `110` och `90`. | SMA saknas under de första 199 barerna. De tre sista SMA-värdena är `100`, `100,05` och `100`. Andelen över SMA är `1/3` av jämförbara dagar. |
| En dagsbar med `na` efter 200 giltiga stängningar. | Aktuella mått som kräver stängningen är `Missing`. SMA återkommer vid den 200:e giltiga stängningen i följd efter den ogiltiga baren. |
| En giltig stängning, eller två giltiga stängningar med samma sessionsdatum. | Prisavkastning och CAGR är `Missing`. Max drawdown är `Missing` när det bara finns en giltig stängning. |
| Tidigare topp `100`, öppen dagsbar med high `105`, low `90` och senaste handel `101`. | Price är `~101`. Current DD är `~0 %` i Close och `~−10 %` i Wicks. Den bekräftade toppen och historiska räknare förändras först vid bekräftelse. |

### Deterministiska P02-exempel

| Fall | Förväntat |
| --- | --- |
| Slutkurs `100` den 3 juni 2024. Äldsta stängning `80` fredagen den 2 juni 2023. | Lördagens måldatum ger fredagen som referens. 1Y är `25 %`. 3Y, 5Y och 10Y är `Missing`. |
| Slutdatum 4 juli 2024. Sessioner 3 och 5 juli 2023, inga barer den 4 juli. | 1Y använder den 3 juli 2023. |
| Slutdatum 29 februari 2024. | 1Y, 3Y, 5Y och 10Y har måldatum den 28 februari i respektive målår. |
| Måldatum 21 november 2023. Stängningen den 20 november är `na` och den 22 november är giltig. | Referensen för den 21 november är osäker och ger `Missing`. Med måldatum 22 november används den giltiga stängningen. |

### Historiska exempel för P03:s tidigare reversalmetod

| Stängningar med 5 % reversal | Avslutade episoddjup och aktiv nedgång |
| --- | --- |
| `100 → 94 → 100 → 80 → 100` | 6 % och 20 %. Antal vid ≥5, ≥10, ≥20 och ≥30 % är 2, 1, 1 och 0. |
| `100 → 94 → 95 → 80 → 84` | En episod på 20 %. Stängning 84 uppfyller exakt 5 % reversal från 80. |
| `100 → 94 → 95 → 80` | 0 avslutade. Active Dip är −20 %. |
| `100 → 90 → 96 → 89 → 95` | Två episoder på 10 % och cirka 7,29 %. Den andra lokala toppen är 96. |
| `100 → 100 → 95 → 95 → 99,74 → 99,75` | Lika topp och botten ger inga dubletter. En episod träffar 5 % djup och reversal exakt. |
| `100 → 70 → na → 80 → 72 → 76` | Första avsnittets pågående episod avbryts. En bekräftad episod på 10 % räknas från den nya toppen 80. |

## Förslag

### Datatäckning

Markera identifierade datagap när det finns tillräckligt underlag för att skilja dem från planerade sessionsuppehåll. En framtida beräkning på 1W måste behandla hela den underliggande dagssekvensen innan resultatet visas på veckocharten. Samma krav på bevarade dagsobservationer gäller intraday.

### Varaktighet och återhämtning till historisk topp

- En episod börjar vid första stängning under det löpande högsta värdet och avslutas vid första stängning på eller över den nivån. Använd den senaste stängningen på toppnivån före nedgången som toppdatum. Botten är den första lägsta stängningen inom episoden. Mät kalenderdagar från topp till botten och från botten till återhämtning. För en pågående episod är botten preliminär och återhämtningstiden `N/A`.
- Räkna en episod som passerar ett identifierat datagap som osäker. Håll den utanför antalen för säkert avslutade och pågående episoder. Max drawdown bygger på observerade stängningar. Visa begränsad täckning om gap kan dölja en djupare botten.

### MA Behavior

- Andelen dagar under SMA beräknas med samma nämnare som andelen över SMA och med antalet dagar strikt under SMA som täljare. Om datagap senare kan identifieras ska fönster som korsar dem uteslutas.
- Typiskt avstånd kan visas som median, beräknad separat för positiva och negativa distanser. Ett extremt avstånd kan beskrivas med en övre percentil på den positiva sidan och en nedre percentil på den negativa. Kvantilmetod, gränser och minsta urval är öppna val. Visa `N/A` för en sida som saknar tillräckliga observationer.

### Deterministiska exempel för förslagen

| Fall | Förväntat med förslaget |
| --- | --- |
| `100 → 85 → 95 → 75 → 100` den 5–9 februari 2024, en stängning per dag. | En avslutad episod vid både 10 och 20 procent, noll vid 30 procent. Tre kalenderdagar till botten och en till återhämtning. Om sista `100` tas bort är episoden pågående med aktuell drawdown `−25 %`. |
| 200 stängningar på `100`, följda av `110` och `90`. | Andelen under SMA är `1/3` av jämförbara dagar. |

## Senare

- **Swing-episoder.** Välj swing-punkter eller tröskelmetod och definiera vad som bekräftar start och slut, vilken dag bekräftelsen blir känd och hur nästlade rörelser räknas. Föreslagna utfall är storlek i procent av episodens startpris, kalenderdagar mellan valt start- och slutdatum samt antal episoder per redovisad mätperiod. Nivåer och segmentering är öppna.
- **Stöd och motstånd kring SMA.** Besluta vad som utlöser och avslutar ett test, vilken tolerans och vilket utfallsfönster som gäller samt hur upprepade kontakter räknas. Andelen lyckade test ska ha objektiva kriterier för täljare och nämnare.
