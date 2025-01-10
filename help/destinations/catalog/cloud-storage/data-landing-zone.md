---
title: Data Landing Zone-mål
description: Lär dig hur du ansluter till Data Landing Zone för att aktivera målgrupper och exportera datamängder.
last-substantial-update: 2023-07-26T00:00:00Z
exl-id: 40b20faa-cce6-41de-81a0-5f15e6c00e64
source-git-commit: 5f932f3de2b875d77904582dfb320e0b6ce17afd
workflow-type: tm+mt
source-wordcount: '1927'
ht-degree: 0%

---

# Data Landing Zone-mål

>[!IMPORTANT]
>
>Den här dokumentationssidan refererar till [!DNL Data Landing Zone] *destination*. Det finns också en [!DNL Data Landing Zone] *källa* i källkatalogen. Mer information finns i dokumentationen för [[!DNL Data Landing Zone] source](/help/sources/connectors/cloud-storage/data-landing-zone.md).


## Översikt {#overview}

[!DNL Data Landing Zone] är ett molnlagringsgränssnitt som tillhandahålls av Adobe Experience Platform, vilket ger dig åtkomst till en säker, molnbaserad fillagringsfunktion för att exportera filer från plattformen. Du har åtkomst till en [!DNL Data Landing Zone]-behållare per sandlåda, och den totala datavolymen för alla behållare är begränsad till den totala datamängden som tillhandahålls med plattformsprodukten och tjänstlicensen. Alla kunder med Platform och dess program som [!DNL Customer Journey Analytics], [!DNL Journey Orchestration], [!DNL Intelligent Services] och [!DNL Real-Time Customer Data Platform] etableras med en [!DNL Data Landing Zone]-behållare per sandlåda.

Plattformen tvingar en strikt TTL (time-to-live) på sju dagar för alla filer som överförs till en [!DNL Data Landing Zone]-behållare. Alla filer tas bort efter sju dagar.

Målanslutningen [!DNL Data Landing Zone] är tillgänglig för kunder som använder molnstödet för Azure eller Amazon Web Service. Autentiseringsmekanismen skiljer sig åt beroende på vilket moln som målet etableras i, allt annat om målet och dess användningsfall är desamma. Läs mer om de två olika autentiseringsmekanismerna i avsnitten [Autentisera till den datalandningszon som har etablerats i Azure-blobben](#authenticate-dlz-azure) och [Autentisera till den datastartzon som har etablerats av AWS](#authenticate-dlz-aws).

![Diagram som visar hur implementeringen av Data Landing Zone-destinationen skiljer sig åt beroende på molnstödet.](/help/destinations/assets/catalog/cloud-storage/data-landing-zone/dlz-workflow-based-on-cloud-implementation.png "Målimplementering för Data Landing Zone via molnstöd"){zoomable="yes"}

## Anslut till ditt [!UICONTROL Data Landing Zone]-lagringsutrymme via API eller användargränssnittet {#connect-api-or-ui}

* Läs avsnitten [Anslut till målet](#connect) och [Aktivera målgrupper till det här målet](#activate) nedan om du vill ansluta till lagringsplatsen [!UICONTROL Data Landing Zone] med hjälp av användargränssnittet för plattformen.
* Om du vill ansluta till din [!UICONTROL Data Landing Zone]-lagringsplats programmatiskt läser du [Aktivera målgrupper till filbaserade mål med hjälp av API-självstudiekursen för Flow-tjänsten](../../api/activate-segments-file-based-destinations.md).

## Målgrupper {#supported-audiences}

I det här avsnittet beskrivs vilka typer av målgrupper du kan exportera till det här målet.

| Målgruppsursprung | Stöds | Beskrivning |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Publiker som genererats via Experience Platform [segmenteringstjänsten](../../../segmentation/home.md). |
| Anpassade överföringar | ✓ | Publikerna [importerade](../../../segmentation/ui/audience-portal.md#import-audience) till Experience Platform från CSV-filer. |

{style="table-layout:auto"}

## Exportera typ och frekvens {#export-type-frequency}

Se tabellen nedan för information om exporttyp och frekvens för destinationen.

| Objekt | Typ | Anteckningar |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Profile-based]** | Du exporterar alla medlemmar i ett segment, tillsammans med tillämpliga schemafält (till exempel ditt PPID), som du har valt på skärmen Välj profilattribut i arbetsflödet för [målaktivering](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| Exportfrekvens | **[!UICONTROL Batch]** | Batchdestinationer exporterar filer till efterföljande plattformar i steg om tre, sex, åtta, tolv eller tjugofyra timmar. Läs mer om [gruppfilsbaserade mål](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## Exportera datauppsättningar {#export-datasets}

Detta mål stöder datauppsättningsexporter. Fullständig information om hur du ställer in datauppsättningsexporter finns i självstudiekurserna:

* Så här [exporterar du datauppsättningar med användargränssnittet för plattformen](/help/destinations/ui/export-datasets.md).
* Så här [exporterar du datauppsättningar programmatiskt med API:t för Flow Service ](/help/destinations/api/export-datasets.md).

## Filformat för exporterade data {#file-format}

När du exporterar *målgruppsdata* skapar Platform en `.csv` -, `parquet` - eller `.json` -fil på den angivna lagringsplatsen. Mer information om filerna finns i avsnittet [Filformat som stöds för export](../../ui/activate-batch-profile-destinations.md#supported-file-formats-export) i självstudiekursen om målgruppsaktivering.

När du exporterar *datauppsättningar* skapar Platform en `.parquet` - eller `.json` -fil på den lagringsplats som du angav. Mer information om filerna finns i avsnittet [Verifiera lyckad datauppsättningsexport](../../ui/export-datasets.md#verify) i självstudiekursen om exportdatamängder.

## Autentisera till den datalandningszon som har etablerats i Azure-blobben {#authenticate-dlz-azure}

>[!AVAILABILITY]
>
>Det här avsnittet gäller implementeringar av Experience Platform som körs på Microsoft Azure. Mer information om den Experience Platform-infrastruktur som stöds finns i [Översikt över flera moln i Experience Platform](https://experienceleague.adobe.com/en/docs/experience-platform/landing/multi-cloud).

Du kan läsa och skriva filer till behållaren via [!DNL Azure Storage Explorer] eller kommandoradsgränssnittet.

[!DNL Data Landing Zone] har stöd för SAS-baserad autentisering och dess data skyddas med standardsäkerhetsmekanismer för lagring i [!DNL Azure Blob] vid vila och överföring. SAS står för [signatur för delad åtkomst](https://learn.microsoft.com/en-us/azure/ai-services/translator/document-translation/how-to-guides/create-sas-tokens?tabs=Containers).

Om du vill skydda dina data över en offentlig internetanslutning använder du SAS-baserad autentisering för att få säker åtkomst till [!DNL Data Landing Zone]-behållaren. Du behöver inte göra några nätverksändringar för att komma åt din [!DNL Data Landing Zone]-behållare, vilket innebär att du inte behöver konfigurera några tillåtelselista- eller korsregionsinställningar för ditt nätverk.

### Anslut [!DNL Data Landing Zone]-behållaren till [!DNL Azure Storage Explorer]

Du kan använda [[!DNL Azure Storage Explorer]](https://azure.microsoft.com/en-us/products/storage/storage-explorer/) för att hantera innehållet i [!DNL Data Landing Zone]-behållaren. Om du vill börja använda [!DNL Data Landing Zone] måste du först hämta dina autentiseringsuppgifter, ange dem i [!DNL Azure Storage Explorer] och ansluta [!DNL Data Landing Zone]-behållaren till [!DNL Azure Storage Explorer].

I användargränssnittet för [!DNL Azure Storage Explorer] väljer du anslutningsikonen i det vänstra navigeringsfältet. Fönstret **Välj resurs** visas med alternativ att ansluta till. Välj **[!DNL Blob container]** om du vill ansluta till ditt [!DNL Data Landing Zone]-lagringsutrymme.

![Välj en resurs som är markerad i Azure-gränssnittet.](/help/sources/images/tutorials/create/dlz/select-resource.png)

Välj sedan **URL för delad åtkomstsignatur (SAS)** som anslutningsmetod och välj sedan **Nästa**.

![Välj anslutningsmetod markerad i Azure-gränssnittet.](/help/sources/images/tutorials/create/dlz/select-connection-method.png)

När du har valt anslutningsmetod måste du ange ett **visningsnamn** och **[!DNL Blob]behållar-SAS-URL:en** som motsvarar din [!DNL Data Landing Zone]-behållare.

>[!BEGINSHADEBOX]

### Hämta autentiseringsuppgifterna för [!DNL Data Landing Zone] {#retrieve-dlz-credentials}

Du måste använda plattforms-API:erna för att hämta dina [!DNL Data Landing Zone]-autentiseringsuppgifter. API-anropet för att hämta dina autentiseringsuppgifter beskrivs nedan. Mer information om hur du hämtar de värden som krävs för rubrikerna finns i guiden [Komma igång med Adobe Experience Platform API:er](/help/landing/api-guide.md).

**API-format**

```http
GET /data/foundation/connectors/landingzone/credentials?type=dlz_destination
```

| Frågeparametrar | Beskrivning |
| --- | --- |
| `dlz_destination` | Typen `dlz_destination` gör att API:t kan skilja en målbehållare för en landningszon från andra typer av behållare som är tillgängliga för dig. |

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

Följande svar returnerar inloggningsinformationen för din landningszon, inklusive din nuvarande `SASToken` och `SASUri` samt den `storageAccountName` som motsvarar din landningszonsbehållare.

```json
{
    "containerName": "dlz-destination",
    "SASToken": "sv=2022-09-11&si=dlz-ed86a61d-201f-4b50-b10f-a1bf173066fd&sr=c&sp=racwdlm&sig=4yTba8voU3L0wlcLAv9mZLdZ7NlMahbfYYPTMkQ6ZGU%3D",
    "storageAccountName": "dlblobstore99hh25i3df123",
    "SASUri": "https://dlblobstore99hh25i3dflek.blob.core.windows.net/dlz-destination?sv=2022-09-11&si=dlz-ed86a61d-201f-4b50-b10f-a1bf173066fd&sr=c&sp=racwdlm&sig=4yTba8voU3L0wlcLAv9mZLdZ7NlMahbfYYPTMkQ6ZGU%3D"
}
```

| Egenskap | Beskrivning |
| --- | --- |
| `containerName` | Namnet på din landningszon. |
| `SASToken` | Den delade åtkomstsignaturtoken för din landningszon. Strängen innehåller all information som krävs för att godkänna en begäran. |
| `SASUri` | Den delade åtkomstsignaturens URI för din landningszon. Den här strängen är en kombination av URI:n till den landningszon som du autentiseras mot och dess motsvarande SAS-token, |

{style="table-layout:auto"}

### Uppdatera autentiseringsuppgifter för [!DNL Data Landing Zone] {#update-dlz-credentials}

Du kan även uppdatera dina inloggningsuppgifter när du vill. Du kan uppdatera `SASToken` genom att göra en POST-förfrågan till `/credentials`-slutpunkten för [!DNL Connectors] API:t.

**API-format**

```http
POST /data/foundation/connectors/landingzone/credentials?type=dlz_destination&action=refresh
```

| Frågeparametrar | Beskrivning |
| --- | --- |
| `dlz_destination` | Typen `dlz_destination` gör att API:t kan skilja en målbehållare för en landningszon från andra typer av behållare som är tillgängliga för dig. |
| `refresh` | Med åtgärden `refresh` kan du återställa dina autentiseringsuppgifter för landningszonen och automatiskt generera en ny `SASToken`. |

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
    "containerName": "dlz-destination",
    "SASToken": "sv=2020-04-08&si=dlz-9c4d03b8-a6ff-41be-9dcf-20123e717e99&sr=c&sp=racwdlm&sig=JbRMoDmFHQU4OWOpgrKdbZ1d%2BkvslO35%2FXTqBO%2FgbRA%3D",
    "storageAccountName": "dlblobstore99hh25i3dflek",
    "SASUri": "https://dlblobstore99hh25i3dflek.blob.core.windows.net/dlz-destination?sv=2020-04-08&si=dlz-9c4d03b8-a6ff-41be-9dcf-20123e717e99&sr=c&sp=racwdlm&sig=JbRMoDmFHQU4OWOpgrKdbZ1d%2BkvslO35%2FXTqBO%2FgbRA%3D"
}
```

>[!ENDSHADEBOX]

Ange ditt visningsnamn (`containerName`) och [!DNL Data Landing Zone] SAS-URL, som returneras i det API-anrop som beskrivs ovan, och välj sedan **Nästa**.

![Ange anslutningsinformation som är markerad i Azure-gränssnittet.](/help/sources/images/tutorials/create/dlz/enter-connection-info.png)

Fönstret **Sammanfattning** visas med en översikt över dina inställningar, inklusive information om din [!DNL Blob]-slutpunkt och behörigheter. Välj **Anslut** när du är klar.

![Sammanfattning av inställningar som visas i Azure-gränssnittet.](/help/sources/images/tutorials/create/dlz/summary.png)

En anslutning uppdaterar användargränssnittet för [!DNL Azure Storage Explorer] med behållaren för [!DNL Data Landing Zone].

![Sammanfattning av DLZ-användarbehållaren markerad i Azure-gränssnittet.](/help/sources/images/tutorials/create/dlz/dlz-user-container.png)

Med din [!DNL Data Landing Zone]-behållare ansluten till [!DNL Azure Storage Explorer] kan du nu börja exportera filer från Experience Platform till [!DNL Data Landing Zone]-behållaren. Om du vill exportera filer måste du upprätta en anslutning till [!DNL Data Landing Zone]-målet i användargränssnittet i Experience Platform, vilket beskrivs i avsnittet nedan.

## Autentisera till AWS-allokerade datalandningszon {#authenticate-dlz-aws}

>[!AVAILABILITY]
>
>Detta avsnitt gäller för implementeringar av Experience Platform som körs på Amazon Web Services (AWS). Experience Platform som körs på AWS är för närvarande tillgängligt för ett begränsat antal kunder. Mer information om den Experience Platform-infrastruktur som stöds finns i [Översikt över flera moln i Experience Platform](https://experienceleague.adobe.com/en/docs/experience-platform/landing/multi-cloud).

Utför åtgärderna nedan för att hämta autentiseringsuppgifter till din [!DNL Data Landing Zone]-instans som har etablerats på AWS. Använd sedan en valfri klient för att ansluta till din [!DNL Data Landing Zone]-instans.

>[!BEGINSHADEBOX]

### Hämta autentiseringsuppgifterna för [!DNL Data Landing Zone] {#retrieve-dlz-credentials-aws}

Du måste använda plattforms-API:erna för att hämta dina [!DNL Data Landing Zone]-autentiseringsuppgifter. API-anropet för att hämta dina autentiseringsuppgifter beskrivs nedan. Mer information om hur du hämtar de värden som krävs för rubrikerna finns i guiden [Komma igång med Adobe Experience Platform API:er](/help/landing/api-guide.md).

**API-format**

```http
GET /data/foundation/connectors/landingzone/credentials?type=dlz_destination'
```

| Frågeparametrar | Beskrivning |
| --- | --- |
| `dlz_destination` | Lägg till frågeparametern `dlz_destination` för att ange att du vill att [!DNL Data Landing Zone] *destination*-typen för behållarautentiseringsuppgifter ska hämtas. Om du vill ansluta och hämta autentiseringsuppgifter för en Data Landing Zone *source* läser du [källdokumentationen](/help/sources/connectors/cloud-storage/data-landing-zone.md). |

{style="table-layout:auto"}

**Begäran**

I följande exempel på begäran hämtas autentiseringsuppgifter för en befintlig landningszon.

```shell
curl --request GET \
  --url 'https://platform.adobe.io/data/foundation/connectors/landingzone/credentials?type=dlz_destination' \
  --header 'Authorization: Bearer ***' \
  --header 'Content-Type: application/json' \
  --header 'x-api-key: your_api_key' \
  --header 'x-gw-ims-org-id: yourorg@AdobeOrg'
```

**Svar**

Följande svar returnerar autentiseringsuppgifter för din landningszon, inklusive din aktuella `awsAccessKeyId`, `awsSecretAccessKey` och annan information.

```json
{
    "credentials": {
        "awsAccessKeyId": "ABCDW3MEC6HE2T73ZVKP",
        "awsSecretAccessKey": "A1B2Zdxj6y4xfR0QZGtf/phj/hNMAbOGtzM/JNeE",
        "awsSessionToken": "***"
    },
    "dlzPath": {
        "bucketName": "your-bucket-name",
        "dlzFolder": "dlz-destination"
    },
    "dlzProvider": "Amazon S3",
    "expiryTime": 1734494017
}
```

| Egenskap | Beskrivning |
| --- | --- |
| `credentials` | Det här objektet innehåller `awsAccessKeyId`, `awsSecretAccessKey` och `awsSessionToken` som Experience Platform använder för att exportera filer till din tilldelade Data Landing Zone-plats. |
| `dlzPath` | Det här objektet innehåller sökvägen till den AWS-plats som har tilldelats av Adobe, där exporterade filer placeras. |
| `dlzProvider` | Anger att detta är en Amazon S3-provisionerad Data Landing Zone. |
| `expiryTime` | Anger när autentiseringsuppgifterna i objektet `credentials` upphör att gälla. Uppdatera autentiseringsuppgifterna genom att utföra begäran igen. |

{style="table-layout:auto"}

>[!ENDSHADEBOX]

## Anslut till målet {#connect}

>[!IMPORTANT]
> 
>Om du vill ansluta till målet behöver du behörigheterna **[!UICONTROL View Destinations]** och **[!UICONTROL Manage Destinations]** [åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontrollsöversikten](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få den behörighet som krävs.

Om du vill ansluta till det här målet följer du stegen som beskrivs i självstudiekursen [för destinationskonfiguration](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html). I arbetsflödet för målkonfiguration fyller du i fälten som listas i de två avsnitten nedan.

### Autentisera till mål {#authenticate}

Kontrollera att du har anslutit [!DNL Data Landing Zone]-behållaren till [!DNL Azure Storage Explorer] enligt beskrivningen i avsnittet [Krav](#prerequisites). Eftersom [!DNL Data Landing Zone] är ett lagringsutrymme som tillhandahålls av Adobe behöver du inte utföra några ytterligare steg i användargränssnittet i Experience Platform för att autentisera mot målet.

### Fyll i målinformation {#destination-details}

Om du vill konfigurera information för målet fyller du i de obligatoriska och valfria fälten nedan. En asterisk bredvid ett fält i användargränssnittet anger att fältet är obligatoriskt.

* **[!UICONTROL Name]**: Fyll i det önskade namnet för det här målet.
* **[!UICONTROL Description]**: Valfritt. Du kan till exempel ange vilken kampanj du använder det här målet för.
* **[!UICONTROL Folder path]**: Ange sökvägen till målmappen som ska vara värd för de exporterade filerna.
* **[!UICONTROL File type]**: Välj det format som Experience Platform ska använda för de exporterade filerna. När du väljer alternativet [!UICONTROL CSV] kan du även [konfigurera filformateringsalternativen](../../ui/batch-destinations-file-formatting-options.md).
* **[!UICONTROL Compression format]**: Välj den komprimeringstyp som Experience Platform ska använda för de exporterade filerna.
* **[!UICONTROL Include manifest file]**: Aktivera det här alternativet om du vill att exporten ska innehålla en manifestfil för JSON som innehåller information om exportplats, exportstorlek och mycket annat. Manifestet har fått ett namn i formatet `manifest-<<destinationId>>-<<dataflowRunId>>.json`. Visa en [exempelmanifestfil](/help/destinations/assets/common/manifest-d0420d72-756c-4159-9e7f-7d3e2f8b501e-0ac8f3c0-29bd-40aa-82c1-f1b7e0657b19.json). Manifestfilen innehåller följande fält:
   * `flowRunId`: [Dataflödet kör](/help/dataflows/ui/monitor-destinations.md#dataflow-runs-for-batch-destinations) som genererade den exporterade filen.
   * `scheduledTime`: Tiden i UTC när filen exporterades.
   * `exportResults.sinkPath`: Sökvägen till lagringsplatsen där den exporterade filen placeras.
   * `exportResults.name`: Namnet på den exporterade filen.
   * `size`: Den exporterade filens storlek i byte.

### Aktivera aviseringar {#enable-alerts}

Du kan aktivera varningar för att få meddelanden om dataflödets status till ditt mål. Välj en avisering i listan om du vill prenumerera och få meddelanden om statusen för ditt dataflöde. Mer information om varningar finns i guiden [prenumerera på destinationsvarningar med användargränssnittet](../../ui/alerts.md).

Välj **[!UICONTROL Next]** när du är klar med att ange information för målanslutningen.

## Aktivera målgrupper till det här målet {#activate}

>[!IMPORTANT]
> 
>* För att aktivera data behöver du behörigheterna **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** och **[!UICONTROL View Segments]** [åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontrollsöversikten](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få den behörighet som krävs.
>* Om du vill exportera *identiteter* måste du ha **[!UICONTROL View Identity Graph]** [åtkomstkontrollbehörighet](/help/access-control/home.md#permissions). <br> ![Markera identitetsnamnområdet som är markerat i arbetsflödet för att aktivera målgrupper till mål.](/help/destinations/assets/overview/export-identities-to-destination.png "Markera identitetsnamnområdet som är markerat i arbetsflödet för att aktivera målgrupper till mål."){width="100" zoomable="yes"}

Se [Aktivera målgruppsdata för att batchprofilera exportmål](../../ui/activate-batch-profile-destinations.md) för instruktioner om hur du aktiverar målgrupper till det här målet.

### Schemaläggning

I steget **[!UICONTROL Scheduling]** kan du [ställa in exportschemat](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling) för ditt [!DNL Data Landing Zone]-mål och du kan även [konfigurera namnet på dina exporterade filer](/help/destinations/ui/activate-batch-profile-destinations.md#file-names).

### Mappa attribut och identiteter {#map}

I steget **[!UICONTROL Mapping]** kan du välja vilka attribut- och identitetsfält som ska exporteras för dina profiler. Du kan också välja att ändra rubrikerna i den exporterade filen till ett valfritt användarvänligt namn. Mer information finns i [mappningssteget](/help/destinations/ui/activate-batch-profile-destinations.md#mapping) i självstudiekursen om aktivering av gruppmål.

## Validera slutförd dataexport {#exported-data}

Kontrollera [!DNL Data Landing Zone]-lagringen och se till att de exporterade filerna innehåller de förväntade profilpopulationerna för att kontrollera om data har exporterats.
