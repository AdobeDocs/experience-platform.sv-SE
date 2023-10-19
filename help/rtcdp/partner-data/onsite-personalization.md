---
title: Använd partnerstödd besöksidentifiering för att personalisera upplevelser på plats
description: Lär dig hur du använder partnerstödd igenkänning av besökare för att leverera personaliserade upplevelser på plats för besökarna.
exl-id: 99677988-1df8-47b1-96b1-0ef6db818a1d
source-git-commit: de8aeb553066405424711e75480204f6136b52ff
workflow-type: tm+mt
source-wordcount: '2472'
ht-degree: 1%

---

# Använd partnerstödd igenkänning av besökare för att personalisera upplevelser på plats

>[!AVAILABILITY]
>
>Den här funktionen är tillgänglig för kunder som har licens för Real-Time CDP (App Service), Adobe Experience Platform Activation, Real-Time CDP, Real-Time CDP Prime, Real-Time CDP Ultimate. Läs mer om dessa paket i [produktbeskrivningar](https://helpx.adobe.com/legal/product-descriptions.html) och kontakta Adobe för mer information.

Lär dig hur du kan använda partnerstödd igenkänning för att leverera personaliserade upplevelser till besökare på era webbegenskaper. Använd den här självstudiekursen för att förstå implementeringssekvensen för olika element i Experience Platform och andra Experience Cloud-lösningar för att visa en personaliserad upplevelse för autentiserade och oautentiserade besökare.

![En infografik som beskriver hur ni använder attribut som tillhandahålls av partners för att leverera personaliserade upplevelser till era besökare.](/help/rtcdp/assets/partner-data/onsite-personalization/onsite-personalization-steps.png)

## Branschexempel {#industry-example}

Som ett exempel kan nämnas ett heminredningsvarumärke som har låg autentiseringsfrekvens. Det här varumärket vill leverera personaliserade upplevelser till förstagångsbesökare, utan tidigare historik eller autentisering, och utan att tona ned beroendet av cookies från tredje part.

Detta varumärke väljer att utnyttja teknik för partnerigenkänning för att troligtvis identifiera besökaren och leverera en mer personaliserad upplevelse. Detta hjälper besökaren att komma vidare när marknadsföringstratten närmar sig. Varumärket kan till exempel använda demografiska signaler som tillhandahålls av partners för innehåll på plats som tilltalar personer som nyligen har flyttat och erbjuder en rabatt på populära DIY-produkter.

## Förutsättningar och planering {#prerequisites-and-planning}

När du planerar att använda attribut som tillhandahålls av partners för att leverera personaliserade upplevelser till autentiserade och oautentiserade besökare bör du tänka på följande under planeringsprocessen:

* Vilka indata förväntas av din partners igenkänningsteknik så att de kan ligga på fler attribut?
* I vilken utsträckning kan ni leverera personalisering i olika kanaler och för olika användningsområden baserat på sannolikhetshärledda attribut, jämfört med bestämningsmässigt bekräftade attribut?
* Hur ska upplevelsen av en förautentiserad men erkänd besökare förändras när de autentiseras?

### UI-funktionalitet, plattformskomponenter och Experience Cloud-produkter som du kommer att använda {#ui-functionality-and-elements}

För att implementera det här användningsexemplet måste du använda flera olika delar av Real-time Customer Data Platform och andra Experience Cloud-lösningar. Se till att du har de nödvändiga [behörigheter för attributbaserad åtkomstkontroll](/help/access-control/abac/overview.md) för alla dessa områden, eller be systemadministratören att ge dig de behörigheter som krävs.

* Datainsamling
   * [Webb-SDK för Adobe Experience Platform](/help/edge/home.md)
   * [Taggar](/help/tags/home.md)
   * [Dataströmmar](/help/datastreams/overview.md)
* Datahantering i Real-Time CDP
   * [Identiteter](/help/identity-service/namespaces.md)
   * [Scheman](/help/xdm/home.md)
   * [Dataanvändningsetiketter](/help/data-governance/labels/overview.md)
   * [Datauppsättningar](/help/catalog/datasets/overview.md)
* Webbegenskapspersonalisering
   * [Kantsegmentering](/help/segmentation/ui/edge-segmentation.md)
   * [Edge Personalization-mål](/help/destinations/destination-types.md#edge-personalization-destinations)
   * [Adobe Target](/help/destinations/catalog/personalization/adobe-target-connection.md) (eller en valfri personaliseringsplattform. Den här självstudiekursen om hur du använder Adobe Target som personaliseringsmotor)

## Videogenomgång {#video-walkthrough}

Se videosjälvstudiekursen nedan för en genomgång av hur ni personaliserar webbplatsupplevelser för okända besökare:

>[!VIDEO](https://video.tv.adobe.com/v/3423076/?learn=on)

## Så här uppnår du användningsfallet: översikt på hög nivå {#achieve-the-use-case-high-level}

![En infografik som beskriver hur ni använder attribut som tillhandahålls av partners för att leverera personaliserade upplevelser till era besökare.](/help/rtcdp/assets/partner-data/onsite-personalization/onsite-personalization-steps.png)

1. Som en **kund** licensierar du från **datapartner** möjlighet att få insikter i realtid om annars anonyma webbplatsbesökare.
2. Som en **kund** distribuerar du klientbibliotek på dina egenskaper för att ringa **partner** API:er och du konfigurerar Web SDK eller Mobile SDK för att skicka signaler från partner till Real-Time CDP.
3. När du surfar på din webbplats eller i din app **besökare** är sannolikhet att identifieras av **partner**, som returnerar attribut tillsammans med ett ID.
4. Real-Time CDP kör kantsegmentering för att utvärdera inkommande händelseträffar och kvarstår som resultat mot [ECID](https://experienceleague.adobe.com/docs/id-service/using/home.html).
5. Adobe Target använder kantsegmentering för att återge upplevelsen **besökare** för personalisering under session.
6. Händelsen bevaras i sin helhet för arbetsflöden längre fram i kedjan, som analys och återmarknadsföring.

## Så här uppnår du användningsfallet: stegvisa instruktioner {#step-by-step-instructions}

Läs igenom avsnitten nedan som innehåller länkar till ytterligare dokumentation för att slutföra varje steg i översikten ovan.

### Datahantering - Skapa ett identitetsnamnutrymme, ett schema och en datauppsättning för att hantera dataattribut {#data-management}

Innan ni kan uppnå användningsexemplet för att personalisera oautentiserade besökares upplevelse, måste ni först skapa datahanteringsstrukturen i Real-Time CDP för att kunna ta emot inkommande data om realtidshändelser och målgruppskvalifikationer.

#### Skapa namnområde för partner-ID

Först måste du skapa ett namnutrymme för en partner-ID-identitet. Navigera till **[!UICONTROL Customer]** > **[!UICONTROL Identities]** i den vänstra listen och välj **[!UICONTROL Create identity namespace]** i skärmens övre högra hörn.

![Dialogrutan Skapa ID-namnområde med partner-ID markerat.](/help/rtcdp/assets/partner-data/onsite-personalization/create-identity-namespace.png)

Läs mer om hur [skapa en namnrymd för partner-ID](/help/rtcdp/partner-data/prospecting.md#create-partner-id-namespace).

#### Skapa ett schema

Skapa sedan en [!UICONTROL Experience Event] schema för att lagra tidsseriedata som du senare kommer att samla in från dina webbegenskaper, och se till att använda [!UICONTROL XDM ExperienceEvent] som basklass för schemat. Läs om hur [skapa ett schema med användargränssnittet i Experience Platform](/help/xdm/ui/resources/schemas.md#create).

![Arbetsytan Scheman med Skapa schema och XDM Experience-händelsen är markerade.](/help/rtcdp/assets/partner-data/onsite-personalization/create-experience-event-schema.png)

När du skapar ditt schema och [lägg till fältgrupper i ditt schema](/help/xdm/ui/resources/schemas.md#add-field-groups)kan du lägga till [Besök webbsidan](/help/xdm/field-groups/event/web-details.md) och [Identitetskarta](/help/xdm/field-groups/profile/identitymap.md) fältgrupper. Detta är utöver andra fältgrupper som är tillämpliga på er digitala egendom och datainsamling.

Dessutom kan du skapa eller återanvända en befintlig fältgrupp och lägga till den i ditt schema för att få partnerinformation om besökaren. Läs om [skapa en fältgrupp](/help/xdm/ui/resources/field-groups.md) och hur [lägg till fält](/help/xdm/ui/resources/field-groups.md) till fältgruppen. Om du till exempel förväntar dig att personalisera mot partnertillhandahållna insikter som åldersintervall, anställningsstatus, månatlig utgiftsstyrka eller köpbeteenden, ska fältgruppen innehålla lämpliga fält.

Om dataparten tillhandahåller en stabil identifierare för besökaren och du vill ta med den till Real-Time CDP måste du se till att ha ett lämpligt namngivet fält för identifieraren i din anpassade fältgrupp. Du bör även markera fältet som en identitet i det identitetsnamnområde som du skapade tidigare. Kom även ihåg att [aktivera schemat som ska inkluderas i profilen](/help/xdm/ui/resources/schemas.md#profile).

#### Skapa en datauppsättning

Därefter måste du skapa en datauppsättning för de tidsseriedata som du samlar in från besökarna på din webbegenskap och som du kommer att använda för personalisering på plats.

Läs självstudiekursen om [hur du skapar en datauppsättning](/help/catalog/datasets/user-guide.md#create) och kom ihåg att välja alternativet att skapa datauppsättningen från ett schema. Skapa datauppsättningen baserat på schemat som du skapade i föregående steg.

På samma sätt som när du skapar ett schema måste du aktivera datauppsättningen som ska inkluderas i [!UICONTROL Real-Time Customer Profile]. Mer information om hur du aktiverar datauppsättningen för användning i [!UICONTROL Real-Time Customer Profile], läsa [skapa schemakurs.](/help/xdm/tutorials/create-schema-ui.md#profile)

### Implementera händelsedatainsamling på din webbegenskap {#implement-data-collection}

När du har konfigurerat datahanteringskonfigurationen måste du nu implementera en realtidshändelse [datainsamling](/help/collection/home.md) på din webbegenskap. Du måste mäta din egendom med Adobe datainsamlingsbiblioteket - [!UICONTROL Web SDK] - för att samla in realtidssamtal och skicka tillbaka dem till Real-Time CDP. Det här objektet består av ett par olika åtgärder för ett fåtal datainsamlingskomponenter.

>[!IMPORTANT]
>
>Om du vill hämta attribut som tillhandahålls av partner måste du också *integrera din webbegenskap med partner-API:er eller andra metoder för att anropa och hämta attribut från datapartners i realtid*. Diskutera den här aspekten med din valfria partner eftersom den inte är underställd kursen.

Använd först programväljaren i skärmens övre högra hörn för att navigera till **[!UICONTROL Data Collection]** -avsnitt.

>[!TIP]
>
>Kontakta systemadministratören och be om åtkomst om du inte kan se [!UICONTROL Data Collection] i programväljaren.

![Appväxlare för att komma till avsnittet Datainsamling.](/help/rtcdp/assets/partner-data/onsite-personalization/app-switcher-data-collection.png)

The **[!UICONTROL Data Collection]** i användargränssnittet ser ut ungefär som bilden nedan.

![Avsnittet Datainsamling i plattformens användargränssnitt.](/help/rtcdp/assets/partner-data/onsite-personalization/data-collection-home.png)

#### Skapa datastream

Som ett första steg i datainsamlingsavsnittet [skapa ett nytt datastream](/help/datastreams/configure.md). Datastream är grunden för hur data samlas in och dirigeras korrekt till rätt Adobe-app, i det här fallet Experience Platform.

När du skapar datastream finns det i **[!UICONTROL Event schema]** markerar du det schema som du skapade tidigare.

![Händelseschemeväljaren markeras när en ny datastream konfigureras.](/help/rtcdp/assets/partner-data/onsite-personalization/event-schema-selector-datastream.png)

[Välj händelsedatamängd](/help/datastreams/configure.md#aep) som du skapade tidigare från listrutan, markerar du rutorna intill **[!UICONTROL Edge Segmentation]** och **[!UICONTROL Personalization Destinations]** och markera **[!UICONTROL Save]**.

Observera att du inte behöver välja någon profildatauppsättning i det här scenariot eftersom du samlar in händelsebaserade tidsseriedata.

#### Skapa taggegenskap

Tänk på en egenskap som en behållare som du fyller med tillägg, regler, dataelement och bibliotek när du distribuerar taggar till webbplatsen.

Navigera till **[!UICONTROL Tags]** och markera **[!UICONTROL New property]**.

![Skapa en ny taggegenskap.](/help/rtcdp/assets/partner-data/onsite-personalization/create-tag-property.png)

Fyll i de obligatoriska fälten och markera **[!UICONTROL Save]**.

![Fyll i obligatoriska fält för den nya egenskapen.](/help/rtcdp/assets/partner-data/onsite-personalization/tag-property-fields.png)

Få fullständig information om hur [skapa en taggegenskap](https://experienceleague.adobe.com/docs/platform-learn/implement-in-websites/configure-tags/create-a-property.html).

Därefter måste du installera olika tillägg i egenskapen. Välj taggegenskap och navigera till [!UICONTROL Extensions] -avsnitt.

![Välj den nya taggegenskapen.](/help/rtcdp/assets/partner-data/onsite-personalization/select-tag-property.png)

Observera att [!UICONTROL Core] tillägget är redan installerat. Du måste installera ytterligare två tillägg, vilket beskrivs i nästa avsnitt.

![Visa installerade tillägg.](/help/rtcdp/assets/partner-data/onsite-personalization/view-existing-extensions.png)

#### Installera SDK-tillägg för webben

Observera att den här självstudiekursen visar hur du kan instrumentera din webbplats med Web SDK. Du kan också använda [Mobile SDK](https://developer.adobe.com/client-sdks/documentation/) i appen för att personalisera upplevelsen för era appbesökare.

![Vy över Web SDK-tillägget i tilläggskatalogen.](/help/rtcdp/assets/partner-data/onsite-personalization/web-sdk-extension.png)

Navigera till **[!UICONTROL Datastreams]** och ange information om sandlådan Experience Platform som du använder. Välj lämplig sandlåda och den datastam som skapades i föregående steg i nästa listruta. Du kan välja samma sandbox- och datastream-värden för alla andra miljöer. Ändra inte de andra inställningarna och välj **[!UICONTROL Save]**.

Få fullständig information om [installera Web SDK](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/tags-configuration/install-web-sdk.html).

#### Installera ID-tjänsttillägg

Använd [Experience Cloud ID-tjänsttillägg](/help/tags/extensions/client/id-service/overview.md) för att skapa en unik enhetsbaserad förstahandsidentitet för besökare i alla Experience Cloud-lösningar. Sök efter **[!UICONTROL ID Service]** i tilläggskatalogen och installera den. Behåll alla standardinställningar när du installerar tillägget.

![Visa ID-tjänsttillägget i tilläggskatalogen.](/help/rtcdp/assets/partner-data/onsite-personalization/id-service-extension.png)

#### Konfigurera miljöer

Gå vidare till **[!UICONTROL Environments]** från den vänstra navigeringen. I det här steget måste du ansluta webbplatsen till Adobe Edge Network för att hämta och leverera besöksinformation i realtid.

Markera ruteikonen till höger för utvecklingsmiljön och kopiera standardversionen av JavaScript-kodfragmentet som visas i ett modalt fönster.

![Markera kryssruteikonen som är markerad i avsnittet Miljö i användargränssnittet för datainsamling.](/help/rtcdp/assets/partner-data/onsite-personalization/select-box-icon.png)

Du måste lägga till det här kodfragmentet högst upp på webbplatsen. På så sätt kommer webbplatsen att anropa Adobe Edge Network för att hämta JavaScript-logik som ska läsas in och köras på sidan. Detta gör att funktioner som generering av besökar-ID, datainsamling och personalisering av realtidsupplevelser kan fungera.

#### Ställ in dataelement

Dataelement är byggstenarna för dataordlistan (eller datamappningen). Ett enskilt dataelement är en variabel vars värde kan mappas till frågesträngar, URL:er, cookie-värden, JavaScript-variabler och så vidare. Läs mer om [dataelement](/help/tags/ui/managing-resources/data-elements.md).

I det här användningsexemplet måste du ställa in två dataelement.

Först konfigurerar du en `partnerData` -element. Navigera till **[!UICONTROL Data Elements]** avsnitt och markera **[!UICONTROL Create New Data Element]**.

![Skapa ett nytt dataelement.](/help/rtcdp/assets/partner-data/onsite-personalization/create-data-element.gif)

Namnge dataelementet `partnerData`lämnar du [!UICONTROL extension] värde som [!UICONTROL Core]och ange **[!UICONTROL Data Element Type]** as **[!UICONTROL JavaScript Variable]**. Retur `partnerData` i fältet **[!UICONTROL JavaScript variable name]** och markera **[!UICONTROL Save]**.

![Markerade markeringar för att konfigurera dataelementet partnerData korrekt.](/help/rtcdp/assets/partner-data/onsite-personalization/create-partnerdata-data-element.png)

Ange det andra dataelementets namn för den nya variabeln `pageVisit`, ange **[!UICONTROL Extension]** till **[!UICONTROL Adobe Experience Platform]** och välja **[!UICONTROL XDM Object]** som datatyp.

![Markerade markeringar för att konfigurera dataelementet pageVisit korrekt.](/help/rtcdp/assets/partner-data/onsite-personalization/page-visit-data-element.png)

I schemat väljer du de tredjepartsattribut som motsvarar de värden som du förväntar dig från dataparten. Markera sedan alternativknappen med namnet **[!UICONTROL Provide entire object]**. Markera ikonen som ser ut som en databas och välj `partnerData` dataelement som du skapade tidigare.

#### Ställ in regler

I **[!UICONTROL Rules]** kan du konfigurera webbplatsen så att den skickar en personaliseringsbegäran till Adobe med de inlästa attributen i de dataelement som du just har skapat. Läs mer om [skapa regler](/help/tags/ui/managing-resources/rules.md).

Välj **[!UICONTROL Create new Rule]**. Namnge den här regeln **[!UICONTROL Personalize]** och välj +-tecknet bredvid **[!UICONTROL Events]**. Välj **[!UICONTROL Page Bottom]** som händelsen och spara.

![Markeringar för händelsetypen i en regel.](/help/rtcdp/assets/partner-data/onsite-personalization/add-events-rule.png)

Markera +-tecknet bredvid **[!UICONTROL Actions]**. Uppdatera tillägget till **[!UICONTROL Adobe Experience Platform Web SDK]** och ange **[!UICONTROL Action Type]** till **[!UICONTROL Send event]**.

![Markeringar för åtgärdstypen i en regel.](/help/rtcdp/assets/partner-data/onsite-personalization/add-action-rule.png)

Från **[!UICONTROL Type]** nedrullningsbar väljare till höger, välj `web.webpagedetails.pageViews` som händelsetyp.

![Välj händelsetyp.](/help/rtcdp/assets/partner-data/onsite-personalization/add-pageview-type-rule.png)

Välj databasikonen bredvid XDM-data och välj `pageVisit` dataelement.

Bläddra nedåt i listan över åtgärdskonfigurationer och se till att markera rutan med namnet **[!UICONTROL Render visual personalization decisions]**. Detta är viktigt för att upplevelser som levereras via Adobe Target eller andra liknande produkter ska kunna återges visuellt på webbsidan. Välj **[!UICONTROL Keep Changes]** och sedan **[!UICONTROL Save]** regeln.

![Markera kryssrutan Återge beslut om visuell personalisering.](/help/rtcdp/assets/partner-data/onsite-personalization/render-visual-personalization-toggle.png)

#### Konfigurera publiceringsarbetsflöde

För att distribuera konfigurationen till webbsidan är nästa steg att skapa ett bibliotek som innehåller de resurser du just skapat. Läs mer om [konfigurera ett publiceringsflöde](/help/tags/ui/publishing/publishing-flow.md).

Välj **[!UICONTROL Publishing Flow]** och sedan **[!UICONTROL Add Library]**.

Välj **[!UICONTROL Add all Changed Resources]**, ger biblioteket ett namn och ställer in miljön på **[!UICONTROL Development]** och markera **[!UICONTROL Save & Build to Development]**.

![Skapa bibliotek och distribuera till utvecklingsmiljö](/help/rtcdp/assets/partner-data/onsite-personalization/create-publishing-workflow.gif)

#### Testa din webbplats

Nu bör webbplatsen vara helt integrerad med Web SDK. Om du vill testa att datainsamlingen fungerar som förväntat kan du navigera till webbplatsen och använda webbläsarens utvecklarverktyg för att inspektera nätverkstrafiken.

Indata `interact` Uppdatera sidan i sökrutan så ser du nätverksanrop från webbplatsen till Adobe Edge-nätverket.

![Vy över nätverkshändelser i utvecklingsverktyg.](/help/rtcdp/assets/partner-data/onsite-personalization/events-filtered.png)

### Personalisering {#personalization}

Nu kan ni skapa och aktivera målgrupper för personalisering.

#### Skapa målgrupper och skapa kantsegmentering

Navigera i plattformsgränssnittet till **[!UICONTROL Customer]** > **[!UICONTROL Audiences]** och skapa en målgrupp som fångar webbplatsens besökare.

![Se hur man navigerar till målgrupper.](/help/rtcdp/assets/partner-data/onsite-personalization/navigate-to-audiences.png)

Ni måste skapa er målgrupp med [kantsegmentering](/help/segmentation/ui/edge-segmentation.md) så att besökarnas medlemskap utvärderas i realtid när de besöker er webbegenskap.

Se även till att ställa in en [policy för aktiv-på-edge-sammanfogning](/help/destinations/ui/activate-edge-personalization-destinations.md#create-merge-policy) för de största målgrupperna.

#### Integrera med Adobe Target eller något annat anpassat personaliseringsmål

Ni är nu redo att integrera med en personaliseringsmotor för att visa personaliserat innehåll för era webb- eller appbesökare. Adobe rekommenderar att du använder [Adobe Target destination](/help/destinations/catalog/personalization/adobe-target-connection.md) för detta ändamål.

>[!IMPORTANT]
>
>Läs självstudiekursen om [aktivera målgrupper för att kanalisera personaliseringsmål](/help/destinations/ui/activate-edge-personalization-destinations.md) för att få en komplett bild av de steg som krävs för att aktivera era målgrupper.

## Begränsningar och felsökning {#limitations-and-troubleshooting}

Observera följande begränsningar när du utforskar användningsfallet som beskrivs på den här sidan:

* Om du använder partner-ID:n ska du vara medveten om att dessa ID:n inte används när du skapar dina [identitetsdiagram](/help/identity-service/ui/identity-graph-viewer.md).

## Andra användningsområden som uppnås genom stöd för partnerdata {#other-use-cases}

Upptäck fler användningsfall tack vare partnerdatastöd i Real-Time CDP:

* [Komplettera förstahandsprofiler med attribut från betrodda datapartners](/help/rtcdp/partner-data/supplement-first-party-profiles.md) för att förbättra er grund för data och få nya insikter om er kundbas och få bättre målgruppsoptimering.
* Använd datastöd från tredje part i Real-Time CDP för att [utöka er profilbas med profiler med potentiella kunder från datapartners och engagera med dem för att förvärva eller nå nya kunder](/help/rtcdp/partner-data/prospecting.md).
* [Utökad aktivering av profiler för potentiella kunder och målgrupper för potentiella kunder](/help/destinations/ui/activate-prospect-audiences.md) för att välja mål.
