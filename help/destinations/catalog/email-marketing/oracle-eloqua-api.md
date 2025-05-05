---
title: (API) Oracle Eloqua-anslutning
description: (API) Oracle Eloqua-destinationen gör att du kan exportera dina kontodata och aktivera dem i Oracle Eloqua för dina affärsbehov.
last-substantial-update: 2023-03-14T00:00:00Z
exl-id: 97ff41a2-2edd-4608-9557-6b28e74c4480
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1967'
ht-degree: 0%

---


# [!DNL (API) Oracle Eloqua]-anslutning

Med [[!DNL Oracle Eloqua]](https://www.oracle.com/cx/marketing/automation/) kan marknadsförare planera och köra kampanjer samtidigt som de levererar en personaliserad kundupplevelse för sina potentiella kunder. Tack vare integrerad hantering av leads och enkel kampanjframtagning kan marknadsförarna engagera rätt målgrupp vid rätt tidpunkt i köparens resa och på ett elegant sätt skala nå målgrupper över olika kanaler, inklusive e-post, webbannonsering, video och mobiler. Säljarna kan sluta fler avtal snabbare och öka avkastningen på marknadsföringen genom realtidsinsikter.

Detta [!DNL Adobe Experience Platform] [mål](/help/destinations/home.md) utnyttjar åtgärden [Uppdatera en kontakt](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/op-api-rest-1.0-data-contact-id-put.html) från [!DNL Oracle Eloqua] REST API, som gör att du kan **uppdatera identiteter** inom en målgrupp till [!DNL Oracle Eloqua].

[!DNL Oracle Eloqua] använder [Grundläggande autentisering](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/Authentication_Basic.html) för att kommunicera med REST API:t [!DNL Oracle Eloqua]. Instruktioner för autentisering till din [!DNL Oracle Eloqua]-instans finns längre ned i avsnittet [Autentisera till mål](#authenticate).

## Användningsfall {#use-cases}

Marknadsföringsavdelningen på en onlineplattform vill sända en e-postbaserad marknadsföringskampanj till en välstrukturerad publik med leads. Plattformens marknadsföringsteam kan uppdatera befintlig huvudinformation via Adobe Experience Platform, bygga målgrupper utifrån sina egna offlinedata och skicka dessa målgrupper till [!DNL Oracle Eloqua], som sedan kan användas för att skicka marknadsföringskampanjens e-post.

## Förhandskrav {#prerequisites}

### Krav för Experience Platform {#prerequisites-in-experience-platform}

Innan du aktiverar data till målet [!DNL Oracle Eloqua] måste du ha ett [schema](/help/xdm/schema/composition.md), en [datamängd](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=sv-SE) och [segment](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=sv-SE) som skapats i [!DNL Experience Platform].

Se Experience Platform-dokumentationen för schemafältgruppen [Information om målgruppsmedlemskap](/help/xdm/field-groups/profile/segmentation.md) om du behöver vägledning om målgruppsstatus.

### Krav för [!DNL Oracle Eloqua] {#prerequisites-destination}

Om du vill exportera data från Experience Platform till ditt [!DNL Oracle Eloqua]-konto måste du ha ett [!DNL Oracle Eloqua]-konto.

Dessutom behöver du minst *&quot;Avancerade användare - marknadsföringsbehörigheter&quot;* för din [!DNL Oracle Eloqua]-instans. Mer information finns i avsnittet *&quot;Säkerhetsgrupper&quot;* på sidan [Skyddad användaråtkomst](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-user/Help/SecurityOverview/SecuredUserAccess.htm) . Målet kräver åtkomst för att [avgöra din bas-URL](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/DeterminingBaseURL.html) programmatiskt när [!DNL Oracle Eloqua]-API:t anropas.

#### Samla in inloggningsuppgifter för [!DNL Oracle Eloqua] {#gather-credentials}

Observera objekten nedan innan du autentiserar till målet [!DNL Oracle Eloqua]:

| Autentiseringsuppgifter | Beskrivning |
| --- | --- |
| `Company Name` | Det företagsnamn som är associerat med ditt [!DNL Oracle Eloqua]-konto. <br>Du kommer senare att använda `Company Name` och [!DNL Oracle Eloqua] `Username` som en sammanfogad sträng som ska användas som **[!UICONTROL Username]** vid [autentisering till målet](#authenticate). |
| `Username` | Användarnamnet för ditt [!DNL Oracle Eloqua]-konto. |
| `Password` | Lösenordet för ditt [!DNL Oracle Eloqua]-konto. |
| `Pod` | [!DNL Oracle Eloqua] har stöd för flera datacenter, där vart och ett har ett unikt domännamn. [!DNL Oracle Eloqua] refererar till dessa som&quot;pods&quot;, det finns för närvarande sju totalt - p01, p02, p03, p04, p06, p07 och p08. Om du vill ta reda på vilken POD du är på loggar du in på [!DNL Oracle Eloqua] och noterar URL:en i webbläsaren när du har loggat in. Om webbläsarens URL är `secure.p01.eloqua.com` är till exempel `pod` `p01`. Mer information finns på sidan [Bestämma POD](https://community.oracle.com/topliners/discussion/4470225/determining-your-pod-number-for-oracle-eloqua). |

Mer information finns i [Logga in på [!DNL Oracle Eloqua]](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-user/Help/Administration/Tasks/SigningInToEloqua.htm#Signing).

## Guardrails {#guardrails}

>[!NOTE]
>
>* [!DNL Oracle Eloqua] anpassade kontaktfält skapas automatiskt med namnen på de målgrupper som valts under **[!UICONTROL Select segments]** -steget.

* [!DNL Oracle Eloqua] har en maxgräns på 250 anpassade kontaktfält.
* Innan du exporterar nya målgrupper ser du till att antalet Experience Platform-målgrupper och antalet befintliga målgrupper inom [!DNL Oracle Eloqua] inte överskrider denna gräns.
* Om den här gränsen överskrids uppstår ett fel i Experience Platform. Detta beror på att [!DNL Oracle Eloqua]-API:t inte kan validera begäran och svarar med ett - *400: Det fanns ett valideringsfel* - felmeddelande som beskriver problemet.
* Om du har nått gränsen ovan måste du ta bort befintliga mappningar från målet och ta bort motsvarande anpassade kontaktfält i ditt [!DNL Oracle Eloqua]-konto innan du kan exportera fler segment.

* Mer information om ytterligare begränsningar finns på sidan [[!DNL Oracle Eloqua] Skapa kontaktfält](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-user/Help/ContactFields/Tasks/CreatingContactFields.htm).

## Identiteter som stöds {#supported-identities}

[!DNL Oracle Eloqua] har stöd för uppdatering av identiteter som beskrivs i tabellen nedan. Läs mer om [identiteter](/help/identity-service/features/namespaces.md).

| Målidentitet | Beskrivning | Obligatoriskt |
|---|---|---|
| `EloquaId` | Unik identifierare för kontakten. | Ja |

## Exportera typ och frekvens {#export-type-frequency}

Se tabellen nedan för information om exporttyp och frekvens för destinationen.

| Objekt | Typ | Anteckningar |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Profile-based]** | <ul><li>Du exporterar alla medlemmar i ett segment, tillsammans med de önskade schemafälten *(till exempel e-postadress, telefonnummer, efternamn)*, enligt fältmappningen.</li><li> För varje vald målgrupp i Experience Platform uppdateras motsvarande [!DNL Oracle Eloqua]-segmentstatus med målgruppsstatus från Experience Platform.</li></ul> |
| Exportfrekvens | **[!UICONTROL Streaming]** | <ul><li>Direktuppspelningsmål är alltid på API-baserade anslutningar. Så snart en profil uppdateras i Experience Platform baserat på målgruppsutvärdering skickar anslutningsprogrammet uppdateringen nedströms till målplattformen. Läs mer om [direktuppspelningsmål](/help/destinations/destination-types.md#streaming-destinations).</li></ul> |

{style="table-layout:auto"}

## Anslut till målet {#connect}

>[!IMPORTANT]
>
>Om du vill ansluta till målet behöver du behörigheterna **[!UICONTROL View Destinations]** och **[!UICONTROL Manage Destinations]** [åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontrollsöversikten](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få den behörighet som krävs.

Om du vill ansluta till det här målet följer du stegen som beskrivs i självstudiekursen [för destinationskonfiguration](../../ui/connect-destination.md). I arbetsflödet för att konfigurera mål fyller du i fälten som listas i de två avsnitten nedan.

I **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]** söker du efter [!DNL (API) Oracle Eloqua]. Du kan också hitta den under kategorin **[!UICONTROL Email Marketing]**.

### Autentisera till mål {#authenticate}

>[!CONTEXTUALHELP]
>id="platform_destinations_apioracleeloqua_companyname_username"
>title="Företag\Användarnamn"
>abstract="Fyll i det här fältet med ditt företagsnamn och ditt användarnamn från Oracle Eloqua i formatet `{COMPANY_NAME}\{USERNAME}`"

Fyll i de obligatoriska fälten nedan. Mer information finns i avsnittet [Samla [!DNL Oracle Eloqua] inloggningsuppgifter](#gather-credentials).
* **[!UICONTROL Password]**: Lösenordet för ditt [!DNL Oracle Eloqua]-konto.
* **[!UICONTROL Username]**: En sammanfogad sträng som består av ditt [!DNL Oracle Eloqua] företagsnamn och [!DNL Oracle Eloqua] användarnamn.<br>Det sammanfogade värdet har formen `{COMPANY_NAME}\{USERNAME}`.<br> Obs! Använd inte klammerparenteser eller mellanslag och bevara `\`. <br>Om ditt [!DNL Oracle Eloqua] företagsnamn till exempel är `MyCompany` och [!DNL Oracle Eloqua] användarnamn är `Username` är det sammanfogade värde som du kommer att använda i fältet **[!UICONTROL Username]** `MyCompany\Username`.

Om du vill autentisera till målet väljer du **[!UICONTROL Connect to destination]**.
![Experience Platform UI, bild som visar hur du autentiserar.](../../assets/catalog/email-marketing/oracle-eloqua-api/authenticate-destination.png)

Om den angivna informationen är giltig visas statusen **[!UICONTROL Connected]** med en grön bockmarkering. Du kan sedan gå vidare till nästa steg.

### Fyll i målinformation {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_apioracleeloqua_pod"
>title="Pod"
>abstract="Du hittar ditt podnummer genom att logga in på Oracle Eloqua. Anteckna URL-adressen i webbläsaren när du har loggat in. "

<!-- >additional-url="https://support.oracle.com/knowledge/Oracle%20Cloud/2307176_1.html" text="Oracle Knowledge base - find out your Pod number" -->

Om du vill konfigurera information för målet fyller du i de obligatoriska och valfria fälten nedan. En asterisk bredvid ett fält i användargränssnittet anger att fältet är obligatoriskt.
![Experience Platform UI-skärmbild med målinformation.](../../assets/catalog/email-marketing/oracle-eloqua-api/destination-details.png)

* **[!UICONTROL Name]**: Ett namn som du känner igen det här målet med i framtiden.
* **[!UICONTROL Description]**: En beskrivning som hjälper dig att identifiera det här målet i framtiden.
* **[!UICONTROL Pod]**: Om du vill ta reda på vilken `pod` du är inloggad loggar du in på [!DNL Oracle Eloqua] och noterar URL:en i webbläsaren när du har loggat in. Om webbläsarens URL till exempelvis är `secure.p01.eloqua.com` är det `pod`-värde som du måste välja `p01`. Mer information finns i avsnittet [Samla [!DNL Oracle Eloqua] inloggningsuppgifter](#gather-credentials).

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

Om du vill skicka målgruppsdata från Adobe Experience Platform till målet [!DNL Oracle Eloqua] måste du gå igenom fältmappningssteget. Mappningen består av att skapa en länk mellan XDM-schemafälten (Experience Data Model) i ditt Experience Platform-konto och deras motsvarande motsvarigheter från målmålet.

Följ de här stegen för att mappa dina XDM-fält till [!DNL Oracle Eloqua]-målfälten:

1. Välj **[!UICONTROL Add new mapping]** i steget **[!UICONTROL Mapping]**. En ny mappningsrad visas på skärmen.
1. Välj kategorin **[!UICONTROL Select attributes]** i fönstret **[!UICONTROL Select source field]** och markera XDM-attributet eller välj **[!UICONTROL Select identity namespace]** och välj en identitet.
1. I fönstret **[!UICONTROL Select target field]** väljer du **[!UICONTROL Select identity namespace]** och väljer en identitet, eller väljer **[!UICONTROL Select custom attributes]** och skriver det önskade attributnamnet i fältet **[!UICONTROL Attribute name]**. Attributnamnet som du anger ska matcha ett befintligt kontaktattribut i [!DNL Oracle Eloqua]. I [[!DNL create a contact]](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/op-api-rest-1.0-data-contact-post.html) finns de exakta attributnamnen som du kan använda i [!DNL Oracle Eloqua].

   * Upprepa dessa steg för att lägga till både nödvändiga och önskade attributmappningar mellan XDM-profilschemat och [!DNL Oracle Eloqua]:

     | Source Field | Målfält | Obligatoriskt |
     |---|---|---|
     | `IdentityMap: Eid` | `Identity: EloquaId` | Ja |
     | `xdm: personalEmail.address` | `Attribute: emailAddress` | Ja |
     | `xdm: personName.firstName` | `Attribute: firstName` | |
     | `xdm: personName.lastName` | `Attribute: lastName` | |
     | `xdm: workAddress.street1` | `Attribute: address1` | |
     | `xdm: workAddress.street2` | `Attribute: address2` | |
     | `xdm: workAddress.street3` | `Attribute: address3` | |
     | `xdm: workAddress.postalCode` | `Attribute: postalCode` | |
     | `xdm: workAddress.country` | `Attribute: country` | |
     | `xdm: workAddress.city` | `Attribute: city` | |

   * Ett exempel med mappningarna ovan visas nedan:

     ![Exempel på skärmbild i Experience Platform UI med attributmappningar.](../../assets/catalog/email-marketing/oracle-eloqua-api/mappings.png)

>[!IMPORTANT]
>
>* Attribut som anges i **[!UICONTROL Target field]** ska ha exakt samma namn som anges i [[!DNL Create a contact]](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/op-api-rest-1.0-data-contact-post.html) eftersom dessa attribut kommer att bilda begärandetexten.
>* Attribut som anges i **[!UICONTROL Source field]** följer inte någon sådan begränsning. Du kan mappa den baserat på dina behov, men om dataformatet inte är korrekt när det skickas till [!DNL Oracle Eloqua] resulterar det i ett fel. Du kan till exempel mappa **[!UICONTROL Source field]**-identitetsnamnutrymmet `contact key`, `ABC ID` osv. till **[!UICONTROL Target field]** : `EloquaId` efter att du kontrollerat att ID-värdena matchar det format som accepteras av [!DNL Oracle Eloqua].
>* Mappningen `EloquaID` är obligatorisk för att uppdatera attribut som motsvarar identiteten.
>* Mappningen `emailAddress` krävs. Utan det genererar API:t ett fel enligt nedan:
>
>```json
>{
>     "type":"ObjectValidationError",
>     "container":{
>           "type":"ObjectKey",
>           "objectType":"Contact"
>     },
>     "property":"emailAddress",
>     "requirement":{
>           "type":"EmailAddressRequirement"
>     },
>     "value":"<null>"
>}
>```

Välj **[!UICONTROL Next]** när du är klar med mappningarna för målanslutningen.

>[!NOTE]
>
>Målet lägger automatiskt till en unik identifierare till de valda målgruppsnamnen vid varje körning när kontaktfältsinformationen skickas till [!DNL Oracle Eloqua]. Detta garanterar att de kontaktfältsnamn som motsvarar målgruppsnamnen inte överlappar varandra. Se skärmbilden [Validera dataexport](#exported-data) för en [!DNL Oracle Eloqua] kontaktinformationssida med ett anpassat kontaktfält som skapats med målgruppsnamnen.

## Validera dataexport {#exported-data}

Följ stegen nedan för att verifiera att du har konfigurerat målet korrekt:

1. Välj **[!UICONTROL Destinations]** > **[!UICONTROL Browse]** och navigera till listan med mål.
1. Välj sedan målet, växla till fliken **[!UICONTROL Activation data]** och välj sedan ett målgruppsnamn.
   ![Exempel på skärmbild i Experience Platform UI som visar aktiveringsdata för destinationer.](../../assets/catalog/email-marketing/oracle-eloqua-api/destinations-activation-data.png)

1. Övervaka målgruppssammanfattningen och kontrollera att antalet profiler motsvarar antalet inom segmentet.
   ![Exempel på skärmbild i Experience Platform UI som visar segment.](../../assets/catalog/email-marketing/oracle-eloqua-api/segment.png)

1. Logga in på webbplatsen [!DNL Oracle Eloqua] och navigera sedan till sidan **[!UICONTROL Contacts Overview]** för att kontrollera om profilerna från målgruppen har lagts till. Om du vill visa målgruppens status går du ned till en **[!UICONTROL Contact Detail]**-sida och kontrollerar om kontaktfältet med det valda målgruppsnamnet som prefix har skapats.

![Oracle Eloqua UI, skärmbild som visar sidan Kontaktinformation med anpassat kontaktfält som skapats med målgruppens namn.](../../assets/catalog/email-marketing/oracle-eloqua-api/contact.png)

## Dataanvändning och styrning {#data-usage-governance}

Alla [!DNL Adobe Experience Platform]-mål är kompatibla med dataanvändningsprinciper när data hanteras. Mer information om hur [!DNL Adobe Experience Platform] använder datastyrning finns i [Datastyrningsöversikten](/help/data-governance/home.md).

## Fel och felsökning {#errors-and-troubleshooting}

När du skapar målet kanske du får något av följande felmeddelanden: `400: There was a validation error` eller `400 BAD_REQUEST`. Detta inträffar när du överskrider gränsen på 250 anpassade kontaktfält, vilket beskrivs i avsnittet [skyddsutkast](#guardrails). Kontrollera att du inte överskrider gränsen för anpassade kontaktfält i [!DNL Oracle Eloqua] för att åtgärda det här felet.
![Experience Platform UI-skärmbild visar ett fel.](../../assets/catalog/email-marketing/oracle-eloqua-api/error.png)

På sidorna [[!DNL Oracle Eloqua] HTTP-statuskoder](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/APIRequests_HTTPStatusCodes.html) och [[!DNL Oracle Eloqua] Valideringsfel](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/APIRequests_HTTPValidationErrors.html) finns en omfattande lista med status- och felkoder med förklaringar.

## Ytterligare resurser {#additional-resources}

Mer information finns i [!DNL Oracle Eloqua]-dokumentationen:

* [Oracle Eloqua Marketing Automation](https://docs.oracle.com/en/cloud/saas/marketing/eloqua.html)
* [REST API for Oracle Eloqua Marketing Cloud Service](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/rest-endpoints.html)

### Changelog

I det här avsnittet beskrivs funktionaliteten och viktiga dokumentationsuppdateringar för den här målanslutningen.

+++ Visa ändringslogg

| Releasamånad | Uppdateringstyp | Beskrivning |
|---|---|---|
| April 2023 | Uppdatering av dokumentation | <ul><li>Vi uppdaterade avsnittet [use-cases](#use-cases) med ett tydligare exempel på när kunder skulle kunna dra nytta av det här målet.</li> <li>Vi uppdaterade avsnittet [mapping](#mapping-considerations-example) med tydliga exempel på både obligatoriska och valfria mappningar.</li> <li>Vi uppdaterade avsnittet [Anslut till målet](#connect) med ett exempel på hur du skapar det sammanfogade värdet för fältet **[!UICONTROL Username]** med hjälp av företagsnamnet [!DNL Oracle Eloqua] och användarnamnet för [!DNL Oracle Eloqua]. (PLATIR-28343)</li><li>Vi uppdaterade avsnitten [Samla [!DNL Oracle Eloqua] in](#gather-credentials) och [Fyll i målinformation](#destination-details) med vägledning om [!DNL Oracle Eloqua] **[!UICONTROL Pod]**-val. Värdet *&quot;Pod&quot;* används av målet för att skapa bas-URL:en för API-anropen. Avsnittet [[!DNL Oracle Eloqua] Krav](#prerequisites-destination) uppdaterades också med vägledning om hur du tilldelar *&quot;Avancerade användare - marknadsföringsbehörigheter&quot;* som en obligatorisk *&quot;Säkerhetsgrupper&quot;* för din [!DNL Oracle Eloqua]-instans.</li></ul> |
| Mars 2023 | Inledande version | Ursprunglig målversion och dokumentationspublicering. |

{style="table-layout:auto"}

+++