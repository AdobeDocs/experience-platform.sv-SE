---
title: Amazon S3-anslutning
description: Skapa en utgående liveanslutning till din Amazon Web Services (AWS) S3-lagringsplats för att regelbundet exportera CSV-datafiler från Adobe Experience Platform till dina egna S3-butiker.
exl-id: 6a2a2756-4bbf-4f82-88e4-62d211cbbb38
source-git-commit: 8771aa0df001e8ef81d4ad712f4d1f9661b405b2
workflow-type: tm+mt
source-wordcount: '1398'
ht-degree: 0%

---

# [!DNL Amazon S3] anslutning {#s3-connection}

## Destinationsändringslogg {#changelog}

+++ Visa ändringslogg


| Releasamånad | Uppdateringstyp | Beskrivning |
|---|---|---|
| Januari 2024 | Funktioner och dokumentation | Amazon S3-målkopplingen har nu stöd för en ny, antagen rollautentiseringstyp. Läs mer om det i [autentiseringssektion](#assumed-role-authentication). |
| Juli 2023 | Funktioner och dokumentation | Med Experience Platform-versionen från juli 2023 [!DNL Amazon S3] mål har nya funktioner enligt nedan: <br><ul><li>[Stöd för dataexport](/help/destinations/ui/export-datasets.md)</li><li>Ytterligare [filnamnsalternativ](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling).</li><li>Möjlighet att ange anpassade filhuvuden i de exporterade filerna via [förbättrat mappningssteg](/help/destinations/ui/activate-batch-profile-destinations.md#mapping).</li><li>[Möjlighet att anpassa formateringen i exporterade CSV-datafiler](/help/destinations/ui/batch-destinations-file-formatting-options.md).</li></ul> |

{style="table-layout:auto"}

+++

## Anslut till [!DNL Amazon S3] lagring via API eller användargränssnitt {#connect-api-or-ui}

* Ansluta till [!DNL Amazon S3] lagringsplats med hjälp av användargränssnittet för plattformen, läs avsnitten [Anslut till målet](#connect) och [Aktivera målgrupper till det här målet](#activate) nedan.
* Ansluta till [!DNL Amazon S3] lagringsplats programmatiskt, läs guiden om hur du [aktivera målgrupper för filbaserade mål med hjälp av API-självstudiekursen för Flow Service](../../api/activate-segments-file-based-destinations.md).

## Målgrupper {#supported-audiences}

I det här avsnittet beskrivs vilka typer av målgrupper du kan exportera till det här målet.

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

![Profilbaserad exporttyp i Amazon S3 är markerad i USA.](../../assets/catalog/cloud-storage/amazon-s3/catalog.png)

## Exportera datauppsättningar {#export-datasets}

Detta mål stöder datauppsättningsexporter. Fullständig information om hur du ställer in datauppsättningsexporter finns i självstudiekurserna:

* Så här gör du [exportera datauppsättningar med hjälp av användargränssnittet för plattformen](/help/destinations/ui/export-datasets.md).
* Så här gör du [exportera datauppsättningar via programmering med API:t för Flow Service](/help/destinations/api/export-datasets.md).

## Filformat för exporterade data {#file-format}

Vid export *målgruppsdata*, skapar Platform en `.csv`, `parquet`, eller `.json` filen på lagringsplatsen som du angav. Mer information om filerna finns i [filformat som stöds för export](../../ui/activate-batch-profile-destinations.md#supported-file-formats-export) i självstudiekursen om målgruppsaktivering.

Vid export *datauppsättningar*, skapar Platform en `.parquet` eller `.json` filen på lagringsplatsen som du angav. Mer information om filerna finns i [verifiera lyckad datauppsättningsexport](../../ui/export-datasets.md#verify) i självstudiekursen om exportdatamängder.

## Anslut till målet {#connect}

>[!IMPORTANT]
> 
>Om du vill ansluta till målet behöver du **[!UICONTROL View Destinations]** och **[!UICONTROL Manage Destinations]** [behörigheter för åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontroll - översikt](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få de behörigheter som krävs.

Om du vill ansluta till det här målet följer du stegen som beskrivs i [självstudiekurs om destinationskonfiguration](../../ui/connect-destination.md). I arbetsflödet för målkonfiguration fyller du i fälten som listas i de två avsnitten nedan.

### Autentisera till mål {#authenticate}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_s3_rsa"
>title="RSA offentlig nyckel"
>abstract="Du kan också bifoga den RSA-formaterade offentliga nyckeln för att lägga till kryptering till de exporterade filerna. Visa ett exempel på en korrekt formaterad nyckel i dokumentationslänken nedan."

Om du vill autentisera mot målet fyller du i de obligatoriska fälten och väljer **[!UICONTROL Connect to destination]**. Amazon S3-målet har stöd för två autentiseringsmetoder:

* Åtkomstnyckel och autentisering av hemlig nyckel
* Antagen rollautentisering

#### Åtkomstnyckel och autentisering av hemlig nyckel

Använd den här autentiseringsmetoden när du vill ange din Amazon S3-åtkomstnyckel och hemlig nyckel för att tillåta Experience Platform att exportera data till dina Amazon S3-egenskaper.

![Bild av de obligatoriska fälten när du väljer åtkomstnyckel och autentisering med hemlig nyckel.](/help/destinations/assets/catalog/cloud-storage/amazon-s3/access-key-secret-key-authentication.png)

* **[!DNL Amazon S3]åtkomstnyckel** och **[!DNL Amazon S3]hemlig nyckel**: I [!DNL Amazon S3], generera ett `access key - secret access key` två för att ge plattformsåtkomst till [!DNL Amazon S3] konto. Läs mer i [Amazon Web Services-dokumentation](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html).
* **[!UICONTROL Encryption key]**: Om du vill kan du bifoga den RSA-formaterade offentliga nyckeln för att lägga till kryptering i de exporterade filerna. Visa ett exempel på en korrekt formaterad krypteringsnyckel i bilden nedan.

  ![Bild som visar ett exempel på en korrekt formaterad PGP-nyckel i användargränssnittet.](../../assets/catalog/cloud-storage/sftp/pgp-key.png)

#### Antagen roll {#assumed-role-authentication}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_s3_assumed_role"
>title="Antagen rollautentisering"
>abstract="Använd den här autentiseringstypen om du inte vill dela kontonycklar och hemliga nycklar med Adobe. I stället ansluter Experience Platform till din Amazon S3-plats med rollbaserad åtkomst. Klistra in ARN för rollen som du skapade i AWS för Adobe-användaren. Mönstret liknar `arn:aws:iam::800873819705:role/destinations-role-customer` "

![Bild av de obligatoriska fälten när du väljer antagen rollautentisering.](/help/destinations/assets/catalog/cloud-storage/amazon-s3/assumed-role-authentication.png)

Använd den här autentiseringstypen om du inte vill dela kontonycklar och hemliga nycklar med Adobe. I stället ansluter Experience Platform till din Amazon S3-plats med rollbaserad åtkomst.

Om du vill göra det måste du skapa en användare för Adobe med [rätt behörigheter](#required-s3-permission) för att skriva till era Amazon S3-program. Skapa en **[!UICONTROL Trusted entity]** i AWS med Adobe **[!UICONTROL 670664943635]**. Mer information finns i [AWS dokumentation om hur du skapar roller](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_create_for-user.html).

* **[!DNL Role]**: Klistra in ARN för rollen som du skapade i AWS för Adobe-användaren. Mönstret liknar `arn:aws:iam::800873819705:role/destinations-role-customer`.
* **[!UICONTROL Encryption key]**: Om du vill kan du bifoga den RSA-formaterade offentliga nyckeln för att lägga till kryptering i de exporterade filerna. Visa ett exempel på en korrekt formaterad krypteringsnyckel i bilden nedan.

### Fyll i målinformation {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_s3_bucket"
>title="Buckennamn"
>abstract="Måste vara mellan 3 och 63 tecken långt. Måste börja och sluta med en bokstav eller siffra. Får endast innehålla gemena bokstäver, siffror eller bindestreck ( - ). Får inte formateras som en IP-adress (till exempel 192.100.1.1)."

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_s3_folderpath"
>title="Mappsökväg"
>abstract="Får endast innehålla tecknen A-Z, a-z, 0-9 och kan innehålla följande specialtecken: `/!-_.'()"^[]+$%.*"`. Infoga makrot om du vill skapa en mapp per målgruppsfil `/%SEGMENT_NAME%` eller `/%SEGMENT_ID%` eller `/%SEGMENT_NAME%/%SEGMENT_ID%` i textfältet. Makron kan bara infogas i slutet av mappsökvägen. Visa makroexempel i dokumentationen."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/cloud-storage/overview.html#use-macros" text="Använd makron för att skapa en mapp på lagringsplatsen"

Om du vill konfigurera information för målet fyller du i de obligatoriska och valfria fälten nedan. En asterisk bredvid ett fält i användargränssnittet anger att fältet är obligatoriskt.

* **[!UICONTROL Name]**: Ange ett namn som hjälper dig att identifiera det här målet.
* **[!UICONTROL Description]**: Ange en beskrivning av destinationen.
* **[!UICONTROL Bucket name]**: Ange namnet på [!DNL Amazon S3] bucket som ska användas för detta mål.
* **[!UICONTROL Folder path]**: Ange sökvägen till målmappen som ska vara värd för de exporterade filerna.
* **[!UICONTROL File type]**: Välj det format som Experience Platform ska använda för de exporterade filerna. När du väljer [!UICONTROL CSV] kan du också [konfigurera filformateringsalternativ](../../ui/batch-destinations-file-formatting-options.md).
* **[!UICONTROL Compression format]**: Välj den komprimeringstyp som Experience Platform ska använda för de exporterade filerna.
* **[!UICONTROL Include manifest file]**: Aktivera det här alternativet om du vill att exporten ska innehålla en manifestfil för JSON som innehåller information om exportplats, exportstorlek med mera. Manifestet har ett namn i formatet `manifest-<<destinationId>>-<<dataflowRunId>>.json`. Visa en [exempelmanifestfil](/help/destinations/assets/common/manifest-d0420d72-756c-4159-9e7f-7d3e2f8b501e-0ac8f3c0-29bd-40aa-82c1-f1b7e0657b19.json). Manifestfilen innehåller följande fält:
   * `flowRunId`: [dataflödeskörning](/help/dataflows/ui/monitor-destinations.md#dataflow-runs-for-batch-destinations) som genererade den exporterade filen.
   * `scheduledTime`: Tiden i UTC när filen exporterades.
   * `exportResults.sinkPath`: Sökvägen till lagringsplatsen där den exporterade filen placeras.
   * `exportResults.name`: Namnet på den exporterade filen.
   * `size`: Storleken på den exporterade filen, i byte.

>[!TIP]
>
>I arbetsflödet för anslutningsmål kan du skapa en anpassad mapp i din Amazon S3-lagring per exporterad målgruppsfil. Läs [Använd makron för att skapa en mapp på lagringsplatsen](overview.md#use-macros) för instruktioner.

### Aktivera aviseringar {#enable-alerts}

Du kan aktivera varningar för att få meddelanden om dataflödets status till ditt mål. Välj en avisering i listan om du vill prenumerera och få meddelanden om statusen för ditt dataflöde. Mer information om varningar finns i guiden på [prenumerera på destinationsvarningar med användargränssnittet](../../ui/alerts.md).

När du är klar med informationen för målanslutningen väljer du **[!UICONTROL Next]**.

### Obligatoriskt [!DNL Amazon S3] behörigheter {#required-s3-permission}

Ansluta och exportera data till [!DNL Amazon S3] lagringsplats, skapa en IAM-användare för [!DNL Platform] in [!DNL Amazon S3] och tilldela behörigheter för följande åtgärder:

* `s3:DeleteObject`
* `s3:GetBucketLocation`
* `s3:GetObject`
* `s3:ListBucket`
* `s3:PutObject`
* `s3:ListMultipartUploadParts`

<!--

Commenting out this note, as write permissions are assigned through the s3:PutObject permission.

>[!IMPORTANT]
>
>Platform needs `write` permissions on the bucket object where the export files will be delivered.

-->

## Aktivera målgrupper till det här målet {#activate}

>[!IMPORTANT]
> 
>* För att aktivera data behöver du **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** och **[!UICONTROL View Segments]** [behörigheter för åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontroll - översikt](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få de behörigheter som krävs.
>* Exportera *identiteter* behöver du **[!UICONTROL View Identity Graph]** [behörighet för åtkomstkontroll](/help/access-control/home.md#permissions). <br> ![Markera det identitetsnamnutrymme som är markerat i arbetsflödet för att aktivera målgrupper till mål.](/help/destinations/assets/overview/export-identities-to-destination.png "Markera det identitetsnamnutrymme som är markerat i arbetsflödet för att aktivera målgrupper till mål."){width="100" zoomable="yes"}

Se [Aktivera målgruppsdata för att batchprofilera exportmål](../../ui/activate-batch-profile-destinations.md) för instruktioner om hur du aktiverar målgrupper till det här målet.

## Validera slutförd dataexport {#exported-data}

Kontrollera dina [!DNL Amazon S3] och se till att de exporterade filerna innehåller de förväntade profilpopulationerna.

## IP-adress tillåtelselista {#ip-address-allow-list}

Se [IP-adress tillåtelselista](ip-address-allow-list.md) artikel om du behöver lägga till IP-adresser för Adobe i en tillåtelselista.