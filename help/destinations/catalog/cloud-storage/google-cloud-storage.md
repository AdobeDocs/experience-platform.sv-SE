---
title: Google Cloud-lagringsanslutning
description: Lär dig hur du ansluter till Google Cloud Storage och aktiverar målgrupper eller exporterar datauppsättningar.
last-substantial-update: 2023-07-26T00:00:00Z
exl-id: ab274270-ae8c-4264-ba64-700b118e6435
source-git-commit: 16365865e349f8805b8346ec98cdab89cd027363
workflow-type: tm+mt
source-wordcount: '978'
ht-degree: 0%

---

# [!DNL Google Cloud Storage] anslutning

## Översikt {#overview}

Skapa en utgående liveanslutning till [!DNL Google Cloud Storage] att regelbundet exportera datafiler från Adobe Experience Platform till era egna.

## Anslut till [!DNL Google Cloud Storage] lagring via API eller användargränssnitt {#connect-api-or-ui}

* Ansluta till [!DNL Google Cloud Storage] lagringsplats med hjälp av användargränssnittet för plattformen, läs avsnitten [Anslut till målet](#connect) och [Aktivera målgrupper till det här målet](#activate) nedan.
* Ansluta till [!DNL Google Cloud Storage] lagringsplats via programmering, läs [Aktivera målgrupper för filbaserade mål med hjälp av API-självstudiekursen för Flow Service](../../api/activate-segments-file-based-destinations.md).

## Målgrupper {#supported-audiences}

I det här avsnittet beskrivs alla målgrupper som du kan exportera till det här målet.

Detta mål stöder aktivering av alla målgrupper som genererats via Experience Platform [Segmenteringstjänst](../../../segmentation/home.md).

*Dessutom* stöder denna destination även aktivering av målgrupper som beskrivs i tabellen nedan.

| Målgruppstyp | Beskrivning |
---------|----------|
| Anpassade överföringar | Målgrupper [importerad](../../../segmentation/ui/overview.md#import-audience) till Experience Platform från CSV-filer. |

{style="table-layout:auto"}

## Exportera typ och frekvens {#export-type-frequency}

Se tabellen nedan för information om exporttyp och frekvens för destinationen.

| Objekt | Typ | Anteckningar |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Profile-based]** | Du exporterar alla medlemmar i ett segment, tillsammans med tillämpliga schemafält, som de har valts på skärmen Välj profilattribut i [arbetsflöde för målaktivering](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| Exportfrekvens | **[!UICONTROL Batch]** | Batchdestinationer exporterar filer till efterföljande plattformar i steg om tre, sex, åtta, tolv eller tjugofyra timmar. Läs mer om [gruppfilsbaserade mål](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## Förutsättningar för att ansluta [!DNL Google Cloud Storage] konto {#prerequisites}

För att kunna ansluta plattformen till [!DNL Google Cloud Storage]måste du först aktivera interoperabilitet för [!DNL Google Cloud Storage] konto. Öppna för att få åtkomst till inställningen för interoperabilitet [!DNL Google Cloud Platform] och markera **[!UICONTROL Settings]** från **[!UICONTROL Cloud Storage]** i navigeringspanelen.

![Kontrollpanelen för Google Cloud-plattformen med molnlagring och inställningar markerade.](../../../sources/images/tutorials/create/google-cloud-storage/nav.png)

The **[!UICONTROL Settings]** visas. Här kan du se information om [!DNL Google] projekt-ID och information om [!DNL Google Cloud Storage] konto. Om du vill komma åt inställningarna för interoperabilitet väljer du **[!UICONTROL Interoperability]** i det övre sidhuvudet.

![Fliken Interoperabilitet visas på kontrollpanelen för Google Cloud-plattformen.](../../../sources/images/tutorials/create/google-cloud-storage/project-access.png)

The **[!UICONTROL Interoperability]** sidan innehåller information om autentisering, åtkomstnycklar och standardprojektet som är kopplat till ditt tjänstkonto. Om du vill generera ett nytt åtkomstnyckel-ID och en hemlig åtkomstnyckel för ditt tjänstkonto väljer du **[!UICONTROL Create a Key for a Service Account]**.

![Create a key for a service account control selected in the Google Cloud Platform dashboard.](../../../sources/images/tutorials/create/google-cloud-storage/interoperability.png)

Du kan använda ditt nyligen genererade ID för åtkomstnyckel och hemlig åtkomstnyckel för att ansluta din [!DNL Google Cloud Storage] konto till plattform.

## Anslut till målet {#connect}

>[!IMPORTANT]
> 
>Om du vill ansluta till målet behöver du **[!UICONTROL Manage Destinations]** [behörighet för åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontroll - översikt](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få de behörigheter som krävs.

Om du vill ansluta till det här målet följer du stegen som beskrivs i [självstudiekurs om destinationskonfiguration](/help/destinations/ui/connect-destination.md). I arbetsflödet för målkonfiguration fyller du i fälten som listas i de två avsnitten nedan.

### Autentisera till mål {#authenticate}

Om du vill autentisera mot målet fyller du i de obligatoriska fälten och väljer **[!UICONTROL Connect to destination]**.

* **[!UICONTROL Access key ID]**: En alfanumerisk sträng på 61 tecken som används för att autentisera [!DNL Google Cloud Storage] konto till plattform. Mer information om hur du får fram det här värdet finns i [krav](#prerequisites) ovan.
* **[!UICONTROL Secret access key]**: En 40-tecken, base64-kodad sträng som används för att autentisera [!DNL Google Cloud Storage] konto till plattform. Mer information om hur du får fram det här värdet finns i [krav](#prerequisites) ovan.
* **[!UICONTROL Encryption key]**: Om du vill kan du bifoga den RSA-formaterade offentliga nyckeln för att lägga till kryptering i de exporterade filerna. Visa ett exempel på en korrekt formaterad krypteringsnyckel i bilden nedan.

  ![Bild som visar ett exempel på en korrekt formaterad PGP-nyckel i användargränssnittet](../../assets/catalog/cloud-storage/sftp/pgp-key.png)

Mer information om dessa värden finns i [Google Cloud Storage HMAC-nycklar](https://cloud.google.com/storage/docs/authentication/hmackeys#overview) guide. Anvisningar om hur du skapar ditt eget ID för åtkomstnyckel och hemlig åtkomstnyckel finns i [[!DNL Google Cloud Storage] källöversikt](/help/sources/connectors/cloud-storage/google-cloud-storage.md).

### Fyll i målinformation {#destination-details}

Om du vill konfigurera information för målet fyller du i de obligatoriska och valfria fälten nedan. En asterisk bredvid ett fält i användargränssnittet anger att fältet är obligatoriskt.

* **[!UICONTROL Name]**: Fyll i det önskade namnet för det här målet.
* **[!UICONTROL Description]**: Valfritt. Du kan till exempel ange vilken kampanj du använder det här målet för.
* **[!UICONTROL Bucket name]**: Ange namnet på [!DNL Google Cloud Storage] bucket som ska användas för detta mål.
* **[!UICONTROL Folder path]**: Ange sökvägen till målmappen som ska vara värd för de exporterade filerna.
* **[!UICONTROL File type]**: välj det format som Experience Platform ska använda för de exporterade filerna. När du väljer [!UICONTROL CSV] kan du också [konfigurera filformateringsalternativ](../../ui/batch-destinations-file-formatting-options.md).
* **[!UICONTROL Compression format]**: välj den komprimeringstyp som Experience Platform ska använda för de exporterade filerna.
* **[!UICONTROL Include manifest file]**: aktivera det här alternativet om du vill att exporten ska innehålla en manifest-JSON-fil som innehåller information om exportplats, exportstorlek med mera.

### Aktivera aviseringar {#enable-alerts}

Du kan aktivera varningar för att få meddelanden om dataflödets status till ditt mål. Välj en avisering i listan om du vill prenumerera och få meddelanden om statusen för ditt dataflöde. Mer information om varningar finns i guiden på [prenumerera på destinationsvarningar med användargränssnittet](../../ui/alerts.md).

När du är klar med informationen för målanslutningen väljer du **[!UICONTROL Next]**.

## Aktivera målgrupper till det här målet {#activate}

>[!IMPORTANT]
> 
>För att aktivera data behöver du **[!UICONTROL Manage Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** och **[!UICONTROL View Segments]** [behörigheter för åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontroll - översikt](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få de behörigheter som krävs.

Se [Aktivera målgruppsdata för att batchprofilera exportmål](../../ui/activate-batch-profile-destinations.md) för instruktioner om hur du aktiverar målgrupper till det här målet.

### Schemaläggning

I **[!UICONTROL Scheduling]** kan du [konfigurera exportschemat](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling) för [!DNL Google Cloud Storage] mål och du kan också [konfigurera namnet på de exporterade filerna](/help/destinations/ui/activate-batch-profile-destinations.md#file-names).

### Mappa attribut och identiteter {#map}

I **[!UICONTROL Mapping]** kan du välja vilka attribut- och identitetsfält som ska exporteras för dina profiler. Du kan också välja att ändra rubrikerna i den exporterade filen till ett valfritt användarvänligt namn. Mer information finns i [mappningssteg](/help/destinations/ui/activate-batch-profile-destinations.md#mapping) i självstudiekursen om att aktivera gruppdestinationer.

## (Beta) Exportera datauppsättningar {#export-datasets}

Detta mål stöder datauppsättningsexporter. Fullständig information om hur du ställer in datauppsättningsexporter finns i självstudiekurserna:

* Så här gör du [exportera datauppsättningar med hjälp av användargränssnittet för plattformen](/help/destinations/ui/export-datasets.md).
* Så här gör du [exportera datauppsättningar via programmering med API:t för Flow Service](/help/destinations/api/export-datasets.md).

## Validera slutförd dataexport {#exported-data}

Kontrollera dina [!DNL Google Cloud Storage] och se till att de exporterade filerna innehåller de förväntade profilpopulationerna.
