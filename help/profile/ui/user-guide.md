---
keywords: Experience Platform;profil;kundprofil i realtid;felsökning;API;enhetlig profil;Enhetlig profil;Enhetlig;Profil;rtcp;aktivera profil;Aktivera profil;Unionsschema;UNIONSPROFIL;unionsprofil
title: Användargränssnittshandbok för kundprofil i realtid
description: Kundprofilen i realtid skapar en helhetsbild av varje enskild kund och kombinerar data från flera kanaler, inklusive online-, offline-, CRM- och tredjepartsdata. Det här dokumentet är en guide för interaktion med kundprofilen i realtid i Adobe Experience Platform användargränssnitt.
exl-id: 792a3a73-58a4-4163-9212-4d43d24c2770
source-git-commit: 4afb2c76f2022423e8f1fa29c91d02b43447ba90
workflow-type: tm+mt
source-wordcount: '2128'
ht-degree: 0%

---

# Användargränssnittshandbok för [!DNL Real-Time Customer Profile]

[!DNL Real-Time Customer Profile] skapar en helhetsbild av varje enskild kund och kombinerar data från flera kanaler, inklusive online-, offline-, CRM- och tredjepartsdata. Det här dokumentet fungerar som en guide för interaktion med [!DNL Real-Time Customer Profile]-data i Adobe Experience Platform användargränssnitt.

## Komma igång

Den här gränssnittshandboken kräver förståelse för de olika [!DNL Experience Platform]-tjänsterna som används för att hantera [!DNL Real-Time Customer Profiles]. Innan du läser den här handboken eller arbetar i användargränssnittet bör du läsa dokumentationen för följande tjänster:

* [[!DNL Real-Time Customer Profile] översikt](../home.md): Tillhandahåller en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.
* [[!DNL Identity Service]](../../identity-service/home.md): Aktiverar [!DNL Real-Time Customer Profile] genom att brygga identiteter från olika datakällor när de hämtas till [!DNL Platform].
* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Det standardiserade ramverket som [!DNL Platform] organiserar kundupplevelsedata med.

## [!UICONTROL Overview]

I Experience Platform-gränssnittet väljer du **[!UICONTROL Profiles]** i den vänstra navigeringen för att öppna fliken **[!UICONTROL Overview]** med profilkontrollpanelen.

>[!NOTE]
>
>Om din organisation är ny på Platform och ännu inte har aktiva profildatauppsättningar eller sammanslagningsprinciper skapade, visas inte instrumentpanelen [!UICONTROL Profiles]. Istället visar fliken [!UICONTROL Overview] länkar och dokumentation som hjälper dig att komma igång med kundprofilen i realtid.

### Kontrollpanel för profil {#profile-dashboard}

På profilkontrollpanelen visas viktiga mätvärden för din organisations profildata.

Mer information finns i [profilkontrollpanelsguiden](../../dashboards/guides/profiles.md).

![Kontrollpanelen för profiler visas.](../../dashboards/images/profiles/dashboard-overview.png)

## [!UICONTROL Browse] tabbvärden

Välj fliken **[!UICONTROL Browse]** om du vill visa flera mätvärden som är relaterade till din organisations profildata. Du kan även använda den här fliken för att bläddra i profilarkivet med hjälp av en sammanfogningsprincip eller en identitet, vilket beskrivs i nästa avsnitt i den här handboken.

Till höger på fliken **[!UICONTROL Browse]** finns antalet [-profiler](#profile-count) samt en lista över [profiler per namnområde](#profiles-by-namespace).

>[!NOTE]
>
>Profilmåtten kan skilja sig från måtten som visas på [profilkontrollpanelen](#profile-dashboard) eftersom de utvärderas med organisationens standardsammanfogningsprincip. Mer information om hur du arbetar med sammanfogningsprinciper, inklusive hur du definierar en standardsammanfogningsprincip, finns i [översikten över sammanfogningsprinciper](../merge-policies/overview.md).

Förutom dessa mått innehåller det här avsnittet ett senaste uppdaterat datum och tid som visar när mätvärdena senast utvärderades.

![Profilmåtten visas och markeras.](../images/user-guide/browse-metrics.png)

### Profilantal {#profile-count}

Profilantalet visar det totala antalet profiler som din organisation har inom Experience Platform, efter att organisationens standardpolicy för sammanslagning har sammanfogats med profilfragment för att bilda en enda profil för varje enskild kund. Med andra ord kan din organisation ha flera profilfragment kopplade till en enskild kund som interagerar med ert varumärke i olika kanaler, men dessa fragment skulle slås samman (enligt standardprincipen för sammanslagning) och skulle returnera antalet&quot;1&quot;-profil eftersom de alla är kopplade till samma individ.

Profilantalet omfattar även både profiler med attribut (postdata) och profiler som endast innehåller tidsseriedata (händelsedata), t.ex. Adobe Analytics-profiler. Profilantalet uppdateras regelbundet för att ge ett aktuellt totalt antal profiler inom plattformen.

#### Uppdaterar måttet för antal profiler

När inmatningen av poster i arkivet [!DNL Profile] ökar eller minskar antalet med mer än 5 %, utlöses ett jobb för att uppdatera antalet. För arbetsflöden med direktuppspelningsdata görs en timkontroll för att avgöra om tröskelvärdet på 5 % har uppnåtts eller ej. Om så är fallet utlöses ett jobb automatiskt för att uppdatera antalet profiler. Om tröskelvärdet på 5 % ökning eller minskning är uppfyllt, körs ett jobb för att uppdatera profilantalet för batchintag inom 15 minuter efter att en batch har importerats till profilbutiken.

### [!UICONTROL Profiles by namespace] {#profiles-by-namespace}

Måttet **[!UICONTROL Profiles by namespace]** visar det totala antalet och uppdelningen av namnutrymmen i alla sammanfogade profiler i profilarkivet. Det totala antalet profiler per namnutrymme (med andra ord, om de värden som visas för varje namnutrymme läggs ihop) kommer alltid att vara högre än det för antalet profiler, eftersom en profil kan ha flera namnutrymmen kopplade till sig. Om en kund till exempel interagerar med varumärket i mer än en kanal kommer flera namnutrymmen att kopplas till den enskilda kunden.

#### Uppdaterar måttet [!UICONTROL Profiles by namespace]

Ungefär som måttet [profile count](#profile-count) , när inmatningen av poster i arkivet [!DNL Profile] ökar eller minskar antalet med mer än 5 %, utlöses ett jobb för att uppdatera namnutrymmesmåtten. För arbetsflöden med direktuppspelningsdata görs en timkontroll för att avgöra om tröskelvärdet på 5 % har uppnåtts eller ej. Om så är fallet utlöses ett jobb automatiskt för att uppdatera antalet profiler. Om tröskelvärdet på 5 % ökning eller minskning uppnås körs ett jobb för att uppdatera måtten för batchförbrukning inom 15 minuter efter att en batch har importerats till [!DNL Profile]-butiken.

## Använd fliken [!UICONTROL Browse] för att visa profiler

På fliken **[!UICONTROL Browse]** kan du visa exempelprofiler med hjälp av en sammanfogningsprincip eller leta upp specifika profiler med hjälp av ett ID-namnutrymme och värde.

![Profilerna som tillhör organisationen visas.](../images/user-guide/none-selected.png)

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

![Exempelprofiler som matchar sammanfogningsprincipen visas.](../images/user-guide/sample-profiles.png)

Mer information om sammanfogningsprinciper och deras roll inom plattformen finns i [översikten över sammanfogningsprinciper](../merge-policies/overview.md).

### Bläddra efter [!UICONTROL Identity] {#browse-identity}

På fliken **[!UICONTROL Browse]** kan du använda ett ID-namnutrymme för att söka efter en viss profil med hjälp av ett identitetsvärde. Om du bläddrar efter en identitet måste du ange en sammanfogningsprincip, ett identitetsnamnutrymme och ett identitetsvärde.

![Väljaren för sammanfogningsprincip är markerad.](../images/user-guide/browse-by-merge-policy.png)

Om det behövs kan du använda väljaren **[!UICONTROL Merge policy]** för att öppna dialogrutan **[!UICONTROL Select merge policy]** och välja den sammanfogningsprincip som du vill använda.

![En dialogruta där du kan välja vilken sammanfogningsprincip som ska filtreras efter visas.](../images/user-guide/select-merge-policy.png)

Använd sedan väljaren **[!UICONTROL Identity namespace]** för att öppna dialogrutan **[!UICONTROL Select identity namespace]** och välj det namnutrymme som du vill söka efter. Om din organisation har många namnutrymmen kan du använda sökfältet i dialogrutan för att börja skriva namnet på ett namnutrymme.

Du kan markera ett namnutrymme om du vill visa mer information eller välja ett namnutrymme genom att markera alternativknappen. Du kan sedan använda **[!UICONTROL Select]** för att fortsätta.

![En dialogruta där du kan välja det identitetsnamnutrymme som ska filtreras visas.](../images/user-guide/select-identity-namespace.png)

När du har valt en [!UICONTROL Identity namespace] och återgår till fliken [!UICONTROL Browse] kan du ange en **[!UICONTROL Identity value]** som är relaterad till det markerade namnutrymmet.

>[!NOTE]
>
>Det här värdet är specifikt för en enskild kundprofil och måste vara en giltig post för det angivna namnutrymmet. Om du t.ex. väljer identitetsnamnet&quot;E-post&quot; krävs ett identitetsvärde i form av en giltig e-postadress.

![Identitetsvärdet som du vill filtrera efter är markerat.](../images/user-guide/filter-identity-value.png)

När ett värde har angetts väljer du **[!UICONTROL View]** och en enda profil som matchar värdet returneras. Välj **[!UICONTROL Profile ID]** om du vill visa profilinformationen.

![Profilen som matchar identitetsvärdet markeras.](../images/user-guide/filtered-identity-value.png)

## Visa profilinformation {#profile-detail}

>[!CONTEXTUALHELP]
>id="platform_errors_uplib_201001_404"
>title="Enheten hittades inte"
>abstract="Detta innebär att plattformen inte kunde hitta den begärda entiteten. Försök med någon av följande lösningar för att åtgärda felet:<ul><li>Kontrollera att rätt profil-ID finns i URL:en för den entitet du försöker få åtkomst till.</li><li>Kontrollera att du har rätt kombination av organisation och sandlåda för den enhet du försöker få åtkomst till.</li></ul>"

När du har valt **[!UICONTROL Profile ID]** öppnas fliken **[!UICONTROL Detail]**. Profilinformationen som visas på fliken **[!UICONTROL Detail]** har sammanfogats från flera profilfragment till en enda vy över den enskilda kunden. Detta inkluderar kundinformation som grundläggande attribut, länkade identiteter och kanalinställningar.

Standardfälten som visas kan också ändras på organisationsnivå för att visa de önskade profilattributen. Om du vill veta mer om hur du anpassar de här fälten, inklusive steg-för-steg-instruktioner om hur du lägger till och tar bort attribut och ändrar storlek på kontrollpaneler, kan du läsa [anpassningsguiden för profildetaljer](profile-customization.md).

![Fliken Detaljer är markerad. Profilinformationen visas.](../images/user-guide/profile-detail-row-name.png)

Du kan också växla mellan att visa attributnamnen som visningsnamn och fältsökvägsnamn. Om du vill växla mellan dessa två skärmar väljer du alternativet **[!UICONTROL Show display names]**.

![Växlingen Visa visningsnamn är markerad och visningsnamnen visas under attributen.](../images/user-guide/profile-detail.png)

Om du vill visa ytterligare information om den enskilda kundprofilen väljer du någon av de andra tillgängliga flikarna. Dessa flikar innehåller attribut, händelser och fliken för målgruppsmedlemskap som visar vilka målgrupper profilen är kvalificerad för.

### Fliken Attribut

Fliken **[!UICONTROL Attributes]** innehåller en listvy med en sammanfattning av alla attribut som hör till en enskild profil, efter att den angivna sammanfogningsprincipen har tillämpats.

Dessa attribut kan också visas som ett JSON-objekt genom att välja till **[!UICONTROL View JSON]**. Detta är praktiskt för alla användare som bättre vill förstå hur profilattributen hämtas till Platform.

![Fliken Attribut är markerad. Profilattributen visas.](../images/user-guide/attributes.png)

Om du vill visa de attribut som är tillgängliga på Edge väljer du **[!UICONTROL Edge]** i dataplatsväljaren.

![Dataplatsväljaren på fliken Attribut är markerad.](../images/user-guide/attributes-select.png)

Mer information om kantprofiler finns i [dokumentationen för kantprofiler](../edge-profiles.md).

### Fliken Händelser

Fliken **[!UICONTROL Events]** innehåller data från de 100 senaste ExperienceEvents som är associerade med kunden. Dessa data kan inkludera öppning av e-post, kundvagnsaktiviteter och sidvyer. Om du väljer **[!UICONTROL View all]** för en enskild händelse hämtas ytterligare fält och värden som en del av händelsen.

Händelser kan också visas som ett JSON-objekt genom att välja till **[!UICONTROL View JSON]**. Detta är praktiskt när du vill veta hur händelser hämtas i Platform.

![Fliken Händelser är markerad. Profilhändelserna visas.](../images/user-guide/events.png)

### Fliken Målgruppsmedlemskap

Fliken **[!UICONTROL Audience membership]** visar en lista med namn och beskrivning av målgrupper som den enskilda kundprofilen för närvarande tillhör. Listan uppdateras automatiskt när profilen kvalificerar sig eller upphör att gälla. Det totala antalet målgrupper som profilen är kvalificerad för visas till höger på fliken.

Mer information om segmentering i Experience Platform finns i [dokumentationen för Experience Platform segmenteringstjänst](../../segmentation/home.md).

![Fliken Målgruppsmedlemskap är markerad. Profilens medlemsinformation visas.](../images/user-guide/audience-membership.png)

Om du vill visa målgruppsmedlemskapet för de profiler som är tillgängliga på Edge väljer du **[!UICONTROL Edge]** i dataplatsväljaren. Mer information om kantsegmentering finns i [kantsegmenteringsguiden](../../segmentation/methods/edge-segmentation.md).

![Dataplatsväljaren på fliken för målgruppsmedlemskap är markerad.](../images/user-guide/audience-membership-select.png)

## Sammanfoga profiler

På huvudmenyn **[!UICONTROL Profiles]** väljer du fliken **[!UICONTROL Merge Policies]** för att visa en lista över sammanfogningsprinciper som tillhör din organisation. Varje listad princip visar sitt namn, oavsett om det är standardprincipen för sammanslagning eller inte, och schemaklassen som den gäller för.

Mer information om sammanfogningsprinciper finns i [översikten över sammanfogningsprinciper](../merge-policies/overview.md).

![Fliken Kopplingsprofiler är markerad. Sammanslagningsprinciper som tillhör organisationen visas.](../images/user-guide/merge-policies.png)

## Unionsschema {#union-schema}

På huvudmenyn **[!UICONTROL Profiles]** väljer du fliken **[!UICONTROL Union Schema]** för att visa tillgängliga unionsscheman för dina inkapslade data. Ett unionsschema är en sammanslagning av alla [!DNL Experience Data Model] (XDM)-fält under samma klass, vars scheman har aktiverats för användning i [!DNL Real-Time Customer Profile].

Mer information om unionsscheman finns i [gränssnittsguiden för unionsscheman](union-schema.md).

![Fliken Unionens schema är markerad. Unionsscheman som tillhör organisationen visas.](../images/user-guide/union-schema.png)

## Beräknade attribut {#computed-attributes}

På huvudmenyn **[!UICONTROL Profiles]** väljer du fliken **[!UICONTROL Computed attributes]** för att visa en lista över beräknade attribut som tillhör din organisation.

![Fliken Beräknade attribut är markerad.](../images/user-guide/computed-attributes.png)

Mer information om beräknade attribut finns i [översikten över beräknade attribut](../computed-attributes/overview.md). Mer information om hur du använder beräknade attribut i plattformsgränssnittet finns i [användargränssnittshandboken för beräknade attribut](../computed-attributes/ui.md).

## Nästa steg

Genom att läsa den här guiden kan du visa och hantera din organisations profildata med hjälp av Experience Platform användargränssnitt. Mer information om hur du arbetar med profildata med Experience Platform API:er finns i [API-handboken för kundprofiler i realtid](../api/overview.md).
