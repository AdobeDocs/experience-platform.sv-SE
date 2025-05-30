---
title: Utveckla kundvärdet en gång till livstidsvärdet
description: Lär dig hur du skapar personaliserade kampanjer för att erbjuda de bästa kompletterande produkterna eller tjänsterna baserat på en viss kunds attribut, beteende och tidigare köp.
feature: Use Cases
exl-id: 45f72b5e-a63b-44ac-a186-28bac9cdd442
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '3156'
ht-degree: 0%

---

# Utveckla kundvärdet en gång till livstidsvärdet

>[!IMPORTANT]
> 
>* På den här sidan visas ett exempel på hur Real-Time CDP och Adobe Journey Optimizer implementeras för att uppnå det beskrivna användningsfallet. Använd sifferdata, kvalificeringskriterier och andra fält som anges på sidan som en vägledning, inte som prediktiva siffror.
>* Du måste ha licens för Real-Time CDP och Adobe Journey Optimizer för att kunna använda produkten. Läs mer i avsnittet [Krav och planering](#prerequisites-and-planning) längre fram.

Implementera engångskundens värde för livstidsanvändning för att öka varumärkesengagemang och varumärkeslojalitet. Bygg en uppkopplad kundupplevelse i flera kanaler eller på en resa med hjälp av kraften i Experience Platform, som utökas av [Real-Time CDP](/help/rtcdp/home.md) och [Journey Optimizer](https://experienceleague.adobe.com/sv/docs/journey-optimizer/using/ajo-home).

Personerna som ni riktar in er på är de ovanliga besökarna av era egendomar som har gjort några inköp de senaste tre månaderna.

Överväg de kunder som besöker era lokaler och sporadiskt köper de produkter eller tjänster ni erbjuder. Ni kanske vill skapa personaliserade kampanjer som tilltalar dessa kunder så att ert varumärke kan erbjuda dem långsiktigt värde istället för engångsvärde. Lär dig mer om:

* Samla in och hantera data
* Skapa målgrupper
* Skapa resor för att inrikta er på dessa målgrupper i Adobe Journey Optimizer och aktivera dem i Real-Time CDP.

![Steg för steg Utveckla engångsvärde till livstidsvärde - översikt på hög nivå.](../evolve-one-time-value-lifetime-value/images/diagram-business-use-case.png){zoomable="yes"}

## Förutsättningar och planering {#prerequisites-and-planning}

Med tanke på att ni internt har definierat ett affärsmål och mål att öka varumärkeslojaliteten. Detta kan leda till att man implementerar ett användningsexempel som kan öka kundengagemanget och lojaliteten.

För att uppnå detta består den teknik som krävs av de två Experience Platform-programmen [Real-Time CDP](https://experienceleague.adobe.com/docs/experience-platform/rtcdp/overview.html?lang=sv) och [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/get-started/get-started.html?lang=sv-SE). Nedan visas olika funktioner och gränssnittselement från de två programmen som du använder när du implementerar användningsexemplet.

>[!TIP]
>
>Kontrollera att du har de [attributbaserade åtkomstkontrollsbehörigheterna](/help/access-control/abac/end-to-end-guide.md) som krävs för alla dessa områden, eller be systemadministratören att ge dig de behörigheter som krävs.

* [[!DNL Adobe Real-Time Customer Data Platform (Real-Time CDP)]](https://experienceleague.adobe.com/docs/platform-learn/tutorials/rtcdp/understanding-the-real-time-customer-data-platform.html?lang=sv-SE): Integrera data mellan datakällor för att driva kampanjen. Dessa data används sedan för att skapa kampanjmålgrupper och ta fram personaliserade dataelement som används i e-postmeddelanden och webbkampanjpaneler (till exempel namn eller kontorelaterad information). Slutligen används Real-Time CDP även för att aktivera målgrupper för betalda mediematerial.
   * [Scheman](/help/xdm/home.md)
   * [Profiler](/help/profile/home.md)
   * [Datauppsättningar](/help/catalog/datasets/overview.md)
   * [Målgrupper](/help/segmentation/home.md)
   * [Mål](/help/destinations/home.md)
* [[!DNL Adobe Journey Optimizer]](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/journey.html?lang=sv-SE): Designa resor, konfigurera utlösare och skapa rätt meddelanden för att adressera besökarna.
   * [Händelse- eller målutlösare](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioning/collect-event-data/data-collection.html?lang=sv-SE)
   * [Publiker och händelser](https://experienceleague.adobe.com/docs/journey-optimizer/using/audiences-profiles-identities/audiences/about-audiences.html?lang=sv-SE)
   * [Resor](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/journey.html?lang=sv-SE)

## Real-Time CDP och Journey Optimizer

Nedan finns en avancerad arkitekturvy över de olika komponenterna i Real-Time CDP och Journey Optimizer. I det här diagrammet visas hur data flödar genom de två Experience Platform-apparna från datainsamling fram till den punkt där de aktiveras via resor eller kampanjer till destinationer för att uppnå det användningsfall som beskrivs på den här sidan.

![Arkitektur - översikt på hög nivå.](/help/rtcdp/use-case-guides/evolve-one-time-value-lifetime-value/images/architecture-diagram.png){zoomable="yes"}

## Så här uppnår du användningsfallet: översikt på hög nivå {#achieve-the-use-case-high-level}

Nedan finns en översikt över arbetsflödet, en kombination av ett arbetsflöde för resan och ett aktiveringsarbetsflöde.

I det exempelarbetsflöde som visas nedan söker du efter kunder som uppfyller vissa villkor och vill locka dem att återvända till din webbplats eller app. Du vill placera dem på en resa där de återkommer mer återkommande i stället för med begränsad aktivitet på din egendom. Du försöker få tillbaka dem till din egendom och när de väl är tillbaka får du dem att gå in på resan för att göra återkommande köp på din webbplats. Kampanjen som läggs upp här är begränsad till ett kundengagemang per månad.

Börja med att skicka ett budskap till er målgrupp med högvärderade och lågfrekventa kunder. Du kontrollerar sedan om de fått det här meddelandet inom de senaste trettio dagarna. Om de inte har det kan du registrera dem på en resa om t.ex. ett nytt prenumerationsprogram. Du kan sedan vänta i några dagar (sju dagar i det här exemplet). Om de inte har köpt den prenumeration som du har skickat meddelanden till dem kan du sedan leverera betalmediereklam via destinationer. Om de har köpt prenumerationen kan du låta dem ange en orderbekräftelseresa och därmed slutföra användningsärendet.

>[!IMPORTANT]
>
>Som beskrivs vidare på den här sidan, genom att ha en [dedikerad fältgrupp för samtycke i ditt schema](#customer-attributes-schema) och genom [att implementera policyer för samtycke](#privacy-consent), implementeras alla åtgärder och arbetsflöden på ett sekretesssäkert och medgivande först.

>[!BEGINSHADEBOX]

![Steg för steg Utveckla engångsvärde till livstidsvärde - översikt på hög nivå.](../evolve-one-time-value-lifetime-value/images/step-by-step.png){zoomable="yes"}

1. Du skapar scheman och datauppsättningar och markerar dem sedan för [!UICONTROL Profile].
2. Data samlas in och integreras i Experience Platform via Web SDK, Mobile Edge SDK eller API. Analytics Data Connector kan också användas, men kan resultera i fördröjning för resan.
3. Ni läser in profiler i Real-Time CDP och bygger styrningspolicyer för att säkerställa ansvarsfull användning.
4. Ni bygger fokuserade målgrupper från listan med profiler för att hitta kunder med högt värde och låg frekvens.
5. Du skapar två resor i [!DNL Adobe Journey Optimizer], en för att meddela användarna om ett nytt prenumerationsprogram och en annan för att meddela dem att de vill bekräfta köpet senare.
6. Om du vill kan du aktivera kunder som inte har köpt din prenumeration till önskade betalmediematerial.

>[!ENDSHADEBOX]

## Hur man uppnår användningsfallet {#achieve-use-case-instruction}

Om du vill slutföra varje steg i översikten ovan läser du igenom avsnitten nedan som innehåller länkar till mer information och mer detaljerade anvisningar.

### Gränssnittsfunktioner och -element som du använder {#ui-functionality-and-elements}

När du är klar med implementeringen av användningsexemplet använder du de Real-Time CDP-, Adobe Journey Optimizer- och gränssnittselement som listas i början av det här dokumentet. Se till att du har de nödvändiga attributbaserade behörigheterna för åtkomstkontroll i alla dessa områden, eller be systemadministratören att ge dig de behörigheter som krävs.

### Skapa en schemadesign och ange fältgrupper {#schema-design}

Experience Data Model-resurser (XDM) hanteras på arbetsytan [!UICONTROL Schemas] i [!DNL Adobe Experience Platform]. Du kan visa och utforska kärnresurser som tillhandahålls av [!DNL Adobe] (till exempel [!UICONTROL field groups]) och skapa anpassade resurser och scheman för din organisation.

Mer information om hur du skapar [scheman](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=sv) finns i självstudiekursen [Skapa schema.](/help/xdm/tutorials/create-schema-ui.md)

Det finns flera schemadesigner som du kan använda i den här exempelimplementeringen för användningsfallet för att ändra ett enstaka värde till ett livstidsvärde. Varje schema innehåller specifika obligatoriska fält som ska ställas in och vissa fält som föreslås.

Baserat på exempelimplementeringar föreslår Adobe att du skapar följande tre scheman för att uppnå detta användningsfall:

* [Kundattributschema](#customer-attributes-schema) (ett profilschema)
* [Kundens schema för digitala transaktioner](#customer-digital-transactions-schema) (ett upplevelsehändelseschema)
* [Kundens offlinetransaktionsschema](#customer-offline-transactions-schema) (ett upplevelsehändelseschema)

#### Kundattributschema {#customer-attributes-schema}

Använd det här schemat för att strukturera och referera till profildata som utgör kundinformationen. Dessa data hämtas vanligtvis in till [!DNL Adobe Experience Platform] via ditt CRM-system eller liknande system och är nödvändiga för att referera till kundinformation som används för personalisering, marknadsföringssamtycke och förbättrade segmenteringsfunktioner.

![Kundattributschema med fältgrupper markerade](/help/rtcdp/use-case-guides/evolve-one-time-value-lifetime-value/images/customer-attributes-schema.png)

Kundattributschemat representeras av en [!UICONTROL XDM Individual Profile]-klass, som innehåller följande fältgrupper:

+++Demografisk information (fältgrupp)

[Demografiska detaljer](/help/xdm/field-groups/profile/demographic-details.md) är en standardschemafältgrupp för klassen XDM Individual Profile. Fältgruppen innehåller ett personobjekt på rotnivå, vars underfält beskriver information om en enskild person.

+++

+++Personlig kontaktinformation (fältgrupp)

[Information om personlig kontakt](/help/xdm/field-groups/profile/personal-contact-details.md) är en standardschemafältgrupp för klassen XDM Individual Profile, som beskriver kontaktinformationen för en enskild person.

+++

+++Extern systemgranskningsinformation för Source (fältgrupp)

[Externa granskningsattribut för Source-system](/help/xdm/data-types/external-source-system-audit-attributes.md) är en XDM-datatyp (Standard Experience Data Model) som samlar in granskningsinformation om ett externt källsystem.

+++

+++Grupper för samtycke och inställningsfält (fältgrupp)

[Fältgruppen för innehåll och inställningar](/help/xdm/field-groups/profile/consents.md) innehåller ett enda fält av objekttyp, samtycke, för att hämta information om samtycke och inställningar.

+++

#### Kundens digitala transaktionsschema {#customer-digital-transactions-schema}

Det här schemat används för att strukturera och referera till händelsedata som utgör kundaktiviteten på din webbplats eller på andra associerade digitala plattformar. Dessa data är vanligtvis insamlade i [!DNL Adobe Experience Platform] via [Web SDK](/help/web-sdk/home.md) och är nödvändiga för att referera till olika bläddrings- och konverteringshändelser som används för att utlösa resor, detaljerad kundanalys online och utökade segmenteringsfunktioner.

![Kundens schema för digitala transaktioner med fältgrupper markerat](/help/rtcdp/use-case-guides/evolve-one-time-value-lifetime-value/images/customer-digital-transactions-schema.png)

Kundens digitala transaktionsschema representeras av en [!UICONTROL XDM ExperienceEvent]-klass, som innehåller följande fältgrupper:

+++Adobe Experience Platform Web SDK ExperienceEvent (fältgrupp)

| Fält | Krav |
| --- | --- |
| `device.model` | Föreslagen |
| `environment.browserDetails.userAgent` | Föreslagen |

+++

+++Webbinformation (fältgrupp)

[Webbinformation](/help/xdm/field-groups/event/web-details.md) är en standardschemafältgrupp för klassen XDM ExperienceEvent, som används för att beskriva information om webbinformationshändelser som interaktion, sidinformation och referent.

+++

+++Consumer Experience Event (Field Group)

Den här fältgruppen innehåller olika typer av information om åtgärder, till exempel köp- och surfningshändelser, som användarna utför på din webbegenskap.

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

Fältgruppen [Information om slutanvändar-ID](/help/xdm/field-groups/event/enduserids.md) innehåller olika information om dina användare, till exempel om de är autentiserade på din webbplats vid besök, och information om deras identitet.

+++

+++Extern systemgranskningsinformation för Source (fältgrupp)

Externa granskningsattribut för Source-system är en XDM-datatyp (Experience Data Model) som samlar in granskningsinformation om ett externt källsystem.

+++

#### Schema för offlinetransaktioner för kund {#customer-offline-transactions-schema}

Det här schemat används för att strukturera och referera till händelsedata som utgör kundaktiviteten på plattformar utanför webbplatsen. Dessa data importeras vanligtvis till [!DNL Adobe Experience Platform] från en POS (eller liknande system) och direktuppspelas oftast till Experience Platform via en API-anslutning. Läs om [gruppinmatning](/help/ingestion/batch-ingestion/getting-started.md). Syftet är att hänvisa till olika offlinekonverteringshändelser som används för att utlösa resor, djupgående kundanalyser online och offline samt förbättrade segmenteringsfunktioner.

![Schema för kundoffline-transaktioner med fältgrupper markerade](/help/rtcdp/use-case-guides/evolve-one-time-value-lifetime-value/images/customer-offline-transactions-schema.png)

Kundens offlinetransaktionsschema representeras av en [!UICONTROL XDM ExperienceEvent]-klass, som innehåller följande fältgrupper:

+++Commerce Details (Field Group)

[Commerce Details](/help/xdm/field-groups/event/commerce-details.md) är en standardschemafältgrupp för klassen [!DNL XDM ExperienceEvent] som används för att beskriva handelsdata, t.ex. produktinformation (SKU, namn, kvantitet) och standardkundvagnsåtgärder (beställning, utcheckning, överlåtelse).

+++

+++Personlig kontaktinformation (fältgrupp)

[[!UICONTROL Personal Contact Details]](/help/xdm/field-groups/profile/personal-contact-details.md) är en standardschemafältgrupp för klassen [!DNL XDM Individual Profile] som beskriver kontaktinformationen för en enskild person.

+++

+++Extern systemgranskningsinformation för Source (fältgrupp)

Externa granskningsattribut för Source-system är en XDM-datatyp (Experience Data Model) som samlar in granskningsinformation om ett externt källsystem.

+++

#### Adobe webbanslutningsschema {#adobe-web-connector-schema}

>[!NOTE]
>
>Detta är en valfri implementering om du använder [!DNL Adobe Analytics Data Connector].

Det här schemat används för att strukturera och referera till händelsedata som utgör kundaktiviteten på din webbplats eller på andra associerade digitala plattformar. Det här schemat liknar kundens schema för digitala transaktioner, men skiljer sig åt på så sätt när Web SDK inte är ett alternativ för datainsamling. Därför kan du använda det här schemat när du använder [!DNL Adobe Analytics Data Connector] för att skicka dina onlinedata till [!DNL Adobe Experience Platform], antingen som ett primärt eller sekundärt datastream.

![Adobe webbanslutningsschema med fältgrupper markerade](/help/rtcdp/use-case-guides/evolve-one-time-value-lifetime-value/images/adobe-web-schema.png)

Webbanslutningsschemat [!DNL Adobe] representeras av en [!UICONTROL XDM ExperienceEvent]-klass, som innehåller följande fältgrupper:

+++Adobe Analytics ExperienceEvent-mall (fältgrupp)

[[!UICONTROL Adobe Analytics ExperienceEvent Full Extension]](/help/xdm/field-groups/event/analytics-full-extension.md) är en standardschemafältgrupp som samlar in vanliga mätvärden som samlas in av Adobe Analytics.

+++

### Skapa en datauppsättning från ett schema {#dataset-from-schema}

En datauppsättning är en lagrings- och hanteringsstruktur för en grupp med data. Varje schema som används för att slutföra den här exempelimplementeringen har en enda datamängd.

Mer information om hur du skapar en [datauppsättning](/help/catalog/datasets/overview.md) från ett schema finns i [gränssnittshandboken för datauppsättningar](/help/catalog/datasets/user-guide.md).

>[!NOTE]
>
>På samma sätt som när du skapar ett schema måste du aktivera datauppsättningen som ska inkluderas i kundprofilen i realtid. Mer information om hur du aktiverar datauppsättningen för användning i kundprofilen i realtid finns i självstudiekursen [Skapa schema.](/help/xdm/tutorials/create-schema-ui.md#profile).

### Integritet, samtycke och datahantering {#privacy-consent}

#### Samtyckesprinciper

>[!IMPORTANT]
>
>Ett juridiskt krav är att ge kunderna möjlighet att säga upp prenumerationen på information från ett varumärke och att se till att detta val respekteras. Läs mer om gällande lagstiftning i [Översikt över sekretesslagstiftning](https://experienceleague.adobe.com/docs/experience-platform/privacy/regulations/overview.html?lang=sv-SE).

Överväg att implementera följande [medgivandeprinciper](https://experienceleague.adobe.com/docs/platform-learn/data-collection/web-sdk/consent/overview.html?lang=sv-SE) och be dina besökare om samtycke innan du kontaktar dem:

* Om `consents.marketing.email.val = "Y"` kan du skicka e-post
* Om `consents.marketing.sms.val = "Y"` så kan SMS
* Om `consents.marketing.push.val = "Y"` kan du trycka
* Om `consents.share.val = "Y"` kan annonsera

#### Etikett och verkställighet för datastyrning

Överväg att lägga till och framtvinga följande [etiketter för datastyrning](/help/data-governance/labels/overview.md):

* Personliga e-postadresser används som direkt identifierbara data som används för att identifiera eller komma i kontakt med en viss individ i stället för en enhet.
   * `personalEmail.address = I1`

#### Marknadspolicyer

Det finns inga [marknadsföringspolicyer](/help/data-governance/policies/overview.md) som krävs för de resor som du skapar som en del av det här användningsärendet. Du kan dock överväga följande profiler:

* Begränsa känsliga data
* Begränsa Advertising på plats
* Begränsa e-postmålning
* Begränsa målgruppsanpassning mellan webbplatser
* Begränsa kombinationen av direkt identifierbara data med anonyma data

### Skapa målgrupper {#create-audiences}

Det här användningsexemplet kräver att du skapar två målgrupper för att definiera specifika attribut eller beteenden som delas av en deluppsättning profiler från din profilbutik för att särskilja en marknadsföringsbar grupp av personer. Målgrupper kan skapas på flera sätt i Adobe Experience Platform:

* Mer information om hur du skapar en målgrupp finns i [Användargränssnittsguiden för målgruppstjänsten](https://experienceleague.adobe.com/docs/experience-platform/segmentation/ui/overview.html?lang=sv-SE#create-audience).
* Mer information om hur du komponerar [målgrupper](/help/segmentation/home.md) finns i [Användargränssnittsguiden för målgruppsdisposition](/help/segmentation/ui/audience-composition.md).
* Mer information om hur du skapar målgrupper med hjälp av Experience Platform-härledda segmentdefinitioner finns i [Användargränssnittshandboken för Audience Builder](/help/segmentation/ui/segment-builder.md).

Du måste skapa och använda två målgrupper i olika steg av användningsfallet, vilket visas i bilden nedan.

![Målgrupper markerade.](/help/rtcdp/use-case-guides/evolve-one-time-value-lifetime-value/images/audiences-highlighted-in-diagram.png){zoomable="yes"}

>[!BEGINTABS]

>[!TAB Adobe Journey Optimizer kvalificerar målgrupp]

Den här värdefulla och lågfrekventa publiken innehåller de profiler som du vill nå ut till via en resa för att informera dem om ett nytt prenumerationsprogram. Publiken finns nedan:

* Beskrivning: Profiler som har spenderat mer än $250 totalt de senaste tre månaderna
* Fält och villkor som behövs i målgruppen:
   * Händelse: `commerce.order.payments.paymentamount`
* Sammanställd summa: >= $250
   * EventType: `commerce.purchases`
* Tidsstämpel: mindre än 3 månader tidigare


>[!TAB Betalad mediepublik]

Den här målgruppen har skapats för att inkludera profiler som har spenderat mer än 250 USD totalt de senaste tre månaderna och som inte har köpt något under de senaste 7 dagarna. Publiken finns nedan:

* Beskrivning: profiler som har spenderat mer än 250 USD totalt de senaste tre månaderna och som inte har köpt något under de senaste sju dagarna.
* Fält och villkor som krävs:
   * EventType: `journey.feedback`
      * Operand: = true
   * Händelse: `experience.journeyOrchestration.stepEvents.nodeName`
      * Operand: = JourneyStepEventTracker - prenumerationen har inte köpts
      * Tidsstämpel: under de senaste 7 dagarna
   * EventType är inte: `commerce.purchases`
      * Tidsstämpel: &lt;= 7 dagar före nu
   * Händelse: SKU
      * Värde: = `subscription`

>[!ENDTABS]

### Resekonfiguration i Adobe Journey Optimizer {#journey-setup}

>[!NOTE]
>
>[!DNL Adobe Journey Optimizer] omfattar inte allt som visas i diagrammen. Alla [betalda mediaannonser](/help/destinations/catalog/social/overview.md) skapas i [!UICONTROL destinations] [arbetsytan](/help/destinations/ui/destinations-workspace.md).

[[!DNL Adobe Journey Optimizer]](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/journey.html?lang=sv-SE) hjälper dig att leverera sammankopplade, kontextuella och personaliserade upplevelser till dina kunder. Kundresan är hela processen för en kunds interaktioner med varumärket. Varje användningsfallsresa kräver specifik information.

För att uppnå detta måste du skapa två separata resor:

* Livslängdsresan, som innehåller det budskap du skickar till dina värdefulla lågfrekventa kunder
* Beställningsbekräftelseresan för användare som svarar på ditt samtal och köper en prenumeration.

![Resor är markerade.](/help/rtcdp/use-case-guides/evolve-one-time-value-lifetime-value/images/journeys-highlighted-in-diagram.png){zoomable="yes"}

Nedan finns de exakta data som behövs för varje resegren.

>[!BEGINTABS]

>[!TAB Livstidsresa]

Livslängden riktar sig till kunder med högt värde och låg frekvens som inte var målinriktade de senaste 30 dagarna. Ett meddelande visas för dessa kunder och om de fortfarande inte köper något efter 7 dagar kan ni inkludera de icke-köpare i en publik som ni kan visa betalda mediereklam för. Om de faktiskt köper kan du ställa in köparna på en orderbekräftelseresa, som anges på den separata fliken.

![Livstidsresan ger en överblick på hög nivå.](/help/rtcdp/use-case-guides/evolve-one-time-value-lifetime-value/images/lifetime-journey.png "Etttidsvärde till heltidsresans visuella översikt på hög nivå."){zoomable="yes"}

+++Detaljerad reselogik

Den resa som visas ovan följer följande logik.

1. Läser målgrupp: Använd en [läsmålgruppsaktivitet](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/read-audience.html?lang=sv-SE) för den första målgruppen som skapas i målgruppsavsnittet ovan.

2. Villkor - föredragen kanal: Använd en [villkorsaktivitet](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/condition-activity.html?lang=sv-SE) för att avgöra hur du ska nå ut till kunder, oavsett om det är via e-post, SMS eller push-meddelanden. Använd tre åtgärdsaktiviteter för att skapa de tre grenarna.

3. Vänta: Använd en [vänteaktivitet](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/read-audience.html?lang=sv-SE) för att vänta tills du lyssnar efter köp.

4. Villkor - Inköpt prenumeration under de senaste 7 dagarna?: Använd en villkorsaktivitet för att lyssna efter produktköp under de senaste sju dagarna.

5. JourneyStepEventTracker - Prenumerationen har inte köpts: Använd en [anpassad åtgärd](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/using-custom-actions.html?lang=sv-SE) för besökare som ännu inte har köpt din prenumeration, trots att du fått ditt meddelande. Som en del av det anpassade villkoret i slutet av resan skapar du en `journey.feedback`-händelse och lägger till den i en datauppsättning baserat på [!UICONTROL Journey Step Event]-schemat. Du kommer att använda den här händelsen för att segmentera den målgrupp som inte har köpt prenumerationen och som du kan rikta in dig på via betalda mediereklam.

+++

>[!TAB Bekräftelseresa för beställning]

Beställningsbekräftelseresan fokuserar på om ett köp gjordes via webbplatsen eller mobilappen. När en kund har slutfört köpet av t.ex. en prenumeration hos ditt företag, kan du ställa in dem på en orderbekräftelseresa.

![Kundorderbekräftelseresan ger en överblick på hög nivå.](/help/rtcdp/use-case-guides/evolve-one-time-value-lifetime-value/images/order-confirmation-journey.png "Kundorderbekräftelseresan ger en överblick på hög nivå."){zoomable="yes"}

+++Reselogik

Använd de föreslagna händelserna, fälten och åtgärderna nedan i bekräftelseresan:

* Resan utlöses av en online-köphändelse
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
   * Välj Målkanal (du kan markera en eller flera kanaler för större räckvidd).
      * Orderbekräftelsen anses vara till sin natur, så det är oftast inte nödvändigt att kontrollera samtycke.
      * E-post
      * Push
      * SMS

   * Channel Content Personalization
      * Visa information om orderdetaljer och kan visa en lista med produkter i ett tabellformat.

+++

>[!ENDTABS]

Mer information om hur du skapar resor i [!DNL Adobe Journey Optimizer] finns i guiden [kom igång med resor](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/journey.html?lang=sv-SE).

### Ställ in ett mål för att visa annonser för betalda media {#paid-media-ads}

Vissa användare kanske inte har köpt din prenumeration ens efter att du har meddelat dem om det nya programmet. Efter att ha väntat i ett antal dagar (sju i det här exemplet) kan du bestämma dig för att visa betalda mediaannonser för dessa användare, för att uppmuntra dem att köpa din prenumeration.

Använd målgruppsramverket i Real-Time CDP för annonser i betalda medier. Välj ett av många tillgängliga annonsdestinationer för att visa betalmediaannonser för dina kunder och aktivera den betalande mediepubliken som du [skapade tidigare](#create-audiences) till ett valfritt mål. Visa en översikt över tillgängliga [annonser](/help/destinations/catalog/advertising/overview.md) och [sociala ](/help/destinations/catalog/social/overview.md) mål.

Läs dokumentationen nedan om du vill lära dig hur du aktiverar data till mål (till exempel [Trade Desk](/help/destinations/catalog/advertising/tradedesk.md) eller [Google Customer Match](/help/destinations/catalog/advertising/google-customer-match.md)):

* [Skapa en ny målanslutning](/help/destinations/ui/connect-destination.md)
* [Aktivera målgruppsdata för direktuppspelad målgruppsexport](/help/destinations/ui/activate-segment-streaming-destinations.md)

## Nästa steg {#next-steps}

Genom att ställa in era lågfrekventa och värdefulla användare på en resa och visa betalda mediereklam för en delmängd av dem har ni förhoppningsvis vänt några av dem från engångsavgift till livstidsvärdefulla kunder, vilket förbättrar er varumärkeslojalitet och kundinteraktionsstatistik.

Därefter kan du utforska andra användningsfall som stöds av Real-Time CDP, till exempel [intelligent återengagerande kunder](/help/rtcdp/use-case-guides/intelligent-re-engagement/intelligent-re-engagement.md) eller [visa personaliserat innehåll för oautentiserade användare](/help/rtcdp/partner-data/onsite-personalization.md) på dina webbegenskaper.
