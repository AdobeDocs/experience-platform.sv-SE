---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: Användarhandbok för kundprofil i realtid
topic: guide
translation-type: tm+mt
source-git-commit: 59dff7687f8a0c5b5084eb1ce7dd222cc18d8dbf
workflow-type: tm+mt
source-wordcount: '1208'
ht-degree: 0%

---


# Användarhandbok för kundprofil i realtid

Kundprofilen i realtid skapar en helhetsbild av varje enskild kund och kombinerar data från flera kanaler, inklusive online-, offline-, CRM- och tredjepartsdata.

Det här dokumentet är en guide för interaktion med kundprofilen i realtid i användargränssnittet i Adobe Experience Platform.

## Komma igång

Den här användarhandboken kräver förståelse för de olika Experience Platform-tjänster som används för att hantera kundprofiler i realtid. Innan du läser den här användarhandboken bör du läsa dokumentationen för följande tjänster:

* [Kundprofil](../home.md)i realtid: Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.
* [Identitetstjänst](../../identity-service/home.md): Möjliggör kundprofil i realtid genom att överbrygga identiteter från olika datakällor när de hämtas till Platform.
* [Experience Data Model (XDM)](../../xdm/home.md): Det standardiserade ramverk som Platform använder för att ordna kundupplevelsedata.

## Översikt

Klicka på [Profiler](http://platform.adobe.com)i den vänstra navigeringen i **Experience Platform-gränssnittet** för att öppna fliken _Översikt_ . På den här fliken finns länkar till dokumentation och videoklipp som hjälper dig att förstå och börja arbeta med profiler.

![](../images/user-guide/profiles-overview.png)

## Bläddra

Välj fliken *Bläddra* för att bläddra bland profiler efter identitet.

![](../images/user-guide/profiles-browse.png)

### Profilmått {#profile-metrics}

Till höger på fliken *Bläddra* finns flera viktiga mätvärden som rör dina profildata, bland annat det totala [profilantalet](#profile-count) och en lista över [profiler per namnutrymme](#profiles-by-namespace).

Dessa profilvärden utvärderas med organisationens standardpolicy för sammanfogning. Mer information om hur du arbetar med sammanfogningsprinciper, inklusive hur du definierar en standardsammanfogningsprincip, finns i användarhandboken för [sammanfogningsprinciper](merge-policies.md).

Förutom dessa mått innehåller avsnittet Profilmått även ett *senast uppdaterat* datum och tid som visar när mätvärdena senast utvärderades.

![](../images/user-guide/profiles-profile-metrics.png)

### Profilantal {#profile-count}

Profilantalet visar det totala antalet profiler som din organisation har i Experience Platform, efter att organisationens standardpolicy för sammanfogning har sammanfogats med profilfragment för att bilda en enda profil för varje enskild kund. Med andra ord kan din organisation ha flera profilfragment kopplade till en enskild kund som interagerar med ert varumärke i olika kanaler, men dessa fragment skulle slås samman (enligt standardprincipen för sammanslagning) och skulle returnera antalet&quot;1&quot;-profil eftersom de alla är kopplade till samma individ.

Profilantalet omfattar även både profiler med attribut (postdata) och profiler som endast innehåller tidsseriedata (händelsedata), t.ex. Adobe Analytics-profiler. Profilantalet uppdateras regelbundet för att ge ett aktuellt totalt antal profiler i Platform.

När intaget av poster i profilarkivet ökar eller minskar antalet med mer än 5 %, utlöses ett jobb för att uppdatera antalet. För arbetsflöden med direktuppspelningsdata görs en timkontroll för att avgöra om tröskelvärdet på 5 % har uppnåtts eller ej. Om så är fallet utlöses ett jobb automatiskt för att uppdatera antalet profiler. Om tröskelvärdet på 5 % ökning eller minskning uppnås, körs ett jobb för att uppdatera profilantalet för batchintag inom 15 minuter efter att en batch har importerats till profilarkivet.

### Profiler efter namnområde {#profiles-by-namespace}

I *Profiler efter namnutrymmesmått* visas totalt antal och uppdelning av namnutrymmen för alla sammanfogade profiler i din profilbutik. Det totala antalet profiler per namnutrymme (med andra ord, om de värden som visas för varje namnutrymme läggs ihop) kommer alltid att vara högre än det för antalet profiler, eftersom en profil kan ha flera namnutrymmen kopplade till sig. Om en kund till exempel interagerar med varumärket i mer än en kanal kommer flera namnutrymmen att kopplas till den enskilda kunden.

På samma sätt som för [profilräknemeterialet](#profile-count) aktiveras ett jobb för att uppdatera namnområdesmåtten när inmatningen av poster i profilarkivet ökar eller minskar antalet med mer än 5 %. För arbetsflöden med direktuppspelningsdata görs en timkontroll för att avgöra om tröskelvärdet på 5 % har uppnåtts eller ej. Om så är fallet utlöses ett jobb automatiskt för att uppdatera antalet profiler. Om tröskelvärdet på 5 % ökning eller minskning uppnås kommer ett jobb att köras för att uppdatera mätvärdena för batchförbrukning inom 15 minuter efter att en batch har importerats till profilbutiken.

### Kopplingsprincip

Väljaren för **sammanfogningsprincip** väljer automatiskt standardprincip för sammanfogning i organisationen. Om du inte vill använda den sammanfogningsprincipen kan du välja `X` bredvid standardsammanfogningsprincipen för att öppna en dialogruta *Välj sammanfogningsprincip* där du kan välja en annan sammanfogningsprincip. Mer information om sammanfogningsprinciper finns i [användarhandboken](merge-policies.md)för sammanfogningsprinciper.

![](../images/user-guide/profiles-search-merge-policy.png)

### Namnutrymme för identitet

Namnutrymmesväljaren för **identitet** öppnar en dialogruta där du kan välja det identitetsnamnutrymme som du vill söka efter. Du kan anpassa de attribut som visas i sökningen genom att markera filterikonen och välja vilka attribut du vill lägga till eller ta bort.

![](../images/user-guide/profiles-search-filter.png)

I dialogrutan *Välj identitetsnamnutrymme* väljer du det namnutrymme som du vill söka efter, eller använder **sökfältet** i dialogrutan för att skriva namnet på ett namnutrymme. Du kan markera ett namnutrymme om du vill visa mer information. När du har hittat namnutrymmet kan du markera alternativknappen och sedan trycka på **Välj** för att fortsätta.

![](../images/user-guide/profiles-select-identity-namespace.png)

### Identitetsvärde

När du har valt ett **identitetsnamnutrymme**&#x200B;återgår du till fliken *Bläddra* där du kan ange ett **identitetsvärde**. Det här värdet är specifikt för en enskild kundprofil och måste vara en giltig post för det angivna namnutrymmet. Om du t.ex. väljer **identitetsnamnutrymmet** &quot;E-post&quot; krävs ett **identitetsvärde** i form av en giltig e-postadress.

![](../images/user-guide/profiles-show-profile.png)

När du har angett ett värde väljer du **Visa profil** och sedan returneras en profil som matchar värdet. Välj **profil-ID** för att visa profilinformationen.

![](../images/user-guide/profiles-display-profile.png)

### Profilinformation

När du väljer **profil-ID**&#x200B;öppnas fliken _Detalj_ . På den här sidan visas information om den valda profilen, inklusive grundläggande attribut, länkade identiteter och tillgängliga kontaktkanaler. Profilinformationen som visas har sammanfogats från flera profilfragment till en enda vy över den enskilda kunden.

![](../images/user-guide/profiles-profile-detail.png)

Du kan visa ytterligare information om profilen, inklusive *Attribut*, *Händelser* och *Segment* som profilen är medlem i.

![](../images/user-guide/profiles-attributes-events-segments.png)

## Sammanfoga profiler

Välj fliken *Sammanfogningsprinciper* om du vill visa en lista över sammanfogningsprinciper som tillhör din organisation. Varje listad princip visar sitt namn, oavsett om det är standardprincipen för sammanslagning eller inte, och det schema som den gäller för.

Mer information om sammanfogningsprinciper finns i [användarhandboken](merge-policies.md)för sammanfogningsprinciper.

![](../images/user-guide/profiles-merge-policies.png)

## Unionsschema

Välj fliken *Unionsschema* för att visa föreningsscheman för din profilbutik. Ett unionsschema är en kombination av alla XDM-fält (Experience Data Model) under samma klass, vars scheman har aktiverats för användning i kundprofilen i realtid. Välj en klass i den vänstra listan för att visa strukturen för dess unionsschema på arbetsytan.

Om du till exempel väljer &quot;XDM-profil&quot; visas unionsschemat för klassen XDM Individual Profile.

Mer information om fackliga scheman och deras roll i kundprofilen i realtid finns i avsnittet om fackliga scheman i guiden [för](../../xdm/schema/composition.md) schemakomposition.

![](../images/user-guide/profiles-union-schema.png)

## Nästa steg

Genom att läsa den här guiden kan du nu visa och hantera dina profildata med hjälp av användargränssnittet i Experience Platform. Mer information om hur du använder kundprofildata i realtid för att generera målgruppssegment finns i [segmenteringsdokumentationen](../../segmentation/home.md).