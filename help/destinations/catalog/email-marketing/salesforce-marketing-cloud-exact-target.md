---
keywords: e-post;E-post;e-post;e-postmål;salesforce;api salesforce marketing cloud destination
title: (API) Salesforce Marketing Cloud-anslutning
description: Med Salesforce Marketing Cloud (tidigare ExactTarget) kan du exportera dina kontodata och aktivera dem i Salesforce Marketing Cloud för dina affärsbehov.
exl-id: 0cf068e6-8a0a-4292-a7ec-c40508846e27
source-git-commit: 017ccadc1689663059aa1214c5440549b509e81b
workflow-type: tm+mt
source-wordcount: '2527'
ht-degree: 1%

---

# [!DNL (API) Salesforce Marketing Cloud] anslutning

## Översikt {#overview}

[[!DNL (API) Salesforce Marketing Cloud]](https://www.salesforce.com/products/marketing-cloud/overview/) (tidigare känt som [!DNL ExactTarget]) är en digital marknadsföringssvit som gör att ni kan skapa och anpassa resor för besökare och kunder för att personalisera deras upplevelse.

>[!IMPORTANT]
>
>Observera skillnaden mellan den här anslutningen och den andra [[!DNL Salesforce Marketing Cloud] anslutning](/help/destinations/catalog/email-marketing/salesforce-marketing-cloud.md) som finns i katalogavsnittet E-postmarknadsföring. Med den andra Salesforce Marketing Cloud-anslutningen kan du exportera filer till en angiven lagringsplats, medan detta är en API-baserad direktuppspelningsanslutning.

Detta [!DNL Adobe Experience Platform] [mål](/help/destinations/home.md) utnyttjar [!DNL Salesforce Marketing Cloud] [uppdatera kontakter](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/updateContacts.html) API, som gör att du kan **lägga till kontakter och uppdatera kontaktdata** efter att ha aktiverat dem i en ny [!DNL Salesforce Marketing Cloud] segment.

[!DNL Salesforce Marketing Cloud] använder OAuth 2 med klientautentiseringsuppgifter som autentiseringsmekanism för att kommunicera med [!DNL Salesforce Marketing Cloud] API. Instruktioner för hur du autentiserar [!DNL Salesforce Marketing Cloud] -instansen är längre ned, i [Autentisera till mål](#authenticate) -avsnitt.

## Användningsfall {#use-cases}

För att du bättre ska förstå hur och när du ska använda [!DNL (API) Salesforce Marketing Cloud] mål, här är ett exempel på användning som Adobe Experience Platform-kunder kan lösa genom att använda den här destinationen.

### Skicka e-post till kontakter för marknadsföringskampanjer {#use-case-send-emails}

Försäljningsavdelningen på en uthyrningsplattform vill sända ett marknadsföringsmejl till en målgrupp. Plattformens marknadsföringsteam kan lägga till nya kontakter/uppdatera befintliga kontakter *(och deras e-postadresser)* genom Adobe Experience Platform, skapa segment utifrån sina egna offlinedata och skicka dessa segment till [!DNL Salesforce Marketing Cloud]som sedan kan användas för att skicka marknadsföringskampanjens e-post.

## Förutsättningar {#prerequisites}

### Förutsättningar i Experience Platform {#prerequisites-in-experience-platform}

Innan du aktiverar data för [!DNL (API) Salesforce Marketing Cloud] mål, du måste ha en [schema](/help/xdm/schema/composition.md), a [datauppsättning](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=en)och [segment](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=en) skapad i [!DNL Experience Platform].

### Förutsättningar [!DNL (API) Salesforce Marketing Cloud] {#prerequisites-destination}

Observera följande krav för att kunna exportera data från Platform till [!DNL Salesforce Marketing Cloud] konto:

#### Du måste ha en [!DNL Salesforce Marketing Cloud] konto {#prerequisites-account}

A [!DNL Salesforce Marketing Cloud] konto med en prenumeration på [Marketing Cloud-kontoengagemang](https://www.salesforce.com/products/marketing-cloud/marketing-automation/) produkten är obligatorisk för att fortsätta.

Nå ut till [[!DNL Salesforce] Support](https://www.salesforce.com/company/contact-us/?d=cta-glob-footer-10) om du inte har en [!DNL Salesforce Marketing Cloud] eller så saknas kontot [!DNL Marketing Cloud Account Engagement] produktprenumeration.

#### Skapa attribut i [!DNL Salesforce Marketing Cloud] {#prerequisites-attribute}

När segment aktiveras för [!DNL (API) Salesforce Marketing Cloud] mål måste du ange ett värde i **[!UICONTROL Mapping ID]** för varje aktiverat segment, i **[Segmentschema](#schedule-segment-export-example)** steg.

[!DNL Salesforce] kräver att det här värdet läser och tolkar segment som kommer in från Experience Platform korrekt och uppdaterar deras segmentstatus inom [!DNL Salesforce Marketing Cloud]. Se dokumentationen för Experience Platform för [Schemafältgrupp för detaljer om segmentmedlemskap](/help/xdm/field-groups/profile/segmentation.md) om du behöver vägledning om segmentstatus.

För varje segment som du aktiverar från Platform till [!DNL Salesforce Marketing Cloud]måste du skapa ett attribut av typen `Text` inom [!DNL Salesforce]. Använd [!DNL Salesforce Marketing Cloud] [!DNL Contact Builder] för att skapa attribut. Attributfältsnamnen används för [!DNL (API) Salesforce Marketing Cloud] målfält och ska skapas under `[!DNL Email Demographics system attribute-set]`. Du kan definiera fälttecknet med högst 4 000 tecken, beroende på dina affärsbehov. Se [!DNL Salesforce Marketing Cloud] [Datatyper för datatillägg](https://help.salesforce.com/s/articleView?id=sf.mc_es_data_extension_data_types.htm&amp;type=5) dokumentationssida för mer information om attributtyper.

Se [!DNL Salesforce Marketing Cloud] dokumentation till [skapa attribut](https://help.salesforce.com/s/articleView?id=mc_cab_create_an_attribute.htm&amp;type=5&amp;language=en_US) om du behöver hjälp med att skapa attribut.

Ett exempel på datadesignerskärmen i [!DNL Salesforce Marketing Cloud]som du ska lägga till attributet i visas nedan:
![Datadesigner för användargränssnittet i Salesforce Marketing Cloud.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/salesforce-data-designer.png)

En vy av [!DNL Salesforce Marketing Cloud] [!DNL Email Demographics] Attributuppsättningen visas nedan:
![Salesforce Marketing Cloud UI email demographics attribute-set.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/salesforce-email-demograhics-fields.png)

The [!DNL (API) Salesforce Marketing Cloud] destinationen använder [!DNL Salesforce Marketing Cloud] [!DNL Search Attribute-Set Definitions REST] [API](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/retrieveAttributeSetDefinitions.html) att dynamiskt hämta attributen och deras attributuppsättningar som definierats i [!DNL Salesforce Marketing Cloud].

Dessa visas i **[!UICONTROL Target field]** markeringsfönstret när du ställer in [mappning](#mapping-considerations-example) i arbetsflödet till [aktivera segment till målet](#activate). Observera att endast mappningar för de attribut som definieras i [!DNL Salesforce Marketing Cloud] `[!DNL Email Demographics]` stöds.

>[!IMPORTANT]
>
>Inom [!DNL Salesforce Marketing Cloud]måste du skapa attribut med **[!UICONTROL FIELD NAME]** som exakt matchar värdet som anges i **[!UICONTROL Mapping ID]** för varje aktiverat plattformssegment. På skärmbilden nedan visas ett attribut med namnet `salesforce_mc_segment_1`. Lägg till `salesforce_mc_segment_1` as **[!UICONTROL Mapping ID]** för att fylla segmentmålgrupper från Experience Platform i detta attribut.

Ett exempel på hur attribut skapas i [!DNL Salesforce Marketing Cloud]visas nedan:
![Användargränssnittet i Salesforce Marketing Cloud med ett attribut.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/salesforce-custom-field.png)

>[!TIP]
>
>* När du skapar attributet ska du inte ta med blankstegstecken i fältnamnet. Använd i stället understrecket `(_)` tecken som avgränsare.
>* Att skilja mellan attribut som används för plattformssegment och andra attribut inom [!DNL Salesforce Marketing Cloud]kan du inkludera ett identifierbart prefix eller suffix för de attribut som används för Adobe-segment. I stället för `test_segment`, använda `Adobe_test_segment` eller `test_segment_Adobe`.
>* Om du redan har andra attribut som [!DNL Salesforce Marketing Cloud]kan du använda samma namn som plattformssegmentet för att enkelt identifiera segmentet i [!DNL Salesforce Marketing Cloud].


#### Samla [!DNL Salesforce Marketing Cloud] autentiseringsuppgifter {#gather-credentials}

Anteckna vad som står nedan innan du autentiserar dig för [!DNL (API) Salesforce Marketing Cloud] mål.

| Autentiseringsuppgifter | Beskrivning | Exempel |
| --- | --- | --- |
| Underdomän | Se [[!DNL Salesforce Marketing Cloud domain prefix]](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/your-subdomain-tenant-specific-endpoints.html) om du vill veta hur du får fram det här värdet från [!DNL Salesforce Marketing Cloud] gränssnitt. | Om [!DNL Salesforce Marketing Cloud] domänen är<br> *`mcq4jrssqdlyc4lph19nnqgzzs84`.login.exactarget.com*, <br>du måste ange `mcq4jrssqdlyc4lph19nnqgzzs84` som värdet. |
| Klient-ID | Se [!DNL Salesforce Marketing Cloud] [dokumentation](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/access-token-s2s.html) om du vill veta hur du får fram det här värdet från [!DNL Salesforce Marketing Cloud] gränssnitt. | r23kxxxxxxxx0z05xxxxxx |
| Klienthemlighet | Se [!DNL Salesforce Marketing Cloud] [dokumentation](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/access-token-s2s.html) om du vill veta hur du får fram det här värdet från [!DNL Salesforce Marketing Cloud] gränssnitt. | ipxxxxxxxxxxT4xxxxxxxxxx |

{style="table-layout:auto"}

### Guardrails {#guardrails}

* Salesforce inför vissa [hastighetsbegränsningar](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/rate-limiting.html).
   * Se [!DNL Salesforce Marketing Cloud] [dokumentation](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/rate-limiting-errors.html) för att åtgärda eventuella begränsningar som kan uppstå och minska antalet fel under körningen.
   * Se [[!DNL Salesforce Marketing Cloud] Priser](https://www.salesforce.com/editions-pricing/marketing-cloud/email/) sida till *Ladda ned jämförelsetabellen för fullversionen* som en pdf som detaljerar de begränsningar som din plan innebär.
   * The [API-översikt](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/apis-overview.html) ytterligare begränsningar för sidinformation.
   * Referens [här](https://salesforce.stackexchange.com/questions/205898/marketing-cloud-api-limits) för en sida som sammanställer dessa uppgifter.
* Antal *anpassade fält tillåtna per objekt* varierar beroende på din Salesforce Edition.
   * Se [!DNL Salesforce] [dokumentation](https://help.salesforce.com/s/articleView?id=sf.custom_field_allocations.htm&amp;type=5) för ytterligare vägledning.
   * Om du har nått gränsen för *anpassade fält tillåtna per objekt* inom [!DNL Salesforce Marketing Cloud] måste du
      * Ta bort äldre attribut innan du lägger till nya attribut i [!DNL Salesforce Marketing Cloud].
      * Uppdatera eller ta bort aktiverade segment i plattformsmål där dessa äldre attributnamn används som angivet värde **[!UICONTROL Mapping ID]** under [segmentplanering](#schedule-segment-export-example) steg.

## Identiteter som stöds {#supported-identities}

[!DNL (API) Salesforce Marketing Cloud] stöder aktivering av identiteter som beskrivs i tabellen nedan. Läs mer om [identiteter](/help/identity-service/namespaces.md).

| Målidentitet | Beskrivning | Överväganden |
|---|---|---|
| contactKey | [!DNL Salesforce Marketing Cloud] Kontaktnyckel. Se [!DNL Salesforce Marketing Cloud] [dokumentation](https://help.salesforce.com/s/articleView?id=sf.mc_cab_contact_builder_best_practices.htm&amp;type=5) om du behöver ytterligare vägledning. | Obligatoriskt |

## Exportera typ och frekvens {#export-type-frequency}

Se tabellen nedan för information om exporttyp och frekvens för destinationen.

| Objekt | Typ | Anteckningar |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Profile-based]** | <ul><li>Du exporterar alla medlemmar i ett segment tillsammans med de önskade schemafälten *(till exempel: e-postadress, telefonnummer, efternamn)*, enligt fältmappningen.</li><li> Varje segmentstatus i [!DNL Salesforce Marketing Cloud] uppdateras med motsvarande segmentstatus från Platform, baserat på **[!UICONTROL Mapping ID]** det värde som anges under [segmentplanering](#schedule-segment-export-example) steg.</li></ul> |
| Exportfrekvens | **[!UICONTROL Streaming]** | Direktuppspelningsmål är alltid på API-baserade anslutningar. Så snart en profil uppdateras i Experience Platform baserat på segmentutvärdering skickar kopplingen uppdateringen nedåt till målplattformen. Läs mer om [mål för direktuppspelning](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Anslut till målet {#connect}

>[!IMPORTANT]
>
>Om du vill ansluta till målet behöver du **[!UICONTROL Manage Destinations]** [åtkomstkontrollbehörighet](/help/access-control/home.md#permissions). Läs [åtkomstkontroll - översikt](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få de behörigheter som krävs.

Om du vill ansluta till det här målet följer du stegen som beskrivs i [självstudiekurs om destinationskonfiguration](../../ui/connect-destination.md). I arbetsflödet för att konfigurera mål fyller du i fälten som listas i de två avsnitten nedan.

Inom **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]**, sök efter [!DNL (API) Salesforce Marketing Cloud]. Du kan även hitta den under **[!UICONTROL Email marketing]** kategori.

### Autentisera till mål {#authenticate}

Om du vill autentisera mot målet fyller du i de obligatoriska fälten nedan och väljer **[!UICONTROL Connect to destination]**. Se [Samla [!DNL Salesforce Marketing Cloud] autentiseringsuppgifter](#gather-credentials) för vägledning.

| [!DNL (API) Salesforce Marketing Cloud] mål | [!DNL Salesforce Marketing Cloud] |
| --- | --- |
| **[!UICONTROL Subdomain]** | Dina [!DNL Salesforce Marketing Cloud] domänprefix. <br>Om din domän till exempel är <br> *`mcq4jrssqdlyc4lph19nnqgzzs84`.login.exactarget.com*, <br> du måste ange `mcq4jrssqdlyc4lph19nnqgzzs84` som värdet. |
| **[!UICONTROL Client ID]** | Din [!DNL Salesforce Marketing Cloud] `Client ID`. |
| **[!UICONTROL Client Secret]** | Din [!DNL Salesforce Marketing Cloud] `Client Secret`. |

![Skärmbild av användargränssnittet för plattformen som visar hur du autentiserar till Salesforce Marketing Cloud.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/authenticate-destination.png)

Om den angivna informationen är giltig visas en **[!UICONTROL Connected]** status med en grön bockmarkering kan du fortsätta till nästa steg.

### Fyll i målinformation {#destination-details}

Om du vill konfigurera information för målet fyller du i de obligatoriska och valfria fälten nedan. En asterisk bredvid ett fält i användargränssnittet anger att fältet är obligatoriskt.
![Skärmbild för användargränssnittet för plattformen som visar målinformationen.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/destination-details.png)

* **[!UICONTROL Name]**: Ett namn som du känner igen det här målet med i framtiden.
* **[!UICONTROL Description]**: En beskrivning som hjälper dig att identifiera det här målet i framtiden.

### Aktivera aviseringar {#enable-alerts}

Du kan aktivera varningar för att få meddelanden om dataflödets status till ditt mål. Välj en avisering i listan om du vill prenumerera och få meddelanden om status för ditt dataflöde. Mer information om varningar finns i guiden [prenumerera på destinationsvarningar med hjälp av användargränssnittet](../../ui/alerts.md).

När du är klar med informationen för målanslutningen väljer du **[!UICONTROL Next]**.

## Aktivera segment till den här destinationen {#activate}

>[!IMPORTANT]
>
>Om du vill aktivera data måste du ha **[!UICONTROL Manage Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** och **[!UICONTROL View Segments]** [behörigheter för åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontroll - översikt](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få de behörigheter som krävs.

Läs [Aktivera profiler och segment för att direktuppspela segmentexportmål](/help/destinations/ui/activate-segment-streaming-destinations.md) om du vill ha instruktioner om hur du aktiverar målgruppssegment till det här målet.

### Mappa överväganden och exempel {#mapping-considerations-example}

Så här skickar du målgruppsdata från Adobe Experience Platform till [!DNL (API) Salesforce Marketing Cloud] mål måste du gå igenom fältmappningssteget. Mappningen består av att skapa en länk mellan XDM-schemafälten (Experience Data Model) i ditt plattformskonto och motsvarande motsvarigheter från målmålet.

Koppla XDM-fälten till [!DNL (API) Salesforce Marketing Cloud] målfält, följ stegen nedan.

>[!IMPORTANT]
>
>Även om attributnamnen är som du vill [!DNL Salesforce Marketing Cloud] konto, mappningar för båda `contactKey` och `personalEmail.address` är obligatoriska. Vid mappning av attribut är det bara attribut från Experience Platform `Email Demographics` ska användas i målfälten.

1. I **[!UICONTROL Mapping]** steg, välja **[!UICONTROL Add new mapping]**. En ny mappningsrad visas på skärmen.
   ![Exempel på skärmbild för användargränssnittet för plattformen för att lägga till ny mappning.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/add-new-mapping.png)
1. I **[!UICONTROL Select source field]** väljer du **[!UICONTROL Select attributes]** och välj XDM-attributet eller välj **[!UICONTROL Select identity namespace]** och välj en identitet.
1. I **[!UICONTROL Select target field]** väljer du **[!UICONTROL Select identity namespace]** och välj en identitet eller välj **[!UICONTROL Select custom attributes]** och välj ett attribut i `Email Demographics` attribut visas efter behov. The [!DNL (API) Salesforce Marketing Cloud] destinationen använder [!DNL Salesforce Marketing Cloud] [!DNL Search Attribute-Set Definitions REST] [API](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/retrieveAttributeSetDefinitions.html) för att dynamiskt hämta de attribut och deras attributuppsättningar som definierats i [!DNL Salesforce Marketing Cloud]. Dessa visas i **[!UICONTROL Target field]** när du ställer in [mappning](#mapping-considerations-example) i [aktivera segment i arbetsflöde](#activate). Obs! Endast mappningar för de attribut som definieras i [!DNL Salesforce Marketing Cloud] `[!DNL Email Demographics]` stöds.

   * Upprepa dessa steg för att lägga till följande mappningar mellan XDM-profilschemat och [!DNL (API) Salesforce Marketing Cloud]: |Källfält|Målfält| Obligatoriskt| |—|—|—| |`IdentityMap: contactKey`|`Identity: salesforceContactKey`| `Mandatory` |\
      |`xdm: person.name.firstName`|`Attribute: Email Demographics.First Name`| - |
|`xdm: personalEmail.address`|`Attribute: Email Addresses.Email Address`| - |

   * Ett exempel på hur du använder dessa mappningar visas nedan:
      ![Exempel på skärmbild för användargränssnittet för plattformen som visar målmappningar.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/mappings.png)

När du har angett mappningarna för målanslutningen väljer du **[!UICONTROL Next]**.

### Schemalägg segmentexport och exempel {#schedule-segment-export-example}

När du utför [Schemalägg segmentexport](/help/destinations/ui/activate-segment-streaming-destinations.md#scheduling) måste du manuellt mappa plattformssegment till [attributes](#prerequisites-attribute) in [!DNL Salesforce Marketing Cloud].

Det gör du genom att markera varje segment och sedan ange namnet på attributet från [!DNL Salesforce Marketing Cloud] i [!DNL (API) Salesforce Marketing Cloud] **[!UICONTROL Mapping ID]** fält. Se [Skapa attribut i [!DNL Salesforce Marketing Cloud]](#prerequisites-custom-field) för vägledning och bästa metoder för att skapa attribut i [!DNL Salesforce Marketing Cloud].

Om [!DNL Salesforce Marketing Cloud] attributet är `salesforce_mc_segment_1`anger du det här värdet i [!DNL (API) Salesforce Marketing Cloud] **[!UICONTROL Mapping ID]** för att fylla segmentmålgrupper från Experience Platform i detta attribut.

Ett exempelattribut från [!DNL Salesforce Marketing Cloud] visas nedan:
![Användargränssnittet i Salesforce Marketing Cloud med ett attribut.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/salesforce-custom-field.png)

Ett exempel som anger platsen för [!DNL (API) Salesforce Marketing Cloud] **[!UICONTROL Mapping ID]** visas nedan:
![Exempel på skärmbild för användargränssnittet för plattformen som visar export av Schedule-segment.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/schedule-segment-export.png)

Som visas [!DNL (API) Salesforce Marketing Cloud] **[!UICONTROL Mapping ID]** ska exakt matcha värdet som anges i [!DNL Salesforce Marketing Cloud] **[!UICONTROL FIELD NAME]**.

Upprepa det här avsnittet för varje aktiverat plattformssegment.

Beroende på ditt sätt att arbeta kan alla aktiverade segment mappas till samma [!DNL Salesforce Marketing Cloud] **[!UICONTROL FIELD NAME]** eller till olika **[!UICONTROL FIELD NAME]** in [!DNL (API) Salesforce Marketing Cloud]. Ett typiskt exempel baserat på bilden ovan kan vara.
| [!DNL (API) Salesforce Marketing Cloud] segmentnamn | [!DNL Salesforce Marketing Cloud] **[!UICONTROL FIELD NAME]** | [!DNL (API) Salesforce Marketing Cloud] **[!UICONTROL Mapping ID]** | | — | — | — | | salesforce mc segment 1 | `salesforce_mc_segment_1` | `salesforce_mc_segment_1` | | salesforce mc segment 2 | `salesforce_mc_segment_2` | `salesforce_mc_segment_2` |

## Validera dataexport {#exported-data}

Följ stegen nedan för att verifiera att du har konfigurerat målet korrekt:

1. Välj **[!UICONTROL Destinations]** > **[!UICONTROL Browse]** för att navigera till listan över destinationer.
   ![Skärmbild av användargränssnittet för plattformen med bläddringsmål.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/browse-destinations.png)

1. Markera målet och validera att statusen är **[!UICONTROL enabled]**.
   ![Skärmbild av användargränssnittet för plattformen med körning av måldataflöde.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/destination-dataflow-run.png)

1. Växla till **[!DNL Activation data]** väljer du ett segmentnamn.
   ![Skärmbild för användargränssnittet för plattformen visar aktiveringsdata för destinationer.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/destinations-activation-data.png)

1. Övervaka segmentsammanfattningen och se till att antalet profiler motsvarar antalet som skapas i segmentet.
   ![Exempel på skärmbild för plattformsgränssnitt som visar segment.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/segment.png)

1. Logga in på [[!DNL Salesforce Marketing Cloud]](https://mc.exacttarget.com/) webbplats. Navigera sedan till **[!DNL Audience Builder]** > **[!DNL Contact Builder]** > **[!DNL All contacts]** > **[!DNL Email]** och kontrollera om profilerna från segmentet har lagts till.
   ![Användargränssnittet i Salesforce Marketing Cloud visar sidan Kontakter med profiler som används i segmentet.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/contacts.png)

1. Navigera till **[!UICONTROL Email]** och verifiera om attributvärdena för profilen från segmentet har uppdaterats. Om du lyckas ser du att varje segment har statusen [!DNL Salesforce Marketing Cloud] uppdaterades med motsvarande segmentstatus från Platform, baserat på **[!UICONTROL Mapping ID]** värdet i [segmentplanering](#schedule-segment-export-example) steg.
   ![Användargränssnittet i Salesforce Marketing Cloud visar den valda e-postkontaktsidan med uppdaterade segmentstatusar.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/contact-detail.png)

## Dataanvändning och styrning {#data-usage-governance}

Alla [!DNL Adobe Experience Platform] destinationerna är kompatibla med dataanvändningsprinciper när data hanteras. Detaljerad information om hur [!DNL Adobe Experience Platform] använder datastyrning, se [Datastyrning - översikt](/help/data-governance/home.md).

## Fel och felsökning {#errors-and-troubleshooting}

### Okända fel påträffades när händelser skickades till Salesforce Marketing Cloud {#unknown-errors}

* När du kontrollerar ett dataflöde kan följande felmeddelande visas: `Unknown errors encountered while pushing events to the destination. Please contact the administrator and try again.`

   ![Skärmbild för användargränssnittet för plattformen visar ett fel.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-exact-target/error.png)

   * Kontrollera att **[!UICONTROL Mapping ID]** som du angav i aktiveringsarbetsflödet för [!DNL (API) Salesforce Marketing Cloud] målet matchar exakt namnet på attributet som du skapade i [!DNL Salesforce Marketing Cloud]. Se [Skapa attribut i [!DNL Salesforce Marketing Cloud]](#prerequisites-custom-field) för vägledning.

* När du aktiverar ett segment kan du få ett felmeddelande: `The client's IP address is unauthorized for this account. Allowlist the client's IP address...`
   * Om du vill åtgärda felet kontaktar du [!DNL Salesforce Marketing Cloud] kontoadministratör att lägga till [Experience Platform IP-adresser](/help/destinations/catalog/streaming/ip-address-allow-list.md) till [!DNL Salesforce Marketing Cloud] kontots betrodda IP-intervall. Se [!DNL Salesforce Marketing Cloud] [IP-adresser som ska inkluderas på Tillåtelselista i Marketing Cloud](https://help.salesforce.com/s/articleView?id=sf.mc_es_ip_addresses_for_inclusion.htm&amp;type=5) dokumentation om du behöver ytterligare vägledning.

## Ytterligare resurser {#additional-resources}

* [!DNL Salesforce Marketing Cloud] [API](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/apis-overview.html)
* [!DNL Salesforce Marketing Cloud] [dokumentation](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/updateContacts.html) förklarar hur kontakter uppdateras med den angivna informationen i de angivna attributgrupperna.

### Changelog {#changelog}

I det här avsnittet beskrivs funktionaliteten och viktiga dokumentationsuppdateringar för den här målanslutningen.

+++ Visa ändringslogg

| Releasamånad | Uppdateringstyp | Beskrivning |
|---|---|---|
| Februari 2023 | Dokumentationsuppdatering | Vi har uppdaterat [Förutsättningar i (API) Salesforce Marketing Cloud](#prerequisites-destination) avsnitt som ska innehålla en referenslänk som anropar den [!DNL Salesforce Marketing Cloud Account Engagement] är en obligatorisk prenumeration för att använda den här destinationen. |
| Februari 2023 | Funktionsuppdatering | Vi har åtgärdat ett problem där en felaktig konfiguration i målet orsakade att ett felaktigt JSON skickades till Salesforce. Detta resulterade i att ett stort antal identiteter inte kunde aktiveras. (PLATIR-26299) |
| Januari 2023 | Dokumentationsuppdatering | <ul><li>Vi har uppdaterat [Förutsättningar [!DNL Salesforce]](#prerequisites-destination) för att ta reda på att attribut måste skapas i [!DNL Salesforce] sida. Det här avsnittet innehåller nu detaljerade anvisningar om hur du gör det och de bästa sätten att namnge attributen i [!DNL Salesforce]. (PLATIR-25602)</li><li>Vi har lagt till tydliga instruktioner om hur du använder mappnings-ID för varje aktiverat segment i [segmentplanering](#schedule-segment-export-example) steg. (PLATIR-25602)</li></ul> |
| Oktober 2022 | Inledande version | Ursprunglig målversion och dokumentationspublicering. |

{style="table-layout:auto"}

+++