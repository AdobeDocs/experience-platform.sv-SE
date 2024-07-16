---
title: Pega Profile Connector
description: Använd Pega Profile Connector för Amazon S3 i Adobe Experience Platform för att exportera fullständiga eller inkrementella, eller båda, profildata till Amazon S3-molnlagring. I Pega Customer Decision Hub kan datafält schemaläggas i kundprofil-Designer för att importera profildata regelbundet från Amazon S3-lagring.
last-substantial-update: 2023-01-25T00:00:00Z
exl-id: f422f21b-174a-4b93-b05d-084b42623314
source-git-commit: ba39f62cd77acedb7bfc0081dbb5f59906c9b287
workflow-type: tm+mt
source-wordcount: '1084'
ht-degree: 0%

---

# Pega Profile Connector

## Översikt {#overview}

Använd [!DNL Pega Profile Connector] i Adobe Experience Platform för att skapa en utgående liveanslutning till din [!DNL Amazon Web Services] (AWS) S3-lagring för att regelbundet exportera profildata till CSV-filer från Adobe Experience Platform till dina egna S3-bucket. I [!DNL Pega Customer Decision Hub] kan du schemalägga datajobb för import av profildata från S3-lagring för att uppdatera profilen [!DNL Pega Customer Decision Hub].

Den här kopplingen hjälper till att ställa in den inledande exporten av profildata och hjälper även till att synkronisera nya profiler regelbundet till [!DNL Pega Customer Decision Hub].  Med uppdaterade data i Kundbeslutshubben får du en bättre och uppdaterad bild av kundbasen för nästa beslut om bästa möjliga åtgärd.

>[!IMPORTANT]
>
>Målanslutningen och dokumentationssidan skapas och underhålls av Pegasystems. Om du har frågor eller uppdateringsfrågor kontaktar du Pega direkt [här](mailto:support@pega.com).

## Användningsfall

För att du bättre ska kunna förstå hur och när du ska använda målet [!DNL Pega Profile Connector] finns det exempel på användning som Adobe Experience Platform-kunder kan lösa genom att använda det här målet.

### Användningsfall 1

En marknadsförare vill initialt konfigurera [!DNL Pega Customer Decision Hub] med profildata inlästa från Adobe Experience Platform. Detta är en inledande full belastning följt av deltasterna på schemalagd basis.

### Användningsfall 2

En marknadsförare vill ha aktuella profildata från Adobe Experience Platform i [!DNL Pega Customer Decision Hub] som förbättrar Pega-insikterna om kundprofiler kontinuerligt.

## Förhandskrav {#prerequisites}

Innan du kan använda det här målet för att exportera data från Adobe Experience Platform och importera profiler till [!DNL Pega Customer Decision Hub] måste du uppfylla följande krav:

* Konfigurera [!DNL Amazon S3]-bucket och mappsökvägen som ska användas för export och import av datafiler.
* Konfigurera åtkomstnyckeln [!DNL Amazon S3] och den hemliga nyckeln [!DNL Amazon S3]: Generera ett `access key - secret access key`-par i [!DNL Amazon S3] för att ge plattformsåtkomst till ditt [!DNL Amazon S3]-konto.
* Om du vill ansluta och exportera data till din [!DNL Amazon S3]-lagringsplats skapar du en IAM-användare (Identity and Access Management) för [!DNL Platform] i [!DNL Amazon S3] och tilldelar behörigheter som `s3:DeleteObject`, `s3:GetBucketLocation`, `s3:GetObject`, `s3:ListBucket`, `s3:PutObject`, `s3:ListMultipartUploadParts`
* Kontrollera att din [!DNL Pega Customer Decision Hub]-instans har uppgraderats till version 8.8 eller senare.

## Identiteter som stöds {#supported-identities}

[!DNL Pega Customer Decision Hub] stöder aktivering av anpassade användar-ID:n som beskrivs i tabellen nedan. Mer information finns i [identiteter](/help/identity-service/features/namespaces.md).

| Målidentitet | Beskrivning |
|---|---|
| *Kund-ID* | En vanlig användaridentifierare som unikt identifierar en profil i [!DNL Pega Customer Decision Hub] och Adobe Experience Platform |

{style="table-layout:auto"}

## Exportera typ och frekvens {#export-type-frequency}

Se tabellen nedan för information om exporttyp och frekvens för destinationen.

| Objekt | Typ | Anteckningar |
|---------|----------|---------|
| Exporttyp | **[!UICONTROL Profile-based]** | Du exporterar alla medlemmar i ett segment tillsammans med de önskade schemafälten (t.ex. e-postadress, telefonnummer, efternamn), som du har valt på skärmen Välj profilattribut i arbetsflödet för [målaktivering](../../ui/activate-batch-profile-destinations.md#select-attributes). |
| Exportfrekvens | **[!UICONTROL Batch]** | Batchdestinationer exporterar filer till efterföljande plattformar i steg om tre, sex, åtta, tolv eller tjugofyra timmar. Läs mer om [gruppfilsbaserade mål](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## Anslut till målet {#connect}

>[!IMPORTANT]
> 
>Om du vill ansluta till målet behöver du behörigheterna **[!UICONTROL View Destinations]** och **[!UICONTROL Manage Destinations]** [åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontrollsöversikten](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få den behörighet som krävs.

Om du vill ansluta till det här målet följer du stegen som beskrivs i självstudiekursen [för destinationskonfiguration](../../ui/connect-destination.md). I arbetsflödet för målkonfiguration fyller du i fälten som listas i de två avsnitten nedan.

### Autentisera till mål {#authenticate}

Fyll i de obligatoriska fälten och välj **[!UICONTROL Connect to destination]** om du vill autentisera mot målet.

* **[!DNL Amazon S3]åtkomstnyckel** och **[!DNL Amazon S3]hemlig nyckel**: Generera ett `access key - secret access key`-par i [!DNL Amazon S3] för att ge Adobe Experience Platform åtkomst till ditt [!DNL Amazon S3]-konto. Läs mer i [Amazon Web Services-dokumentationen](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html).

### Fyll i målinformation {#destination-details}

När du har upprättat autentiseringsanslutningen till [!DNL Amazon S3] anger du följande information för målet:

![Bild av gränssnittsskärmen som visar slutförda fält för målinformationen för Pega Profile Connector ](../../assets/catalog/personalization/pega-profile/pega-profile-connect-destination.png)

Om du vill konfigurera information för målet fyller du i de obligatoriska fälten och väljer **[!UICONTROL Next]**. En asterisk bredvid ett fält i användargränssnittet anger att fältet är obligatoriskt.

* **[!UICONTROL Name]**: Ange ett namn som hjälper dig att identifiera det här målet.
* **[!UICONTROL Description]**: Ange en beskrivning av det här målet.
* **[!UICONTROL Bucket name]**: Ange namnet på den [!DNL Amazon S3]-bucket som ska användas för det här målet.
* **[!UICONTROL Folder path]**: Ange sökvägen till målmappen som ska vara värd för de exporterade filerna.
* **[!UICONTROL Compression Type]**: Välj komprimeringstyp som GZIP eller NONE.

>[!TIP]
>
>I arbetsflödet för anslutningsmål kan du skapa en anpassad mapp i din Amazon S3-lagring per exporterad målgruppsfil. Läs [Använd makron för att skapa en mapp på din lagringsplats](/help/destinations/catalog/cloud-storage/overview.md#use-macros) för instruktioner.

### Aktivera aviseringar {#enable-alerts}

Du kan aktivera varningar för att få meddelanden om dataflödets status till ditt mål. Välj en avisering i listan om du vill prenumerera och få meddelanden om statusen för ditt dataflöde. Mer information om varningar finns i guiden [prenumerera på destinationsvarningar med användargränssnittet](../../ui/alerts.md).

Välj **[!UICONTROL Next]** när du är klar med att ange information för målanslutningen.

## Aktivera målgrupper till det här målet {#activate}

>[!IMPORTANT]
> 
>* För att aktivera data behöver du behörigheterna **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** och **[!UICONTROL View Segments]** [åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontrollsöversikten](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få den behörighet som krävs.
>* Om du vill exportera *identiteter* måste du ha **[!UICONTROL View Identity Graph]** [åtkomstkontrollbehörighet](/help/access-control/home.md#permissions). <br> ![Markera identitetsnamnområdet som är markerat i arbetsflödet för att aktivera målgrupper till mål.](/help/destinations/assets/overview/export-identities-to-destination.png "Markera identitetsnamnområdet som är markerat i arbetsflödet för att aktivera målgrupper till mål."){width="100" zoomable="yes"}

Se [Aktivera målgruppsdata för att batchprofilera exportmål](../../ui/activate-batch-profile-destinations.md) för instruktioner om hur du aktiverar målgrupper till det här målet.

### Mappa attribut och identiteter {#map}

I steget **[!UICONTROL Mapping]** kan du välja vilka attribut- och identitetsfält som ska exporteras för dina profiler. Du kan också välja att ändra rubrikerna i den exporterade filen till ett valfritt användarvänligt namn. Mer information finns i [mappningssteget](/help/destinations/ui/activate-batch-profile-destinations.md#mapping) i självstudiekursen om aktivering av gruppmål.

## Validera dataexport {#exported-data}

För [!DNL Pega Profile Connector] mål skapar [!DNL Platform] en `.csv`-fil på den Amazon S3-lagringsplats som du har angett. Mer information om filerna finns i [Aktivera målgruppsdata till exportmål för gruppprofiler](../../ui/activate-batch-profile-destinations.md) i självstudiekursen om målgruppsaktivering.

En import av profildata från S3 infogar data i [!DNL Pega Customer]-profildatalagret. Importerade kundprofildata kan valideras i [!DNL Pega Customer Profile Designer], vilket visas i följande bild.
![Bild av gränssnittsskärmen där du kan validera Adobe profildata i Designer för kundprofil](../../assets/catalog/personalization/pega-profile/pega-profile-data.png)

I [!DNL Pega Customer Decision Hub] kan dataadministratörer konfigurera datajobb i [!DNL Customer Profile Designer] så att profildata importeras periodiskt från S3 enligt följande bild. Mer information om hur du konfigurerar datajobb att importera profildata från [!DNL Amazon S3] finns i [ytterligare resurser](#additional-resources).
![Bild av gränssnittsskärmen för att konfigurera datajobb i kundprofilen Designer](../../assets/catalog/personalization/pega-profile/pega-profile-screen-image1.png)

## Ytterligare resurser {#additional-resources}

Se [Importera datajobb](https://academy.pega.com/topic/import-data-jobs/v1) i [!DNL Pega Customer Decision Hub].

## Dataanvändning och styrning {#data-usage-governance}

Alla [!DNL Adobe Experience Platform]-mål är kompatibla med dataanvändningsprinciper när data hanteras. Mer information om hur [!DNL Adobe Experience Platform] använder datastyrning finns i [Datastyrningsöversikten](/help/data-governance/home.md).
