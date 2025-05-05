---
keywords: crm;CRM;crm destination;Utanför;Utanför crm-mål
title: Utdataanslutning
description: Med Outreach-destinationen kan du exportera dina kontodata och aktivera dem inom ramarna för ditt företags behov.
exl-id: 7433933d-7a4e-441d-8629-a09cb77d5220
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1639'
ht-degree: 0%

---

# [!DNL Outreach]-anslutning

## Översikt {#overview}

[[!DNL Outreach]](https://www.outreach.io/) är en plattform för Försäljningskörning med de flesta interaktionsdata för B2B-köpare i världen och betydande investeringar i egna AI-tekniker för att omvandla säljdata till intelligens. [!DNL Outreach] hjälper organisationer att automatisera säljengagemanget och agera på intäktsanalys för att förbättra deras effektivitet, förutsägbarhet och tillväxt.

Detta [!DNL Adobe Experience Platform] [mål](/help/destinations/home.md) använder [Resurs-API:t för uppdatering av utdata](https://api.outreach.io/api/v2/docs#update-an-existing-resource), som gör att du kan uppdatera identiteter inom en målgrupp som motsvarar potentiella kunder i [!DNL Outreach].

[!DNL Outreach] använder OAuth 2 med auktoriseringsauktorisering som autentiseringsmekanism för att kommunicera med [!DNL Outreach] [!DNL Update Resource API]. Instruktioner för autentisering till din [!DNL Outreach]-instans finns längre ned i avsnittet [Autentisera till mål](#authenticate).

## Användningsfall {#use-cases}

Som marknadsförare kan ni leverera personaliserade upplevelser till era presumtiva kunder, baserat på attribut från deras Adobe Experience Platform-profiler. Du kan skapa målgrupper utifrån dina offlinedata och skicka dessa målgrupper till [!DNL Outreach] för att visa dem i presumtiva kunders flöden så snart som målgrupper och profiler uppdateras i Adobe Experience Platform.

## Förhandskrav {#prerequisites}

### Krav för Experience Platform {#prerequisites-in-experience-platform}

Innan du aktiverar data till målet [!DNL Outreach] måste du ha ett [schema](/help/xdm/schema/composition.md), en [datamängd](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html) och [segment](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html) som skapats i [!DNL Experience Platform].

Se Adobe dokumentation för schemafältgruppen [Information om målgruppsmedlemskap](/help/xdm/field-groups/profile/segmentation.md) om du behöver vägledning om målgruppsstatus.

### Förutsättningar {#prerequisites-destination}

Observera följande krav i [!DNL Outreach] för att kunna exportera data från Experience Platform till ditt [!DNL Outreach]-konto:

#### Du måste ha ett Outlook-konto {#prerequisites-account}

Gå till sidan [!DNL Outreach] [Logga in](https://accounts.outreach.io/users/sign_in) för att registrera och skapa ett konto, om du inte redan har ett. Se även sidan [!DNL Outreach] support [för mer information.](https://support.outreach.io/hc/en-us/articles/207238607-Claim-Your-Outreach-Account)

Observera objekten nedan innan du autentiserar till CRM-målet [!DNL Outreach]:

| Autentiseringsuppgifter | Beskrivning |
|---|---|
| E-post | E-postadress till ditt [!DNL Outreach]-konto |
| Lösenord | Lösenord för ditt [!DNL Outreach]-konto |

#### Ställ in anpassade fältetiketter {#prerequisites-custom-fields}

[!DNL Outreach] stöder anpassade fält för [prospects](https://support.outreach.io/hc/en-us/articles/360001557554-Outreach-Prospect-Profile-Overview). Mer information finns i [Så här lägger du till ett anpassat fält i Utdata](https://support.outreach.io/hc/en-us/articles/219124908-How-To-Add-a-Custom-Field-in-Outreach). För att underlätta identifieringen rekommenderar vi att etiketterna uppdateras manuellt till motsvarande målgruppsnamn i stället för att standardvärdena behålls. Exempel:

[!DNL Outreach] inställningssida för potentiella kunder som visar anpassade fält.
![Skärmbild av gränssnittet som visar anpassade fält på inställningssidan visas.](../../assets/catalog/crm/outreach/outreach-custom-fields.png)

[!DNL Outreach] inställningssida för potentiella kunder som visar anpassade fält med *användarvänliga* etiketter som matchar målgruppsnamnen. Du kan visa målgruppsstatus på den potentiella kundens sida mot dessa etiketter.
![Skärmbild av gränssnittet som visar anpassade fält med associerade etiketter på inställningssidan.](../../assets/catalog/crm/outreach/outreach-custom-field-labels.png)

>[!NOTE]
>
> Etikettnamn är bara till för att underlätta identifiering. De används inte vid uppdatering av potentiella kunder.

## Guardrails

API:t [!DNL Outreach] har en hastighetsgräns på 10 000 begäranden per timme och användare. Om du når den här gränsen får du ett `429`-svar med följande meddelande: `You have exceeded your permitted rate limit of 10,000; please try again at 2017-01-01T00:00:00.`.

Om du får det här meddelandet måste du uppdatera ditt exportschema för målgruppen så att det uppfyller tröskelvärdet.

Mer information finns i [[!DNL Outreach] dokumentationen](https://api.outreach.io/api/v2/docs#rate-limiting).

## Identiteter som stöds {#supported-identities}

[!DNL Outreach] har stöd för uppdatering av identiteter som beskrivs i tabellen nedan. Läs mer om [identiteter](/help/identity-service/features/namespaces.md).

| Målidentitet | Beskrivning | Överväganden |
|---|---|---|
| `OutreachId` | <ul><li>Identifierare för [!DNL Outreach]. Detta är ett numeriskt värde som motsvarar profilen för potentiell kund.</li><li>ID:t måste matcha ID:t inom URL:en för [!DNL Outreach] för den potentiella kund som uppdateras.</li><li>Mer information finns i [[!DNL Outreach] dokumentationen](https://api.outreach.io/api/v2/docs#update-an-existing-resource).</li></ul> | Obligatoriskt |

## Exportera typ och frekvens {#export-type-frequency}

Se tabellen nedan för information om exporttyp och frekvens för destinationen.

| Objekt | Typ | Anteckningar |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Profile-based]** | <ul><li> Du exporterar alla medlemmar i ett segment, tillsammans med de önskade schemafälten *(till exempel e-postadress, telefonnummer, efternamn)*, enligt fältmappningen.</li><li> Varje segmentstatus i [!DNL Outreach] uppdateras med motsvarande målgruppsstatus från Experience Platform, baserat på det [!UICONTROL Mapping ID]-värde som angavs under [målgruppsplaneringssteget](#schedule-segment-export-example).</li></ul> |
| Exportfrekvens | **[!UICONTROL Streaming]** | <ul><li> Direktuppspelningsmål är alltid på API-baserade anslutningar. Så snart en profil uppdateras i Experience Platform baserat på målgruppsutvärdering skickar anslutningsprogrammet uppdateringen nedströms till målplattformen. Läs mer om [direktuppspelningsmål](/help/destinations/destination-types.md#streaming-destinations).</li></ul> |

{style="table-layout:auto"}

## Anslut till målet {#connect}

>[!IMPORTANT]
> 
> Om du vill ansluta till målet måste du ha **[!UICONTROL Manage Destinations]** [åtkomstkontrollbehörighet](/help/access-control/home.md#permissions). Läs [åtkomstkontrollsöversikten](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få den behörighet som krävs.

Om du vill ansluta till det här målet följer du stegen som beskrivs i självstudiekursen [för destinationskonfiguration](../../ui/connect-destination.md). I arbetsflödet för att konfigurera mål fyller du i fälten som listas i de två avsnitten nedan.

I **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]** söker du efter [!DNL Outreach]. Du kan också hitta den under CRM-kategorin.

### Autentisera till mål {#authenticate}

Om du vill autentisera till målet väljer du **[!UICONTROL Connect to destination]**.

![Experience Platform UI, skärmbild som visar hur du autentiserar till Outreach.](../../assets/catalog/crm/outreach/authenticate-destination.png)

Du visas inloggningssidan för [!DNL Outreach]. Ange din e-postadress.

![Skärmbild av gränssnittet som visar fältet för att mata in e-post för autentisering till utdataenheten.](../../assets/catalog/crm/outreach/authenticate-destination-login-email.png)

Ange sedan ditt lösenord.

![Skärmbild av gränssnittet som visar fältet som anger lösenordssteg för autentisering till utdataenheten.](../../assets/catalog/crm/outreach/authenticate-destination-login-password.png)

* **[!UICONTROL Username]**: E-postadressen till ditt [!DNL Outreach]-konto.
* **[!UICONTROL Password]**: Lösenordet för ditt [!DNL Outreach]-konto.

Om den angivna informationen är giltig visas statusen **Ansluten** med en grön bockmarkering. Du kan sedan gå vidare till nästa steg.

### Fyll i målinformation {#destination-details}

Om du vill konfigurera information för målet fyller du i de obligatoriska och valfria fälten nedan. En asterisk bredvid ett fält i användargränssnittet anger att fältet är obligatoriskt.
![Experience Platform UI-skärmbild som visar hur du fyller i information för målplatsen Utanför.](../../assets/catalog/crm/outreach/destination-details.png)

* **[!UICONTROL Name]**: Ett namn som du känner igen det här målet med i framtiden.
* **[!UICONTROL Description]**: En beskrivning som hjälper dig att identifiera det här målet i framtiden.

### Aktivera aviseringar {#enable-alerts}

Du kan aktivera varningar för att få meddelanden om dataflödets status till ditt mål. Välj en avisering i listan om du vill prenumerera och få meddelanden om statusen för ditt dataflöde. Mer information om varningar finns i guiden [prenumerera på destinationsvarningar med användargränssnittet](../../ui/alerts.md).

Välj **[!UICONTROL Next]** när du är klar med att ange information för målanslutningen.

## Aktivera målgrupper till det här målet {#activate}

>[!IMPORTANT]
> 
>* För att aktivera data behöver du behörigheterna **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** och **[!UICONTROL View Segments]** [åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontrollsöversikten](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få den behörighet som krävs.
>* Om du vill exportera *identiteter* måste du ha **[!UICONTROL View Identity Graph]** [åtkomstkontrollbehörighet](/help/access-control/home.md#permissions). <br> ![Markera identitetsnamnområdet som är markerat i arbetsflödet för att aktivera målgrupper till mål.](/help/destinations/assets/overview/export-identities-to-destination.png "Markera identitetsnamnområdet som är markerat i arbetsflödet för att aktivera målgrupper till mål."){width="100" zoomable="yes"}

Läs [Aktivera profiler och målgrupper för att direktuppspela målgruppsexportdestinationer](../../ui/activate-segment-streaming-destinations.md) för instruktioner om hur du aktiverar målgrupper till det här målet.

### Mappa överväganden och exempel {#mapping-considerations-example}

Om du vill skicka målgruppsdata från Adobe Experience Platform till målet [!DNL Outreach] måste du gå igenom fältmappningssteget. Mappningen består av att skapa en länk mellan XDM-schemafälten (Experience Data Model) i ditt Experience Platform-konto och deras motsvarande motsvarigheter från målmålet. Följ de här stegen för att mappa dina XDM-fält korrekt till målfälten för [!DNL Outreach]:

1. Klicka på **[!UICONTROL Add new mapping]** i steget [!UICONTROL Mapping]. En ny mappningsrad visas på skärmen.
   ![Experience Platform UI, bild som visar hur du lägger till ny mappning](../../assets/catalog/crm/outreach/add-new-mapping.png)

1. Välj kategorin **[!UICONTROL Select identity namespace]** i fönstret [!UICONTROL Select source field] och lägg till de önskade mappningarna.
   ![Experience Platform UI, skärmbild som visar Source-mappning](../../assets/catalog/crm/outreach/source-mapping.png)

1. I fönstret [!UICONTROL Select target field] väljer du den typ av målfält som du vill mappa källfältet till.
   * **[!UICONTROL Select identity namespace]**: välj det här alternativet om du vill mappa källfältet till ett identitetsnamnområde från listan.

     ![Experience Platform UI-skärmbild som visar Target-mappning med OutreachId.](../../assets/catalog/crm/outreach/target-mapping.png)

   * Lägg till följande mappning mellan ditt XDM-profilschema och din [!DNL Outreach]-instans:

     | XDM-profilschema | [!DNL Outreach]-instans | Obligatoriskt |
     |---|---|---|
     | `Oid` | `OutreachId` | Ja |

   * **[!UICONTROL Select custom attributes]**: välj det här alternativet om du vill mappa källfältet till ett anpassat attribut som du definierar i fältet [!UICONTROL Attribute name]. Se [[!DNL Outreach] dokumentationen för den potentiella kunden](https://api.outreach.io/api/v2/docs#prospect) för en utförlig lista över attribut som stöds.

     ![Experience Platform UI-skärmbild som visar Target-mappning med LastName.](../../assets/catalog/crm/outreach/target-mapping-lastname.png)

   * Beroende på vilka värden du vill uppdatera lägger du till följande mappning mellan XDM-profilschemat och [!DNL Outreach]-instansen:

     | XDM-profilschema | [!DNL Outreach]-instans |
     |---|---|
     | `person.name.firstName` | `firstName` |
     | `person.name.lastName` | `lastName` |

   * Ett exempel på hur du använder dessa mappningar visas nedan:

     ![Exempel på skärmbild i Experience Platform UI som visar målmappningar.](../../assets/catalog/crm/outreach/mappings.png)

### Schemalägg målgruppsexport och exempel {#schedule-segment-export-example}

* När du utför steget [Schemalägg målgruppsexport](../../ui/activate-segment-streaming-destinations.md) måste du manuellt mappa Experience Platform-målgrupper till det anpassade fältattributet i [!DNL Outreach].

* Det gör du genom att markera varje segment och sedan ange motsvarande numeriska värde som motsvarar fältet *Egen fältetikett `N`* från [!DNL Outreach] i fältet **[!UICONTROL Mapping ID]**.

  >[!IMPORTANT]
  >
  > * Det numeriska värdet *(`N`)* som används i [!UICONTROL Mapping ID] ska matcha det anpassade attributnyckelsuffixet med det numeriska värdet i [!DNL Outreach]. Exempel: *Eget fält `N` Etikett*.
  > * Du behöver bara ange det numeriska värdet, inte hela etiketten för anpassade fält.
  > * [!DNL Outreach] stöder maximalt 150 anpassade etikettfält.
  > * Mer information finns i [[!DNL Outreach] dokumentationen för den potentiella kunden](https://api.outreach.io/api/v2/docs#prospect).

   * Exempel:

     | [!DNL Outreach]-fält | Experience Platform Mappnings-ID |
     |---|---|
     | Etikett för anpassat fält `4` | `4` |

     ![Experience Platform UI-skärmbild som visar ett exempel på mappnings-ID vid export av schemalagda målgrupper.](../../assets/catalog/crm/outreach/schedule-segment-export.png)

## Validera dataexport {#exported-data}

Följ stegen nedan för att verifiera att du har konfigurerat målet korrekt:

1. Välj **[!UICONTROL Destinations]** > **[!UICONTROL Browse]** för att navigera till listan över mål.
   ![Experience Platform UI, skärmbild med Sök mål.](../../assets/catalog/crm/outreach/browse-destinations.png)

1. Markera målet och validera att statusen är **[!UICONTROL enabled]**.
   ![Experience Platform UI-skärmbild med körning av måldataflöde för det valda målet.](../../assets/catalog/crm/outreach/destination-dataflow-run.png)

1. Växla till fliken **[!DNL Activation data]** och välj sedan ett publiknamn.
   ![Experience Platform UI, skärmbild med aktiveringsdata för destinationer.](../../assets/catalog/crm/outreach/destinations-activation-data.png)

1. Övervaka målgruppssammanfattningen och se till att antalet profiler motsvarar antalet som skapas inom segmentet.
   ![Experience Platform UI-skärmbild med segmentsammanfattning.](../../assets/catalog/crm/outreach/segment.png)

1. Logga in på webbplatsen [!DNL Outreach], gå till sidan [!DNL Apps] > [!DNL Contacts] och kontrollera om profilerna från målgruppen har lagts till. Du kan se att varje målgruppsstatus i [!DNL Outreach] har uppdaterats med motsvarande målgruppsstatus från Experience Platform, baserat på värdet [!UICONTROL Mapping ID] som angavs under steget [målgruppsplanering](#schedule-segment-export-example).

![Skärmbild av gränssnittet som visar sidan Utanför potentiell kund med de uppdaterade målgruppsstatusarna visas.](../../assets/catalog/crm/outreach/outreach-prospect.png)

## Dataanvändning och styrning {#data-usage-governance}

Alla [!DNL Adobe Experience Platform]-mål är kompatibla med dataanvändningsprinciper när data hanteras. Mer information om hur [!DNL Adobe Experience Platform] använder datastyrning finns i [Datastyrningsöversikten](/help/data-governance/home.md).

## Fel och felsökning {#errors-and-troubleshooting}

När du kontrollerar ett dataflöde kan följande felmeddelande visas: `Bad request reported while pushing events to the destination. Please contact the administrator and try again.`

![Experience Platform UI-skärmbild som visar felet Felaktig begäran.](../../assets/catalog/crm/outreach/error.png)

Om du vill åtgärda det här felet kontrollerar du att [!UICONTROL Mapping ID] som du har angett i Experience Platform för din [!DNL Outreach]-målgrupp är giltig och finns i [!DNL Outreach].

## Ytterligare resurser {#additional-resources}

[[!DNL Outreach] Dokumentationen](https://api.outreach.io/api/v2/docs/) innehåller information om [Felsvar](https://api.outreach.io/api/v2/docs#error-responses) som du kan använda för att felsöka eventuella problem.
