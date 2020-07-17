---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: Översikt över kundprofiler i realtid
topic: guide
translation-type: tm+mt
source-git-commit: f910351d49de9c4a18a444b99b7f102f4ce3ed5b
workflow-type: tm+mt
source-wordcount: '1666'
ht-degree: 0%

---


# [!DNL Real-time Customer Profile] översikt

Med Adobe Experience Platform kan ni skapa samordnade, enhetliga och relevanta upplevelser för era kunder oavsett var och när de interagerar med ert varumärke. Med [!DNL Real-time Customer Profile]det kan ni få en helhetsbild av varje enskild kund som kombinerar data från flera kanaler, inklusive online-, offline-, CRM- och tredjepartsdata. [!DNL Profile] kan ni sammanställa era olika kunddata i en enhetlig vy som ger ett användbart, tidsstämplat konto för varje kundinteraktion. Den här översikten hjälper dig att förstå rollen och användningen av [!DNL Real-time Customer Profile] i [!DNL Experience Platform].

## Förstå [!DNL Real-time Customer Profile]

[!DNL Real-time Customer Profile] är ett generiskt uppslagsarkiv som sammanfogar data från olika företagsdataresurser och sedan ger tillgång till dessa data i form av enskilda kundprofiler och relaterade tidsseriehändelser. This feature enables marketers to drive coordinated, consistent and relevant experiences with their audiences across multiple channels.

### [!DNL Profile] datalager

Även om inkapslade data [!DNL Real-time Customer Profile] bearbetas och Adobe Experience Platform används [!DNL Identity Service] för att sammanfoga relaterade data via identitetsmappning, behåller det sina egna data i [!DNL Profile] arkivet. Med andra ord är [!DNL Profile] arkivet skilt från [!DNL Catalog] data ([!DNL Data Lake]) och [!DNL Identity Service] data (identitetsdiagram).

### [!DNL Profile] och [!DNL Platform] tjänster

Relationen mellan [!DNL Real-time Customer Profile] och andra tjänster inom [!DNL Experience Platform] visas i följande diagram:

![Förhållandet mellan Profil och andra Experience Platform-tjänster.](images/profile-overview/profile-in-platform.png)

### Profiler och registrera data

A profile is a representation of a subject, an organization or an individual, also referred to as record data. For example, the profile of a product may include a SKU and description, whereas the profile of a person contains information like first name, last name, and email address. Med [!DNL Experience Platform]kan du anpassa profiler så att de använder datatyper som är relevanta för ditt företag. Standardklassen [!DNL Experience Data Model] (XDM) [!DNL Individual Profile] är den klass som oftast används för att skapa ett schema när kundpostdata beskrivs, och som tillhandahåller data som är integrerade i många interaktioner mellan Platform tjänster. Mer information om hur du arbetar med scheman i [!DNL Experience Platform]finns i [XDM-systemöversikten](../xdm/home.md).

### Tidsseriehändelser

Med tidsseriedata får du en ögonblicksbild av systemet när en åtgärd vidtas antingen direkt eller indirekt av ett ämne, samt data som detaljerar själva händelsen. Tidsseriedata representeras av standardschemaklassen XDM ExperienceEvent och kan beskriva händelser som objekt som läggs till i en kundvagn, länkar som klickas och videofilmer som visas. Tidsseriedata kan användas för att basera segmenteringsregler på, och händelser kan nås individuellt i en profils kontext.

### Identiteter

Alla företag vill kommunicera med sina kunder på ett sätt som känns personligt. However, one of the challenges of delivering relevant digital experiences to customers is understanding how to tie their disconnected data together, which is often spread across different digital channels such as tablets, mobile phones and laptops. [!DNL Identity Service] gör att ni kan sammanställa hela bilden av kunden genom att länka identiteter från flera kanaler, skapa ett identitetsdiagram för varje kund så att ni bättre kan förstå dem. Mer information finns i översikten över [identitetstjänsten](../identity-service/home.md) .

### Segmentering

Adobe Experience Platform [!DNL Segmentation Service] producerar de målgrupper som behövs för att ge era enskilda kunder bättre upplevelser. När ett målgruppssegment skapas läggs ID:t för det segmentet till i listan över segmentmedlemskap för alla kvalificerande profiler. Segmentregler byggs och tillämpas på [!DNL Real-time Customer Profile] data med RESTful API:er och användargränssnittet i Segment Builder. To learn more about segmentation, please begin by reading the [Segmentation Service overview](../segmentation/home.md).

### Profilfragment och föreningsscheman {#profile-fragments-and-union-schemas}

En av de viktigaste funktionerna i [!DNL Real-time Customer Profile] är möjligheten att sammanställa flerkanalsdata. När [!DNL Real-time Customer Profile] används för att få åtkomst till en enhet kan den ge dig en sammanslagen vy över alla profilfragment för den entiteten i alla datauppsättningar, som kallas unionsvyn och som görs möjlig genom ett så kallat unionsschema. [!DNL Real-time Customer Profile] data sammanfogas mellan olika källor när en enhet eller profil används av dess ID eller exporteras som ett segment. To learn more about accessing profiles and union views using the [!DNL Real-time Customer Profile] API, visit the [entities endpoint guide](api/entities.md).

### Sammanfoga profiler

När ni sammanfogar data från flera olika källor och kombinerar dem för att få en fullständig bild av var och en av era enskilda kunder, är sammanfogningsprinciper reglerna som [!DNL Platform] använder för att avgöra hur data ska prioriteras och vilka data som ska kombineras för att skapa den enhetliga vyn. Med RESTful API:er eller användargränssnittet kan du skapa nya kopplingsprofiler, hantera befintliga profiler och ange en standardkopplingsprofil för organisationen. Mer information om hur du arbetar med sammanfogningsprinciper med [!DNL Real-time Customer Profile] API finns i [slutpunktshandboken](api/merge-policies.md)för sammanfogningsprinciper. Om du vill arbeta med sammanfogningsprinciper med hjälp av [!DNL Experience Platform] användargränssnittet läser du i användarhandboken för [sammanfogningsprinciper](ui/merge-policies.md).

### (Alfa) Konfigurera beräknade attribut

>[!IMPORTANT]
>Den beräknade attributfunktionaliteten som beskrivs i det här dokumentet är alfavärden. Dokumentationen och funktionaliteten kan komma att ändras.

Med beräknade attribut kan du automatiskt beräkna fältvärden baserat på andra värden, beräkningar och uttryck. Beräknade attribut fungerar på profilnivån, vilket innebär att du kan samla värden för alla poster och händelser. Varje beräknat attribut innehåller ett uttryck, eller &quot;rule&quot;, som utvärderar inkommande data och lagrar resultatvärdet i ett profilattribut eller i en händelse. Med hjälp av dessa beräkningar kan du enkelt besvara frågor som rör inköpstid, tid mellan köp eller antal programöppningar, utan att behöva utföra komplexa beräkningar manuellt varje gång informationen behövs. Mer information om beräknade attribut och steg-för-steg-instruktioner om hur du arbetar med dem med API:t finns i [!DNL Real-time Customer Profile] slutpunktshandboken [](api/computed-attributes.md)för beräknade attribut. Den här guiden hjälper dig att bättre förstå vilken roll beräknade attribut spelar i Adobe Experience Platform, och den innehåller exempel på API-anrop för grundläggande CRUD-åtgärder.

## Realtidskomponenter

I det här avsnittet introduceras de komponenter som gör det möjligt [!DNL Real-time Customer Profile] att uppdatera och övervaka post- och tidsseriedata i realtid.

### Direktuppspelningsuppläsning och direktuppspelningssegmentering

Realtidsinmatning är möjlig genom en process som kallas direktuppspelning. När data från profil- och tidsserier hämtas bestämmer sig [!DNL Real-time Customer Profile] automatiskt för att inkludera eller exkludera data från segment via en pågående process som kallas direktuppspelningssegmentering, innan de slås samman med befintliga data och unionsvyn uppdateras. Resultatet blir att ni omedelbart kan utföra beräkningar och fatta beslut för att leverera förbättrade, individanpassade upplevelser till kunderna när de interagerar med ert varumärke. När data importeras valideras de också för att säkerställa att de importeras på rätt sätt och att de överensstämmer med det schema som datauppsättningen baseras på. Om du vill ha mer information om vilken validering som görs under importen kan du börja med att läsa [kvalitetsöversikten](../ingestion/quality/overview.md)för dataimporten.

### Konfiguration och mål för Edge-projektion

För att kunna skapa samordnade, enhetliga och personaliserade upplevelser för era kunder i flera kanaler i realtid måste rätt data vara lätt tillgängliga och uppdateras kontinuerligt när förändringar sker. Adobe Experience Platform ger realtidsåtkomst till data genom att använda kanter. En kant är en geografiskt placerad server som lagrar data och som gör dem tillgängliga för program. For example, Adobe applications such as Adobe Target and Adobe Campaign use edges in order to provide personalized customer experiences in real-time. Data dirigeras till en kant med en projektion, med en projektionsdestination som definierar den kant till vilken data ska skickas och en projektionskonfiguration som definierar den specifika information som ska göras tillgänglig på kanten. Om du vill veta mer och börja arbeta med projektioner med hjälp av [!DNL Real-time Customer Profile] API:t kan du läsa guiden [för](api/edge-projections.md)kantprojektionsslutpunkter.

## Lägg till data i [!DNL Real-time Customer Profile]

[!DNL Platform] kan konfigureras för att skicka data från poster och tidsserier till [!DNL Profile]med stöd för direktuppspelning i realtid och batchförbrukning. For more information, see the tutorial outlining how to [add data to Real-time Customer Profile](tutorials/add-profile-data.md).

>[!Note]
>Data collected through Adobe solutions, including [!DNL Analytics Cloud], [!DNL Marketing Cloud], and [!DNL Advertising Cloud], flows into [!DNL Experience Platform] and is ingested into [!DNL Profile].

### [!DNL Profile] ingestion metrics

Observability Insights allows you to expose key metrics in Adobe Experience Platform. In addition to [!DNL Platform] usage statistics and performance indicators for various [!DNL Platform] functionalities, there are specific [!DNL Profile]-related metrics that allow you to gain insight into incoming request rates, successful ingestion rates, ingested record sizes, and more. To learn more, begin by reading the [Observability Insights overview](../observability/home.md), and for a complete list of [!DNL Profile] metrics, see the documentation on [available metrics](../observability/metrics.md).

## [!DNL Data governance] och [!DNL Privacy]

[!DNL Data governance] is a series of strategies and technologies used to manage customer data and ensure compliance with regulations, restrictions, and policies applicable to data use.

As it relates to accessing data, data governance plays a key role within [!DNL Experience Platform] at various levels:
* Data usage labeling
* Data access policies
* Access control on data for marketing actions

[!DNL Data governance] is managed at several points. These include deciding what data is ingested into [!DNL Platform] and what data is accessible after ingestion for a given marketing action. For more information, begin by reading the [data governance overview](../data-governance/home.md).

### Handling opt-out and data privacy requests

[!DNL Experience Platform] enables your customers to send opt-out requests related to the usage and storage of their data within [!DNL Real-time Customer Profile]. Mer information om hur avanmälningsbegäranden hanteras finns i dokumentationen om [hur avanmälningsbegäranden](../segmentation/honoring-opt-outs.md)respekteras.

## [!DNL Profile] guidelines

[!DNL Experience Platform] has a series of guidelines to follow in order to effectively use [!DNL Profile].

| Avsnitt | Gräns |
| ------- | -------- |
| [!DNL Profile] union schema | A maximum of **20** datasets can contribute to the [!DNL Profile] union schema. |
| Multi-entity relationships | A maximum of **5** multi-entity relationship can be created. |
| JSON depth for multi-entity association | The maximum JSON depth is **4**. |
| Time series data | Time-series data is **not** permitted in [!DNL Profile] for non-people entities. |
| Non-people schema relationships | Non-people schema relationships are **not** permitted. |
| Profile fragment | The recommended maximum size of a profile fragment is **10kB**.<br><br> The absolute maximum size of a profile fragment is **1MB**. |
| Non-person entity | The maximum total size for a single non-person entity is **200MB**. |
| Datasets per non-person entity | A maximum of **1** dataset can be associated to a non-person entity. |

<!--
| Section | Boundary | Enforcement |
| ------- | -------- | ----------- |
| Profile union schema | A maximum of **20** datasets can contribute to the Profile union schema. | A message stating you've reached the maximum number of datasets appears. You must either disable or clean up other obsolete datasets in order to create a new dataset. |
| Multi-entity relationships | A maximum of **5** multi-entity relationship can be created. | A message stating all available mappings have been used appears when the fifth relationship is mapped. An error message letting you know you have exceeded the number of available mappings appears when attempting to map a sixth relationship. | 
| JSON depth for multi-entity association | The maximum JSON depth is **4**. | When trying to use the relationship selector with a field that is more than four levels deep, an error message appears, stating it is ineligible for multi-entity association. |
| Time series data | Time-series data is **not** permitted in Profile for non-people entities. | A message stating that this data cannot be enabled for Profile because it is of an unsupported type appears. |
| Non-people schema relationships | Non-people schema relationships are **not** permitted. | Relationships between two non-people schemas cannot be created. The relationships checkbox will be disabled. |
| Profile fragment | The recommended maximum size of a profile fragment is **10kB**.<br><br> The absolute maximum size of a profile fragment is **1MB**. | If you upload a fragment that is larger than 10kB, a warning appears, stating that performance may be degraded since the fragment exceeds the recommended maximum working size.<br><br> If you upload a fragment that is larger than 1MB, ingestion will fail, and an alert letting you know that records have failed will be sent. |
| Non-person entity | The maximum total size for a single non-person entity is **200MB**. | If you load an object as a non-person entity that is larger than 200MB, an alert will appear, stating that the entity has exceeded the maximum allowable size and will not be useable for segmentation. |
| Datasets per non-person entity | A maximum of **1** dataset can be associated to a non-person entity. | If you try to create a second dataset that is associated to the same non-person entity, an error appears, stating that only one dataset can be active per non-person entity. |

--->

>[!NOTE]
>
>
>En icke-personenhet refererar till alla XDM-klasser som **inte** ingår i [!DNL Profile].

## Nästa steg och ytterligare resurser

Om du vill veta mer [!DNL Real-time Customer Profile]kan du fortsätta läsa dokumentationen och komplettera din inlärning genom att titta på videon nedan eller utforska andra videokurser [för](https://docs.adobe.com/content/help/en/platform-learn/tutorials/overview.html)Experience Platform.

>[!WARNING]
>Gränssnittet [!DNL Platform] som visas i följande video är inaktuellt. Läs användarhandboken för [kundprofilen i realtid](ui/user-guide.md) för de senaste skärmbilderna och funktionerna i användargränssnittet.

>[!VIDEO](https://video.tv.adobe.com/v/27251?quality=12)