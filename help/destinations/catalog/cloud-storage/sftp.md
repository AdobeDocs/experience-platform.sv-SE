---
title: SFTP-anslutning
description: Skapa en utgående liveanslutning till SFTP-servern för att regelbundet exportera avgränsade datafiler från Adobe Experience Platform.
exl-id: 27abfc38-ec19-4321-b743-169370d585a0
source-git-commit: 93b1c26e85ddd0fa232b26712f88faa824f19f30
workflow-type: tm+mt
source-wordcount: '970'
ht-degree: 0%

---

# SFTP-anslutning

## Destinationsändringslogg {#changelog}

I juli 2023-Experience Platform-versionen innehåller SFTP-målet nya funktioner enligt nedan:

* [Stöd för dataexport](/help/destinations/ui/export-datasets.md).
* Ytterligare [filnamnsalternativ](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling).
* Möjlighet att ange anpassade filhuvuden i de exporterade filerna via [förbättrat mappningssteg](/help/destinations/ui/activate-batch-profile-destinations.md#mapping).
* [Möjlighet att anpassa formateringen i exporterade CSV-datafiler](/help/destinations/ui/batch-destinations-file-formatting-options.md).

## Översikt {#overview}

Skapa en utgående liveanslutning till SFTP-servern för att regelbundet exportera avgränsade datafiler från Adobe Experience Platform.

>[!IMPORTANT]
>
> Experience Platform stöder dataexport till SFTP-servrar, men de rekommenderade molnlagringsplatserna för dataexport är [!DNL Amazon S3] och [!DNL Azure Blob].

## Ansluta till SFTP via API eller gränssnitt {#connect-api-or-ui}

* Läs avsnitten om hur du ansluter till din SFTP-lagringsplats med hjälp av användargränssnittet för plattformen [Anslut till målet](#connect) och [Aktivera målgrupper till det här målet](#activate) nedan.
* Om du vill ansluta till din SFTP-lagringsplats via programkod läser du [Aktivera målgrupper för filbaserade mål med hjälp av API-självstudiekursen för Flow Service](../../api/activate-segments-file-based-destinations.md).

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
| Exporttyp | **[!UICONTROL Profile-based]** | Du exporterar alla medlemmar i ett segment tillsammans med de önskade schemafälten (t.ex. e-postadress, telefonnummer, efternamn), som du har valt på skärmen Välj profilattribut i [arbetsflöde för målaktivering](../../ui/activate-batch-profile-destinations.md#select-attributes). |
| Exportfrekvens | **[!UICONTROL Batch]** | Batchdestinationer exporterar filer till efterföljande plattformar i steg om tre, sex, åtta, tolv eller tjugofyra timmar. Läs mer om [gruppfilsbaserade mål](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

![Profilbaserad SFTP-exporttyp](../../assets/catalog/cloud-storage/sftp/catalog.png)

## Anslut till målet {#connect}

>[!IMPORTANT]
> 
>Om du vill ansluta till målet behöver du **[!UICONTROL Manage Destinations]** [behörighet för åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontroll - översikt](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få de behörigheter som krävs.

Om du vill ansluta till det här målet följer du stegen som beskrivs i [självstudiekurs om destinationskonfiguration](../../ui/connect-destination.md). I arbetsflödet för att konfigurera mål fyller du i fälten som listas i de två avsnitten nedan.

### Autentiseringsinformation {#authentication-information}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_sftp_rsa"
>title="RSA offentlig nyckel"
>abstract="Du kan också bifoga den RSA-formaterade offentliga nyckeln för att lägga till kryptering till de exporterade filerna. Visa ett exempel på en korrekt formaterad nyckel i dokumentationslänken nedan."

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_sftp_ssh"
>title="Privat SSH-nyckel"
>abstract="Den privata SSH-nyckeln måste vara en RSA-formaterad, Base64-kodad sträng och får inte vara lösenordsskyddad."

Om du väljer **[!UICONTROL SFTP with password]** autentiseringstyp för att ansluta till din SFTP-plats:

![Grundläggande autentisering för SFTP-mål](../../assets/catalog/cloud-storage/sftp/stfp-basic-authentication.png)

* **[!UICONTROL Domain]**: Adress till din SFTP-lagringsplats.
* **[!UICONTROL Username]**: Användarnamnet som ska loggas in på din SFTP-lagringsplats;
* **[!UICONTROL Port]**: Den port som används av SFTP-lagringsplatsen;
* **[!UICONTROL Password]**: Lösenordet för att logga in på din SFTP-lagringsplats.
* **[!UICONTROL Encryption key]**: Om du vill kan du bifoga den RSA-formaterade offentliga nyckeln för att lägga till kryptering i de exporterade filerna. Visa ett exempel på en korrekt formaterad krypteringsnyckel i bilden nedan.

  ![Bild som visar ett exempel på en korrekt formaterad PGP-nyckel i användargränssnittet](../../assets/catalog/cloud-storage/sftp/pgp-key.png)


Om du väljer **[!UICONTROL SFTP with SSH key]** autentiseringstyp för att ansluta till din SFTP-plats:

![SSH-nyckelautentisering för SFTP-mål](../../assets/catalog/cloud-storage/sftp/sftp-ssh-key-authentication.png)

* **[!UICONTROL Domain]**: Fyll i IP-adressen eller domännamnet för ditt SFTP-konto
* **[!UICONTROL Port]**: Den port som används av SFTP-lagringsplatsen;
* **[!UICONTROL Username]**: Användarnamnet som ska loggas in på din SFTP-lagringsplats;
* **[!UICONTROL SSH Key]**: Den privata SSH-nyckeln som används för att logga in på din SFTP-lagringsplats. Den privata nyckeln måste vara en RSA-formaterad, Base64-kodad sträng och får inte vara lösenordsskyddad.
* **[!UICONTROL Encryption key]**: Om du vill kan du bifoga den RSA-formaterade offentliga nyckeln för att lägga till kryptering i de exporterade filerna. Visa ett exempel på en korrekt formaterad krypteringsnyckel i bilden nedan.

  ![Bild som visar ett exempel på en korrekt formaterad PGP-nyckel i användargränssnittet](../../assets/catalog/cloud-storage/sftp/pgp-key.png)

### Destinationsinformation {#destination-details}

När du har upprättat autentiseringsanslutningen till SFTP-platsen anger du följande information för målet:

![Tillgänglig målinformation för SFTP-mål](../../assets/catalog/cloud-storage/sftp/sftp-destination-details.png)

* **[!UICONTROL Name]**: Ange ett namn som gör det lättare att identifiera destinationen i användargränssnittet i Experience Platform;
* **[!UICONTROL Description]**: Ange en beskrivning av destinationen;
* **[!UICONTROL Folder path]**: Ange sökvägen till mappen på din SFTP-plats där filerna ska exporteras.
* **[!UICONTROL File type]**: Välj det format som Experience Platform ska använda för de exporterade filerna. När du väljer [!UICONTROL CSV] kan du också [konfigurera filformateringsalternativ](../../ui/batch-destinations-file-formatting-options.md).
* **[!UICONTROL Compression format]**: Välj den komprimeringstyp som Experience Platform ska använda för de exporterade filerna.
* **[!UICONTROL Include manifest file]**: Aktivera det här alternativet om du vill att exporten ska innehålla en manifestfil för JSON som innehåller information om exportplats, exportstorlek med mera. Manifestet har ett namn i formatet `manifest-<<destinationId>>-<<dataflowRunId>>.json`. Visa en [exempelmanifestfil](/help/destinations/assets/common/manifest-d0420d72-756c-4159-9e7f-7d3e2f8b501e-0ac8f3c0-29bd-40aa-82c1-f1b7e0657b19.json). Manifestfilen innehåller följande fält:
   * `flowRunId`: [dataflödeskörning](/help/dataflows/ui/monitor-destinations.md#dataflow-runs-for-batch-destinations) som genererade den exporterade filen.
   * `scheduledTime`: Tiden i UTC när filen exporterades.
   * `exportResults.sinkPath`: Sökvägen till lagringsplatsen där den exporterade filen placeras.
   * `exportResults.name`: Namnet på den exporterade filen.
   * `size`: Storleken på den exporterade filen, i byte.

## Aktivera målgrupper till det här målet {#activate}

>[!IMPORTANT]
> 
>* För att aktivera data behöver du **[!UICONTROL Manage Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** och **[!UICONTROL View Segments]** [behörigheter för åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontroll - översikt](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få de behörigheter som krävs.
>* Exportera *identiteter* behöver du **[!UICONTROL View Identity Graph]** [behörighet för åtkomstkontroll](/help/access-control/home.md#permissions). <br> ![Markera det identitetsnamnutrymme som är markerat i arbetsflödet för att aktivera målgrupper till mål.](/help/destinations/assets/overview/export-identities-to-destination.png "Markera det identitetsnamnutrymme som är markerat i arbetsflödet för att aktivera målgrupper till mål."){width="100" zoomable="yes"}

Se [Aktivera målgruppsdata för att batchprofilera exportmål](../../ui/activate-batch-profile-destinations.md) för instruktioner om hur du aktiverar målgrupper till det här målet.

## (Beta) Exportera datauppsättningar {#export-datasets}

Detta mål stöder datauppsättningsexporter. Fullständig information om hur du ställer in datauppsättningsexporter finns i självstudiekurserna:

* Så här gör du [exportera datauppsättningar med hjälp av användargränssnittet för plattformen](/help/destinations/ui/export-datasets.md).
* Så här gör du [exportera datauppsättningar via programmering med API:t för Flow Service](/help/destinations/api/export-datasets.md).

## Exporterade data {#exported-data}

För [!DNL SFTP] mål, Platform skapar en `.csv` filen på lagringsplatsen som du angav. Mer information om filerna finns i [Aktivera målgruppsdata för att batchprofilera exportmål](../../ui/activate-batch-profile-destinations.md) i självstudiekursen om målgruppsaktivering.

## IP-adress tillåtelselista {#ip-address-allow-list}

Se [IP-adress tillåtelselista för SFTP-mål](ip-address-allow-list.md) om du behöver lägga till IP-adresser för Adobe i ett tillåtelselista.
