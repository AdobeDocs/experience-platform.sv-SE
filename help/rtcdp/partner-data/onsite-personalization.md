---
title: Personalisera upplevelser på plats för okända besökare med partnerstödd besökarigenkänning
description: Lär dig hur du använder partnerstödd igenkänning av besökare för att leverera personaliserade upplevelser på plats för besökarna.
feature: Use Cases, Personalization, Customer Acquisition
exl-id: 99677988-1df8-47b1-96b1-0ef6db818a1d
source-git-commit: 5b37b51308dc2097c05b0e763293467eb12a2f21
workflow-type: tm+mt
source-wordcount: '2565'
ht-degree: 1%

---

# Personalisera upplevelser på plats för okända besökare med partnerstödd besökarigenkänning

>[!AVAILABILITY]
>
>Den här funktionen är tillgänglig för kunder som har licens för Real-Time CDP (App Service), Adobe Experience Platform Activation, Real-Time CDP, Real-Time CDP Prime, Real-Time CDP Ultimate. Läs mer om de här paketen i [produktbeskrivningarna](https://helpx.adobe.com/legal/product-descriptions.html) och kontakta din Adobe-representant för mer information.

Lär dig hur du kan använda partnerstödd igenkänning för att leverera personaliserade upplevelser till besökare på era webbegenskaper. Använd den här självstudiekursen för att förstå implementeringssekvensen för olika element i Experience Platform och andra Experience Cloud-lösningar för att visa en personaliserad upplevelse för autentiserade och oautentiserade besökare.

![En infografik som beskriver hur du använder partnertillhandahållna attribut för att leverera personaliserade upplevelser till dina besökare.](/help/rtcdp/assets/partner-data/onsite-personalization/onsite-personalization-overview.png)

## Varför ska man tänka på det här användningsexemplet? {#why-this-use-case}

Fragmentering av digitala upplevelser när konsumenterna interagerar med varumärken på många olika sätt är mycket verkligt och blir allt svårare att lösa. De bästa strategierna för kundengagemang för sammanhängande upplevelser, målinriktade rekommendationer och skräddarsydda interaktioner begränsas alla av användarigenkänningen.

Här kan partnerstödd realtidsigenkänning göra en meningsfull skillnad. Med Adobe kan identitetspartners ansluta sig till våra avancerade datainsamlingar på klientsidan och marknadsledande upplevelseoptimeringserbjudanden för att effektivt höja ribban när det gäller upplevelseleverans från första besöket och framåt, utan tidigare historik eller autentisering.

Detta är särskilt värdefullt för vertikala annonser med låga autentiseringsnivåer, som konsumentförpackade varor, onlinebutiker med mera.

## Branschexempel {#industry-example}

Som ett exempel kan nämnas ett heminredningsvarumärke som har låg autentiseringsfrekvens. Det här varumärket vill leverera personaliserade upplevelser till förstagångsbesökare, utan tidigare historik eller autentisering, och utan att tona ned beroendet av cookies från tredje part.

Detta varumärke väljer att utnyttja teknik för partnerigenkänning för att troligtvis identifiera besökaren och leverera en mer personaliserad upplevelse. Detta hjälper besökaren att komma vidare när marknadsföringstratten närmar sig. Varumärket kan till exempel använda demografiska signaler som tillhandahålls av partners för innehåll på plats som tilltalar personer som nyligen har flyttat och erbjuder en rabatt på populära DIY-produkter.

## Förutsättningar och planering {#prerequisites-and-planning}

När du planerar att använda attribut som tillhandahålls av partners för att leverera personaliserade upplevelser till autentiserade och oautentiserade besökare bör du tänka på följande under planeringsprocessen:

* Vilka indata förväntas av din partners igenkänningsteknik så att de kan ligga på fler attribut?
* I vilken utsträckning kan ni leverera personalisering i olika kanaler och för olika användningsområden baserat på sannolikhetshärledda datauppsättningar, jämfört med deterministiskt bekräftade attribut?
* Hur ska upplevelsen av en förautentiserad men erkänd besökare förändras när de autentiseras?

### UI-funktionalitet, plattformskomponenter och Experience Cloud-produkter som du kommer att använda {#ui-functionality-and-elements}

För att implementera det här användningsexemplet måste du använda flera olika delar av Real-time Customer Data Platform och andra Experience Cloud-lösningar. Kontrollera att du har de [attributbaserade åtkomstkontrollsbehörigheterna](/help/access-control/abac/overview.md) som krävs för alla dessa områden, eller be systemadministratören att ge dig de behörigheter som krävs.

* Datainsamling
   * [Webb-SDK för Adobe Experience Platform](/help/web-sdk/home.md)
   * [Taggar](/help/tags/home.md)
   * [Dataströmmar](/help/datastreams/overview.md)
* Datahantering i Real-Time CDP
   * [Identiteter](/help/identity-service/features/namespaces.md)
   * [Scheman](/help/xdm/home.md)
   * [Dataanvändningsetiketter](/help/data-governance/labels/overview.md)
   * [Datauppsättningar](/help/catalog/datasets/overview.md)
* Webbegenskapspersonalisering
   * [Edge segmentering](/help/segmentation/ui/edge-segmentation.md)
   * [Edge Personalization-mål](/help/destinations/destination-types.md#edge-personalization-destinations)
   * [Adobe Target](/help/destinations/catalog/personalization/adobe-target-connection.md) (eller en valfri personaliseringsplattform. Den här självstudiekursen om hur du använder Adobe Target som personaliseringsmotor)

## Videogenomgång {#video-walkthrough}

Se videosjälvstudiekursen nedan för en genomgång av hur ni personaliserar webbplatsupplevelser för okända besökare:

>[!VIDEO](https://video.tv.adobe.com/v/3423076/?learn=on)

## Så här uppnår du användningsfallet: översikt på hög nivå {#achieve-the-use-case-high-level}

![En infografik som beskriver hur du använder partnertillhandahållna attribut för att leverera personaliserade upplevelser till dina besökare.](/help/rtcdp/assets/partner-data/onsite-personalization/onsite-personalization-steps.png)

1. Som **kund** licensierar du från **datapartnern** möjligheten att hämta insikter i realtid om annars anonyma webbplatsbesökare.
2. Som **kund** distribuerar du bibliotek på klientsidan på dina egenskaper för att anropa **partner** API:er och du konfigurerar Web SDK eller Mobile SDK för att skicka signaler från partner till Real-Time CDP.
3. När du surfar på din webbplats eller i din app identifieras **besökaren** troligtvis av **partnern** som returnerar attribut tillsammans med ett ID.
4. Real-Time CDP kör kantsegmentering för att utvärdera inkommande händelseträffar och kvarstår resultat mot [ECID-identifieraren](https://experienceleague.adobe.com/docs/id-service/using/home.html).
5. Adobe Target använder kantsegmenteringsutdata för att återge upplevelsen till **besökaren** för anpassning under sessionen.
6. Händelsen bevaras i sin helhet för arbetsflöden längre fram i kedjan, som analys och återmarknadsföring.

## Så här uppnår du användningsfallet: stegvisa instruktioner {#step-by-step-instructions}

Läs igenom avsnitten nedan som innehåller länkar till ytterligare dokumentation för att slutföra varje steg i översikten ovan.

### Datahantering - Skapa ett identitetsnamnutrymme, ett schema och en datauppsättning för att hantera dataattribut {#data-management}

Innan ni kan uppnå användningsexemplet för att personalisera oautentiserade besökares upplevelse, måste ni först skapa datahanteringsstrukturen i Real-Time CDP för att kunna ta emot inkommande data om realtidshändelser och målgruppskvalifikationer.

#### Skapa namnområde för partner-ID

Först måste du skapa ett namnutrymme för en partner-ID-identitet. Navigera till **[!UICONTROL Customer]** > **[!UICONTROL Identities]** i den vänstra listen och välj sedan **[!UICONTROL Create identity namespace]** i skärmens övre högra hörn.

![Dialogrutan Skapa ID-namnområde med partner-ID markerad.](/help/rtcdp/assets/partner-data/onsite-personalization/create-identity-namespace.png)

Läs mer om hur du [skapar ett namnområde för en partner-ID ](/help/rtcdp/partner-data/prospecting.md#create-partner-id-namespace).

#### Skapa ett schema

Skapa sedan ett [!UICONTROL Experience Event]-schema för de tidsseriedata som du senare samlar in från dina webbegenskaper och se till att du använder [!UICONTROL XDM ExperienceEvent] som basklass för schemat. Läs om hur du [skapar ett schema med hjälp av användargränssnittet i Experience Platform](/help/xdm/ui/resources/schemas.md#create).

![Arbetsytan Scheman med schemat Skapa och XDM Experience-händelsen har markerats.](/help/rtcdp/assets/partner-data/onsite-personalization/create-experience-event-schema.png)

När du skapar schemat och [lägger till fältgrupper i schemat](/help/xdm/ui/resources/schemas.md#add-field-groups) bör du lägga till fältgrupperna [Besök webbsidan](/help/xdm/field-groups/event/web-details.md) och [Identitetskarta](/help/xdm/field-groups/profile/identitymap.md). Detta är utöver andra fältgrupper som är tillämpliga på er digitala egendom och datainsamling.

Dessutom kan du skapa eller återanvända en befintlig fältgrupp och lägga till den i ditt schema för att få partnerinformation om besökaren. Läs om hur du [skapar en fältgrupp](/help/xdm/ui/resources/field-groups.md) och om hur du [lägger till fält](/help/xdm/ui/resources/field-groups.md) i fältgruppen. Om du till exempel förväntar dig att personalisera mot partnertillhandahållna insikter som åldersintervall, anställningsstatus, månatlig utgiftsstyrka eller köpbeteenden, ska fältgruppen innehålla lämpliga fält.

Om dataparten tillhandahåller en stabil identifierare för besökaren och du vill ta med den till Real-Time CDP måste du se till att ha ett lämpligt namngivet fält för identifieraren i din anpassade fältgrupp. Du bör även markera fältet som en identitet i det identitetsnamnområde som du skapade tidigare. Kom även ihåg att [aktivera schemat som ska inkluderas i profilen](/help/xdm/ui/resources/schemas.md#profile).

#### Skapa en datauppsättning

Därefter måste du skapa en datauppsättning för de tidsseriedata som du samlar in från besökarna på din webbegenskap och som du kommer att använda för personalisering på plats.

Läs självstudiekursen om [hur du skapar en datauppsättning](/help/catalog/datasets/user-guide.md#create) och kom ihåg att välja alternativet att skapa datauppsättningen från ett schema. Skapa datauppsättningen baserat på schemat som du skapade i föregående steg.

På samma sätt som när du skapar ett schema måste du aktivera datauppsättningen som ska inkluderas i [!UICONTROL Real-Time Customer Profile]. Mer information om hur du aktiverar datauppsättningen för användning i [!UICONTROL Real-Time Customer Profile] finns i självstudiekursen [Skapa schema.](/help/xdm/tutorials/create-schema-ui.md#profile)

### Implementera händelsedatainsamling på din webbegenskap {#implement-data-collection}

När du har konfigurerat datahanteringskonfigurationen måste du nu implementera [datainsamling](/help/collection/home.md) i realtid för händelsen på din webbegenskap. Du måste mäta din egendom med datainsamlingsbiblioteket Adobe - [!UICONTROL Web SDK] - för att samla in händelsesamtal i realtid och skicka tillbaka dem till Real-Time CDP. Det här objektet består av ett par olika åtgärder för ett fåtal datainsamlingskomponenter.

>[!IMPORTANT]
>
>Om du vill hämta attribut från partner måste du även *integrera din webbegenskap med partner-API:er eller andra metoder för att anropa och hämta attribut från datapartners i realtid*. Diskutera den här aspekten med din valfria partner eftersom den inte är underställd kursen.

Använd först programväljaren i skärmens övre högra hörn för att navigera till avsnittet **[!UICONTROL Data Collection]**.

>[!TIP]
>
>Kontakta systemadministratören och be om åtkomst om du inte kan se [!UICONTROL Data Collection] i programväljaren.

![Appväxlare för att komma till avsnittet Datainsamling.](/help/rtcdp/assets/partner-data/onsite-personalization/app-switcher-data-collection.png)

Avsnittet **[!UICONTROL Data Collection]** i gränssnittet ser ut ungefär som bilden nedan.

![Datainsamlingssektionen i plattformsgränssnittet.](/help/rtcdp/assets/partner-data/onsite-personalization/data-collection-home.png)

#### Skapa datastream

Som ett första steg i datainsamlingsavsnittet [skapar du ett nytt datastream](/help/datastreams/configure.md). Datastream är grunden för hur data samlas in och dirigeras korrekt till rätt Adobe-app, i det här fallet Experience Platform.

När du skapar datastream väljer du det schema som du skapade tidigare i fältet **[!UICONTROL Event schema]**.

![Händelseschemeväljaren markerades när en ny datastream konfigurerades.](/help/rtcdp/assets/partner-data/onsite-personalization/event-schema-selector-datastream.png)

[Markera händelsedatamängden](/help/datastreams/configure.md#aep) som du skapade tidigare i listrutan, markera rutorna intill **[!UICONTROL Edge Segmentation]** och **[!UICONTROL Personalization Destinations]** och välj **[!UICONTROL Save]**.

Observera att du inte behöver välja någon profildatauppsättning i det här scenariot eftersom du samlar in händelsebaserade tidsseriedata.

#### Skapa taggegenskap

Tänk på en egenskap som en behållare som du fyller med tillägg, regler, dataelement och bibliotek när du distribuerar taggar till webbplatsen.

Navigera till **[!UICONTROL Tags]** och välj **[!UICONTROL New property]**.

![Skapa en ny taggegenskap.](/help/rtcdp/assets/partner-data/onsite-personalization/create-tag-property.png)

Fyll i obligatoriska fält och välj **[!UICONTROL Save]**.

![Fyll i obligatoriska fält för den nya egenskapen.](/help/rtcdp/assets/partner-data/onsite-personalization/tag-property-fields.png)

Få fullständig information om hur du [skapar en taggegenskap](https://experienceleague.adobe.com/docs/platform-learn/implement-in-websites/configure-tags/create-a-property.html).

Därefter måste du installera olika tillägg i egenskapen. Välj taggegenskapen och navigera till avsnittet [!UICONTROL Extensions].

![Välj en ny taggegenskap.](/help/rtcdp/assets/partner-data/onsite-personalization/select-tag-property.png)

Observera att tillägget [!UICONTROL Core] redan är installerat. Du måste installera ytterligare två tillägg, vilket beskrivs i nästa avsnitt.

![Visa installerade tillägg.](/help/rtcdp/assets/partner-data/onsite-personalization/view-existing-extensions.png)

#### Installera SDK-tillägg för webben

Observera att den här självstudiekursen visar hur du kan instrumentera din webbplats med Web SDK. Du kan också använda [Mobile SDK](https://developer.adobe.com/client-sdks/documentation/) i din app för att anpassa upplevelsen för appbesökarna.

![Vy över Web SDK-tillägget i tilläggskatalogen.](/help/rtcdp/assets/partner-data/onsite-personalization/web-sdk-extension.png)

Gå ned till avsnittet **[!UICONTROL Datastreams]** på skärmen för att konfigurera Web SDK och ange information om den Experience Platform-sandlåda som du använder. Välj lämplig sandlåda och den datastam som skapades i föregående steg i nästa listruta. Du kan välja samma sandbox- och datastream-värden för alla andra miljöer. Ändra inte de andra inställningarna och välj **[!UICONTROL Save]**.

Få fullständig information om [hur du installerar Web SDK](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/tags-configuration/install-web-sdk.html).

#### Installera ID-tjänsttillägg

Använd [Experience Cloud ID-tjänsttillägget](/help/tags/extensions/client/id-service/overview.md) för att skapa en unik enhetsbaserad förstapartidentitet för besökare i alla Experience Cloud-lösningar. Sök efter **[!UICONTROL ID Service]** i tilläggskatalogen och installera den. Behåll alla standardinställningar när du installerar tillägget.

![Vy över ID-tjänsttillägget i tilläggskatalogen.](/help/rtcdp/assets/partner-data/onsite-personalization/id-service-extension.png)

#### Konfigurera miljöer

Gå sedan vidare till avsnittet **[!UICONTROL Environments]** från den vänstra navigeringen. I det här steget måste du ansluta webbplatsen till Adobe Edge Network för att hämta och leverera besöksinformation i realtid.

Markera ruteikonen till höger om utvecklingsmiljön och kopiera standardversionen av JavaScript-kodfragmentet som visas i ett modalt fönster.

![En ruta markeras i avsnittet Miljö i användargränssnittet för datainsamling.](/help/rtcdp/assets/partner-data/onsite-personalization/select-box-icon.png)

Du måste lägga till det här kodfragmentet högst upp på webbplatsen. På grund av detta kommer webbplatsen att ringa Adobe Edge Network för att hämta JavaScript-logik som ska läsas in och köras på sidan. Detta gör att funktioner som generering av besökar-ID, datainsamling och personalisering av realtidsupplevelser kan fungera.

#### Ställ in dataelement

Dataelement är byggstenarna för dataordlistan (eller datamappningen). Ett enskilt dataelement är en variabel vars värde kan mappas till frågesträngar, URL:er, cookie-värden, JavaScript-variabler osv. Läs mer om [dataelement](/help/tags/ui/managing-resources/data-elements.md).

I det här användningsexemplet måste du ställa in två dataelement.

Konfigurera först ett `partnerData`-element. Navigera till avsnittet **[!UICONTROL Data Elements]** och välj **[!UICONTROL Create New Data Element]**.

![Skapa ett nytt dataelement.](/help/rtcdp/assets/partner-data/onsite-personalization/create-data-element.gif)

Namnge dataelementet `partnerData`, lämna [!UICONTROL extension]-värdet som [!UICONTROL Core] och ange **[!UICONTROL Data Element Type]** som **[!UICONTROL JavaScript Variable]**. Ange `partnerData` i fältet **[!UICONTROL JavaScript variable name]** och välj **[!UICONTROL Save]**.

![Markerade markeringar för att konfigurera dataelementet partnerData korrekt.](/help/rtcdp/assets/partner-data/onsite-personalization/create-partnerdata-data-element.png)

Om du vill konfigurera det andra dataelementet ger du den nya variabeln `pageVisit` ett namn, anger **[!UICONTROL Extension]** som **[!UICONTROL Adobe Experience Platform]** och väljer **[!UICONTROL XDM Object]** som datatyp.

![Markerade markeringar som konfigurerar dataelementet pageVisit korrekt.](/help/rtcdp/assets/partner-data/onsite-personalization/page-visit-data-element.png)

I schemat väljer du de tredjepartsattribut som motsvarar de värden som du förväntar dig från dataparten. Välj sedan alternativknappen **[!UICONTROL Provide entire object]**. Markera ikonen som ser ut som en databas och välj dataelementet `partnerData` som du skapade tidigare.

#### Ställ in regler

I avsnittet **[!UICONTROL Rules]** kan du konfigurera din webbplats så att den skickar en personaliseringsbegäran till Adobe med de inlästa attributen i de dataelement som du just har skapat. Läs mer om [att skapa regler](/help/tags/ui/managing-resources/rules.md).

Välj **[!UICONTROL Create new Rule]**.  Ge den här regeln namnet **[!UICONTROL Personalize]** och välj plustecknet bredvid **[!UICONTROL Events]**. Välj **[!UICONTROL Page Bottom]** som händelse och spara.

![Markeringar för händelsetypen i en regel.](/help/rtcdp/assets/partner-data/onsite-personalization/add-events-rule.png)

Markera plustecknet bredvid **[!UICONTROL Actions]**. Uppdatera tillägget till **[!UICONTROL Adobe Experience Platform Web SDK]** och ange **[!UICONTROL Action Type]** till **[!UICONTROL Send event]**.

![Markeringar för åtgärdstypen som ingår i en regel.](/help/rtcdp/assets/partner-data/onsite-personalization/add-action-rule.png)

Välj `web.webpagedetails.pageViews` som händelsetyp i listrutan **[!UICONTROL Type]** till höger.

![Välj händelsetyp.](/help/rtcdp/assets/partner-data/onsite-personalization/add-pageview-type-rule.png)

Markera databasikonen bredvid XDM-data och markera dataelementet `pageVisit`.

Bläddra nedåt i listan över åtgärdskonfigurationer och kontrollera att kryssrutan **[!UICONTROL Render visual personalization decisions]** är markerad. Detta är viktigt för att upplevelser som levereras via Adobe Target eller andra liknande produkter ska kunna återges visuellt på webbsidan. Välj **[!UICONTROL Keep Changes]** och sedan **[!UICONTROL Save]** regeln.

![Markera kryssrutan för beslut om visuell återgivning.](/help/rtcdp/assets/partner-data/onsite-personalization/render-visual-personalization-toggle.png)

#### Konfigurera publiceringsarbetsflöde

För att distribuera konfigurationen till webbsidan är nästa steg att skapa ett bibliotek som innehåller de resurser du just skapat. Läs mer om hur [konfigurerar ett publiceringsflöde](/help/tags/ui/publishing/publishing-flow.md).

Välj **[!UICONTROL Publishing Flow]** och sedan **[!UICONTROL Add Library]**.

Välj **[!UICONTROL Add all Changed Resources]**, ge biblioteket ett namn, ställ in miljön på **[!UICONTROL Development]** och välj **[!UICONTROL Save & Build to Development]**.

![Skapa bibliotek och distribuera till utvecklingsmiljö](/help/rtcdp/assets/partner-data/onsite-personalization/create-publishing-workflow.gif)

#### Testa din webbplats

Nu bör webbplatsen vara helt integrerad med Web SDK. Om du vill testa att datainsamlingen fungerar som förväntat kan du navigera till webbplatsen och använda webbläsarens utvecklarverktyg för att inspektera nätverkstrafiken.

Ange `interact` i sökrutan, uppdatera sidan och se nätverksanrop från din webbplats till Adobe Edge-nätverkets ifyllnad.

![Vy över nätverkshändelser i utvecklarverktyg.](/help/rtcdp/assets/partner-data/onsite-personalization/events-filtered.png)

### Personalisering {#personalization}

Nu kan ni skapa och aktivera målgrupper för personalisering.

#### Skapa målgrupper och skapa kantsegmentering

I plattformsgränssnittet går du till **[!UICONTROL Customer]** > **[!UICONTROL Audiences]** och skapar en målgrupp som fångar webbplatsens besökare.

![Vy över hur du navigerar till målgrupper.](/help/rtcdp/assets/partner-data/onsite-personalization/navigate-to-audiences.png)

Du måste konfigurera din målgrupp med [kantsegmentering](/help/segmentation/ui/edge-segmentation.md) så att besökarnas målgruppsmedlemskap utvärderas i realtid när de besöker din webbegenskap.

Se även till att ställa in en [aktiv-vid-kant-sammanfogningsprincip](/help/destinations/ui/activate-edge-personalization-destinations.md#create-merge-policy) för kantmålgrupperna.

#### Integrera med Adobe Target eller något annat anpassat personaliseringsmål

Ni är nu redo att integrera med en personaliseringsmotor för att visa personaliserat innehåll för era webb- eller appbesökare. Adobe rekommenderar att du använder [Adobe Target-målet](/help/destinations/catalog/personalization/adobe-target-connection.md) för detta ändamål.

>[!IMPORTANT]
>
>Läs självstudiekursen [Aktivera målgrupper mot kantanpassningsmål](/help/destinations/ui/activate-edge-personalization-destinations.md) för att få en komplett vy över de steg som krävs för att aktivera dina målgrupper.

## Begränsningar och felsökning {#limitations-and-troubleshooting}

Observera följande begränsningar när du utforskar användningsfallet som beskrivs på den här sidan:

* Om du använder partner-ID:n ska du vara medveten om att dessa ID:n inte används när du skapar [identitetsdiagrammet](/help/identity-service/features/identity-graph-viewer.md).

## Andra användningsområden som uppnås genom stöd för partnerdata {#other-use-cases}

Upptäck fler användningsfall tack vare partnerdatastöd i Real-Time CDP:

* [Komplettera förstahandsprofiler med attribut från betrodda datapartners](/help/rtcdp/partner-data/supplement-first-party-profiles.md) för att förbättra er grund för data och få nya insikter om er kundbas och få bättre målgruppsoptimering.
* Använd datastöd från tredje part i Real-Time CDP för att [utöka din profilbas med profiler för potentiella kunder från datapartner och engagera med dem för att förvärva eller nå nya kunder](/help/rtcdp/partner-data/prospecting.md).
* [Utökad aktivering av profiler för potentiella kunder och målgrupper](/help/destinations/ui/activate-prospect-audiences.md) för utvalda mål.
