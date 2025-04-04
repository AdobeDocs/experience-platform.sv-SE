---
title: Mailchimp-taggar
description: Med Mailchimp Tags-målet kan du exportera dina kontodata och aktivera dem i Mailchimp för att interagera med kontakterna.
last-substantial-update: 2024-02-20T00:00:00Z
exl-id: 0f278ca8-4fcf-4c47-b538-9cffa45a3d90
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1601'
ht-degree: 0%

---

# [!DNL Mailchimp Tags]-anslutning

[[!DNL Mailchimp]](https://mailchimp.com) *(kallas även [!DNL Intuit Mailchimp])* är en populär plattform för automatiserad marknadsföring och en e-postmarknadsföringstjänst som används av företag för att hantera och kommunicera med kontakter *(kunder, kunder eller andra berörda parter)* med hjälp av e-postlistor och e-postmarknadsföringskampanjer.

[!DNL Mailchimp Tags] använder [målgrupper](https://mailchimp.com/help/getting-started-audience/) och [taggar](https://mailchimp.com/help/getting-started-tags/) för att hantera din kontaktinformation. Taggar är etiketter som du använder för att ordna dina kontakter och etikettera dem för din interna kategorisering i [!DNL Mailchimp].

Jämfört med [!DNL Mailchimp Interest Categories] som du skulle använda för att sortera dina kontakter baserat på deras intressen och inställningar, är [!DNL Mailchimp Tags] tänkt att hantera prenumerationer på ämnen som dina kontakter kan vara intresserade av. *Obs! Experience Platform har också en anslutning för [!DNL Mailchimp Interest Categories], du kan checka ut den på sidan [[!DNL Mailchimp Interest Categories]](/help/destinations/catalog/email-marketing/mailchimp-interest-categories.md).*

Detta [!DNL Adobe Experience Platform] [mål](/help/destinations/home.md) drar nytta av slutpunkten [[!DNL Mailchimp batch subscribe or unsubscribe API]](https://mailchimp.com/developer/marketing/api/lists/batch-subscribe-or-unsubscribe/). Du kan **lägga till nya kontakter** eller **uppdatera taggar för befintliga [!DNL Mailchimp] kontakter** inom en befintlig [!DNL Mailchimp]-målgrupp efter att ha aktiverat dem inom en ny målgrupp. [!DNL Mailchimp Tags] använder de valda målgruppsnamnen från Experience Platform som taggnamn i [!DNL Mailchimp].

## Användningsfall {#use-cases}

För att du bättre ska kunna förstå hur och när du ska använda målet [!DNL Mailchimp Tags] finns det ett exempel på användning som Adobe Experience Platform-kunder kan lösa genom att använda det här målet.

### Skicka e-post till kontakter för marknadsföringskampanjer {#use-case-send-emails}

Försäljningsavdelningen i en organisation vill sända en e-postbaserad marknadsföringskampanj till en välstrukturerad lista med kontakter. Kontaktlistorna tas emot i grupper från olika offlinekällor och måste därför spåras. Teamet identifierar en befintlig [!DNL Mailchimp]-målgrupp och börjar bygga upp de Experience Platform-målgrupper i vilka kontakterna från varje lista läggs till. När du har skickat dessa målgrupper till [!DNL Mailchimp Tags], och om det inte finns några kontakter i den valda [!DNL Mailchimp]-målgruppen, läggs de till med en associerad tagg som innehåller det målgruppsnamn som kontakten tillhör. Om det redan finns kontakter i målgruppen [!DNL Mailchimp] läggs en ny tagg med målgruppens namn till. Eftersom etiketterna är synliga i [!DNL Mailchimp] går det lätt att identifiera offlinekällorna. När data har skickats över till [!DNL Mailchimp] skickar de marknadsföringskampanjens e-post till målgruppen.

## Förhandskrav {#prerequisites}

I avsnitten nedan finns information om eventuella krav som du måste konfigurera i Experience Platform och [!DNL Mailchimp]. Här finns även information som du måste samla in innan du kan arbeta med målet för [!DNL Mailchimp Tags].

### Förutsättningar i Experience Platform {#prerequisites-in-experience-platform}

Innan du aktiverar data till målet [!DNL Mailchimp Tags] måste du ha ett [schema](/help/xdm/schema/composition.md), en [datamängd](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=en) och [målgrupper](https://experienceleague.adobe.com/docs/platform-learn/tutorials/audiences/create-audiences.html) som skapats i [!DNL Experience Platform].

### Krav för målet [!DNL Mailchimp Tags] {#prerequisites-destination}

Observera följande krav för att kunna exportera data från Experience Platform till ditt [!DNL Mailchimp Tags]-konto:

#### Du måste ha ett [!DNL Mailchimp]-konto {#prerequisites-account}

Innan du kan skapa ett [!DNL Mailchimp Tags]-mål måste du se till att du har ett [!DNL Mailchimp]-konto. Om du inte redan har någon går du till [[!DNL Mailchimp] registreringssidan](https://login.mailchimp.com/signup/) och registrerar och skapar ditt konto.

#### Samla in [!DNL Mailchimp] API-nyckel {#gather-credentials}

Du behöver din [!DNL Mailchimp] **API-nyckel** för att autentisera [!DNL Mailchimp Interest Categories]-målet mot ditt [!DNL Mailchimp]-konto. **API-nyckeln** fungerar som **Lösenord** när du [autentiserar målet](#authenticate).

Om du inte har din **API-nyckel** loggar du in på ditt [!DNL Mailchimp]-konto och läser [!DNL Mailchimp] -dokumentationen om [hur du genererar API-nyckeln](https://mailchimp.com/developer/marketing/guides/quick-start/#generate-your-api-key).

Ett exempel på en API-nyckel är `0123456789abcdef0123456789abcde-us14`.

>[!IMPORTANT]
>
>Om du genererar **API-nyckeln** skriver du ned den eftersom du inte kommer att kunna komma åt den efter genereringen.

#### Identifiera ditt [!DNL Mailchimp]-datacenter {#identify-data-center}

Därefter måste du identifiera ditt [!DNL Mailchimp]-datacenter. Det gör du genom att logga in på ditt [!DNL Mailchimp]-konto och navigera till avsnittet **API-nycklar** för ditt konto.

Datacenter-ID är det första avsnittet i URL:en som du ser i webbläsaren. Om URL:en är *https://`us14`.mailchimp.com/account/api/* är datacentret `us14`.

Datacenter-ID:t läggs också till i API-nyckeln i formatet *key-dc*. Om din API-nyckel till exempel är `0123456789abcdef0123456789abcde-us14` är datacentret `us14`.

Skriv ned datacentervärdet *(`us14` i det här exemplet)*. Du behöver det här värdet när du [fyller i målinformationen](#destination-details).

Om du behöver mer hjälp kan du läsa [[!DNL Mailchimp] Grundläggande dokumentation](https://mailchimp.com/developer/marketing/docs/fundamentals/#api-structure).

### Guardrails {#guardrails}

Se [!DNL Mailchimp] [hastighetsgränserna](https://mailchimp.com/developer/marketing/docs/fundamentals/#api-limits) för detaljerad information om de begränsningar som gäller för API:t [!DNL Mailchimp].

## Identiteter som stöds {#supported-identities}

[!DNL Mailchimp] stöder aktivering av identiteter som beskrivs i tabellen nedan. Läs mer om [identiteter](/help/identity-service/features/namespaces.md).

| Målidentitet | Beskrivning | Överväganden |
|---|---|---|
| E-post | Kontaktens e-postadress. | Obligatoriskt |

{style="table-layout:auto"}

## Målgrupper {#supported-audiences}

I det här avsnittet beskrivs vilken typ av målgrupper du kan exportera till det här målet.

| Målgruppsursprung | Stöds | Beskrivning |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Publiker som genererats via Experience Platform [segmenteringstjänst](../../../segmentation/home.md). |
| Anpassade överföringar | ✓ | Publikerna [importerade](../../../segmentation/ui/audience-portal.md#import-audience) till Experience Platform från CSV-filer. |

{style="table-layout:auto"}

## Exportera typ och frekvens {#export-type-frequency}

Se tabellen nedan för information om exporttyp och frekvens för destinationen.

| Objekt | Typ | Anteckningar |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Profile-based]** | <ul><li>Du exporterar alla medlemmar i en målgrupp tillsammans med de önskade schemafälten *(till exempel e-postadress, telefonnummer, efternamn)*, enligt fältmappningen.</li><li> För varje målgrupp som valts i Experience Platform uppdateras motsvarande [!DNL Mailchimp Tags]-segmentstatus med målgruppsstatus från Experience Platform.</li></ul> |
| Exportfrekvens | **[!UICONTROL Streaming]** | Direktuppspelningsmål är alltid på API-baserade anslutningar. Så snart en profil uppdateras i Experience Platform baserat på målgruppsutvärdering skickar anslutningsprogrammet uppdateringen nedströms till målplattformen. Läs mer om [direktuppspelningsmål](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Anslut till målet {#connect}

>[!IMPORTANT]
>
>Om du vill ansluta till målet måste du ha **[!UICONTROL Manage Destinations]** [åtkomstkontrollbehörighet](/help/access-control/home.md#permissions). Läs [åtkomstkontrollsöversikten](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få den behörighet som krävs.

Om du vill ansluta till det här målet följer du stegen som beskrivs i självstudiekursen [för destinationskonfiguration](../../ui/connect-destination.md). I arbetsflödet för att konfigurera mål fyller du i fälten som listas i de två avsnitten nedan.

Sök efter [!DNL Mailchimp Tags] inom **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]**. Du kan också hitta den under kategorin **[!UICONTROL Email marketing]**.

### Autentisera till mål {#authenticate}

Om du vill autentisera mot målet fyller du i de obligatoriska fälten nedan och väljer **[!UICONTROL Connect to destination]**.

| Fält | Beskrivning |
| --- | --- |
| **[!UICONTROL Username]** | Ditt [!DNL Mailchimp]-användarnamn. |
| **[!UICONTROL Password]** | Din [!DNL Mailchimp] **API-nyckel**, som du har noterat i avsnittet [Samla [!DNL Mailchimp] inloggningsuppgifter](#gather-credentials).<br> Din API-nyckel har formen av `{KEY}-{DC}`, där delen `{KEY}` refererar till det värde som anges i avsnittet [[!DNL Mailchimp]  API-nyckel ](#gather-credentials) och delen `{DC}` refererar till [[!DNL Mailchimp] datacenter](#identify-data-center). <br>Du kan antingen ange delen `{KEY}` eller hela formuläret.<br> Om din API-nyckel till exempel är <br>*`0123456789abcdef0123456789abcde-us14`*<br> kan du ange antingen *`0123456789abcdef0123456789abcde`*eller *`0123456789abcdef0123456789abcde-us14`*som värde. |

{style="table-layout:auto"}

![Experience Platform UI, bild som visar hur du autentiserar.](../../assets/catalog/email-marketing/mailchimp-tags/authenticate-destination.png)

Om den angivna informationen är giltig visas statusen **[!UICONTROL Connected]** med en grön bockmarkering. Du kan sedan gå vidare till nästa steg.

### Fyll i målinformation {#destination-details}

Om du vill konfigurera information för målet fyller du i de obligatoriska och valfria fälten nedan. En asterisk bredvid ett fält i användargränssnittet anger att fältet är obligatoriskt.

![Experience Platform UI-skärmbild med målinformation.](../../assets/catalog/email-marketing/mailchimp-tags/destination-details.png)

| Fält | Beskrivning |
| --- | --- |
| **[!UICONTROL Name]** | Ett namn som du känner igen det här målet med i framtiden. |
| **[!UICONTROL Description]** | En beskrivning som hjälper dig att identifiera det här målet i framtiden. |
| **[!UICONTROL Data center]** | Ditt [!DNL Mailchimp]-konto `data center`. Mer information finns i avsnittet [Identifiera [!DNL Mailchimp] datacenter](#identify-data-center). |
| **[!UICONTROL Audience Name (Please enter Data center first)]** | När du har angett **[!UICONTROL Data center]** fylls den här listrutan automatiskt i med målgruppsnamnen från ditt [!DNL Mailchimp]-konto. Välj den målgrupp som du vill uppdatera med data från Experience Platform. |

{style="table-layout:auto"}

### Aktivera aviseringar {#enable-alerts}

Du kan aktivera varningar för att få meddelanden om dataflödets status till ditt mål. Välj en avisering i listan om du vill prenumerera och få meddelanden om statusen för ditt dataflöde. Mer information om varningar finns i guiden [prenumerera på destinationsvarningar med användargränssnittet](../../ui/alerts.md).

Välj **[!UICONTROL Next]** när du är klar med att ange information för målanslutningen.

## Aktivera målgrupper till det här målet {#activate}

>[!IMPORTANT]
> 
>* För att aktivera data behöver du behörigheterna **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** och **[!UICONTROL View Segments]** [åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontrollsöversikten](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få den behörighet som krävs.
>* Om du vill exportera *identiteter* måste du ha **[!UICONTROL View Identity Graph]** [åtkomstkontrollbehörighet](/help/access-control/home.md#permissions). <br> ![Markera identitetsnamnområdet som är markerat i arbetsflödet för att aktivera målgrupper till mål.](/help/destinations/assets/overview/export-identities-to-destination.png "Markera identitetsnamnområdet som är markerat i arbetsflödet för att aktivera målgrupper till mål."){width="100" zoomable="yes"}

Läs [Aktivera målgrupper till direktuppspelningsmål](/help/destinations/ui/activate-segment-streaming-destinations.md) om du vill ha instruktioner om hur du aktiverar målgrupper till det här målet.

### Mappa överväganden och exempel {#mapping-considerations-example}

Om du vill skicka målgruppsdata från Adobe Experience Platform till målet [!DNL Mailchimp Tags] måste du gå igenom fältmappningssteget. Mappningen består av att skapa en länk mellan XDM-schemafälten (Experience Data Model) i ditt Experience Platform-konto och deras motsvarande motsvarigheter från målmålet.

Följ stegen nedan för att mappa dina XDM-fält korrekt till målfälten för [!DNL Mailchimp Tags]:

1. Välj **[!UICONTROL Add new mapping]** i steget **[!UICONTROL Mapping]**. En ny mappningsrad visas på skärmen.
1. I fönstret **[!UICONTROL Select source field]** väljer du **[!UICONTROL Select identity namespace]** och sedan identitetsnamnutrymmet `Email`.

   ![Experience Platform UI-skärmbild med Source-fält som e-post från identitetsnamnområdet.](../../assets/catalog/email-marketing/mailchimp-tags/source-field.png)

1. I fönstret **[!UICONTROL Select target field]** väljer du **[!UICONTROL Select identity namespace]** och sedan identitetsnamnutrymmet `Email`.

   ![Experience Platform UI-skärmbild med målfält som e-post från identitetsnamnområdet.](../../assets/catalog/email-marketing/mailchimp-tags/target-field.png)

   Mappningarna mellan ditt XDM-profilschema och [!DNL Mailchimp Tags] visas nedan:

   | Source Field | Målfält | Obligatoriskt |
   | --- | --- | --- |
   | `IdentityMap: Email` | `Identity: Email` | Ja |

   Ett exempel med de slutförda mappningarna visas nedan:
   ![Exempel på skärmbild i Experience Platform UI som visar fältkopplingar.](../../assets/catalog/email-marketing/mailchimp-tags/mappings.png)

När du har angett mappningarna för målanslutningen väljer du **[!UICONTROL Next]**.

## Validera dataexport {#exported-data}

Följ stegen nedan för att verifiera att du har konfigurerat målet korrekt:

1. Logga in på ditt [[!DNL Mailchimp]](https://login.mailchimp.com/)-konto. Gå sedan till sidan **[!DNL Audience]** > **[!DNL All Contacts]** och kontrollera om kontakterna från målgruppen har lagts till och om kontakterna inom målgruppen har uppdaterats med målgruppens namn.
   ![Skärmbild för Mailchimp-användargränssnitt som visar målsidan.](../../assets/catalog/email-marketing/mailchimp-tags/contacts.png)

## Dataanvändning och styrning {#data-usage-governance}

Alla [!DNL Adobe Experience Platform]-mål är kompatibla med dataanvändningsprinciper när data hanteras. Mer information om hur [!DNL Adobe Experience Platform] använder datastyrning finns i [Datastyrningsöversikten](/help/data-governance/home.md).

## Fel och felsökning {#errors-and-troubleshooting}

På sidan [[!DNL Mailchimp] errors](https://mailchimp.com/developer/marketing/docs/errors/) finns en omfattande lista över status- och felkoder med förklaringar.

## Ytterligare resurser {#additional-resources}

Ytterligare användbar information från dokumentationen för [!DNL Mailchimp] finns nedan:
* [Komma igång med [!DNL Mailchimp]](https://mailchimp.com/help/getting-started-with-mailchimp/)
* [Komma igång med målgrupper](https://mailchimp.com/help/getting-started-audience/)
* [Skapa en publik](https://mailchimp.com/help/create-audience/)
* [Komma igång med taggar](https://mailchimp.com/help/getting-started-tags/)
* [Marknadsförings-API](https://mailchimp.com/developer/marketing/api/)
