---
keywords: aktivera profildestinationer;aktivera destinationer;aktivera data; aktivera e-postmarknadsföringsmål, aktivera molnlagringsmål
title: Aktivera målgruppsdata för att batchprofilera exportmål
type: Tutorial
description: Lär dig hur du aktiverar målgruppsdata som du har i Adobe Experience Platform genom att skicka segment till gruppprofilbaserade mål.
exl-id: 82ca9971-2685-453a-9e45-2001f0337cda
source-git-commit: 70670f7aec2ab6a5594f5e69672236c7bcc3ce81
workflow-type: tm+mt
source-wordcount: '2440'
ht-degree: 0%

---

# Aktivera målgruppsdata för att batchprofilera exportmål

>[!IMPORTANT]
> 
>Om du vill aktivera data måste du ha **[!UICONTROL Manage Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** och **[!UICONTROL View Segments]** [behörigheter för åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontroll - översikt](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få de behörigheter som krävs.

## Översikt {#overview}

I den här artikeln förklaras det arbetsflöde som krävs för att aktivera målgruppsdata i Adobe Experience Platform batchprofilbaserade mål, som molnlagring och e-postmarknadsföringsmål.

## Förutsättningar {#prerequisites}

Du måste ha aktiverat data till destinationer [ansluten till ett mål](./connect-destination.md). Om du inte redan har gjort det går du till [målkatalog](../catalog/overview.md), bläddra bland de mål som stöds och konfigurera det mål som du vill använda.

## Välj mål {#select-destination}

1. Gå till **[!UICONTROL Connections > Destinations]** och väljer **[!UICONTROL Catalog]** -fliken.

   ![Färgmarkering för hur du kommer till fliken Målkatalog](../assets/ui/activate-batch-profile-destinations/catalog-tab.png)

1. Välj **[!UICONTROL Activate segments]** på kortet som motsvarar destinationen där du vill aktivera dina segment, vilket visas i bilden nedan.

   ![Markera bilden med knappen Aktivera segment](../assets/ui/activate-batch-profile-destinations/activate-segments-button.png)

1. Markera målanslutningen som du vill använda för att aktivera dina segment och välj sedan **[!UICONTROL Next]**.

   ![Bild som visar hur du väljer ett eller flera mål att aktivera segment till](../assets/ui/activate-batch-profile-destinations/select-destination.png)

1. Gå till nästa avsnitt till [markera segment](#select-segments).

## Välj segment {#select-segments}

Använd kryssrutorna till vänster om segmentnamnen för att markera de segment som du vill aktivera för målet och markera sedan **[!UICONTROL Next]**.

![Bildmarkering som visar hur du markerar ett eller flera segment som ska aktiveras](../assets/ui/activate-batch-profile-destinations/select-segments.png)


## Schemalägg segmentexport {#scheduling}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_schedule"
>title="Schema"
>abstract="Använd pennikonen för att ange filexportformat (fullständiga eller stegvisa filer) och exportfrekvens."

[!DNL Adobe Experience Platform] exporterar data för e-postmarknadsföring och molnlagringsdestinationer i form av [!DNL CSV] filer. I **[!UICONTROL Scheduling]** kan du konfigurera schemat och filnamnen för varje segment som du exporterar. Det är obligatoriskt att konfigurera schemat, men det är valfritt att konfigurera filnamnet.

>[!IMPORTANT]
> 
>[!DNL Adobe Experience Platform] delar automatiskt upp exportfilerna i 5 miljoner poster (rader) per fil. Varje rad representerar en profil.
>
>Delade filnamn läggs till med en siffra som anger att filen är en del av en större export: `filename.csv`, `filename_2.csv`, `filename_3.csv`.

Välj **[!UICONTROL Create schedule]** som motsvarar det segment som du vill skicka till målet.

![Markera bilder med knappen Skapa schema](../assets/ui/activate-batch-profile-destinations/create-schedule-button.png)

### Exportera fullständiga filer {#export-full-files}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_exportoptions"
>title="Alternativ för filexport"
>abstract="Välj **Exportera fullständiga filer** om du vill exportera en fullständig ögonblicksbild av alla profiler som är kvalificerade för segmentet. Välj **Exportera inkrementella filer** om du bara vill exportera de profiler som är kvalificerade för segmentet sedan den senaste exporten. <br> Den första stegvisa filexporten innehåller alla profiler som kvalificerar sig för segmentet och fungerar som en bakgrundsfyllning. Framtida inkrementella filer innehåller endast de profiler som är kvalificerade för segmentet sedan den första inkrementella filexporten."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations.html#export-incremental-files" text="Exportera inkrementella filer"

>[!CONTEXTUALHELP]
>id="platform_destinations_activationchaining_aftersegmentevaluation"
>title="Aktivera efter segmentutvärdering"
>abstract="Aktiveringen körs omedelbart efter det dagliga segmenteringsjobbet. Detta garanterar att de senaste profilerna exporteras."

>[!CONTEXTUALHELP]
>id="platform_destinations_activationchaining_scheduled"
>title="Schemalagd aktivering"
>abstract="Aktiveringen körs vid en fast tidpunkt på dagen."

Välj **[!UICONTROL Export full files]** för att utlösa export av en fil som innehåller en fullständig ögonblicksbild av alla profilkvalifikationer för det valda segmentet.

![Bild av användargränssnittet med alternativet Exportera hela filer markerat.](../assets/ui/activate-batch-profile-destinations/export-full-files.png)

1. Använd **[!UICONTROL Frequency]** för att välja exportfrekvens:

   * **[!UICONTROL Once]**: schemalägg en enda gång vid behov av fullständig filexport.
   * **[!UICONTROL Daily]**: schemalägga fullständig filexport en gång om dagen, varje dag, vid den tidpunkt du anger.

1. Använd **[!UICONTROL Time]** växla för att välja om exporten ska ske omedelbart efter segmentutvärderingen eller enligt schema, vid en viss tidpunkt. När du väljer **[!UICONTROL Scheduled]** kan du använda väljaren för att välja tid på dygnet, i [!DNL UTC] format, när exporten ska ske.

   >[!NOTE]
   >
   >The **[!UICONTROL After segment evaluation]** det alternativ som beskrivs nedan är för närvarande endast tillgängligt för utvalda Beta-kunder.

   Använd **[!UICONTROL After segment evaluation]** Möjlighet att låta aktiveringsjobbet köras omedelbart efter att det dagliga batchsegmenteringsjobbet för plattformen har slutförts. Detta garanterar att de senaste profilerna exporteras till ditt mål när aktiveringsjobbet körs.

   <!-- Batch segmentation currently runs at {{insert time of day}} and lasts for an average {{x hours}}. Adobe reserves the right to modify this schedule. -->

   ![Bild som markerar alternativet för utvärdering av After segment i aktiveringsflödet för batchmål.](../assets/ui/activate-batch-profile-destinations/after-segment-evaluation-option.png)
Använd **[!UICONTROL Scheduled]** möjlighet att köra aktiveringsjobbet på en fast tidpunkt. Detta garanterar att profildata för Experience Platform exporteras vid samma tidpunkt varje dag, men de profiler du exporterar kanske inte är de mest aktuella, beroende på om gruppsegmenteringsjobbet har slutförts innan aktiveringsjobbet startar.

   ![Bild som markerar alternativet Schemalagd i aktiveringsflödet för batchdestinationer och visar tidsväljaren.](../assets/ui/activate-batch-profile-destinations/scheduled-option.png)

   >[!IMPORTANT]
   >
   >På grund av hur de interna Experience Platform-processerna är konfigurerade kanske den första inkrementella eller fullständiga filexporten inte innehåller alla data för bakåtfyllnad. <br> <br> För att säkerställa en fullständig och mest aktuell dataexport med bakåtfyllnad för både fullständiga och inkrementella filer rekommenderar Adobe att du ställer in den första filexporttiden efter 12 PM GMT följande dag. Denna begränsning kommer att åtgärdas i framtida versioner.

1. Använd **[!UICONTROL Date]** för att välja dag eller intervall när exporten ska ske. För daglig export är det bästa sättet att ställa in start- och slutdatum så att de motsvarar kampanjernas längd i era nedströmsplattformar.

   >[!IMPORTANT]
   >
   > När du väljer ett exportintervall inkluderas inte den sista dagen i intervallet i exporten. Om du till exempel väljer intervallet 4-11 januari kommer den sista filexporten att äga rum den 10 januari.

1. Välj **[!UICONTROL Create]** för att spara schemat.

### Exportera inkrementella filer {#export-incremental-files}

Välj **[!UICONTROL Export incremental files]** för att starta en export där den första filen är en fullständig ögonblicksbild av alla profilkvalifikationer för det valda segmentet, och efterföljande filer är stegvisa profilkvalifikationer sedan den föregående exporten.

>[!IMPORTANT]
>
>Den första exporterade stegvisa filen innehåller alla profiler som kvalificerar sig för ett segment och fungerar som en bakgrundsfyllning.

![Bild av användargränssnittet med alternativet Exportera stegvisa filer markerat.](../assets/ui/activate-batch-profile-destinations/export-incremental-files.png)

1. Använd **[!UICONTROL Frequency]** för att välja exportfrekvens:

   * **[!UICONTROL Daily]**: schemalägg inkrementell filexport en gång om dagen, varje dag, vid den tidpunkt du anger.
   * **[!UICONTROL Hourly]**: schemalägg stegvis filexport var 3, 6, 8 eller 12:e timme.

1. Använd **[!UICONTROL Time]** väljaren för att välja tid på dagen, i [!DNL UTC] format, när exporten ska ske.

   >[!IMPORTANT]
   >
   >På grund av hur de interna Experience Platform-processerna är konfigurerade kanske den första inkrementella eller fullständiga filexporten inte innehåller alla data för bakåtfyllnad. <br> <br> För att säkerställa en fullständig och mest aktuell dataexport med bakåtfyllnad för både fullständiga och inkrementella filer rekommenderar Adobe att du ställer in den första filexporttiden efter 12 PM GMT följande dag. Denna begränsning kommer att åtgärdas i framtida versioner.

1. Använd **[!UICONTROL Date]** för att välja intervallet när exporten ska ske. Det bästa sättet är att ställa in start- och slutdatumet så att det passar kampanjernas längd på era nedströmsplattformar.

   >[!IMPORTANT]
   >
   >Den sista dagen i intervallet inkluderas inte i exporten. Om du till exempel väljer intervallet 4-11 januari kommer den sista filexporten att äga rum den 10 januari.

1. Välj **[!UICONTROL Create]** för att spara schemat.

### Konfigurera filnamn {#file-names}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_filename"
>title="Konfigurera filnamn"
>abstract="För filbaserade mål genereras ett unikt filnamn per segment. Använd filnamnsredigeraren för att skapa och redigera ett unikt filnamn eller behåll standardnamnet."

Standardfilnamnen består av målnamn, segment-ID och datum- och tidsindikator. Du kan till exempel redigera de exporterade filnamnen för att skilja mellan olika kampanjer eller för att lägga till tiden för dataexport till filerna.

Välj pennikonen för att öppna ett modalt fönster och redigera filnamnen. Filnamn får innehålla högst 255 tecken.

>[!NOTE]
>
>Bilden nedan visar hur filnamn kan redigeras för Amazon S3-mål, men processen är identisk för alla gruppmål (till exempel SFTP eller Azure Blob Storage).

![Bild som markerar pennikonen, som används för att konfigurera filnamn.](../assets/ui/activate-batch-profile-destinations/configure-name.png)

I filnamnsredigeraren kan du välja olika komponenter att lägga till i filnamnet.

![Bild som visar alla tillgängliga filnamnsalternativ.](../assets/ui/activate-batch-profile-destinations/activate-workflow-configure-step-2.png)

Målnamnet och segment-ID kan inte tas bort från filnamn. Utöver dessa kan du lägga till följande:

* **[!UICONTROL Segment name]**: Du kan lägga till segmentnamnet till filnamnet.
* **[!UICONTROL Date and time]**: Välj mellan att lägga till en `MMDDYYYY_HHMMSS` format eller en Unix 10-siffrig tidsstämpel för den tid då filerna genereras. Välj ett av dessa alternativ om du vill att ett dynamiskt filnamn ska skapas för varje stegvis export.
* **[!UICONTROL Custom text]**: Lägg till egen text i filnamnen.

Välj **[!UICONTROL Apply changes]** för att bekräfta ditt val.

>[!IMPORTANT]
> 
>Om du inte markerar **[!UICONTROL Date and Time]** -komponenten kommer filnamnen att vara statiska och den nya exporterade filen kommer att skriva över den tidigare filen på lagringsplatsen vid varje export. Detta är det rekommenderade alternativet när du kör ett återkommande importjobb från en lagringsplats till en e-postmarknadsföringsplattform.

När du har konfigurerat alla segment väljer du **[!UICONTROL Next]** för att fortsätta.

## Välj profilattribut {#select-attributes}

För profilbaserade mål måste du välja de profilattribut som du vill skicka till målmålet.


1. I **[!UICONTROL Select attributes]** sida, markera **[!UICONTROL Add new field]**.

   ![Markera bilden med knappen Lägg till nytt fält.](../assets/ui/activate-batch-profile-destinations/add-new-field.png)

1. Markera pilen till höger om **[!UICONTROL Schema field]** post.

   ![Bildmarkering som visar hur du väljer ett källfält.](../assets/ui/activate-batch-profile-destinations/select-target-field.png)

1. I **[!UICONTROL Select field]** väljer du de XDM-attribut som du vill skicka till målet och väljer **[!UICONTROL Select]**.

   ![Bild som visar de olika fälten som är tillgängliga som källfält.](../assets/ui/activate-batch-profile-destinations/target-field-page.png)

1. Om du vill lägga till fler mappningar upprepar du steg ett till tre.

>[!NOTE]
>
> Adobe Experience Platform fyller markeringen i förväg med fyra rekommenderade attribut från ditt schema: `person.name.firstName`, `person.name.lastName`, `personalEmail.address`, `segmentMembership.status`.

Filexporter varierar på följande sätt, beroende på om `segmentMembership.status` är markerat:
* Om `segmentMembership.status` fältet är markerat, exporterade filer innehåller **[!UICONTROL Active]** medlemmar i den första fullständiga ögonblicksbilden och **[!UICONTROL Active]** och **[!UICONTROL Expired]** medlemmar i efterföljande stegvisa exporter.
* Om `segmentMembership.status` fältet är inte markerat, exporterade filer innehåller endast **[!UICONTROL Active]** medlemmar i den första fullständiga ögonblicksbilden och i efterföljande stegvisa exporter.

![Bild som visar förifyllda rekommenderade attribut i mappningssteget i segmentaktiveringsarbetsflödet.](../assets/ui/activate-batch-profile-destinations/mandatory-deduplication.png)

### Obligatoriska attribut {#mandatory-attributes}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_mandatorykey"
>title="Om obligatoriska attribut"
>abstract="Välj de XDM-schemaattribut som alla exporterade profiler ska inkludera. Profiler utan den obligatoriska nyckeln exporteras inte till målet. Om du inte väljer en obligatorisk nyckel exporteras alla kvalificerade profiler oavsett deras attribut."

Ett obligatoriskt attribut är en användaraktiverad kryssruta som ser till att alla profilposter innehåller det valda attributet. Till exempel: alla exporterade profiler innehåller en e-postadress. &#x200B;

Du kan markera attribut som obligatoriska för att säkerställa att [!DNL Platform] exporterar bara de profiler som innehåller det specifika attributet. Det innebär att den kan användas som en extra form av filtrering. Markera ett attribut som obligatoriskt är **not** krävs.

Om du inte väljer ett obligatoriskt attribut exporteras alla kvalificerade profiler oavsett deras attribut.

Vi rekommenderar att ett av attributen är [unik identifierare](../../destinations/catalog/email-marketing/overview.md#identity) från ditt schema. Mer information om obligatoriska attribut finns i avsnittet om identitet i [E-postmarknadsföringsmål](../../destinations/catalog/email-marketing/overview.md#identity) dokumentation.

### Dedupliceringsnycklar {#deduplication-keys}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_deduplicationkey"
>title="Om dedupliceringsnycklar"
>abstract="Eliminera flera poster med samma profil i exportfilerna genom att välja en dedupliceringsnyckel. Välj ett namnutrymme eller upp till två XDM-schemaattribut som en dedupliceringsnyckel. Om du inte väljer en dedupliceringsnyckel kan det leda till dubblettprofilposter i exportfilerna."

En dedupliceringsnyckel är en användardefinierad primärnyckel som avgör identiteten som användarna vill att deras profiler ska dedupliceras med. &#x200B;

Avdupliceringsnycklar eliminerar möjligheten att ha flera poster med samma profil i en exportfil.

Det finns tre sätt att använda dedupliceringstangenter på [!DNL Platform]:

* Använda ett enskilt ID-namnutrymme som [!UICONTROL deduplication key]
* Använda ett profilattribut från ett [!DNL XDM] profil som [!UICONTROL deduplication key]
* Använda en kombination av två profilattribut från en [!DNL XDM] profil som sammansatt nyckel

>[!IMPORTANT]
>
> Du kan exportera ett enskilt ID-namnutrymme till ett mål, och namnutrymmet anges automatiskt som en dedupliceringsnyckel. Det går inte att skicka flera namnutrymmen till ett mål.
> 
> Du kan inte använda en kombination av ID-namnutrymmen och profilattribut som dedupliceringsnycklar.

### Exempel på borttagning av dubbletter {#deduplication-example}

I det här exemplet visas hur borttagning av dubbletter fungerar, beroende på de valda dedupliceringstangenterna.

Låt oss titta på följande två profiler.

**Profil A**

```json
{
  "identityMap": {
    "Email": [
      {
        "id": "johndoe_1@example.com"
      },
      {
        "id": "johndoe_2@example.com"
      }
    ]
  },
  "segmentMembership": {
    "ups": {
      "fa5c4622-6847-4199-8dd4-8b7c7c7ed1d6": {
        "status": "existing",
        "lastQualificationTime": "2021-03-10 10:03:08"
      }
    }
  },
  "person": {
    "name": {
      "lastName": "Doe",
      "firstName": "John"
    }
  },
  "personalEmail": {
    "address": "johndoe@example.com"
  }
}
```

**Profil B**

```json
{
  "identityMap": {
    "Email": [
      {
        "id": "johndoe_1@example.com"
      },
      {
        "id": "johndoe_2@example.com"
      }
    ]
  },
  "segmentMembership": {
    "ups": {
      "fa5c4622-6847-4199-8dd4-8b7c7c7ed1d6": {
        "status": "existing",
        "lastQualificationTime": "2021-04-10 11:33:28"
      }
    }
  },
  "person": {
    "name": {
      "lastName": "D",
      "firstName": "John"
    }
  },
  "personalEmail": {
    "address": "johndoe@example.com"
  }
}
```

### Användning av borttagning av dubbletter, fall 1: ingen deduplicering {#deduplication-use-case-1}

Om du inte använder borttagning av dubbletter innehåller exportfilen följande poster.

| personalEmail | firstName | lastName |
|---|---|---|
| johndoe@example.com | John | Doe |
| johndoe@example.com | John | D |


### Användning vid borttagning av dubbletter, fall 2: deduplicering baserad på ID-namnutrymme {#deduplication-use-case-2}

Anta borttagning av dubbletter av [!DNL Email] -namnutrymmet innehåller exportfilen följande poster. Profil B är den senaste som kvalificerar sig för segmentet, så det är den enda som exporteras.

| E-post* | personalEmail | firstName | lastName |
|---|---|---|---|
| johndoe_1@example.com | johndoe@example.com | John | D |
| johndoe_2@example.com | johndoe@example.com | John | D |

### Användning av borttagning av dubbletter, exempel 3: deduplicering baserad på ett enda profilattribut {#deduplication-use-case-3}

Anta borttagning av dubbletter av `personal Email` skulle exportfilen innehålla följande post. Profil B är den senaste som kvalificerar sig för segmentet, så det är den enda som exporteras.

| personalEmail* | firstName | lastName |
|---|---|---|
| johndoe@example.com | John | D |


### Användning vid borttagning av dubbletter - fall 4: deduplicering baserad på två profilattribut {#deduplication-use-case-4}

Anta borttagning av dubbletter med den sammansatta nyckeln `personalEmail + lastName`, skulle exportfilen innehålla följande poster.

| personalEmail* | lastName* | firstName |
|---|---|---|
| johndoe@example.com | D | John |
| johndoe@example.com | Doe | John |


Adobe rekommenderar att du väljer ett identitetsnamnutrymme som [!DNL CRM ID] eller e-postadress som en dedupliceringsnyckel för att säkerställa att alla profilposter identifieras unikt.

>[!NOTE]
> 
>Om några dataanvändningsetiketter har tillämpats på vissa fält i en datauppsättning (i stället för på hela datauppsättningen), tillämpas dessa fältetiketter vid aktiveringen på följande villkor:
>
>* Fälten används i segmentdefinitionen.
>* Fälten konfigureras som projicerade attribut för målmålet.
>
> Om fältet `person.name.firstName` har vissa dataanvändningsetiketter som är i konflikt med målets marknadsföringsåtgärd, visas en överträdelse av dataanvändningsprincipen i granskningssteget. Mer information finns i [Datastyrning i Adobe Experience Platform](../../rtcdp/privacy/data-governance-overview.md#destinations).

## Granska {#review}

På **[!UICONTROL Review]** kan du se en sammanfattning av markeringen. Välj **[!UICONTROL Cancel]** för att bryta upp flödet, **[!UICONTROL Back]** för att ändra dina inställningar, eller **[!UICONTROL Finish]** för att bekräfta ditt val och börja skicka data till målet.

>[!IMPORTANT]
>
>I det här steget söker Adobe Experience Platform efter brott mot dataanvändningspolicyn. Nedan visas ett exempel där en princip överträds. Du kan inte slutföra arbetsflödet för segmentaktivering förrän du har löst konflikten. Mer information om hur du löser policyöverträdelser finns i [Politiska åtgärder](../../rtcdp/privacy/data-governance-overview.md#enforcement) i dokumentationsavsnittet för datastyrning.

![Bild som visar ett exempel på dataprincipöverträdelse.](../assets/common/data-policy-violation.png)

Om inga principöverträdelser har identifierats väljer du **[!UICONTROL Finish]** för att bekräfta ditt val och börja skicka data till målet.

![Bild som visar granskningsskärmen för segmentaktiveringsarbetsflödet.](../assets/ui/activate-batch-profile-destinations/review.png)

## Verifiera segmentaktivering {#verify}


För e-postmarknadsföringsmål och molnlagringsmål skapar Adobe Experience Platform en `.csv` filen på lagringsplatsen som du angav. Förvänta dig att en ny fil ska skapas på din lagringsplats varje dag. Standardfilformatet är:
`<destinationName>_segment<segmentID>_<timestamp-yyyymmddhhmmss>.csv`

De filer du får tre dagar i följd kan se ut så här:

```console
Salesforce_Marketing_Cloud_segment12341e18-abcd-49c2-836d-123c88e76c39_20200408061804.csv
Salesforce_Marketing_Cloud_segment12341e18-abcd-49c2-836d-123c88e76c39_20200409052200.csv
Salesforce_Marketing_Cloud_segment12341e18-abcd-49c2-836d-123c88e76c39_20200410061130.csv
```

De här filerna finns på lagringsplatsen och du har fått en bekräftelse på att aktiveringen har slutförts. För att förstå hur de exporterade filerna är strukturerade kan du [hämta en CSV-exempelfil](../assets/common/sample_export_file_segment12341e18-abcd-49c2-836d-123c88e76c39_20200408061804.csv). Den här exempelfilen innehåller profilattributen `person.firstname`, `person.lastname`, `person.gender`, `person.birthyear`och `personalEmail.address`.
