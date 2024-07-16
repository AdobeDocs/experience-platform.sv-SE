---
keywords: Experience Platform;hem;populära ämnen;id namespace;Identity namespace
solution: Experience Platform
title: Felsökningsguide för identitetstjänst
description: Det här dokumentet innehåller svar på vanliga frågor om Adobe Experience Platform Identity Service samt en felsökningsguide för vanliga fel.
exl-id: dac31bc3-7003-46d6-9d41-9f6fd3645c2c
source-git-commit: 3fe94be9f50d64fc893b16555ab9373604b62e59
workflow-type: tm+mt
source-wordcount: '2166'
ht-degree: 0%

---

# Felsökningsguide för identitetstjänst

Det här dokumentet innehåller svar på vanliga frågor om Adobe Experience Platform [!DNL Identity Service] samt en felsökningsguide för vanliga fel. Mer information och felsökning om [!DNL Platform] API:er i allmänhet finns i [felsökningsguiden för Adobe Experience Platform API](../landing/troubleshooting.md).

Data som identifierar en enskild kund fragmenteras ofta över olika enheter och system som de använder för att interagera med ert varumärke. [!DNL Identity Service] samlar ihop dessa fragmenterade identiteter och underlättar en fullständig förståelse för kundbeteenden så att ni kan leverera slagkraftiga digitala upplevelser i realtid. Mer information finns i [Översikt över identitetstjänsten](./home.md).

## Vanliga frågor och svar

Nedan följer en lista med svar på vanliga frågor om [!DNL Identity Service].

## Vad är identitetsdata?

Identitetsuppgifter är alla data som kan användas för att identifiera en enskild person. Beroende på hur data används inom organisationen kan identitetsdata innehålla användarnamn, e-postadresser och ID:n från CRM-system. Identitetsdata är inte begränsade till registrerade användare av din webbplats eller tjänst, eftersom anonyma användare också kan identifieras med deras enhets- eller cookie-ID.

## Vad är fördelen med att märka datafält som identiteter?

Genom att sätta etiketter på vissa datafält som identiteter i data för post- och tidsserier kan du mappa identitetsrelationer inom den naturliga datastrukturen och stämma av duplicerade data i olika kanaler. Mer information finns i [Översikt över identitetstjänsten](./home.md).

## Vad är kända och anonyma identiteter?

En känd identitet avser ett identitetsvärde som kan användas fristående eller tillsammans med annan information för att identifiera, kontakta eller hitta en enskild person. Exempel på kända identiteter kan vara e-postadresser, telefonnummer och CRM-ID.

En anonym identitet refererar till ett identitetsvärde som inte kan användas fristående eller tillsammans med annan information för att identifiera, kontakta eller hitta en enskild person (till exempel ett cookie-ID).

## Vad är ett privat identitetsdiagram?

Ett privat identitetsdiagram är en privat karta över relationer mellan sammanfogade och länkade identiteter, som bara är synlig för din organisation.

När fler än en identitet ingår i data som har importerats från en direktuppspelningsslutpunkt eller skickats till en datauppsättning som har aktiverats för [!DNL Identity Service], länkas dessa identiteter i det privata identitetsdiagrammet. [!DNL Identity Service] använder det här diagrammet för att identifiera en viss konsument eller enhet, vilket möjliggör sammanslagning av identiteter och profiler.

## Hur skapar jag flera identitetsfält i ett XDM-schema?

[XDM-scheman (Experience Data Model)](../xdm/home.md) har stöd för flera identitetsfält. Alla datafält av typen `string` i ett schema som implementerar den enskilda XDM-profilen eller XDM ExperienceEvent-klassen kan märkas som ett identitetsfält. När de har etiketterats läggs alla data i dessa fält till i profilens identitetskarta.

Anvisningar om hur du etiketterar ett XDM-fält som ett identitetsfält med användargränssnittet finns i avsnittet [Identitet](../xdm/tutorials/create-schema-ui.md) i schemaredigerarens självstudiekurs. Om du använder API:t kan du läsa avsnittet [Identitetsbeskrivare](../xdm/tutorials/create-schema-api.md) i API-självstudiekursen för schemaregistret.

## Finns det kontexter där vissa fält inte ska märkas som identiteter?

Identitetsfält ska reserveras för värden som är unika för varje individ. Ta till exempel en datauppsättning för ett kundlojalitetsprogram. Fältet &quot;lojalitetsnivå&quot; (guld, silver, brons) skulle inte vara ett användbart identitetsfält, medan det skulle vara ett unikt ID.

Fält som ZIP-koder och IP-adresser ska inte märkas som identiteter för enskilda, eftersom dessa värden kan gälla för mer än en enskild person. Dessa typer av fält bör endast märkas som identiteter för marknadsföringsstrategier på hushållsnivå.

## Varför länkar inte mina identitetsfält på det sätt jag förväntar mig?

Med [`/cluster/members`-slutpunkten ](./api/list-cluster-identites.md) i identitetstjänstens API kan du visa associerade identiteter för ett eller flera identitetsfält. Om svaret inte returnerar de länkade identiteter som du förväntar dig ska du se till att du anger rätt identitetsinformation i dina XDM-data. Mer information finns i avsnittet [Tillhandahålla XDM-data till identitetstjänsten](./home.md) i översikten för identitetstjänsten.

## Vad är ett identitetsnamnutrymme?

Ett ID-namnutrymme ger kontext för hur identitetsfält relaterar till en kunds identitet. Identitetsfält under namnutrymmet&quot;E-post&quot; ska till exempel överensstämma med ett standardformat för e-post (namn <span>@emailprovider.com) medan fält som använder namnutrymmet&quot;Telefon&quot; ska överensstämma med ett standardtelefonnummer (till exempel 987-555-1234 i Nordamerika).

Namnutrymmen skiljer på liknande identitetsvärden mellan olika CRM-system. Ta till exempel en profil som innehåller ett numeriskt lojalitets-ID som är kopplat till ditt företags belöningsprogram. Ett namnutrymme med &quot;Loyalty&quot; skulle separera det här värdet från ett liknande numeriskt ID för e-handelssystemet som också visas i samma profil.

Mer information finns i [översikten över identitetsnamnområdet](./home.md).

## Hur associerar jag en identitet med ett identitetsnamnutrymme?

Identitetsfält måste kopplas till ett befintligt ID-namnutrymme när de skapas. Alla nya namnutrymmen måste vara [skapade med API:t](#how-do-i-create-a-custom-namespace-for-my-organization) innan de kopplas till identitetsfält.

Stegvisa instruktioner om hur du definierar ett namnutrymme när du skapar en identitetsbeskrivning med API:t finns i avsnittet [Skapa en beskrivning](../xdm/tutorials/create-schema-ui.md) i utvecklarhandboken för schemaregister. Om du vill markera ett schemafält som en identitet i användargränssnittet följer du stegen i [schemaredigerarens självstudiekurs](../xdm/tutorials/create-schema-api.md).

## Vilka är de vanliga ID-namnutrymmena från Experience Platform? {#standard-namespaces}

Standardnamnutrymmen för identiteter är namnutrymmen som är tillgängliga för alla organisationer. En fullständig lista över tillgängliga standardnamnutrymmen finns i [Översikt över identitetsnamnutrymmen](./features/namespaces.md).

## Var hittar jag en lista över de identitetsnamnutrymmen som är tillgängliga för min organisation?

Med hjälp av [identitetstjänstens API](https://www.adobe.io/experience-platform-apis/references/identity-service) kan du visa alla tillgängliga identitetsnamnutrymmen för din organisation genom att göra en GET-begäran till `/idnamespace/identities`-slutpunkten. Mer information finns i avsnittet [med en lista över tillgängliga namnutrymmen](./api/list-namespaces.md) i API-översikten för identitetstjänsten.

## Hur skapar jag ett anpassat namnutrymme för min organisation?

Med hjälp av [Identitetstjänstens API](https://www.adobe.io/experience-platform-apis/references/identity-service) kan du skapa ett anpassat identitetsnamnutrymme för din organisation genom att göra en POST-förfrågan till `/idnamespace/identities`-slutpunkten. Mer information finns i avsnittet [Skapa ett anpassat namnområde](./api/create-custom-namespace.md) i API-översikten för identitetstjänsten.

## Vad är sammansatta identiteter och XID:n?

Identiteter refereras i API-anrop antingen av deras sammansatta identitet eller XID. En sammansatt identitet är en representation av en identitet som innehåller ett ID-värde och ett namnutrymme. Ett XID är en identifierare med ett enda värde som representerar samma konstruktion som en sammansatt identitet (ett ID och ett namnutrymme), och tilldelas automatiskt till nya identiteter när de bevaras av identitetstjänsten. Mer information finns i [API-översikten för identitetstjänsten](./home.md).

## Hur hanterar Identity Service personligt identifierbar information (PII)?

Identitetstjänsten har standardnamnutrymmen som stöder inmatning av hash-kodade identitetsvärden för telefonnummer och e-post. Du ansvarar dock för att värden hash-kodas. Mer information om att hash-koda data som är inkapslade i plattformen finns i [[!DNL Data Prep] handboken om mappningsfunktioner](../data-prep/functions.md#hashing).

## Är det något du bör tänka på när du hash-kodar PII-baserade identiteter?

Om du skickar hash-kodade PII-värden till identitetstjänsten måste du använda samma krypteringsmetod i alla datauppsättningar. Detta garanterar att samma identitetsvärde för alla datauppsättningar genererar samma hash-kodade värden och kan matchas och länkas korrekt i identitetsdiagrammet.

<!-- Documentation does not show any methods of editing the identityMap directly, and this table never overtly recommends using identityMap anyway. This should probably be removed unless PM thinks otherwise. -->
<!-- ## When should I use the Identity map rather than labeling individual XDM schema fields?

The following table describes when the recommended approach for including identity data in your XDM would be identity map and when an identity field is the better method.

>[!NOTE]
>
>An advantage `identityMap` has is the ability to include multiple identity values for a single namespace.

Write|XDM identity field|`identityMap`
---|---|---
UI|Supported|Supported
Developer|Recommended|Supported
ETL|Recommended|Avoid - While this is supported, data should be formatted naturally when using an ETL, favoring identity fields over `identityMap`.
Internal solutions|Preferred|Common

--- -->

## Varför kan jag inte komma åt identitetsdiagramsidan eller API:erna?

Din plattformsadministratör måste tilldela dig behörigheten `view-identity-graph` för att du ska kunna visa data i identitetsdiagram. Utan den här behörigheten får du ett meddelande om nekad behörighet på identitetsdiagramvisningsprogramsidan och när du anropar plattforms-API:er. Mer information om behörigheter finns i [åtkomstkontrollsöversikten](../access-control/home.md).

## Felsökning

Följande avsnitt innehåller felsökningsförslag för specifika felkoder och oväntade beteenden som du kan träffa på när du arbetar med [!DNL Identity Service]-API:t.

## [!DNL Identity Service] felmeddelanden

Nedan följer en lista över felmeddelanden som du kan stöta på när du använder API:t [!DNL Identity Service].

### Obligatorisk frågeparameter saknas

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "Missing required query parameter - namespace"
}
```

Det här felet visas när en obligatorisk frågeparameter inte inkluderades i sökvägen till begäran. Felmeddelandets `detail` innehåller namnet på den parameter som saknas. Variationer i det här felmeddelandet inkluderar:

- Obligatorisk frågeparameter saknas - nsId
- Obligatorisk frågeparameter saknas - id
- Obligatorisk frågeparameter saknas - xid eller (nsid,id)
- Obligatorisk frågeparameter saknas - targetNs
- Obligatorisk frågeparameter saknas - xids eller compositeXids

Kontrollera att du tar med den angivna parametern i sökvägen för begäran innan du försöker igen.

### Tidsstämpeln bör vara inom de senaste 180 dagarna

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "Timestamp should be within last 180 days"
}
```

[!DNL Identity Service] rensar data som är äldre än 180 dagar. Det här felmeddelandet visas när du försöker komma åt data som är äldre än det här.

### Det finns en gräns på 1 000 XID i ett enda samtal

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "There is a limit of 1000 XIDs in a single call"
}
```

Det här felmeddelandet visas när du försöker hämta identitetsinformation för mer än det maximala antalet [XID](#what-are-composite-identities-and-xids) som tillåts i ett enda API-anrop. Minska antalet XID i din begäran till under den gräns som visas för att lösa problemet.


### Det finns en gräns för 1000 compositeXids i ett enskilt anrop

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "There is a limit for 1000 compositeXids in a single call"
}
```

Det här felmeddelandet visas när du försöker hämta identitetsinformation för fler än det maximala antalet [sammansatta identiteter](#what-are-composite-identities-and-xids) som tillåts i ett enda API-anrop. Minska antalet sammansatta identiteter i din begäran till under den gräns som visas för att lösa problemet.

### Den angivna diagramtypen är ogiltig

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "The graph-type abc specified is invalid. Please provide a valid graph-type"
}
```

Det här felmeddelandet visas när en `graph-type`-frågeparameter tilldelas ett ogiltigt värde i sökvägen till begäran. I avsnittet [identitetsdiagram](./home.md) i översikten [!DNL Identity Service] finns information om vilka diagramtyper som stöds.

### Tjänsttoken har inte ett giltigt scope

```json
{
    "title": "UnauthorizedAccess",
    "status": 401,
    "detail": "Service token does not have valid scope. Either acp.core.identity or acp.foundation is required"
}
```

Det här felmeddelandet visas när din organisation inte har tilldelats rätt behörigheter för [!DNL Identity Service]. Kontakta systemadministratören för att lösa problemet.

### Gatewaytjänstens token är inte giltig

```json
{
    "title": "UnauthorizedAccess",
    "status": 401,
    "detail": "Gateway service token is not valid"
}
```

Om det här felet inträffar är din åtkomsttoken ogiltig. Åtkomsttoken upphör att gälla var 24:e timme och måste genereras om för att du ska kunna fortsätta använda [!DNL Platform] API:er. Se självstudiekursen [Autentisering](https://www.adobe.com/go/platform-api-authentication-en) för instruktioner om hur du skapar nya åtkomsttoken.

### Autentiseringstjänsttoken är inte giltig

```json
{
    "title": "UnauthorizedAccess",
    "status": 401,
    "detail": "Authorization service token is not valid"
}
```

Om det här felet inträffar är din åtkomsttoken ogiltig. Åtkomsttoken upphör att gälla var 24:e timme och måste genereras om för att du ska kunna fortsätta använda [!DNL Platform] API:er. Se självstudiekursen [Autentisering](https://www.adobe.com/go/platform-api-authentication-en) för instruktioner om hur du skapar nya åtkomsttoken.

### Användartoken har inte en giltig produktkontext

```json
{
    "title": "UnauthorizedAccess",
    "status": 401,
    "detail": "User token does not have valid product context"
}
```

Det här felmeddelandet visas när din åtkomsttoken inte har genererats från en [!DNL Experience Platform]-integrering. Se självstudiekursen [Autentisering](https://www.adobe.com/go/platform-api-authentication-en) för instruktioner om hur du skapar nya åtkomsttoken för en [!DNL Experience Platform]-integrering.

### Internt fel vid hämtning av ursprungligt XID från identitets- och namnutrymmeskod

```json
{
    "title": "UnauthorizedAccess",
    "status": 401,
    "detail": "Invalid IMS Token/IMS Org | Internal error - when tried to get native XID from identity and namespace code"
}
```

När [!DNL Identity Service] består av en identitet tilldelas ID:t och det associerade namnområdes-ID:t en unik identifierare som kallas XID. Det här meddelandet visas när ett fel inträffar under sökningen efter XID för ett givet ID-värde och namnutrymme.

### IMS-organisationen har inte etablerats för [!DNL Identity Service]-användning

```json
{
    "title": "AccountNotProvisioned",
    "status": 403,
    "detail": "The IMS Org. {IMS_ORG_NAME} is not provisioned for Identity Service usage"
}
```

Det här felmeddelandet visas när din organisation inte har tilldelats rätt behörigheter för [!DNL Identity Service]. Kontakta systemadministratören för att lösa problemet.

### Internt serverfel

```json
{
    "title": "InternalError",
    "status": 500,
    "detail": "Internal Server Error. There was a problem processing your request"
}
```

Det här felet visas när ett oväntat undantag inträffar vid körningen av ett [!DNL Platform]-tjänstanrop. Det bästa sättet är att programmera dina automatiska anrop så att de kan försöka igen några gånger med ett tidsintervall när det här felet tas emot. Kontakta systemadministratören om problemet kvarstår.

## Felkoder för batchinmatning

[!DNL Identity Service] importerar identitetsdata från post- och tidsseriedata som överförs till [!DNL Platform] med hjälp av gruppinmatning. Eftersom gruppinmatning är en asynkron process måste du visa information för en grupp för att kunna se fel. Fel ackumuleras allt eftersom batchen fortskrider tills batchen är klar.

Nedan följer en lista över felmeddelanden som rör [!DNL Identity Service] som du kan stöta på när du använder [API:t för gruppinmatning](https://developer.adobe.com/experience-platform-apis/references/batch-ingestion/).

### Okänt XDM-schema

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "Unknown XDM schema"
}
```

[!DNL Identity Service] använder bara identiteter för post- eller tidsseriedata som uppfyller klasserna [!DNL Profile] respektive [!DNL ExperienceEvent]. Om du försöker importera data för [!DNL Identity Service] som inte är i någon av klasserna utlöses det här felet.

### Det fanns 0 giltiga identiteter i de första 100 raderna i den bearbetade gruppen

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "There were 0 valid identities in the first 100 rows of the processed batch"
}
```

Det här felet visas när de första 100 raderna i en batch inte visade några identiteter. Detta fel innebär dock inte att inga identiteter hittades i efterföljande poster.

### Poster hoppades över eftersom de bara hade en identitet per XDM-post

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "Skipped {NUMBER_OF_RECORDS} records as they had only 1 identity per XDM record"
}
```

[!DNL Identity Service] länkar bara identiteter när enskilda poster har två eller flera identitetsvärden. Det här felmeddelandet visas en gång för varje inkapslad sats och visar antalet poster där endast en identitet kunde hittas och som inte resulterade i någon ändring av identitetsdiagrammet.

### Namnområdeskoden har inte registrerats för denna IMS-organisation

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "Namespace Code {ERRONEOUS_CODE} is not registered for this IMS Org"
}
```

Det här felet visas när en inkapslad post visar en identitet vars associerade namnutrymme inte finns eller inte är tillgängligt för din organisation.

### Hoppar över batchinmatning eftersom IMS-organisation inte har etablerats för privat identitetsdiagram

```json
{
    "title": "AccountNotProvisioned",
    "status": 403,
    "detail": "Skipping batch ingestion as IMS Org is not provisioned for Private Identity Graph"
}
```

Vid inhämtning av batchdata visas det här felmeddelandet när din organisation inte har tilldelats rätt behörigheter för [!DNL Identity Service]. Kontakta systemadministratören för att lösa problemet.

### Internt fel

```json
{
    "title": "InternalError",
    "status": 500,
    "detail": "Internal Error. There was a problem during the ingestion"
}
```

Det här felet visas när ett oväntat undantag inträffar under en gruppinmatning. Det bästa sättet är att programmera dina automatiska anrop så att de kan försöka igen några gånger med ett tidsintervall när det här felet tas emot. Kontakta systemadministratören om problemet kvarstår.
