---
keywords: crm;CRM;crm destination;salesforce crm;salesforce crm destination
title: Salesforce CRM-anslutning
description: Med Salesforce CRM-destinationen kan du exportera dina kontodata och aktivera dem i Salesforce CRM för dina affärsbehov.
exl-id: bd9cb656-d742-4a18-97a2-546d4056d093
source-git-commit: edf49d8a52eeddea65a18c1dad0035ec7e5d2c12
workflow-type: tm+mt
source-wordcount: '2985'
ht-degree: 0%

---

# [!DNL Salesforce CRM] anslutning

## Översikt {#overview}

[[!DNL Salesforce CRM]](https://www.salesforce.com/crm/) är en populär CRM-plattform (Customer Relationship Management) som har stöd för följande:

* [Leads](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_objects_lead.htm) - Ett lead är namnet på en person eller ett företag som kan (eller inte) vara intresserad av de produkter eller tjänster som du säljer.
* [Kontakter](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_objects_contact.htm) - En kontakt är en person med vilken en av dina representanter har upprättat en relation och har kvalificerats som en potentiell kund.

Detta [!DNL Adobe Experience Platform] [mål](/help/destinations/home.md) utnyttjar [[!DNL Salesforce composite API]](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/resources_composite_sobjects_collections_update.htm), som stöder båda profiltyperna som beskrivs ovan.

När [aktivera segment](#activate)kan du välja mellan antingen leads eller kontakter och uppdatera attribut och segmentera data i [!DNL Salesforce CRM].

[!DNL Salesforce CRM] använder OAuth 2 med lösenordsbeviljande som autentiseringsmekanism för att kommunicera med Salesforce REST API. Instruktioner för hur du autentiserar [!DNL Salesforce CRM] -instansen är längre ned, i [Autentisera till mål](#authenticate) -avsnitt.

## Användningsfall {#use-cases}

Som marknadsförare kan ni leverera personaliserade upplevelser till era användare, baserat på attribut från deras Adobe Experience Platform-profiler. Du kan skapa segment utifrån dina offlinedata och skicka dessa segment till Salesforce CRM, som visas i användarens flöden så snart segment och profiler uppdateras i Adobe Experience Platform.

## Förutsättningar {#prerequisites}

### Förutsättningar i Experience Platform {#prerequisites-in-experience-platform}

Innan du aktiverar data till Salesforce CRM-målet måste du ha en [schema](/help/xdm/schema/composition.md), a [datauppsättning](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=en)och [segment](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=en) skapad i [!DNL Experience Platform].

### Förutsättningar [!DNL Salesforce CRM] {#prerequisites-destination}

Observera följande krav i [!DNL Salesforce CRM]för att exportera data från Platform till ditt Salesforce-konto:

#### Du måste ha en [!DNL Salesforce] konto {#prerequisites-account}

Gå till [!DNL Salesforce] [testversion](https://www.salesforce.com/in/form/signup/freetrial-sales/) för att registrera och skapa [!DNL Salesforce] om du inte redan har ett konto.

#### Konfigurera en ansluten app i [!DNL Salesforce] {#prerequisites-connected-app}

Först måste du konfigurera en [[!DNL Salesforce] ansluten app](https://help.salesforce.com/s/articleView?id=sf.connected_app_create.htm&amp;language=en_US&amp;r=https%3A%2F%2Fhelp.salesforce.com%2F&amp;type=5) inom [!DNL Salesforce] om du inte redan har ett konto. [!DNL Salesforce CRM] utnyttjar den anslutna appen för att ansluta till [!DNL Salesforce].

Nästa, aktivera [!DNL OAuth Settings for API Integration] för [!DNL Salesforce connected app]. Se [[!DNL Salesforce]](https://help.salesforce.com/s/articleView?id=connected_app_create_api_integration.htm&amp;type=5&amp;language=en_US) dokumentation för vägledning.

Se även till att [scope](https://help.salesforce.com/s/articleView?id=connected_app_create_api_integration.htm&amp;type=5&amp;language=en_US) som anges nedan är markerade för [!DNL Salesforce connected app].

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

Slutligen måste du se till att `password` anslaget är aktiverat i [!DNL Salesforce] konto. Se [!DNL Salesforce] [OAuth 2.0-användarnamn-lösenord för specialscenarier](https://help.salesforce.com/s/articleView?id=sf.remoteaccess_oauth_username_password_flow.htm&amp;type=5) dokumentation om du behöver hjälp.

>[!IMPORTANT]
>
>Om [!DNL Salesforce] kontoadministratören har begränsat åtkomsten till betrodda IP-intervall, du måste kontakta dem för att få [IP-adresser för Experience Platform](/help/destinations/catalog/streaming/ip-address-allow-list.md) tillåtslista. Se [!DNL Salesforce] [Begränsa åtkomst till betrodda IP-intervall för ett anslutet program](https://help.salesforce.com/s/articleView?id=sf.connected_app_edit_ip_ranges.htm&amp;type=5) dokumentation om du behöver ytterligare vägledning.

#### Skapa anpassade fält i [!DNL Salesforce] {#prerequisites-custom-field}

När segment aktiveras för [!DNL Salesforce CRM] mål måste du ange ett värde i **[!UICONTROL Mapping ID]** för varje aktiverat segment, i **[Segmentschema](#schedule-segment-export-example)** steg.

[!DNL Salesforce CRM] kräver att det här värdet läser och tolkar segment som kommer in från Experience Platform korrekt och uppdaterar deras segmentstatus inom [!DNL Salesforce]. Se dokumentationen för Experience Platform för [Schemafältgrupp för detaljer om segmentmedlemskap](/help/xdm/field-groups/profile/segmentation.md) om du behöver vägledning om segmentstatus.

För varje segment som du aktiverar från Platform till [!DNL Salesforce CRM]måste du skapa ett anpassat fält av typen `Text Area (Long)` inom [!DNL Salesforce]. Du kan definiera längden på fälttecknen i valfri storlek mellan 256 och 131 072 tecken beroende på ditt företags behov. Se [!DNL Salesforce] [Anpassade fälttyper](https://help.salesforce.com/s/articleView?id=sf.custom_field_types.htm&amp;type=5) dokumentationssida för mer information om anpassade fälttyper. Se även [!DNL Salesforce] dokumentation till [skapa anpassade fält](https://help.salesforce.com/s/articleView?id=mc_cab_create_an_attribute.htm&amp;type=5&amp;language=en_US) om du behöver hjälp med att skapa fält.

>[!IMPORTANT]
>
>Ta inte med blankstegstecken i fältnamnet. Använd i stället understrecket `(_)` tecken som avgränsare.
>Inom [!DNL Salesforce] du måste skapa anpassade fält med **[!UICONTROL Field Name]** som exakt matchar värdet som anges i **[!UICONTROL Mapping ID]** för varje aktiverat plattformssegment. På skärmbilden nedan visas ett anpassat fält med namnet `crm_2_seg`. Lägg till `crm_2_seg` as **[!UICONTROL Mapping ID]** för att fylla i segment från Experience Platform i detta anpassade fält.

Ett exempel på hur du skapar anpassade fält i [!DNL Salesforce], *Steg 1 - Välj datatyp*visas nedan:
![Skärmbild för användargränssnittet i Salesforce som visar hur du skapar anpassade fält, steg 1 - Välj datatyp.](../../assets/catalog/crm/salesforce/create-salesforce-custom-field-step-1.png)

Ett exempel på hur du skapar anpassade fält i [!DNL Salesforce], *Steg 2 - Ange information för det anpassade fältet*visas nedan:
![Skärmbild för användargränssnittet i Salesforce som visar hur du skapar anpassade fält, steg 2 - Ange information för anpassade fält.](../../assets/catalog/crm/salesforce/create-salesforce-custom-field-step-2.png)

>[!TIP]
>
>* Att skilja mellan anpassade fält som används för plattformssegment och andra anpassade fält i [!DNL Salesforce] du kan inkludera ett identifierbart prefix eller suffix när du skapar det anpassade fältet. I stället för `test_segment`, använda `Adobe_test_segment` eller `test_segment_Adobe`
>* Om du redan har andra anpassade fält skapade i [!DNL Salesforce]kan du använda samma namn som plattformssegmentet för att enkelt identifiera segmentet i [!DNL Salesforce].


>[!NOTE]
>
>* Objekt i Salesforce är begränsade till 25 externa fält, se [Anpassade fältattribut](https://help.salesforce.com/s/articleView?id=sf.custom_field_attributes.htm&amp;type=5).
>* Den här begränsningen innebär att du bara kan ha högst 25 Experience Platform-segmentmedlemskap aktiva åt gången.
>* Om du har nått den här gränsen i Salesforce måste du ta bort de anpassade attribut från Salesforce som användes för att lagra segmentstatusen mot äldre segment i Experience Platform före ett nytt **[!UICONTROL Mapping ID]** kan användas.


#### Samla [!DNL Salesforce CRM] autentiseringsuppgifter {#gather-credentials}

Anteckna vad som står nedan innan du autentiserar dig för [!DNL Salesforce CRM] mål:

| Autentiseringsuppgifter | Beskrivning | Exempel |
| --- | --- | --- |
| `Username` | Dina [!DNL Salesforce] användarnamn för konto. |  |
| `Password` | Dina [!DNL Salesforce] kontolösenord. |  |
| `Security Token` | Dina [!DNL Salesforce] säkerhetstoken som du senare lägger till i slutet av din [!DNL Salesforce] Lösenord för att skapa en sammanfogad sträng som ska användas som **[!UICONTROL Password]** när [autentiserar mot målet](#authenticate).<br> Se [!DNL Salesforce] dokumentation till [återställa din säkerhetstoken](https://help.salesforce.com/s/articleView?id=sf.user_security_token.htm&amp;type=5) om du vill lära dig hur du genererar om det från [!DNL Salesforce] om du inte har säkerhetstoken. |  |
| `Custom Domain` | Dina [!DNL Salesforce] domänprefix. <br> Se [[!DNL Salesforce] dokumentation](https://help.salesforce.com/s/articleView?id=sf.domain_name_setting_login_policy.htm&amp;type=5) om du vill veta hur du får fram det här värdet från [!DNL Salesforce] gränssnitt. | Om [!DNL Salesforce] domänen är<br> *`d5i000000isb4eak-dev-ed`.my.salesforce.com*,<br> du kommer att behöva `d5i000000isb4eak-dev-ed` som värdet. |
| `Client ID` | Din Salesforce `Consumer Key`. <br> Se [[!DNL Salesforce] dokumentation](https://help.salesforce.com/s/articleView?id=sf.connected_app_rotate_consumer_details.htm&amp;type=5) om du vill veta hur du får fram det här värdet från [!DNL Salesforce] gränssnitt. |  |
| `Client Secret` | Din Salesforce `Consumer Secret`. <br> Se [[!DNL Salesforce] dokumentation](https://help.salesforce.com/s/articleView?id=sf.connected_app_rotate_consumer_details.htm&amp;type=5) om du vill veta hur du får fram det här värdet från [!DNL Salesforce] gränssnitt. |  |

### Guardrails {#guardrails}

[!DNL Salesforce] balanserar transaktionsbelastningen genom att införa gränser för antal begäranden, frekvens och tidsgräns. Se [API-begärandegränser och allokeringar](https://developer.salesforce.com/docs/atlas.en-us.salesforce_app_limits_cheatsheet.meta/salesforce_app_limits_cheatsheet/salesforce_app_limits_platform_api.htm) för mer information.

Om [!DNL Salesforce] kontoadministratören har infört IP-begränsningar, du måste lägga till [Experience Platform IP-adresser](/help/destinations/catalog/streaming/ip-address-allow-list.md) till [!DNL Salesforce] kontots betrodda IP-intervall. Se [!DNL Salesforce] [Begränsa åtkomst till betrodda IP-intervall för ett anslutet program](https://help.salesforce.com/s/articleView?id=sf.connected_app_edit_ip_ranges.htm&amp;type=5) dokumentation om du behöver ytterligare vägledning.

>[!IMPORTANT]
>
>När [aktivera segment](#activate) du måste välja mellan *Kontakt* eller *Lead* typer. Du måste se till att era segment har rätt datamappning beroende på vilken typ som valts.

## Identiteter som stöds {#supported-identities}

[!DNL Salesforce CRM] har stöd för uppdatering av identiteter som beskrivs i tabellen nedan. Läs mer om [identiteter](/help/identity-service/namespaces.md).

| Målidentitet | Beskrivning | Överväganden |
|---|---|---|
| `SalesforceId` | The [!DNL Salesforce CRM] identifierare för de kontakt- eller lead-ID som du exporterar eller uppdaterar genom ditt segment. | Obligatoriskt |

## Exportera typ och frekvens {#export-type-frequency}

Se tabellen nedan för information om exporttyp och frekvens för destinationen.

| Objekt | Typ | Anteckningar |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Profile-based]** | <ul><li>Du exporterar alla medlemmar i ett segment tillsammans med de önskade schemafälten *(till exempel: e-postadress, telefonnummer, efternamn)*, enligt fältmappningen.</li><li> Varje segmentstatus i [!DNL Salesforce CRM] uppdateras med motsvarande segmentstatus från Platform, baserat på **[!UICONTROL Mapping ID]** det värde som anges under [segmentplanering](#schedule-segment-export-example) steg.</li></ul> |
| Exportfrekvens | **[!UICONTROL Streaming]** | <ul><li>Direktuppspelningsmål är alltid på API-baserade anslutningar. Så snart en profil uppdateras i Experience Platform baserat på segmentutvärdering skickar kopplingen uppdateringen nedåt till målplattformen. Läs mer om [mål för direktuppspelning](/help/destinations/destination-types.md#streaming-destinations).</li></ul> |

{style=&quot;table-layout:auto&quot;}

## Anslut till målet {#connect}

>[!IMPORTANT]
>
>Om du vill ansluta till målet behöver du **[!UICONTROL Manage Destinations]** [åtkomstkontrollbehörighet](/help/access-control/home.md#permissions). Läs [åtkomstkontroll - översikt](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få de behörigheter som krävs.

Om du vill ansluta till det här målet följer du stegen som beskrivs i [självstudiekurs om destinationskonfiguration](../../ui/connect-destination.md). I arbetsflödet för att konfigurera mål fyller du i fälten som listas i de två avsnitten nedan.

Inom **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]** sök efter [!DNL Salesforce CRM]. Du kan även hitta den under **[!UICONTROL CRM]** kategori.

### Autentisera till mål {#authenticate}

Om du vill autentisera mot målet fyller du i de obligatoriska fälten nedan och väljer **[!UICONTROL Connect to destination]**. Se [Samla [!DNL Salesforce CRM] autentiseringsuppgifter](#gather-credentials) för vägledning.
| Autentiseringsuppgifter | Beskrivning | | — | — | | **[!UICONTROL Username]** | Dina [!DNL Salesforce] användarnamn för konto. | | **[!UICONTROL Password]** | En sammanfogad sträng som består av [!DNL Salesforce] kontolösenordet har bifogats med [!DNL Salesforce] Säkerhetstoken.<br>Det sammanfogade värdet har formen av `{PASSWORD}{TOKEN}`.<br> Observera att du inte ska använda klammerparenteser eller mellanslag.<br>Till exempel om [!DNL Salesforce] Lösenordet är `MyPa$$w0rd123` och [!DNL Salesforce] Säkerhetstoken är `TOKEN12345....0000`, det sammanfogade värde som du kommer att använda i **[!UICONTROL Password]** fältet är `MyPa$$w0rd123TOKEN12345....0000`. | | **[!UICONTROL Custom Domain]** | Dina [!DNL Salesforce] domänprefix. <br>Om din domän till exempel är *`d5i000000isb4eak-dev-ed`.my.salesforce.com* måste du ange `d5i000000isb4eak-dev-ed` som värdet. | | **[!UICONTROL Client ID]** | Dina [!DNL Salesforce] ansluten app `Consumer Key`. | | **[!UICONTROL Client Secret]** | Dina [!DNL Salesforce] ansluten app `Consumer Secret`. |

![Skärmbild av användargränssnittet för plattformen som visar hur man autentiserar.](../../assets/catalog/crm/salesforce/authenticate-destination.png)

Om den angivna informationen är giltig visas en **[!UICONTROL Connected]** status med en grön bockmarkering kan du fortsätta till nästa steg.

### Fyll i målinformation {#destination-details}

Om du vill konfigurera information för målet fyller du i de obligatoriska och valfria fälten nedan. En asterisk bredvid ett fält i användargränssnittet anger att fältet är obligatoriskt.
* **[!UICONTROL Name]**: Ett namn som du känner igen det här målet med i framtiden.
* **[!UICONTROL Description]**: En beskrivning som hjälper dig att identifiera det här målet i framtiden.
* **[!UICONTROL Salesforce ID Type]**:
   * Välj **[!UICONTROL Contact]** om de identiteter du vill exportera eller uppdatera är av typen *Kontakt*.
   * Välj **[!UICONTROL Lead]** om de identiteter du vill exportera eller uppdatera är av typen *Lead*.

![Skärmbild för användargränssnittet för plattformen som visar målinformationen.](../../assets/catalog/crm/salesforce/destination-details.png)

### Aktivera aviseringar {#enable-alerts}

Du kan aktivera varningar för att få meddelanden om dataflödets status till ditt mål. Välj en avisering i listan om du vill prenumerera och få meddelanden om status för ditt dataflöde. Mer information om varningar finns i guiden [prenumerera på destinationsvarningar med hjälp av användargränssnittet](../../ui/alerts.md).

När du är klar med informationen för målanslutningen väljer du **[!UICONTROL Next]**.

## Aktivera segment till den här destinationen {#activate}

>[!IMPORTANT]
>
>Om du vill aktivera data måste du ha **[!UICONTROL Manage Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** och **[!UICONTROL View Segments]** [behörigheter för åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontroll - översikt](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få de behörigheter som krävs.

Läs [Aktivera profiler och segment för att direktuppspela segmentexportmål](/help/destinations/ui/activate-segment-streaming-destinations.md) om du vill ha instruktioner om hur du aktiverar målgruppssegment till det här målet.

### Mappa överväganden och exempel {#mapping-considerations-example}

Så här skickar du målgruppsdata från Adobe Experience Platform till [!DNL Salesforce CRM] mål måste du gå igenom fältmappningssteget. Mappningen består av att skapa en länk mellan XDM-schemafälten (Experience Data Model) i ditt plattformskonto och motsvarande motsvarigheter från målmålet.

Attribut som anges i **[!UICONTROL Target field]** ska namnges exakt så som beskrivs i tabellen för attributmappningar eftersom dessa attribut kommer att utgöra begärandetexten.

Attribut som anges i **[!UICONTROL Source field]** inte följer någon sådan begränsning. Du kan mappa den baserat på dina behov, men se till att indata-formatet är giltigt enligt [[!DNL Salesforce] dokumentation](https://help.salesforce.com/s/articleView?id=sf.custom_field_attributes.htm&amp;type=5). Om indata inte är giltiga anropas uppdateringsanropet till [!DNL Salesforce] kommer att misslyckas och dina kontakter/leads uppdateras inte.

Koppla XDM-fälten till [!DNL (API) Salesforce CRM] målfält, följ dessa steg:

1. I **[!UICONTROL Mapping]** steg, välja **[!UICONTROL Add new mapping]**visas en ny mappningsrad på skärmen.
   ![Exempel på skärmbild för användargränssnittet för plattformen för att lägga till ny mappning.](../../assets/catalog/crm/salesforce/add-new-mapping.png)
1. I **[!UICONTROL Select source field]** väljer du **[!UICONTROL Select attributes]** och välj XDM-attributet eller välj **[!UICONTROL Select identity namespace]** och välj en identitet.
1. I **[!UICONTROL Select target field]** väljer du **[!UICONTROL Select identity namespace]** och välj en identitet eller välj **[!UICONTROL Select custom attributes]** och välj ett attribut eller definiera ett med **[!UICONTROL Attribute name]** vid behov. Se [[!DNL Salesforce CRM] dokumentation](https://help.salesforce.com/s/articleView?id=sf.custom_field_attributes.htm&amp;type=5) för vägledning om attribut som stöds.
   * Upprepa dessa steg för att lägga till följande mappningar mellan XDM-profilschemat och [!DNL (API) Salesforce CRM]:

   **Arbeta med kontakter**

   * Om du arbetar med *Kontakter* inom ditt segment, se objektreferensen i Salesforce för [Kontakt](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_objects_contact.htm) för att definiera mappningar för de fält som ska uppdateras.
   * Du kan identifiera obligatoriska fält genom att söka efter ordet *Obligatoriskt*, som nämns i fältbeskrivningar i länken ovan.
   * Beroende på vilka fält du vill exportera eller uppdatera lägger du till mappningar mellan XDM-profilschemat och [!DNL (API) Salesforce CRM]: |Källfält|Målfält| Anteckningar | | — | — | — | |`IdentityMap: crmID`|`Identity: SalesforceId`|`Mandatory`| |`xdm: person.name.lastName`|`Attribute: LastName`| `Mandatory`. Kontaktens efternamn är högst 80 tecken. |\
      |`xdm: person.name.firstName`|`Attribute: FirstName`| Kontaktens förnamn är högst 40 tecken långt. | |`xdm: personalEmail.address`|`Attribute: Email`| Kontaktens e-postadress. |

   * Ett exempel på hur du använder dessa mappningar visas nedan:
      ![Exempel på skärmbild för användargränssnittet för plattformen som visar målmappningar.](../../assets/catalog/crm/salesforce/mappings-contacts.png)

   **Arbeta med leads**

   * Om du arbetar med *Leads* inom ditt segment, se objektreferensen i Salesforce för [Lead](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_objects_lead.htm) för att definiera mappningar för de fält som ska uppdateras.
   * Du kan identifiera obligatoriska fält genom att söka efter ordet *Obligatoriskt*, som nämns i fältbeskrivningar i länken ovan.
   * Beroende på vilka fält du vill exportera eller uppdatera lägger du till mappningar mellan XDM-profilschemat och [!DNL (API) Salesforce CRM]: |Källfält|Målfält| Anteckningar | | — | — | — | |`IdentityMap: crmID`|`Identity: SalesforceId`|`Mandatory`| |`xdm: person.name.lastName`|`Attribute: LastName`| `Mandatory`. Ledningens efternamn är högst 80 tecken. |\
      |`xdm: b2b.companyName`|`Attribute: Company`| `Mandatory`. Ledarens företag. | |`xdm: personalEmail.address`|`Attribute: Email`| Leads e-postadress. |

   * Ett exempel på hur du använder dessa mappningar visas nedan:
      ![Exempel på skärmbild för användargränssnittet för plattformen som visar målmappningar.](../../assets/catalog/crm/salesforce/mappings-leads.png)



När du har angett mappningarna för målanslutningen väljer du **[!UICONTROL Next]**.

### Schemalägg segmentexport och exempel {#schedule-segment-export-example}

När du utför [Schemalägg segmentexport](/help/destinations/ui/activate-segment-streaming-destinations.md#scheduling) steg måste du manuellt mappa segment som har aktiverats från Platform till deras motsvarande anpassade fält i [!DNL Salesforce].

Det gör du genom att markera varje segment och sedan ange det anpassade fältnamnet från [!DNL Salesforce] i [!DNL Salesforce CRM] **[!UICONTROL Mapping ID]** fält. Se [Skapa anpassade fält i [!DNL Salesforce]](#prerequisites-custom-field) för vägledning och bästa metoder för att skapa anpassade fält i [!DNL Salesforce].

Om [!DNL Salesforce] anpassat fält är `crm_2_seg`anger du det här värdet i [!DNL Salesforce CRM] **[!UICONTROL Mapping ID]** för att fylla i segment från Experience Platform i detta anpassade fält.

Ett exempel på ett anpassat fält från [!DNL Salesforce] visas nedan:
![[!DNL Salesforce] Skärmbild i användargränssnittet med anpassat fält.](../../assets/catalog/crm/salesforce/salesforce-custom-field.png)

Ett exempel som anger platsen för [!DNL Salesforce CRM] **[!UICONTROL Mapping ID]** visas nedan:
![Exempel på skärmbild för användargränssnittet för plattformen som visar export av Schedule-segment.](../../assets/catalog/crm/salesforce/schedule-segment-export.png)

Som visas ovan [!DNL Salesforce] **[!UICONTROL Field Name]** matchar exakt värdet som anges i [!DNL Salesforce CRM] **[!UICONTROL Mapping ID]**.

Beroende på ditt sätt att arbeta kan alla aktiverade segment mappas till samma [!DNL Salesforce] anpassat fält eller till annat **[!UICONTROL Field Name]** in [!DNL Salesforce CRM]. Ett typiskt exempel baserat på bilden ovan kan vara.
| [!DNL Salesforce CRM] segmentnamn | [!DNL Salesforce] **[!UICONTROL Field Name]** | [!DNL Salesforce CRM] **[!UICONTROL Mapping ID]** | | — | — | — | | crm_1_seg | `crm_1_seg` | `crm_1_seg` | | crm_2_seg | `crm_2_seg` | `crm_2_seg` |

Upprepa det här avsnittet för varje aktiverat plattformssegment.

## Validera dataexport {#exported-data}

Följ stegen nedan för att verifiera att du har konfigurerat målet korrekt:

1. Välj **[!UICONTROL Destinations]** > **[!UICONTROL Browse]** för att navigera till listan över destinationer.
   ![Skärmbild av användargränssnittet för plattformen med bläddringsmål.](../../assets/catalog/crm/salesforce/browse-destinations.png)

1. Markera målet och validera att statusen är **[!UICONTROL enabled]**.
   ![Skärmbild av användargränssnittet för plattformen med körning av måldataflöde.](../../assets/catalog/crm/salesforce/destination-dataflow-run.png)

1. Växla till **[!UICONTROL Activation data]** väljer du ett segmentnamn.
   ![Skärmbild för användargränssnittet för plattformen visar aktiveringsdata för destinationer.](../../assets/catalog/crm/salesforce/destinations-activation-data.png)

1. Övervaka segmentsammanfattningen och se till att antalet profiler motsvarar antalet som skapas i segmentet.
   ![Exempel på skärmbild för plattformsgränssnitt som visar segment.](../../assets/catalog/crm/salesforce/segment.png)

1. Logga sedan in på Salesforce-webbplatsen och validera om profilerna från segmentet har lagts till eller uppdaterats.

   **Arbeta med kontakter**

   * Om du har valt *Kontakter* i ditt plattformssegment navigerar du till **[!DNL Apps]** > **[!DNL Contacts]** sida.
      ![Salesforce CRM-skärmbild som visar sidan Kontakter med profilerna från segmentet.](../../assets/catalog/crm/salesforce/contacts.png)

   * Välj en *Kontakt* och kontrollera om fälten har uppdaterats. Du kan se att varje segmentstatus i [!DNL Salesforce CRM] uppdaterades med motsvarande segmentstatus från Platform, baserat på **[!UICONTROL Mapping ID]** det värde som anges under [segmentplanering](#schedule-segment-export-example).
      ![Salesforce CRM-skärmbild som visar sidan Kontaktinformation med uppdaterade segmentstatusar.](../../assets/catalog/crm/salesforce/contact-info.png)

   **Arbeta med leads**

   * Om du har valt *Leads* i ditt plattformssegment, navigera sedan till **[!DNL Apps]** > **[!DNL Leads]** sida.
      ![Salesforce CRM-skärmbild som visar sidan Leads med profilerna från segmentet.](../../assets/catalog/crm/salesforce/leads.png)

   * Välj en *Lead* och kontrollera om fälten har uppdaterats. Du kan se att varje segmentstatus i [!DNL Salesforce CRM] uppdaterades med motsvarande segmentstatus från Platform, baserat på **[!UICONTROL Mapping ID]** det värde som anges under [segmentplanering](#schedule-segment-export-example).
      ![Salesforce CRM, bild som visar sidan Leadinformation med uppdaterade segmentstatusar.](../../assets/catalog/crm/salesforce/lead-info.png)


## Dataanvändning och styrning {#data-usage-governance}

Alla [!DNL Adobe Experience Platform] destinationerna är kompatibla med dataanvändningsprinciper när data hanteras. Detaljerad information om hur [!DNL Adobe Experience Platform] använder datastyrning, se [Datastyrning - översikt](/help/data-governance/home.md).

## Fel och felsökning {#errors-and-troubleshooting}

### Okända fel påträffades när händelser skickades till målet {#unknown-errors}

* När du kontrollerar ett dataflöde kan följande felmeddelande visas: `Unknown errors encountered while pushing events to the destination. Please contact the administrator and try again.`

   ![Skärmbild för användargränssnittet för plattformen visar ett fel.](../../assets/catalog/crm/salesforce/error.png)

   * Kontrollera att **[!UICONTROL Mapping ID]** som du angav i aktiveringsarbetsflödet för [!DNL Salesforce CRM] målet matchar exakt värdet för den anpassade fälttyp som du skapade i [!DNL Salesforce]. Se [Skapa anpassade fält i [!DNL Salesforce]](#prerequisites-custom-field) för vägledning.

* När du aktiverar ett segment kan du få ett felmeddelande: `The client's IP address is unauthorized for this account. Allowlist the client's IP address...`
   * Om du vill åtgärda felet kontaktar du [!DNL Salesforce] kontoadministratör att lägga till [Experience Platform IP-adresser](/help/destinations/catalog/streaming/ip-address-allow-list.md) till [!DNL Salesforce] kontots betrodda IP-intervall. Se [!DNL Salesforce] [Begränsa åtkomst till betrodda IP-intervall för ett anslutet program](https://help.salesforce.com/s/articleView?id=sf.connected_app_edit_ip_ranges.htm&amp;type=5) dokumentation om du behöver ytterligare vägledning.

## Ytterligare resurser {#additional-resources}

Ytterligare användbar information från [Salesforce-utvecklarportal](https://developer.salesforce.com/) är under:
* [Snabbstart](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/quickstart.htm)
* [Skapa en post](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/dome_sobject_create.htm)
* [Anpassade rekommendationsmålgrupper](https://developer.salesforce.com/docs/atlas.en-us.236.0.chatterapi.meta/chatterapi/connect_resources_recommendation_audiences_list.htm)
* [Använda sammansatta resurser](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/using_composite_resources.htm?q=composite)
* Detta mål utnyttjar [Uppgradera flera poster](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/resources_composite_sobjects_collections_update.htm) API i stället för [Uppgradera en post](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/dome_composite_upsert_example.htm?q=contacts) API-anrop.