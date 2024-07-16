---
title: Proportioner för Acxiom - undertryckning
description: Exportera era egna målgrupper till Acxiom-destinationen så att Acxiom kan inaktivera kända eller konverterade kunder. Använd sedan källkopplingen för Acxiom för att importera och aktivera listor med potentiella kunder från Acxiom, med kända eller konverterade kunder borttagna.
last-substantial-update: 2024-03-14T00:00:00Z
badge: Beta
exl-id: d82e8cd3-970c-44af-99b0-ea154eb3655e
source-git-commit: c35b43654d31f0f112258e577a1bb95e72f0a971
workflow-type: tm+mt
source-wordcount: '1430'
ht-degree: 0%

---

# Målanslutning för [!DNL Acxiom Prospect-Suppression]

>[!NOTE]
>
>Målet [!DNL Acxiom Prospect-Suppression] är i betaversion. Den här målanslutningen och dokumentationssidan skapas och underhålls av Acxiom-teamet. Om du har frågor eller uppdateringsfrågor kan du kontakta dem direkt på acxiom-adobe-help@acxiom.com.

## Översikt {#overview}

Använd [!DNL Acxiom Prospect-Suppression] för att leverera de mest produktiva målgrupperna för potentiella kunder. Denna koppling exporterar data från Real-time Customer Data Platform och kör dem på ett säkert sätt via en prisbelönt hygien- och identitetsupplösning som producerar en datafil som ska användas som en undertryckningslista. Detta matchas mot databasen [!DNL Acxiom Global] som gör att listor med potentiella kunder kan anpassas för import. Använd sedan [[!DNL Acxiom Prospecting Data Import]](/help/sources/connectors/data-partners/acxiom-prospecting-data-import.md)-källkopplingen för att skapa listor med potentiella kunder från Acxiom tillbaka till Real-Time CDP, där dina kända eller konverterade kunder tas bort.

![Marknadsföringsdiagram för export av förstahandsdata till Acxiom och sedan import av data för potentiella kunder tillbaka till Real-Time CDP](/help/destinations/assets/catalog/data-partner/acxiom/marketing-workflow.png)

Acxiom erbjuder branschens mest framgångsrika målgrupper med över 12 000 globala dataattribut som är särskilt inriktade på att leverera personaliserade upplevelser. Utnyttja obegränsade kombinationer av högkvalitativa data för att skapa och distribuera målgrupper för specifika kampanjbehov.

I den här självstudiekursen beskrivs hur du skapar en [!DNL Acxiom Prospect-Suppression]-målanslutning och ett dataflöde med Adobe Experience Platform-användargränssnittet. Den här kopplingen används för att leverera data till tjänsten för potentiella kunder i Acxiom med Amazon S3 som utgångspunkt. Kontakta din kontorepresentant för Acxiom när du har börjat exportera filer till Amazon S3-släpppunkten.

![Målkatalogen med Acxiom-målet markerat.](../../assets/catalog/data-partner/acxiom/image-destination-catalog.png)

## Användningsfall {#use-cases}

För att du bättre ska kunna förstå hur och när du ska använda målet [!DNL Acxiom Prospect-Suppression] finns det exempel på användning som Adobe Experience Platform-kunder kan lösa genom att använda det här målet.

### Skapa en undertryckningslista för datauppsättningar för prospektering {#create-suppression-list}

Marknadsförare som vill effektivisera sina utåtriktade strategier använder ofta att skapa en undertryckningslista. Denna förteckning omfattar befintliga kunder och specifika segment, vilket säkerställer att de inte omfattas av prospekteringsverksamhet under riktade kampanjer. Denna strategiska strategi hjälper till att förfina målgruppen, undviker överflödig kommunikation och bidrar till en mer fokuserad och effektiv marknadsföring.

Som marknadsförare kanske ni vill bredda er kampanjräckvidd genom att lägga till riktade profiler för potentiella kunder till era kampanjer baserat på de segmenterings- och undertryckningskriterier som ni har angett.

Användningsexemplet körs genom en kombination av både mål- och källanslutningar.

Du börjar först med att exportera dina befintliga kundprofiler med den här målkopplingen som ska användas som en undertryckningsfil. Detta säkerställer att inga befintliga kundposter inkluderas.

Acxioms tjänst skulle söka efter filen, hämta den och använda den tillsammans med andra urvalskriterier och generera en potentiell fil. Du använder sedan motsvarande [[!DNL Acxiom Prospecting Data Import]](/help/sources/connectors/data-partners/acxiom-prospecting-data-import.md)-källanslutning för att importera profiler för potentiella kunder till Adobe Real-Time CDP.

## Förhandskrav {#prerequisites}

>[!IMPORTANT]
>
>* Om du vill ansluta till målet behöver du behörigheterna **[!UICONTROL View Destinations]**, **[!UICONTROL Manage Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** och **[!UICONTROL View Segments]** [åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontrollsöversikten](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få den behörighet som krävs.
>* Om du vill exportera *identiteter* måste du ha **[!UICONTROL View Identity Graph]** [åtkomstkontrollbehörighet](/help/access-control/home.md#permissions). <br> ![Markera identitetsnamnområdet som är markerat i arbetsflödet för att aktivera målgrupper till mål.](/help/destinations/assets/overview/export-identities-to-destination.png "Markera identitetsnamnområdet som är markerat i arbetsflödet för att aktivera målgrupper till mål."){width="100" zoomable="yes"}

## Målgrupper {#supported-audiences}

I det här avsnittet beskrivs vilken typ av målgrupper du kan exportera till det här målet.

| Målgruppsursprung | Stöds | Beskrivning |
|-----------------------------|-----------|---------------------------------------------------------------------------------------------------------------------|
| [!DNL Segmentation Service] | ✓ | Publiker som genererats via Experience Platform [segmenteringstjänsten](../../../segmentation/home.md). |
| Anpassade överföringar | x | Publikerna [importerade](../../../segmentation/ui/audience-portal.md#import-audience) till Experience Platform från CSV-filer. |

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
>Om du vill ansluta till målet behöver du behörigheterna **[!UICONTROL View Destinations]** och **[!UICONTROL Manage Destinations]** [åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontrollsöversikten](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få den behörighet som krävs.

Om du vill ansluta till det här målet följer du stegen som beskrivs i självstudiekursen [för destinationskonfiguration](../../ui/connect-destination.md). I arbetsflödet för målkonfiguration fyller du i fälten som listas i de två avsnitten nedan.

### Autentisera till mål {#authenticate}

Fyll i de obligatoriska fälten och välj **[!UICONTROL Connect to destination]** om du vill autentisera mot målet.

För att få åtkomst till din bucket på Experience Platform måste du ange giltiga värden för följande autentiseringsuppgifter:

| Autentiseringsuppgifter | Beskrivning |
|---------------|----------------------------------------------------------------------------------------------------------|
| S3-åtkomstnyckel | Åtkomstnyckel-ID för din bucket. Du kan hämta värdet från [!DNL Acxiom]-teamet. |
| S3-hemlig nyckel | Det hemliga nyckel-ID:t för din bucket. Du kan hämta värdet från [!DNL Acxiom]-teamet. |
| Buckennamn | Det här är din bucket där filer delas. Du kan hämta värdet från [!DNL Acxiom]-teamet. |

### Nytt konto

Så här definierar du en ny plats för hanterad Acxiom S3:

![Nytt konto](../../assets/catalog/data-partner/acxiom/image-destination-new-account.png)

### Befintligt konto

Konton som redan har definierats med målet [!DNL Acxiom Prospect Suppression] visas i en lista. När du väljer det här alternativet visas information om kontot i den högra listen. Visa exemplet från gränssnittet när du navigerar till **[!UICONTROL Destinations]** > **[!UICONTROL Accounts]**:

![Befintligt konto](../../assets/catalog/data-partner/acxiom/image-destination-account.png)

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

Bearbetning kräver namn- och adresselement, men alla element krävs inte, förutsatt att så mycket som möjligt hjälper till med matchningen.  Mappningsförslag ges i tabellen nedan som listar de attribut på målsidan som används av Acxiom-bearbetning som kunder kan mappa profilattribut till.  Detta bör behandlas som förslag eftersom inte alla element är obligatoriska och källvärdena beror på kontots behov.

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

{style="table-layout:auto"}

>[!NOTE]
>
>Ytterligare fält som inte anges ovan inkluderas i exporten, men ignoreras av Acxiom-bearbetningen.

## Granska ditt dataflöde

Använd granskningssidan för att få en sammanfattning av dataflödet innan du skickar in det

![Granska](../../assets/catalog/data-partner/acxiom/image-destination-review.png)

## Validera dataexport {#exported-data}

Kontrollera [!DNL Amazon S3 Storage]-pytsen och se till att de exporterade filerna innehåller de förväntade profilpopulationerna för att kontrollera om data har exporterats utan fel.

## Nästa steg

Genom att följa den här självstudiekursen har du skapat ett dataflöde för att exportera batchdata från Experience Platform till din [!DNL Acxiom] hanterade S3-plats. Du måste kontakta din Acxiom-representant med namnet på kontot, filnamnet och bucket-sökvägen så att bearbetningen kan konfigureras.

## Dataanvändning och styrning {#data-usage-governance}

Alla [!DNL Adobe Experience Platform]-mål är kompatibla med dataanvändningsprinciper när data hanteras. Mer information om hur [!DNL Adobe Experience Platform] använder datastyrning finns i [Översikt över datastyrning](/help/data-governance/home.md).

## Ytterligare resurser {#additional-resources}

*Acxiom Audience Data and Distribution:* https://www.acxiom.com/customer-data/audience-data-distribution/
