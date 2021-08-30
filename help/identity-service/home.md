---
keywords: Experience Platform;hem;populära ämnen;identitet;Identitet;XDM-diagram;identitetstjänst;Identitetstjänst
solution: Experience Platform
title: Översikt över identitetstjänsten
topic-legacy: overview
description: Adobe Experience Platform identitetstjänst hjälper er att få en bättre bild av era kunder och deras beteende genom att skapa en bro mellan identiteter på olika enheter och system, så att ni kan leverera slagkraftiga, personliga digitala upplevelser i realtid.
exl-id: a22dc3f0-3b7d-4060-af3f-fe4963b45f18
source-git-commit: 947d8803416cee584b35a8d480929e2684d0057f
workflow-type: tm+mt
source-wordcount: '1807'
ht-degree: 0%

---

# [!DNL Identity Service] översikt

För att kunna leverera relevanta digitala upplevelser måste ni ha en fullständig förståelse för era kunder. Detta blir svårare när era kunddata fragmenteras över olika system, vilket gör att varje enskild kund ser ut att ha flera&quot;identiteter&quot;.

Adobe Experience Platform identitetstjänst ger er en heltäckande bild av era kunder och deras beteende genom att skapa en bro mellan identiteter på olika enheter och system, så att ni kan leverera slagkraftiga, personliga digitala upplevelser i realtid.

Med [!DNL Identity Service] kan du:

- Se till att era kunder får en enhetlig, personaliserad och relevant upplevelse genom varje interaktion.
- Sammanfoga flera olika identiteter från olika källor och skapa en heltäckande bild av era kunder.
- Använd ett identitetsdiagram för att mappa olika identitetsnamnutrymmen, vilket ger en visuell representation av hur kunderna interagerar med ert varumärke i olika kanaler.

## Komma igång

Innan du börjar gå in på detaljerna i [!DNL Identity Service] är det här en kort sammanfattning av nyckeltermerna:

| Term | Definition |
| --- | --- |
| Identitet | En identitet är data som är unika för en enhet, vanligtvis en enskild person. En identitet, t.ex. ett inloggnings-ID, ECID eller lojalitets-ID, kallas också för en&quot;känd identitet&quot;. |
| ECID | Experience Cloud ID (ECID) är ett delat ID-namnutrymme som används i Experience Platform- och Adobe Experience Cloud-program. ECID utgör grunden för kundidentiteten och används som primärt ID för enheter och som basnod för identitetsdiagram. Mer information finns i [ECID-översikt](./ecid.md). |
| Namnutrymme för identitet | Ett identitetsnamnutrymme används för att skilja på kontexten eller typen för en identitet. En identitet särskiljer till exempel&quot;name<span>@email.com&quot; som en e-postadress eller&quot;443522&quot; som ett numeriskt CRM-ID. Identitetsnamnutrymmen används för att leta upp enskilda identiteter och ange kontext för identitetsvärden. På så sätt kan du bestämma att två [!DNL Profile]-fragment som innehåller olika primära ID:n, men delar samma värde för `email`-identitetens namnutrymme, faktiskt är samma individ. Mer information finns i [översikten över identitetsnamnrymden](./namespaces.md). |
| Identitetsdiagram | Ett identitetsdiagram är en karta över relationer mellan olika identiteter, som gör att du kan visualisera och bättre förstå vilka kundidentiteter som sammanfogas, och hur. Mer information finns i självstudiekursen om [användning av identitetsdiagramvisningsprogrammet](./ui/identity-graph-viewer.md). |
| Personligt identifierbar information (PII) | PII är information som direkt kan identifiera en kund, till exempel en e-postadress eller ett telefonnummer. PII-värden används ofta för att matcha. en kunds olika identiteter i olika system. |
| Unik identitet | En unik identitet är en identitet som bara finns i en viss sandlåda. |
| Okända eller anonyma identiteter | Okända eller anonyma identiteter är indikatorer som isolerar enheter utan att identifiera den person som använder enheten. Okända och anonyma identiteter innehåller information som besökarens IP-adress och cookie-ID. Även om okända och anonyma identiteter kan tillhandahålla beteendedata, begränsas de tills en kund levererar sina PII-filer. |

## Vad är [!DNL Identity Service]?

Varje dag interagerar kunderna med ert företag och skapar en ständigt växande relation med ert varumärke. En typisk kund kan vara aktiv i valfritt antal system i organisationens datainfrastruktur, t.ex. e-handel, lojalitet och helpdesk-system. Samma kund kan även engagera anonymt på valfritt antal enheter. [!DNL Identity Service] gör att ni kan sammanställa en komplett bild av kunden och sammanställa relaterade data som annars skulle kunna isoleras mellan olika system.

Ett exempel på hur en konsument kan kommunicera med ert varumärke varje dag:

- Mary har ett konto på din e-handelsplats där hon har gjort några beställningar tidigare. Hon använder vanligtvis sin egen bärbara dator för att handla, där hon loggar in varje gång. Men under ett av hennes besök använder hon sin surfplatta för att handla sandaler, men lägger ingen order och loggar inte in.
- Nu visas Marys aktivitet som två separata profiler:
   - Hennes e-handelsinloggning
   - Hennes surfplatta kanske identifieras med enhets-ID
- Mary återupptar sin surfplattesession och anger sin e-postadress när han/hon prenumererar på ditt nyhetsbrev. När du gör det läggs en ny identitet till som postdata i profilen. Därför relaterar [!DNL Identity Service] nu Marys aktivitet för surfplattor till hennes historik för e-handelskonton.
- Nästa gång du klickar på hennes surfplatta kan målinnehållet återspegla Marys fullständiga profil och historia, i stället för bara en surfplatta som används av en okänd köpare.

![Identitetssammanfogning på plattform](./images/identity-service-stitching.png)

Med [!DNL Identity Service] kan ni sammanfoga en fullständig bild av kunden och samla ihop relaterade data som annars skulle kunna vara spridda över olika system. De identitetsrelationer som definieras och upprätthålls av kundprofilen i realtid för att skapa en komplett bild av kunden och deras interaktioner med ert varumärke. [!DNL Identity Service] Mer information finns i [Översikt över kundprofilen i realtid](../profile/home.md).

### Användningsfall

Exempel på [!DNL Identity Service]-implementeringar är:

- Ett telekomföretag kan förlita sig på värdet för&quot;telefonnummer&quot;, där ett telefonnummer hänvisar till samma person i intresse både offline och online.
- Ett detaljhandelsföretag kan använda&quot;e-postadress&quot; i offline-datauppsättningar och ECID i online-datauppsättningar på grund av den stora andelen anonyma besökare.
- En bank kan föredra&quot;kontonummer&quot; i offlinedatauppsättningar, t.ex. filialtransaktioner. De kan vara beroende av&quot;inloggnings-ID&quot; i onlinedatauppsättningar, eftersom de flesta besökare autentiseras under besöket.
- Dina kunder kan också ha unika egna ID:n, som GUID eller andra universellt unika ID:n.

## Identitetsnamnutrymmen

Om du frågade en person&quot;Vad är ditt ID?&quot; utan vidare sammanhang skulle det vara svårt för dem att ge ett användbart svar. Med samma logik är ett strängvärde som representerar ett identitetsvärde, oavsett om det är ett systemgenererat ID eller en e-postadress, endast fullständigt när det levereras med en kvalificerare som ger strängvärdeskontexten: identitetsnamnutrymmet.


Era kunder kan interagera med ert varumärke genom en kombination av online- och offlinekanaler, vilket kan vara en utmaning när det gäller att kombinera dessa fragmenterade interaktioner med en enda kundidentitet.

Förståelse för kunden i flera olika enheter och kanaler börjar med att känna igen dem i varje kanal. Plattformen uppnår detta genom att använda ID-namnutrymmen. Ett identitetsnamnutrymme är en identifierare, till exempel E-post eller Telefon, som används för att skapa ytterligare kontext för kundidentiteter. Identitetsnamnutrymmen används för att söka efter eller länka enskilda identiteter och ange kontext för identitetsvärden. Mer information finns i [översikten över identitetsnamnrymden](./namespaces.md).

## Identitetsdiagram

Ett identitetsdiagram är en karta över relationer mellan olika identitetsnamnutrymmen som gör att du kan visualisera och bättre förstå vilka kundidentiteter som sammanfogas, och hur. Mer information finns i självstudiekursen om [användning av identitetsdiagramvisningsprogrammet](./ui/identity-graph-viewer.md).

Följande video är avsedd att ge stöd för din förståelse av identiteter och identitetsdiagram. Det täcker de tre funktionerna för identitetssamling, identitetsdiagram och API. Här beskrivs också hur deterministiska och sannolikhetsalgoritmer används för att skapa privata identitetsdiagram, och deras roll behandlas tillsammans med tredjepartsdiagram och Adobe Experience Platform Identity Service Co-Op Graph.

>[!VIDEO](https://video.tv.adobe.com/v/27841?quality=12&learn=on)

## Identitetsdata skickas till [!DNL Identity Service]

I det här avsnittet beskrivs hur data som skickas till Adobe Experience Platform behandlas innan de används av [!DNL Identity Service] för att skapa ett identitetsdiagram för varje kund.

### Bestäm dig för identitetsfält

Beroende på er strategi för insamling av företagsdata avgör de datafält som du anger som identiteter vilka data som inkluderas i identitetskartan. För att få ut så mycket som möjligt av Adobe Experience Platform och de mest omfattande kundidentiteterna bör du ladda upp både online- och offlinedata.

- Onlinedata är data som beskriver närvaro och beteende online, t.ex. användarnamn och e-postadresser.

- Offlinedata avser data som inte är direkt relaterade till onlinenärvaro, t.ex. ID:n från CRM-system. Den här typen av data gör era identiteter mer robusta och stöder datamedlemskap i olika system.

### Skapa ytterligare identitetsnamnutrymmen

Experience Platform har en mängd standardnamnutrymmen, men du kan behöva skapa ytterligare namnutrymmen för att kategorisera dina identiteter ordentligt. Mer information finns i avsnittet [visa och skapa namnutrymmen för din organisation](./namespaces.md) i översikten över namnutrymmet identity.

>[!NOTE]
>
>Identitetsnamnutrymmen är en kvalificerare för identiteter. Därför kan ett namnutrymme inte tas bort när det väl har skapats.

### Inkludera identitetsdata i [!DNL Experience Data Model] (XDM)

Som det standardiserade ramverket som [!DNL Platform] organiserar kunddata med, tillåter [!DNL Experience Data Model] (XDM) att data delas och tolkas mellan Experience Platform och andra tjänster som interagerar med [!DNL Platform]. Mer information finns i [XDM-systemöversikt](../xdm/home.md).

Både schema för inspelnings- och tidsserier ger möjlighet att inkludera identitetsdata. När data importeras skapar identitetsdiagrammet nya relationer mellan datafragment från olika namnutrymmen om de visar sig dela gemensamma identitetsdata.

### Markera XDM-fält som identitet

Alla fält av typen `string` i scheman som implementerar antingen post- eller tidsseriens XDM-klasser kan märkas som ett identitetsfält. Därför betraktas alla data som hämtas in till det fältet som identitetsdata.

>[!NOTE]
>
>Array- och mappningstypsfält stöds inte och kan inte markeras och märkas som identitetsfält.

I identitetsfält går det också att länka identiteter om de delar gemensamma PII-data.
Genom att exempelvis etikettera telefonnummerfält som identitetsfält, så skapar [!DNL Identity Service] automatiskt relationer med andra personer som använder samma telefonnummer.

>[!NOTE]
>
>Namnutrymmet för resulterande identiteter anges när fältet etiketteras.

### Konfigurera en datauppsättning för [!DNL Identity Service]

Under direktuppspelningsprocessen hämtar [!DNL Identity Service ]automatiskt identitetsdata från post- och tidsseriedata. Innan data kan importeras måste de dock aktiveras för [!DNL Identity Service]. Mer information finns i självstudiekursen [Konfigurera en datauppsättning för kundprofil och identitetstjänst i realtid med API:er](../profile/tutorials/dataset-configuration.md).

### Infoga data till [!DNL Identity Service]

[!DNL Identity Service] förbrukar XDM-kompatibla data som skickas till Experience Platform antingen via  [batchinmatning ](../ingestion/batch-ingestion/overview.md) eller  [direktuppspelning](../ingestion/streaming-ingestion/overview.md).

Följande video är avsedd att ge stöd för din förståelse av identitetstjänsten. I den här videon visas hur du kan märka datafält som identiteter, importera identitetsdata och sedan verifiera att data har skickats till Adobe Experience Platform Identity Service Private Graph.

>[!WARNING]
>
>Användargränssnittet [!DNL Platform] som visas i följande video är inaktuellt. Läs dokumentationen om de senaste skärmbilderna och funktionerna i användargränssnittet.

>[!VIDEO](https://video.tv.adobe.com/v/28167?quality=12&learn=on)

## Datastyrning

Adobe Experience Platform har byggts med sekretess i åtanke och innehåller ett ramverk för datastyrning som skyddar kundernas PII-data. Identitetsdata under namnutrymmet&quot;email&quot; eller&quot;phone&quot; krypteras som standard, men för att säkerställa att känsliga data krypteras innan de bevaras kan dataanvändningsetiketter tillämpas på data när de importeras eller när de kommer in i [!DNL Platform]. Mer information finns i [översikten över datastyrning](../data-governance/home.md).

## Nästa steg

Nu när du förstår de viktigaste begreppen för [!DNL Identity Service] och dess roll i Experience Platform kan du börja lära dig hur du arbetar med identitetsdiagrammet med [[!DNL Identity Service API]](./api/getting-started.md).
