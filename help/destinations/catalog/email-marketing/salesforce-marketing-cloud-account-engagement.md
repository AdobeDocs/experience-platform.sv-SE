---
title: Salesforce Marketing Cloud Account Engagement
description: Lär dig hur du använder Salesforce Marketing Cloud Account Engagement-målet (tidigare Pardot) för att exportera dina kontodata och aktivera dem i Salesforce Marketing Cloud Account Engagement för dina affärsbehov.
last-substantial-update: 2023-04-14T00:00:00Z
exl-id: fca9d4f4-8717-4bfa-9992-5164ba98bea4
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1482'
ht-degree: 0%

---

# [!DNL Salesforce Marketing Cloud Account Engagement]-anslutning

Använd målet [[!DNL Salesforce Marketing Cloud Account Engagement]](https://www.salesforce.com/products/marketing-cloud/marketing-automation/) *(tidigare kallat [!DNL Pardot])* för att hämta, spåra, poängsätta och betygsätta leads. Ni kan också utforma huvudspår för alla faser av pipeline för riktade målgrupper och kundgrupper via e-postdroppkampanjer och lead-hantering med näring, poängsättning och kampanjsegmentering.

Jämfört med [!DNL Salesforce Marketing Cloud Engagement], som är mer inriktad på **B2C** -marknadsföring, är [!DNL Marketing Cloud Account Engagement] idealiskt för **B2B**-användningsfall där flera avdelningar och beslutsfattare behöver längre försäljnings- och beslutscykler. Dessutom ligger ni närmare och är bättre integrerade med CRM för att fatta lämpliga beslut om försäljning och marknadsföring. *Obs! Experience Platform har även anslutningar för [!DNL Salesforce Marketing Cloud Engagement], du kan kontrollera dem på sidorna [[!DNL Salesforce Marketing Cloud]](/help/destinations/catalog/email-marketing/salesforce-marketing-cloud.md) och [[!DNL (API) Salesforce Marketing Cloud]](/help/destinations/catalog/email-marketing/salesforce-marketing-cloud-exact-target.md).*

Detta [!DNL Adobe Experience Platform] [mål](/help/destinations/home.md) utnyttjar [[!DNL Salesforce Account Engagement API > Prospect Upsert by Email]](https://developer.salesforce.com/docs/marketing/pardot/guide/prospect-v5.html#prospect-upsert-by-email)-slutpunkten för att **lägga till eller uppdatera dina leads** efter att de har aktiverats i ett nytt [!DNL Marketing Cloud Account Engagement]-segment.

[!DNL Marketing Cloud Account Engagement] använder OAuth 2 med Authorization Code-protokollet för att autentisera till API:t [!DNL Account Engagement]. Instruktioner för autentisering till din [!DNL Marketing Cloud Account Engagement]-instans finns längre ned i avsnittet [Autentisera till mål](#authenticate).

## Användningsfall {#use-cases}

För att du bättre ska kunna förstå hur och när du ska använda målet [!DNL Marketing Cloud Account Engagement] finns det ett exempel på användning som Adobe Experience Platform-kunder kan lösa genom att använda det här målet.

### Skicka e-post till kontakter för marknadsföringskampanjer {#use-case-send-emails}

Marknadsföringsavdelningen på en onlineplattform vill sända en e-postbaserad marknadsföringskampanj till en välstrukturerad publik av B2B-leads. Plattformens marknadsföringsteam kan lägga till nya leads eller uppdatera befintlig lead-information via Adobe Experience Platform, bygga målgrupper utifrån sina egna offlinedata och skicka dessa målgrupper till [!DNL Marketing Cloud Account Engagement], som sedan kan användas för att skicka marknadsföringskampanjens e-post.

## Förhandskrav {#prerequisites}

I avsnitten nedan finns information om eventuella krav som du måste konfigurera i Experience Platform och [!DNL Salesforce]. Här finns även information som du måste samla in innan du kan arbeta med målet för [!DNL Marketing Cloud Account Engagement].

### Förutsättningar i Experience Platform {#prerequisites-in-experience-platform}

Innan du aktiverar data till målet [!DNL Marketing Cloud Account Engagement] måste du ha ett [schema](/help/xdm/schema/composition.md), en [datamängd](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html) och [segment](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html) som skapats i [!DNL Experience Platform].

### Förutsättningar i [!DNL Marketing Cloud Account Engagement] {#prerequisites-destination}

Observera följande krav för att kunna exportera data från Experience Platform till ditt [!DNL Marketing Cloud Account Engagement]-konto:

#### Du måste ha ett [!DNL Marketing Cloud Account Engagement]-konto {#prerequisites-account}

Ett [!DNL Marketing Cloud Account Engagement]-konto med en prenumeration på [Marketing Cloud Account Engagement](https://www.salesforce.com/products/marketing-cloud/marketing-automation/)-produkten är obligatoriskt för att fortsätta.

Ditt [!DNL Salesforce]-konto bör ha [!DNL Salesforce] `Account Engagement Administrator role`. Detta krävs för att [skapa anpassade fält för potentiell kund](https://help.salesforce.com/s/articleView?id=sf.pardot_fields_create_custom_field.htm&amp;type=5).

Slutligen bör ditt konto även kunna komma åt [[!DNL Account Engagement Lightning App]](https://help.salesforce.com/s/articleView?id=sf.pardot_lightning_enable.htm&amp;type=5).

Kontakta [[!DNL Salesforce] support](https://www.salesforce.com/company/contact-us/?d=cta-glob-footer-10) eller din [!DNL Salesforce]-kontoadministratör om du inte har något konto, eller om kontot saknar [!DNL Marketing Cloud Account Engagement]-prenumerationen eller [!DNL Account Engagement Administrator role].

#### Samla in inloggningsuppgifter för [!DNL Marketing Cloud Account Engagement] {#gather-credentials}

Anteckna objekten nedan innan du autentiserar till målet [!DNL Marketing Cloud Account Engagement].

| Autentiseringsuppgifter | Beskrivning |
| --- | --- |
| `Username` | Användarnamn för ditt [!DNL Marketing Cloud Account Engagement]-konto. |
| `Password` | Lösenordet för ditt [!DNL Marketing Cloud Account Engagement]-konto. |
| `Account Engagement Business Unit ID` | Använd installationsprogrammet i [!DNL Salesforce] för att hitta affärsenhets-ID för kontoengagemang. Ange *Business Unit Setup* i rutan Snabbsökning i installationsprogrammet. Affärsenhets-ID för ditt kontoengagemang börjar med `0Uv` och är 18 tecken långt. Om du inte kan komma åt Business Unit Setup-informationen ber du [!DNL Salesforce]-kontoadministratören att ge dig `Account Engagement Business Unit ID`. Om du behöver ytterligare vägledning kan du läsa hjälpsidan för [[!DNL Salesforce] Autentisering](https://developer.salesforce.com/docs/marketing/pardot/guide/authentication). |

{style="table-layout:auto"}

### Guardrails {#guardrails}

Se [!DNL Marketing Cloud Account Engagement] [hastighetsbegränsningarna](https://developer.salesforce.com/docs/marketing/pardot/guide/overview.html#rate-limits) som anger vilka begränsningar som din plan innebär och som även gäller för Experience Platform-körningarna.

>[!IMPORTANT]
>
>Om din [!DNL Salesforce]-kontoadministratör har begränsat åtkomsten till betrodda IP-intervall måste du kontakta dem för att få [tillåtslista Experience Platform IP](/help/destinations/catalog/streaming/ip-address-allow-list.md). Mer information finns i dokumentationen för [!DNL Salesforce] [Begränsa åtkomst till betrodda IP-intervall för ett anslutet program](https://help.salesforce.com/s/articleView?id=sf.connected_app_edit_ip_ranges.htm&amp;type=5) om du behöver ytterligare hjälp.

## Identiteter som stöds {#supported-identities}

[!DNL Marketing Cloud Account Engagement] stöder aktivering av identiteter som beskrivs i tabellen nedan. Läs mer om [identiteter](/help/identity-service/features/namespaces.md).

| Målidentitet | Beskrivning | Överväganden |
|---|---|---|
| E-post | E-postadress för potentiell kund | Obligatoriskt |

{style="table-layout:auto"}

## Exportera typ och frekvens {#export-type-frequency}

Se tabellen nedan för information om exporttyp och frekvens för destinationen.

| Objekt | Typ | Anteckningar |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Profile-based]** | <ul><li>Du exporterar alla medlemmar i ett segment, tillsammans med de önskade schemafälten *(till exempel e-postadress, telefonnummer, efternamn)*, enligt fältmappningen.</li><li> För varje vald målgrupp i Experience Platform uppdateras motsvarande [!DNL Salesforce Marketing Cloud Account Engagement]-segmentstatus med målgruppsstatus från Experience Platform.</li></ul> |
| Exportfrekvens | **[!UICONTROL Streaming]** | Direktuppspelningsmål är alltid på API-baserade anslutningar. Så snart en profil uppdateras i Experience Platform baserat på målgruppsutvärdering skickar anslutningsprogrammet uppdateringen nedströms till målplattformen. Läs mer om [direktuppspelningsmål](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Anslut till målet {#connect}

>[!IMPORTANT]
>
>Om du vill ansluta till målet behöver du behörigheterna **[!UICONTROL View Destinations]** och **[!UICONTROL Manage Destinations]** [åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontrollsöversikten](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få den behörighet som krävs.

Om du vill ansluta till det här målet följer du stegen som beskrivs i självstudiekursen [för destinationskonfiguration](../../ui/connect-destination.md). I arbetsflödet för att konfigurera mål fyller du i fälten som listas i de två avsnitten nedan.

Sök efter [!DNL Salesforce Marketing Cloud Account Engagement] inom **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]**. Du kan också hitta den under kategorin **[!UICONTROL Email marketing]**.

### Autentisera till mål {#authenticate}

Om du vill autentisera till målet väljer du **[!UICONTROL Connect to destination]**. Du dirigeras till inloggningssidan för [!DNL Salesforce]. Ange autentiseringsuppgifterna för ditt [!DNL Marketing Cloud Account Engagement]-konto och välj [!DNL Log In].

![Experience Platform UI, bild som visar hur du autentiserar till Marketing Cloud Account Engagement.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement/authenticate-destination.png)

Välj sedan [!UICONTROL Allow] i det efterföljande fönstret för att ge **Adobe Experience Platform**-appen behörighet att komma åt ditt [!DNL Salesforce Marketing Cloud Account Engagement]-konto. *Du behöver bara göra detta en gång*.

![Bekräftelsepopup för skärmavbild i Salesforce App för att ge Experience Platform-appen åtkomst till Marketing Cloud Account Engagement.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement/allow-app.png)

Om den angivna informationen är giltig visas ett meddelande i användargränssnittet: *Du har anslutit till Salesforce Marketing Cloud Account Engagement-kontot* och en **[!UICONTROL Connected]**-status med en grön bockmarkering kan du fortsätta till nästa steg.

### Fyll i målinformation {#destination-details}

Om du vill konfigurera information för målet fyller du i de obligatoriska och valfria fälten nedan. En asterisk bredvid ett fält i användargränssnittet anger att fältet är obligatoriskt. Mer information finns i avsnittet [Samla [!DNL Marketing Cloud Account Engagement] inloggningsuppgifter](#gather-credentials).

![Experience Platform UI-skärmbild med målinformation.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement/destination-details.png)

| Fält | Beskrivning |
| --- | --- |
| **[!UICONTROL Name]** | Ett namn som du känner igen det här målet med i framtiden. |
| **[!UICONTROL Description]** | En beskrivning som hjälper dig att identifiera det här målet i framtiden. |
| **[!UICONTROL Account Engagement Business Unit ID]** | Din [!DNL Salesforce] `Account Engagement Business Unit ID`. |

{style="table-layout:auto"}

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

Om du vill skicka målgruppsdata från Adobe Experience Platform till målet [!DNL Marketing Cloud Account Engagement] måste du gå igenom fältmappningssteget. Mappningen består av att skapa en länk mellan XDM-schemafälten (Experience Data Model) i ditt Experience Platform-konto och deras motsvarande motsvarigheter från målmålet.

Följ stegen nedan för att mappa dina XDM-fält till målfälten för [!DNL Marketing Cloud Account Engagement] korrekt.

1. Välj **[!UICONTROL Add new mapping]** i steget **[!UICONTROL Mapping]**. En ny mappningsrad visas på skärmen.
1. Välj kategorin **[!UICONTROL Select attributes]** i fönstret **[!UICONTROL Select source field]** och markera XDM-attributet eller välj **[!UICONTROL Select identity namespace]** och välj en identitet.
1. I fönstret **[!UICONTROL Select target field]** väljer du **[!UICONTROL Select identity namespace]** och väljer en identitet eller väljer kategorin **[!UICONTROL Select custom attributes]** och anger i listan med [[!DNL Prospect API fields]](https://developer.salesforce.com/docs/marketing/pardot/guide/prospect-v5.html#fields) från det tillgängliga schemat.

   * Upprepa de här stegen för att lägga till mappningar mellan XDM-profilschemat och [!DNL Marketing Cloud Account Engagement]:

     | Source Field | Målfält | Obligatoriskt |
     | --- | --- | --- |
     | `IdentityMap: Email` | `Identity: email` | Ja |
     | `xdm: MailingAddress.city` | `xdm: city` | |
     | `xdm: person.name.firstName` | `Attribute: firstName` | |

   * Ett exempel med mappningarna ovan visas nedan:

     ![Exempel på skärmbild i Experience Platform UI som visar målmappningar.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement/mappings.png)

När du har angett mappningarna för målanslutningen väljer du **[!UICONTROL Next]**.

## Validera dataexport {#exported-data}

Följ stegen nedan för att verifiera att du har konfigurerat målet korrekt:

1. Navigera till en av de valda målgrupperna. Klicka på fliken **[!DNL Activation data]**.  Kolumnen **[!UICONTROL Mapping ID]** visar namnet på det anpassade fält som genereras på sidan [!DNL Marketing Cloud Account Engagement Prospects].
   ![Exempel på skärmbild i Experience Platform UI som visar mappnings-ID för ett markerat segment.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement/selected-segment-mapping-id.png)

1. Logga in på webbplatsen [[!DNL Salesforce]](https://login.salesforce.com/). Gå sedan till sidan **[!DNL Account Engagement]** > **[!DNL Prospects]** > **[!DNL Pardot Prospects]** och kontrollera om potentiella kunder från målgruppen har lagts till/uppdaterats. Du kan även komma åt [[!DNL Salesforce Pardot]](https://pi.pardot.com/) och få åtkomst till sidan **[!DNL Prospects]**.
   ![Salesforce UI, skärmbild som visar sidan Prospects.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement/prospects.png)

1. Om du vill kontrollera om potentiella kunder har uppdaterats väljer du en potentiell kund och kontrollerar om fältet för anpassad potentiell kund har uppdaterats med Experience Platform målgruppsstatus.
   ![Salesforce UI-skärmbild som visar den valda sidan för potentiell kund, det anpassade fältet för potentiell kund uppdateras med målgruppens status.](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement/prospect.png)

## Dataanvändning och styrning {#data-usage-governance}

Alla [!DNL Adobe Experience Platform]-mål är kompatibla med dataanvändningsprinciper när data hanteras. Mer information om hur [!DNL Adobe Experience Platform] använder datastyrning finns i [Datastyrningsöversikten](/help/data-governance/home.md).

## Ytterligare resurser {#additional-resources}

* [!DNL Marketing Cloud Account Engagement] [API-dokumentation](https://developer.salesforce.com/docs/marketing/pardot/guide/overview.html).
