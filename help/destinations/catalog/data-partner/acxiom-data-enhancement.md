---
title: Dataförbättring i Acxiom
description: Använd den här kopplingen för att aktivera egna Adobe-profiler i Real-Time CDP till Acxiom för att berika och använda data i alla marknadsföringskanaler. Du kan sedan använda Acxiom-källan för att importera profilerna med förbättrade data och arbeta med dem i Real-Time CDP.
last-substantial-update: 2024-03-14T00:00:00Z
badge: Beta
exl-id: 59edc43d-ae8e-4c3d-820c-b5be1c4483f9
source-git-commit: 82ff222d22255b9c99de76111d25d4a3cf6f2d5c
workflow-type: tm+mt
source-wordcount: '1439'
ht-degree: 2%

---

# Målanslutning för [!DNL Acxiom Data Enhancement]

>[!NOTE]
>
>Målet [!DNL Acxiom Data Enhancement] är i betaversion.  Den här målanslutningen och dokumentationssidan skapas och underhålls av Acxiom-teamet. Om du har frågor eller uppdateringsfrågor kan du kontakta dem direkt på acxiom-adobe-help@acxiom.com.

## Översikt {#overview}

Använd [!DNL Acxiom Data Enhancement]-anslutningen för att förse dina kundprofiler med ytterligare beskrivande data, som kan användas i program för analys, segmentering och målinriktning. Med hundratals tillgängliga element kan ni segmentera och modellera data bättre, vilket resulterar i mer korrekt målinriktning och prediktiv modellering.

![Marknadsföringsdiagram som exporterar förstahandsdata till Acxiom och sedan importerar berikade data tillbaka till Real-Time CDP](/help/destinations/assets/catalog/data-partner/acxiom/marketing-workflow-data-enhancement.png)

I den här självstudiekursen beskrivs hur du skapar en [!DNL Acxiom Data Enhancement]-målanslutning och ett dataflöde med Adobe Experience Platform-användargränssnittet. Den här kopplingen används för att leverera data till Acxiom-förbättringstjänsten med Amazon S3 som utgångspunkt.

![Målkatalogen med Acxiom-målet markerat.](../../assets/catalog/data-partner/acxiom/image-destination-enhancement-catalog.png)

## Användningsfall {#use-cases}

För att du bättre ska kunna förstå hur och när du ska använda målet [!DNL Acxiom Data Enhancement] finns det exempel på användning som Adobe Experience Platform-kunder kan lösa genom att använda det här målet.

### Förbättra kunddata {#enhance-customer-data}

Denna koppling ska användas av marknadsförare som vill förbättra effektiviteten i sina utåtriktade strategier genom att lägga till utvalda beskrivande element i sina kundprofiler och använda dessa för att bättre målinrikta kampanjer.

Som marknadsförare kanske du vill fördjupa din förståelse för era befintliga målgrupper genom att förbättra deras profiler med ytterligare data. Om du gör det kommer ni att förbättra era segmenterings- och målinriktningsstrategier, vilket leder till en ökad personalisering och konvertering av kampanjer.

Användningsexemplet körs genom en kombination av både mål- och källanslutningar.

Du börjar med att exportera dina befintliga kundposter för anrikning med den här målkopplingen. Acxioms tjänst skulle söka efter filen, hämta den, berika den med data från Acxiom och generera en fil.

Kunden använder sedan motsvarande [Acxiom-källkort](/help/sources/connectors/data-partners/acxiom-data-ingestion.md) för att importera de hydrerade kundprofilerna tillbaka till Adobe Real-Time CDP.

## Förutsättningar {#prerequisites}

>[!IMPORTANT]
>
>* Om du vill ansluta till målet behöver du behörigheterna **[!UICONTROL View Destinations]**, **[!UICONTROL Manage Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** och **[!UICONTROL View Segments]** [åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontrollsöversikten](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få den behörighet som krävs.
>* Om du vill exportera *identiteter* måste du ha **[!UICONTROL View Identity Graph]** [åtkomstkontrollbehörighet](/help/access-control/home.md#permissions). <br> ![Markera identitetsnamnområdet som är markerat i arbetsflödet för att aktivera målgrupper till mål.](/help/destinations/assets/overview/export-identities-to-destination.png "Markera identitetsnamnområdet som är markerat i arbetsflödet för att aktivera målgrupper till mål."){width="100" zoomable="yes"}

## Målgrupper {#supported-audiences}

I det här avsnittet beskrivs vilken typ av målgrupper du kan exportera till det här målet.

| Målgruppsursprung | Stöds | Beskrivning |
|---------|----------|----------|
| [!DNL Segmentation Service] | Ja | Publiker som genererats via Experience Platform [segmenteringstjänst](../../../segmentation/home.md). |
| Alla andra målgrupper kommer | Nej | Den här kategorin omfattar alla målgrupper som kommer utanför målgrupper som genereras via [!DNL Segmentation Service]. Läs om de [olika målgruppernas ursprung](/help/segmentation/ui/audience-portal.md#customize). Några exempel är: <ul><li> anpassade uppladdningsgrupper [importerade](../../../segmentation/ui/audience-portal.md#import-audience) till Experience Platform från CSV-filer,</li><li> lookalike-målgrupper, </li><li> federerade målgrupper, </li><li> målgrupper som genererats i andra Experience Platform-appar som Adobe Journey Optimizer, </li><li> med mera. </li></ul> |

{style="table-layout:auto"}




Målgrupper som stöds av olika typer av målgruppsdata:

| Typ av målgruppsdata | Stöds | Beskrivning | Användningsfall |
|--------------------|-----------|-------------|-----------|
| [Målgrupper](/help/segmentation/types/people-audiences.md) | Ja | Baserat på kundprofiler kan ni inrikta er på specifika grupper av människor för marknadsföringskampanjer. | Ofta köpare, övergivna varukorgar |
| [Kontomålgrupper](/help/segmentation/types/account-audiences.md) | Nej | Rikta er till individer inom specifika organisationer för kontobaserade marknadsföringsstrategier. | B2B-marknadsföring |
| [Prospektera målgrupper](/help/segmentation/types/prospect-audiences.md) | Nej | Rikta er till individer som ännu inte är kunder men som delar egenskaper med er målgrupp. | Prospektera med data från tredje part |
| [Datauppsättningsexport](/help/catalog/datasets/overview.md) | Nej | Samlingar med strukturerade data som lagras i Adobe Experience Platform Data Lake. | Arbetsflöden för rapportering, datavetenskap |

{style="table-layout:auto"}


## Exportera typ och frekvens {#export-type-frequency}

Se tabellen nedan för information om exporttyp och frekvens för destinationen.

| Objekt | Typ | Anteckningar |
|------------------|--------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Exporttyp | **[!UICONTROL Profile-based]** | Du exporterar alla medlemmar i ett segment tillsammans med de önskade schemafälten (t.ex. e-postadress, telefonnummer, efternamn), som du har valt på skärmen Välj profilattribut i arbetsflödet för [målaktivering](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| Exportfrekvens | **[!UICONTROL Batch]** | Batchdestinationer exporterar filer till efterföljande plattformar i steg om tre, sex, åtta, tolv eller tjugofyra timmar. Läs mer om [gruppfilsbaserade mål](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## Anslut till målet {#connect}

>[!IMPORTANT]
>
>Om du vill ansluta till målet behöver du behörigheterna **[!UICONTROL View Destinations]** och **[!UICONTROL Manage and Activate Dataset Destinations]** [åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontrollsöversikten](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få den behörighet som krävs.

Om du vill ansluta till det här målet följer du stegen som beskrivs i självstudiekursen [för destinationskonfiguration](../../ui/connect-destination.md). I arbetsflödet för målkonfiguration fyller du i fälten som listas i de två avsnitten nedan.

### Autentisera till mål {#authenticate}

Fyll i de obligatoriska fälten och välj **[!UICONTROL Connect to destination]** om du vill autentisera mot målet.

Om du vill komma åt din bucket på Experience Platform måste du ange giltiga värden för följande autentiseringsuppgifter:

| Autentiseringsuppgifter | Beskrivning |
|---------------|----------------------------------------------------------------------------------------------------------|
| S3-åtkomstnyckel | Åtkomstnyckel-ID för din bucket. Du kan hämta värdet från [!DNL Acxiom]-teamet. |
| S3-hemlig nyckel | Det hemliga nyckel-ID:t för din bucket. Du kan hämta värdet från [!DNL Acxiom]-teamet. |
| Buckennamn | Det här är din bucket där filer delas. Du kan hämta värdet från [!DNL Acxiom]-teamet. |

### Nytt konto

Så här definierar du en ny plats för hanterad Acxiom S3:

![Nytt konto](../../assets/catalog/data-partner/acxiom/image-destination-new-account.png)

### Befintligt konto

Konton som redan har definierats med målet [!DNL Acxiom Data Enhancement] visas i en lista. När du väljer det här alternativet visas information om kontot i den högra listen. Visa exemplet från gränssnittet när du navigerar till **[!UICONTROL Destinations]** > **[!UICONTROL Accounts]**;

![Befintligt konto](../../assets/catalog/data-partner/acxiom/image-destination-enhancement-account.png)

### Fyll i målinformation {#destination-details}

Om du vill konfigurera information för målet fyller du i de obligatoriska och valfria fälten nedan. En asterisk bredvid ett fält i användargränssnittet anger att fältet är obligatoriskt.

![Måldetalj](../../assets/catalog/data-partner/acxiom/image-destination-details.png)

* **Namn (obligatoriskt)** - Namnet som målet sparas under
* **Beskrivning** - En kort förklaring av målets syfte
* **Bucket Name (Required)** - Namn på Amazon S3-bucket som konfigurerats på S3
* **Mappsökväg (obligatoriskt)** - Om underkataloger i en bucket används måste en sökväg definieras, eller &#39;/&#39; för att referera till rotsökvägen.
* **Filtyp** - Välj det format som Experience Platform ska använda för de exporterade filerna. För närvarande är CSV den enda filtypen som Acxiom-bearbetning kan förväntas vara

>[!IMPORTANT]
>
>När du väljer CSV-alternativet visas alternativen *Avgränsare*, *Citattecken*, *Escape-tecken*, *Tomt värde*, *Null-värde*, *Komprimeringsformat* och *Inkludera manifestfil* i följande dokument: mer ingående [konfigurera formateringsalternativen](../../ui/batch-destinations-file-formatting-options.md).

![CSV-alternativ](../../assets/catalog/data-partner/acxiom/image-destination-csv-options.png)

### Aktivera aviseringar {#enable-alerts}

Du kan aktivera varningar för att få meddelanden om dataflödets status till ditt mål. Välj en avisering i listan om du vill prenumerera och få meddelanden om statusen för ditt dataflöde. Mer information om varningar finns i guiden [prenumerera på destinationsvarningar med användargränssnittet](../../ui/alerts.md).

Välj **[!UICONTROL Next]** när du är klar med att ange information för målanslutningen.

## Aktivera målgrupper till det här målet {#activate}

>[!IMPORTANT]
>
>* För att aktivera data behöver du behörigheterna **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** och **[!UICONTROL View Segments]** [åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontrollsöversikten](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få den behörighet som krävs.
>* Om du vill exportera *identiteter* måste du ha **[!UICONTROL View Identity Graph]** [åtkomstkontrollbehörighet](/help/access-control/home.md#permissions). <br> ![Markera identitetsnamnområdet som är markerat i arbetsflödet för att aktivera målgrupper till mål.](/help/destinations/assets/overview/export-identities-to-destination.png "Markera identitetsnamnområdet som är markerat i arbetsflödet för att aktivera målgrupper till mål."){width="100" zoomable="yes"}

Läs [Aktivera målgruppsdata för att batchprofilera exportmål](/help/destinations/ui/activate-batch-profile-destinations.md) om du vill ha instruktioner om hur du aktiverar målgrupper till det här målet.

### Mappningsförslag

För att filerna på Acxiom-sidan ska kunna bearbetas på rätt sätt krävs namn- och adresselement. Även om det inte krävs alla element, kommer det att vara till hjälp att matchningen blir så framgångsrik som möjligt om alla delar anges.

Mappningsförslag ges i tabellen nedan som listar de attribut på målsidan som används av Acxiom-bearbetning som kunder kan mappa profilattribut till. Behandla dessa element som förslag eftersom inte alla element är obligatoriska och källvärdena beror på kontots behov.

| Målfält | Source Description |
|--------------|-------------------------------------------------------------|
| name | Värdet `person.name.fullName` i Experience Platform. |
| firstName | Värdet `person.name.firstName` i Experience Platform. |
| lastName | Värdet `person.name.lastName` i Experience Platform. |
| adress1 | Värdet `mailingAddress.street1` i Experience Platform. |
| adress2 | Värdet `mailingAddress.street2` i Experience Platform. |
| stad | Värdet `mailingAddress.city` i Experience Platform. |
| läge | Värdet `mailingAddress.state` i Experience Platform. |
| zip | Värdet `mailingAddress.postalCode` i Experience Platform. |

>[!NOTE]
>
>Om du mappar ytterligare fält som inte finns med ovan i dataflödet inkluderas de i dataexporten, men ignoreras av Acxiom-bearbetningen.

## Validera dataexport {#exported-data}

Kontrollera [!DNL Amazon S3 Storage]-pytsen och se till att de exporterade filerna innehåller de förväntade profilpopulationerna för att kontrollera om data har exporterats utan fel.

## Nästa steg

Genom att följa den här självstudiekursen har du skapat ett dataflöde för att exportera profildata från Experience Platform till din [!DNL Acxiom] hanterade S3-plats. Därefter kontaktar du din Acxiom-representant med namnet på kontot, filnamnen och bucket-sökvägen så att bearbetningen kan konfigureras.

## Dataanvändning och styrning {#data-usage-governance}

Alla [!DNL Adobe Experience Platform]-mål är kompatibla med dataanvändningsprinciper när data hanteras. Mer information om hur [!DNL Adobe Experience Platform] använder datastyrning finns i [Översikt över datastyrning](/help/data-governance/home.md).

## Ytterligare resurser {#additional-resources}

*Acxiom Infobase:* https://www.acxiom.com/wp-content/uploads/2022/02/fs-acxiom-infobase_AC-0268-22.pdf
