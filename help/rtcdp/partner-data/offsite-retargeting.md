---
title: Återannonsering utanför webbplatsen av oautentiserade besökare
description: Lär dig hur du omdirigerar oautentiserade användare genom att använda ID:n för potentiella kunder för att skapa ett beräknat attribut som kan användas för att skapa en publik med oautentiserade användare.
feature: Use Cases, Customer Acquisition
exl-id: cffa3873-d713-445a-a3e1-1edf1aa8eebb
source-git-commit: 5b37b51308dc2097c05b0e763293467eb12a2f21
workflow-type: tm+mt
source-wordcount: '1358'
ht-degree: 0%

---

# Återmarknadsföring utomhus av oautentiserade besökare

>[!AVAILABILITY]
>
>Den här funktionen är tillgänglig för kunder som har licens för Real-Time CDP (App Service), Adobe Experience Platform Activation, Real-Time CDP, Real-Time CDP Prime, Real-Time CDP Ultimate. Läs mer om de här paketen i [produktbeskrivningarna](https://helpx.adobe.com/legal/product-descriptions.html) och kontakta din Adobe-representant för mer information.

Lär dig hur du skapar en publik med oautentiserade besökare och omdirigerar dem med partnertillhandahållna varaktiga ID:n.

![En infografik som visar flödet av partnerdata från förtäring till Adobe Experience Platform till utdata via målgrupper till ett nedströmsmål.](../assets/offsite-retargeting/header.png)

## Varför ska man överväga det här användningsexemplet? {#why-use-case}

I och med att cookies från tredje part fasas ut måste digitala marknadsförare omforma sina strategier för att återengagera anonyma besökare. Varumärken som väljer att integrera med identitetsleverantörer för besöksigenkänning i realtid kan också utnyttja partnertillhandahållna varaktiga identifierare för återmarknadsföring via betalmedia utanför webbplatsen.

Trots en hög trafikvolym ser många varumärken en betydande nedgång under konverteringsfasen. Besökarna interagerar med innehåll och produktdemonstrationer, men lämnar dem utan att behöva registrera sig eller göra ett köp.

Ni kan inte bara bygga målgrupper baserat på webbplatsengagemang för att personalisera marknadsföringsmeddelanden, ni kan också använda Adobe support för partner-ID:n för att återengagera besökare över betalmediematerial.

## Förutsättningar och planering {#prerequisites-and-planning}

När du planerar att återannonsera oautentiserade besökare bör du tänka på följande under planeringsprocessen:

- Har jag konfigurerat partner-ID:n med rätt ID-namnutrymmen?

För att implementera användningsexemplet använder du dessutom följande Real-Time CDP-funktioner och gränssnittselement. Se till att du har de nödvändiga attributbaserade behörigheterna för åtkomstkontroll i alla dessa områden eller be systemadministratören att ge dig de behörigheter som krävs.

- [Målgrupper](../../segmentation/home.md)
- [Beräknade attribut](../../profile/computed-attributes/overview.md)
- [Mål ](../../destinations/home.md)
- [Webb-SDK](../../web-sdk/home.md)

## Hämta partnerdata till Real-Time CDP {#get-data-in}

Om ni vill skapa en publik med oautentiserade besökare måste ni först få in era partnerdata i Real-Time CDP.

Om du vill lära dig hur du bäst importerar data till Real-Time CDP med Web SDK läser du [avsnitten om datahantering och händelsedatainsamling](./onsite-personalization.md#data-management) i användningsexemplet om anpassning av webbplatser.

## Förse partnern med ID:n {#bring-partner-ids-forward}

När du har importerat partnertillhandahållna ID:n till en händelsedatamängd måste du hämta dessa data till profilposterna. Du kan göra detta genom att använda beräknade attribut.

Med beräknade attribut kan du snabbt konvertera profilbeteendedata till aggregerade värden på profilnivå. Det innebär att du kan använda dessa uttryck, till exempel&quot;total köptid för livstid&quot; i profilen, så att du enkelt kan använda det beräknade attributet inom dina målgrupper. Mer information om beräknade attribut finns i [översikten över beräknade attribut](../../profile/computed-attributes/overview.md).

Om du vill komma åt beräknade attribut väljer du **[!UICONTROL Profiles]** följt av **[!UICONTROL Computed attributes]** och **[!UICONTROL Create computed attribute]**.

![Knappen [!UICONTROL Create computed attributes] markeras förutom fliken [!UICONTROL Computed attributes] på arbetsytan i [!UICONTROL Profiles].](../assets/offsite-retargeting/create-ca.png)

Sidan **[!UICONTROL Create computed attribute]** visas. På den här sidan kan du använda komponenterna för att skapa ett beräknat attribut.

![Arbetsytan för att skapa beräknade attribut visas.](../assets/offsite-retargeting/ca-page.png)

>[!NOTE]
>
>Mer information om hur du skapar beräknade attribut finns i [användargränssnittshandboken för beräknade attribut](../../profile/computed-attributes/ui.md).

I det här fallet kan du skapa ett beräknat attribut som, om partner-ID:t finns, hämtar det senaste värdet för partner-ID:t inom de senaste 24 timmarna.

Med hjälp av sökfältet kan du hitta och lägga till händelsen &quot;Partner-ID&quot; som [du skapade under användningsexemplet ](#get-data-in) för anpassning på plats i den beräknade attributarbetsytan.

![Fliken [!UICONTROL Events] och sökfältet är markerade.](../assets/offsite-retargeting/ca-add-partner-id.png)

När du har lagt till händelsen &quot;Partner ID&quot; i definitionen anger du villkoret för händelsefiltrering till **[!UICONTROL Exists]**, anger att villkoret för händelsefiltrering ska vara **[!UICONTROL Most Recent]**-värdet för det partner-ID som lagts till och med en uppslagsperiod på 24 timmar.

![Definitionen av det beräknade attribut som du vill skapa är markerad.](../assets/offsite-retargeting/ca-add-definition.png)

Ge det beräknade attributet ett lämpligt namn (till exempel&quot;partner-ID&quot;) och en beskrivning, och välj sedan **[!UICONTROL Publish]** för att slutföra den beräknade processen för att skapa attribut.

![Grundinformationen för det beräknade attribut som du vill skapa är markerad.](../assets/offsite-retargeting/ca-publish.png)

## Skapa en målgrupp med det beräknade attributet {#create-audience}

Nu när du har skapat det beräknade attributet kan du använda det här beräknade attributet för att skapa en målgrupp. I det här exemplet kommer du att skapa en målgrupp bestående av besökare som besökt din webbplats mer än fem gånger den här månaden, men som ännu inte har registrerat sig.

Om du vill skapa en målgrupp väljer du **[!UICONTROL Audiences]** följt av **[!UICONTROL Create audience]**.

![Knappen [!UICONTROL Create audience] är markerad.](../assets/offsite-retargeting/create-audience.png)

En dialogruta visas där du uppmanas att välja mellan [!UICONTROL Compose audience] och [!UICONTROL Build rule]. Välj **[!UICONTROL Build rule]** följt av **[!UICONTROL Create]**.

![Knappen [!UICONTROL Build rule] är markerad.](../assets/offsite-retargeting/select-build-rule.png)

Sidan Segment Builder visas. På den här sidan kan du använda komponenterna för att skapa en målgrupp.

![Segmentbyggaren visas.](../assets/offsite-retargeting/segment-builder.png)

>[!NOTE]
>
>Mer information om hur du använder segmentbyggaren finns i [gränssnittsguiden för segmentbyggaren](../../segmentation/ui/segment-builder.md).

För att kunna hitta de här besökarna måste du först lägga till en **[!UICONTROL Page View]**-händelse till din målgrupp. Välj fliken **[!UICONTROL Events]** under **[!UICONTROL Fields]**, dra och släpp sedan händelsen **[!UICONTROL Page View]** och lägg till den på arbetsytan för händelseavsnittet.

![Fliken [!UICONTROL Events] i avsnittet [!UICONTROL Fields] är markerad när [!UICONTROL Page View]händelsen ](../assets/offsite-retargeting/add-page-view.png) visas.

Välj den nyligen tillagda **[!UICONTROL Page View]**-händelsen. Ändra uppslagsperioden från **[!UICONTROL Any time]** till **[!UICONTROL This month]** och ändra händelseregeln så att den omfattar **minst 5**.

![Information om den tillagda [!UICONTROL Page View]-händelsen visas.](../assets/offsite-retargeting/edit-event.png)

När du har lagt till händelsen måste du lägga till ett attribut. Eftersom du arbetar med oautentiserade besökare kan du lägga till det beräknade attributet som du nyss skapade. Det nya beräknade attributet gör att du kan länka partner-ID:n till en målgrupp.

Om du vill lägga till det beräknade attributet väljer du **[!UICONTROL XDM Individual Profile]** under **[!UICONTROL Attributes]**, följt av **[organisationens klient-ID](../../xdm/api/getting-started.md#know-your-tenant-id).**, **[!UICONTROL SystemComputedAttributes]** och **[!UICONTROL PartnerID]**. Lägg till **[!UICONTROL Value]** av det beräknade attributet i attributavsnittet på arbetsytan.

![Mappsökvägen för åtkomst av det beräknade attributet visas.](../assets/offsite-retargeting/access-computed-attribute.png)

Sök dessutom efter **[!UICONTROL Personal Email]** och lägg till attributet **[!UICONTROL Address]** nedan **[!UICONTROL PartnerID]** i attributavsnittet på arbetsytan.

![Det [!UICONTROL PartnerID] beräknade attributet och attributet [!UICONTROL Personal Email Address] markeras på arbetsytan i Segment Builder.](../assets/offsite-retargeting/added-attributes.png)

Nu när du har lagt till dina attribut måste du ange deras utvärderingskriterier. För **[!UICONTROL PartnerID]** anger du villkoret till **[!UICONTROL exists]** och för **[!UICONTROL Address]** anger du villkoret till **[!UICONTROL does not exist]**.

![De korrekta värdena för attributen är markerade.](../assets/offsite-retargeting/set-attribute-values.png)

Du har nu skapat en målgrupp som letar efter besökare med hög intensitet som har ett partnertillhandahållet ID men som ännu inte har registrerat sig för webbplatsen. Ge din målgrupp namnet&quot;Återannonsera oautentiserade användare&quot; och välj **[!UICONTROL Save]** för att slutföra målgruppen.

![Publiken har markerats.](../assets/offsite-retargeting/save-audience-properties.png)

## Aktivera er målgrupp {#activate-audience}

När ni har skapat er målgrupp kan ni nu aktivera målgruppen för efterföljande destinationer. Välj **[!UICONTROL Audiences]** i den vänstra navigeringslisten, sök efter den nya målgruppen, markera ellipsikonen och välj **[!UICONTROL Activate to destination]**.

![Knappen [!UICONTROL Activate to destination] är markerad.](../assets/offsite-retargeting/activate-to-destination.png)

>[!NOTE]
>
>Alla måltyper, inklusive filbaserade mål, stöder målgruppsaktivering med partner-ID:n.
>
>Mer information om hur du aktiverar målgrupper till ett mål finns i [aktiveringsöversikten](../../destinations/ui/activation-overview.md).

Sidan **[!UICONTROL Activate destination]** visas. På den här sidan kan du välja vilket mål du vill aktivera målet till. Välj **[!UICONTROL Next]** när du har valt önskat mål.

![Målet som du vill aktivera målgruppen för markeras.](../assets/offsite-retargeting/select-destination.png)

Sidan **[!UICONTROL Scheduling]** visas. På den här sidan kan du skapa ett schema som anger hur ofta du vill att målgruppen ska aktiveras. Välj **[!UICONTROL Create schedule]** om du vill skapa ett schema för målgruppsaktiveringen.

![Knappen [!UICONTROL Create schedule] är markerad.](../assets/offsite-retargeting/select-create-schedule.png)

[!UICONTROL Scheduling]-pekaren visas. På den här sidan kan du skapa ett schema för målgruppsaktivering. När du har konfigurerat schemat väljer du **[!UICONTROL Create]** för att fortsätta.

![Schemaläggningsdrivrutinen för konfiguration visas.](../assets/offsite-retargeting/configure-schedule.png)

När du har bekräftat schemaläggningsinformationen väljer du **[!UICONTROL Next]**.

![Information om schemat visas.](../assets/offsite-retargeting/created-schedule.png)

Sidan **[!UICONTROL Select attributes]** visas. På den här sidan kan du välja vilka attribut du vill exportera tillsammans med den aktiva målgruppen. Du bör åtminstone inkludera partner-ID, eftersom detta gör att du kan identifiera de besökare som du planerar att återannonsera. Välj **[!UICONTROL Add new mapping]** och sök efter det beräknade attributet. När du har lagt till de nödvändiga attributen väljer du **[!UICONTROL Next]**.

![Både knappen [!UICONTROL Add new mapping] och det beräknade attributet är markerade.](../assets/offsite-retargeting/add-new-mapping.png)

Sidan **[!UICONTROL Review]** visas. På den här sidan kan du läsa mer om målgruppsaktiveringen. Om du är nöjd med den angivna informationen väljer du **[!UICONTROL Finish]**.

![Sidan [!UICONTROL Review] visas med information om målgruppsaktiveringen.](../assets/offsite-retargeting/review-destination-activation.png)

Du har nu aktiverat en publik av oautentiserade användare till en nedladdad destination för ytterligare återmarknadsföring.

## Andra användningsområden {#other-use-cases}

Du kan utforska fler användningsfall som aktiveras via partnerdatasupport i Real-Time CDP:

- [Engagera och skaffa nya kunder](./prospecting.md) med partnerdata.
- [Anpassa upplevelser på plats](./offsite-retargeting.md) med partnerstödd besökarigenkänning.
- [Komplettera förstapartsprofiler](./supplement-first-party-profiles.md) med attribut som tillhandahålls av partner.
