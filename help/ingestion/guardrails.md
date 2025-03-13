---
keywords: Experience Platform;felsökning;skyddsförslag;riktlinjer;
title: Guardsedningar för datainmatning
description: Läs om hur du skyddar dig mot dataintrång i Adobe Experience Platform.
exl-id: f07751cb-f9d3-49ab-bda6-8e6fec59c337
source-git-commit: a862e532382472eadf29aee2568c550b1a71211a
workflow-type: tm+mt
source-wordcount: '827'
ht-degree: 0%

---

# Guardsedningar för datainmatning

>[!IMPORTANT]
>
>Gardrafiler för att lägga till grupper och strömmande innehåll beräknas vanligtvis på organisationsnivå och inte på sandlådenivå. Detta innebär att din dataanvändning per sandlåda är bunden till det totala licensanvändningsberättigande som motsvarar hela din organisation. Dessutom är dataanvändningen i utvecklingssandlådor begränsad till 10 % av det totala antalet profiler. Mer information om berättigande för licensanvändning finns i [handboken om bästa praxis för datahantering](../landing/license-usage-and-guardrails/data-management-best-practices.md).

Garantier är trösklar som ger vägledning för data- och systemanvändning, prestandaoptimering och undvikande av fel eller oväntade resultat i Adobe Experience Platform. Garantier kan avse din användning eller konsumtion av data och bearbetning i relation till dina licensrättigheter.

>[!IMPORTANT]
>
>Kontrollera dina licensrättigheter i din försäljningsorder och motsvarande [produktbeskrivning](https://helpx.adobe.com/legal/product-descriptions.html) om faktiska användningsbegränsningar, utöver den här sidan med skyddsförslag.

I det här dokumentet finns riktlinjer för hur man skyddar mot dataintrång i Adobe Experience Platform.

## Garantier för batchförtäring

I följande tabell visas skyddsutkast som ska beaktas när [API:t för batchimport](./batch-ingestion/overview.md) eller källor används:

| Typ av förtäring | Riktlinjer | Anteckningar |
| --- | --- | --- |
| Intag av data i sjön med hjälp av API för gruppinmatning | <ul><li>Du kan importera upp till 20 GB data per timme till en datasjön med hjälp av API:t för gruppinmatning.</li><li>Det högsta antalet filer per grupp är 1500.</li><li>Den maximala batchstorleken är 100 GB.</li><li>Det maximala antalet egenskaper eller fält per rad är 10000.</li><li>Högsta antal batchar per minut, per användare är 2 000.</li></ul> | |
| Intag av data i sjön med hjälp av batchkällor | <ul><li>Du kan inhämta upp till 200 GB data per timme till datavjön med hjälp av batchmatningskällor som [!DNL Azure Blob], [!DNL Amazon S3] och [!DNL SFTP].</li><li>Batchstorleken bör vara mellan 256 MB och 100 GB. Detta gäller både okomprimerade och komprimerade data. När komprimerade data är okomprimerade i datasjön gäller dessa begränsningar.</li><li>Det högsta antalet filer per grupp är 1500.</li><li>Den minsta storleken för en fil eller mapp är 1 byte. Du kan inte importera filer eller mappar med storleken 0 byte.</li></ul> | Läs [källÖversikt](../sources/home.md) om du vill se en katalog med källor som du kan använda för datainmatning. |
| Gruppinmatning till profil | <ul><li>Den största tillåtna storleken för en postklass är 100 kB (hård).</li><li>Den största tillåtna storleken för en ExperienceEvent-klass är 10 kB (hårddisk).</li></ul> | |
| Antal profiler eller ExperienceEvent-batchar som har importerats per dag | **Det maximala antalet inkapslade Profile- eller ExperienceEvent-batchar per dag är 90 per sandlåda.** Det innebär att den sammanlagda summan av de profiler och ExperienceEvent-batchar som hämtas varje dag inte får överstiga 90. Om ytterligare batchar registreras påverkas systemets prestanda. | Det här är en mjuk gräns. Det går att gå längre än en mjuk gräns, men mjuka gränser ger en rekommenderad vägledning för systemprestanda. Dessutom är skyddsprofilen **per sandbox**, inte per organisation. |
| Krypterad dataöverföring | Den största tillåtna storleken för en krypterad fil är 1 GB. Du kan till exempel importera 2 eller fler GB-data i en enda dataflödeskörning, men ingen enskild fil i dataflödeskörningen kan överstiga 1 GB. | Processen med att importera krypterade data kan ta längre tid än den som sker vid vanlig datainmatning. Mer information finns i [API-handboken för krypterad datainhämtning](../sources/tutorials/api/encrypt-data.md). |
| Uppgradera batchinmatning | Inmatning av uppgraderingsbatchar kan vara upp till 10 gånger långsammare än vanliga batchar. Därför bör du **hålla dina uppgraderingsbatchar under två miljoner poster** för att säkerställa en effektiv körningstid och undvika att blockera andra batchar från att bearbetas i sandlådan. | Även om du utan tvekan kan importera batchar som överskrider två miljoner poster, kommer tiden för ditt intag att bli avsevärt längre på grund av begränsningar i små sandlådor. |

{style="table-layout:auto"}

## Gardrutor för direktuppspelad förtäring

Läs [översikten över direktuppspelningsuppläsning](./streaming-ingestion/overview.md) om du vill ha mer information om skyddsförslag för direktuppspelningsuppläsning.

## Gardrutor för direktuppspelningskällor

I följande tabell visas skyddsutkast som du bör tänka på när du använder direktuppspelningskällor:

| Typ av förtäring | Riktlinjer | Anteckningar |
| --- | --- | --- |
| Direktuppspelningskällor | <ul><li>Den maximala poststorleken är 1 MB och den rekommenderade storleken är 10 kB.</li><li>Direktuppspelningskällor har stöd för mellan 4000 och 5000 begäranden per sekund vid import till sjön. Detta gäller både för nyligen skapade källanslutningar utöver befintliga källanslutningar. **Obs!** Det kan ta upp till 30 minuter innan direktuppspelningsdata bearbetas fullständigt till datasjön.</li><li>Direktuppspelningskällor har stöd för högst 1 500 begäranden per sekund vid import av data till profil eller direktuppspelningssegmentering.</li></ul> | Direktuppspelningskällor som [!DNL Kafka], [!DNL Azure Event Hubs] och [!DNL Amazon Kinesis] använder inte DCCS-vägen ([!DNL Data Collection Core Service]) och kan ha olika genomströmningsbegränsningar. I [källÖversikt](../sources/home.md) finns en katalog med källor som du kan använda för datainmatning. |

{style="table-layout:auto"}

## Nästa steg

I följande dokumentation finns mer information om andra Experience Platform servicemarginaler, om total latenstid och licensieringsinformation från Real-Time CDP produktbeskrivningsdokument:

* [Real-Time CDP skyddsräcken](/help/rtcdp/guardrails/overview.md)
* [Avancerade latensdiagram](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/deployment/guardrails.html?lang=en#end-to-end-latency-diagrams) för olika Experience Platform-tjänster.
* [Real-Time Customer Data Platform (B2C Edition - Prime- och Ultimate-paket)](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2c-edition-prime-and-ultimate-packages.html)
* [Real-Time Customer Data Platform (B2P - Prime- och Ultimate-paket)](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2p-edition-prime-and-ultimate-packages.html)
* [Real-Time Customer Data Platform (B2B - Prime- och Ultimate-paket)](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html)
