---
title: Amazon S3-anslutning
description: Skapa en utgående liveanslutning till din Amazon Web Services (AWS) S3-lagringsplats för att regelbundet exportera CSV-datafiler från Adobe Experience Platform till dina egna S3-butiker.
exl-id: 6a2a2756-4bbf-4f82-88e4-62d211cbbb38
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1461'
ht-degree: 0%

---

# [!DNL Amazon S3]-anslutning {#s3-connection}

## Destinationsändringslogg {#changelog}

+++ Visa ändringslogg


| Releasamånad | Uppdateringstyp | Beskrivning |
|---|---|---|
| Januari 2024 | Funktioner och dokumentation | Amazon S3-målkopplingen har nu stöd för en ny, antagen rollautentiseringstyp. Läs mer om det i avsnittet [autentisering](#assumed-role-authentication). |
| Juli 2023 | Funktioner och dokumentation | Med Experience Platform från juli 2023 har målet [!DNL Amazon S3] nya funktioner enligt nedan: <br><ul><li>[Exportstöd för datauppsättningar](/help/destinations/ui/export-datasets.md)</li><li>Ytterligare [namngivningsalternativ](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling).</li><li>Möjlighet att ange anpassade filhuvuden i de exporterade filerna via det [förbättrade mappningssteget](/help/destinations/ui/activate-batch-profile-destinations.md#mapping).</li><li>[Möjlighet att anpassa formateringen för exporterade CSV-datafiler](/help/destinations/ui/batch-destinations-file-formatting-options.md).</li></ul> |

{style="table-layout:auto"}

+++

## Anslut till ditt [!DNL Amazon S3]-lagringsutrymme via API eller användargränssnittet {#connect-api-or-ui}

* Om du vill ansluta till lagringsplatsen [!DNL Amazon S3] med Experience Platform användargränssnitt läser du avsnitten [Anslut till målet](#connect) och [Aktivera målgrupper till det här målet](#activate) nedan.
* Om du vill ansluta till din [!DNL Amazon S3]-lagringsplats programmatiskt läser du guiden om hur du [aktiverar målgrupper till filbaserade mål med hjälp av API-självstudiekursen för Flow-tjänsten](../../api/activate-segments-file-based-destinations.md).

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

![Profilbaserad exporttyp för Amazon S3 är markerad i USA.](../../assets/catalog/cloud-storage/amazon-s3/catalog.png)

## Exportera datauppsättningar {#export-datasets}

Detta mål stöder datauppsättningsexporter. Fullständig information om hur du ställer in datauppsättningsexporter finns i självstudiekurserna:

* Så här [exporterar du datauppsättningar med Experience Platform användargränssnitt](/help/destinations/ui/export-datasets.md).
* Så här [exporterar du datauppsättningar programmatiskt med API:t för Flow Service ](/help/destinations/api/export-datasets.md).

## Filformat för exporterade data {#file-format}

När du exporterar *målgruppsdata* skapar Experience Platform en `.csv` -, `parquet` - eller `.json` -fil på den angivna lagringsplatsen. Mer information om filerna finns i avsnittet [Filformat som stöds för export](../../ui/activate-batch-profile-destinations.md#supported-file-formats-export) i självstudiekursen om målgruppsaktivering.

När du exporterar *datauppsättningar* skapar Experience Platform en `.parquet`- eller `.json`-fil på den lagringsplats som du angav. Mer information om filerna finns i avsnittet [Verifiera lyckad datauppsättningsexport](../../ui/export-datasets.md#verify) i självstudiekursen om exportdatamängder.

## Anslut till målet {#connect}

>[!IMPORTANT]
> 
>Om du vill ansluta till målet behöver du behörigheterna **[!UICONTROL View Destinations]** och **[!UICONTROL Manage Destinations]** [åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontrollsöversikten](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få den behörighet som krävs.

Om du vill ansluta till det här målet följer du stegen som beskrivs i självstudiekursen [för destinationskonfiguration](../../ui/connect-destination.md). I arbetsflödet för målkonfiguration fyller du i fälten som listas i de två avsnitten nedan.

### Autentisera till mål {#authenticate}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_s3_rsa"
>title="RSA offentlig nyckel"
>abstract="Du kan också bifoga den RSA-formaterade offentliga nyckeln för att lägga till kryptering till de exporterade filerna. Visa ett exempel på en korrekt formaterad nyckel i dokumentationslänken nedan."

Fyll i de obligatoriska fälten och välj **[!UICONTROL Connect to destination]** om du vill autentisera mot målet. Amazon S3-målet har stöd för två autentiseringsmetoder:

* Åtkomstnyckel och autentisering av hemlig nyckel
* Antagen rollautentisering

#### Åtkomstnyckel och autentisering av hemlig nyckel

Använd den här autentiseringsmetoden när du vill ange din Amazon S3-åtkomstnyckel och hemlig nyckel så att Experience Platform kan exportera data till dina Amazon S3-egenskaper.

![Bild av obligatoriska fält när åtkomstnyckel och autentisering av hemliga nycklar väljs.](/help/destinations/assets/catalog/cloud-storage/amazon-s3/access-key-secret-key-authentication.png)

* **[!DNL Amazon S3]åtkomstnyckel** och **[!DNL Amazon S3]hemlig nyckel**: Generera ett `access key - secret access key`-par i [!DNL Amazon S3] för att ge Experience Platform åtkomst till ditt [!DNL Amazon S3]-konto. Läs mer i [Amazon Web Services-dokumentationen](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html).
* **[!UICONTROL Encryption key]**: Om du vill kan du bifoga den RSA-formaterade offentliga nyckeln för att lägga till kryptering i de exporterade filerna. Visa ett exempel på en korrekt formaterad krypteringsnyckel i bilden nedan.

  ![Bild som visar ett exempel på en korrekt formaterad PGP-nyckel i gränssnittet.](../../assets/catalog/cloud-storage/sftp/pgp-key.png)

#### Antagen roll {#assumed-role-authentication}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_s3_assumed_role"
>title="Antagen rollautentisering"
>abstract="Använd den här autentiseringstypen om du inte vill dela kontonycklar och hemliga nycklar med Adobe. I stället ansluter Experience Platform till din Amazon S3-plats med rollbaserad åtkomst. Klistra in ARN för rollen som du skapade i AWS för Adobe-användaren. Mönstret liknar `arn:aws:iam::800873819705:role/destinations-role-customer` "

![Bild av de obligatoriska fälten när du väljer autentisering av antagen roll.](/help/destinations/assets/catalog/cloud-storage/amazon-s3/assumed-role-authentication.png)

Använd den här autentiseringstypen om du inte vill dela kontonycklar och hemliga nycklar med Adobe. I stället ansluter Experience Platform till din Amazon S3-plats med rollbaserad åtkomst.

För att kunna göra detta måste du skapa en användare för Adobe i AWS-konsolen med de [behörigheter som krävs](#minimum-permissions-iam-user) för att skriva till dina Amazon S3-bucket. Skapa en **[!UICONTROL Trusted entity]** i AWS med Adobe-kontot **[!UICONTROL 670664943635]**. Mer information finns i [AWS-dokumentationen om hur du skapar roller](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_create_for-user.html).

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
>abstract="Får endast innehålla tecknen A-Z, a-z, 0-9 och kan innehålla följande specialtecken: `/!-_.'()"^[]+$%.*"`. Om du vill skapa en mapp per målgruppsfil infogar du makrot `/%SEGMENT_NAME%`, `/%SEGMENT_ID%` eller `/%SEGMENT_NAME%/%SEGMENT_ID%` i textfältet. Makron kan bara infogas i slutet av mappsökvägen. Visa makroexempel i dokumentationen."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/cloud-storage/overview.html?lang=sv-SE#use-macros" text="Använd makron för att skapa en mapp på lagringsplatsen"

Om du vill konfigurera information för målet fyller du i de obligatoriska och valfria fälten nedan. En asterisk bredvid ett fält i användargränssnittet anger att fältet är obligatoriskt.

* **[!UICONTROL Name]**: Ange ett namn som hjälper dig att identifiera det här målet.
* **[!UICONTROL Description]**: Ange en beskrivning av det här målet.
* **[!UICONTROL Bucket name]**: Ange namnet på den [!DNL Amazon S3]-bucket som ska användas för det här målet.
* **[!UICONTROL Folder path]**: Ange sökvägen till målmappen som ska vara värd för de exporterade filerna.
* **[!UICONTROL File type]**: Välj det format som Experience Platform ska använda för de exporterade filerna. När du väljer alternativet [!UICONTROL CSV] kan du även [konfigurera filformateringsalternativen](../../ui/batch-destinations-file-formatting-options.md).
* **[!UICONTROL Compression format]**: Välj den komprimeringstyp som Experience Platform ska använda för de exporterade filerna.
* **[!UICONTROL Include manifest file]**: Aktivera det här alternativet om du vill att exporten ska innehålla en manifestfil för JSON som innehåller information om exportplats, exportstorlek och mycket annat. Manifestet har fått ett namn i formatet `manifest-<<destinationId>>-<<dataflowRunId>>.json`. Visa en [exempelmanifestfil](/help/destinations/assets/common/manifest-d0420d72-756c-4159-9e7f-7d3e2f8b501e-0ac8f3c0-29bd-40aa-82c1-f1b7e0657b19.json). Manifestfilen innehåller följande fält:
   * `flowRunId`: [Dataflödet kör](/help/dataflows/ui/monitor-destinations.md#dataflow-runs-for-batch-destinations) som genererade den exporterade filen.
   * `scheduledTime`: Tiden i UTC när filen exporterades.
   * `exportResults.sinkPath`: Sökvägen till lagringsplatsen där den exporterade filen placeras.
   * `exportResults.name`: Namnet på den exporterade filen.
   * `size`: Den exporterade filens storlek i byte.

>[!TIP]
>
>I arbetsflödet för anslutningsmål kan du skapa en anpassad mapp i din Amazon S3-lagring per exporterad målgruppsfil. Läs [Använd makron för att skapa en mapp på din lagringsplats](overview.md#use-macros) för instruktioner.

### Aktivera aviseringar {#enable-alerts}

Du kan aktivera varningar för att få meddelanden om dataflödets status till ditt mål. Välj en avisering i listan om du vill prenumerera och få meddelanden om statusen för ditt dataflöde. Mer information om varningar finns i guiden [prenumerera på destinationsvarningar med användargränssnittet](../../ui/alerts.md).

Välj **[!UICONTROL Next]** när du är klar med att ange information för målanslutningen.

### [!DNL Amazon S3] behörigheter som krävs {#required-s3-permission}

Om du vill ansluta och exportera data till din [!DNL Amazon S3]-lagringsplats skapar du en IAM-användare (Identity and Access Management) för [!DNL Experience Platform] i [!DNL Amazon S3] och tilldelar behörigheter för följande åtgärder:

* `s3:DeleteObject`
* `s3:GetBucketLocation`
* `s3:GetObject`
* `s3:ListBucket`
* `s3:PutObject`
* `s3:ListMultipartUploadParts`

#### Minsta nödvändiga behörigheter för IAM-implementerad rollautentisering {#minimum-permissions-iam-user}

När du konfigurerar IAM-rollen som kund ska du kontrollera att behörighetsprincipen som är associerad med rollen innehåller de nödvändiga åtgärderna för målmappen i bucket och åtgärden `s3:ListBucket` för bucket-roten. Visa ett exempel på lägsta behörighetsprincip för den här autentiseringstypen nedan:

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "VisualEditor0",
            "Effect": "Allow",
            "Action": [
                "s3:PutObject",
                "s3:GetObject",
                "s3:DeleteObject",
                "s3:GetBucketLocation",
                "s3:ListMultipartUploadParts"
            ],
            "Resource": "arn:aws:s3:::bucket/folder/*"
        },
        {
            "Sid": "VisualEditor1",
            "Effect": "Allow",
            "Action": [
                "s3:ListBucket"
            ],
            "Resource": "arn:aws:s3:::bucket"
        }
    ]
}  
```

<!--

Commenting out this note, as write permissions are assigned through the s3:PutObject permission.

>[!IMPORTANT]
>
>Experience Platform needs `write` permissions on the bucket object where the export files will be delivered.

-->

## Aktivera målgrupper till det här målet {#activate}

>[!IMPORTANT]
> 
>* För att aktivera data behöver du behörigheterna **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** och **[!UICONTROL View Segments]** [åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontrollsöversikten](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få den behörighet som krävs.
>* Om du vill exportera *identiteter* måste du ha **[!UICONTROL View Identity Graph]** [åtkomstkontrollbehörighet](/help/access-control/home.md#permissions). <br> ![Markera identitetsnamnområdet som är markerat i arbetsflödet för att aktivera målgrupper till mål.](/help/destinations/assets/overview/export-identities-to-destination.png "Markera identitetsnamnområdet som är markerat i arbetsflödet för att aktivera målgrupper till mål."){width="100" zoomable="yes"}

Se [Aktivera målgruppsdata för att batchprofilera exportmål](../../ui/activate-batch-profile-destinations.md) för instruktioner om hur du aktiverar målgrupper till det här målet.

## Validera slutförd dataexport {#exported-data}

Kontrollera [!DNL Amazon S3]-lagringen och se till att de exporterade filerna innehåller de förväntade profilpopulationerna för att kontrollera om data har exporterats.

## IP-adress tillåtelselista {#ip-address-allow-list}

Läs artikeln [IP-adressen tillåtelselista](ip-address-allow-list.md) om du behöver lägga till Adobe IP-adresser i en tillåtelselista.