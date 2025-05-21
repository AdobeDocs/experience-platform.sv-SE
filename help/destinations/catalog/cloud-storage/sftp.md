---
title: SFTP-anslutning
description: Skapa en utgående liveanslutning till SFTP-servern för att regelbundet exportera avgränsade datafiler från Adobe Experience Platform.
exl-id: 27abfc38-ec19-4321-b743-169370d585a0
source-git-commit: 45f22addbff9ec81d64e9e756e4c27e8af4b477d
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# SFTP-anslutning

## Destinationsändringslogg {#changelog}

I juli 2023-versionen av Experience Platform har SFTP-målet nya funktioner enligt nedan:

* [Exportstöd för datauppsättningar](/help/destinations/ui/export-datasets.md).
* Ytterligare [namngivningsalternativ](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling).
* Möjlighet att ange anpassade filhuvuden i de exporterade filerna via det [förbättrade mappningssteget](/help/destinations/ui/activate-batch-profile-destinations.md#mapping).
* [Möjlighet att anpassa formateringen för exporterade CSV-datafiler](/help/destinations/ui/batch-destinations-file-formatting-options.md).

## Översikt {#overview}

Skapa en utgående liveanslutning till SFTP-servern för att regelbundet exportera avgränsade datafiler från Adobe Experience Platform.

>[!IMPORTANT]
>
> Experience Platform stöder dataexport till SFTP-servrar, men de rekommenderade molnlagringsplatserna för dataexport är [!DNL Amazon S3] och [!DNL Azure Blob].

## Ansluta till SFTP via API eller gränssnitt {#connect-api-or-ui}

* Läs avsnitten [Anslut till målet](#connect) och [Aktivera målgrupper till det här målet](#activate) nedan om du vill ansluta till din SFTP-lagringsplats med Experience Platform-användargränssnittet.
* Om du vill ansluta till din SFTP-lagringsplats programmatiskt läser du [Aktivera målgrupper till filbaserade mål med hjälp av API-självstudiekursen för Flow Service](../../api/activate-segments-file-based-destinations.md).

## Målgrupper {#supported-audiences}

I det här avsnittet beskrivs vilka typer av målgrupper du kan exportera till det här målet.

| Målgruppsursprung | Stöds | Beskrivning |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Publiker som genererats via Experience Platform [segmenteringstjänst](../../../segmentation/home.md). |
| Anpassade överföringar | ✓ | Publikerna [importerade](../../../segmentation/ui/audience-portal.md#import-audience) till Experience Platform från CSV-filer. |

{style="table-layout:auto"}

## Exportera typ och frekvens {#export-type-frequency}

Se tabellen nedan för information om exporttyp och frekvens för destinationen.

| Objekt | Typ | Anteckningar |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Profile-based]** | Du exporterar alla medlemmar i ett segment tillsammans med de önskade schemafälten (t.ex. e-postadress, telefonnummer, efternamn), som du har valt på skärmen Välj profilattribut i arbetsflödet för [målaktivering](../../ui/activate-batch-profile-destinations.md#select-attributes). |
| Exportfrekvens | **[!UICONTROL Batch]** | Batchdestinationer exporterar filer till efterföljande plattformar i steg om tre, sex, åtta, tolv eller tjugofyra timmar. Läs mer om [gruppfilsbaserade mål](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

![Profilbaserad SFTP-exporttyp markerad i målkatalogen.](../../assets/catalog/cloud-storage/sftp/catalog.png)

## Exportera datauppsättningar {#export-datasets}

Detta mål stöder datauppsättningsexporter. Fullständig information om hur du ställer in datauppsättningsexporter finns i självstudiekurserna:

* Så här [exporterar du datauppsättningar med Experience Platform användargränssnitt](/help/destinations/ui/export-datasets.md).
* Så här [exporterar du datauppsättningar programmatiskt med API:t för Flow Service ](/help/destinations/api/export-datasets.md).

## Filformat för exporterade data {#file-format}

När du exporterar *målgruppsdata* skapar Experience Platform en `.csv` -, `parquet` - eller `.json` -fil på den angivna lagringsplatsen. Mer information om filerna finns i avsnittet [Filformat som stöds för export](../../ui/activate-batch-profile-destinations.md#supported-file-formats-export) i självstudiekursen om målgruppsaktivering.

När du exporterar *datauppsättningar* skapar Experience Platform en `.parquet`- eller `.json`-fil på den lagringsplats som du angav. Mer information om filerna finns i avsnittet [Verifiera lyckad datauppsättningsexport](../../ui/export-datasets.md#verify) i självstudiekursen om exportdatamängder.

## Anslutningskrav för SFTP-server {#sftp-connection-requirements}

För att dataexporten ska lyckas måste du konfigurera SFTP-målservern så att ett tillräckligt antal samtidiga anslutningar tillåts. Om din SFTP-server begränsar antalet samtidiga anslutningar kan du råka ut för misslyckade exportjobb, särskilt när du exporterar flera målgrupper eller datauppsättningar samtidigt.

**Rekommendation**
För optimala prestanda bör SFTP-servern tillåta minst en samtidig anslutning för varje målgrupp eller datauppsättning som exporteras. Servern bör minst ha stöd för minst 30 % av det totala antalet målgrupper eller datauppsättningar som schemalagts för export samtidigt.

**Exempel**\
Om du schemalägger export för 100 målgrupper eller datauppsättningar samtidigt bör SFTP-servern tillåta minst 30 samtidiga anslutningar.

Om du konfigurerar anslutningsgränserna för SFTP-servern korrekt kan du förhindra misslyckad export och säkerställa tillförlitlig dataleverans från Adobe Experience Platform.

## Anslut till målet {#connect}

>[!IMPORTANT]
> 
>Om du vill ansluta till målet behöver du behörigheterna **[!UICONTROL View Destinations]** och **[!UICONTROL Manage Destinations]** [åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontrollsöversikten](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få den behörighet som krävs.

Om du vill ansluta till det här målet följer du stegen som beskrivs i självstudiekursen [för destinationskonfiguration](../../ui/connect-destination.md). I arbetsflödet för att konfigurera mål fyller du i fälten som listas i de två avsnitten nedan.

### Autentiseringsinformation {#authentication-information}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_sftp_rsa"
>title="RSA offentlig nyckel"
>abstract="Du kan också bifoga den RSA-formaterade offentliga nyckeln för att lägga till kryptering till de exporterade filerna. Visa ett exempel på en korrekt formaterad nyckel i dokumentationslänken nedan."

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_sftp_ssh"
>title="Privat SSH-nyckel"
>abstract="Den privata SSH-nyckeln måste vara en RSA-formaterad, Base64-kodad sträng och får inte vara lösenordsskyddad."

Om du väljer autentiseringstypen **[!UICONTROL SFTP with password]** för att ansluta till din SFTP-plats:

![Grundläggande autentisering med lösenord för SFTP-mål.](../../assets/catalog/cloud-storage/sftp/stfp-basic-authentication.png)

* **[!UICONTROL Domain]**: Adress till din SFTP-lagringsplats.
* **[!UICONTROL Username]**: Användarnamnet som loggas in på din SFTP-lagringsplats;
* **[!UICONTROL Port]**: Den port som används av din SFTP-lagringsplats;
* **[!UICONTROL Password]**: Lösenordet för att logga in på din SFTP-lagringsplats.
* **[!UICONTROL Encryption key]**: Om du vill kan du bifoga den RSA-formaterade offentliga nyckeln för att lägga till kryptering i de exporterade filerna. Visa ett exempel på en korrekt formaterad krypteringsnyckel i bilden nedan.

  ![Bild som visar ett exempel på en korrekt formaterad PGP-nyckel i gränssnittet.](../../assets/catalog/cloud-storage/sftp/pgp-key.png)


Om du väljer autentiseringstypen **[!UICONTROL SFTP with SSH key]** för att ansluta till din SFTP-plats:

![SSH-nyckelautentisering för SFTP-mål.](../../assets/catalog/cloud-storage/sftp/sftp-ssh-key-authentication.png)

* **[!UICONTROL Domain]**: Fyll i IP-adressen eller domännamnet för ditt SFTP-konto
* **[!UICONTROL Port]**: Den port som används av din SFTP-lagringsplats;
* **[!UICONTROL Username]**: Användarnamnet som loggas in på din SFTP-lagringsplats;
* **[!UICONTROL SSH Key]**: Den privata SSH-nyckeln som används för att logga in på din SFTP-lagringsplats. Den privata nyckeln måste vara en RSA-formaterad, Base64-kodad sträng och får inte vara lösenordsskyddad.
* **[!UICONTROL Encryption key]**: Om du vill kan du bifoga den RSA-formaterade offentliga nyckeln för att lägga till kryptering i de exporterade filerna. Visa ett exempel på en korrekt formaterad krypteringsnyckel i bilden nedan.

  ![Bild som visar ett exempel på en korrekt formaterad PGP-nyckel i gränssnittet.](../../assets/catalog/cloud-storage/sftp/pgp-key.png)

### Destinationsinformation {#destination-details}

När du har upprättat autentiseringsanslutningen till SFTP-platsen anger du följande information för målet:

![Målinformationsfält för SFTP-målet.](../../assets/catalog/cloud-storage/sftp/sftp-destination-details.png)

* **[!UICONTROL Name]**: Ange ett namn som hjälper dig att identifiera det här målet i Experience Platform användargränssnitt;
* **[!UICONTROL Description]**: Ange en beskrivning för det här målet;
* **[!UICONTROL Folder path]**: Ange sökvägen till mappen på din SFTP-plats där filerna ska exporteras.
* **[!UICONTROL File type]**: Välj det format som Experience Platform ska använda för de exporterade filerna. När du väljer alternativet [!UICONTROL CSV] kan du även [konfigurera filformateringsalternativen](../../ui/batch-destinations-file-formatting-options.md).
* **[!UICONTROL Compression format]**: Välj den komprimeringstyp som Experience Platform ska använda för de exporterade filerna.
* **[!UICONTROL Include manifest file]**: Aktivera det här alternativet om du vill att exporten ska innehålla en manifestfil för JSON som innehåller information om exportplats, exportstorlek och mycket annat. Manifestet har fått ett namn i formatet `manifest-<<destinationId>>-<<dataflowRunId>>.json`. Visa en [exempelmanifestfil](/help/destinations/assets/common/manifest-d0420d72-756c-4159-9e7f-7d3e2f8b501e-0ac8f3c0-29bd-40aa-82c1-f1b7e0657b19.json). Manifestfilen innehåller följande fält:
   * `flowRunId`: [Dataflödet kör](/help/dataflows/ui/monitor-destinations.md#dataflow-runs-for-batch-destinations) som genererade den exporterade filen.
   * `scheduledTime`: Tiden i UTC när filen exporterades.
   * `exportResults.sinkPath`: Sökvägen till lagringsplatsen där den exporterade filen placeras.
   * `exportResults.name`: Namnet på den exporterade filen.
   * `size`: Den exporterade filens storlek i byte.

## Aktivera målgrupper till det här målet {#activate}

>[!IMPORTANT]
> 
>* För att aktivera data behöver du behörigheterna **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** och **[!UICONTROL View Segments]** [åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontrollsöversikten](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få den behörighet som krävs.
>* Om du vill exportera *identiteter* måste du ha **[!UICONTROL View Identity Graph]** [åtkomstkontrollbehörighet](/help/access-control/home.md#permissions). <br> ![Markera identitetsnamnområdet som är markerat i arbetsflödet för att aktivera målgrupper till mål.](/help/destinations/assets/overview/export-identities-to-destination.png "Markera identitetsnamnområdet som är markerat i arbetsflödet för att aktivera målgrupper till mål."){width="100" zoomable="yes"}

Se [Aktivera målgruppsdata för att batchprofilera exportmål](../../ui/activate-batch-profile-destinations.md) för instruktioner om hur du aktiverar målgrupper till det här målet.

## Validera slutförd dataexport {#exported-data}

Kontrollera SFTP-lagringen och se till att de exporterade filerna innehåller de förväntade profilpopulationerna för att kontrollera om data har exporterats.

## IP-adress tillåtelselista {#ip-address-allow-list}

Läs artikeln [IP-adressen tillåtelselista](ip-address-allow-list.md) om du behöver lägga till Adobe IP-adresser i en tillåtelselista.
