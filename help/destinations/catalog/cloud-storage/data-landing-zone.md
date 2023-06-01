---
title: Data Landing Zone-mål
description: Lär dig hur du ansluter till Data Landing Zone för att aktivera segment och exportera datauppsättningar.
exl-id: 40b20faa-cce6-41de-81a0-5f15e6c00e64
source-git-commit: 55f72e4f229e18648e0e745a2a60e9add50455b0
workflow-type: tm+mt
source-wordcount: '1162'
ht-degree: 0%

---

# (Beta) Data Landing Zone-mål

>[!IMPORTANT]
>
>* Den här destinationen finns för närvarande i betaversionen och är endast tillgänglig för ett begränsat antal kunder. Om du vill begära åtkomst till [!DNL Data Landing Zone] kontakta din Adobe-representant och uppge [!DNL Organization ID].
>* Dokumentationssidan refererar till [!DNL Data Landing Zone] *mål*. Det finns också en [!DNL Data Landing Zone] *källa* i källkatalogen. Mer information finns i [[!DNL Data Landing Zone] källa](/help/sources/connectors/cloud-storage/data-landing-zone.md) dokumentation.



## Översikt {#overview}

[!DNL Data Landing Zone] är en [!DNL Azure Blob] lagringsgränssnittet som tillhandahålls av Adobe Experience Platform och ger dig tillgång till en säker, molnbaserad fillagringsfunktion för att exportera filer från plattformar. Du har tillgång till en [!DNL Data Landing Zone] behållare per sandlåda och den totala datavolymen för alla behållare begränsas till den totala datamängd som ingår i din licens för plattformsprodukter och -tjänster. Alla kunder med Platform och dess programtjänster som [!DNL Customer Journey Analytics], [!DNL Journey Orchestration], [!DNL Intelligent Services]och [!DNL Real-Time Customer Data Platform] har etablerats med en [!DNL Data Landing Zone] behållare per sandlåda. Du kan läsa och skriva filer till behållaren via [!DNL Azure Storage Explorer] eller kommandoradsgränssnittet.

[!DNL Data Landing Zone] stöder SAS-baserad autentisering och dess data skyddas med standard [!DNL Azure Blob] Mekanismer för förvaringssäkerhet i vila och under transitering. SAS-baserad autentisering ger säker åtkomst till [!DNL Data Landing Zone] behållaren via en offentlig internetanslutning. Du behöver inte göra några nätverksändringar [!DNL Data Landing Zone] container, vilket betyder att du inte behöver konfigurera några tillåtelselista- eller korsregionsinställningar för ditt nätverk.

Plattformen har en strikt TTL-regel (time-to-live) på sju dagar för alla filer som överförs till en [!DNL Data Landing Zone] behållare. Alla filer tas bort efter sju dagar.

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

Du kan använda [[!DNL Azure Storage Explorer]](https://azure.microsoft.com/en-us/features/storage-explorer/) för att hantera innehållet i [!DNL Data Landing Zone] behållare. Börja använda [!DNL Data Landing Zone], måste du först hämta dina inloggningsuppgifter och ange dem i [!DNL Azure Storage Explorer]och koppla samman [!DNL Data Landing Zone] behållare till [!DNL Azure Storage Explorer].

I [!DNL Azure Storage Explorer] Välj anslutningsikonen i det vänstra navigeringsfältet. The **Välj resurs** visas så att du kan ansluta till dem. Välj **[!DNL Blob container]** för att ansluta till [!DNL Data Landing Zone] lagring.

![select-resource](/help/sources/images/tutorials/create/dlz/select-resource.png)

Nästa, välj **URL för delad åtkomstsignatur (SAS)** som anslutningsmetod och välj **Nästa**.

![select-connection-method](/help/sources/images/tutorials/create/dlz/select-connection-method.png)

När du har valt anslutningsmetod måste du ange en **visningsnamn** och **[!DNL Blob]container SAS-URL** som motsvarar dina [!DNL Data Landing Zone] behållare.

>[!BEGINSHADEBOX]

### Hämta autentiseringsuppgifterna för din [!DNL Data Landing Zone]

Du måste använda plattforms-API:erna för att hämta [!DNL Data Landing Zone] autentiseringsuppgifter. API-anropet för att hämta dina autentiseringsuppgifter beskrivs nedan. Mer information om hur du hämtar de värden som krävs för rubrikerna finns i [Komma igång med Adobe Experience Platform API:er](/help/landing/api-guide.md) guide.

**API-format**

```http
GET /data/foundation/connectors/landingzone/credentials?type=dlz_destination
```

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

Följande svar returnerar autentiseringsuppgifter för din landningszon, inklusive din nuvarande `SASToken` och `SASUri`, samt `storageAccountName` som motsvarar behållaren för landningszonen.

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

>[!ENDSHADEBOX]

Ange ditt visningsnamn (`containerName`) och [!DNL Data Landing Zone] SAS-URL, som returneras i det API-anrop som beskrivs ovan, och välj sedan **Nästa**.

![enter-connection-info](/help/sources/images/tutorials/create/dlz/enter-connection-info.png)

The **Sammanfattning** visas så att du får en översikt över dina inställningar, inklusive information om [!DNL Blob] slutpunkt och behörigheter. Välj **Anslut**.

![sammanfattning](/help/sources/images/tutorials/create/dlz/summary.png)

Anslutningen uppdaterar [!DNL Azure Storage Explorer] Gränssnitt med [!DNL Data Landing Zone] behållare.

![dlz-user-container](/help/sources/images/tutorials/create/dlz/dlz-user-container.png)

Med [!DNL Data Landing Zone] behållare ansluten till [!DNL Azure Storage Explorer]kan du nu börja exportera filer från Experience Platform till [!DNL Data Landing Zone] behållare. Om du vill exportera filer måste du skapa en anslutning till [!DNL Data Landing Zone] mål i användargränssnittet i Experience Platform, enligt beskrivningen i avsnittet nedan.

## Anslut till målet {#connect}

>[!IMPORTANT]
> 
>Om du vill ansluta till målet behöver du **[!UICONTROL Manage Destinations]** [åtkomstkontrollbehörighet](/help/access-control/home.md#permissions). Läs [åtkomstkontroll - översikt](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få de behörigheter som krävs.

Om du vill ansluta till det här målet följer du stegen som beskrivs i [självstudiekurs om destinationskonfiguration](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html). I arbetsflödet för målkonfiguration fyller du i fälten som listas i de två avsnitten nedan.

### Autentisera till mål {#authenticate}

Kontrollera att du har anslutit [!DNL Data Landing Zone] behållare till [!DNL Azure Storage Explorer] enligt beskrivningen i [krav](#prerequisites) -avsnitt. För [!DNL Data Landing Zone] är ett lagringsutrymme som tillhandahålls av Adobe behöver du inte utföra några ytterligare steg i användargränssnittet i Experience Platform för att autentisera mot målet.

### Fyll i målinformation {#destination-details}

Om du vill konfigurera information för målet fyller du i de obligatoriska och valfria fälten nedan. En asterisk bredvid ett fält i användargränssnittet anger att fältet är obligatoriskt.

* **[!UICONTROL Name]**: Fyll i det önskade namnet för det här målet.
* **[!UICONTROL Description]**: Valfritt. Du kan till exempel ange vilken kampanj du använder det här målet för.
* **[!UICONTROL Folder path]**: Ange sökvägen till målmappen som ska vara värd för de exporterade filerna.
* **[!UICONTROL File type]**: väljer du vilket format Experience Platform ska använda för de exporterade filerna. När du väljer [!UICONTROL CSV] kan du också [konfigurera filformateringsalternativ](../../ui/batch-destinations-file-formatting-options.md).
* **[!UICONTROL Compression format]**: välj den komprimeringstyp som Experience Platform ska använda för de exporterade filerna.
* 
   * **[!UICONTROL Include manifest file]**: aktivera det här alternativet om du vill att exporten ska innehålla en manifestfil för JSON som innehåller information om exportplats, exportstorlek och mycket annat.

### Aktivera aviseringar {#enable-alerts}

Du kan aktivera varningar för att få meddelanden om dataflödets status till ditt mål. Välj en avisering i listan om du vill prenumerera och få meddelanden om status för ditt dataflöde. Mer information om varningar finns i guiden [prenumerera på destinationsvarningar med hjälp av användargränssnittet](../../ui/alerts.md).

När du är klar med informationen för målanslutningen väljer du **[!UICONTROL Next]**.

## Aktivera segment till den här destinationen {#activate}

>[!IMPORTANT]
> 
>Om du vill aktivera data måste du ha **[!UICONTROL Manage Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** och **[!UICONTROL View Segments]** [behörigheter för åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontroll - översikt](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få de behörigheter som krävs.

Se [Aktivera målgruppsdata för att batchprofilera exportmål](../../ui/activate-batch-profile-destinations.md) om du vill ha instruktioner om hur du aktiverar målgruppssegment till det här målet.

### Schemaläggning

I **[!UICONTROL Scheduling]** kan du [konfigurera exportschemat](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling) för [!DNL Data Landing Zone] mål och du kan också [konfigurera namnet på de exporterade filerna](/help/destinations/ui/activate-batch-profile-destinations.md#file-names).

### Mappa attribut och identiteter {#map}

I **[!UICONTROL Mapping]** kan du välja vilka attribut- och identitetsfält som ska exporteras för dina profiler. Du kan också välja att ändra rubrikerna i den exporterade filen till ett valfritt användarvänligt namn. Mer information finns i [mappningssteg](/help/destinations/ui/activate-batch-profile-destinations.md#mapping) i självstudiekursen om att aktivera gruppdestinationer.

## (Beta) Exportera datauppsättningar {#export-datasets}

Detta mål stöder datauppsättningsexporter. Fullständig information om hur du ställer in datauppsättningsexporter finns i [självstudiekurs om hur du exporterar datauppsättningar](/help/destinations/ui/export-datasets.md).

## Validera slutförd dataexport {#exported-data}

Kontrollera dina [!DNL Data Landing Zone] och se till att de exporterade filerna innehåller de förväntade profilpopulationerna.
