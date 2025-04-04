---
keywords: Experience Platform;profil;kundprofil i realtid;felsökning;API
title: Felsökningsguide för kundprofiler i realtid
type: Documentation
description: Det här dokumentet innehåller svar på vanliga frågor om kundprofilen i realtid samt en felsökningsguide för vanliga fel när du arbetar med profildata med Adobe Experience Platform.
exl-id: 0b340025-093b-41e4-8053-969a8e80e889
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '964'
ht-degree: 0%

---

# Felsökningsguide för kundprofiler i realtid

Det här dokumentet innehåller svar på vanliga frågor om kundprofilen i realtid samt en felsökningsguide för vanliga fel. För frågor och felsökning som rör andra tjänster i Adobe Experience Platform, se [Experience Platform felsökningsguide](../landing/troubleshooting.md).

Med [!DNL Real-Time Customer Profile] kan du se en helhetsbild av varje enskild kund genom att kombinera data från flera kanaler, inklusive online, offline, CRM och tredje part. Detta gör att marknadsförarna kan skapa samordnade, enhetliga och relevanta kundupplevelser i flera kanaler.

## Vanliga frågor och svar

Nedan följer en lista med svar på vanliga frågor om kundprofilen i realtid.

### Vilka typer av data accepteras för kundprofilen i realtid?

Profilen godkänner både **post**- och **tidsserie**-data, förutsatt att data i fråga innehåller minst ett identitetsvärde som associerar data med en unik individ.

Precis som alla Experience Platform-tjänster kräver Profile att data i den ska vara semantiskt strukturerade under ett XDM-schema (Experience Data Model). Schemat måste i sin tur ha en **primär identitet** definierad och vara aktiverat för användning i profilen.

Om du inte känner till XDM kan du börja med [XDM-översikten](../xdm/home.md) och lära dig mer. Gå sedan till användarhandboken för XDM för steg om hur du [anger identitetsfält](../xdm/tutorials/create-schema-ui.md#identity-field) och [aktiverar ett schema för profil](../xdm/tutorials/create-schema-ui.md#profile).

### Var lagras profildata?

Kundprofilen i realtid underhåller ett eget datalager (kallas&quot;profilarkiv&quot;) som är skilt från datasjön som innehåller andra inkapslade Experience Platform-data.

### Om jag redan har inhämtat data till Experience Platform, kan jag då göra dem tillgängliga i profilbutiken?

Om data har importerats till en datauppsättning som inte är en profildatauppsättning måste du importera dessa data på nytt till en profilaktiverad datauppsättning för att kunna göra dem tillgängliga i profilarkivet. Det går att aktivera en befintlig datauppsättning för profilen, men alla data som har importerats före den konfigurationen visas fortfarande inte i profilarkivet.

Om du vill lägga till tidigare inkapslade data i profilarkivet följer du [självstudiekursen för konfiguration av datauppsättning](./tutorials/dataset-configuration.md) för att skapa en ny datauppsättning eller konverterar en befintlig datauppsättning som ska aktiveras för profilen, och sedan importerar du önskade data till datauppsättningen igen.

### Hur kan jag visa mina inkapslade profildata?

Det finns flera sätt att visa profildata, beroende på om du använder API:t eller gränssnittet.

#### Använda API:et

Om du känner till ID:n för de profilentiteter som du vill komma åt kan du använda slutpunkten `/entities` (profilåtkomst) i profil-API:t för att söka efter dessa entiteter. Mer information finns i avsnittet om [entiteter](./api/entities.md) i utvecklarhandboken.

Du kan också använda API:t för Adobe Experience Platform segmenteringstjänst för att få tillgång till de enskilda profilerna för kunder som har kvalificerat sig för ett målgruppsmedlemskap. Mer information finns i [Översikt över segmenteringstjänsten](../segmentation/home.md).

#### Använda gränssnittet

I Experience Platform-gränssnittet kan du visa det totala antalet profiler och söka efter enskilda profiler med hjälp av deras ID-värde på fliken **[!UICONTROL Browse]** på arbetsytan **[!UICONTROL Profiles]**. Mer information finns i [Användarhandboken för profilen](./ui/user-guide.md).

Du kan även visa en lista över dina målgrupper på fliken **[!UICONTROL Browse]** på arbetsytan i **[!UICONTROL Audiences]**. När du har valt en målgrupp visas ett exempel på profiler som är kvalificerade för den målgruppen. Du kan sedan välja någon av profilerna i listan för att visa deras information. Mer information finns i [Översikt över segmenteringsgränssnittet](../segmentation/ui/overview.md).

## Felkoder

Nedan följer en lista över felmeddelanden som du kan stöta på när du arbetar med kundprofils-API:t i realtid. Om felet som du stöter på inte finns med här kan du hitta det i den allmänna [felsökningsguiden](../landing/troubleshooting.md) för Experience Platform istället.

### Det gick inte att hitta schemat för det beräknade attributet för den angivna sökvägen

```json
{
  "code": "400",
  "message": "Could not lookup schema of the computed attribute for the provided path"
}
```

När ett nytt beräknat attribut skapas inträffar det här felet när systemet inte kan hitta schemat som anges i nyttolasten för begäran. Kontrollera att du har angett rätt innehavar-ID i nyttolastens `path`-egenskap och att värdena för `schema.name` är ett giltigt schemanamn.

Om du inte känner till ditt klient-ID kan du hämta det genom att följa stegen i [Utvecklarhandbok för schemaregister](../xdm/api/getting-started.md).

### Det finns redan en funktion med samma namn för det angivna schemat eller definedOn

```json
{
  "code": "400",
  "message": "Function with the same name already exists for the specified schema or definedOn"
}
```

När du skapar ett nytt beräknat attribut inträffar det här felet när den angivna `name`-egenskapen redan används för det schema som anges under `schema.name`. Ersätt värdet med ett unikt namn innan du försöker igen.

### Returschemat för uttrycket är inte detsamma som schemat för det beräknade attributet i XDM-schemat

```json
{
  "code": "400",
  "message": "Return schema of the expression is not same as the schema of the computed attribute in the XDM schema"
}
```

När du skapar ett nytt beräknat attribut inträffar det här felet när den angivna `name`-egenskapen redan används för det schema som anges under `schema.name`. Ersätt värdet med ett unikt namn innan du försöker igen.

### Ogiltig borttagningsbegäran (profilsystemjobb)

```json
{
  "code": "400",
  "message": "Invalid delete request (Profile System Job)"
}
```

Det här felet inträffar när en ogiltig nyttolast anges för ett raderingssystemjobb. Se till att du anger ett giltigt data- eller batch-ID under nyttolastens `dataSetID`- respektive `batchID`-egenskap. Mer information finns i avsnittet [Skapa en borttagningsbegäran](./api/profile-system-jobs.md#create-a-delete-request) i guiden för profilutvecklare.

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
