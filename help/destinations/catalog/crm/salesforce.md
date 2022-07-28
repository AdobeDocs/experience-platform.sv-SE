---
keywords: crm;CRM;crm destination;salesforce crm;salesforce crm destination
title: Salesforce CRM-anslutning
description: Med Salesforce CRM-destinationen kan du exportera dina kontodata och aktivera dem i Salesforce CRM för dina affärsbehov.
source-git-commit: 154cca31c5b434a2f036773ef9cda088f84eb1e5
workflow-type: tm+mt
source-wordcount: '1674'
ht-degree: 1%

---


# [!DNL Salesforce CRM] anslutning

## Översikt {#overview}

[Salesforce CRM](https://www.salesforce.com/) är en populär CRM-plattform (Customer Relationship Management).

Detta [!DNL Adobe Experience Platform] [mål](/help/destinations/home.md) utnyttjar [Salesforce REST API](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/dome_composite_upsert_example.htm?q=contacts), som gör att du kan uppdatera identiteter inom ett segment till Salesforce CRM.

Salesforce CRM använder OAuth 2 med lösenordsbeviljande som autentiseringsmekanism för att kommunicera med Salesforce REST API. Instruktioner för autentisering till din Salesforce CRM-instans finns längre ned i [Autentisera till mål](#authenticate) -avsnitt.

## Användningsfall {#use-cases}

Som marknadsförare kan ni leverera personaliserade upplevelser till era användare, baserat på attribut från deras Adobe Experience Platform-profiler. Du kan skapa segment utifrån dina offlinedata och skicka dessa segment till Salesforce CRM som visas i användarens flöden så snart segment och profiler uppdateras i Adobe Experience Platform.

## Förutsättningar {#prerequisites}

### Förutsättningar i Experience Platform {#prerequisites-in-experience-platform}

Innan du aktiverar data till Salesforce CRM-målet måste du ha en [schema](/help/xdm/schema/composition.md), a [datauppsättning](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=en)och [segment](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=en) skapad i [!DNL Experience Platform].

### Förutsättningar i Salesforce CRM {#prerequisites-destination}

Observera följande krav i Salesforce för att kunna exportera data från Platform till ditt Salesforce-konto:

#### Du måste ha ett Salesforce-konto {#prerequisites-account}

Gå till Salesforce [testversion](https://www.salesforce.com/in/form/signup/freetrial-sales/) om du vill registrera och skapa ett Salesforce-konto, om du inte redan har ett.

#### Konfigurera en ansluten app {#prerequisites-connected-app}

Sedan måste du konfigurera en [ansluten app](https://help.salesforce.com/s/articleView?id=sf.connected_app_create.htm&amp;language=en_US&amp;r=https%3A%2F%2Fhelp.salesforce.com%2F&amp;type=5) i Salesforce-kontot, om du inte redan har ett.

I den anslutna appen ser du till att [OAuth-inställningar](https://help.salesforce.com/s/articleView?id=connected_app_create_api_integration.htm&amp;type=5&amp;language=en_US) är aktiverat.

Se även till att [scope](https://help.salesforce.com/s/articleView?id=connected_app_create_api_integration.htm&amp;type=5&amp;language=en_US) som nämns nedan är markerade.

* ``chatter_api``
* ``lightning``
* ``visualforce``
* ``content``
* ``openid``
* ``full``
* ``api``
* ``web``
* ``refresh_token``
* ``offline_access``

#### Skapa anpassat fält i Salesforce {#prerequisites-custom-field}

Skapa ett anpassat typfält `Text Area Long` vilken Experience Platform som ska använda för att uppdatera segmentstatusen i Salesforce CRM.
Läs Salesforce-dokumentationen för att [skapa anpassade fält](https://help.salesforce.com/s/articleView?id=sf.adding_fields.htm&amp;type=5) om du behöver ytterligare vägledning.

>[!IMPORTANT]
>
> Kontrollera att det inte finns några blankstegstecken i fältnamnet. Använd i stället understrecket `(_)` tecken som avgränsare.

>[!NOTE]
>
> * Objekt i Salesforce är begränsade till 25 externa fält, se [Anpassade fältattribut](https://help.salesforce.com/s/articleView?id=sf.custom_field_attributes.htm&amp;type=5).
> * Den här begränsningen innebär att du endast kan ha 25 Experience Platform-medlemskap som är aktiva när som helst.
> * Om du har nått denna gräns i Salesforce måste du ta bort det anpassade attributet från Salesforce som användes för att lagra segmentstatusen mot äldre segment i Experience Platform innan ett nytt mappnings-ID kan användas.


Läs Adobe Experience Platform-dokumentationen för [Schemafältgrupp för detaljer om segmentmedlemskap](/help/xdm/field-groups/profile/segmentation.md) om du behöver vägledning om segmentstatus.

#### Samla in Salesforce-inloggningsuppgifter {#gather-credentials}

Observera objekten nedan innan du autentiserar till Salesforce CRM-målet:

| Autentiseringsuppgifter | Beskrivning | Exempel |
| --- | --- | --- |
| <ul><li>Salesforce-domänprefix</li></ul> | Se [Salesforce-domänprefix](https://help.salesforce.com/s/articleView?id=sf.domain_name_setting_login_policy.htm&amp;type=5) för ytterligare vägledning. | <ul><li>Om din domän är som nedan behöver du det markerade värdet.<br> <i>`d5i000000isb4eak-dev-ed`.my.salesforce.com</i></li></ul> |
| <ul><li>Konsumentnyckel</li><li>Konsumenthemlighet</li></ul> | Se [Salesforce-dokumentation](https://help.salesforce.com/s/articleView?id=sf.connected_app_rotate_consumer_details.htm&amp;type=5) om du behöver ytterligare vägledning. | <ul><li>r23kxxxxxx0z05xxxx</li><li>ipxxxxxxxxxxT4xxxxxxxx</li></ul> |

## Identiteter som stöds {#supported-identities}

Salesforce CRM har stöd för uppdatering av identiteter som beskrivs i tabellen nedan. Läs mer om [identiteter](/help/identity-service/namespaces.md).

| Målidentitet | Beskrivning | Överväganden |
|---|---|---|
| SalesforceId | Anpassad Salesforce CRM-identifierare som stöder mappning av alla identiteter. | Obligatoriskt. Du kan skicka alla [identity](../../../identity-service/namespaces.md) till [!DNL Salesforce CRM] mål, förutsatt att du mappar det till `SalesforceId`. |

## Exportera typ och frekvens {#export-type-frequency}

Se tabellen nedan för information om exporttyp och frekvens för destinationen.

| Objekt | Typ | Anteckningar |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Profile-based]** | <ul><li>Du exporterar alla medlemmar i ett segment tillsammans med de önskade schemafälten *(till exempel: e-postadress, telefonnummer, efternamn)*, enligt fältmappningen.</li><li> Status för plattformssegment exporteras till [!DNL Salesforce CRM] genom att ange deras motsvarande anpassade fältattribut i [!DNL Salesforce CRM] i **[!UICONTROL Activate Destination]** > **[!UICONTROL Schedule segment export]** > **[!UICONTROL Mapping ID]** fält.</li></ul> |
| Exportfrekvens | **[!UICONTROL Streaming]** | <ul><li>Direktuppspelningsmål är alltid på API-baserade anslutningar. Så snart en profil uppdateras i Experience Platform baserat på segmentutvärdering skickar kopplingen uppdateringen nedåt till målplattformen. Läs mer om [mål för direktuppspelning](/help/destinations/destination-types.md#streaming-destinations).</li></ul> |

{style=&quot;table-layout:auto&quot;}

## Anslut till målet {#connect}

>[!IMPORTANT]
> 
>Om du vill ansluta till målet behöver du **[!UICONTROL Manage Destinations]** [åtkomstkontrollbehörighet](/help/access-control/home.md#permissions). Läs [åtkomstkontroll - översikt](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få de behörigheter som krävs.

Om du vill ansluta till det här målet följer du stegen som beskrivs i [självstudiekurs om destinationskonfiguration](../../ui/connect-destination.md). I arbetsflödet för att konfigurera mål fyller du i fälten som listas i de två avsnitten nedan.

![Katalog](../../assets/catalog/crm/salesforce/catalog.png)

### Autentisera till mål {#authenticate}

Om du vill autentisera mot målet fyller du i de obligatoriska fälten och väljer **[!UICONTROL Connect to destination]**.

![Exempelbild som visar hur du autentiserar till Salesforce CRM](../../assets/catalog/crm/salesforce/authenticate-destination.png)

* **[!UICONTROL Password]**: Lösenordet för ditt Salesforce-konto.
* **[!UICONTROL Client ID]**: Din Salesforce-anslutna app konsumentnyckel.
* **[!UICONTROL Client Secret]**: Din Salesforce-anslutna app, hemlighet.
* **[!UICONTROL Username]**: Ditt Salesforce-användarnamn.

Om den angivna informationen är giltig visas en **Ansluten** status med en grön bockmarkering kan du fortsätta till nästa steg.

### Fyll i målinformation {#destination-details}

Om du vill konfigurera information för målet fyller du i de obligatoriska och valfria fälten nedan. En asterisk bredvid ett fält i användargränssnittet anger att fältet är obligatoriskt.
![Exempelbild som visar hur du fyller i detaljer för Salesforce CRM](../../assets/catalog/crm/salesforce/destination-details.png)

* **[!UICONTROL Name]**: Ett namn som du känner igen det här målet med i framtiden.
* **[!UICONTROL Description]**: En beskrivning som hjälper dig att identifiera det här målet i framtiden.
* **[!UICONTROL Custom Domain]**: Din Salesforce-domän.

### Aktivera aviseringar {#enable-alerts}

Du kan aktivera varningar för att få meddelanden om dataflödets status till ditt mål. Välj en avisering i listan om du vill prenumerera och få meddelanden om status för ditt dataflöde. Mer information om varningar finns i guiden [prenumerera på destinationsvarningar med hjälp av användargränssnittet](../../ui/alerts.md).

När du är klar med informationen för målanslutningen väljer du **[!UICONTROL Next]**.

## Aktivera segment till den här destinationen {#activate}

>[!IMPORTANT]
> 
>Om du vill aktivera data måste du ha **[!UICONTROL Manage Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** och **[!UICONTROL View Segments]** [behörigheter för åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontroll - översikt](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få de behörigheter som krävs.

Läs [Aktivera profiler och segment för att direktuppspela segmentexportmål](/help/destinations/ui/activate-segment-streaming-destinations.md) om du vill ha instruktioner om hur du aktiverar målgruppssegment till det här målet.

### Mappa överväganden och exempel {#mapping-considerations-example}

Om du vill skicka målgruppsdata från Adobe Experience Platform till Salesforce CRM-målet på rätt sätt måste du gå igenom fältmappningssteget. Mappningen består av att skapa en länk mellan XDM-schemafälten (Experience Data Model) i ditt plattformskonto och motsvarande motsvarigheter från målmålet. Följ de här stegen för att mappa dina XDM-fält till målfälten i Salesforce CRM:

1. Klicka på i mappningssteget **[!UICONTROL Add new mapping]** visas en ny mappningsrad på skärmen.

   ![Lägg till ny mappning](../../assets/catalog/crm/salesforce/add-new-mapping.png)

1. När du markerar källfältet i fönstret Välj källfält **[!UICONTROL Select attributes]** och lägg till mappningarna.

   ![Källmappning](../../assets/catalog/crm/salesforce/source-mapping.png)

1. Markera målfältet och välj **[!UICONTROL Select identity namespace]** och lägg till mappningarna.

   ![Målmappning med SalesforceId](../../assets/catalog/crm/salesforce/target-mapping-salesforceid.png)

1. För anpassade attribut väljer du målfältet i fönstret för att välja målfält och väljer **[!UICONTROL Select custom attributes]** -kategorin anger du sedan det önskade målattributnamnet och lägger till de önskade mappningarna.

   ![Målmappning med LastName](../../assets/catalog/crm/salesforce/target-mapping-lastname.png)

1. Du kan till exempel lägga till följande mappning mellan XDM-profilschemat och [!DNL Salesforce CRM] instans:

   |  | XDM-profilschema | [!DNL Salesforce CRM] Instans | Obligatoriskt |
   |---|---|---|---|
   | Attribut | <ul><li>person.name.firstName</code></li><li>person.name.lastName</code></li><li>personalEmail.address</code></li></ul> | <ul><li>FirstName</code></li><li>LastName</code></li><li>E-post</code></li></ul> |
   | Identiteter | <ul><li>crmID</code></li></ul> | <ul><li>SalesforceId</code></li></ul> | Ja |

1. Ett exempel på hur du använder dessa mappningar visas nedan:

   ![Målkartläggning](../../assets/catalog/crm/salesforce/mappings.png)

### Schemalägg segmentexport och exempel {#schedule-segment-export-example}

När du utför [Schemalägg segmentexport](/help/destinations/ui/activate-segment-streaming-destinations.md#scheduling) steg du måste manuellt mappa plattformssegment till det anpassade fältattributet i Salesforce.

Det gör du genom att markera varje segment och sedan ange motsvarande attribut för anpassade fält i Salesforce i dialogrutan **[!UICONTROL Mapping ID]** fält.

>[!IMPORTANT]
>
>* Värdet som används för **[!UICONTROL Mapping ID]** ska matcha namnet på det anpassade fältattributet som skapats i Salesforce.
>* Kontrollera att namnet på det anpassade fältattributet som du har skapat i Salesforce inte använder blankstegstecknet.


Ett exempel visas nedan:
![Schemalägg segmentexport](../../assets/catalog/crm/salesforce/schedule-segment-export.png)

## Validera dataexport {#exported-data}

Följ stegen nedan för att verifiera att du har konfigurerat målet korrekt:

1. Välj **[!UICONTROL Destinations]** > **[!UICONTROL Browse]** för att navigera till listan över destinationer.
   ![Bläddra bland mål](../../assets/catalog/crm/salesforce/browse-destinations.png)

1. Markera målet och validera att statusen är **[!UICONTROL enabled]**.
   ![Körning av måldataflöde](../../assets/catalog/crm/salesforce/destination-dataflow-run.png)

1. Växla till **[!DNL Activation data]** väljer du ett segmentnamn.
   ![Aktiveringsdata för destinationer](../../assets/catalog/crm/salesforce/destinations-activation-data.png)

1. Övervaka segmentsammanfattningen och se till att antalet profiler motsvarar antalet som skapas i segmentet.
   ![Segment](../../assets/catalog/crm/salesforce/segment.png)

1. Logga in på Salesforce-webbplatsen och navigera sedan till **[!DNL Apps]** > **[!DNL Contacts]** och kontrollera om profilerna från segmentet har lagts till.
   ![Salesforce-kontakter](../../assets/catalog/crm/salesforce/contacts.png)

1. Klicka på en kontakt och kontrollera om fälten har uppdaterats. Du kommer att märka att segmentstatusen från Experience Platform har uppdaterats mot motsvarande anpassade fältattribut som fanns i **Mappnings-ID** fältet under **[!UICONTROL Activate destination]** > **[!UICONTROL Schedule segment export]** steg.
   ![Salesforce-kontakter](../../assets/catalog/crm/salesforce/contact-info.png)

## Dataanvändning och styrning {#data-usage-governance}

Alla [!DNL Adobe Experience Platform] destinationerna är kompatibla med dataanvändningsprinciper när data hanteras. Detaljerad information om hur [!DNL Adobe Experience Platform] använder datastyrning, se [Datastyrning - översikt](/help/data-governance/home.md).

## Fel och felsökning {#errors-and-troubleshooting}

### Okända fel påträffades när händelser skickades till målet {#unknown-errors}

Om felmeddelandet nedan visas när du kontrollerar ett dataflöde kontrollerar du att det mappnings-ID som du angav i [!DNL Salesforce CRM] för ditt plattformssegment är giltigt och finns inom [!DNL Salesforce CRM].
![Fel](../../assets/catalog/crm/salesforce/error.png)

## Ytterligare resurser {#additional-resources}

Ytterligare användbar information från [Salesforce-utvecklarportal](https://developer.salesforce.com/) är under:
* [Skapa en post](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/dome_sobject_create.htm)
* [Anpassade rekommendationsmålgrupper](https://developer.salesforce.com/docs/atlas.en-us.236.0.chatterapi.meta/chatterapi/connect_resources_recommendation_audiences_list.htm)
* [Använda sammansatta resurser](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/using_composite_resources.htm?q=composite)
* [Snabbstart](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/quickstart.htm)

### Gränser {#limits}

Salesforce balanserar transaktionsbelastningar genom att införa begränsningar för antal begäranden, frekvens och tidsgräns. Se [API-begärandegränser och allokeringar](https://developer.salesforce.com/docs/atlas.en-us.salesforce_app_limits_cheatsheet.meta/salesforce_app_limits_cheatsheet/salesforce_app_limits_platform_api.htm) för mer information.