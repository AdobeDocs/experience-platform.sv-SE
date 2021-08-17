---
keywords: aktivera profildestinationer;aktivera destinationer;aktivera data; aktivera e-postmarknadsföringsmål, aktivera molnlagringsmål
title: Aktivera målgruppsdata för att batchprofilera exportmål
type: Tutorial
seo-title: Aktivera målgruppsdata för att batchprofilera exportmål
description: Lär dig hur du aktiverar målgruppsdata som du har i Adobe Experience Platform genom att skicka segment till gruppprofilbaserade mål.
seo-description: Lär dig hur du aktiverar målgruppsdata som du har i Adobe Experience Platform genom att skicka segment till gruppprofilbaserade mål.
source-git-commit: 02c22453470d55236d4235c479742997e8407ef3
workflow-type: tm+mt
source-wordcount: '1943'
ht-degree: 0%

---


# Aktivera målgruppsdata för att batchprofilera exportmål

## Översikt {#overview}

I den här artikeln förklaras det arbetsflöde som krävs för att aktivera målgruppsdata i Adobe Experience Platform batchprofilbaserade mål, som molnlagring och e-postmarknadsföringsmål.

## Förutsättningar {#prerequisites}

Om du vill aktivera data till mål måste du ha [anslutit till ett mål](./connect-destination.md). Om du inte redan har gjort det går du till [målkatalogen](../catalog/overview.md), bläddrar bland de mål som stöds och konfigurerar det mål som du vill använda.

## Välj mål {#select-destination}

1. Gå till **[!UICONTROL Connections > Destinations]** och välj fliken **[!UICONTROL Browse]**.

   ![Fliken Målsökning](../assets/ui/activate-batch-profile-destinations/browse-tab.png)

1. Markera **[!UICONTROL Add segments]**-knappen som motsvarar målet där du vill aktivera dina segment, vilket visas i bilden nedan.

   ![Aktivera knappar](../assets/ui/activate-batch-profile-destinations/activate-buttons-browse.png)

1. Gå till nästa avsnitt för att [markera dina segment](#select-segments).

## Välj segment {#select-segments}

Använd kryssrutorna till vänster om segmentnamnen för att markera de segment som du vill aktivera för målet och välj sedan **[!UICONTROL Next]**.

![Markera segment](../assets/ui/activate-batch-profile-destinations/select-segments.png)


## Schemalägg segmentexport {#scheduling}

[!DNL Adobe Experience Platform] exporterar data för e-postmarknadsföring och molnlagringsdestinationer i form av  [!DNL CSV] filer. På sidan **[!UICONTROL Scheduling]** kan du konfigurera schemat och filnamnen för varje segment som du exporterar. Det är obligatoriskt att konfigurera schemat, men det är valfritt att konfigurera filnamnet.

>[!IMPORTANT]
> 
>[!DNL Adobe Experience Platform] delar automatiskt upp exportfilerna i 5 miljoner poster (rader) per fil. Varje rad representerar en profil.
>
>Delade filnamn läggs till med en siffra som anger att filen är en del av en större export: `filename.csv`, `filename_2.csv`, `filename_3.csv`.

Välj knappen **[!UICONTROL Create schedule]** för det segment som du vill skicka till målet.

![Knappen Skapa schema](../assets/ui/activate-batch-profile-destinations/create-schedule-button.png)

### Exportera fullständiga filer {#export-full-files}

Välj **[!UICONTROL Export full files]** om du vill att de exporterade filerna ska innehålla en fullständig ögonblicksbild av alla profiler som är kvalificerade för det segmentet.

![Exportera fullständiga filer](../assets/ui/activate-batch-profile-destinations/export-full-files.png)

1. Använd **[!UICONTROL Frequency]**-väljaren för att välja mellan engångsexporter (**[!UICONTROL Once]**) eller **[!UICONTROL Daily]**. Vid export av en fullständig fil **[!UICONTROL Daily]** exporteras filen varje dag från startdatumet till slutdatumet kl. 12:00 UTC (7:00 EST).
2. Använd **[!UICONTROL Time]**-väljaren för att välja tidpunkten på dagen, i [!DNL UTC]-format, när exporten ska ske. När du exporterar en fil **[!UICONTROL Daily]** exporteras filen varje dag från startdatumet till slutdatumet vid den tidpunkt du väljer.

   >[!IMPORTANT]
   >
   >Alternativet att exportera filer vid en viss tidpunkt finns för närvarande i betaversion och är endast tillgängligt för ett visst antal kunder.<br> <br> På grund av hur de interna Experience Platform-processerna är konfigurerade kanske den första inkrementella eller fullständiga filexporten inte innehåller alla data för bakåtfyllnad.  <br> <br> För att säkerställa en fullständig och mest aktuell dataexport med bakåtfyllnad för både fullständiga och inkrementella filer rekommenderar Adobe att du ställer in den första filexporttiden efter 12 PM GMT följande dag. Detta är en begränsning som kommer att åtgärdas i framtida versioner.

3. Använd **[!UICONTROL Date]**-väljaren för att välja dag eller intervall när exporten ska ske.
4. Välj **[!UICONTROL Create]** om du vill spara schemat.


### Exportera inkrementella filer {#export-incremental-files}

Välj **[!UICONTROL Export incremental files]** om du vill att de exporterade filerna bara ska innehålla de profiler som är kvalificerade för det segmentet sedan den senaste exporten.

>[!IMPORTANT]
>
>Den första exporterade stegvisa filen innehåller alla profiler som kvalificerar sig för ett segment och fungerar som en bakgrundsfyllning.

![Exportera inkrementella filer](../assets/ui/activate-batch-profile-destinations/export-incremental-files.png)

1. Använd **[!UICONTROL Frequency]**-väljaren för att välja mellan **[!UICONTROL Daily]** eller **[!UICONTROL Hourly]**-exporter. Vid export av en inkrementell fil **[!UICONTROL Daily]** exporteras filen varje dag från startdatumet till slutdatumet kl. 12:00 UTC (07:00 EST).
   * När du väljer **[!UICONTROL Hourly]** använder du **[!UICONTROL Every]**-väljaren för att välja mellan alternativen **[!UICONTROL 3]**, **[!UICONTROL 6]**, **[!UICONTROL 8]** och **[!UICONTROL 12]** timme.

      >[!IMPORTANT]
      >
      >Alternativet att exportera inkrementella filer var 3, 6, 8 eller 12:e timme finns för närvarande i betaversionen och är bara tillgängligt för ett visst antal kunder. Kunder som inte är beta kan exportera inkrementella filer en gång om dagen.

2. Använd **[!UICONTROL Time]**-väljaren för att välja tidpunkten på dagen, i [!DNL UTC]-format, när exporten ska ske.

   >[!IMPORTANT]
   >
   >Alternativet att välja tid på dagen för exporten är bara tillgängligt för ett visst antal kunder. <br> <br> På grund av hur de interna Experience Platform-processerna är konfigurerade kanske den första inkrementella eller fullständiga filexporten inte innehåller alla data för bakåtfyllnad.  <br> <br> För att säkerställa en fullständig och mest aktuell dataexport med bakåtfyllnad för både fullständiga och inkrementella filer rekommenderar Adobe att du ställer in den första filexporttiden efter 12 PM GMT följande dag. Detta är en begränsning som kommer att åtgärdas i framtida versioner.

3. Använd **[!UICONTROL Date]**-väljaren för att välja dag eller intervall när exporten ska ske.
4. Välj **[!UICONTROL Create]** om du vill spara schemat.

### Konfigurera filnamn {#file-names}

Standardfilnamnen består av målnamn, segment-ID och datum- och tidsindikator. Du kan till exempel redigera de exporterade filnamnen för att skilja mellan olika kampanjer eller för att lägga till tiden för dataexport till filerna.

Välj pennikonen för att öppna ett modalt fönster och redigera filnamnen. Filnamn får innehålla högst 255 tecken.

![konfigurera filnamn](../assets/ui/activate-batch-profile-destinations/configure-name.png)

I filnamnsredigeraren kan du välja olika komponenter att lägga till i filnamnet.

![redigera filnamnsalternativ](../assets/ui/activate-batch-profile-destinations/activate-workflow-configure-step-2.png)

Målnamnet och segment-ID kan inte tas bort från filnamn. Utöver dessa kan du lägga till följande:

* **[!UICONTROL Segment name]**: Du kan lägga till segmentnamnet till filnamnet.
* **[!UICONTROL Date and time]**: Välj mellan att lägga till ett  `MMDDYYYY_HHMMSS` format eller en Unix 10-siffrig tidsstämpel för den tidpunkt då filerna genereras. Välj ett av dessa alternativ om du vill att ett dynamiskt filnamn ska skapas för varje stegvis export.
* **[!UICONTROL Custom text]**: Lägg till egen text i filnamnen.

Välj **[!UICONTROL Apply changes]** för att bekräfta ditt val.

>[!IMPORTANT]
> 
>Om du inte markerar komponenten **[!UICONTROL Date and Time]** kommer filnamnen att vara statiska och den nya exporterade filen kommer att skriva över den tidigare filen på lagringsplatsen vid varje export. Detta är det rekommenderade alternativet när du kör ett återkommande importjobb från en lagringsplats till en e-postmarknadsföringsplattform.

När du har konfigurerat alla segment väljer du **[!UICONTROL Next]** för att fortsätta.

## Välj profilattribut {#select-attributes}

För profilbaserade mål måste du välja de profilattribut som du vill skicka till målmålet.


1. Välj **[!UICONTROL Add new field]** på sidan **[!UICONTROL Select attributes]**.

   ![Lägg till ny mappning](../assets/ui/activate-batch-profile-destinations/add-new-field.png)

1. Markera pilen till höger om **[!UICONTROL Schema field]**-posten.

   ![Välj källfält](../assets/ui/activate-batch-profile-destinations/select-target-field.png)

1. På sidan **[!UICONTROL Select field]** markerar du de XDM-attribut som du vill skicka till målet och väljer sedan **[!UICONTROL Select]**.

   ![Välj källfältssida](../assets/ui/activate-batch-profile-destinations/target-field-page.png)


1. Om du vill lägga till fler mappningar upprepar du steg 1 till 3.


>[!NOTE]
>
> Adobe Experience Platform fyller markeringen i förväg med fyra rekommenderade attribut från ditt schema: `person.name.firstName`, `person.name.lastName`, `personalEmail.address`, `segmentMembership.status`.

Filexporter varierar på följande sätt, beroende på om `segmentMembership.status` är markerat:
* Om fältet `segmentMembership.status` är markerat innehåller exporterade filer **[!UICONTROL Active]**-medlemmar i den första fullständiga ögonblicksbilden och **[!UICONTROL Active]**- och **[!UICONTROL Expired]**-medlemmar i efterföljande stegvisa exporter.
* Om fältet `segmentMembership.status` inte är markerat innehåller exporterade filer endast **[!UICONTROL Active]** medlemmar i den första fullständiga ögonblicksbilden och i efterföljande stegvisa exporter.

![rekommenderade attribut](../assets/ui/activate-batch-profile-destinations/mandatory-deduplication.png)

### Obligatoriska attribut {#mandatory-attributes}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_mandatorykey"
>title="Om obligatoriska attribut"
>abstract="Välj de XDM-schemaattribut som alla exporterade profiler ska inkludera. Profiler utan den obligatoriska nyckeln exporteras inte till målet. Om du inte väljer en obligatorisk nyckel exporteras alla kvalificerade profiler oavsett deras attribut."
>additional-url="http://www.adobe.com/go/destinations-mandatory-attributes-en" text="Läs mer i dokumentationen"

Du kan markera attribut som obligatoriska för att vara säker på att [!DNL Platform] bara exporterar de profiler som innehåller det specifika attributet. Det innebär att den kan användas som en extra form av filtrering. Det är **inte** obligatoriskt att markera ett attribut som obligatoriskt.

Om du inte väljer ett obligatoriskt attribut exporteras alla kvalificerade profiler oavsett deras attribut.

Vi rekommenderar att ett av attributen är en [unik identifierare](../../destinations/catalog/email-marketing/overview.md#identity) från ditt schema. Mer information om obligatoriska attribut finns i avsnittet om identitet i [E-postmarknadsföringsmål](../../destinations/catalog/email-marketing/overview.md#identity)-dokumentationen.

### Dedupliceringsnycklar {#deduplication-keys}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_deduplicationkey"
>title="Om dedupliceringsnycklar"
>abstract="Eliminera flera poster med samma profil i exportfilerna genom att välja en dedupliceringsnyckel. Välj ett namnutrymme eller upp till två XDM-schemaattribut som en dedupliceringsnyckel. Om du inte väljer en dedupliceringsnyckel kan det leda till dubblettprofilposter i exportfilerna."
>additional-url="http://www.adobe.com/go/destinations-deduplication-keys-en" text="Läs mer i dokumentationen"

>[!IMPORTANT]
>
>Alternativet att använda dedupliceringsnycklar finns för närvarande i betaversion och är bara tillgängligt för ett visst antal kunder.

Avdupliceringsnycklar eliminerar möjligheten att ha flera poster med samma profil i en exportfil.

Det finns tre sätt att använda dedupliceringsnycklar i [!DNL Platform]:

* Använda ett enskilt identitetsnamnutrymme som [!UICONTROL deduplication key]
* Använda ett profilattribut från en [!DNL XDM]-profil som [!UICONTROL deduplication key]
* Använda en kombination av två profilattribut från en [!DNL XDM]-profil som en sammansatt nyckel

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

### Användning av borttagning av dubbletter, fall 1: ingen deduplicering

Om du inte använder borttagning av dubbletter innehåller exportfilen följande poster.

| personalEmail | firstName | lastName |
|---|---|---|
| johndoe@example.com | John | Doe |
| johndoe@example.com | John | D |


### Användning vid borttagning av dubbletter, fall 2: deduplicering baserad på ID-namnutrymme

Om du utgår från borttagning av dubbletter av namnutrymmet [!DNL Email] innehåller exportfilen följande poster. Profil B är den senaste som kvalificerar sig för segmentet, så det är den enda som exporteras.

| E-post* | personalEmail | firstName | lastName |
|---|---|---|---|
| johndoe_1@example.com | johndoe@example.com | John | D |
| johndoe_2@example.com | johndoe@example.com | John | D |

### Användning av borttagning av dubbletter, exempel 3: deduplicering baserad på ett enda profilattribut

Om attributet `personal Email` tar bort dubbletter innehåller exportfilen följande post. Profil B är den senaste som kvalificerar sig för segmentet, så det är den enda som exporteras.

| personalEmail* | firstName | lastName |
|---|---|---|
| johndoe@example.com | John | D |


### Användning vid borttagning av dubbletter - fall 4: deduplicering baserad på två profilattribut (sammansatt dedupliceringsnyckel)

Om den sammansatta nyckeln `personalEmail + lastName` tar bort dubbletter innehåller exportfilen följande poster.

| personalEmail* | lastName* | firstName |
|---|---|---|
| johndoe@example.com | D | John |
| johndoe@example.com | Doe | John |


Adobe rekommenderar att du väljer ett identitetsnamnutrymme som [!DNL CRM ID] eller en e-postadress som en dedupliceringsnyckel för att se till att alla profilposter identifieras unikt.

>[!NOTE]
> 
>Om några dataanvändningsetiketter har tillämpats på vissa fält i en datauppsättning (i stället för på hela datauppsättningen), tillämpas dessa fältetiketter vid aktiveringen på följande villkor:
>
>* Fälten används i segmentdefinitionen.
>* Fälten konfigureras som projicerade attribut för målmålet.

>
> 
Om till exempel fältet `person.name.firstName` har vissa etiketter för dataanvändning som är i konflikt med målets marknadsföringsåtgärd, visas en överträdelse av dataanvändningsprincipen i granskningssteget. Mer information finns i [Datastyrning i Adobe Experience Platform](../../rtcdp/privacy/data-governance-overview.md#destinations).

## Granska {#review}

På sidan **[!UICONTROL Review]** visas en sammanfattning av ditt val. Välj **[!UICONTROL Cancel]** om du vill dela upp flödet, **[!UICONTROL Back]** om du vill ändra inställningarna eller **[!UICONTROL Finish]** om du vill bekräfta valet och börja skicka data till målet.

>[!IMPORTANT]
>
>I det här steget söker Adobe Experience Platform efter brott mot dataanvändningspolicyn. Nedan visas ett exempel där en princip överträds. Du kan inte slutföra arbetsflödet för segmentaktivering förrän du har löst konflikten. Mer information om hur du löser policyöverträdelser finns i [Politiska åtgärder](../../rtcdp/privacy/data-governance-overview.md#enforcement) i dokumentationsavsnittet för datastyrning.

![dataprincipöverträdelse](../assets/common/data-policy-violation.png)

Om inga principöverträdelser har identifierats markerar du **[!UICONTROL Finish]** för att bekräfta ditt val och börja skicka data till målet.

![Granska](../assets/ui/activate-batch-profile-destinations/review.png)

## Verifiera segmentaktivering {#verify}


För e-postmarknadsföringsmål och molnlagringsmål skapar Adobe Experience Platform en tabbavgränsad `.csv`-fil på den lagringsplats som du angav. Förvänta dig att en ny fil ska skapas på din lagringsplats varje dag. Standardfilformatet är:
`<destinationName>_segment<segmentID>_<timestamp-yyyymmddhhmmss>.csv`

De filer du får tre dagar i följd kan se ut så här:

```console
Salesforce_Marketing_Cloud_segment12341e18-abcd-49c2-836d-123c88e76c39_20200408061804.csv
Salesforce_Marketing_Cloud_segment12341e18-abcd-49c2-836d-123c88e76c39_20200409052200.csv
Salesforce_Marketing_Cloud_segment12341e18-abcd-49c2-836d-123c88e76c39_20200410061130.csv
```

De här filerna finns på lagringsplatsen och du har fått en bekräftelse på att aktiveringen har slutförts. Om du vill veta hur de exporterade filerna är strukturerade kan du [hämta en csv-exempelfil](../assets/common/sample_export_file_segment12341e18-abcd-49c2-836d-123c88e76c39_20200408061804.csv). Den här exempelfilen innehåller profilattributen `person.firstname`, `person.lastname`, `person.gender`, `person.birthyear` och `personalEmail.address`.
