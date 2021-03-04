---
keywords: Experience Platform;hem;populära ämnen;identitet;Identitet;XDM-diagram;identitetstjänst;Identitetstjänst
solution: Experience Platform
title: Översikt över identitetstjänsten
topic: översikt
description: Adobe Experience Platform identitetstjänst hjälper er att få en bättre bild av era kunder och deras beteende genom att skapa en bro mellan identiteter på olika enheter och system, så att ni kan leverera slagkraftiga, personliga digitala upplevelser i realtid.
translation-type: tm+mt
source-git-commit: 126b3d1cf6d47da73c6ab045825424cf6f99e5ac
workflow-type: tm+mt
source-wordcount: '1733'
ht-degree: 0%

---


# [!DNL Identity Service] översikt

För att kunna leverera relevanta digitala upplevelser måste ni ha en fullständig förståelse för era kunder. Detta blir svårare när era kunddata fragmenteras över olika system, vilket gör att varje enskild kund ser ut att ha flera&quot;identiteter&quot;. Adobe Experience Platform [!DNL Identity Service] hjälper er att få en bättre bild av era kunder och deras beteende genom att skapa en bro mellan identiteter på olika enheter och system, så att ni kan leverera slagkraftiga, personliga digitala upplevelser i realtid.

## Förstå [!DNL Identity Service]

Varje dag interagerar kunderna med ert företag och skapar en ständigt växande relation med ert varumärke. En typisk kund kan vara aktiv i valfritt antal system i organisationens datainfrastruktur, t.ex. e-handel, lojalitet och helpdesk-system. Samma kund kan även engagera anonymt på valfritt antal enheter. [!DNL Identity Service] gör att ni kan sammanställa en komplett bild av kunden och sammanställa relaterade data som annars skulle kunna isoleras mellan olika system.

Ett exempel på hur en konsument kan kommunicera med ert varumärke varje dag:

Mary har ett konto på din e-handelsplats där hon har gjort några beställningar tidigare. Hon använder vanligtvis sin egen bärbara dator för att handla, där hon loggar in varje gång. Men under ett av hennes besök använder hon sin surfplatta för att handla sandaler, men lägger ingen order och loggar inte in.

Nu visas Marys aktivitet som två separata profiler: hennes e-handelsinloggning och hennes surfplatteenhet, kanske identifierad med enhets-ID.

Mary återupptar sin surfplattesession och anger sin e-postadress när han/hon prenumererar på ditt nyhetsbrev. När du gör det läggs en ny identitet till som postdata i profilen. Därför relaterar [!DNL Identity Service] nu Marys aktivitet för surfplattor till hennes historik för e-handelskonton.

Nästa gång du klickar på hennes surfplatta kan målinnehållet återspegla Marys fullständiga profil och historia, i stället för bara en surfplatta som används av en okänd köpare.

Identitetsrelationerna som definieras och upprätthålls av [!DNL Identity Service] utnyttjas av [!DNL Real-time Customer Profile] för att skapa en fullständig bild av en kund och deras interaktioner med ert varumärke. Mer information finns i [Översikt över kundprofilen i realtid](../profile/home.md).

### Identiteter

En identitet är data som är unika för en enhet, vanligtvis en enskild person. En identitet som ett inloggnings-ID, ECID eller lojalitets-ID kallas en känd identitet.

PII, som e-postadress och telefonnummer, används för att identifiera en kund direkt. Resultatet blir att PII-kod används för att matcha en kunds olika identiteter i olika system.

Okända eller anonyma identiteter singlar ut en enhet utan att identifiera den person som använder den. Den här kategorin innehåller information som en besökares IP-adress och cookie-ID. Beteendedata kan samlas in från en enhet med hjälp av okända identiteter, men att koppla dessa identiteter till olika enheter eller medier är begränsat tills kunden tillhandahåller PII under resan.

Som framgår av bilden nedan är både kända och anonyma identiteter viktiga komponenter i [identitetsdiagram](#identity-graphs), som beskrivs senare i det här dokumentet.

![Identitetssammanfogning på plattform](./images/identity-service-stitching.png)

Exempel på [!DNL Identity Service]-implementeringar är:

- Ett telekomföretag kan förlita sig på värdet för&quot;telefonnummer&quot;, där ett telefonnummer hänvisar till samma person i intresse både offline och online.
- Ett detaljhandelsföretag kan använda&quot;e-postadress&quot; i offline-datauppsättningar och ECID i online-datauppsättningar på grund av den stora andelen anonyma besökare.
- En bank kan föredra&quot;kontonummer&quot; i offlinedatauppsättningar, t.ex. filialtransaktioner. De kan vara beroende av&quot;inloggnings-ID&quot; i onlinedatauppsättningar, eftersom de flesta besökare autentiseras under besöket.
- Dina kunder kan också ha unika egna ID:n, som GUID eller andra universellt unika ID:n.

### Identitetsdata

Om du frågade en person&quot;Vad är ditt ID?&quot; utan vidare sammanhang skulle det vara svårt för dem att ge ett användbart svar. Med samma logik är ett strängvärde som representerar ett identitetsvärde, oavsett om det är ett systemgenererat ID eller en e-postadress, endast fullständigt när det levereras med en kvalificerare som ger strängvärdeskontexten: identitetsnamnutrymmet.

## Identitetsnamnutrymmen och identitetsdiagram

Era kunder kan interagera med ert varumärke genom en kombination av online- och offlinekanaler, vilket kan leda till en utmaning i att förena dessa fragmenterade interaktioner med en enda kundidentitet.

[!DNL Experience Platform] löser detta problem på två sätt:  [identitetsnamnutrymmen ](#identity-namespaces) och  [identitetsdiagram](#identity-graphs).

Följande video är avsedd att ge stöd för din förståelse av identiteter och identitetsdiagram. I följande video visas de tre funktionerna i Identity Collection, Identity Graphs och API:erna. Här beskrivs också hur deterministiska och sannolikhetsalgoritmer används för att konstruera privata identitetsdiagram och beskriver rollen för privata identitetsdiagram, Adobe Experience Platform Identity Service Co-Op Graph och tredjepartsdiagram.

>[!IMPORTANT]
>
> Sannolikheten för privata diagram är fortfarande under utveckling och kommer att släppas vid ett senare datum.

>[!VIDEO](https://video.tv.adobe.com/v/27841?quality=12&learn=on)

### Identitetsnamnutrymmen

När kunden interagerar med ert varumärke i flera kanaler, inklusive webben, mobilappar, callcenter eller en butik, kan det vara svårt att förstå och serva dem om ni inte kan observera och spåra deras aktivitet i alla kanaler.

Förståelse för kunden i flera olika enheter och kanaler börjar med att känna igen dem i varje kanal. Adobe Experience Platform uppnår detta genom att använda ID-namnutrymmen.
Ett identitetsnamnutrymme är en identifierare, t.ex. enhets-ID eller e-post-ID, som används för att ange från vilket sammanhang data kommer. Identitetsnamnutrymmen används för att söka efter eller länka enskilda identiteter och för att tillhandahålla kontext för identitetsvärden för att förhindra datakonflikter. ID:t&quot;123456&quot; kan till exempel avse en person i ditt eCommerce-system och en annan person i ditt helpdesk-system. Mer information finns i [översikten över identitetsnamnrymden](./namespaces.md).

### Identitetsdiagram

Ett identitetsdiagram är en karta över relationer mellan olika identitetsnamnutrymmen, som ger dig en visuell representation av hur kunden interagerar med varumärket i olika kanaler.

Alla kundidentitetsdiagram hanteras och uppdateras gemensamt av [!DNL Identity Service] i nära realtid som svar på kundaktivitet.

[!DNL Identity Service] hanterar ett identitetsdiagram som bara är synligt för din organisation och som bygger på dina data, kallas för det privata diagrammet. [!DNL Identity Service] förbättrar det privata diagrammet när en inkapslad datapost innehåller mer än en identitet, vilket lägger till en relation mellan de identifierade identiteterna.

Som ett exempel på möjliga typer av faktorer som du bör tänka på när du anger och etiketterar identitetsdata, kan användning av telefonnummer som &quot;arbetstelefon&quot; resultera i fler relationer än du tänkt dig i identitetsdiagrammet. Det kan finnas många anställda som hänvisar till samma nummer för arbetet, och att&quot;hem&quot; och&quot;mobil&quot; fungerar bättre för att hålla relationerna så exakta som möjligt.

Mer information finns i självstudiekursen om [åtkomst till identitetsdiagramvisningsprogrammet](./ui/identity-graph-viewer.md)

## Identitetsdata skickas till [!DNL Identity Service]

I det här avsnittet beskrivs hur data som skickas till Adobe Experience Platform behandlas innan de används av [!DNL Identity Service] för att skapa ett identitetsdiagram för varje kund.

### Bestäm dig för identitetsfält

Beroende på er strategi för insamling av företagsdata avgör de datafält som du anger som identiteter vilka data som inkluderas i identitetskartan. För att få ut så mycket som möjligt av Adobe Experience Platform och de mest omfattande kundidentiteterna bör du ladda upp både online- och offlinedata.

- Onlinedata är data som beskriver närvaro och beteende online, t.ex. användarnamn och e-postadresser.

- Offlinedata avser data som inte är direkt relaterade till onlinenärvaro, t.ex. ID:n från CRM-system. Den här typen av data gör era identiteter mer robusta och stöder datamedlemskap i olika system.

### Skapa ytterligare identitetsnamnutrymmen

[!DNL Experience Platform] har en mängd standardnamnutrymmen, men du kan behöva skapa ytterligare namnutrymmen för att kategorisera dina identiteter korrekt. Mer information finns i avsnittet [visa och skapa namnutrymmen för din organisation](./namespaces.md) i översikten över namnutrymmet identity.

>[!NOTE]
>
>Identitetsnamnutrymmen är en kvalificerare för identiteter. Därför kan ett namnutrymme inte tas bort när det väl har skapats.

### Inkludera identitetsdata i [!DNL Experience Data Model] (XDM)

Som det standardiserade ramverket som [!DNL Platform] organiserar kunddata med, tillåter [!DNL Experience Data Model] (XDM) att data delas och tolkas över [!DNL Experience Platform] och andra tjänster som interagerar med [!DNL Platform]. Mer information finns i [XDM-systemöversikt](../xdm/home.md).

Både schema för inspelnings- och tidsserier ger möjlighet att inkludera identitetsdata. När data importeras skapar identitetsdiagrammet nya relationer mellan datafragment från olika namnutrymmen om de visar sig dela gemensamma identitetsdata.

### Markera XDM-fält som identitet

Alla fält av typen `string` i scheman som implementerar antingen post- eller tidsseriens XDM-klasser kan märkas som ett identitetsfält. Därför betraktas alla data som hämtas in till det fältet som identitetsdata.

I identitetsfält går det också att länka identiteter om de delar gemensamma PII-data.
Genom att exempelvis etikettera telefonnummerfält som identitetsfält, så skapar [!DNL Identity Service] automatiskt relationer med andra personer som använder samma telefonnummer.

>[!NOTE]
>
>Namnutrymmet för resulterande identiteter anges när fältet etiketteras.

### Konfigurera en datauppsättning för [!DNL Identity Service]

Under direktuppspelningsprocessen hämtar [!DNL Identity Service ]automatiskt identitetsdata från post- och tidsseriedata. Innan data kan importeras måste de dock aktiveras för [!DNL Identity Service]. Mer information finns i självstudiekursen [Konfigurera en datauppsättning för kundprofil och identitetstjänst i realtid med API:er](../profile/tutorials/dataset-configuration.md).

### Infoga data till [!DNL Identity Service]

[!DNL Identity Service] förbrukar XDM-kompatibla data som skickas till  [!DNL Experience Platform] antingen via  [batchinmatning ](../ingestion/batch-ingestion/overview.md) eller  [direktuppspelning](../ingestion/streaming-ingestion/overview.md).

Följande video är avsedd att ge stöd för din förståelse av identitetstjänsten. I den här videon visas hur du kan märka datafält som identiteter, importera identitetsdata och sedan verifiera att data har skickats till Adobe Experience Platform Identity Service Private Graph.

>[!WARNING]
>
>Användargränssnittet [!DNL Platform] som visas i följande video är inaktuellt. Läs dokumentationen om de senaste skärmbilderna och funktionerna i användargränssnittet.

>[!VIDEO](https://video.tv.adobe.com/v/28167?quality=12&learn=on)

## Datastyrning

Adobe Experience Platform har byggts med sekretess i åtanke och innehåller ett ramverk för datastyrning som skyddar kundernas PII-data. Identitetsdata under namnutrymmet&quot;email&quot; eller&quot;phone&quot; krypteras som standard, men för att säkerställa att känsliga data krypteras innan de bevaras kan dataanvändningsetiketter tillämpas på data när de importeras eller när de kommer in i [!DNL Platform]. Mer information finns i [översikten över datastyrning](../data-governance/home.md).

## Nästa steg

Nu när du förstår de viktigaste begreppen i [!DNL Identity Service] och dess roll i [!DNL Experience Platform] kan du börja lära dig hur du arbetar med identitetsdiagrammet med [[!DNL Identity Service API]](./api/getting-started.md).
