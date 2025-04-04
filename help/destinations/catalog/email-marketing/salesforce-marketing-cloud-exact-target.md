---
title: (API) Salesforce Marketing Cloud-anslutning
description: Med Salesforce Marketing Cloud-destinationen (tidigare ExactTarget) kan du exportera dina kontodata och aktivera dem inom Salesforce Marketing Cloud för dina affärsbehov.
exl-id: 0cf068e6-8a0a-4292-a7ec-c40508846e27
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '2824'
ht-degree: 1%

---

# [!DNL (API) Salesforce Marketing Cloud]-anslutning

## Översikt {#overview}

[[!DNL (API) Salesforce Marketing Cloud]](https://www.salesforce.com/products/marketing-cloud/engagement/) (tidigare kallat [!DNL ExactTarget]) är en digital marknadsföringssvit som gör att du kan skapa och anpassa resor för besökare och kunder för att anpassa deras upplevelse.

>[!IMPORTANT]
>
> Observera skillnaden mellan den här anslutningen och den andra [[!DNL Salesforce Marketing Cloud] anslutningen](/help/destinations/catalog/email-marketing/salesforce-marketing-cloud.md) som finns i katalogavsnittet E-postmarknadsföring. Med den andra Salesforce Marketing Cloud-anslutningen kan du exportera filer till en angiven lagringsplats, medan detta är en API-baserad direktuppspelningsanslutning.

Jämfört med [!DNL Salesforce Marketing Cloud Account Engagement], som är mer inriktad på **B2B**-marknadsföring, är [!DNL (API) Salesforce Marketing Cloud]-målet idealiskt för **B2C**-användningsfall med kortare beslutscykler för transaktioner. Du kan konsolidera större datauppsättningar som representerar målgruppens beteende för att justera och förbättra marknadsföringskampanjer genom att prioritera och segmentera kontakter, särskilt från datauppsättningar utanför [!DNL Salesforce]. *Obs! Experience Platform har också en anslutning för [[!DNL Salesforce Marketing Cloud Account Engagement]](/help/destinations/catalog/email-marketing/salesforce-marketing-cloud-account-engagement.md).*

Det här [!DNL Adobe Experience Platform] [målet](/help/destinations/home.md) använder API:t [!DNL Salesforce Marketing Cloud] [Uppdatera kontakter](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/updateContacts.html) som gör att du kan **lägga till kontakter och uppdatera kontaktdata** för dina affärsbehov efter att du har aktiverat dem i ett nytt [!DNL Salesforce Marketing Cloud]-segment.

[!DNL Salesforce Marketing Cloud] använder OAuth 2 med klientautentiseringsuppgifter som autentiseringsmekanism för att kommunicera med [!DNL Salesforce Marketing Cloud] API. Instruktioner för autentisering till din [!DNL Salesforce Marketing Cloud]-instans finns längre ned i avsnittet [Autentisera till mål](#authenticate).

## Användningsfall {#use-cases}

För att du bättre ska kunna förstå hur och när du ska använda målet [!DNL (API) Salesforce Marketing Cloud] finns det ett exempel på användning som Adobe Experience Platform-kunder kan lösa genom att använda det här målet.

### Skicka e-post till kontakter för marknadsföringskampanjer {#use-case-send-emails}

Försäljningsavdelningen på en uthyrningsplattform vill sända ett marknadsföringsmejl till en målgrupp. Plattformens marknadsföringsteam kan lägga till nya kontakter/uppdatera befintliga kontakter *(och deras e-postadresser)* via Adobe Experience Platform, bygga målgrupper utifrån deras egna offlinedata och skicka dessa målgrupper till [!DNL Salesforce Marketing Cloud] som sedan kan användas för att skicka marknadsföringskampanjens e-post.

## Förhandskrav {#prerequisites}

### Förutsättningar i Experience Platform {#prerequisites-in-experience-platform}

Innan du aktiverar data till målet [!DNL (API) Salesforce Marketing Cloud] måste du ha ett [schema](/help/xdm/schema/composition.md), en [datamängd](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html) och [segment](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html) som skapats i [!DNL Experience Platform].

### Förutsättningar i [!DNL (API) Salesforce Marketing Cloud] {#prerequisites-destination}

Observera följande krav för att kunna exportera data från Experience Platform till ditt [!DNL Salesforce Marketing Cloud]-konto:

#### Du måste ha ett [!DNL Salesforce Marketing Cloud]-konto {#prerequisites-account}

Ett [!DNL Salesforce Marketing Cloud]-konto med en prenumeration på [[!DNL Marketing Cloud Engagement]](https://www.salesforce.com/products/marketing-cloud/engagement/)-produkten är obligatoriskt för att fortsätta.

Kontakta [[!DNL Salesforce] support](https://www.salesforce.com/company/contact-us/?d=cta-glob-footer-10) om du inte har något [!DNL Salesforce Marketing Cloud]-konto eller om ditt konto saknar produktprenumerationen [!DNL Marketing Cloud Engagement].

#### Skapa attribut i [!DNL Salesforce Marketing Cloud] {#prerequisites-attribute}

När du aktiverar målgrupper till målet [!DNL (API) Salesforce Marketing Cloud] måste du ange ett värde i fältet **[!UICONTROL Mapping ID]** för varje aktiverad målgrupp i steget **[Målgruppsschema](#schedule-segment-export-example)**.

[!DNL Salesforce] kräver det här värdet för att läsa och tolka målgrupper som kommer från Experience Platform korrekt och för att uppdatera deras målgruppsstatus inom [!DNL Salesforce Marketing Cloud]. Se Experience Platform-dokumentationen för schemafältgruppen [Information om målgruppsmedlemskap](/help/xdm/field-groups/profile/segmentation.md) om du behöver vägledning om målgruppsstatus.

För varje målgrupp som du aktiverar från Experience Platform till [!DNL Salesforce] måste du ha ett attribut av typen `Text` länkat till datatillägget [!DNL Email Demographics] i [!DNL Salesforce Marketing Cloud]. Använd [!DNL Salesforce Marketing Cloud] [!DNL Contact Builder] för att skapa attribut. Läs [!DNL Salesforce Marketing Cloud]-dokumentationen om du vill [skapa attribut](https://help.salesforce.com/s/articleView?id=mc_cab_create_an_attribute.htm&amp;type=5&amp;language=en_US) om du behöver hjälp med att skapa attribut.

Attributfältsnamnen används för målfältet [!DNL (API) Salesforce Marketing Cloud] under steget **[!UICONTROL Mapping]**. Du kan definiera fälttecknet med högst 4 000 tecken, beroende på dina affärsbehov. Mer information om attributtyper finns på dokumentationssidan [!DNL Salesforce Marketing Cloud] [Datatilläggsdatatyper](https://help.salesforce.com/s/articleView?id=sf.mc_es_data_extension_data_types.htm&amp;type=5) .

Ett exempel på datadesignerskärmen i [!DNL Salesforce Marketing Cloud] där du ska lägga till attributet visas nedan:
![ Salesforce Marketing Cloud UI data designer.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/salesforce-data-designer.png)

En vy över en [!DNL Salesforce Marketing Cloud] [!DNL Email Data]-attributgrupp med attribut som motsvarar målgruppens status i datatillägget [!DNL Email Demographics] visas nedan:
![Salesforce Marketing Cloud UI email data attribute group.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/salesforce-email-demographics-fields.png)

Målet [!DNL (API) Salesforce Marketing Cloud] använder [!DNL Salesforce Marketing Cloud] [!DNL Search Attribute-Set Definitions REST] [ API](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/retrieveAttributeSetDefinitions.html) för att dynamiskt hämta datatilläggen och deras länkade attribut som definierats i [!DNL Salesforce Marketing Cloud].

Dessa visas i urvalsfönstret **[!UICONTROL Target field]** när du ställer in [mappningen](#mapping-considerations-example) i arbetsflödet för att [aktivera målgrupper till målet](#activate).

>[!IMPORTANT]
>
> Inom [!DNL Salesforce Marketing Cloud] måste du skapa attribut med en **[!UICONTROL FIELD NAME]** som exakt matchar värdet som anges i **[!UICONTROL Mapping ID]** för varje aktiverat Experience Platform-segment. Skärmbilden nedan visar till exempel attributet `salesforce_mc_segment_1`. När du aktiverar en målgrupp på det här målet lägger du till `salesforce_mc_segment_1` som **[!UICONTROL Mapping ID]** för att fylla målgrupper från Experience Platform i det här attributet.

Ett exempel på hur du skapar attribut i [!DNL Salesforce Marketing Cloud] visas nedan:
![Salesforce Marketing Cloud UI, skärmbild som visar ett attribut.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/salesforce-custom-field.png)

>[!TIP]
>
> * När du skapar attributet ska du inte ta med blankstegstecken i fältnamnet. Använd i stället understrecket `(_)` som avgränsare.
> * Om du vill skilja mellan attribut som används för Experience Platform-målgrupper och andra attribut inom [!DNL Salesforce Marketing Cloud] kan du inkludera ett identifierbart prefix eller suffix för de attribut som används för Adobe-segment. Använd till exempel `Adobe_test_segment` eller `test_segment_Adobe` i stället för `test_segment`.
> * Om du redan har andra attribut skapade i [!DNL Salesforce Marketing Cloud] kan du använda samma namn som Experience Platform-segmentet för att enkelt identifiera målgruppen i [!DNL Salesforce Marketing Cloud].

#### Tilldela användarroller och behörigheter i [!DNL Salesforce Marketing Cloud] {#prerequisites-roles-permissions}

Eftersom [!DNL Salesforce Marketing Cloud] har stöd för anpassade roller beroende på ditt användningsfall, bör din användare tilldelas de relevanta rollerna för att uppdatera dina attribut i [!DNL Salesforce Marketing Cloud]. Ett exempel på roller som tilldelats en användare visas nedan:
![Salesforce Marketing Cloud-gränssnitt för en vald användare som visar sina tilldelade roller.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/salesforce-edit-roles.png)

Beroende på vilka roller din [!DNL Salesforce Marketing Cloud]-användare har tilldelats, måste du även tilldela behörigheter till datatillägget [!DNL Salesforce Marketing Cloud] som är länkade till de fält som du vill uppdatera.

Eftersom det här målet kräver åtkomst till `[!DNL data extension]` måste du tillåta dem. Till exempel för `Email` [!DNL data extension] som du måste tillåta enligt nedan:

![Användargränssnittet i Salesforce Marketing Cloud visar e-postdatatillägget med tillåtna behörigheter.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/salesforce-permisions-list.png)

Om du vill begränsa åtkomstnivån kan du även åsidosätta individuell åtkomst genom att använda detaljerade behörigheter.
![Användargränssnittet i Salesforce Marketing Cloud visar e-postdatatillägget med detaljerad behörighet.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/sales-email-attribute-set-permission.png)

Mer information finns på sidorna [[!DNL Marketing Cloud Roles]](https://help.salesforce.com/s/articleView?language=en_US&amp;id=sf.mc_overview_marketing_cloud_roles.htm&amp;type=5) och [[!DNL Marketing Cloud Roles and Permissions]](https://help.salesforce.com/s/articleView?language=en_US&amp;id=sf.mc_overview_roles.htm&amp;type=5).

#### Samla in inloggningsuppgifter för [!DNL Salesforce Marketing Cloud] {#gather-credentials}

Anteckna objekten nedan innan du autentiserar till målet [!DNL (API) Salesforce Marketing Cloud].

| Autentiseringsuppgifter | Beskrivning | Exempel |
| --- | --- | --- |
| Underdomän | Mer information om hur du hämtar det här värdet från gränssnittet [!DNL Salesforce Marketing Cloud] finns i [[!DNL Salesforce Marketing Cloud domain prefix]](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/your-subdomain-tenant-specific-endpoints.html). | Om din [!DNL Salesforce Marketing Cloud]-domän är <br> *`mcq4jrssqdlyc4lph19nnqgzzs84`.login.exactarget.com*, <br>du måste ange `mcq4jrssqdlyc4lph19nnqgzzs84` som värde. |
| Klient-ID | Läs [!DNL Salesforce Marketing Cloud] [documentation](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/access-token-s2s.html) om du vill veta hur du hämtar det här värdet från gränssnittet [!DNL Salesforce Marketing Cloud]. | r23kxxxxxx0z05xxxx |
| Klienthemlighet | Läs [!DNL Salesforce Marketing Cloud] [documentation](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/access-token-s2s.html) om du vill veta hur du hämtar det här värdet från gränssnittet [!DNL Salesforce Marketing Cloud]. | ipxxxxxxxxxxT4xxxxxxxx |

{style="table-layout:auto"}

### Guardrails {#guardrails}

* Salesforce tillämpar vissa [hastighetsbegränsningar](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/rate-limiting.html).
   * Läs [!DNL Salesforce Marketing Cloud] [dokumentation](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/rate-limiting-errors.html) om du vill åtgärda eventuella begränsningar som kan uppstå och minska antalet fel under körningen.
   * Gå till sidan [[!DNL Salesforce Marketing Cloud] Åtagandepriser](https://www.salesforce.com/editions-pricing/marketing-cloud/email/) för att *hämta jämförelsetabellen med fullständiga utgåvor* som en pdf som innehåller information om de begränsningar som din plan innebär.
   * Sidan [API-översikt](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/apis-overview.html) innehåller ytterligare begränsningar.
   * Gå till [här](https://salesforce.stackexchange.com/questions/205898/marketing-cloud-api-limits) för en sida som samlar in dessa uppgifter.
* Antalet *anpassade fält som tillåts per objekt* varierar beroende på din Salesforce Edition.
   * Mer information finns i [!DNL Salesforce] [dokumentationen](https://help.salesforce.com/s/articleView?id=sf.custom_field_allocations.htm&amp;type=5).
   * Om du har nått gränsen som definierats för *anpassade fält som tillåts per objekt* inom [!DNL Salesforce Marketing Cloud] måste du
      * Ta bort äldre attribut innan du lägger till nya attribut i [!DNL Salesforce Marketing Cloud].
      * Uppdatera eller ta bort aktiverade målgrupper i Experience Platform-mål som använder dessa äldre attributnamn som det värde som anges för **[!UICONTROL Mapping ID]** under steget [målgruppsplanering](#schedule-segment-export-example).

## Identiteter som stöds {#supported-identities}

[!DNL (API) Salesforce Marketing Cloud] stöder aktivering av identiteter som beskrivs i tabellen nedan. Läs mer om [identiteter](/help/identity-service/features/namespaces.md).

| Målidentitet | Beskrivning | Överväganden |
|---|---|---|
| contactKey | [!DNL Salesforce Marketing Cloud] Kontaktnyckel. Mer information finns i [!DNL Salesforce Marketing Cloud] [dokumentationen](https://help.salesforce.com/s/articleView?id=sf.mc_cab_contact_builder_best_practices.htm&amp;type=5) om du behöver ytterligare vägledning. | Obligatoriskt |

## Målgrupper {#supported-audiences}

I det här avsnittet beskrivs vilka typer av målgrupper du kan exportera till det här målet.

| Målgruppsursprung | Stöds | Beskrivning |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Publiker som genererats via Experience Platform [segmenteringstjänst](../../../segmentation/home.md). |
| Anpassade överföringar | X | Publikerna [importerade](../../../segmentation/ui/audience-portal.md#import-audience) till Experience Platform från CSV-filer. |

{style="table-layout:auto"}

## Exportera typ och frekvens {#export-type-frequency}

Se tabellen nedan för information om exporttyp och frekvens för destinationen.

| Objekt | Typ | Anteckningar |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Profile-based]** | <ul><li>Du exporterar alla medlemmar i ett segment, tillsammans med de önskade schemafälten *(till exempel e-postadress, telefonnummer, efternamn)*, enligt fältmappningen.</li><li> Varje segmentstatus i [!DNL Salesforce Marketing Cloud] uppdateras med motsvarande målgruppsstatus från Experience Platform, baserat på det **[!UICONTROL Mapping ID]**-värde som angavs under [målgruppsplaneringssteget](#schedule-segment-export-example).</li></ul> |
| Exportfrekvens | **[!UICONTROL Streaming]** | Direktuppspelningsmål är alltid på API-baserade anslutningar. Så snart en profil uppdateras i Experience Platform baserat på målgruppsutvärdering skickar anslutningsprogrammet uppdateringen nedströms till målplattformen. Läs mer om [direktuppspelningsmål](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Anslut till målet {#connect}

>[!IMPORTANT]
>
> Om du vill ansluta till målet måste du ha **[!UICONTROL Manage Destinations]** [åtkomstkontrollbehörighet](/help/access-control/home.md#permissions). Läs [åtkomstkontrollsöversikten](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få den behörighet som krävs.

Om du vill ansluta till det här målet följer du stegen som beskrivs i självstudiekursen [för destinationskonfiguration](../../ui/connect-destination.md). I arbetsflödet för att konfigurera mål fyller du i fälten som listas i de två avsnitten nedan.

Sök efter [!DNL (API) Salesforce Marketing Cloud] inom **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]**. Du kan också hitta den under kategorin **[!UICONTROL Email marketing]**.

### Autentisera till mål {#authenticate}

Om du vill autentisera mot målet fyller du i de obligatoriska fälten nedan och väljer **[!UICONTROL Connect to destination]**. Mer information finns i avsnittet [Samla [!DNL Salesforce Marketing Cloud] inloggningsuppgifter](#gather-credentials).

| [!DNL (API) Salesforce Marketing Cloud] mål | [!DNL Salesforce Marketing Cloud] |
| --- | --- |
| **[!UICONTROL Subdomain]** | Domänprefixet [!DNL Salesforce Marketing Cloud]. <br>Om din domän till exempel är <br> *`mcq4jrssqdlyc4lph19nnqgzzs84`.login.exactarget.com*, <br> du måste ange `mcq4jrssqdlyc4lph19nnqgzzs84` som värde. |
| **[!UICONTROL Client ID]** | Din [!DNL Salesforce Marketing Cloud] `Client ID`. |
| **[!UICONTROL Client Secret]** | Din [!DNL Salesforce Marketing Cloud] `Client Secret`. |

![Experience Platform-användargränssnitt som visar hur du autentiserar till Salesforce Marketing Cloud.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/authenticate-destination.png)

Om den angivna informationen är giltig visar gränssnittet **[!UICONTROL Connected]**-status med en grön bockmarkering, och du kan sedan fortsätta till nästa steg.

### Fyll i målinformation {#destination-details}

Om du vill konfigurera information för målet fyller du i de obligatoriska och valfria fälten nedan. En asterisk bredvid ett fält i användargränssnittet anger att fältet är obligatoriskt.
![Experience Platform UI-skärmbild med målinformation.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/destination-details.png)

* **[!UICONTROL Name]**: Ett namn som du känner igen det här målet med i framtiden.
* **[!UICONTROL Description]**: En beskrivning som hjälper dig att identifiera det här målet i framtiden.

### Aktivera aviseringar {#enable-alerts}

Du kan aktivera varningar för att få meddelanden om dataflödets status till ditt mål. Välj en avisering i listan om du vill prenumerera och få meddelanden om statusen för ditt dataflöde. Mer information om varningar finns i guiden [prenumerera på destinationsvarningar med användargränssnittet](../../ui/alerts.md).

Välj **[!UICONTROL Next]** när du är klar med att ange information för målanslutningen.

## Aktivera målgrupper till det här målet {#activate}

>[!IMPORTANT]
> 
> * För att aktivera data behöver du behörigheterna **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** och **[!UICONTROL View Segments]** [åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontrollsöversikten](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få den behörighet som krävs.
> * Om du vill exportera *identiteter* måste du ha **[!UICONTROL View Identity Graph]** [åtkomstkontrollbehörighet](/help/access-control/home.md#permissions). <br> ![Markera identitetsnamnområdet som är markerat i arbetsflödet för att aktivera målgrupper till mål.](/help/destinations/assets/overview/export-identities-to-destination.png "Markera identitetsnamnområdet som är markerat i arbetsflödet för att aktivera målgrupper till mål."){width="100" zoomable="yes"}

Läs [Aktivera profiler och målgrupper för att direktuppspela målgruppsexportdestinationer](/help/destinations/ui/activate-segment-streaming-destinations.md) för instruktioner om hur du aktiverar målgrupper till det här målet.

### Mappa överväganden och exempel {#mapping-considerations-example}

Om du vill skicka målgruppsdata från Adobe Experience Platform till målet [!DNL (API) Salesforce Marketing Cloud] måste du gå igenom fältmappningssteget. Mappningen består av att skapa en länk mellan XDM-schemafälten (Experience Data Model) i ditt Experience Platform-konto och deras motsvarande motsvarigheter från målmålet.

Följ stegen nedan för att mappa dina XDM-fält till målfälten för [!DNL (API) Salesforce Marketing Cloud] korrekt.

>[!IMPORTANT]
>
> * Även om dina attributnamn är som de är för ditt [!DNL Salesforce Marketing Cloud]-konto är mappningarna för både `contactKey` och `personalEmail.address` obligatoriska.
>
> * Integrationen med [!DNL Salesforce Marketing Cloud]-API:t har en sidnumreringsgräns för hur många attribut Experience Platform kan hämta från Salesforce. Detta innebär att målfältschemat kan visa högst 2 000 attribut från ditt Salesforce-konto under steget **[!UICONTROL Mapping]**.

1. Välj **[!UICONTROL Add new mapping]** i steget **[!UICONTROL Mapping]**. En ny mappningsrad visas på skärmen.
   ![Experience Platform UI, skärmbild för Lägg till ny mappning.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/add-new-mapping.png)
1. Välj kategorin **[!UICONTROL Select attributes]** i fönstret **[!UICONTROL Select source field]** och markera XDM-attributet eller välj **[!UICONTROL Select identity namespace]** och välj en identitet.
1. I fönstret **[!UICONTROL Select target field]** väljer du **[!UICONTROL Select identity namespace]** och väljer en identitet eller en **[!UICONTROL Select attributes]**-kategori och väljer ett attribut bland de datatillägg som visas efter behov. Målet [!DNL (API) Salesforce Marketing Cloud] använder [!DNL Salesforce Marketing Cloud] [!DNL Search Attribute-Set Definitions REST] [ API](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/retrieveAttributeSetDefinitions.html) för att dynamiskt hämta datatilläggen och deras länkade attribut som definierats i [!DNL Salesforce Marketing Cloud]. Dessa visas i popup-fönstret **[!UICONTROL Target field]** när du konfigurerar [mappningen](#mapping-considerations-example) i arbetsflödet [aktivera målgrupper](#activate).

   * Upprepa de här stegen för att lägga till följande mappningar mellan XDM-profilschemat och [!DNL (API) Salesforce Marketing Cloud]:

     | Source Field | Målfält | Obligatoriskt |
     |---|---|---|
     | `IdentityMap: contactKey` | `Identity: salesforceContactKey` | `Mandatory` |
     | `xdm: personalEmail.address` | `Attribute: Email Address` från datatillägget [!DNL Salesforce Marketing Cloud] [!DNL Email Addresses]. | `Mandatory` när nya kontakter läggs till. |
     | `xdm: person.name.firstName` | `Attribute: First Name` från det önskade datatillägget [!DNL Salesforce Marketing Cloud]. | – |

   * Ett exempel på hur du använder dessa mappningar visas nedan:
     ![Exempel på skärmbild i Experience Platform UI som visar målmappningar.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/mappings.png)

När du har angett mappningarna för målanslutningen väljer du **[!UICONTROL Next]**.

### Schemalägg målgruppsexport och exempel {#schedule-segment-export-example}

När du utför steget [Schemalägg målgruppsexport](/help/destinations/ui/activate-segment-streaming-destinations.md#scheduling) måste du manuellt mappa Experience Platform-målgrupper till [attributen](#prerequisites-attribute) i [!DNL Salesforce Marketing Cloud].

Det gör du genom att markera varje segment och sedan ange attributets namn från [!DNL Salesforce Marketing Cloud] i fältet [!DNL (API) Salesforce Marketing Cloud] **[!UICONTROL Mapping ID]**. Mer information om hur du skapar attribut i [!DNL Salesforce Marketing Cloud] finns i avsnittet [Skapa attribut i [!DNL Salesforce Marketing Cloud]](#prerequisites-custom-field).

Om attributet [!DNL Salesforce Marketing Cloud] till exempel är `salesforce_mc_segment_1` anger du det här värdet i [!DNL (API) Salesforce Marketing Cloud] **[!UICONTROL Mapping ID]** för att fylla målgrupper från Experience Platform i det här attributet.

Ett exempelattribut från [!DNL Salesforce Marketing Cloud] visas nedan:
![Salesforce Marketing Cloud UI, skärmbild som visar ett attribut.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/salesforce-custom-field.png)

Ett exempel som anger platsen för [!DNL (API) Salesforce Marketing Cloud] **[!UICONTROL Mapping ID]** visas nedan:

![Exempel på skärmbild i Experience Platform som visar export av schemalagda målgrupper.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/schedule-segment-export.png)

Så som visas ska [!DNL (API) Salesforce Marketing Cloud] **[!UICONTROL Mapping ID]** exakt matcha värdet som anges i [!DNL Salesforce Marketing Cloud] **[!UICONTROL FIELD NAME]**.

Upprepa det här avsnittet för varje aktiverat Experience Platform-segment.

Ett typiskt exempel baserat på bilden ovan kan vara.

| [!DNL (API) Salesforce Marketing Cloud] segmentnamn | [!DNL Salesforce Marketing Cloud] **[!UICONTROL FIELD NAME]** | [!DNL (API) Salesforce Marketing Cloud] **[!UICONTROL Mapping ID]** |
| --- | --- | --- |
| salesforce mc målgrupp 1 | `salesforce_mc_segment_1` | `salesforce_mc_segment_1` |
| salesforce mc målgrupp 2 | `salesforce_mc_segment_2` | `salesforce_mc_segment_2` |

## Validera dataexport {#exported-data}

Följ stegen nedan för att verifiera att du har konfigurerat målet korrekt:

1. Välj **[!UICONTROL Destinations]** > **[!UICONTROL Browse]** för att navigera till listan över mål.
   ![Experience Platform UI, skärmbild med Sök mål.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/browse-destinations.png)

1. Markera målet och validera att statusen är **[!UICONTROL enabled]**.
   ![Experience Platform UI, skärmbild med körning av måldataflöde.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/destination-dataflow-run.png)

1. Växla till fliken **[!DNL Activation data]** och välj sedan ett publiknamn.
   ![Exempel på skärmbild i Experience Platform UI som visar aktiveringsdata för destinationer.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/destinations-activation-data.png)

1. Övervaka målgruppssammanfattningen och se till att antalet profiler motsvarar antalet som skapas inom segmentet.
   ![Exempel på skärmbild i Experience Platform UI som visar segment.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/segment.png)

1. Logga in på webbplatsen [[!DNL Salesforce Marketing Cloud]](https://mc.exacttarget.com/). Gå sedan till sidan **[!DNL Audience Builder]** > **[!DNL Contact Builder]** > **[!DNL All contacts]** > **[!DNL Email]** och kontrollera om profilerna från målgruppen har lagts till.
   ![Salesforce Marketing Cloud användargränssnitt visar sidan Kontakter med profiler som används i segmentet.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/contacts.png)

1. Om du vill kontrollera om några profiler har uppdaterats går du till sidan **[!UICONTROL Email]** och kontrollerar om attributvärdena för profilen från målgruppen har uppdaterats. Om det lyckas kan du se att varje målgruppsstatus i [!DNL Salesforce Marketing Cloud] har uppdaterats med motsvarande målgruppsstatus från Experience Platform, baserat på värdet **[!UICONTROL Mapping ID]** som anges i steget [målgruppsplanering](#schedule-segment-export-example).
   ![Salesforce Marketing Cloud UI, skärmbild som visar den valda e-postsidan för kontakter med uppdaterade målgruppsstatus.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/contact-detail.png)

## Dataanvändning och styrning {#data-usage-governance}

Alla [!DNL Adobe Experience Platform]-mål är kompatibla med dataanvändningsprinciper när data hanteras. Mer information om hur [!DNL Adobe Experience Platform] använder datastyrning finns i [Datastyrningsöversikten](/help/data-governance/home.md).

## Fel och felsökning {#errors-and-troubleshooting}

### Okända fel påträffades när händelser skickades till Salesforce Marketing Cloud {#unknown-errors}

* När du kontrollerar ett dataflöde kan följande felmeddelande visas: `Unknown errors encountered while pushing events to the destination. Please contact the administrator and try again.`
  ![Experience Platform UI-skärmbild visar ett fel.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/error.png)

   * Om du vill åtgärda det här felet kontrollerar du att **[!UICONTROL Mapping ID]** som du angav i aktiveringsarbetsflödet till [!DNL (API) Salesforce Marketing Cloud]-målet exakt matchar namnet på attributet som du skapade i [!DNL Salesforce Marketing Cloud]. Mer information finns i avsnittet [Skapa attribut i [!DNL Salesforce Marketing Cloud]](#prerequisites-custom-field).

* När du aktiverar ett segment kan du få ett felmeddelande: `The client's IP address is unauthorized for this account. Allowlist the client's IP address...`
   * Om du vill åtgärda det här felet kontaktar du kontoadministratören för [!DNL Salesforce Marketing Cloud] och lägger till [Experience Platform IP-adresser](/help/destinations/catalog/streaming/ip-address-allow-list.md) i [!DNL Salesforce Marketing Cloud]-kontonas betrodda IP-intervall. Om du behöver ytterligare hjälp kan du läsa [!DNL Salesforce Marketing Cloud] [IP-adresser för Inkludering på Tillåtelselista i Marketing Cloud](https://help.salesforce.com/s/articleView?id=sf.mc_es_ip_addresses_for_inclusion.htm&amp;type=5) -dokumentationen.

## Ytterligare resurser {#additional-resources}

* [!DNL Salesforce Marketing Cloud] [API](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/apis-overview.html)
* [!DNL Salesforce Marketing Cloud] [dokumentation](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/updateContacts.html) som förklarar hur kontakter uppdateras med den angivna informationen.

### Changelog {#changelog}

I det här avsnittet beskrivs funktionaliteten och viktiga dokumentationsuppdateringar för den här målanslutningen.

+++ Visa ändringslogg

| Releasamånad | Uppdateringstyp | Beskrivning |
|---|---|---|
| Oktober 2023 | Uppdatering av dokumentation | <ul><li>Vi har uppdaterat avsnittet [Krav i (API) Salesforce Marketing Cloud](#prerequisites-destination) och har i allmänhet tagit bort onödiga referenser till attributgrupper i hela dokumentet.</li> <li>Uppdaterad dokumentation som anger att attribut för målgruppsstatus endast ska skapas inom [!DNL Salesforce Marketing Cloud] inuti datatillägget [!DNL Email Demographics].</li> <li>Mappningstabellen i avsnittet [Mappningsöverväganden och exempel](#mapping-considerations-example) har uppdaterats. Mappningen för attributet `Email Address` i datatillägget `Email Addresses` har markerats som obligatorisk. Detta krav nämndes i bildtexten som är markerad som VIKTIGT, men utelämnades från tabellen.</li></ul> |
| April 2023 | Uppdatering av dokumentation | <ul><li>Vi har korrigerat en instruktions- och referenslänk i API:t (Salesforce Marketing Cloud ](#prerequisites-destination)) för att anropa att [!DNL Salesforce Marketing Cloud Engagement] är en obligatorisk prenumeration för att kunna använda det här målet. [ Avsnittet som tidigare anropade felaktigt att användare behöver en prenumeration på Marketing Cloud **Account** för att kunna fortsätta.</li> <li>Vi lade till ett avsnitt under [Krav](#prerequisites) för [roller och behörigheter](#prerequisites-roles-permissions) som ska tilldelas [!DNL Salesforce]-användaren för att det här målet ska fungera. (PLATIR-26299)</li></ul> |
| Februari 2023 | Uppdatering av dokumentation | Vi har uppdaterat avsnittet [Krav i (API) Salesforce Marketing Cloud](#prerequisites-destination) så att det innehåller en referenslänk som anropar att [!DNL Salesforce Marketing Cloud Engagement] är en obligatorisk prenumeration för att kunna använda det här målet. |
| Februari 2023 | Funktionsuppdatering | Ett problem har korrigerats där en felaktig konfiguration i målet orsakade att ett felaktigt JSON skickades till Salesforce. Detta resulterade i att ett stort antal identiteter inte kunde aktiveras. (PLATIR-26299) |
| Januari 2023 | Uppdatering av dokumentation | <ul><li>Vi har uppdaterat avsnittet [Krav i [!DNL Salesforce]](#prerequisites-destination) för att anropa att attribut måste skapas på sidan [!DNL Salesforce]. Det här avsnittet innehåller nu detaljerade anvisningar om hur du gör det och de bästa sätten att namnge attributen i [!DNL Salesforce]. (PLATIR-25602)</li><li>Vi har lagt till tydliga instruktioner om hur du använder mappnings-ID för varje aktiverad målgrupp i steget [målgruppsplanering](#schedule-segment-export-example). (PLATIR-25602)</li></ul> |
| Oktober 2022 | Inledande version | Ursprunglig målversion och dokumentationspublicering. |

{style="table-layout:auto"}

+++
