---
title: Intelligent återanvändning
description: Leverera övertygande och uppkopplade upplevelser under de viktiga konverteringsögonblicken för att på ett intelligent sätt engagera sällsynta kunder på nytt.
source-git-commit: 79ba0e350d64f43558af9bc3c2ecd4ac13d11499
workflow-type: tm+mt
source-wordcount: '3403'
ht-degree: 2%

---

# Engagera kunderna på nytt på ett intelligent sätt för att få dem tillbaka

Engagera kunder som avbrutit konverteringen på nytt innan de slutför den på ett intelligent och ansvarsfullt sätt. Engagera kunderna genom upplevelser snarare än påminnelser för att öka konverteringsgraden och driva på tillväxten av kundernas livstidsvärde.

Ta hänsyn till kundernas alla egenskaper och beteenden i realtid, ta hänsyn till dem och erbjud snabb omkvalificering baserat på både online- och offlinehändelser.

![Steg för steg intelligent återkoppling av en visuell översikt på hög nivå.](../intelligent-re-engagement/images/step-by-step.png)

## Använd ärendeöversikt

Ni kommer att skapa scheman, datauppsättningar och målgrupper när ni arbetar med exempel på återengagemangsresor. Du kommer också att upptäcka de funktioner som behövs för att konfigurera exempelresor i [!DNL Adobe Journey Optimizer] och de som behövs för att skapa betalannonser i destinationer. I den här guiden används exempel på hur man återengagerar kunder i de användningsfall som beskrivs nedan:

* **Resor för återengagemang** - Rikta in er på kunder som har slutat surfa på webben och i mobilappar.
* **Övergiven kundvagnsresa** - Rikta in er på kunder som har lagt produkter i varukorgen men ännu inte köpt dem på både webbplatsen och i mobilappen.
* **Beställningsbekräftelseresa** - Fokuserar på produktinköp via webbplatsen och mobilappen.

## Förutsättningar och planering {#prerequisites-and-planning}

När du är klar med implementeringen av användningsexemplet kommer du att använda följande Real-Time CDP-funktioner och gränssnittselement (listade i den ordning som du ska använda dem). Se till att du har de nödvändiga attributbaserade behörigheterna för åtkomstkontroll i alla dessa områden, eller be systemadministratören att ge dig de behörigheter som krävs.

* [[!DNL Adobe Real-Time Customer Data Platform (Real-Time CDP)]](https://experienceleague.adobe.com/docs/platform-learn/tutorials/rtcdp/understanding-the-real-time-customer-data-platform.html) - Integrerar data mellan datakällor för att ge kampanjens drivkraft. Dessa data används sedan för att skapa kampanjmålgrupper och ta fram personaliserade dataelement som används i e-postmeddelanden och webbkampanjpaneler (till exempel namn eller kontorelaterad information). CDP används också för att aktivera målgrupper via e-post och webben (via [!DNL Adobe Target]).
   * [Scheman](/help/xdm/home.md)
   * [Profiler](/help/profile/home.md)
   * [Datauppsättningar](/help/catalog/datasets/overview.md)
   * [Målgrupper](/help/segmentation/home.md)
   * [[!DNL Adobe Journey Optimizer]](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/journey.html)
   * [Mål ](/help/destinations/home.md)
   * [Händelse- eller målutlösare](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioning/collect-event-data/data-collection.html)
   * [Målgrupper/evenemang](https://experienceleague.adobe.com/docs/journey-optimizer/using/audiences-profiles-identities/audiences/about-audiences.html)
   * [Reseåtgärder](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/journey.html)

### Så här uppnår du användningsfallet: översikt på hög nivå {#achieve-the-use-case-high-level}

Nedan visas en översikt över de tre exemplen på återengagemangsresor.

>[!BEGINTABS]

>[!TAB Engagement Journey på nytt]

Återengagemanget syftar till att överge produktsurfning både på webbplatsen och i mobilappen. Den här resan utlöses när en produkt har visats men inte köpts eller lagts till i kundvagnen. Varumärkesinteraktionen utlöses efter tre dagar om det inte finns några listtillägg under de senaste 24 timmarna.<p>![Kundens intelligenta resa för återengagemang på hög visuell nivå.](../intelligent-re-engagement/images/re-engagement-journey.png "Kundens intelligenta resa för återengagemang på hög visuell nivå."){width="2560" zoomable="yes"}</p>

1. Du kan skapa scheman och datauppsättningar och sedan markera för [!UICONTROL Profile].
2. Data integreras i Experience Platform via Web SDK, Mobile Edge SDK eller API. Analytics Data Connector kan också användas, men kan resultera i fördröjning för resan.
3. Ni läser in profiler i Real-Time CDP och bygger styrningspolicyer för att säkerställa ansvarsfull användning.
4. Du bygger fokuserade målgrupper från listan med profiler för att kontrollera om en **kund** har gjort ett engagemang de senaste tre dagarna.
5. Ni skapar en resa för återengagemang i [!DNL Adobe Journey Optimizer].
6. Arbeta med **datapartner** för aktivering av målgrupper till önskade betalmediematerial.
7. [!DNL Adobe Journey Optimizer] söker efter samtycke och skickar ut de olika konfigurerade åtgärderna.

>[!TAB Övergiven Cart Journey]

Den övergivna kundvagnsresan avser produkter som har placerats i vagnen men ännu inte köpts på både webbplatsen och mobilappen. Betalda mediekampanjer startas och stoppas med den här metoden.<p>![Kundens övergivna kundvagnsresa en överblick på hög nivå.](../intelligent-re-engagement/images/abandoned-cart-journey.png "Kundens övergivna kundvagnsresa en överblick på hög nivå."){width="2560" zoomable="yes"}</p>

1. Du skapar scheman och datauppsättningar, [!UICONTROL Profile].
2. Data integreras i Experience Platform via Web SDK, Mobile Edge SDK eller API. Analytics Data Connector kan också användas, men kan resultera i fördröjning för resan.
3. Ni läser in profiler i Real-Time CDP och bygger styrningspolicyer för att säkerställa ansvarsfull användning.
4. Du bygger fokuserade målgrupper från listan med profiler för att kontrollera om en **kund** har placerat en artikel i kundvagnen men inte slutfört köpet. The **[!UICONTROL Add to cart]** event startar en timer som väntar i 30 minuter och sedan söker efter köp. Om inget köp har gjorts **kund** läggs till i **[!UICONTROL Abandon Cart]** målgrupper.
5. Du skapar en övergiven kundvagnsresa i [!DNL Adobe Journey Optimizer].
6. Arbeta med **datapartner** för aktivering av målgrupper till önskade betalmediematerial.
7. [!DNL Adobe Journey Optimizer] söker efter samtycke och skickar ut de olika konfigurerade åtgärderna.

>[!TAB Orderbekräftelse - Resa]

Beställningsbekräftelsen fokuserar på produktinköp via webbplatsen och mobilappen.<p>![Kundorderbekräftelseresan - en överblick på hög nivå.](../intelligent-re-engagement/images/order-confirmation-journey.png "Kundorderbekräftelseresan - en överblick på hög nivå."){width="2560" zoomable="yes"}</p>

1. Du kan skapa scheman och datauppsättningar och sedan markera för [!UICONTROL Profile].
2. Data integreras i Experience Platform via Web SDK, Mobile Edge SDK eller API. Analytics Data Connector kan också användas, men kan resultera i fördröjning för resan.
3. Ni läser in profiler i Real-Time CDP och bygger styrningspolicyer för att säkerställa ansvarsfull användning.
4. Du skapar en bekräftelseresa i [!DNL Adobe Journey Optimizer].
5. [!DNL Adobe Journey Optimizer] skickar ett orderbekräftelsemeddelande via den önskade kanalen.

>[!ENDTABS]

## Hur man uppnår användningsfallet {#achieve-use-case-instruction}

Om du vill slutföra varje steg i översikterna ovan kan du läsa igenom avsnitten nedan som innehåller länkar till mer information och mer detaljerade anvisningar.

### Gränssnittsfunktioner och -element som du använder {#ui-functionality-and-elements}

När du är klar med implementeringen av användningsexemplet kommer du att använda de Real-Time CDP-funktioner och gränssnittselement som listas i början av det här dokumentet. Se till att du har de nödvändiga attributbaserade behörigheterna för åtkomstkontroll i alla dessa områden, eller be systemadministratören att ge dig de behörigheter som krävs.

### Skapa en schemadesign och ange fältgrupper {#schema-design}

Experience Data Model-resurser (XDM) hanteras i [!UICONTROL Schemas] arbetsyta i [!DNL Adobe Experience Platform]. Du kan se och utforska de viktigaste resurserna i [!DNL Adobe] (till exempel [!UICONTROL Field Groups]) och skapa anpassade resurser och scheman för er organisation.

Mer information om hur du skapar [scheman](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=sv), läsa [skapa schemakurs.](/help/xdm/tutorials/create-schema-ui.md)

Det finns fyra schemadesigner som används för återanvändning. Varje schema kräver att specifika fält ställs in och vissa fält som är starkt rekommenderade.

#### Kundattributschema

Det här schemat används för att strukturera och referera till profildata som utgör kundinformationen. Dessa data är vanligtvis insamlade i [!DNL Adobe Experience Platform] via ditt CRM-system eller liknande system och är nödvändigt för att referera till kundinformation som används för personalisering, marknadsföringsmedgivande och förbättrade segmenteringsfunktioner.

Kundattributschemat representeras av en [!UICONTROL XDM Individual Profile] -klass, som innehåller följande fältgrupper:

+++Personlig kontaktinformation (fältgrupp)

[Kontaktinformation, privat](/help/xdm/field-groups/profile/personal-contact-details.md) är en standardschemafältgrupp för klassen XDM Individual Profile som beskriver kontaktinformationen för en enskild person.

| Fält | Krav | Beskrivning |
| --- | --- | --- |
| `mobilePhone.number` | Obligatoriskt | Personens mobiltelefonnummer, som kommer att användas för SMS. |
| `personalEmail.address` | Obligatoriskt | Personens e-postadress. |

+++

+++Demografisk information (fältgrupp)

[Demografiska detaljer](/help/xdm/field-groups/profile/demographic-details.md) är en standardschemafältgrupp för klassen XDM Individual Profile. Fältgruppen innehåller ett personobjekt på rotnivå, vars underfält beskriver information om en enskild person.

| Fält | Krav |
| --- | --- |
| `person.name.firstName` | Föreslagen |
| `person.name.lastName` | Föreslagen |

+++

+++Extern källsystemsgranskningsinformation (fältgrupp)

[Granskningsattribut för externt källsystem](/help/xdm/data-types/external-source-system-audit-attributes.md) är en XDM-datatyp (Standard Experience Data Model) som samlar in granskningsinformation om ett externt källsystem.

+++

+++Grupper för samtycke och inställningsfält (fältgrupp)

[Innehåll och inställningar](/help/xdm/field-groups//profile/consents.md) fältgruppen innehåller ett enda fält av objekttyp, samtycke, för att hämta information om samtycke och inställningar.

| Fält | Krav |
| --- | --- |
| `consents.marketing.email.val` | Obligatoriskt |
| `consents.marketing.preferred` | Obligatoriskt |
| `consents.marketing.push.val` | Obligatoriskt |
| `consents.marketing.sms.val` | Obligatoriskt |
| `consents.personalize.content.val` | Obligatoriskt |
| `consents.share.val` | Obligatoriskt |

+++

+++Profiltestinformation (fältgrupp)

Den här fältgruppen används för bästa praxis.

+++

#### Kundens digitala transaktionsschema

Det här schemat används för att strukturera och referera till händelsedata som utgör kundaktiviteten på din webbplats och/eller tillhörande digitala plattformar. Dessa data är vanligtvis insamlade i [!DNL Adobe Experience Platform] via Web SDK och är nödvändigt för att kunna hänvisa till de olika bläddrings- och konverteringshändelser som används för att utlösa resor, detaljerad kundanalys online och utökade segmenteringsfunktioner.

Kundens digitala transaktionsschema representeras av en [!UICONTROL XDM ExperienceEvent] -klass, som innehåller följande fältgrupper:

+++Adobe Experience Platform Web SDK ExperienceEvent (fältgrupp)

| Fält | Krav |
| --- | --- |
| `device.model` | Föreslagen |
| `environment.browserDetails.userAgent` | Föreslagen |

+++

+++Webbinformation (fältgrupp)

Webbinformation är en standardschemafältgrupp för klassen XDM ExperienceEvent, som används för att beskriva information om webbinformationshändelser som interaktion, sidinformation och referent.

| Fält | Krav | Beskrivning |
| --- | --- | --- |
| `web.webInteraction.linkClicks.id` | Föreslagen | ID för webblänken eller URL-adressen som motsvarar interaktionen. |
| `web.webInteraction.linkClicks.value` | Föreslagen | Antalet klick för webblänken eller URL-adressen som motsvarar interaktionen. |
| `web.webInteraction.name` | Föreslagen | Webbsidans namn. |
| `web.webInteraction.URL` | Föreslagen | Webbsidans URL. |
| `web.webPageDetails.name` | Föreslagen | Namnet på webbsidan där webbinteraktionen inträffade. |
| `web.webPageDetails.URL` | Föreslagen | Webbsidans URL där webbinteraktionen inträffade. |
| `web.webReferrer.URL` | Föreslagen | Beskriver referenten till en webbinteraktion, vilket är den URL som en besökare kom från omedelbart innan den aktuella webbinteraktionen spelades in. |

+++

+++Consumer Experience Event (Field Group)

| Fält | Krav |
| --- | --- |
| `commerce.cart.cartID` | Föreslagen |
| `commerce.cart.cartSource` | Föreslagen |
| `commerce.cartAbandons.id` | Föreslagen |
| `commerce.cartAbandons.value` | Föreslagen |
| `commerce.order.orderType` | Föreslagen |
| `commerce.order.payments.paymentAmount` | Föreslagen |
| `commerce.order.payments.paymentType` | Föreslagen |
| `commerce.order.payments.transactionID` | Föreslagen |
| `commerce.order.priceTotal` | Föreslagen |
| `commerce.order.purchaseID` | Föreslagen |
| `commerce.productListAdds.id` | Föreslagen |
| `commerce.productListAdds.value` | Föreslagen |
| `commerce.productListOpens.id` | Föreslagen |
| `commerce.productListOpens.value` | Föreslagen |
| `commerce.productListRemoval.id` | Föreslagen |
| `commerce.productListRemoval.value` | Föreslagen |
| `commerce.productListViews.id` | Föreslagen |
| `commerce.productListViews.value` | Föreslagen |
| `commerce.productViews.id` | Föreslagen |
| `commerce.productViews.value` | Föreslagen |
| `commerce.purchases.id` | Föreslagen |
| `commerce.purchases.value` | Föreslagen |
| `marketing.campaignGroup` | Föreslagen |
| `marketing.campaignName` | Föreslagen |
| `marketing.trackingCode` | Föreslagen |
| `productListItems.name` | Föreslagen |
| `productListItems.priceTotal` | Föreslagen |
| `productListItems.product` | Föreslagen |
| `productListItems.quantity` | Föreslagen |

+++

+++Slutanvändar-ID-information (fältgrupp)

| Fält | Krav | Beskrivning |
| --- | --- | --- |
| `endUserIDs._experience.emailid.authenticatedState` | Obligatoriskt | Slutanvändarens e-postadress-ID har autentiserats. |
| `endUserIDs._experience.emailid.id` | Obligatoriskt | Slutanvändarens e-postadress-ID. |
| `endUserIDs._experience.emailid.namespace.code` | Obligatoriskt | ID-namnområdeskod för slutanvändarens e-postadress. |
| `endUserIDs._experience.mcid.authenticatedState` | Obligatoriskt | [!DNL Adobe] Marketing Cloud ID (MCID) autentiserad. MCID kallas nu Experience Cloud-ID (ECID). |
| `endUserIDs._experience.mcid.id` | Obligatoriskt | [!DNL Adobe] Marketing Cloud ID (MCID). MCID kallas nu Experience Cloud-ID (ECID). |
| `endUserIDs._experience.mcid.namespace.code` | Obligatoriskt | [!DNL Adobe] Marketing Cloud ID-namnområdeskod (MCID). |

+++

+++Extern källsystemsgranskningsinformation (fältgrupp)

Granskningsattribut för externt källsystem är en XDM-datatyp (Experience Data Model) som samlar in granskningsinformation om ett externt källsystem.

+++

#### Schema för offlinetransaktioner för kund

Det här schemat används för att strukturera och referera till händelsedata som utgör kundaktiviteten på plattformar utanför webbplatsen. Dessa data är vanligtvis insamlade i [!DNL Adobe Experience Platform] från en POS (eller liknande system) och som oftast strömmas till plattformen via en API-anslutning. Syftet är att hänvisa till olika offlinekonverteringshändelser som används för att utlösa resor, djupgående kundanalyser online och offline samt förbättrade segmenteringsfunktioner.

Kundens offlinetransaktionsschema representeras av en [!UICONTROL XDM ExperienceEvent] -klass, som innehåller följande fältgrupper:

+++Commerce Details (fältgrupp)

| Fält | Krav | Beskrivning |
| --- | --- | --- |
| `commerce.cart.cartID` | Obligatoriskt | Ett ID för kundvagnen. |
| `commerce.order.orderType` | Obligatoriskt | Ett objekt som beskriver produktordertypen. |
| `commerce.order.payments.paymentAmount` | Obligatoriskt | Ett objekt som beskriver betalningsbeloppet för produktorder. |
| `commerce.order.payments.paymentType` | Obligatoriskt | Ett objekt som beskriver betalningstypen för produktorder. |
| `commerce.order.payments.transactionID` | Obligatoriskt | Ett transaktions-ID för objektproduktorder. |
| `commerce.order.purchaseID` | Obligatoriskt | Ett objektproduktorderns inköps-ID. |
| `productListItems.name` | Obligatoriskt | En lista med artikelnamn som representerar de produkter som en kund har valt. |
| `productListItems.priceTotal` | Obligatoriskt | Det totala priset på en lista med artiklar som representerar de produkter som kunden har valt. |
| `productListItems.product` | Obligatoriskt | Produkten/produkterna som valts. |
| `productListItems.quantity` | Obligatoriskt | Kvantiteten i en lista över artiklar som representerar de produkter som kunden har valt. |

+++

+++Personlig kontaktinformation (fältgrupp)

| Fält | Krav | Beskrivning |
| --- | --- | --- |
| `mobilePhone.number` | Obligatoriskt | Personens mobiltelefonnummer, som kommer att användas för SMS. |
| `personalEmail.address` | Obligatoriskt | Personens e-postadress. |

+++

+++Extern källsystemsgranskningsinformation (fältgrupp)

Granskningsattribut för externt källsystem är en XDM-datatyp (Experience Data Model) som samlar in granskningsinformation om ett externt källsystem.

+++

#### Adobe webbanslutningsschema

>[!NOTE]
>
>Detta är en valfri implementering om du använder [!DNL Adobe Analytics Data Connector].

Det här schemat används för att strukturera och referera till händelsedata som utgör kundaktiviteten på din webbplats och/eller tillhörande digitala plattformar. Det här schemat liknar kundens schema för digitala transaktioner, men skiljer sig åt på så sätt att det är avsett att användas när Web SDK inte är ett alternativ för datainsamling. Därför behövs det här schemat när du använder [!DNL Adobe Analytics Data Connector] för att skicka onlinedata till [!DNL Adobe Experience Platform] antingen som primär eller sekundär datastream.

The [!DNL Adobe] webbanslutningsschemat representeras av en [!UICONTROL XDM ExperienceEvent] -klass, som innehåller följande fältgrupper:

+++Adobe Analytics ExperienceEvent-mall (fältgrupp)

| Fält | Krav | Beskrivning |
| --- | --- | --- |
| `web.webInteraction.linkClicks.id` | Föreslagen | ID för webblänken eller URL-adressen som motsvarar interaktionen. |
| `web.webInteraction.linkClicks.value` | Föreslagen | Antalet klick för webblänken eller URL-adressen som motsvarar interaktionen. |
| `web.webInteraction.name` | Föreslagen | Webbsidans namn. |
| `web.webInteraction.URL` | Föreslagen | Webbsidans URL. |
| `web.webPageDetails.name` | Föreslagen | Namnet på webbsidan där webbinteraktionen inträffade. |
| `web.webPageDetails.URL` | Föreslagen | Webbsidans URL där webbinteraktionen inträffade. |
| `web.webReferrer.URL` | Föreslagen | Beskriver referenten till en webbinteraktion, vilket är den URL som en besökare kom från omedelbart innan den aktuella webbinteraktionen spelades in. |
| `commerce.cart.cartID` | Föreslagen | |
| `commerce.cart.cartSource` | Föreslagen | |
| `commerce.cartAbandons.id` | Föreslagen | |
| `commerce.cartAbandons.value` | Föreslagen | |
| `commerce.order.orderType` | Föreslagen | |
| `commerce.order.payments.paymentAmount` | Föreslagen | |
| `commerce.order.payments.paymentType` | Föreslagen | |
| `commerce.order.payments.transactionID` | Föreslagen | |
| `commerce.order.priceTotal` | Föreslagen | |
| `commerce.order.purchaseID` | Föreslagen | |
| `commerce.productListAdds.id` | Föreslagen | |
| `commerce.productListAdds.value` | Föreslagen | |
| `commerce.productListOpens.id` | Föreslagen | |
| `commerce.productListOpens.value` | Föreslagen | |
| `commerce.productListRemoval.id` | Föreslagen | |
| `commerce.productListRemoval.value` | Föreslagen | |
| `commerce.productListViews.id` | Föreslagen | |
| `commerce.productListViews.value` | Föreslagen | |
| `commerce.productViews.id` | Föreslagen | |
| `commerce.productViews.value` | Föreslagen | |
| `commerce.purchases.id` | Föreslagen | |
| `commerce.purchases.value` | Föreslagen | |
| `marketing.campaignGroup` | Föreslagen | |
| `marketing.campaignName` | Föreslagen | |
| `marketing.trackingCode` | Föreslagen | |
| `productListItems.name` | Föreslagen | |
| `productListItems.priceTotal` | Föreslagen | |
| `productListItems.product` | Föreslagen | |
| `productListItems.quantity` | Föreslagen | |
| `endUserIDs._experience.emailid.authenticatedState` | Obligatoriskt | Slutanvändarens e-postadress-ID har autentiserats. |
| `endUserIDs._experience.emailid.id` | Obligatoriskt | Slutanvändarens e-postadress-ID. |
| `endUserIDs._experience.emailid.namespace.code` | Obligatoriskt | ID-namnområdeskod för slutanvändarens e-postadress. |
| `endUserIDs._experience.mcid.authenticatedState` | Obligatoriskt | [!DNL Adobe] Marketing Cloud ID (MCID) autentiserad. MCID kallas nu Experience Cloud-ID (ECID). |
| `endUserIDs._experience.mcid.id` | Obligatoriskt | [!DNL Adobe] Marketing Cloud ID (MCID). MCID kallas nu Experience Cloud-ID (ECID). |
| `endUserIDs._experience.mcid.namespace.code` | Obligatoriskt | [!DNL Adobe] Marketing Cloud ID-namnområdeskod (MCID). |

+++

+++Extern källsystemsgranskningsinformation (fältgrupp)

Granskningsattribut för externt källsystem är en XDM-datatyp (Experience Data Model) som samlar in granskningsinformation om ett externt källsystem.

+++

### Skapa en datauppsättning från ett schema {#dataset-from-schema}

En datauppsättning är en lagrings- och hanteringsstruktur för en grupp med data. Varje schema för intelligenta återengagemangsresor har en enda datauppsättning.

Mer information om hur du skapar en [datauppsättning](/help/catalog/datasets/overview.md) från ett schema, läs [Användargränssnittshandbok för datauppsättningar](/help/catalog/datasets/user-guide.md).

>[!NOTE]
>
>På samma sätt som när du skapar ett schema måste du aktivera datauppsättningen som ska inkluderas i kundprofilen i realtid. Mer information om hur du aktiverar datauppsättningen för användning i kundprofilen i realtid finns i [skapa schemakurs.](/help/xdm/tutorials/create-schema-ui.md#profile).

### Integritet, samtycke och datahantering {#privacy-consent}

#### Samtyckesprinciper

>[!IMPORTANT]
>
>Att ge kunderna möjlighet att säga upp prenumerationen på information från ett varumärke är ett juridiskt krav, liksom att se till att detta val respekteras. Läs mer om gällande lagstiftning i [Översikt över sekretessbestämmelser](https://experienceleague.adobe.com/docs/experience-platform/privacy/regulations/overview.html).

Följande gäller när du skapar en ny engagemangsväg: [medgivandeprinciper](https://experienceleague.adobe.com/docs/platform-learn/data-collection/web-sdk/consent/overview.html) bör beaktas:

* If `consents.marketing.email.val = "Y"` kan e-posta
* If `consents.marketing.sms.val = "Y"` kan SMS
* If `consents.marketing.push.val = "Y"` sedan Can Push
* If `consents.share.val = "Y"` så kan annonsera

#### Etikett och verkställighet för datastyrning

Följande gäller när du skapar en ny engagemangsväg: [Etiketter för datastyrning](/help/data-governance/labels/overview.md) bör beaktas:

* Personliga e-postadresser används som direkt identifierbara data som används för att identifiera eller komma i kontakt med en viss individ i stället för en enhet.
   * `personalEmail.address = I1`

#### Marknadspolicyer

Det finns inga [marknadsföringspolicyer](/help/data-governance/policies/overview.md) som krävs för resor med återengagemang bör dock följande beaktas efter behov:

* Begränsa känsliga data
* Begränsa annonsering på plats
* Begränsa e-postmålning
* Begränsa mål för flera webbplatser
* Begränsa kombinationen av direkt identifierbara data med anonyma data

### Skapa en målgrupp {#create-audience}

#### Målgruppsskapande för varumärkesåterengagemangsresor

Återengagemangsresorna använder målgrupper för att definiera specifika attribut eller beteenden som delas av en deluppsättning profiler från din profilbutik för att skilja en marknadsföringsbar grupp av människor från er kundbas. Målgrupper kan skapas på flera sätt [!DNL Adobe Experience Platform].

Mer information om hur du skapar en målgrupp finns i [Användargränssnittsguide för målgruppstjänst](https://experienceleague.adobe.com/docs/experience-platform/segmentation/ui/overview.html#create-audience).

Mer information om hur du skapar direkt [Målgrupper](/help/segmentation/home.md), läsa [Användargränssnittsguide för målgruppskomposition](/help/segmentation/ui/audience-composition.md).

Mer information om hur du bygger målgrupper med hjälp av plattformsbaserade segmentdefinitioner finns i [Användargränssnittshandbok för Audience Builder](/help/segmentation/ui/segment-builder.md).

>[!BEGINTABS]

>[!TAB Engagement Journey på nytt]

Den här målgruppen har skapats som en förbättring av det klassiska&quot;Cart Abandonment&quot;-scenariot. Medan kundvagnsuppsägning vanligtvis fokuserar på ett kundvagnstillägg utan att man behöver göra ett senare inköp under en viss tidsperiod, letar denna målgrupp efter ett tidigare engagemang, särskilt de som har bläddrat efter en viss produkt men inte lagt till den i kundvagnen och inte haft någon uppföljningsaktivitet på er webbplats inom en viss tidsperiod. Den här målgruppen ser till att ert varumärke&quot;ligger överst&quot; för kunder som uppfyller detta inkluderingskriterier och kan även utnyttjas för kunder vars digitala egenskaper kan skilja sig från en traditionell e-handelsmodell.

Följande händelser används för återengagemangsresan där användarna tittade på produkter online och inte lade till i kundvagnen under de kommande 24 timmarna, följt av inget varumärkesengagemang under de kommande 3 dagarna.

Följande fält och villkor krävs när du konfigurerar den här målgruppen:

* `EventType: commerce.productViews`
   * `Timestamp: <= 24 hours before now`
* `EventType is not: commerce.procuctListAdds`
   * `Timestamp: <= 24 hours before now, GAP(>= 3 days)`
* `EventType: application.launch or web.webpagedetails.pageViews or commerce.purchases`
   * `Timestamp: <= 2 days before now`

Beskrivningen för återengagemangsresan visas som:

`Include audience who have at least 1 EventType = ProductViews event THEN have at least 1 Any event where (EventType does not equal commerce.productListAdds) and occurs in last 24 hour(s) then after 3 days do not have any Any event where (EventType = application.launch or web.webpagedetails.pageViews or commerce.purchases) and occurs in last 2 day(s).`

>[!TAB Övergiven Cart Journey]

Den här målgruppen har skapats för att stödja det klassiska&quot;Cart Abandonment&quot;-scenariot. Syftet är att hitta kunder som har lagt till en produkt i kundvagnen men i slutändan inte har lyckats med ett köp. Den här målgruppen hjälper er att inte bara hålla ert varumärke&quot;högst i sinnet&quot; för era kunder, utan även de produkter de lämnade utan ett efterföljande köp.

Följande händelser används för den övergivna kundvagnsresan där användarna lade till en produkt i kundvagnen, men inte slutförde köpet eller rensade kundvagnen de senaste 24 timmarna.

Följande fält och villkor krävs när du konfigurerar den här målgruppen:

* `EventType: commerce.productListAdds`
   * `Timestamp: >= 1 days before now and <= 4 days before now `
* `EventType: commerce.purchases`
   * `Timestamp: <= 4 days before now`
* `EventType: commerce.productListRemovals`
   * `Timestamp: <= 4 days before now`

Beskrivningen för den övergivna kundvagnsresan visas som:

`Include EventType = commerce.productListAdds between 30 min and 1440 minutes before now. exclude EventType = commerce.purchases 30 minutes before now OR EventType = commerce.productListRemovals AND Cart ID equals Product List Adds1 Cart ID (the inclusion event).`

>[!TAB Orderbekräftelse - Resa]

Den här resan kräver inte att någon målgrupp skapas.

>[!ENDTABS]

### Resekonfiguration i Adobe Journey Optimizer {#journey-setup}

>[!NOTE]
>
>[!DNL Adobe Journey Optimizer] omfattar inte allt som visas i diagrammen. Alla [annonser för betalda medier](/help/destinations/catalog/social/overview.md) skapas i [!UICONTROL Destinations].

[[!DNL Adobe Journey Optimizer]](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/journey.html) hjälper er att leverera sammankopplade, kontextuella och personaliserade upplevelser till era kunder. Kundresan är hela processen för en kunds interaktioner med varumärket. Varje användningsfallsresa kräver specifik information. Nedan finns de exakta data som behövs för varje resegren.

>[!BEGINTABS]

>[!TAB Engagement Journey på nytt]

Återengagemanget syftar till att överge produktsurfning både på webbplatsen och i mobilappen.<p>![Kundens intelligenta resa för återengagemang på hög visuell nivå.](../intelligent-re-engagement/images/re-engagement-journey.png "Kundens intelligenta resa för återengagemang på hög visuell nivå."){width="2560" zoomable="yes"}</p>

+++Händelser

* Händelse 1: Produktvyer
   * Schema: Digitala kundtransaktioner
   * Fält:
      * `EventType`
   * Villkor:
      * `EventType = commerce.productViews`
      * Fält:
         * `Commerce.productViews.id`
         * `Commerce.productViews.value`
         * `eventType`
         * `identityMap.authenticatedState`
         * `identityMap.id`
         * `identityMap.primary`
         * `productListItems.SKU`
         * `productListItems.currencyCode`
         * `productListItems.name`
         * `productListItems.priceTotal`
         * `productListItems.product`
         * `productListItems.productImageUrl`
         * `productListItems.quantity`
         * `timestamp`
         * `endUserIDs._experience.emailid.authenticatedState`
         * `endUserIDs._experience.emailid.id`
         * `endUserIDs._experience.emailid.namespace.code`
         * `_id`

* Händelse 2: Lägg i kundvagnen
   * Schema: Digitala kundtransaktioner
   * Fält:
      * `EventType`
   * Villkor:
      * `EventType = commerce.productListAdds`
      * Fält:
         * `Commerce.productListAdds.id`
         * `Commerce.productListAdds.value`
         * `eventType`
         * `identityMap.authenticatedState`
         * `identityMap.id`
         * `identityMap.primary`
         * `productListItems.SKU`
         * `productListItems.currencyCode`
         * `productListItems.name`
         * `productListItems.priceTotal`
         * `productListItems.product`
         * `productListItems.productImageUrl`
         * `productListItems.quantity`
         * `timestamp`
         * `commerce.cart.cartID`
         * `endUserIDs._experience.emailid.authenticatedState`
         * `endUserIDs._experience.emailid.id`
         * `endUserIDs._experience.emailid.namespace.code`
         * `_id`

* Händelse 3: Varumärkesengagemang
   * Schema: Digitala kundtransaktioner
   * Fält:
      * `EventType`
   * Villkor:
      * `EventType in application.launch, commerce.purchases, web.webpagedetails.pageViews`
      * Fält:
         * `eventType`
         * `identityMap.authenticatedState`
         * `identityMap.id`
         * `identityMap.primary`
         * `productListItems.SKU`
         * `productListItems.currencyCode`
         * `productListItems.name`
         * `productListItems.priceTotal`
         * `productListItems.product`
         * `productListItems.productImageUrl`
         * `productListItems.quantity`
         * `timestamp`
         * `web.webpagedetails.URL`
         * `web.webpagedetails.isHomePage`
         * `web.webpagedetails.name`
         * `endUserIDs._experience.emailid.authenticatedState`
         * `endUserIDs._experience.emailid.id`
         * `endUserIDs._experience.emailid.namespace.code`
         * `_id`
         * `Commerce.purchases.id`
         * `Commerce.purchases.value`
         * `shipping.address.city`
         * `shipping.address.countryCode`
         * `shipping.address.postalCode`
         * `shipping.address.state`
         * `shipping.address.street1`
         * `shipping.address.street2`
         * `shipping.shipDate`
         * `shipping.trackingNumber`
         * `shipping.trackingURL`

+++

+++Key Journey logic

* Inmatningslogik för resebidrag
   * Produktvyhändelse

* Villkor
   * Kontrollera om det finns minst en köphändelse online eller offline sedan produkten senast visades.
      * Schema: Digitala kundtransaktioner
      * `eventType = commerce.purchases`
      * `timestamp > timestamp of product last viewed`

   * Sök efter minst ett offlineköp sedan produkten senast visades:
      * Schema: Kundoffline-transaktioner
      * `eventType = commerce.purchases`
      * `timestamp > timestamp of product last viewed`

   * Villkor - Välj målkanal
      * E-post
         * `consents.marketing.email.val = y`
      * Push
         * `consents.marketing.push.val=y`
      * SMS
         * `consents.marketing.sms.val = y`

   * Kanalanpassning
      * Personaliserat kanalinnehåll baserat på produktvy.

+++

>[!TAB Övergiven Cart Journey]

Den övergivna kundvagnsresan avser produkter som har placerats i vagnen men ännu inte köpts på både webbplatsen och mobilappen.<p>![Kundens övergivna kundvagnsresa en överblick på hög nivå.](../intelligent-re-engagement/images/abandoned-cart-journey.png "Kundens övergivna kundvagnsresa en överblick på hög nivå."){width="2560" zoomable="yes"}</p>

+++Händelser

* Händelse 2: Lägg i kundvagnen
   * Schema: Digitala kundtransaktioner
   * Fält:
      * `EventType`
   * Villkor:
      * `EventType = commerce.productListAdds`
      * Fält:
         * `Commerce.productListAdds.id`
         * `Commerce.productListAdds.value`
         * `eventType`
         * `identityMap.authenticatedState`
         * `identityMap.id`
         * `identityMap.primary`
         * `productListItems.SKU`
         * `productListItems.currencyCode`
         * `productListItems.name`
         * `productListItems.priceTotal`
         * `productListItems.product`
         * `productListItems.productImageUrl`
         * `productListItems.quantity`
         * `timestamp`
         * `commerce.cart.cartID`
         * `endUserIDs._experience.emailid.authenticatedState`
         * `endUserIDs._experience.emailid.id`
         * `endUserIDs._experience.emailid.namespace.code`
         * `_id`

* Evenemang 4: Onlineköp
   * Schema: Digitala kundtransaktioner
   * Fält:
      * `EventType`
   * Villkor:
      * `EventType = commerce.purchases`
      * Fält:
         * `Commerce.purchases.id`
         * `Commerce.purchases.value`
         * `eventType`
         * `identityMap.authenticatedState`
         * `identityMap.id`
         * `identityMap.primary`
         * `productListItems.SKU`
         * `productListItems.currencyCode`
         * `productListItems.name`
         * `productListItems.priceTotal`
         * `productListItems.product`
         * `productListItems.productImageUrl`
         * `productListItems.quantity`
         * `timestamp`
         * `endUserIDs._experience.emailid.authenticatedState`
         * `endUserIDs._experience.emailid.id`
         * `endUserIDs._experience.emailid.namespace.code`
         * `_id`

* Händelse 3: Varumärkesengagemang
   * Schema: Digitala kundtransaktioner
   * Fält:
      * `EventType`
   * Villkor:
      * `EventType in application.launch, commerce.purchases, web.webpagedetails.pageViews`
      * Fält:
         * `eventType`
         * `identityMap.authenticatedState`
         * `identityMap.id`
         * `identityMap.primary`
         * `productListItems.SKU`
         * `productListItems.currencyCode`
         * `productListItems.name`
         * `productListItems.priceTotal`
         * `productListItems.product`
         * `productListItems.productImageUrl`
         * `productListItems.quantity`
         * `timestamp`
         * `web.webpagedetails.URL`
         * `web.webpagedetails.isHomePage`
         * `web.webpagedetails.name`
         * `endUserIDs._experience.emailid.authenticatedState`
         * `endUserIDs._experience.emailid.id`
         * `endUserIDs._experience.emailid.namespace.code`
         * `_id`
         * `Commerce.purchases.id`
         * `Commerce.purchases.value`
         * `shipping.address.city`
         * `shipping.address.countryCode`
         * `shipping.address.postalCode`
         * `shipping.address.state`
         * `shipping.address.street1`
         * `shipping.address.street2`
         * `shipping.shipDate`
         * `shipping.trackingNumber`
         * `shipping.trackingURL`

+++

+++Key Journey Logic

* Inmatningslogik för resebidrag
   * `AddToCart` Händelse

* AuthenticatedState in authenticated

* Villkor: Offlineköp sedan vagnen senast övergavs:
   * Schema: Kundoffline-transaktioner
   * `eventType = commerce.purchases`
   * `timestamp > timestamp of cart was last abandoned`

* Villkor: vagnen har rensats sedan vagnen senast övergavs:
   * Schema: Digitala kundtransaktioner
   * `eventType = commerce.cartCleared`
   * `cartID` (ID för vagnen)
   * `timestamp > timestamp of cart was last abandoned`

* Välj målkanal (markera en eller flera kanaler för bredare räckvidd)
   * E-post
      * `consents.marketing.email.val = y`
   * Push
      * `consents.marketing.push.val = y`
   * SMS
      * `consents.marketing.sms.val = y`
   * Kanalanpassning
      * Visa kundvagnsinformation och kan visa flera produkter i ett tabellformat.

+++

>[!TAB Orderbekräftelse - Resa]

Beställningsbekräftelsen fokuserar på produktinköp via webbplatsen och mobilappen.<p>![Kundorderbekräftelseresan - en överblick på hög nivå.](../intelligent-re-engagement/images/order-confirmation-journey.png "Kundorderbekräftelseresan - en överblick på hög nivå."){width="2560" zoomable="yes"}</p>

+++Händelser

* Evenemang 4: Onlineköp
   * Schema: Digitala kundtransaktioner
   * Fält:
      * `EventType`
   * Villkor:
      * `EventType = commerce.purchases`
      * Fält:
         * `Commerce.purchases.id`
         * `Commerce.purchases.value`
         * `eventType`
         * `identityMap.authenticatedState`
         * `identityMap.id`
         * `identityMap.primary`
         * `productListItems.SKU`
         * `productListItems.currencyCode`
         * `productListItems.name`
         * `productListItems.priceTotal`
         * `productListItems.product`
         * `productListItems.productImageUrl`
         * `productListItems.quantity`
         * `timestamp`
         * `endUserIDs._experience.emailid.authenticatedState`
         * `endUserIDs._experience.emailid.id`
         * `endUserIDs._experience.emailid.namespace.code`
         * `_id`

+++

+++Key Journey logic

* Inmatningslogik för resebidrag
   * Orderhändelse

* Villkor
   * Välj Målkanal (markera en eller flera kanaler för större räckvidd).
      * Orderbekräftelsen anses vara till sin natur, så det är oftast inte nödvändigt att kontrollera samtycke.
      * E-post
      * Push
      * SMS

   * Kanalinnehållspersonalisering
      * Visa information om orderdetaljer och kan visa en lista med produkter i ett tabellformat.

+++

>[!ENDTABS]

Mer information om hur du skapar resor i [!DNL Adobe Journey Optimizer], läsa [Kom igång med reseguiden](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/journey.html).

### Konfigurera annonser för betalda medier i destinationer {#paid-media-ads}

Målramverket används för annonser i betalda medier. När samtycke har checkats ut skickas det till de olika konfigurerade destinationerna. Mer information om destinationer finns i [Översikt över destinationer](/help/destinations/home.md) -dokument.

#### Data som krävs för destinationer

Målplatser för direktuppspelad segmentexport (som Facebook, Google Customer Match, Google DV360) stöder olika identiteter från kunddata:

* `personalEmail.address`
* `ECID`
* `mobilePhone.number`

Övergivningsvagnssegmentet är direktuppspelning och kan därför användas av målramverket för det här användningsfallet.

* Strömma/utlöst
   * [Reklam](/help/destinations/catalog/advertising/overview.md)/[Betalda medier och sociala medier](/help/destinations/catalog/social/overview.md)
   * [Mobil](/help/destinations/catalog/mobile-engagement/overview.md)
   * [Direktuppspelningsmål](/help/destinations/catalog/streaming/http-destination.md)
   * [Anpassad Destination SDK](/help/destinations/destination-sdk/overview.md)
