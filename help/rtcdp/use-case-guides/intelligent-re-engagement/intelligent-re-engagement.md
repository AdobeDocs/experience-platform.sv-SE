---
title: Intelligent återanvändning
description: Leverera övertygande och sammanhängande upplevelser under de viktiga konverteringstunderna för att på ett intelligent sätt engagera ovanliga kunder.
hide: true
hidefromtoc: true
source-git-commit: 43e365e20a2fd91a0e822eb6f66bb7db6fc218f5
workflow-type: tm+mt
source-wordcount: '2915'
ht-degree: 2%

---

# Engagera kunderna på nytt på ett intelligent sätt för att få dem tillbaka

Engagera kunder som har övergett konverteringen på nytt innan de slutför den på ett intelligent och ansvarsfullt sätt. Engagera kunderna genom upplevelser snarare än påminnelser för att öka konverteringsgraden och driva på tillväxten av kundernas livstidsvärde.

Ta hänsyn till kundernas alla egenskaper och beteenden i realtid, ta hänsyn till dem och erbjud snabb omkvalificering baserat på både online- och offlinehändelser.

![Steg för steg intelligent återkoppling av en visuell översikt på hög nivå.](../intelligent-re-engagement/images/step-by-step.png)

## Använd ärendeöversikt

Ni kommer att skapa scheman, datauppsättningar och målgrupper när ni arbetar med exempel på återengagemangsresor. Du kommer också att upptäcka de funktioner som behövs för att konfigurera exempelresor i [!DNL Adobe Journey Optimizer] och de som behövs för att skapa betalannonser i destinationer. I den här guiden används exempel på hur man återengagerar kunder i de användningsfall som beskrivs nedan:

* **Resor för återengagemang** - Rikta in er på kunder som har slutat surfa på webben och i mobilappar.
* **Övergiven kundvagnsresa** - Rikta in er på kunder som har lagt produkter i varukorgen men ännu inte köpt dem på både webbplatsen och i mobilappen.
* **Beställningsbekräftelseresa** - Fokuserar på produktinköp via webbplatsen och mobilappen.

## Förutsättningar och planering {#prerequisites-and-planning}

När du är klar med implementeringen av användningsexemplet kommer du att använda följande Real-Time CDP-funktioner och gränssnittselement (listade i den ordning som du ska använda dem). Se till att du har de nödvändiga attributbaserade behörigheterna för åtkomstkontroll i alla dessa områden, eller be systemadministratören att ge dig de behörigheter som krävs.

* [Adobe Real-time Customer Data Platform (Real-Time CDP)](https://experienceleague.adobe.com/docs/platform-learn/tutorials/rtcdp/understanding-the-real-time-customer-data-platform.html) - Sammanställer data från olika datakällor för att driva kampanjen framåt. Dessa data används sedan för att skapa kampanjmålgrupper och ta fram personaliserade dataelement som används i e-postmeddelanden och webbkampanjpaneler (till exempel namn eller kontorelaterad information). CDP används också för att aktivera målgrupper via e-post och webben (via Adobe Target).
   * [Scheman](/help/xdm/home.md)
   * [Profiler](/help/profile/home.md)
   * [Datauppsättningar](/help/catalog/datasets/overview.md)
   * [Målgrupper](/help/segmentation/home.md)
   * [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/journey.html)
   * [Mål ](/help/destinations/home.md)
   * [Händelse- eller målutlösare](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioning/collect-event-data/data-collection.html)
   * [Målgrupper/evenemang](https://experienceleague.adobe.com/docs/journey-optimizer/using/audiences-profiles-identities/audiences/about-audiences.html)
   * [Reseåtgärder](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/journey.html)

### Så här uppnår du användningsfallet: översikt på hög nivå {#achieve-the-use-case-high-level}

Nedan visas en översikt över de tre exemplen på återengagemangsresor.

>[!BEGINTABS]

>[!TAB Engagement Journey på nytt]

Återengagemanget syftar till att överge produktsurfning både på webbplatsen och i mobilappen. Den här resan utlöses när en produkt har visats men inte köpts eller lagts till i kundvagnen. Varumärkesinteraktionen utlöses efter tre dagar om det inte finns några listtillägg under de senaste 24 timmarna.<p>![Kundens intelligenta resa för återengagemang på hög visuell nivå.](../intelligent-re-engagement/images/re-engagement-journey.png "Kundens intelligenta resa för återengagemang på hög visuell nivå."){width="1920" zoomable="yes"}</p>

1. Du skapar scheman och datauppsättningar som är markerade för [!UICONTROL Profile].
2. Data samlas i Experience Platform via Web SDK, Mobile Edge SDK eller API. Analytics Data Connector kan också användas, men kan resultera i fördröjning för resan.
3. Ni läser in profiler i Real-Time CDP och bygger styrningspolicyer för att säkerställa ansvarsfull användning.
4. Du bygger fokuserade målgrupper från listan med profiler för att kontrollera om en **kund** har gjort ett engagemang de senaste tre dagarna.
5. Ni skapar en resa för återengagemang i [!DNL Adobe Journey Optimizer].
6. Arbeta med **datapartner** för aktivering av målgrupper till önskade betalmediematerial.
7. [!DNL Adobe Journey Optimizer] söker efter samtycke och skickar ut de olika konfigurerade åtgärderna.

>[!TAB Övergiven Cart Journey]

Den övergivna kundvagnsresan avser produkter som har placerats i vagnen men ännu inte köpts på både webbplatsen och mobilappen. Betalda mediekampanjer startas och stoppas med den här metoden.<p>![Kundens övergivna kundvagnsresa en överblick på hög nivå.](../intelligent-re-engagement/images/abandoned-cart-journey.png "Kundens övergivna kundvagnsresa en överblick på hög nivå."){width="1920" zoomable="yes"}</p>

1. Du skapar scheman och datauppsättningar som är markerade för [!UICONTROL Profile].
2. Data samlas i Experience Platform via Web SDK, Mobile Edge SDK eller API. Analytics Data Connector kan också användas, men kan resultera i fördröjning för resan.
3. Ni läser in profiler i Real-Time CDP och bygger styrningspolicyer för att säkerställa ansvarsfull användning.
4. Du bygger fokuserade målgrupper från listan med profiler för att kontrollera om en **kund** har placerat en artikel i kundvagnen men inte slutfört köpet. The **[!UICONTROL Add to cart]** event startar en timer som väntar i 30 minuter och sedan söker efter köp. Om inget köp har gjorts **kund** läggs till i **[!UICONTROL Abandon Cart]** målgrupper.
5. Du skapar en övergiven kundvagnsresa i Adobe Journey Optimizer
6. Arbeta med **datapartner** för aktivering av målgrupper till önskade betalmediematerial.
7. [!DNL Adobe Journey Optimizer] söker efter samtycke och skickar ut de olika konfigurerade åtgärderna.

>[!TAB Orderbekräftelse - Resa]

Beställningsbekräftelsen fokuserar på produktinköp via webbplatsen och mobilappen.<p>![Kundorderbekräftelseresan - en överblick på hög nivå.](../intelligent-re-engagement/images/order-confirmation-journey.png "Kundorderbekräftelseresan - en överblick på hög nivå."){width="1920" zoomable="yes"}</p>

1. Du skapar scheman och datauppsättningar som är markerade för [!UICONTROL Profile].
2. Data samlas i Experience Platform via Web SDK, Mobile Edge SDK eller API. Analytics Data Connector kan också användas, men kan resultera i fördröjning för resan.
3. Ni läser in profiler i Real-Time CDP och bygger styrningspolicyer för att säkerställa ansvarsfull användning.
4. Du bygger fokuserade målgrupper från listan med profiler för att kontrollera om en **kund** har köpt något.
5. Du skapar en bekräftelseresa i Adobe Journey Optimizer.
6. [!DNL Adobe Journey Optimizer] skickar ett orderbekräftelsemeddelande via den önskade kanalen.

>[!ENDTABS]

## Så här uppnår du användningsfallet: stegvisa instruktioner {#step-by-step-instructions}

Om du vill slutföra varje steg i översikterna ovan kan du läsa igenom avsnitten nedan som innehåller länkar till mer information och mer detaljerade anvisningar.

### Gränssnittsfunktioner och -element som du använder {#ui-functionality-and-elements}

När du är klar med implementeringen av användningsexemplet kommer du att använda de Real-Time CDP-funktioner och gränssnittselement som listas i början av det här dokumentet. Se till att du har de nödvändiga attributbaserade behörigheterna för åtkomstkontroll i alla dessa områden, eller be systemadministratören att ge dig de behörigheter som krävs.

### Skapa en schemadesign och ange fältgrupper

Experience Data Model-resurser (XDM) hanteras i [!UICONTROL Schemas] i Adobe Experience Platform. Du kan visa och utforska kärnresurser från Adobe och skapa anpassade resurser och scheman för din organisation.

Mer information om att skapa scheman finns i [skapa schemakurs.](/help/xdm/tutorials/create-schema-ui.md)

Det finns fyra schemadesigner som används för återengagemangsresan. Varje schema kräver att specifika fält ställs in och vissa fält som är starkt rekommenderade.

#### Kundattributschema

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
| `endUserIDs._experience.mcid.authenticatedState` | Obligatoriskt | Autentiserat tillstånd för Adobe Marketing Cloud ID (MCID). MCID kallas nu Experience Cloud-ID (ECID). |
| `endUserIDs._experience.mcid.id` | Obligatoriskt | Adobe Marketing Cloud ID (MCID). MCID kallas nu Experience Cloud-ID (ECID). |
| `endUserIDs._experience.mcid.namespace.code` | Obligatoriskt | Adobe Marketing Cloud ID-namnområdeskod (MCID). |

+++

+++klassvärde (fältgrupp)

| Fält | Krav |
| --- | --- |
| `eventType` | Obligatoriskt |
| `timestamp` | Obligatoriskt |

+++

+++Extern källsystemsgranskningsinformation (fältgrupp)

Granskningsattribut för externt källsystem är en XDM-datatyp (Experience Data Model) som samlar in granskningsinformation om ett externt källsystem.

+++

#### Schema för offlinetransaktioner för kund

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

+++klassvärde (fältgrupp)

| Fält | Krav |
| --- | --- |
| `eventType` | Obligatoriskt |
| `timestamp` | Obligatoriskt |

+++

+++Extern källsystemsgranskningsinformation (fältgrupp)

Granskningsattribut för externt källsystem är en XDM-datatyp (Experience Data Model) som samlar in granskningsinformation om ett externt källsystem.

+++

#### Adobe webbanslutningsschema

Adobe webbanslutningsschema representeras av en [!UICONTROL XDM ExperienceEvent] -klass, som innehåller följande fältgrupper:

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
| `endUserIDs._experience.mcid.authenticatedState` | Obligatoriskt | Autentiserat tillstånd för Adobe Marketing Cloud ID (MCID). MCID kallas nu Experience Cloud-ID (ECID). |
| `endUserIDs._experience.mcid.id` | Obligatoriskt | Adobe Marketing Cloud ID (MCID). MCID kallas nu Experience Cloud-ID (ECID). |
| `endUserIDs._experience.mcid.namespace.code` | Obligatoriskt | Adobe Marketing Cloud ID-namnområdeskod (MCID). |

+++

+++klassvärde (fältgrupp)

| Fält | Krav |
| --- | --- |
| `eventType` | Obligatoriskt |
| `timestamp` | Obligatoriskt |

+++

+++Extern källsystemsgranskningsinformation (fältgrupp)

Granskningsattribut för externt källsystem är en XDM-datatyp (Experience Data Model) som samlar in granskningsinformation om ett externt källsystem.

+++

### Skapa en datauppsättning från ett schema

En datauppsättning är en lagrings- och hanteringsstruktur för en grupp data, ofta en tabell med fält (rader) och ett schema (kolumner). Alla scheman för intelligenta återengagemangsresor har en enda datauppsättning.

Mer information om hur du skapar en datauppsättning från ett schema finns i [Användargränssnittshandbok för datauppsättningar](/help/catalog/datasets/user-guide.md).

>[!NOTE]
>
>På samma sätt som när du skapar ett schema måste du aktivera datauppsättningen som ska inkluderas i kundprofilen i realtid. Mer information om hur du aktiverar datauppsättningen för användning i kundprofilen i realtid finns i [skapa schemakurs.](/help/xdm/tutorials/create-schema-ui.md#profile).

### Integritet, samtycke och datahantering

#### Samtyckesprinciper

>[!IMPORTANT]
>
>Att ge kunderna möjlighet att säga upp prenumerationen på information från ett varumärke är ett juridiskt krav, liksom att se till att detta val respekteras. Läs mer om gällande lagstiftning i [Experience Platform dokumentation](https://experienceleague.adobe.com/docs/experience-platform/privacy/regulations/overview.html).

När du skapar en väg för återengagemang måste följande policyer för medgivande beaktas och användas:

* If `consents.marketing.email.val = "Y"` kan e-posta
* If `consents.marketing.sms.val = "Y"` kan SMS
* If `consents.marketing.push.val = "Y"` sedan Can Push
* If `consents.share.val = "Y"` så kan annonsera
* Behovet definierat av kundimplementeringen

#### DULE-etikett och tvång

Personliga e-postadresser används som direkt identifierbara data som används för att identifiera eller komma i kontakt med en viss individ i stället för en enhet.

* `personalEmail.address = I1`

#### Marknadspolicyer

Det finns inga ytterligare marknadsföringspolicyer som krävs för återengagemangsresor, men följande bör beaktas efter behov:

* Begränsa känsliga data
* Begränsa annonsering på plats
* Begränsa e-postmålning
* Begränsa mål för flera webbplatser
* Begränsa kombinationen av direkt identifierbara data med anonyma data

### Skapa en målgrupp

#### Målgruppsskapande för varumärkesåterengagemangsresor

Återengagemangsresorna använder målgrupper för att definiera specifika attribut eller beteenden som delas av en deluppsättning profiler från din profilbutik för att skilja en marknadsföringsbar grupp av människor från er kundbas. Målgrupper kan skapas på två olika sätt i Adobe Experience Platform - antingen direkt sammansatta som målgrupper eller med plattformsbaserade segmentdefinitioner.

Mer information om hur du skapar målgrupper direkt finns i [Användargränssnittsguide för målgruppskomposition](/help/segmentation/ui/audience-composition.md).

Mer information om hur du bygger målgrupper med hjälp av plattformsbaserade segmentdefinitioner finns i [Användargränssnittshandbok för Audience Builder](/help/segmentation/ui/segment-builder.md).

>[!BEGINTABS]

>[!TAB Engagement Journey på nytt]

Följande händelser används för återengagemangsresan där användarna tittade på produkter online och inte lade till i kundvagnen under de kommande 24 timmarna, följt av inget varumärkesengagemang under de kommande 3 dagarna.

Följande fält och villkor krävs när du konfigurerar den här målgruppen:

* `EventType: commerce.productViews`
   * `Timestamp: <= 24 hours before now`
* `EventType is not: commerce.productListAdds`
   * `Timestamp: <= 24 hours before now, GAP(>= 3 days)`
* `EventType: application.launch or web.webpagedetails.pageViews or commerce.purchases`
   * `Timestamp: <= 2 days before now`

Beskrivningen för återengagemangsresan visas som:

`Include audience who have at least 1 EventType = ProductViews event THEN have at least 1 Any event where (EventType does not equal commerce.productListAdds) and occurs in last 24 hour(s) then after 3 days do not have any Any event where (EventType = application.launch or web.webpagedetails.pageViews or commerce.purchases) and occurs in last 2 day(s).`

>[!TAB Övergiven Cart Journey]

Följande händelser används för den övergivna kundvagnsresan där användarna lade till en produkt i kundvagnen, men inte slutförde köpet eller rensade kundvagnen de senaste 24 timmarna.

Följande fält och villkor krävs när du konfigurerar den här målgruppen:

* `EventType: commerce.productListAdds`
   * `Timestamp: >= 30 minutes before now and <= 1440 minutes before now`
* `EventType: commerce.purchases`
   * `Timestamp: <= 30 minutes before now`
* `EventType: commerce.productListRemovals`
   * `Timestamp: <= 30 minutes before now`

Beskrivningen för den övergivna kundvagnsresan visas som:

`Include EventType = commerce.productListAdds between 30 min and 1440 minutes before now. exclude EventType = commerce.purchases 30 minutes before now OR EventType = commerce.productListRemovals AND Cart ID equals Product List Adds1 Cart ID (the inclusion event).`

>[!ENDTABS]

### Resekonfiguration i Adobe Journey Optimizer

>[!NOTE]
>
>Adobe Journey Optimizer omfattar inte allt som visas i diagrammen högst upp på den här sidan. Alla annonser för betalda medier skapas i [!UICONTROL Destinations].

Adobe Journey Optimizer hjälper er att leverera sammankopplade, kontextuella och personaliserade upplevelser till era kunder. Kundresan är hela processen för en kunds interaktioner med varumärket. Varje användningsfallsresa kräver specifik information. Nedan finns de exakta data som behövs för varje resegren.

>[!BEGINTABS]

>[!TAB Engagement Journey på nytt]

+++Händelser

* Produktvisningar
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

* Lägg i kundvagnen
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

* Varumärkesengagemang
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
      * Schema: Kundoffline-transaktioner v.1
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

+++Händelser

* Lägg i kundvagnen
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

* Onlineköp
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

* Varumärkesengagemang
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
   * Schema: Kundoffline-transaktioner v.1
   * `eventType = commerce.purchases`
   * `timestamp > timestamp of cart was last abandoned`

* Villkor: vagnen har rensats sedan vagnen senast övergavs:
   * Schema: Customer Digital Transactions v.1
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

+++Händelser

* Onlineköp
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

Mer information om hur du skapar resor i [Adobe Journey Optimizer], läsa [Kom igång med reseguiden](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/journey.html).

### Konfigurera annonser för betalda medier i destinationer

Målramverket används för annonser i betalda medier. När samtycke har checkats ut skickas det till de olika konfigurerade destinationerna. Till exempel direktreklam, e-post, push och SMS.

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

* Fil/schemalagd var tredje timme
   * [E-postmarknadsföring](/help/destinations/catalog/email-marketing/overview.md)
