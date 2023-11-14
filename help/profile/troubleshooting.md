---
keywords: Experience Platform;profil;kundprofil i realtid;felsökning;API
title: Felsökningsguide för kundprofiler i realtid
type: Documentation
description: Det här dokumentet innehåller svar på vanliga frågor om kundprofilen i realtid samt en felsökningsguide för vanliga fel när du arbetar med profildata med Adobe Experience Platform.
exl-id: 0b340025-093b-41e4-8053-969a8e80e889
source-git-commit: 8ae18565937adca3596d8663f9c9e6d84b0ce95a
workflow-type: tm+mt
source-wordcount: '1003'
ht-degree: 0%

---

# Felsökningsguide för kundprofiler i realtid

Det här dokumentet innehåller svar på vanliga frågor om kundprofilen i realtid samt en felsökningsguide för vanliga fel. För frågor och felsökning som rör andra tjänster i Adobe Experience Platform, se [Felsökningsguide för Experience Platform](../landing/troubleshooting.md).

Med [!DNL Real-Time Customer Profile]kan ni få en helhetsbild av varje enskild kund genom att kombinera data från flera kanaler, inklusive online, offline, CRM och tredje part. Detta gör att marknadsförarna kan skapa samordnade, enhetliga och relevanta kundupplevelser i flera kanaler.

## Vanliga frågor och svar

Nedan följer en lista med svar på vanliga frågor om kundprofilen i realtid.

### Vilka typer av data accepteras för kundprofilen i realtid?

Profilen godkänner båda **record** och **tidsserie** data, förutsatt att uppgifterna i fråga innehåller minst ett identitetsvärde som associerar data med en unik enskild person.

Precis som alla plattformstjänster kräver Profile att data i profilen ska vara semantiskt strukturerade under ett XDM-schema (Experience Data Model). Det här schemat måste i sin tur ha en **primär identitet** definieras och aktiveras för användning i profilen.

Om du inte känner till XDM kan du börja med [XDM - översikt](../xdm/home.md) om du vill veta mer. Läs sedan användarhandboken för XDM om hur du [ange identitetsfält](../xdm/tutorials/create-schema-ui.md#identity-field) och [aktivera ett schema för profil](../xdm/tutorials/create-schema-ui.md#profile).

### Var lagras profildata?

Kundprofilen i realtid underhåller ett eget datalager (kallas&quot;profilarkiv&quot;) som är skilt från datasjön som innehåller andra inkapslade plattformsdata.

### Om jag redan har inhämtat data till Platform, kan jag göra dem tillgängliga i profilbutiken?

Om data har importerats till en datauppsättning som inte är en profildatauppsättning måste du importera dessa data på nytt till en profilaktiverad datauppsättning för att kunna göra dem tillgängliga i profilarkivet. Det går att aktivera en befintlig datauppsättning för profilen, men alla data som har importerats före den konfigurationen visas fortfarande inte i profilarkivet.

Om du vill lägga till tidigare importerade data i profilarkivet följer du [självstudiekurs om konfiguration av datauppsättning](./tutorials/dataset-configuration.md) för att skapa en ny datauppsättning eller konvertera en befintlig datauppsättning som ska aktiveras för profilen och sedan importera önskade data till datauppsättningen igen.

### Hur kan jag visa mina inkapslade profildata?

Det finns flera sätt att visa profildata, beroende på om du använder API:t eller gränssnittet.

#### Använda API:et

Om du känner till ID:n för de profilenheter du vill komma åt kan du använda `/entities` (Profilåtkomst) slutpunkt i profil-API för att söka efter dessa enheter. Se avsnittet om [enheter](./api/entities.md) i utvecklarhandboken för mer information.

Du kan också använda API:t för Adobe Experience Platform segmenteringstjänst för att få tillgång till de enskilda profilerna för kunder som har kvalificerat sig för ett målgruppsmedlemskap. Se [Översikt över segmenteringstjänsten](../segmentation/home.md) för mer information.

#### Använda gränssnittet

I användargränssnittet i Experience Platform **[!UICONTROL Browse]** i **[!UICONTROL Profiles]** kan du visa det totala antalet profiler och söka efter enskilda profiler utifrån deras identitetsvärde. Se [Användarhandbok för profil](./ui/user-guide.md) för mer information.

Du kan även visa en lista över dina målgrupper under **[!UICONTROL Browse]** i **[!UICONTROL Audiences]** arbetsyta. När du har valt en målgrupp visas ett exempel på profiler som är kvalificerade för den målgruppen. Du kan sedan välja någon av profilerna i listan för att visa deras information. Se [Översikt över segmenteringsgränssnittet](../segmentation/ui/overview.md) för mer information.

## Felkoder

Nedan följer en lista över felmeddelanden som du kan stöta på när du arbetar med kundprofils-API:t i realtid. Om felet som du stöter på inte finns med här kan du hitta det i det allmänna [Felsökningsguide för plattformen](../landing/troubleshooting.md) i stället.

### Det gick inte att hitta schemat för det beräknade attributet för den angivna sökvägen

```json
{
  "code": "400",
  "message": "Could not lookup schema of the computed attribute for the provided path"
}
```

När ett nytt beräknat attribut skapas inträffar det här felet när systemet inte kan hitta schemat som anges i nyttolasten för begäran. Kontrollera att du har angett rätt innehavar-ID i nyttolastens `path` och att värdena för `schema.name` är ett giltigt schema.

Om du inte känner till ditt klient-ID kan du hämta det genom att följa stegen i [Utvecklarhandbok för schemaregister](../xdm/api/getting-started.md).

### Det finns redan en funktion med samma namn för det angivna schemat eller definedOn

```json
{
  "code": "400",
  "message": "Function with the same name already exists for the specified schema or definedOn"
}
```

När du skapar ett nytt beräknat attribut inträffar det här felet när den angivna `name` egenskapen används redan för schemat som anges under `schema.name`. Ersätt värdet med ett unikt namn innan du försöker igen.

### Returschemat för uttrycket är inte detsamma som schemat för det beräknade attributet i XDM-schemat

```json
{
  "code": "400",
  "message": "Return schema of the expression is not same as the schema of the computed attribute in the XDM schema"
}
```

När du skapar ett nytt beräknat attribut inträffar det här felet när den angivna `name` egenskapen används redan för schemat som anges under `schema.name`. Ersätt värdet med ett unikt namn innan du försöker igen.

### Ogiltig borttagningsbegäran (profilsystemjobb)

```json
{
  "code": "400",
  "message": "Invalid delete request (Profile System Job)"
}
```

Det här felet inträffar när en ogiltig nyttolast anges för ett raderingssystemjobb. Se till att du tillhandahåller en giltig datauppsättning eller ett batch-ID under nyttolastens `dataSetID` eller `batchID` egenskapen. Se avsnittet om [skapa en borttagningsbegäran](./api/profile-system-jobs.md#create-a-delete-request) i Profilutvecklarhandboken för mer information.

### Det gick inte att hitta någon grupp för profildatauppsättningen

```json
{
  "requestId":"LlTmQkhgHKFGHGHnIkmUxcIL4YTFSpQw",
  "errors":{
    "400":[
      {
        "code":"400",
        "message":"Batch not found for profile dataset '5da688d2c4e60518ad25b7b1'"
      }
    ]
  }
}
```

Det här felet inträffar när det inte går att hitta en giltig grupp när en begäran om att ta bort profildata skapas. Kontrollera att du har angett rätt ID för en profilaktiverad datauppsättning innan du försöker igen.

### Projektionsmålet har inte skapats ännu

```json
{
  "status":404,
  "title":"The projection destination has not yet been created.",
  "type":"http://ns.adobe.com/adobecloud/problem/missing-entity"
}
```

Det här felet inträffar när `destinationId` som tillhandahålls i `POST /config/projections` begäran är ogiltig. Kontrollera att du har angett ett giltigt mål-ID innan du försöker igen. Om du vill skapa ett nytt mål följer du de steg som beskrivs i [Profilutvecklarguide](./api/edge-projections.md#create-a-destination).

### Medietypen stöds inte

```json
{
  "status": 415,
  "title": "HTTP 415 Unsupported Media Type",
  "type": "http://ns.adobe.com/adobecloud/problem/unsupported-media-type"
}
```

Det här felet inträffar när en POST- eller PUT-begäran med en ogiltig Content-Type-rubrik skickas. Dubbelkontrollera att du anger ett giltigt Content-Type-värde för slutpunkten som du använder.

De flesta profilslutpunkter accepterar &quot;application/json&quot; för sin Content-Type-rubrik, med följande undantag:

| Slutpunkt | Content-Type |
| --- | --- |
| `/config/projections` | application/vnd.adobe.platform.projectionConfig+json; version=1 |
| `/config/destinations` | application/vnd.adobe.platform.projectionDestination+json; version=1 |
