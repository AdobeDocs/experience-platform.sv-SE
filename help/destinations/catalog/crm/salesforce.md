---
keywords: crm;CRM;crm destination;salesforce crm;salesforce crm destination
title: Salesforce CRM-anslutning
description: Med Salesforce CRM-destinationen kan du exportera dina kontodata och aktivera dem i Salesforce CRM för dina affärsbehov.
exl-id: bd9cb656-d742-4a18-97a2-546d4056d093
source-git-commit: ba39f62cd77acedb7bfc0081dbb5f59906c9b287
workflow-type: tm+mt
source-wordcount: '2712'
ht-degree: 0%

---

# [!DNL Salesforce CRM]-anslutning

## Översikt {#overview}

[[!DNL Salesforce CRM]](https://www.salesforce.com/crm/) är en populär CRM-plattform (Customer Relationship Management) och stöder profiltyperna som beskrivs nedan:

* [Leads](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_objects_lead.htm) - Ett lead är namnet på en person eller ett företag som kan (eller inte) vara intresserad av de produkter eller tjänster som du säljer.
* [Kontakter](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_objects_contact.htm) - En kontakt är en person med vilken en av dina representanter har upprättat en relation och har kvalificerats som en potentiell kund.

Det här [!DNL Adobe Experience Platform] [målet](/help/destinations/home.md) använder [[!DNL Salesforce composite API]](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/resources_composite_sobjects_collections_update.htm), som har stöd för båda profiltyperna som beskrivs ovan.

När du [aktiverar segment](#activate) kan du välja mellan leads eller kontakter och uppdatera attribut och målgruppsdata till [!DNL Salesforce CRM].

[!DNL Salesforce CRM] använder OAuth 2 med lösenordsbeviljande som autentiseringsmekanism för att kommunicera med Salesforce REST API. Instruktioner för autentisering till din [!DNL Salesforce CRM]-instans finns längre ned i avsnittet [Autentisera till mål](#authenticate).

## Användningsfall {#use-cases}

Som marknadsförare kan ni leverera personaliserade upplevelser till era användare, baserat på attribut från deras Adobe Experience Platform-profiler. Du kan bygga målgrupper utifrån dina offlinedata och skicka dessa målgrupper till Salesforce CRM för att uppdatera CRM-medlemskapet så snart som målgrupper och profiler uppdateras i Adobe Experience Platform.

## Förhandskrav {#prerequisites}

### Förutsättningar i Experience Platform {#prerequisites-in-experience-platform}

Innan du aktiverar data till Salesforce CRM-målet måste du ha ett [schema](/help/xdm/schema/composition.md), en [datamängd](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html) och [segment](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html) som skapats i [!DNL Experience Platform].

### Förutsättningar i [!DNL Salesforce CRM] {#prerequisites-destination}

Observera följande krav i [!DNL Salesforce CRM] för att kunna exportera data från plattformen till ditt Salesforce-konto:

#### Du måste ha ett [!DNL Salesforce]-konto {#prerequisites-account}

Gå till sidan [!DNL Salesforce] [utvärderingsversion](https://www.salesforce.com/in/form/signup/freetrial-sales/) om du vill registrera och skapa ett [!DNL Salesforce]-konto, om du inte redan har ett.

#### Konfigurera en ansluten app i [!DNL Salesforce] {#prerequisites-connected-app}

Först måste du konfigurera en [[!DNL Salesforce] ansluten app](https://help.salesforce.com/s/articleView?id=sf.connected_app_create.htm&amp;language=en_US&amp;r=https%3A%2F%2Fhelp.salesforce.com%2F&amp;type=5) i ditt [!DNL Salesforce]-konto, om du inte redan har en. [!DNL Salesforce CRM] utnyttjar den anslutna appen för att ansluta till [!DNL Salesforce].

Aktivera sedan [!DNL OAuth Settings for API Integration] för [!DNL Salesforce connected app]. Mer information finns i [[!DNL Salesforce]](https://help.salesforce.com/s/articleView?id=connected_app_create_api_integration.htm&amp;type=5&amp;language=en_US)-dokumentationen.

Se även till att de [omfattningar](https://help.salesforce.com/s/articleView?id=connected_app_create_api_integration.htm&amp;type=5&amp;language=en_US) som nämns nedan är markerade för [!DNL Salesforce connected app].

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

Kontrollera slutligen att `password`-anslaget är aktiverat i ditt [!DNL Salesforce]-konto. Om du behöver hjälp kan du läsa dokumentationen för [!DNL Salesforce] [OAuth 2.0-användarnamn-lösenord för särskilda scenarier](https://help.salesforce.com/s/articleView?id=sf.remoteaccess_oauth_username_password_flow.htm&amp;type=5) .

>[!IMPORTANT]
>
>Om din [!DNL Salesforce]-kontoadministratör har begränsat åtkomsten till betrodda IP-intervall måste du kontakta dem för att få [Experience Platform IP:ns](/help/destinations/catalog/streaming/ip-address-allow-list.md) tillåtslista. Mer information finns i dokumentationen för [!DNL Salesforce] [Begränsa åtkomst till betrodda IP-intervall för ett anslutet program](https://help.salesforce.com/s/articleView?id=sf.connected_app_edit_ip_ranges.htm&amp;type=5) om du behöver ytterligare hjälp.

#### Skapa anpassade fält i [!DNL Salesforce] {#prerequisites-custom-field}

När du aktiverar målgrupper till målet [!DNL Salesforce CRM] måste du ange ett värde i fältet **[!UICONTROL Mapping ID]** för varje aktiverad målgrupp i steget **[Målgruppsschema](#schedule-segment-export-example)**.

[!DNL Salesforce CRM] kräver det här värdet för att kunna läsa och tolka målgrupper som kommer från Experience Platform korrekt och för att uppdatera deras målgruppsstatus inom [!DNL Salesforce]. Se Experience Platform-dokumentationen för schemafältgruppen [Information om målgruppsmedlemskap](/help/xdm/field-groups/profile/segmentation.md) om du behöver vägledning om målgruppsstatus.

För varje målgrupp som du aktiverar från Platform till [!DNL Salesforce CRM] måste du skapa ett anpassat fält av typen `Text Area (Long)` i [!DNL Salesforce]. Du kan definiera längden på fälttecknen i valfri storlek mellan 256 och 131 072 tecken beroende på ditt företags behov. Mer information om anpassade fälttyper finns på dokumentationssidan [!DNL Salesforce] [Anpassade fälttyper](https://help.salesforce.com/s/articleView?id=sf.custom_field_types.htm&amp;type=5). Se även [!DNL Salesforce]-dokumentationen för att [skapa anpassade fält](https://help.salesforce.com/s/articleView?id=mc_cab_create_an_attribute.htm&amp;type=5&amp;language=en_US) om du behöver hjälp med att skapa fält.

>[!IMPORTANT]
>
>Ta inte med blankstegstecken i fältnamnet. Använd i stället understrecket `(_)` som avgränsare.
>Inom [!DNL Salesforce] måste du skapa anpassade fält med en **[!UICONTROL Field Name]** som exakt matchar värdet som anges i **[!UICONTROL Mapping ID]** för varje aktiverat plattformssegment. Skärmbilden nedan visar till exempel ett anpassat fält med namnet `crm_2_seg`. När du aktiverar en målgrupp på det här målet lägger du till `crm_2_seg` som **[!UICONTROL Mapping ID]** för att fylla målgrupper från Experience Platform i det här anpassade fältet.

Ett exempel på hur du skapar anpassade fält i [!DNL Salesforce], *Steg 1 - Välj datatyp* visas nedan:
![Salesforce-användargränssnitt som visar hur du skapar anpassade fält, steg 1 - Välj datatyp.](../../assets/catalog/crm/salesforce/create-salesforce-custom-field-step-1.png)

Ett exempel på hur du skapar anpassade fält i [!DNL Salesforce], *Steg 2 - Ange information för anpassade fält* visas nedan:
![Salesforce-användargränssnitt som visar hur du skapar anpassade fält, steg 2 - Ange information för anpassade fält.](../../assets/catalog/crm/salesforce/create-salesforce-custom-field-step-2.png)

>[!TIP]
>
>* Om du vill skilja mellan anpassade fält som används för plattformsmålgrupper och andra anpassade fält i [!DNL Salesforce] kan du inkludera ett identifierbart prefix eller suffix när du skapar det anpassade fältet. Använd till exempel `Adobe_test_segment` eller `test_segment_Adobe` i stället för `test_segment`
>* Om du redan har andra anpassade fält skapade i [!DNL Salesforce] kan du använda samma namn som plattformssegmentet för att enkelt identifiera målgruppen i [!DNL Salesforce].

>[!NOTE]
>
>* Objekt i Salesforce är begränsade till 25 externa fält, se [Anpassade fältattribut](https://help.salesforce.com/s/articleView?id=sf.custom_field_attributes.htm&amp;type=5).
>* Den här begränsningen innebär att du bara kan ha högst 25 medlemskap för Experience Platform som är aktiva när som helst.
>* Om du har nått den här gränsen i Salesforce måste du ta bort de anpassade attribut från Salesforce som användes för att lagra målgruppsstatusen mot äldre målgrupper inom Experience Platform innan en ny **[!UICONTROL Mapping ID]** kan användas.

#### Samla in inloggningsuppgifter för [!DNL Salesforce CRM] {#gather-credentials}

Observera objekten nedan innan du autentiserar till målet [!DNL Salesforce CRM]:

| Autentiseringsuppgifter | Beskrivning | Exempel |
| --- | --- | --- |
| `Username` | Användarnamn för ditt [!DNL Salesforce]-konto. | |
| `Password` | Lösenordet för ditt [!DNL Salesforce]-konto. | |
| `Security Token` | Din [!DNL Salesforce]-säkerhetstoken som du senare lägger till i slutet av ditt [!DNL Salesforce]-lösenord för att skapa en sammanfogad sträng som ska användas som **[!UICONTROL Password]** vid [autentisering till målet](#authenticate).<br> Läs [!DNL Salesforce]-dokumentationen för att [återställa din säkerhetstoken](https://help.salesforce.com/s/articleView?id=sf.user_security_token.htm&amp;type=5) och lär dig hur du återskapar den från [!DNL Salesforce]-gränssnittet om du inte har säkerhetstoken. |  |
| `Custom Domain` | Domänprefixet [!DNL Salesforce]. <br> Läs [[!DNL Salesforce] dokumentationen](https://help.salesforce.com/s/articleView?id=sf.domain_name_setting_login_policy.htm&amp;type=5) om du vill veta hur du hämtar det här värdet från gränssnittet [!DNL Salesforce]. | Om din [!DNL Salesforce]-domän är <br> *`d5i000000isb4eak-dev-ed`.my.salesforce.com*,<br> du behöver `d5i000000isb4eak-dev-ed` som värde. |
| `Client ID` | Din Salesforce `Consumer Key`. <br> Mer information om hur du hämtar det här värdet från gränssnittet [!DNL Salesforce] finns i [[!DNL Salesforce] dokumentationen](https://help.salesforce.com/s/articleView?id=sf.connected_app_rotate_consumer_details.htm&amp;type=5). | |
| `Client Secret` | Din Salesforce `Consumer Secret`. <br> Mer information om hur du hämtar det här värdet från gränssnittet [!DNL Salesforce] finns i [[!DNL Salesforce] dokumentationen](https://help.salesforce.com/s/articleView?id=sf.connected_app_rotate_consumer_details.htm&amp;type=5). | |

### Guardrails {#guardrails}

[!DNL Salesforce] balanserar transaktionsinläsningar genom att införa gräns för antal begäranden, frekvens och tidsgräns. Mer information finns i [API-begäransgränser och allokeringar](https://developer.salesforce.com/docs/atlas.en-us.salesforce_app_limits_cheatsheet.meta/salesforce_app_limits_cheatsheet/salesforce_app_limits_platform_api.htm).

Om din [!DNL Salesforce]-kontoadministratör har infört IP-begränsningar måste du lägga till [Experience Platform IP-adresser](/help/destinations/catalog/streaming/ip-address-allow-list.md) i [!DNL Salesforce]-kontonas betrodda IP-intervall. Mer information finns i dokumentationen för [!DNL Salesforce] [Begränsa åtkomst till betrodda IP-intervall för ett anslutet program](https://help.salesforce.com/s/articleView?id=sf.connected_app_edit_ip_ranges.htm&amp;type=5) om du behöver ytterligare hjälp.

>[!IMPORTANT]
>
>När du [aktiverar segment](#activate) måste du välja mellan typerna *Kontakt* eller *Lead*. Ni måste se till att era målgrupper har rätt datamappning beroende på vilken typ som valts.

## Identiteter som stöds {#supported-identities}

[!DNL Salesforce CRM] har stöd för uppdatering av identiteter som beskrivs i tabellen nedan. Läs mer om [identiteter](/help/identity-service/features/namespaces.md).

| Målidentitet | Beskrivning | Överväganden |
|---|---|---|
| `SalesforceId` | Identifieraren [!DNL Salesforce CRM] för de kontakt- eller lead-ID som du exporterar eller uppdaterar genom ditt segment. | Obligatoriskt |

## Exportera typ och frekvens {#export-type-frequency}

Se tabellen nedan för information om exporttyp och frekvens för destinationen.

| Objekt | Typ | Anteckningar |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Profile-based]** | <ul><li>Du exporterar alla medlemmar i ett segment, tillsammans med de önskade schemafälten *(till exempel e-postadress, telefonnummer, efternamn)*, enligt fältmappningen.</li><li> Varje målgruppsstatus i [!DNL Salesforce CRM] uppdateras med motsvarande målgruppsstatus från Platform, baserat på värdet **[!UICONTROL Mapping ID]** som tillhandahölls under steget [målgruppsplanering](#schedule-segment-export-example).</li></ul> |
| Exportfrekvens | **[!UICONTROL Streaming]** | <ul><li>Direktuppspelningsmål är alltid på API-baserade anslutningar. Så snart en profil uppdateras i Experience Platform baserat på målgruppsutvärdering skickar anslutningsprogrammet uppdateringen nedströms till målplattformen. Läs mer om [direktuppspelningsmål](/help/destinations/destination-types.md#streaming-destinations).</li></ul> |

{style="table-layout:auto"}

## Anslut till målet {#connect}

>[!IMPORTANT]
>
>Om du vill ansluta till målet behöver du behörigheterna **[!UICONTROL View Destinations]** och **[!UICONTROL Manage Destinations]** [åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontrollsöversikten](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få den behörighet som krävs.

Om du vill ansluta till det här målet följer du stegen som beskrivs i självstudiekursen [för destinationskonfiguration](../../ui/connect-destination.md). I arbetsflödet för att konfigurera mål fyller du i fälten som listas i de två avsnitten nedan.

I **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]** söker du efter [!DNL Salesforce CRM]. Du kan också hitta den under kategorin **[!UICONTROL CRM]**.

### Autentisera till mål {#authenticate}

Om du vill autentisera mot målet fyller du i de obligatoriska fälten nedan och väljer **[!UICONTROL Connect to destination]**. Mer information finns i avsnittet [Samla [!DNL Salesforce CRM] inloggningsuppgifter](#gather-credentials).
| Autentiseringsuppgifter | Beskrivning |
| — | — |
| **[!UICONTROL Username]** | Användarnamn för ditt [!DNL Salesforce] -konto. |
| **[!UICONTROL Password]** | En sammanfogad sträng som består av ditt [!DNL Salesforce]-kontolösenord som har lagts till med din [!DNL Salesforce] säkerhetstoken.<br>Det sammanfogade värdet har formen `{PASSWORD}{TOKEN}`.<br> Obs! Använd inga klammerparenteser eller mellanslag.<br>Om ditt [!DNL Salesforce] lösenord till exempel är `MyPa$$w0rd123` och [!DNL Salesforce] säkerhetstoken är `TOKEN12345....0000` är det sammanfogade värde som du kommer att använda i fältet **[!UICONTROL Password]** `MyPa$$w0rd123TOKEN12345....0000`. |
| **[!UICONTROL Custom Domain]** | Ditt [!DNL Salesforce] -domänprefix. <br>Om din domän till exempel är *`d5i000000isb4eak-dev-ed`.my.salesforce.com* måste du ange `d5i000000isb4eak-dev-ed` som värde. |
| **[!UICONTROL Client ID]** | Ditt [!DNL Salesforce] anslutna program `Consumer Key` . |
| **[!UICONTROL Client Secret]** | Ditt [!DNL Salesforce] anslutna program `Consumer Secret` . |

![Skärmbild av användargränssnittet för plattformen som visar hur du autentiserar.](../../assets/catalog/crm/salesforce/authenticate-destination.png)

Om den angivna informationen är giltig visar gränssnittet **[!UICONTROL Connected]**-status med en grön bockmarkering, och du kan sedan fortsätta till nästa steg.

### Fyll i målinformation {#destination-details}

Om du vill konfigurera information för målet fyller du i de obligatoriska och valfria fälten nedan. En asterisk bredvid ett fält i användargränssnittet anger att fältet är obligatoriskt.
* **[!UICONTROL Name]**: Ett namn som du känner igen det här målet med i framtiden.
* **[!UICONTROL Description]**: En beskrivning som hjälper dig att identifiera det här målet i framtiden.
* **[!UICONTROL Salesforce ID Type]**:
   * Välj **[!UICONTROL Contact]** om de identiteter som du vill exportera eller uppdatera är av typen *Kontakt*.
   * Välj **[!UICONTROL Lead]** om de identiteter som du vill exportera eller uppdatera är av typen *Lead*.

![Skärmbild för plattformsgränssnitt som visar målinformationen.](../../assets/catalog/crm/salesforce/destination-details.png)

### Aktivera aviseringar {#enable-alerts}

Du kan aktivera varningar för att få meddelanden om dataflödets status till ditt mål. Välj en avisering i listan om du vill prenumerera och få meddelanden om statusen för ditt dataflöde. Mer information om varningar finns i guiden [prenumerera på destinationsvarningar med användargränssnittet](../../ui/alerts.md).

Välj **[!UICONTROL Next]** när du är klar med att ange information för målanslutningen.

## Aktivera målgrupper till det här målet {#activate}

>[!IMPORTANT]
> 
>* För att aktivera data behöver du behörigheterna **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** och **[!UICONTROL View Segments]** [åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontrollsöversikten](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få den behörighet som krävs.
>* Om du vill exportera *identiteter* måste du ha **[!UICONTROL View Identity Graph]** [åtkomstkontrollbehörighet](/help/access-control/home.md#permissions). <br> ![Markera identitetsnamnområdet som är markerat i arbetsflödet för att aktivera målgrupper till mål.](/help/destinations/assets/overview/export-identities-to-destination.png "Markera identitetsnamnområdet som är markerat i arbetsflödet för att aktivera målgrupper till mål."){width="100" zoomable="yes"}

Läs [Aktivera profiler och målgrupper för att direktuppspela målgruppsexportdestinationer](/help/destinations/ui/activate-segment-streaming-destinations.md) för instruktioner om hur du aktiverar målgrupper till det här målet.

### Mappa överväganden och exempel {#mapping-considerations-example}

Om du vill skicka målgruppsdata från Adobe Experience Platform till målet [!DNL Salesforce CRM] måste du gå igenom fältmappningssteget. Mappningen består av att skapa en länk mellan XDM-schemafälten (Experience Data Model) i ditt plattformskonto och motsvarande motsvarigheter från målmålet.

Attribut som anges i **[!UICONTROL Target field]** ska namnges exakt så som beskrivs i tabellen för attributmappningar eftersom dessa attribut kommer att utgöra begärandetexten.

Attribut som anges i **[!UICONTROL Source field]** följer inte någon sådan begränsning. Du kan mappa den baserat på dina behov, men kontrollera att indata-formatet är giltigt enligt [[!DNL Salesforce] dokumentationen](https://help.salesforce.com/s/articleView?id=sf.custom_field_attributes.htm&amp;type=5). Om indata inte är giltiga kommer uppdateringsanropet till [!DNL Salesforce] att misslyckas och dina kontakter/leads kommer inte att uppdateras.

Följ de här stegen för att mappa dina XDM-fält korrekt till målfälten för [!DNL (API) Salesforce CRM]:

1. I steget **[!UICONTROL Mapping]** väljer du **[!UICONTROL Add new mapping]** så visas en ny mappningsrad på skärmen.
   ![Exempel på skärmbild för användargränssnittet för plattformen för Lägg till ny mappning.](../../assets/catalog/crm/salesforce/add-new-mapping.png)
1. Välj kategorin **[!UICONTROL Select attributes]** i fönstret **[!UICONTROL Select source field]** och markera XDM-attributet eller välj **[!UICONTROL Select identity namespace]** och välj en identitet.
1. I fönstret **[!UICONTROL Select target field]** väljer du **[!UICONTROL Select identity namespace]** och sedan en identitet eller väljer **[!UICONTROL Select custom attributes]**-kategori och väljer ett attribut eller definierar ett med hjälp av fältet **[!UICONTROL Attribute name]** efter behov. Mer information om attribut som stöds finns i [[!DNL Salesforce CRM] dokumentationen](https://help.salesforce.com/s/articleView?id=sf.custom_field_attributes.htm&amp;type=5).
   * Upprepa de här stegen för att lägga till följande mappningar mellan XDM-profilschemat och [!DNL (API) Salesforce CRM]:

   **Arbeta med kontakter**

   * Om du arbetar med *Kontakter* i ditt segment kan du definiera mappningar för de fält som ska uppdateras genom att läsa objektreferensen i Salesforce för [kontakt](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_objects_contact.htm).
   * Du kan identifiera obligatoriska fält genom att söka efter ordet *Obligatorisk*, som anges i fältbeskrivningar i länken ovan.
   * Beroende på vilka fält du vill exportera eller uppdatera lägger du till mappningar mellan XDM-profilschemat och [!DNL (API) Salesforce CRM]:
|Source-fält|Målfält| Anteckningar |
| — | — | — |
|`IdentityMap: crmID`|`Identity: SalesforceId`|`Mandatory`|
|`xdm: person.name.lastName`|`Attribute: LastName`| `Mandatory`. Kontaktens efternamn är högst 80 tecken. |\
     |`xdm: person.name.firstName`|`Attribute: FirstName`| Kontaktens förnamn är högst 40 tecken långt. |
|`xdm: personalEmail.address`|`Attribute: Email`| Kontaktens e-postadress. |

   * Ett exempel på hur du använder dessa mappningar visas nedan:
     ![Exempel på skärmbild för plattformsgränssnitt som visar målmappningar.](../../assets/catalog/crm/salesforce/mappings-contacts.png)

   **Arbeta med leads**

   * Om du arbetar med *Leads* i ditt segment kan du definiera mappningar för fälten som ska uppdateras genom att läsa objektreferensen i Salesforce för [Lead](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_objects_lead.htm) .
   * Du kan identifiera obligatoriska fält genom att söka efter ordet *Obligatorisk*, som anges i fältbeskrivningar i länken ovan.
   * Beroende på vilka fält du vill exportera eller uppdatera lägger du till mappningar mellan XDM-profilschemat och [!DNL (API) Salesforce CRM]:
|Source-fält|Målfält| Anteckningar |
| — | — | — |
|`IdentityMap: crmID`|`Identity: SalesforceId`|`Mandatory`|
|`xdm: person.name.lastName`|`Attribute: LastName`| `Mandatory`. Ledningens efternamn är högst 80 tecken. |\
     |`xdm: b2b.companyName`|`Attribute: Company`| `Mandatory`. Ledarens företag. |
|`xdm: personalEmail.address`|`Attribute: Email`| Leadens e-postadress. |

   * Ett exempel på hur du använder dessa mappningar visas nedan:
     ![Exempel på skärmbild för plattformsgränssnitt som visar målmappningar.](../../assets/catalog/crm/salesforce/mappings-leads.png)

När du har angett mappningarna för målanslutningen väljer du **[!UICONTROL Next]**.

### Schemalägg målgruppsexport och exempel {#schedule-segment-export-example}

När du utför steget [Schemalägg målgruppsexport](/help/destinations/ui/activate-segment-streaming-destinations.md#scheduling) måste du manuellt mappa målgrupper som har aktiverats från Platform till deras motsvarande anpassade fält i [!DNL Salesforce].

Det gör du genom att markera varje segment och sedan ange det anpassade fältnamnet från [!DNL Salesforce] i fältet [!DNL Salesforce CRM] **[!UICONTROL Mapping ID]**. Mer information om hur du skapar anpassade fält i [!DNL Salesforce] finns i avsnittet [Skapa anpassade fält i [!DNL Salesforce]](#prerequisites-custom-field).

Om det anpassade fältet [!DNL Salesforce] till exempel är `crm_2_seg` anger du det här värdet i [!DNL Salesforce CRM] **[!UICONTROL Mapping ID]** för att fylla målgrupper från Experience Platform i det här anpassade fältet.

Ett exempel på ett anpassat fält från [!DNL Salesforce] visas nedan:
![[!DNL Salesforce] Skärmbild i användargränssnittet med anpassat fält. ](../../assets/catalog/crm/salesforce/salesforce-custom-field.png)

Ett exempel som anger platsen för [!DNL Salesforce CRM] **[!UICONTROL Mapping ID]** visas nedan:
![Exempel på skärmbild i användargränssnittet för plattformen som visar export av schemalagda målgrupper.](../../assets/catalog/crm/salesforce/schedule-segment-export.png)

Som visas ovan matchar [!DNL Salesforce] **[!UICONTROL Field Name]** exakt det värde som anges i [!DNL Salesforce CRM] **[!UICONTROL Mapping ID]**.

Beroende på ditt användningssätt kan alla aktiverade målgrupper mappas till samma anpassade [!DNL Salesforce]-fält eller till olika **[!UICONTROL Field Name]** i [!DNL Salesforce CRM]. Ett typiskt exempel baserat på bilden ovan kan vara.
| [!DNL Salesforce CRM] segmentnamn | [!DNL Salesforce] **[!UICONTROL Field Name]** | [!DNL Salesforce CRM] **[!UICONTROL Mapping ID]** |
| — | — | — |
| crm_1_seg | `crm_1_seg` | `crm_1_seg` |
| crm_2_seg | `crm_2_seg` | `crm_2_seg` |

Upprepa det här avsnittet för varje aktiverat plattformssegment.

## Validera dataexport {#exported-data}

Följ stegen nedan för att verifiera att du har konfigurerat målet korrekt:

1. Välj **[!UICONTROL Destinations]** > **[!UICONTROL Browse]** för att navigera till listan över mål.
   ![Skärmbild för plattformsgränssnitt med bläddringsmål.](../../assets/catalog/crm/salesforce/browse-destinations.png)

1. Markera målet och validera att statusen är **[!UICONTROL enabled]**.
   ![Skärmbild för plattformsgränssnitt med körning av måldataflöde.](../../assets/catalog/crm/salesforce/destination-dataflow-run.png)

1. Växla till fliken **[!UICONTROL Activation data]** och välj sedan ett publiknamn.
   ![Exempel på skärmbild för användargränssnittet för plattformen som visar aktiveringsdata för destinationer.](../../assets/catalog/crm/salesforce/destinations-activation-data.png)

1. Övervaka målgruppssammanfattningen och se till att antalet profiler motsvarar antalet som skapas inom segmentet.
   ![Exempel på skärmbild för plattformsgränssnitt som visar segment.](../../assets/catalog/crm/salesforce/segment.png)

1. Logga sedan in på Salesforce-webbplatsen och validera om profilerna från målgruppen har lagts till eller uppdaterats.

   **Arbeta med kontakter**

   * Om du har valt *Kontakter* i ditt plattformssegment går du till sidan **[!DNL Apps]** > **[!DNL Contacts]**.
     ![Salesforce CRM-skärmbild som visar sidan Kontakter med profilerna från segmentet.](../../assets/catalog/crm/salesforce/contacts.png)

   * Välj en *kontakt* och kontrollera om fälten har uppdaterats. Du kan se att varje målgruppsstatus i [!DNL Salesforce CRM] har uppdaterats med motsvarande målgruppsstatus från Platform, baserat på värdet **[!UICONTROL Mapping ID]** som angavs under [målgruppsplaneringen](#schedule-segment-export-example).
     ![Salesforce CRM-skärmbild som visar sidan Kontaktinformation med uppdaterade målgruppsstatusar.](../../assets/catalog/crm/salesforce/contact-info.png)

   **Arbeta med leads**

   * Om du har valt *Leads* i ditt plattformssegment går du till sidan **[!DNL Apps]** > **[!DNL Leads]**.
     ![Salesforce CRM-skärmbild som visar sidan Leads med profilerna från segmentet.](../../assets/catalog/crm/salesforce/leads.png)

   * Välj en *lead* och kontrollera om fälten har uppdaterats. Du kan se att varje målgruppsstatus i [!DNL Salesforce CRM] har uppdaterats med motsvarande målgruppsstatus från Platform, baserat på värdet **[!UICONTROL Mapping ID]** som angavs under [målgruppsplaneringen](#schedule-segment-export-example).
     ![Salesforce CRM-skärmbild som visar sidan Leadinformation med uppdaterade målgruppsstatusar.](../../assets/catalog/crm/salesforce/lead-info.png)

## Dataanvändning och styrning {#data-usage-governance}

Alla [!DNL Adobe Experience Platform]-mål är kompatibla med dataanvändningsprinciper när data hanteras. Mer information om hur [!DNL Adobe Experience Platform] använder datastyrning finns i [Datastyrningsöversikten](/help/data-governance/home.md).

## Fel och felsökning {#errors-and-troubleshooting}

### Okända fel påträffades när händelser skickades till målet {#unknown-errors}

* När du kontrollerar ett dataflöde kan följande felmeddelande visas: `Unknown errors encountered while pushing events to the destination. Please contact the administrator and try again.`
  ![Skärmbild för plattformsgränssnitt visar ett fel.](../../assets/catalog/crm/salesforce/error.png)

   * Om du vill åtgärda det här felet kontrollerar du att **[!UICONTROL Mapping ID]** som du angav i aktiveringsarbetsflödet till [!DNL Salesforce CRM]-målet exakt matchar värdet för den anpassade fälttyp som du skapade i [!DNL Salesforce]. Mer information finns i avsnittet [Skapa anpassade fält i [!DNL Salesforce]](#prerequisites-custom-field).

* När du aktiverar ett segment kan du få ett felmeddelande: `The client's IP address is unauthorized for this account. Allowlist the client's IP address...`
   * Om du vill åtgärda det här felet kontaktar du kontoadministratören för [!DNL Salesforce] och lägger till [Experience Platform IP-adresser](/help/destinations/catalog/streaming/ip-address-allow-list.md) i [!DNL Salesforce]-kontonas betrodda IP-intervall. Mer information finns i dokumentationen för [!DNL Salesforce] [Begränsa åtkomst till betrodda IP-intervall för ett anslutet program](https://help.salesforce.com/s/articleView?id=sf.connected_app_edit_ip_ranges.htm&amp;type=5) om du behöver ytterligare hjälp.

## Ytterligare resurser {#additional-resources}

Ytterligare användbar information från [Salesforce-utvecklarportalen](https://developer.salesforce.com/) finns nedan:
* [Snabbstart](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/quickstart.htm)
* [Skapa en post](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/dome_sobject_create.htm)
* [Anpassade rekommendationspubliker](https://developer.salesforce.com/docs/atlas.en-us.236.0.chatterapi.meta/chatterapi/connect_resources_recommendation_audiences_list.htm)
* [Använder sammansatta resurser](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/using_composite_resources.htm?q=composite)
* Det här målet utnyttjar API-anropet [Uppdatera flera poster](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/resources_composite_sobjects_collections_update.htm) i stället för API-anropet [Uppdatera enstaka post](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/dome_composite_upsert_example.htm?q=contacts).