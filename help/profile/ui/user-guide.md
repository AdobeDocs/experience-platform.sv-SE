---
keywords: Erfarenhetsplattform; profil; kundprofil i realtid; Felsökning; Application Programming Interface; enhetlig profil; Enhetlig profil; enhetlig; Profil; RTCP; aktivera profil; Aktivera profil; Unionschema; FACKLIG PROFIL; Facklig profil
title: Realtids kundprofil UI-guide
description: Real-Time Customer Profile skapar en helhetsbild av var och en av dina enskilda kunder, genom att kombinera data från flera kanaler, inklusive online, offline, CRM och tredjepartsdata. Detta dokument fungerar som en guide för att interagera med kundprofilen i realtid i användargränssnittet för Adobe Experience Platform.
exl-id: 792a3a73-58a4-4163-9212-4d43d24c2770
source-git-commit: d2694170e2860bd32783ad3f1860b0397e847289
workflow-type: tm+mt
source-wordcount: '1921'
ht-degree: 0%

---

# [!DNL Real-Time Customer Profile] UI-guide

[!DNL Real-Time Customer Profile] skapar en helhetsbild av varje kund och kombinerar data från flera kanaler, inklusive online, offline, CRM och tredjepartsdata. Detta dokument fungerar som en vägledning för att interagera med [!DNL Real-Time Customer Profile] data i Adobe Experience Platforms användargränssnitt (UI).

## Komma igång

Denna UI-guide kräver förståelse för de olika [!DNL Experience Platform] tjänster som ingår i hantering [!DNL Real-Time Customer Profiles]. Innan du läser denna guide eller arbetar i användargränssnittet, vänligen granska dokumentationen för följande tjänster:

* [[!DNL Real-Time Customer Profile] översikt](../home.md): Tillhandahåller en enhetlig, realtidsprofil för konsumenter baserad på aggregerad data från flera källor.
* [[!DNL Identity Service]](../../identity-service/home.md): Möjliggör [!DNL Real-Time Customer Profile] genom att brygga identiteter från olika datakällor när de tas in i [!DNL Experience Platform].
* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Det standardiserade ramverket som [!DNL Experience Platform] organiserar kundupplevelsedata med.

## [!UICONTROL Overview]

I Experience Platform-gränssnittet väljer du **[!UICONTROL Profiles]** i den vänstra navigeringen för att öppna fliken **[!UICONTROL Overview]** med profilkontrollpanelen.

>[!NOTE]
>
>Om din organisation inte har använt Experience Platform tidigare och ännu inte har några aktiva profildatauppsättningar eller sammanslagningsprinciper skapade, visas inte instrumentpanelen [!UICONTROL Profiles]. Istället visar fliken [!UICONTROL Overview] länkar och dokumentation som hjälper dig att komma igång med kundprofilen i realtid.

### Kontrollpanel för profil {#profile-dashboard}

På profilkontrollpanelen visas viktiga mätvärden för din organisations profildata.

För att lära dig mer, besök profilens dashboardguide[](../../dashboards/guides/profiles.md).

![Profilpanelen visas.](../../dashboards/images/profiles/dashboard-overview.png)

## Fliken [!UICONTROL Browse]

På fliken **[!UICONTROL Browse]** kan du visa dina profiler antingen i vyn **kort** eller i vyn **diagram** genom att välja växlingsknappen.

![Växlingsknappen för kort- och diagramvyn är markerad.](../images/user-guide/card-graph-view.png)

Dessutom kan du bläddra bland dina profiler med hjälp av en sammanfogningsprincip eller leta upp specifika profiler med hjälp av ett identitetsnamnutrymme och värde.

![Profilerna som tillhör organisationen visas.](../images/user-guide/profile-browse.png)

### Bläddra efter [!UICONTROL Merge policy]

Fliken **[!UICONTROL Browse]** är som standard inställd på en sammanfogningsprincip för din organisation. Om du vill välja en annan sammanfogningsprincip markerar du `X` bredvid sammanfogningsprincipnamnet och använder sedan väljaren för att öppna dialogrutan **[!UICONTROL Select merge policy]**.

>[!NOTE]
>
>Om ingen sammanfogningsprincip är markerad använder du väljarknappen bredvid fältet **[!UICONTROL Merge policy]** för att öppna markeringsdialogrutan.

![Principväljaren för sammanslagning är markerad.](../images/user-guide/browse-by-merge-policy.png)

Om du vill välja en sammanfogningsprincip i dialogrutan **[!UICONTROL Select merge policy]** markerar du alternativknappen bredvid principnamnet och använder sedan **[!UICONTROL Select]** för att gå tillbaka till fliken [!UICONTROL Browse]. Du kan sedan välja **[!UICONTROL View]** om du vill uppdatera exempelprofilerna och se ett exempel på profiler med den nya sammanfogningsprincipen.

![En dialogruta där du kan välja vilken sammanfogningsprincip som ska filtreras efter visas.](../images/user-guide/select-merge-policy.png)

Profilerna som visas representerar ett urval på upp till 20 profiler från din organisations profilbutik efter att den valda sammanfogningsprincipen har tillämpats. Exempelprofilerna för den valda sammanfogningsprincipen uppdateras när nya data läggs till i organisationens profilarkiv.

Om du vill visa information om en av exempelprofilerna väljer du **[!UICONTROL Profile ID]**. Mer information finns i avsnittet om att [visa profilinformation](#profile-detail) senare i den här handboken.

![Exempelprofiler som matchar sammanfogningsprincipen visas.](../images/user-guide/profile-browse-table.png)

Mer information om sammanfogningsprinciper och deras roll i Experience Platform finns i [översikten över sammanfogningsprinciper](../merge-policies/overview.md).

### Bläddra förbi [!UICONTROL Identity] {#browse-identity}

På fliken **[!UICONTROL Browse]** kan du använda ett identitetsnamnutrymme för att slå upp en specifik profil via ett identitetsvärde. Att bläddra efter en identitet kräver att du anger en sammanslagningspolicy, ett identitetsnamnrymd och ett identitetsvärde.

![Väljaren för sammanfogningsprincip är markerad.](../images/user-guide/browse-by-merge-policy.png)

Om det behövs kan du använda väljaren **[!UICONTROL Merge policy]** för att öppna dialogrutan **[!UICONTROL Select merge policy]** och välja den sammanfogningsprincip som du vill använda.

![En dialogruta där du kan välja vilken sammanfogningsprincip som ska filtreras efter visas.](../images/user-guide/select-merge-policy.png)

Använd sedan väljaren **[!UICONTROL Identity namespace]** för att öppna dialogrutan **[!UICONTROL Select identity namespace]** och välj det namnutrymme som du vill söka efter. Om din organisation har många namnutrymmen kan du använda sökfältet i dialogrutan för att börja skriva namnet på ett namnutrymme.

Du kan markera ett namnutrymme om du vill visa mer information eller välja ett namnutrymme genom att markera alternativknappen. Du kan sedan använda **[!UICONTROL Select]** för att fortsätta.

![En dialog där du kan välja identitetsnamnrymden att filtrera efter visas.](../images/user-guide/select-identity-namespace.png)

Efter att ha valt en [!UICONTROL Identity namespace] och återvänt till fliken [!UICONTROL Browse] kan du ange en **[!UICONTROL Identity value]** relaterad till namnrymden du valt.

>[!NOTE]
>
>Detta värde är specifikt för en individuell kundprofil och måste vara en giltig post för det angivna namnrymden. Till exempel skulle valet av identitetsnamnrymden &quot;Email&quot; kräva ett identitetsvärde i form av en giltig e-postadress.

![Identitetsvärdet du vill filtrera efter markeras.](../images/user-guide/browse-identity.png)

När ett värde har matats in, välj **[!UICONTROL View]** och en enda profil som matchar värdet returneras. Välj för **[!UICONTROL Profile ID]** att se en profil.

![Profilen som matchar identitetsvärdet markeras.](../images/user-guide/filtered-identity-value.png)

## Visa profil {#view-profile}

>[!CONTEXTUALHELP]
>id="platform_errors_uplib_201001_404"
>title="Enheten hittades inte"
>abstract="Detta innebär att Experience Platform inte kunde hitta den begärda entiteten. Försök med någon av följande lösningar för att åtgärda felet:<ul><li>Kontrollera att rätt profil-ID finns i URL:en för den entitet du försöker få åtkomst till.</li><li>Kontrollera att du har rätt kombination av organisation och sandlåda för den enhet du försöker få åtkomst till.</li></ul>"

När du har valt **[!UICONTROL Profile ID]** öppnas fliken **[!UICONTROL Detail]**. Profilinformationen som visas på fliken **[!UICONTROL Detail]** har sammanfogats från flera profilfragment till en enda vy över den enskilda kunden. Detta inkluderar kundinformation som grundläggande attribut, länkade identiteter och kanalinställningar.

Dessutom kan du visa annan information om profiler, till exempel dess [attribut](#attributes), [händelser](#events) och [målgruppsmedlemskap](#audience-membership).

### Fliken Detaljer {#profile-detail}

Fliken **[!UICONTROL Details]** ger mer detaljerad information om den valda profilen och är uppdelad i fyra sektioner: Kundprofilinsikter, AI-insiktswidgets, anpassningsbara widgets och automatiskt klassificerade widgets.

![Profilens detaljsida visas.](../images/user-guide/profile-details.png)

Dessutom kan du växla om AI-genererade insikter visas, visa detaljer för hubben jämfört med edge, samt visa detaljerna i grafvyn.

![De ovan nämnda växlarna (AI-genererade insikter, Hub- eller Edge-data samt kort- eller grafvy) är markerade.](../images/user-guide/profile-toggles.png)

#### Kundprofilinsikter {#customer-profile-insights}

Avsnittet **[!UICONTROL Customer profile insights]** visar en kort introduktion till profilens attribut. Detta inkluderar profil-ID, e-post, telefonnummer, kön, födelsedatum samt profilens identiteter och medlemskap i målgruppen.

![Avsnittet för kundprofilinsikter visas.](../images/user-guide/customer-profile-insights.png)

#### AI-insiktswidgets {#ai-insight-widgets}

[!BADGE Alpha]{type=Informative} : Denna funktion finns för närvarande i Alpha.

Sektionen **[!UICONTROL AI insight widgets]** visar widgets som genereras av AI. Dessa widgets ger snabba insikter om profilen, baserat på profildata inklusive demografi (såsom ålder, kön eller plats), användarbeteenden (såsom köphistorik, webbplatsaktivitet eller engagemang i sociala medier) samt psykologiska data (såsom intressen, preferenser eller livsstilsval). Alla AI-widgetar använder data som **redan** finns i profilen.

![AI-widgetar visas.](../images/user-guide/ai-insight-widgets.png)

#### Anpassningsbara widgetar {#customizable-widgets}

I avsnittet **[!UICONTROL Customizable widgets]** visas widgetar som du kan anpassa efter dina affärsbehov. Du kan gruppera attribut i separata widgetar, ta bort oönskade widgetar eller justera widgetarnas layout.

Standardfälten som visas kan också ändras på organisationsnivå för att visa de önskade profilattributen. Om du vill veta mer om hur du anpassar de här fälten, inklusive steg-för-steg-instruktioner om hur du lägger till och tar bort attribut och ändrar storlek på kontrollpaneler, kan du läsa [anpassningsguiden för profildetaljer](profile-customization.md).

![Avsnittet för anpassningsbara widgets visas.](../images/user-guide/customizable-widgets.png)

Du kan också välja att växla mellan att se attributnamnen som deras visningsnamn och deras fältvägsnamn. Om du vill växla mellan dessa två skärmar väljer du alternativet **[!UICONTROL Show display names]**.

![Växlingen av visningsnamn är markerad.](../images/user-guide/show-display-names.png)

#### Automatiskt klassificerade widgetar {#auto-classified-widgets}

[!BADGE Alpha]{type=Informative} Den här funktionen finns i Alpha.

Avsnittet **[!UICONTROL Auto-classified widgets]** visar widgetar som utnyttjar unionsschemat för att avgöra vilka källfältsgrupper ett attribut tillhör, vilket ger en tydligare kontext om varifrån data kommer. Du kan använda sökfältet för att enklare söka efter nyckelord i dina widgetar.

Dessa widgetar kombinerar både händelsedata (med Experience-händelsewidgeten) och attributdata, så att du får en enhetlig vy över din profil. Du kan använda de här widgetarna för att utforska strukturen för din profils data för att bättre strukturera dina [anpassningsbara widgetar](#customizable-widgets).

>[!NOTE]
>
>Om det finns flera källfältsgrupper kommer widgetarna endast att använda **ett** av de tillgängliga alternativen.

![Avsnittet med automatiskt klassificerade widgetar visas.](../images/user-guide/auto-classified-widgets.png)

### Fliken Attribut {#attributes}

Fliken **[!UICONTROL Attributes]** innehåller en listvy med en sammanfattning av alla attribut som hör till en enskild profil, efter att den angivna sammanfogningsprincipen har tillämpats.

Dessa attribut kan också visas som ett JSON-objekt genom att välja till **[!UICONTROL View JSON]**. Detta är praktiskt för alla som vill förstå hur profilattributen importeras till Experience Platform.

![Fliken Attribut är markerad. Profilattributen visas.](../images/user-guide/attributes.png)

Om du vill visa de attribut som är tillgängliga på Edge väljer du **[!UICONTROL Edge]** i dataplatsväljaren.

![Dataplatsväljaren på fliken Attribut är markerad.](../images/user-guide/attributes-select.png)

För mer information om edgeprofiler, vänligen [läs edge-profilernas dokumentation](../edge-profiles.md).

### Fliken Evenemang {#events}

Fliken **[!UICONTROL Events]** innehåller data från de 100 senaste ExperienceEvents kopplade till kunden. Denna data kan inkludera e-postöppningar, kundvagnsaktiviteter och sidvisningar. Att välja **[!UICONTROL View all]** för en enskild händelse ger ytterligare fält och värdefångar som en del av evenemanget.

Händelser kan också visas som ett JSON-objekt genom att välja till **[!UICONTROL View JSON]**. Detta är praktiskt när du vill veta hur händelser spelas in i Experience Platform.

![Fliken Händelser är markerad. Profilhändelserna visas.](../images/user-guide/events.png)

### Fliken Målgruppsmedlemskap {#audience-membership}

Fliken **[!UICONTROL Audience membership]** visar en lista med namn och beskrivning av målgrupper som den enskilda kundprofilen för närvarande tillhör. Listan uppdateras automatiskt när profilen kvalificerar sig eller upphör att gälla. Det totala antalet målgrupper som profilen är kvalificerad för visas till höger på fliken.

Mer information om segmentering i Experience Platform finns i [dokumentationen för Experience Platform segmenteringstjänst](../../segmentation/home.md).

![Fliken Målgruppsmedlemskap är markerad. Profilens medlemsinformation visas.](../images/user-guide/audience-membership.png)

Om du vill visa målgruppsmedlemskapet för de profiler som är tillgängliga på Edge väljer du **[!UICONTROL Edge]** i dataplatsväljaren. Mer information om kantsegmentering finns i [kantsegmenteringsguiden](../../segmentation/methods/edge-segmentation.md).

![Dataplatsväljaren på fliken för målgruppsmedlemskap är markerad.](../images/user-guide/audience-membership-select.png)

## Sammanfoga profiler

På huvudmenyn **[!UICONTROL Profiles]** väljer du fliken **[!UICONTROL Merge Policies]** för att visa en lista över sammanfogningsprinciper som tillhör din organisation. Varje listad princip visar sitt namn, oavsett om det är standardprincipen för sammanslagning eller inte, och schemaklassen som den gäller för.

Mer information om sammanfogningsprinciper finns i [översikten över sammanfogningsprinciper](../merge-policies/overview.md).

![Fliken Kopplingsprofiler är markerad. Sammanslagningsprinciper som tillhör organisationen visas.](../images/user-guide/merge-policies.png)

## Unionschema {#union-schema}

På huvudmenyn **[!UICONTROL Profiles]** väljer du fliken **[!UICONTROL Union Schema]** för att visa tillgängliga unionsscheman för dina inkapslade data. Ett unionsschema är en sammanslagning av alla [!DNL Experience Data Model] (XDM)-fält under samma klass, vars scheman har aktiverats för användning i [!DNL Real-Time Customer Profile].

Mer information om unionsscheman finns i [gränssnittsguiden för unionsscheman](union-schema.md).

![Fliken Unionens schema är markerad. Unionsscheman som tillhör organisationen visas.](../images/user-guide/union-schema.png)

## Beräknade attribut {#computed-attributes}

Från huvudmenyn **[!UICONTROL Profiles]** väljer du fliken **[!UICONTROL Computed attributes]** för att visa en lista över beräknade attribut som tillhör din organisation.

![Fliken Beräknade attribut är markerad.](../images/user-guide/computed-attributes.png)

För mer information om beräknade attribut, vänligen läs översikten[ över ](../computed-attributes/overview.md)beräknade attribut. För mer information om hur du använder beräknade attribut i Experience Platform UI, vänligen läs guiden[ för ](../computed-attributes/ui.md)UI för beräknade attribut.

## Nästa steg

Genom att läsa denna guide vet du hur du kan se och hantera din organisations profildata med Experience Platform UI. För information om hur du arbetar med profildata med Experience Platform API:er, vänligen se Real-Time Customer Profile API-guiden[](../api/overview.md).
