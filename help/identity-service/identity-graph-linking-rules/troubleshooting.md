---
title: Felsökningsguide för länkningsregler för identitetsdiagram
description: Lär dig hur du felsöker vanliga problem i länkningsregler för identitetsdiagram.
badge: Beta
exl-id: 98377387-93a8-4460-aaa6-1085d511cacc
source-git-commit: edda302a1f24c9991074c16fd9e770f2bf262b7c
workflow-type: tm+mt
source-wordcount: '3174'
ht-degree: 0%

---

# Felsökningsguide för länkningsregler för identitetsdiagram

>[!AVAILABILITY]
>
>Regelfunktionen för länkning av identitetsdiagram finns för närvarande i betaversionen. Kontakta ditt Adobe-kontoteam för att få information om deltagandekriterierna. Funktionen och dokumentationen kan komma att ändras.

När du testar och validerar regler för länkning av identitetsdiagram kan du stöta på problem som rör datainmatning och diagrambeteende. Läs det här dokumentet om du vill veta mer om hur du felsöker några vanliga problem som kan uppstå när du arbetar med länkningsregler för identitetsdiagram.

## Översikt över dataöverföringsflöde {#data-ingestion-flow-overview}

Bilden nedan är en förenklad representation av hur data flödar in i Adobe Experience Platform och Program. Använd det här diagrammet som referens för att få en bättre förståelse för innehållet på den här sidan.

![Ett diagram över hur datainmatning flödar i identitetstjänsten.](../images/troubleshooting/dataflow_in_identity.png)

Det är viktigt att notera följande faktorer:

* För strömmande data börjar kundprofil, identitetstjänst och datasjön i realtid att bearbeta data när data skickas. Fördröjningen för att slutföra bearbetningen av data beror dock på tjänsten. Vanligtvis tar det längre tid att bearbeta datasjön jämfört med profil och identitet.
   * Om data inte visas när en fråga körs mot en datauppsättning även efter några timmar är det troligt att data inte har importerats till Experience Platform.
* För gruppdata kommer alla data först att flöda in i datasjön, sedan kommer data att spridas till Profil och Identitet om datauppsättningen är aktiverad för Profil och Identitet.
* För frågor som rör inmatning är det viktigt att problemet isoleras på tjänstenivå för korrekt felsökning och felsökning. Det finns tre möjliga problemtyper att tänka på:

| Typ av problem med inmatning | hämtas data in i datasjön? | hämtas data in i profilen? | Inhämtas data från identitetstjänsten? |
| --- | --- | --- | --- |
| Allmänt problem med intag | Nej | Nej | Nej |
| Diagramproblem | Ja | Ja | Nej |
| Problem med profilfragment | Ja | Nej | Ja |

## Problem med datainmatning {#data-ingestion-issues}

>[!NOTE]
>
>* I det här avsnittet förutsätts att data har importerats till datasjön och att det inte fanns några syntaxfel eller andra fel som skulle förhindra att data hämtas in till Experience Platform från början.
>
>* I exemplen används ECID som cookie-namnutrymme och CRMID som personnamnutrymme.

### Mina identiteter importeras inte till identitetstjänsten{#my-identities-are-not-getting-ingested-into-identity-service}

Det finns olika orsaker till varför detta kan inträffa, bland annat följande:

* [Datauppsättningen är inte aktiverad för profilen ](../../catalog/datasets/enable-for-profile.md).
* Posten hoppas över eftersom det bara finns en identitet i händelsen.
* [Ett verifieringsfel uppstod i identitetstjänsten ](../guardrails.md#identity-value-validation).
   * Ett ECID kan till exempel ha överskridit den maximala längden på 38 tecken.
* Som standard är [AAID:n spärrade från inmatning](../guardrails.md#identity-namespace-ingestion).
* Identiteten har tagits bort på grund av [systemskyddsräcken](../guardrails.md#understanding-the-deletion-logic-when-an-identity-graph-at-capacity-is-updated).

Inom ramen för länkningsreglerna för identitetsdiagram kan en post refuseras från identitetstjänsten eftersom den inkommande händelsen har två eller flera identiteter med samma unika namnutrymme men olika identitetsvärde. Detta scenario inträffar vanligtvis på grund av implementeringsfel.

Tänk på följande händelse med två antaganden:

* Fältnamnet CRMID är markerat som en identitet med namnutrymmet CRMID.
* Namnutrymmets CRMID definieras som ett unikt namnutrymme.

Följande händelse returnerar ett felmeddelande som anger att importen misslyckades.

<!-- because the ingestion of this erroneous event would have resulted in graph collapse. In the following event, two entities (Alice and Bob) are both associated with the same namespace (CRMID). -->

```json
{ 
  "_id": "random_string", 
  "eventType": "web browsing event", 
  "identityMap": { 
    "ECID": [ 
      { 
        "id": "11111111111111111111111111111111111111", 
        "primary": false 
      } 
    ], 
    "CRMID": [ 
      { 
        "id": "Alice", 
        "primary": true 
      } 
    ] 
  }, 
  "CRMID": "Bob", 
  "timestamp": "2024-08-17T15:22:51+00:00", 
  "web": { 
    "webPageDetails": { 
      "URL": "https://www.adobe.com/acrobat.html", 
      "name": "Adobe Acrobat" 
    } 
  } 
} 
```

**Felsökningssteg**

För att lösa det här felet måste du först samla in följande information:

* Identitetsvärdet (`identity_value`) som du förväntade dig skulle vara inkapslat i identitetsdiagrammet.
* Den datauppsättning (`dataset_name`) som händelsen skickades i.

Använd sedan [Adobe Experience Platform Query Service](../../query-service/home.md) och kör följande fråga:

>[!TIP]
>
>Ersätt `dataset_name` och `identity_value` med den information som du har samlat in.

```sql
  SELECT key, col.id as identityValue, timestamp, _id, identityMap, * 
  FROM (SELECT key, explode(value), * 
  FROM (SELECT explode(identityMap), * 
  FROM dataset_name)) WHERE col.id = 'identity_value' 
```

När du har kört frågan letar du reda på den händelsepost som du förväntade dig att generera ett diagram och kontrollerar sedan att identitetsvärdena är olika på samma rad. Visa följande bild som ett exempel:

![En namnlös fråga som resulterade i duplicerade namnutrymmen.](../images/troubleshooting/duplicated_unique_namespace.png)

>[!NOTE]
>
>Om de två identiteterna är exakt likadana, och om händelsen hämtas via direktuppspelning, kommer både Identitet och Profil att deduplicera identiteten.

### Mina upplevelsehändelsefragment importeras inte till profilen {#my-experience-event-fragments-are-not-getting-ingested-into-profile}

Det finns olika orsaker till varför dina händelsefragment inte kommer in i profilen, bland annat men inte begränsat till:

* [Datauppsättningen är inte aktiverad för profilen ](../../catalog/datasets/enable-for-profile.md).
* [Ett verifieringsfel kan ha inträffat i profilen ](../../xdm/classes/experienceevent.md).
   * En upplevelsehändelse måste till exempel innehålla både `_id` och `timestamp`.
   * Dessutom måste `_id` vara unik för varje händelse (post).
* Namnutrymmet med högst prioritet är en tom sträng.

När det gäller namnområdesprioritet avvisar profilen:

* Alla händelser som innehåller två eller flera identiteter med den högsta namnområdesprioriteten. Om exempelvis GAID inte är markerat som ett unikt namnutrymme och två identiteter båda med ett GAID-namnutrymme och olika identitetsvärden kommer in, kommer profilen inte att lagra någon av händelserna.
* Alla händelser där namnutrymmet med högst prioritet är en tom sträng.

**Felsökningssteg**

Om dina data skickas till en datalinje, men inte till en profil, och du tror att det beror på att två eller flera identiteter med den högsta namnområdesprioriteten i en enda händelse skickas, kan du köra följande fråga för att verifiera att två olika identitetsvärden har skickats mot samma namnutrymme:

>[!TIP]
>
>I följande frågor:
>
>* Ersätt `_testimsorg.identification.core.email` med sökvägen som skickar identiteten.
>* Ersätt `Email` med namnutrymmet med högsta prioritet. Det här är samma namnutrymme som inte importeras.
>* Ersätt `dataset_name` med den datauppsättning som du vill fråga.

```sql
  SELECT identityMap, key, col.id as identityValue, _testimsorg.identification.core.email, _id, timestamp 
  FROM (SELECT key, explode(value), * 
  FROM (SELECT explode(identityMap), * 
  FROM dataset_name)) WHERE col.id != _testimsorg.identification.core.email and key = 'Email' 
```

Du kan också köra följande fråga för att kontrollera om det inte sker någon inmatning till profilen på grund av att det högsta namnutrymmet har en tom sträng:

```sql
  SELECT identityMap, key, col.id as identityValue, _testimsorg.identification.core.email, _id, timestamp 
  FROM (SELECT key, explode(value), * 
  FROM (SELECT explode(identityMap), * 
  FROM dataset_name)) WHERE (col.id = '' or _testimsorg.identification.core.email = '') and key = 'Email' 
```

Dessa två frågor förutsätter att en identitet skickas från identityMap och att en annan identitet skickas från en identitetsbeskrivare. **OBS!**: I XDM-scheman (Experience Data Model) är identitetsbeskrivningen det fält som markerats som en identitet.

### Mina upplevelsehändelsefragment är inkapslade, men har fel primära identitet i profilen

Namnområdesprioriteten spelar en viktig roll i hur händelsefragment bestämmer den primära identiteten.

* När du har konfigurerat och sparat dina [identitetsinställningar](./identity-settings-ui.md) för en viss sandlåda använder profilen [namnområdesprioritet](namespace-priority.md#real-time-customer-profile-primary-identity-determination-for-experience-events) för att fastställa den primära identiteten. När det gäller identityMap kommer Profile inte längre att använda flaggan `primary=true`.
* Profilen refererar inte längre till den här flaggan, men andra tjänster på Experience Platform kan fortsätta använda flaggan `primary=true`.

För att [autentiserade användarhändelser](configuration.md#ingest-your-data) ska kunna kopplas till personnamnområdet måste alla autentiserade händelser innehålla personnamnområdet (CRMID). Detta innebär att även efter att en användare har loggat in måste personens namnutrymme fortfarande finnas på varje autentiserad händelse.

Du kan fortsätta att se flaggan `primary=true` events när du söker efter en profil i profilvisningsprogrammet. Detta ignoreras dock och används inte av profilen.

AAID:n blockeras som standard. Om du använder [Adobe Analytics-källkopplingen](../../sources/tutorials/ui/create/adobe-applications/analytics.md) måste du därför se till att ECID prioriteras högre än ECID så att de oautentiserade händelserna får en primär ECID-identitet.

**Felsökningssteg**

* Om du vill verifiera att autentiserade händelser innehåller både namnområdet för person och cookie läser du stegen som beskrivs i avsnittet [felsökningsfel för data som inte hämtas till identitetstjänsten](#my-identities-are-not-getting-ingested-into-identity-service).
* Om du vill verifiera att autentiserade händelser har den primära identiteten för personnamnutrymmet (t.ex. CRMID), söker du i namnutrymmet person i profilvisningsprogrammet med principen för sammanfogning utan sammanfogning (detta är den sammanfogningsprincip som inte använder ett privat diagram). Den här sökningen returnerar bara händelser som är associerade med personnamnutrymmet.

## Problem relaterade till diagrambeteende {#graph-behavior-related-issues}

I det här avsnittet beskrivs vanliga problem som du kan råka ut för när identitetsdiagrammet fungerar.

### Identiteten länkas till fel person

Identitetsoptimeringsalgoritmen respekterar [de senast upprättade länkarna och tar bort de äldsta länkarna](./identity-optimization-algorithm.md#identity-optimization-algorithm-details). Det är därför möjligt att när den här funktionen är aktiverad kan ECID:n omtilldelas (länkas) från en person till en annan. Följ stegen nedan för att förstå hur en identitet länkas över tid:

**Felsökningssteg**

>[!NOTE]
>
>Följande steg hämtar information under följande antaganden:
>
>* En enskild datauppsättning används (detta kommer inte att fråga efter flera datauppsättningar).
>
>* Data tas inte bort från datasjön på grund av borttagning av [Advanced Data Lifecycle Management](../../hygiene/home.md), [Privacy Service](../../privacy-service/home.md) eller andra tjänster som utför borttagning.

Först måste du samla in följande information:

* Identitetssymbolen (namespaceCode) för cookie-namnutrymmet (t.ex. ECID) och det namnutrymme (t.ex. CRMID) som skickades.
   * För Web SDK-implementeringar är dessa vanligtvis de namnutrymmen som ingår i identityMap.
   * För källkopplingsimplementationer för analyser är detta cookie-identifieraren som ingår i identityMap. Personidentifieraren är ett eVar-fält som är markerat som en identitet.
* Den datauppsättning som händelsen skickades i (dataset_name).
* Identitetsvärdet för det cookie-namnutrymme som ska slås upp (identity_value).

Identitetssymboler (namespaceCode) är skiftlägeskänsliga. Om du vill hämta alla identitetssymboler för en viss datauppsättning i identityMap kör du följande fråga:

```sql
SELECT distinct explode(*)FROM (SELECT map_keys(identityMap) FROM dataset_name)
```

Om du inte känner till identitetsvärdet för din cookie-identifierare och du vill söka efter ett cookie-ID som skulle ha länkats till flera personidentifierare, måste du köra följande fråga. Den här frågan förutsätter ECID som cookie-namnområde och CRMID som personnamnområde.

>[!BEGINTABS]

>[!TAB Web SDK-implementering]

```sql
  SELECT identityMap['ECID'][0]['id'], count(distinct identityMap['CRMID'][0]['id']) as crmidCount FROM dataset_name GROUP BY identityMap['ECID'][0]['id'] ORDER BY crmidCount desc 
```

>[!TAB Implementering av analyskällans anslutning]

```sql
  SELECT identityMap['ECID'][0]['id'], count(distinct personID) as crmidCount FROM dataset_name group by identityMap['ECID'][0]['id'] ORDER BY crmidCount desc 
```

**Obs!** personID refererar till sökvägen för beskrivningen. Den här informationen finns under scheman.

>[!ENDTABS]

Granska sedan associationen för cookie-namnutrymmet i tidsstämpelordning genom att köra följande fråga:

>[!BEGINTABS]

>[!TAB Web SDK-implementering]

```sql
  SELECT identityMap['CRMID'][0]['id'] as personEntity, * 
  FROM dataset_name 
  WHERE identitymap['ECID'][0].id ='identity_value' 
  ORDER BY timestamp desc 
```

>[!TAB Implementering av analyskällans anslutning]

```sql
SELECT _experience.analytics.customDimensions.eVars.eVar10 as personEntity, * 
FROM dataset_name 
WHERE identitymap['ECID'][0].id ='identity_value' 
ORDER BY timestamp desc 
```

**Obs!**: I det här exemplet antas att `eVar10` har markerats som en identitet. För dina konfigurationer måste du ändra eVarna baserat på implementeringen i din egen organisation.

>[!ENDTABS]

### Identitetsoptimeringsalgoritmen fungerar inte som förväntat

**Felsökningssteg**

Mer information finns i dokumentationen om [identitetsoptimeringsalgoritmen](./identity-optimization-algorithm.md), samt i de typer av diagramstrukturer som stöds.

* I [diagramkonfigurationsguiden](./example-configurations.md) finns exempel på diagramstrukturer som stöds.
* Du kan även läsa [implementeringshandboken](./configuration.md#appendix) för exempel på diagramstrukturer som inte stöds. Det finns två scenarier:
   * Inget enskilt namnutrymme i alla profiler.
   * Ett [&quot;farligt ID&quot;](./configuration.md#dangling-loginid-scenario)-scenario inträffar. I det här scenariot går det inte att avgöra om det farliga ID:t är kopplat till någon av personenheterna i diagrammen.

Du kan också använda [diagramsimuleringsverktyget i gränssnittet](./graph-simulation.md) för att simulera händelser och konfigurera egna inställningar för namnutrymmes- och namnområdesprioritet. Om du gör det kan du få en grundläggande förståelse för hur identitetsoptimeringsalgoritmen ska fungera.

Om simuleringsresultaten matchar dina diagrambeteendeförväntningar kan du kontrollera och se om dina [identitetsinställningar](./identity-settings-ui.md) matchar de inställningar som du har konfigurerat i simuleringen.

### Jag ser fortfarande komprimerade diagram i sandlådan även efter att jag har konfigurerat identitetsinställningarna

Identitetsdiagram följer din konfigurerade unika namnområdes- och namnområdesprioritet _när_ inställningarna har sparats. Komprimerade diagram som finns _före_ som du sparar dina nya inställningar påverkas inte förrän nya data har infogats så att det komprimerade diagrammet uppdateras. Den primära identiteten för händelsefragment i kundprofilen i realtid uppdateras inte ens när namnområdesprioriteten har ändrats.

**Felsökningssteg**

Du kan använda [identitetsdiagramvisningsprogrammet](../features/identity-graph-viewer.md) för att kontrollera om diagrammet har importerats före eller efter dina inställningar. Undersök den senaste uppdaterade tidsstämpeln under [!UICONTROL Link properties] för att se när identitetstjänsten importerade diagrammet. Om tidsstämpeln är före konfigurationen tyder det på att det&quot;komprimerade&quot; diagrammet skapades innan funktionen aktiverades.

![Identitetsdiagramvisningsprogrammet med ett exempeldiagram.](../images/troubleshooting/graph_viewer.png)

### Jag vill veta hur många komprimerade diagram som finns i min sandlåda

Använd identitetspanelen för att få insikter om identitetsgrafens tillstånd, till exempel antalet identiteter och diagram. I måttet &quot;Antal diagram med flera namnutrymmen&quot; finns ett antal komprimerade diagram - det här är diagram som innehåller två eller flera identiteter med samma namnutrymme. Om du utgår ifrån att sandlådan inte har några data och har konfigurerat ett namnutrymme (t.ex. CRMID) som unikt, är det förväntat att det ska finnas nolldiagram med två eller flera CRMID:n. I exemplet nedan finns det två diagram som innehåller två eller flera e-postadresser.

![Identitetspanelen med mått för identitetsantal, antal diagram, antal diagram per namnområde, antal diagram per storlek och antal diagram för diagram som är fler än två namnutrymmen.](../images/troubleshooting/identity_dashboard.png)

Du kan hitta en detaljerad beskrivning i [datamängden för export av ögonblicksbilder](../../dashboards/query.md) i datasjön genom att köra frågan nedan:

>[!NOTE]
>
>* Ersätt `dataset_name` med det faktiska namnet på datauppsättningen.
>
>* Antalet matchar eventuellt inte exakt. Identitetspanelen baseras på antalet identitetsdiagram och följande fråga baseras på antalet profiler med två eller flera identiteter. Data behandlas och uppdateras av tjänsten oberoende av varandra.

```sql
  SELECT key, identityCountInGraph, count(identityCountInGraph) as graphCount 
  FROM (SELECT key, cardinality(value) as identityCountInGraph 
  FROM (SELECT explode(identityMap) 
  FROM dataset_name 
  WHERE cardinality(identityMap) > 1)) /* by definition, graphs have 2 or more identities */ 
  WHERE key not in ('ecid', 'aaid', 'idfa', 'gaid') /* filter out common device/cookie namespaces */ 
  GROUP BY 1, 2 
  ORDER BY 1, 2 asc 
```

Du kan använda följande fråga i datauppsättningen för export av ögonblicksbilder för att hämta exempel på identiteter från komprimerade diagram.

```sql
  SELECT identityMap 
  FROM dataset_name 
  WHERE cardinality(identityMap['CRMID'])>1 /* any graphs with 2+ CRMID. Change CRMID namespace if needed */ 
```

>[!TIP]
>
>De två frågor som anges ovan ger förväntade resultat om sandlådan inte är aktiverad för den delade enhetens övergångsmetod och beter sig annorlunda än länkningsreglerna för identitetsdiagram.

## Vanliga frågor och svar {#faq}

I det här avsnittet finns en lista med svar på vanliga frågor om länkningsregler för identitetsdiagram.

### Identitetsoptimeringsalgoritm {#identity-optimization-algorithm}

#### Jag har ett CRMID för varje affärsenhet (B2C CRMID, B2B CRMID), men jag har inget unikt namnutrymme för alla mina profiler. Vad händer om jag markerar B2C CRMID och B2B CRMID som unika och aktiverar mina identitetsinställningar?

Scenariot stöds inte. Därför kan du se att diagram komprimeras om en användare använder sitt B2C CRMID för att logga in och en annan användare använder sitt B2B CRMID för att logga in. Mer information finns i avsnittet [Krav på namnutrymme för en person](./configuration.md#single-person-namespace-requirement) på implementeringssidan.

#### Åtgärdar identitetsoptimeringsalgoritmen befintliga komprimerade diagram?

Befintliga komprimerade diagram påverkas (&quot;fast&quot;) endast av diagramalgoritmen om dessa diagram uppdateras när du har sparat de nya inställningarna.

#### Vad händer med händelserna om två personer loggar in och ut med samma enhet? Överför alla händelser till den senast autentiserade användaren?

* Anonyma händelser (händelser med ECID som primär identitet i kundprofilen i realtid) överförs till den senast autentiserade användaren. Detta beror på att ECID kommer att länkas till CRMID för den senaste autentiserade användaren (i identitetstjänsten).
* Alla autentiserade händelser (händelser med CRMID definierat som primär identitet) kommer att finnas kvar hos personen.

Mer information finns i guiden [fastställa den primära identiteten för upplevelsehändelser](../identity-graph-linking-rules/namespace-priority.md#real-time-customer-profile-primary-identity-determination-for-experience-events).

#### Hur kommer resor i Adobe Journey Optimizer att påverkas när ECID överförs från en person till en annan?

CRMID för den senaste autentiserade användaren kommer att länkas till ECID (delad enhet). ECID kan omtilldelas från en person till en annan baserat på användarbeteende. Effekten beror på hur resan är uppbyggd, så det är viktigt att kunderna testar resan i en sandlådemiljö för att validera beteendet.

De viktigaste punkterna som ska markeras är följande:

* När en profil inträder på en resa leder omtilldelning av ECID inte till att profilen avslutas mitt på en resa.
   * Reseutgångar aktiveras inte av diagramändringar.
* Om en profil inte längre är kopplad till ett ECID kan det leda till att kundens resa ändras om det finns ett villkor som använder målgruppskvalifikation.
   * ECID-borttagning kan ändra händelser som är kopplade till en profil, vilket kan leda till förändringar i målgruppens kvalifikationer.
* Återinträde av en resa beror på resans egenskaper.
   * Om du inaktiverar återinträde för en resa kommer samma profil inte att användas förrän om 91 dagar (baserat på den globala tidsgränsen) när en profil avslutas från den resan.
* Om en resa börjar med ett ECID-namnområde, den profil som anges och den profil som tar emot åtgärden (t.ex. e-post, erbjudande) kan vara annorlunda beroende på hur resan är utformad.
   * Om det till exempel finns ett väntevillkor mellan åtgärderna och ECID-överföringar under vänteperioden kan en annan profil användas.
   * Med den här funktionen är ECID inte längre kopplat till en profil.
   * Rekommendationen är att påbörja resor med personliga namnutrymmen.

### Namnområdesprioritet

#### Jag har aktiverat mina identitetsinställningar. Vad händer med mina inställningar om jag vill lägga till ett anpassat namnutrymme efter att inställningarna har aktiverats?

Det finns två &#39;bucket&#39; med namnutrymmen: namnutrymmen för personer och namnutrymmen för enheter/cookies. Det nya anpassade namnutrymmet har den lägsta prioriteten i varje &#39;bucket&#39; så att det nya anpassade namnutrymmet inte påverkar befintlig datainmatning.

#### Om kundprofilen i realtid inte längre använder flaggan&quot;primär&quot; på identityMap, måste det här värdet ändå skickas?

Ja, den primära flaggan för identityMap används av andra tjänster. Mer information finns i guiden [om konsekvenserna av namnområdesprioritet för andra Experience Platform-tjänster](../identity-graph-linking-rules/namespace-priority.md#implications-on-other-experience-platform-services).

#### Gäller namnområdesprioriteten profilpostdatauppsättningar i kundprofilen i realtid?

Nej. Namnområdesprioriteten gäller bara Experience Event-datauppsättningar som använder klassen XDM ExperienceEvent.

#### Hur fungerar den här funktionen tillsammans med identitetsgrafens skyddsytor med 50 identiteter per diagram? Påverkar namnområdesprioriteten den systemdefinierade skyddsprofilen?

Identitetsoptimeringsalgoritmen används först för att säkerställa personentitetsrepresentationen. Om diagrammet därefter försöker överskrida [identitetdiagrammet ](../guardrails.md) (50 identiteter per diagram) används den här logiken. Namnområdesprioriteten påverkar inte borttagningslogiken för det 50 identitets-/diagramskyddsutkastet.

### Testning

#### Vilka scenarier bör jag testa i en utvecklingssandlådemiljö?

Generellt sett bör testning i en utvecklingssandlåda efterlikna de användningsfall som du tänker köra i din produktionssandlåda. I följande tabell finns några viktiga områden att validera vid utförlig testning:

| Testfall | Teststeg | Förväntat resultat |
| --- | --- | --- |
| Korrekt personentitetsrepresentation | <ul><li>Mimisk anonym surfning</li><li>Mimitera två personer (John, Jane) som loggar in med samma enhet</li></ul> | <ul><li>Både John och Jane ska associeras med sina attribut och autentiserade händelser.</li><li>Den senast autentiserade användaren bör kopplas till de anonyma surfhändelserna.</li></ul> |
| Segmentering | Skapa fyra segmentdefinitioner (**Obs!**: Varje segmentdefinitionspar ska ha en utvärderad med hjälp av batch och en annan direktuppspelning.) <ul><li>Segmentdefinition A: Segmentkvalificering baserad på Johns autentiserade händelser.</li><li>Segmentdefinition B: Segmentkvalificering baserad på Jane autentiserade händelser.</li></ul> | Oberoende av scenarier med delade enheter bör John och Jane alltid vara kvalificerade för sina respektive segment. |
| Målgruppskvalifikationer/enhetsresor på Adobe Journey Optimizer | <ul><li>Skapa en resa som börjar med en målgruppskvalifikationsaktivitet (t.ex. den direktuppspelningssegmentering som skapas ovan).</li><li>Skapa en resa som börjar med ett enastående evenemang. Den här enhetshändelsen ska vara en autentiserad händelse.</li><li>Du måste inaktivera återinträde när du skapar dessa resor.</li></ul> | <ul><li>Oberoende av scenarier med delade enheter bör John och Jane utlösa resorna som de ska delta i.</li><li>John och Jane bör inte återkomma till resan när ECID överförs till dem.</li></ul> |

{style="table-layout:auto"}

#### Hur verifierar jag att den här funktionen fungerar som väntat?

Använd [diagramsimuleringsverktyget](./graph-simulation.md) för att verifiera att funktionen fungerar på en enskild diagramnivå.

Om du vill validera funktionen på sandlådenivå ska du läsa avsnittet [!UICONTROL Graph count with multiple namespaces] på identitetspanelen.