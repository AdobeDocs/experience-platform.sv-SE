---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API;unified profile;Unified Profile;unified;Profile;rtcp;enable profile;Enable profile;Union schema;UNION PROFILE;union profile
title: Användargränssnittsguide för kundprofiler i realtid
topic: guide
description: Kundprofilen i realtid skapar en helhetsbild av varje enskild kund och kombinerar data från flera kanaler, inklusive online-, offline-, CRM- och tredjepartsdata. Det här dokumentet är en guide för interaktion med kundprofiler i realtid i Adobe Experience Platform användargränssnitt.
translation-type: tm+mt
source-git-commit: 295315ab052ff151bea9037567bf2690d705367b
workflow-type: tm+mt
source-wordcount: '1210'
ht-degree: 0%

---


# [!DNL Real-time Customer Profile] Användargränssnittsguide

[!DNL Real-time Customer Profile] skapar en helhetsbild av var och en av era enskilda kunder och kombinerar data från flera kanaler, inklusive online-, offline-, CRM- och tredjepartsdata. Det här dokumentet är en guide för interaktion med [!DNL Real-time Customer Profile] data i Adobe Experience Platform användargränssnitt.

## Komma igång

Den här gränssnittshandboken kräver förståelse för de olika [!DNL Experience Platform] tjänster som är kopplade till hantering [!DNL Real-time Customer Profiles]. Innan du läser den här handboken eller arbetar i användargränssnittet bör du läsa dokumentationen för följande tjänster:

* [[!DNL Real-time Customer Profile]](../home.md): Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.
* [[!DNL Identity Service]](../../identity-service/home.md): Möjliggör [!DNL Real-time Customer Profile] genom att överbrygga identiteter från olika datakällor när de hämtas till [!DNL Platform].
* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Det standardiserade ramverket som [!DNL Platform] organiserar kundupplevelsedata.

## Översikt

I [[!DNL Experience Platform] användargränssnittet](http://platform.adobe.com)väljer du **[!UICONTROL Profiles]** i den vänstra navigeringen för att öppna **[!UICONTROL Overview]** fliken. På den här fliken finns länkar till dokumentation och videoklipp som hjälper dig att förstå och börja arbeta med profiler.

![](../images/user-guide/profiles-overview.png)

## Bläddra

Välj fliken för att bläddra bland profiler efter identitet. **[!UICONTROL Browse]**

![](../images/user-guide/profiles-browse.png)

### Profilmått {#profile-metrics}

Till höger på **[!UICONTROL Browse]** fliken finns flera viktiga mätvärden för dina profildata, inklusive det totala [profilantalet](#profile-count) samt en lista över [profiler per namnutrymme](#profiles-by-namespace).

Dessa profilvärden utvärderas med organisationens standardpolicy för sammanfogning. Mer information om hur du arbetar med sammanfogningsprinciper, inklusive hur du definierar en standardsammanfogningsprincip, finns i användarhandboken för [sammanfogningsprinciper](merge-policies.md).

Förutom dessa mått innehåller profilmätningsavsnittet även ett senast uppdaterat datum och en uppdaterad tid, som visar när mätvärdena senast utvärderades.

![](../images/user-guide/profiles-profile-metrics.png)

### Profilantal {#profile-count}

Profilantalet visar det totala antalet profiler som din organisation har i [!DNL Experience Platform], efter att din organisations standardpolicy för sammanfogning har sammanfogat profilfragment till en enda profil för varje enskild kund. Med andra ord kan din organisation ha flera profilfragment kopplade till en enskild kund som interagerar med ert varumärke i olika kanaler, men dessa fragment skulle slås samman (enligt standardprincipen för sammanslagning) och skulle returnera antalet&quot;1&quot;-profil eftersom de alla är kopplade till samma individ.

Profilantalet omfattar även både profiler med attribut (postdata) och profiler som endast innehåller tidsseriedata (händelsedata), t.ex. Adobe Analytics-profiler. Profilantalet uppdateras regelbundet för att ge ett aktuellt totalt antal profiler inom plattformen.

När inmatningen av poster i [!DNL Profile] butiken ökar eller minskar antalet med mer än 5 %, utlöses ett jobb för att uppdatera antalet. För arbetsflöden med direktuppspelningsdata görs en timkontroll för att avgöra om tröskelvärdet på 5 % har uppnåtts eller ej. Om så är fallet utlöses ett jobb automatiskt för att uppdatera antalet profiler. Om tröskelvärdet på 5 % ökning eller minskning är uppfyllt, körs ett jobb för att uppdatera profilantalet för batchintag inom 15 minuter efter att en batch har importerats till profilbutiken.

### Profiler efter namnområde {#profiles-by-namespace}

I måttet visas det totala antalet och den totala uppdelningen av namnutrymmen för alla sammanfogade profiler i din profilbutik. **[!UICONTROL Profiles by namespace]** Det totala antalet profiler per namnutrymme (med andra ord, om de värden som visas för varje namnutrymme läggs ihop) kommer alltid att vara högre än det för antalet profiler, eftersom en profil kan ha flera namnutrymmen kopplade till sig. Om en kund till exempel interagerar med varumärket i mer än en kanal kommer flera namnutrymmen att kopplas till den enskilda kunden.

Ungefär som [profilräknemeterialet](#profile-count) , utlöses ett jobb för att uppdatera namnområdesmåtten när inmatningen av poster i [!DNL Profile] butiken ökar eller minskar antalet med mer än 5 %. För arbetsflöden med direktuppspelningsdata görs en timkontroll för att avgöra om tröskelvärdet på 5 % har uppnåtts eller ej. Om så är fallet utlöses ett jobb automatiskt för att uppdatera antalet profiler. Om tröskelvärdet på 5 % ökning eller minskning uppnås kommer ett jobb att köras för att uppdatera mätvärdena för batchförbrukning inom 15 minuter efter att en batch har importerats till [!DNL Profile] butiken.

### Kopplingsprincip

Väljaren väljer automatiskt **[!UICONTROL Merge policy]** standardprincip för sammanslagning för din organisation. Om du inte vill använda den sammanfogningsprincipen kan du välja `X` bredvid standardsammanfogningsprincipen för att öppna **[!UICONTROL Select merge policy]** dialogrutan där du kan välja en annan sammanfogningsprincip. Mer information om kopplingsprofiler och deras roll inom plattformen finns i [användargränssnittshandboken](merge-policies.md)för kopplingsprofiler.

![](../images/user-guide/profiles-search-merge-policy.png)

### Namnutrymme för identitet

Väljaren öppnar en dialogruta där du kan välja det identitetsnamnutrymme som du vill söka efter, och du kan anpassa de attribut som visas i sökningen genom att markera filterikonen och välja vilka attribut du vill lägga till eller ta bort. **[!UICONTROL Identity namespace]**

![](../images/user-guide/profiles-search-filter.png)

I **[!UICONTROL Select identity namespace]** dialogrutan väljer du det namnutrymme som du vill söka efter, eller använder sökfältet i dialogrutan för att skriva namnet på ett namnutrymme. Du kan markera ett namnutrymme om du vill visa mer information, och när du har hittat namnutrymmet kan du markera alternativknappen och trycka på **[!UICONTROL Select]** för att fortsätta.

![](../images/user-guide/profiles-select-identity-namespace.png)

### Identitetsvärde

När du har valt ett identitetsnamnutrymme återgår du till den **[!UICONTROL Browse]** flik där du kan ange ett **[!UICONTROL Identity value]**. Det här värdet är specifikt för en enskild kundprofil och måste vara en giltig post för det angivna namnutrymmet. Om du t.ex. väljer identitetsnamnet&quot;E-post&quot; krävs ett identitetsvärde i form av en giltig e-postadress.

![](../images/user-guide/profiles-show-profile.png)

När ett värde har angetts, väljer du **[!UICONTROL Show profile]** och returnerar en enda profil som matchar värdet. Välj det här alternativet om du **[!UICONTROL Profile ID]** vill visa profilinformationen.

![](../images/user-guide/profiles-display-profile.png)

### Profilinformation {#profile-detail}

När du väljer **[!UICONTROL Profile ID]**&#x200B;öppnas **[!UICONTROL Detail]** fliken. Profilinformationen som visas på **[!UICONTROL Detail]** fliken har sammanfogats från flera profilfragment till en enda vy över den enskilda kunden. Detta inkluderar kundinformation som grundläggande attribut, länkade identiteter och kanalinställningar. Standardfälten som visas kan också ändras på organisationsnivå för att visa de önskade profilattributen. Om du vill veta mer om hur du anpassar de här fälten, inklusive stegvisa instruktioner för hur du lägger till och tar bort attribut och ändrar storlek på kontrollpaneler, läser du [anpassningsguiden](profile-customization.md)för profildetaljer.

![](../images/user-guide/profiles-profile-detail.png)

Du kan visa ytterligare information om den enskilda profilen genom att välja en annan av de tillgängliga flikarna. Dessa flikar innehåller attribut, händelser och segmentmedlemskap, som visar de segment som profilen är kvalificerad för just nu.

![](../images/user-guide/profiles-attributes-events-segments.png)

## Sammanfoga profiler

På huvudmenyn **[!UICONTROL Profiles]** väljer du **[!UICONTROL Merge Policies]** fliken för att visa en lista över sammanfogningsprinciper som tillhör organisationen. Varje listad princip visar sitt namn, oavsett om det är standardprincipen för sammanslagning eller inte, och schemaklassen som den gäller för.

Mer information om sammanfogningsprinciper finns i [användargränssnittshandboken](merge-policies.md)för sammanfogningsprinciper.

![](../images/user-guide/profiles-merge-policies.png)

## Unionsschema {#union-schema}

På huvudmenyn **[!UICONTROL Profiles]** väljer du **[!UICONTROL Union Schema]** fliken för att visa föreningsscheman för dina inkapslade data. Ett unionsschema är en kombination av alla [!DNL Experience Data Model] (XDM) fält under samma klass, vars scheman har aktiverats för användning i [!DNL Real-time Customer Profile].

Mer information om unionsscheman finns i användargränssnittshandboken för [unionsscheman](union-schema.md).

![](../images/user-guide/profiles-union-schema.png)

## Nästa steg

Genom att läsa den här guiden kan du nu visa och hantera dina [!DNL Profile] data med hjälp av [!DNL Experience Platform] användargränssnittet. Mer information om hur du arbetar med profildata med hjälp av kundprofils-API:t i realtid finns i [profilutvecklarhandboken](../api/overview.md).