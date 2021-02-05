---
keywords: Experience Platform;profil;kundprofil i realtid;felsökning;API;enhetlig profil;Enhetlig profil;Enhetlig;Profil;rtcp;aktivera profil;Aktivera profil;Unionsschema;UNIONSPROFIL;unionsprofil
title: Användargränssnittshandbok för kundprofil i realtid
topic: guide
description: Kundprofilen i realtid skapar en helhetsbild av varje enskild kund och kombinerar data från flera kanaler, inklusive online-, offline-, CRM- och tredjepartsdata. Det här dokumentet är en guide för interaktion med kundprofiler i realtid i Adobe Experience Platform användargränssnitt.
translation-type: tm+mt
source-git-commit: cad9c690be986961aea2969ef0ade975f33a8ee5
workflow-type: tm+mt
source-wordcount: '1315'
ht-degree: 0%

---


# [!DNL Real-time Customer Profile] Användargränssnittsguide

[!DNL Real-time Customer Profile] skapar en helhetsbild av var och en av era enskilda kunder och kombinerar data från flera kanaler, inklusive online-, offline-, CRM- och tredjepartsdata. Det här dokumentet fungerar som en guide för interaktion med [!DNL Real-time Customer Profile]-data i Adobe Experience Platform användargränssnitt.

## Komma igång

Användargränssnittshandboken kräver förståelse för de olika [!DNL Experience Platform]-tjänsterna som används för att hantera [!DNL Real-time Customer Profiles]. Innan du läser den här handboken eller arbetar i användargränssnittet bör du läsa dokumentationen för följande tjänster:

* [[!DNL Real-time Customer Profile]](../home.md): Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.
* [[!DNL Identity Service]](../../identity-service/home.md): Möjliggör  [!DNL Real-time Customer Profile] genom att överbrygga identiteter från olika datakällor när de hämtas till  [!DNL Platform].
* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Det standardiserade ramverket som  [!DNL Platform] organiserar kundupplevelsedata.

## Översikt

I användargränssnittet för Experience Platform väljer du **[!UICONTROL Profiles]** i den vänstra navigeringen för att öppna fliken **[!UICONTROL Overview]**. På den här fliken finns länkar till dokumentation och videoklipp som hjälper dig att förstå och börja arbeta med profiler.

![](../images/user-guide/profiles-overview.png)

### (Alfa) Kontrollpanel för profil

>[!IMPORTANT]
>
>Instrumentpanelsfunktionen är för närvarande alfavärden och är inte tillgänglig för alla användare. Dokumentationen och funktionaliteten kan komma att ändras.

För vissa användare kan du välja **[!UICONTROL Profiles]** i den vänstra navigeringen och öppna fliken **[!UICONTROL Overview]** och visa en instrumentpanel med nyckelvärden relaterade till dina profildata.

Mer information finns i [guiden för profilkontrollpanelen](profile-dashboard.md).

## Bläddra

Välj fliken **[!UICONTROL Browse]** om du vill bläddra bland profiler efter identitet.

![](../images/user-guide/profiles-browse.png)

### Profilmått {#profile-metrics}

Till höger på fliken **[!UICONTROL Browse]** finns flera viktiga mätvärden som relaterar till dina profildata, inklusive det totala [profilantalet](#profile-count) och en lista över [profiler efter namnområde](#profiles-by-namespace).

Dessa profilvärden utvärderas med organisationens standardpolicy för sammanfogning. Mer information om hur du arbetar med sammanfogningsprinciper, inklusive hur du definierar en standardsammanfogningsprincip, finns i [användarhandboken för sammanfogningsprinciper](merge-policies.md).

Förutom dessa mått innehåller profilmätningsavsnittet även ett senast uppdaterat datum och en uppdaterad tid, som visar när mätvärdena senast utvärderades.

![](../images/user-guide/profiles-profile-metrics.png)

### Profilantal {#profile-count}

Profilantalet visar det totala antalet profiler som din organisation har inom [!DNL Experience Platform], efter att organisationens standardpolicy för sammanfogning har sammanfogats med profilfragment för att bilda en enda profil för varje enskild kund. Med andra ord kan din organisation ha flera profilfragment kopplade till en enskild kund som interagerar med ert varumärke i olika kanaler, men dessa fragment skulle slås samman (enligt standardprincipen för sammanslagning) och skulle returnera antalet&quot;1&quot;-profil eftersom de alla är kopplade till samma individ.

Profilantalet omfattar även både profiler med attribut (postdata) och profiler som endast innehåller tidsseriedata (händelsedata), t.ex. Adobe Analytics-profiler. Profilantalet uppdateras regelbundet för att ge ett aktuellt totalt antal profiler inom plattformen.

När inmatningen av poster i [!DNL Profile]-butiken ökar eller minskar antalet med mer än 5 %, utlöses ett jobb för att uppdatera antalet. För arbetsflöden med direktuppspelningsdata görs en timkontroll för att avgöra om tröskelvärdet på 5 % har uppnåtts eller ej. Om så är fallet utlöses ett jobb automatiskt för att uppdatera antalet profiler. Om tröskelvärdet på 5 % ökning eller minskning är uppfyllt, körs ett jobb för att uppdatera profilantalet för batchintag inom 15 minuter efter att en batch har importerats till profilbutiken.

### Profiler efter namnområde {#profiles-by-namespace}

Måttet **[!UICONTROL Profiles by namespace]** visar totalt antal och uppdelning av namnutrymmen för alla sammanfogade profiler i din profilbutik. Det totala antalet profiler per namnutrymme (med andra ord, om de värden som visas för varje namnutrymme läggs ihop) kommer alltid att vara högre än det för antalet profiler, eftersom en profil kan ha flera namnutrymmen kopplade till sig. Om en kund till exempel interagerar med varumärket i mer än en kanal kommer flera namnutrymmen att kopplas till den enskilda kunden.

Ungefär som [profilantalet](#profile-count), när inmatningen av poster i [!DNL Profile]-arkivet ökar eller minskar antalet med mer än 5 %, utlöses ett jobb för att uppdatera namnutrymmesmåtten. För arbetsflöden med direktuppspelningsdata görs en timkontroll för att avgöra om tröskelvärdet på 5 % har uppnåtts eller ej. Om så är fallet utlöses ett jobb automatiskt för att uppdatera antalet profiler. Om tröskelvärdet på 5 % ökning eller minskning uppnås körs ett jobb för att uppdatera mätvärdena för batchförbrukning inom 15 minuter efter att en batch har importerats till [!DNL Profile]-butiken.

### Kopplingsprincip

Väljaren **[!UICONTROL Merge policy]** väljer automatiskt standardprincip för sammanslagning för din organisation. Om du inte vill använda den sammanfogningsprincipen kan du välja `X` bredvid standardsammanfogningsprincipen för att öppna dialogrutan **[!UICONTROL Select merge policy]** där du kan välja en annan sammanfogningsprincip.

Mer information om kopplingsprofiler och deras roll inom plattformen finns i [användargränssnittshandboken för kopplingsprofiler](merge-policies.md).

![](../images/user-guide/profiles-search-merge-policy.png)

### Namnutrymme för identitet

Väljaren **[!UICONTROL Identity namespace]** öppnar en dialogruta där du kan välja det identitetsnamnutrymme som du vill söka efter, och du kan anpassa de attribut som visas i sökningen genom att markera filterikonen och välja vilka attribut du vill lägga till eller ta bort.

![](../images/user-guide/profiles-search-filter.png)

I dialogrutan **[!UICONTROL Select identity namespace]** väljer du det namnutrymme som du vill söka efter, eller använder sökfältet i dialogrutan för att skriva namnet på ett namnutrymme. Du kan markera ett namnutrymme om du vill visa mer information, och när du har hittat det namnutrymme du vill använda kan du markera alternativknappen och trycka på **[!UICONTROL Select]** för att fortsätta.

![](../images/user-guide/profiles-select-identity-namespace.png)

### Identitetsvärde

När du har valt ett identitetsnamnutrymme återgår du till fliken **[!UICONTROL Browse]** där du kan ange ett **[!UICONTROL Identity value]**. Det här värdet är specifikt för en enskild kundprofil och måste vara en giltig post för det angivna namnutrymmet. Om du t.ex. väljer identitetsnamnet&quot;E-post&quot; krävs ett identitetsvärde i form av en giltig e-postadress.

![](../images/user-guide/profiles-show-profile.png)

När ett värde har angetts väljer du **[!UICONTROL Show profile]** och en enda profil som matchar värdet returneras. Välj **[!UICONTROL Profile ID]** för att visa profilinformationen.

![](../images/user-guide/profiles-display-profile.png)

### Profilinformation {#profile-detail}

När du väljer **[!UICONTROL Profile ID]** öppnas fliken **[!UICONTROL Detail]**. Profilinformationen som visas på fliken **[!UICONTROL Detail]** har sammanfogats från flera profilfragment till en enda vy över den enskilda kunden. Detta inkluderar kundinformation som grundläggande attribut, länkade identiteter och kanalinställningar. Standardfälten som visas kan också ändras på organisationsnivå för att visa de önskade profilattributen. Om du vill veta mer om hur du anpassar de här fälten, inklusive stegvisa instruktioner för att lägga till och ta bort attribut och ändra storlek på kontrollpaneler, läser du [anpassningsguiden för profildetaljer](profile-customization.md).

![](../images/user-guide/profiles-profile-detail.png)

Du kan visa ytterligare information om den enskilda profilen genom att välja en annan av de tillgängliga flikarna. Dessa flikar innehåller attribut, händelser och segmentmedlemskap, som visar de segment som profilen är kvalificerad för just nu.

![](../images/user-guide/profiles-attributes-events-segments.png)

## Sammanfoga profiler

På huvudmenyn **[!UICONTROL Profiles]** väljer du fliken **[!UICONTROL Merge Policies]** för att visa en lista över sammanfogningsprinciper som tillhör din organisation. Varje listad princip visar sitt namn, oavsett om det är standardprincipen för sammanslagning eller inte, och schemaklassen som den gäller för.

Mer information om sammanfogningsprinciper finns i [användargränssnittshandboken för sammanfogningsprinciper](merge-policies.md).

Mer information om hur du arbetar med sammanfogningspolicyer med API:t för kundprofil i realtid finns i [slutpunktshandboken för sammanfogningspolicyer](../api/merge-policies.md).

![](../images/user-guide/profiles-merge-policies.png)

## Unionsschema {#union-schema}

På huvudmenyn **[!UICONTROL Profiles]** väljer du fliken **[!UICONTROL Union Schema]** för att visa tillgängliga unionsscheman för dina inkapslade data. Ett unionsschema är en sammanslagning av alla [!DNL Experience Data Model] (XDM)-fält under samma klass, vars scheman har aktiverats för användning i [!DNL Real-time Customer Profile].

Mer information om unionsscheman finns i [gränssnittsguiden för unionsscheman](union-schema.md).

![](../images/user-guide/profiles-union-schema.png)

## Nästa steg

Genom att läsa den här guiden kan du nu visa och hantera dina [!DNL Profile]-data med hjälp av användargränssnittet i [!DNL Experience Platform]. Mer information om hur du arbetar med profildata med hjälp av kundprofils-API:t i realtid finns i [Profilutvecklarhandboken](../api/overview.md).