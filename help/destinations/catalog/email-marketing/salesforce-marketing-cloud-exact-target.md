---
title: (API) Salesforce Marketing Cloud-anslutning
description: Med Salesforce Marketing Cloud (tidigare ExactTarget) kan du exportera dina kontodata och aktivera dem i Salesforce Marketing Cloud för dina affärsbehov.
exl-id: 0cf068e6-8a0a-4292-a7ec-c40508846e27
source-git-commit: ba39f62cd77acedb7bfc0081dbb5f59906c9b287
workflow-type: tm+mt
source-wordcount: '2803'
ht-degree: 0%

---

# [!DNL (API) Salesforce Marketing Cloud] anslutning

## Översikt {#overview}

[[!DNL (API) Salesforce Marketing Cloud]](https://www.salesforce.com/products/marketing-cloud/engagement/) (tidigare känt som [!DNL ExactTarget]) är en digital marknadsföringssvit som gör att ni kan skapa och anpassa resor för besökare och kunder för att personalisera deras upplevelse.

>[!IMPORTANT]
>
> Observera skillnaden mellan den här anslutningen och den andra [[!DNL Salesforce Marketing Cloud] anslutning](/help/destinations/catalog/email-marketing/salesforce-marketing-cloud.md) som finns i katalogavsnittet E-postmarknadsföring. Med den andra Salesforce Marketing Cloud-anslutningen kan du exportera filer till en angiven lagringsplats, medan detta är en API-baserad direktuppspelningsanslutning.

Jämfört med [!DNL Salesforce Marketing Cloud Account Engagement] som är mer inriktad på **B2B** marknadsföring, [!DNL (API) Salesforce Marketing Cloud] målet är idealiskt för **B2C** Användningsfall med kortare handläggningstider. Ni kan konsolidera större datauppsättningar som representerar målgruppens beteende för att justera och förbättra marknadsföringskampanjer genom att prioritera och segmentera kontakter, särskilt från datauppsättningar utanför [!DNL Salesforce]. *Observera att Experience Platform också har en anslutning till [[!DNL Salesforce Marketing Cloud Account Engagement]](/help/destinations/catalog/email-marketing/salesforce-marketing-cloud-account-engagement.md).*

Detta [!DNL Adobe Experience Platform] [mål](/help/destinations/home.md) använder [!DNL Salesforce Marketing Cloud] [uppdatera kontakter](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/updateContacts.html) API, som gör att du kan **lägga till kontakter och uppdatera kontaktdata** efter att ha aktiverat dem i en ny [!DNL Salesforce Marketing Cloud] segment.

[!DNL Salesforce Marketing Cloud] använder OAuth 2 med klientautentiseringsuppgifter som autentiseringsmekanism för att kommunicera med [!DNL Salesforce Marketing Cloud] API. Instruktioner för hur du autentiserar [!DNL Salesforce Marketing Cloud] -instansen är längre ned, i [Autentisera till mål](#authenticate) -avsnitt.

## Användningsfall {#use-cases}

För att du bättre ska förstå hur och när du ska använda [!DNL (API) Salesforce Marketing Cloud] mål, här är ett exempel på användning som Adobe Experience Platform-kunder kan lösa genom att använda den här destinationen.

### Skicka e-post till kontakter för marknadsföringskampanjer {#use-case-send-emails}

Försäljningsavdelningen på en uthyrningsplattform vill sända ett marknadsföringsmejl till en målgrupp. Plattformens marknadsföringsteam kan lägga till nya kontakter/uppdatera befintliga kontakter *(och deras e-postadresser)* via Adobe Experience Platform, bygga målgrupper utifrån deras egna offlinedata och skicka dessa målgrupper till [!DNL Salesforce Marketing Cloud]som sedan kan användas för att skicka marknadsföringskampanjens e-post.

## Förutsättningar {#prerequisites}

### Förutsättningar i Experience Platform {#prerequisites-in-experience-platform}

Innan du aktiverar data för [!DNL (API) Salesforce Marketing Cloud] mål, du måste ha [schema](/help/xdm/schema/composition.md), a [datauppsättning](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html)och [segment](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html) som [!DNL Experience Platform].

### Krav [!DNL (API) Salesforce Marketing Cloud] {#prerequisites-destination}

Observera följande krav för att kunna exportera data från Platform till [!DNL Salesforce Marketing Cloud] konto:

#### Du måste ha en [!DNL Salesforce Marketing Cloud] konto {#prerequisites-account}

A [!DNL Salesforce Marketing Cloud] konto med en prenumeration på [[!DNL Marketing Cloud Engagement]](https://www.salesforce.com/products/marketing-cloud/engagement/) produkten är obligatorisk för att fortsätta.

Nå ut till [[!DNL Salesforce] Support](https://www.salesforce.com/company/contact-us/?d=cta-glob-footer-10) om du inte har en [!DNL Salesforce Marketing Cloud] eller så saknas kontot [!DNL Marketing Cloud Engagement] produktprenumeration.

#### Skapa attribut i [!DNL Salesforce Marketing Cloud] {#prerequisites-attribute}

När målgrupper aktiveras för [!DNL (API) Salesforce Marketing Cloud] mål måste du ange ett värde i **[!UICONTROL Mapping ID]** för varje aktiverad målgrupp, i **[Målgruppsschema](#schedule-segment-export-example)** steg.

[!DNL Salesforce] kräver att det här värdet läser och tolkar målgrupper som kommer från Experience Platform korrekt och uppdaterar deras målgruppsstatus inom [!DNL Salesforce Marketing Cloud]. Se dokumentationen för Experience Platform för [Schemafältgrupp för målgruppsmedlemskapsdetaljer](/help/xdm/field-groups/profile/segmentation.md) om ni behöver vägledning om målgruppsstatus.

För varje målgrupp som du aktiverar från Platform till [!DNL Salesforce]måste du ha ett attribut av typen `Text` länkad till [!DNL Email Demographics] datatillägg inom [!DNL Salesforce Marketing Cloud]. Använd [!DNL Salesforce Marketing Cloud] [!DNL Contact Builder] för att skapa attribut. Se [!DNL Salesforce Marketing Cloud] dokumentation till [skapa attribut](https://help.salesforce.com/s/articleView?id=mc_cab_create_an_attribute.htm&amp;type=5&amp;language=en_US) om du behöver hjälp med att skapa attribut.

Attributfältsnamnen används för [!DNL (API) Salesforce Marketing Cloud] målfält under **[!UICONTROL Mapping]** steg. Du kan definiera fälttecknet med högst 4 000 tecken, beroende på dina affärsbehov. Se [!DNL Salesforce Marketing Cloud] [Datatyper för datatillägg](https://help.salesforce.com/s/articleView?id=sf.mc_es_data_extension_data_types.htm&amp;type=5) dokumentationssida för mer information om attributtyper.

Ett exempel på datadesignerskärmen i [!DNL Salesforce Marketing Cloud]som du ska lägga till attributet i visas nedan:
![Datadesigner för användargränssnittet i Salesforce Marketing Cloud.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/salesforce-data-designer.png)

En vy av en [!DNL Salesforce Marketing Cloud] [!DNL Email Data] attributgrupp med attribut som motsvarar målgruppsstatusen i [!DNL Email Demographics] datatillägg visas nedan:
![E-postattributgrupp för användargränssnittet i Salesforce Marketing Cloud.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/salesforce-email-demographics-fields.png)

The [!DNL (API) Salesforce Marketing Cloud] destinationen använder [!DNL Salesforce Marketing Cloud] [!DNL Search Attribute-Set Definitions REST] [API](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/retrieveAttributeSetDefinitions.html) att dynamiskt hämta datatilläggen och deras länkade attribut som definierats i [!DNL Salesforce Marketing Cloud].

Dessa visas i **[!UICONTROL Target field]** markeringsfönstret när du ställer in [mappning](#mapping-considerations-example) till [aktivera målgrupper till målet](#activate).

>[!IMPORTANT]
>
> Inom [!DNL Salesforce Marketing Cloud]måste du skapa attribut med **[!UICONTROL FIELD NAME]** som exakt matchar värdet som anges i **[!UICONTROL Mapping ID]** för varje aktiverat plattformssegment. På skärmbilden nedan visas ett attribut med namnet `salesforce_mc_segment_1`. Lägg till `salesforce_mc_segment_1` as **[!UICONTROL Mapping ID]** för att fylla målgrupper från Experience Platform i detta attribut.

Ett exempel på hur attribut skapas i [!DNL Salesforce Marketing Cloud], visas nedan:
![Användargränssnittet i Salesforce Marketing Cloud med ett attribut.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/salesforce-custom-field.png)

>[!TIP]
>
> * När du skapar attributet ska du inte ta med blankstegstecken i fältnamnet. Använd i stället understrecket `(_)` tecken som avgränsare.
> * Att skilja mellan attribut som används för plattformens målgrupper och andra attribut inom [!DNL Salesforce Marketing Cloud]kan du inkludera ett identifierbart prefix eller suffix för de attribut som används för Adobe-segment. I stället för `test_segment`, använda `Adobe_test_segment` eller `test_segment_Adobe`.
> * Om du redan har andra attribut som [!DNL Salesforce Marketing Cloud]kan du använda samma namn som plattformssegmentet för att enkelt identifiera målgruppen i [!DNL Salesforce Marketing Cloud].

#### Tilldela användarroller och behörigheter i [!DNL Salesforce Marketing Cloud] {#prerequisites-roles-permissions}

Som [!DNL Salesforce Marketing Cloud] har stöd för anpassade roller beroende på ditt användningsfall, bör din användare tilldelas de relevanta rollerna för att uppdatera dina attribut inom [!DNL Salesforce Marketing Cloud]. Ett exempel på roller som tilldelats en användare visas nedan:
![Användargränssnittet Salesforce Marketing Cloud för en vald användare som visar sina tilldelade roller.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/salesforce-edit-roles.png)

Beroende på vilka roller du [!DNL Salesforce Marketing Cloud] användaren har tilldelats, du måste även tilldela behörigheter till [!DNL Salesforce Marketing Cloud] som är länkade till de fält som du vill uppdatera.

Eftersom det här målet kräver åtkomst till `[!DNL data extension]`måste du tillåta dem. Till exempel för `Email` [!DNL data extension] du måste tillåta enligt nedan:

![Användargränssnittet i Salesforce Marketing Cloud visar e-postdatatillägget med tillåtna behörigheter.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/salesforce-permisions-list.png)

Om du vill begränsa åtkomstnivån kan du även åsidosätta individuell åtkomst genom att använda detaljerade behörigheter.
![Användargränssnittet i Salesforce Marketing Cloud visar e-postdatatillägget med detaljerad behörighet.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/sales-email-attribute-set-permission.png)

Se [[!DNL Marketing Cloud Roles]](https://help.salesforce.com/s/articleView?language=en_US&amp;id=sf.mc_overview_marketing_cloud_roles.htm&amp;type=5) och [[!DNL Marketing Cloud Roles and Permissions]](https://help.salesforce.com/s/articleView?language=en_US&amp;id=sf.mc_overview_roles.htm&amp;type=5) sidor för detaljerad vägledning.

#### Samla [!DNL Salesforce Marketing Cloud] autentiseringsuppgifter {#gather-credentials}

Anteckna nedanstående innan du autentiserar dig för [!DNL (API) Salesforce Marketing Cloud] mål.

| Autentiseringsuppgifter | Beskrivning | Exempel |
| --- | --- | --- |
| Underdomän | Se [[!DNL Salesforce Marketing Cloud domain prefix]](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/your-subdomain-tenant-specific-endpoints.html) om du vill veta hur du får fram det här värdet från [!DNL Salesforce Marketing Cloud] gränssnitt. | Om [!DNL Salesforce Marketing Cloud] domänen är<br> *`mcq4jrssqdlyc4lph19nnqgzzs84`.login.exacttarget.com*, <br>du måste ange `mcq4jrssqdlyc4lph19nnqgzzs84` som värdet. |
| Klient-ID | Se [!DNL Salesforce Marketing Cloud] [dokumentation](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/access-token-s2s.html) om du vill veta hur du får fram det här värdet från [!DNL Salesforce Marketing Cloud] gränssnitt. | r23kxxxxxx0z05xxxx |
| Klienthemlighet | Se [!DNL Salesforce Marketing Cloud] [dokumentation](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/access-token-s2s.html) om du vill veta hur du får fram det här värdet från [!DNL Salesforce Marketing Cloud] gränssnitt. | ipxxxxxxxxxxT4xxxxxxxx |

{style="table-layout:auto"}

### Guardrails {#guardrails}

* Salesforce inför vissa [hastighetsbegränsningar](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/rate-limiting.html).
   * Se [!DNL Salesforce Marketing Cloud] [dokumentation](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/rate-limiting-errors.html) för att åtgärda eventuella begränsningar som kan uppstå och minska antalet fel under körningen.
   * Se [[!DNL Salesforce Marketing Cloud] Engagemangspris](https://www.salesforce.com/editions-pricing/marketing-cloud/email/) sida till *Ladda ned jämförelsetabellen för fullversionen* som en pdf som detaljerar de begränsningar som din plan innebär.
   * The [API-översikt](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/apis-overview.html) ytterligare begränsningar för sidinformation.
   * Referens [här](https://salesforce.stackexchange.com/questions/205898/marketing-cloud-api-limits) för en sida som sammanställer dessa uppgifter.
* Antal *anpassade fält tillåtna per objekt* varierar beroende på din Salesforce Edition.
   * Se [!DNL Salesforce] [dokumentation](https://help.salesforce.com/s/articleView?id=sf.custom_field_allocations.htm&amp;type=5) för ytterligare vägledning.
   * Om du har nått gränsen för *anpassade fält tillåtna per objekt* inom [!DNL Salesforce Marketing Cloud] måste du
      * Ta bort äldre attribut innan du lägger till nya attribut i [!DNL Salesforce Marketing Cloud].
      * Uppdatera eller ta bort aktiverade målgrupper i plattformsmål som använder dessa äldre attributnamn som det angivna värdet **[!UICONTROL Mapping ID]** under [målgruppsplanering](#schedule-segment-export-example) steg.

## Identiteter som stöds {#supported-identities}

[!DNL (API) Salesforce Marketing Cloud] stöder aktivering av identiteter som beskrivs i tabellen nedan. Läs mer om [identiteter](/help/identity-service/features/namespaces.md).

| Målidentitet | Beskrivning | Överväganden |
|---|---|---|
| contactKey | [!DNL Salesforce Marketing Cloud] Kontaktnyckel. Se [!DNL Salesforce Marketing Cloud] [dokumentation](https://help.salesforce.com/s/articleView?id=sf.mc_cab_contact_builder_best_practices.htm&amp;type=5) om du behöver ytterligare vägledning. | Obligatoriskt |

## Målgrupper {#supported-audiences}

I det här avsnittet beskrivs vilka typer av målgrupper du kan exportera till det här målet.

| Målgruppsursprung | Stöds | Beskrivning |
---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Målgrupper som skapats genom Experience Platform [Segmenteringstjänst](../../../segmentation/home.md). |
| Anpassade överföringar | X | Målgrupper [importerad](../../../segmentation/ui/overview.md#import-audience) till Experience Platform från CSV-filer. |

{style="table-layout:auto"}

## Exportera typ och frekvens {#export-type-frequency}

Se tabellen nedan för information om exporttyp och frekvens för destinationen.

| Objekt | Typ | Anteckningar |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Profile-based]** | <ul><li>Du exporterar alla medlemmar i ett segment tillsammans med de önskade schemafälten *(t.ex. e-postadress, telefonnummer, efternamn)*, enligt fältmappningen.</li><li> Varje segmentstatus i [!DNL Salesforce Marketing Cloud] uppdateras med motsvarande målgruppsstatus från Platform, baserat på **[!UICONTROL Mapping ID]** det värde som anges under [målgruppsplanering](#schedule-segment-export-example) steg.</li></ul> |
| Exportfrekvens | **[!UICONTROL Streaming]** | Direktuppspelningsmål är alltid på API-baserade anslutningar. Så snart en profil uppdateras i Experience Platform baserat på målgruppsutvärdering skickar anslutningsprogrammet uppdateringen nedströms till målplattformen. Läs mer om [mål för direktuppspelning](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Anslut till målet {#connect}

>[!IMPORTANT]
>
> Om du vill ansluta till målet behöver du **[!UICONTROL Manage Destinations]** [behörighet för åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontroll - översikt](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få de behörigheter som krävs.

Om du vill ansluta till det här målet följer du stegen som beskrivs i [självstudiekurs om destinationskonfiguration](../../ui/connect-destination.md). I arbetsflödet för att konfigurera mål fyller du i fälten som listas i de två avsnitten nedan.

Inom **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]**, sök efter [!DNL (API) Salesforce Marketing Cloud]. Du kan även hitta den under **[!UICONTROL Email marketing]** kategori.

### Autentisera till mål {#authenticate}

Om du vill autentisera mot målet fyller du i de obligatoriska fälten nedan och väljer **[!UICONTROL Connect to destination]**. Se [Samla [!DNL Salesforce Marketing Cloud] autentiseringsuppgifter](#gather-credentials) för vägledning.

| [!DNL (API) Salesforce Marketing Cloud] mål | [!DNL Salesforce Marketing Cloud] |
| --- | --- |
| **[!UICONTROL Subdomain]** | Dina [!DNL Salesforce Marketing Cloud] domänprefix. <br>Om din domän till exempel är <br> *`mcq4jrssqdlyc4lph19nnqgzzs84`.login.exacttarget.com*, <br> du måste ange `mcq4jrssqdlyc4lph19nnqgzzs84` som värdet. |
| **[!UICONTROL Client ID]** | Dina [!DNL Salesforce Marketing Cloud] `Client ID`. |
| **[!UICONTROL Client Secret]** | Dina [!DNL Salesforce Marketing Cloud] `Client Secret`. |

![Skärmbild av användargränssnittet för plattformen som visar hur du autentiserar till Salesforce Marketing Cloud.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/authenticate-destination.png)

Om den angivna informationen är giltig visas en **[!UICONTROL Connected]** status med en grön bockmarkering kan du fortsätta till nästa steg.

### Fyll i målinformation {#destination-details}

Om du vill konfigurera information för målet fyller du i de obligatoriska och valfria fälten nedan. En asterisk bredvid ett fält i användargränssnittet anger att fältet är obligatoriskt.
![Skärmbild för användargränssnittet för plattformen som visar målinformationen.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/destination-details.png)

* **[!UICONTROL Name]**: Ett namn som du känner igen det här målet med i framtiden.
* **[!UICONTROL Description]**: En beskrivning som hjälper dig att identifiera det här målet i framtiden.

### Aktivera aviseringar {#enable-alerts}

Du kan aktivera varningar för att få meddelanden om dataflödets status till ditt mål. Välj en avisering i listan om du vill prenumerera och få meddelanden om statusen för ditt dataflöde. Mer information om varningar finns i guiden på [prenumerera på destinationsvarningar med användargränssnittet](../../ui/alerts.md).

När du är klar med informationen för målanslutningen väljer du **[!UICONTROL Next]**.

## Aktivera målgrupper till det här målet {#activate}

>[!IMPORTANT]
> 
> * För att aktivera data behöver du **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** och **[!UICONTROL View Segments]** [behörigheter för åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontroll - översikt](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få de behörigheter som krävs.
> * Exportera *identiteter* behöver du **[!UICONTROL View Identity Graph]** [behörighet för åtkomstkontroll](/help/access-control/home.md#permissions). <br> ![Markera det identitetsnamnutrymme som är markerat i arbetsflödet för att aktivera målgrupper till mål.](/help/destinations/assets/overview/export-identities-to-destination.png "Markera det identitetsnamnutrymme som är markerat i arbetsflödet för att aktivera målgrupper till mål."){width="100" zoomable="yes"}

Läs [Aktivera profiler och målgrupper för att strömma målgruppernas exportdestinationer](/help/destinations/ui/activate-segment-streaming-destinations.md) för instruktioner om hur du aktiverar målgrupper till det här målet.

### Mappa överväganden och exempel {#mapping-considerations-example}

Så här skickar du målgruppsdata från Adobe Experience Platform till [!DNL (API) Salesforce Marketing Cloud] mål måste du gå igenom fältmappningssteget. Mappningen består av att skapa en länk mellan XDM-schemafälten (Experience Data Model) i ditt plattformskonto och motsvarande motsvarigheter från målmålet.

Mappa XDM-fälten korrekt till [!DNL (API) Salesforce Marketing Cloud] målfält, följ stegen nedan.

>[!IMPORTANT]
>
> * Även om attributnamnen är som du vill [!DNL Salesforce Marketing Cloud] konto, mappningar för båda `contactKey` och `personalEmail.address` är obligatoriska.
>
> * Integrationen med [!DNL Salesforce Marketing Cloud] API har en sidnumreringsgräns som anger hur många attribut Experience Platform kan hämta från Salesforce. Detta innebär att **[!UICONTROL Mapping]** målfältets schema kan visa högst 2 000 attribut från ditt Salesforce-konto.

1. I **[!UICONTROL Mapping]** steg, välja **[!UICONTROL Add new mapping]**. En ny mappningsrad visas på skärmen.
   ![Exempel på skärmbild för användargränssnittet för plattformen för att lägga till ny mappning.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/add-new-mapping.png)
1. I **[!UICONTROL Select source field]** väljer du **[!UICONTROL Select attributes]** och välj XDM-attributet eller välj **[!UICONTROL Select identity namespace]** och välj en identitet.
1. I **[!UICONTROL Select target field]** väljer du **[!UICONTROL Select identity namespace]** och välj en identitet eller välj **[!UICONTROL Select attributes]** och välj ett attribut bland de datatillägg som visas efter behov. The [!DNL (API) Salesforce Marketing Cloud] destinationen använder [!DNL Salesforce Marketing Cloud] [!DNL Search Attribute-Set Definitions REST] [API](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/retrieveAttributeSetDefinitions.html) att dynamiskt hämta datatilläggen och deras länkade attribut som definierats i [!DNL Salesforce Marketing Cloud]. Dessa visas i **[!UICONTROL Target field]** popup-fönster när du ställer in [mappning](#mapping-considerations-example) i [aktivera målgruppsarbetsflöde](#activate).

   * Upprepa dessa steg för att lägga till följande mappningar mellan XDM-profilschemat och [!DNL (API) Salesforce Marketing Cloud]:

     | Källfält | Målfält | Obligatoriskt |
     |---|---|---|
     | `IdentityMap: contactKey` | `Identity: salesforceContactKey` | `Mandatory` |
     | `xdm: personalEmail.address` | `Attribute: Email Address` från [!DNL Salesforce Marketing Cloud] [!DNL Email Addresses] datatillägg. | `Mandatory`när nya kontakter läggs till. |
     | `xdm: person.name.firstName` | `Attribute: First Name` från önskat [!DNL Salesforce Marketing Cloud] datatillägg. | – |

   * Ett exempel på hur du använder dessa mappningar visas nedan:
     ![Exempel på skärmbild för användargränssnittet för plattformen som visar målmappningar.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/mappings.png)

När du har angett mappningarna för målanslutningen väljer du **[!UICONTROL Next]**.

### Schemalägg målgruppsexport och exempel {#schedule-segment-export-example}

När du utför [Schemalägg målgruppsexport](/help/destinations/ui/activate-segment-streaming-destinations.md#scheduling) måste du manuellt mappa plattformsmålgrupper till [attributes](#prerequisites-attribute) in [!DNL Salesforce Marketing Cloud].

Det gör du genom att markera varje segment och sedan ange namnet på attributet från [!DNL Salesforce Marketing Cloud] i [!DNL (API) Salesforce Marketing Cloud] **[!UICONTROL Mapping ID]** fält. Se [Skapa attribut i [!DNL Salesforce Marketing Cloud]](#prerequisites-custom-field) för vägledning och bästa metoder för att skapa attribut i [!DNL Salesforce Marketing Cloud].

Om [!DNL Salesforce Marketing Cloud] attributet är `salesforce_mc_segment_1`anger du det här värdet i dialogrutan [!DNL (API) Salesforce Marketing Cloud] **[!UICONTROL Mapping ID]** för att fylla målgrupper från Experience Platform i detta attribut.

Ett exempelattribut från [!DNL Salesforce Marketing Cloud] visas nedan:
![Användargränssnittet i Salesforce Marketing Cloud med ett attribut.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/salesforce-custom-field.png)

Ett exempel som anger platsen för [!DNL (API) Salesforce Marketing Cloud] **[!UICONTROL Mapping ID]** visas nedan:
![Exempel på skärmbild för användargränssnittet för plattformen som visar export av schemalagda målgrupper.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/schedule-segment-export.png)

Som visas [!DNL (API) Salesforce Marketing Cloud] **[!UICONTROL Mapping ID]** ska exakt matcha värdet som anges i [!DNL Salesforce Marketing Cloud] **[!UICONTROL FIELD NAME]**.

Upprepa det här avsnittet för varje aktiverat plattformssegment.

Ett typiskt exempel baserat på bilden ovan kan vara.
| [!DNL (API) Salesforce Marketing Cloud] segmentnamn | [!DNL Salesforce Marketing Cloud] **[!UICONTROL FIELD NAME]** | [!DNL (API) Salesforce Marketing Cloud] **[!UICONTROL Mapping ID]** | | — | — | — | | salesforce mc målgrupp 1 | `salesforce_mc_segment_1` | `salesforce_mc_segment_1` | | salesforce mc målgrupp 2 | `salesforce_mc_segment_2` | `salesforce_mc_segment_2` |

## Validera dataexport {#exported-data}

Följ stegen nedan för att verifiera att du har konfigurerat målet korrekt:

1. Välj **[!UICONTROL Destinations]** > **[!UICONTROL Browse]** för att navigera till listan över destinationer.
   ![Skärmbild av användargränssnittet för plattformen med bläddringsmål.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/browse-destinations.png)

1. Markera målet och validera att statusen är **[!UICONTROL enabled]**.
   ![Skärmbild av användargränssnittet för plattformen med körning av måldataflöde.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/destination-dataflow-run.png)

1. Växla till **[!DNL Activation data]** väljer du ett målgruppsnamn.
   ![Skärmbild för användargränssnittet för plattformen visar aktiveringsdata för destinationer.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/destinations-activation-data.png)

1. Övervaka målgruppssammanfattningen och se till att antalet profiler motsvarar antalet som skapas inom segmentet.
   ![Exempel på skärmbild för plattformsgränssnitt som visar segment.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/segment.png)

1. Logga in på [[!DNL Salesforce Marketing Cloud]](https://mc.exacttarget.com/) webbplats. Navigera sedan till **[!DNL Audience Builder]** > **[!DNL Contact Builder]** > **[!DNL All contacts]** > **[!DNL Email]** och kontrollera om profilerna från målgruppen har lagts till.
   ![Användargränssnittet i Salesforce Marketing Cloud visar sidan Kontakter med profiler som används i segmentet.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/contacts.png)

1. Om du vill kontrollera om några profiler har uppdaterats går du till **[!UICONTROL Email]** och verifiera om attributvärdena för profilen från målgruppen har uppdaterats. Om det lyckas ser du att varje målgrupps status [!DNL Salesforce Marketing Cloud] uppdaterades med motsvarande målgruppsstatus från Platform, baserat på **[!UICONTROL Mapping ID]** värdet i [målgruppsplanering](#schedule-segment-export-example) steg.
   ![Användargränssnittet i Salesforce Marketing Cloud visar den valda e-postsidan för kontakter med uppdaterade målgruppsstatus.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/contact-detail.png)

## Dataanvändning och styrning {#data-usage-governance}

Alla [!DNL Adobe Experience Platform] destinationerna är kompatibla med dataanvändningsprinciper när data hanteras. Detaljerad information om hur [!DNL Adobe Experience Platform] använder datastyrning, se [Datastyrning - översikt](/help/data-governance/home.md).

## Fel och felsökning {#errors-and-troubleshooting}

### Okända fel påträffades när händelser skickades till Salesforce Marketing Cloud {#unknown-errors}

* När du kontrollerar ett dataflöde kan följande felmeddelande visas: `Unknown errors encountered while pushing events to the destination. Please contact the administrator and try again.`
  ![Skärmbild för användargränssnittet för plattformen visar ett fel.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/error.png)

   * Du kan åtgärda felet genom att kontrollera att **[!UICONTROL Mapping ID]** som du angav i aktiveringsarbetsflödet för [!DNL (API) Salesforce Marketing Cloud] målet matchar exakt namnet på attributet som du skapade i [!DNL Salesforce Marketing Cloud]. Se [Skapa attribut i [!DNL Salesforce Marketing Cloud]](#prerequisites-custom-field) för vägledning.

* När du aktiverar ett segment kan du få ett felmeddelande: `The client's IP address is unauthorized for this account. Allowlist the client's IP address...`
   * Om du vill åtgärda felet kontaktar du [!DNL Salesforce Marketing Cloud] kontoadministratör att lägga till [Experience Platform IP-adresser](/help/destinations/catalog/streaming/ip-address-allow-list.md) till [!DNL Salesforce Marketing Cloud] kontots betrodda IP-intervall. Se [!DNL Salesforce Marketing Cloud] [IP-adresser som ska inkluderas på Tillåtelselista i Marketing Cloud](https://help.salesforce.com/s/articleView?id=sf.mc_es_ip_addresses_for_inclusion.htm&amp;type=5) dokumentation om du behöver ytterligare vägledning.

## Ytterligare resurser {#additional-resources}

* [!DNL Salesforce Marketing Cloud] [API](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/apis-overview.html)
* [!DNL Salesforce Marketing Cloud] [dokumentation](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/updateContacts.html) förklarar hur kontakter uppdateras med den angivna informationen.

### Changelog {#changelog}

I det här avsnittet beskrivs funktionaliteten och viktiga dokumentationsuppdateringar för den här målanslutningen.

+++ Visa ändringslogg

| Releasamånad | Uppdateringstyp | Beskrivning |
|---|---|---|
| Oktober 2023 | Dokumentation - uppdatering | <ul><li>Vi uppdaterade [Förutsättningar i (API) Salesforce Marketing Cloud](#prerequisites-destination) och i allmänhet har onödiga referenser till attributgrupper i dokumentet tagits bort.</li> <li>Uppdaterad dokumentation som anger att attribut för målgruppsstatus ska skapas i [!DNL Salesforce Marketing Cloud] innanför [!DNL Email Demographics] endast datatillägg.</li> <li>Vi uppdaterade mappningstabellen i [Mappa överväganden och exempel](#mapping-considerations-example) -avsnitt, mappning för `Email Address` -attribut i `Email Addresses` Datatillägget är markerat som obligatoriskt. Detta krav omnämndes i den pratbubbla som är markerad som VIKTIGT, men utelämnades från tabellen.</li></ul> |
| April 2023 | Dokumentation - uppdatering | <ul><li>Vi korrigerade en instruktion och en referenslänk i [Förutsättningar i (API) Salesforce Marketing Cloud](#prerequisites-destination) för att ta reda på det [!DNL Salesforce Marketing Cloud Engagement] är en obligatorisk prenumeration för att använda den här destinationen. Avsnittet som tidigare felaktigt anropade att användare behöver en prenumeration på Marketing Cloud **Konto** Åtagande att fortsätta.</li> <li>Vi lade till ett avsnitt under [krav](#prerequisites) for [roller och behörigheter](#prerequisites-roles-permissions) som ska tilldelas [!DNL Salesforce] för att den här destinationen ska fungera. (PLATIR-26299)</li></ul> |
| Februari 2023 | Dokumentation - uppdatering | Vi uppdaterade [Förutsättningar i (API) Salesforce Marketing Cloud](#prerequisites-destination) -avsnitt som ska innehålla en referenslänk som anropar den [!DNL Salesforce Marketing Cloud Engagement] är en obligatorisk prenumeration för att använda den här destinationen. |
| Februari 2023 | Funktionsuppdatering | Vi har åtgärdat ett problem där en felaktig konfiguration i målet orsakade att ett felaktigt JSON skickades till Salesforce. Detta resulterade i att ett stort antal identiteter inte kunde aktiveras. (PLATIR-26299) |
| Januari 2023 | Dokumentation - uppdatering | <ul><li>Vi uppdaterade [Krav [!DNL Salesforce]](#prerequisites-destination) för att ta reda på att attribut måste skapas i [!DNL Salesforce] sida. Det här avsnittet innehåller nu detaljerade anvisningar om hur du gör det och de bästa sätten att namnge attributen i [!DNL Salesforce]. (PLATIR-25602)</li><li>Vi har lagt till tydliga instruktioner om hur du använder mappnings-ID för varje aktiverad målgrupp i [målgruppsplanering](#schedule-segment-export-example) steg. (PLATIR-25602)</li></ul> |
| Oktober 2022 | Inledande version | Ursprunglig målversion och dokumentationspublicering. |

{style="table-layout:auto"}

+++
