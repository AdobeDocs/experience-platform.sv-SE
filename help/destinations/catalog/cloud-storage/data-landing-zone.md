---
title: Data Landing Zone-mål
description: Lär dig hur du ansluter till Data Landing Zone för att aktivera målgrupper och exportera datamängder.
last-substantial-update: 2023-07-26T00:00:00Z
exl-id: 40b20faa-cce6-41de-81a0-5f15e6c00e64
source-git-commit: 661ef040398a9e2ef8dd9cebdf7bd27d4268636b
workflow-type: tm+mt
source-wordcount: '1443'
ht-degree: 0%

---

# Data Landing Zone-mål

>[!IMPORTANT]
>
>Dokumentationssidan refererar till [!DNL Data Landing Zone] *mål*. Det finns också en [!DNL Data Landing Zone] *källa* i källkatalogen. Mer information finns i [[!DNL Data Landing Zone] källa](/help/sources/connectors/cloud-storage/data-landing-zone.md) dokumentation.


## Översikt {#overview}

[!DNL Data Landing Zone] är en [!DNL Azure Blob] lagringsgränssnittet som tillhandahålls av Adobe Experience Platform, vilket ger dig tillgång till en säker, molnbaserad fillagringsfunktion för att exportera filer från plattformar. Du har tillgång till en [!DNL Data Landing Zone] behållare per sandlåda och den totala datavolymen för alla behållare begränsas till den totala datamängd som ingår i din licens för plattformsprodukter och -tjänster. Alla kunder med Platform och dess programtjänster som [!DNL Customer Journey Analytics], [!DNL Journey Orchestration], [!DNL Intelligent Services]och [!DNL Real-Time Customer Data Platform] har etablerats med en [!DNL Data Landing Zone] behållare per sandlåda. Du kan läsa och skriva filer till behållaren via [!DNL Azure Storage Explorer] eller kommandoradsgränssnittet.

[!DNL Data Landing Zone] stöder SAS-baserad autentisering och dess data skyddas med standard [!DNL Azure Blob] Mekanismer för förvaringssäkerhet i vila och under transitering. SAS-baserad autentisering ger säker åtkomst till [!DNL Data Landing Zone] behållaren via en offentlig internetanslutning. Du behöver inte göra några nätverksändringar [!DNL Data Landing Zone] container, vilket betyder att du inte behöver konfigurera några tillåtelselista- eller korsregionsinställningar för ditt nätverk.

Plattformen har en strikt TTL-regel (time-to-live) på sju dagar för alla filer som överförs till en [!DNL Data Landing Zone] behållare. Alla filer tas bort efter sju dagar.

## Anslut till [!UICONTROL Data Landing Zone] lagring via API eller användargränssnitt {#connect-api-or-ui}

* Ansluta till [!UICONTROL Data Landing Zone] lagringsplats med hjälp av användargränssnittet för plattformen, läs avsnitten [Anslut till målet](#connect) och [Aktivera målgrupper till det här målet](#activate) nedan.
* Ansluta till [!UICONTROL Data Landing Zone] lagringsplats via programmering, läs [Aktivera målgrupper för filbaserade mål med hjälp av API-självstudiekursen för Flow Service](../../api/activate-segments-file-based-destinations.md).

## Målgrupper {#supported-audiences}

I det här avsnittet beskrivs vilken typ av målgrupper du kan exportera till det här målet.

| Målgruppsursprung | Stöds | Beskrivning |
---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Målgrupper som skapats genom Experience Platform [Segmenteringstjänst](../../../segmentation/home.md). |
| Anpassade överföringar | ✓ | Målgrupper [importerad](../../../segmentation/ui/overview.md#import-audience) till Experience Platform från CSV-filer. |

{style="table-layout:auto"}

## Exportera typ och frekvens {#export-type-frequency}

Se tabellen nedan för information om exporttyp och frekvens för destinationen.

| Objekt | Typ | Anteckningar |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Profile-based]** | Du exporterar alla medlemmar i ett segment tillsammans med tillämpliga schemafält (till exempel ditt PPID), som du väljer på skärmen Välj profilattribut i [arbetsflöde för målaktivering](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| Exportfrekvens | **[!UICONTROL Batch]** | Batchdestinationer exporterar filer till efterföljande plattformar i steg om tre, sex, åtta, tolv eller tjugofyra timmar. Läs mer om [gruppfilsbaserade mål](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## Förutsättningar {#prerequisites}

Observera följande krav som måste vara uppfyllda innan du kan använda [!DNL Data Landing Zone] mål.

### Koppla samman [!DNL Data Landing Zone] behållare till [!DNL Azure Storage Explorer]

Du kan använda [[!DNL Azure Storage Explorer]](https://azure.microsoft.com/en-us/products/storage/storage-explorer/) för att hantera innehållet i [!DNL Data Landing Zone] behållare. Börja använda [!DNL Data Landing Zone], måste du först hämta dina inloggningsuppgifter, ange dem i [!DNL Azure Storage Explorer]och koppla samman [!DNL Data Landing Zone] behållare till [!DNL Azure Storage Explorer].

I [!DNL Azure Storage Explorer] Välj anslutningsikonen i det vänstra navigeringsfältet. The **Välj resurs** visas så att du kan ansluta till dem. Välj **[!DNL Blob container]** för att ansluta till [!DNL Data Landing Zone] lagring.

![select-resource](/help/sources/images/tutorials/create/dlz/select-resource.png)

Nästa, välj **URL för delad åtkomstsignatur (SAS)** som anslutningsmetod och välj sedan **Nästa**.

![select-connection-method](/help/sources/images/tutorials/create/dlz/select-connection-method.png)

När du har valt anslutningsmetod måste du ange en **visningsnamn** och **[!DNL Blob]container SAS-URL** som motsvarar dina [!DNL Data Landing Zone] behållare.

>[!BEGINSHADEBOX]

### Hämta autentiseringsuppgifterna för din [!DNL Data Landing Zone] {#retrieve-dlz-credentials}

Du måste använda plattforms-API:erna för att hämta [!DNL Data Landing Zone] autentiseringsuppgifter. API-anropet för att hämta dina autentiseringsuppgifter beskrivs nedan. Mer information om hur du hämtar de värden som krävs för rubrikerna finns i [Komma igång med Adobe Experience Platform API:er](/help/landing/api-guide.md) guide.

**API-format**

```http
GET /data/foundation/connectors/landingzone/credentials?type=dlz_destination
```

| Frågeparametrar | Beskrivning |
| --- | --- |
| `dlz_destination` | The `dlz_destination` -typ gör att API:t kan skilja en målbehållare för en landningszon från andra typer av behållare som är tillgängliga för dig. |

{style="table-layout:auto"}

**Begäran**

I följande exempel på begäran hämtas autentiseringsuppgifter för en befintlig landningszon.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/connectors/landingzone/credentials?type=dlz_destination' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

**Svar**

Följande svar returnerar autentiseringsuppgifter för din landningszon, inklusive din nuvarande `SASToken` och `SASUri`och `storageAccountName` som motsvarar behållaren för landningszonen.

```json
{
    "containerName": "dlz-user-container",
    "SASToken": "sv=2022-09-11&si=dlz-ed86a61d-201f-4b50-b10f-a1bf173066fd&sr=c&sp=racwdlm&sig=4yTba8voU3L0wlcLAv9mZLdZ7NlMahbfYYPTMkQ6ZGU%3D",
    "storageAccountName": "dlblobstore99hh25i3df123",
    "SASUri": "https://dlblobstore99hh25i3dflek.blob.core.windows.net/dlz-user-container?sv=2022-09-11&si=dlz-ed86a61d-201f-4b50-b10f-a1bf173066fd&sr=c&sp=racwdlm&sig=4yTba8voU3L0wlcLAv9mZLdZ7NlMahbfYYPTMkQ6ZGU%3D"
}
```

| Egenskap | Beskrivning |
| --- | --- |
| `containerName` | Namnet på din landningszon. |
| `SASToken` | Den delade åtkomstsignaturtoken för din landningszon. Strängen innehåller all information som krävs för att godkänna en begäran. |
| `SASUri` | Den delade åtkomstsignaturens URI för din landningszon. Den här strängen är en kombination av URI:n till den landningszon som du autentiseras mot och dess motsvarande SAS-token, |

{style="table-layout:auto"}

### Uppdatera [!DNL Data Landing Zone] autentiseringsuppgifter {#update-dlz-credentials}

Du kan även uppdatera dina inloggningsuppgifter när du vill. Du kan uppdatera din `SASToken` genom att göra en POST-förfrågan till `/credentials` slutpunkt för [!DNL Connectors] API.

**API-format**

```http
POST /data/foundation/connectors/landingzone/credentials?type=dlz_destination&action=refresh
```

| Frågeparametrar | Beskrivning |
| --- | --- |
| `dlz_destination` | The `dlz_destination` -typ gör att API:t kan skilja en målbehållare för en landningszon från andra typer av behållare som är tillgängliga för dig. |
| `refresh` | The `refresh` kan du återställa dina inloggningsuppgifter för landningszonen och automatiskt generera en ny `SASToken`. |

{style="table-layout:auto"}

**Begäran**

Följande begäran uppdaterar dina inloggningsuppgifter för landningszonen.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/connectors/landingzone/credentials?type=dlz_destination&action=refresh' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

**Svar**

Följande svar returnerar uppdaterade värden för `SASToken` och `SASUri`.

```json
{
    "containerName": "dlz-user-container",
    "SASToken": "sv=2020-04-08&si=dlz-9c4d03b8-a6ff-41be-9dcf-20123e717e99&sr=c&sp=racwdlm&sig=JbRMoDmFHQU4OWOpgrKdbZ1d%2BkvslO35%2FXTqBO%2FgbRA%3D",
    "storageAccountName": "dlblobstore99hh25i3dflek",
    "SASUri": "https://dlblobstore99hh25i3dflek.blob.core.windows.net/dlz-user-container?sv=2020-04-08&si=dlz-9c4d03b8-a6ff-41be-9dcf-20123e717e99&sr=c&sp=racwdlm&sig=JbRMoDmFHQU4OWOpgrKdbZ1d%2BkvslO35%2FXTqBO%2FgbRA%3D"
}
```

>[!ENDSHADEBOX]

Ange ditt visningsnamn (`containerName`) och [!DNL Data Landing Zone] SAS-URL, som returneras i det API-anrop som beskrivs ovan, och välj sedan **Nästa**.

![enter-connection-info](/help/sources/images/tutorials/create/dlz/enter-connection-info.png)

The **Sammanfattning** visas så att du får en översikt över dina inställningar, inklusive information om [!DNL Blob] slutpunkt och behörigheter. När du är klar väljer du **Anslut**.

![sammanfattning](/help/sources/images/tutorials/create/dlz/summary.png)

Anslutningen uppdaterar [!DNL Azure Storage Explorer] Gränssnitt med [!DNL Data Landing Zone] behållare.

![dlz-user-container](/help/sources/images/tutorials/create/dlz/dlz-user-container.png)

Med [!DNL Data Landing Zone] behållare ansluten till [!DNL Azure Storage Explorer]kan du nu börja exportera filer från Experience Platform till [!DNL Data Landing Zone] behållare. Om du vill exportera filer måste du skapa en anslutning till [!DNL Data Landing Zone] mål i användargränssnittet i Experience Platform, enligt beskrivningen i avsnittet nedan.

## Anslut till målet {#connect}

>[!IMPORTANT]
> 
>Om du vill ansluta till målet behöver du **[!UICONTROL Manage Destinations]** [behörighet för åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontroll - översikt](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få de behörigheter som krävs.

Om du vill ansluta till det här målet följer du stegen som beskrivs i [självstudiekurs om destinationskonfiguration](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html). I arbetsflödet för målkonfiguration fyller du i fälten som listas i de två avsnitten nedan.

### Autentisera till mål {#authenticate}

Kontrollera att du har anslutit din [!DNL Data Landing Zone] behållare till [!DNL Azure Storage Explorer] enligt beskrivningen i [krav](#prerequisites) -avsnitt. För [!DNL Data Landing Zone] är ett lagringsutrymme som tillhandahålls av Adobe behöver du inte utföra några ytterligare steg i användargränssnittet i Experience Platform för att autentisera mot målet.

### Fyll i målinformation {#destination-details}

Om du vill konfigurera information för målet fyller du i de obligatoriska och valfria fälten nedan. En asterisk bredvid ett fält i användargränssnittet anger att fältet är obligatoriskt.

* **[!UICONTROL Name]**: Fyll i det önskade namnet för det här målet.
* **[!UICONTROL Description]**: Valfritt. Du kan till exempel ange vilken kampanj du använder det här målet för.
* **[!UICONTROL Folder path]**: Ange sökvägen till målmappen som ska vara värd för de exporterade filerna.
* **[!UICONTROL File type]**: Välj det format som Experience Platform ska använda för de exporterade filerna. När du väljer [!UICONTROL CSV] kan du också [konfigurera filformateringsalternativ](../../ui/batch-destinations-file-formatting-options.md).
* **[!UICONTROL Compression format]**: Välj den komprimeringstyp som Experience Platform ska använda för de exporterade filerna.
* **[!UICONTROL Include manifest file]**: Aktivera det här alternativet om du vill att exporten ska innehålla en manifestfil för JSON som innehåller information om exportplats, exportstorlek med mera. Manifestet har ett namn i formatet `manifest-<<destinationId>>-<<dataflowRunId>>.json`. Visa en [exempelmanifestfil](/help/destinations/assets/common/manifest-d0420d72-756c-4159-9e7f-7d3e2f8b501e-0ac8f3c0-29bd-40aa-82c1-f1b7e0657b19.json). Manifestfilen innehåller följande fält:
   * `flowRunId`: [dataflödeskörning](/help/dataflows/ui/monitor-destinations.md#dataflow-runs-for-batch-destinations) som genererade den exporterade filen.
   * `scheduledTime`: Tiden i UTC när filen exporterades.
   * `exportResults.sinkPath`: Sökvägen till lagringsplatsen där den exporterade filen placeras.
   * `exportResults.name`: Namnet på den exporterade filen.
   * `size`: Storleken på den exporterade filen, i byte.

### Aktivera aviseringar {#enable-alerts}

Du kan aktivera varningar för att få meddelanden om dataflödets status till ditt mål. Välj en avisering i listan om du vill prenumerera och få meddelanden om statusen för ditt dataflöde. Mer information om varningar finns i guiden på [prenumerera på destinationsvarningar med användargränssnittet](../../ui/alerts.md).

När du är klar med informationen för målanslutningen väljer du **[!UICONTROL Next]**.

## Aktivera målgrupper till det här målet {#activate}

>[!IMPORTANT]
> 
>* För att aktivera data behöver du **[!UICONTROL Manage Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** och **[!UICONTROL View Segments]** [behörigheter för åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontroll - översikt](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få de behörigheter som krävs.
>* Exportera *identiteter* behöver du **[!UICONTROL View Identity Graph]** [behörighet för åtkomstkontroll](/help/access-control/home.md#permissions). <br> ![Markera det identitetsnamnutrymme som är markerat i arbetsflödet för att aktivera målgrupper till mål.](/help/destinations/assets/overview/export-identities-to-destination.png "Markera det identitetsnamnutrymme som är markerat i arbetsflödet för att aktivera målgrupper till mål."){width="100" zoomable="yes"}

Se [Aktivera målgruppsdata för att batchprofilera exportmål](../../ui/activate-batch-profile-destinations.md) för instruktioner om hur du aktiverar målgrupper till det här målet.

### Schemaläggning

I **[!UICONTROL Scheduling]** kan du [konfigurera exportschemat](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling) för [!DNL Data Landing Zone] mål och du kan också [konfigurera namnet på de exporterade filerna](/help/destinations/ui/activate-batch-profile-destinations.md#file-names).

### Mappa attribut och identiteter {#map}

I **[!UICONTROL Mapping]** kan du välja vilka attribut- och identitetsfält som ska exporteras för dina profiler. Du kan också välja att ändra rubrikerna i den exporterade filen till ett valfritt användarvänligt namn. Mer information finns i [mappningssteg](/help/destinations/ui/activate-batch-profile-destinations.md#mapping) i självstudiekursen om att aktivera gruppdestinationer.

## (Beta) Exportera datauppsättningar {#export-datasets}

Detta mål stöder datauppsättningsexporter. Fullständig information om hur du ställer in datauppsättningsexporter finns i självstudiekurserna:

* Så här gör du [exportera datauppsättningar med hjälp av användargränssnittet för plattformen](/help/destinations/ui/export-datasets.md).
* Så här gör du [exportera datauppsättningar via programmering med API:t för Flow Service](/help/destinations/api/export-datasets.md).

## Validera slutförd dataexport {#exported-data}

Kontrollera dina [!DNL Data Landing Zone] och se till att de exporterade filerna innehåller de förväntade profilpopulationerna.
