---
keywords: Experience Platform;felsökning;skyddsförslag;riktlinjer;
title: Guardsedningar för datainmatning
description: Det här dokumentet innehåller riktlinjer för hur man skyddar mot dataintrång i Adobe Experience Platform
exl-id: f07751cb-f9d3-49ab-bda6-8e6fec59c337
source-git-commit: 4debc301b930643565b25218f4822a67e88063bb
workflow-type: tm+mt
source-wordcount: '588'
ht-degree: 0%

---

# Guardsedningar för datainmatning

Garantier är trösklar som ger vägledning för data- och systemanvändning, prestandaoptimering och undvikande av fel eller oväntade resultat i Adobe Experience Platform. Garantier kan avse din användning eller konsumtion av data och bearbetning i relation till dina licensrättigheter.

I det här dokumentet finns riktlinjer för hur man skyddar mot dataintrång i Adobe Experience Platform.

## Garantier för batchförtäring

I följande tabell visas skyddsutkast som ska beaktas när du använder [API för gruppinmatning](./batch-ingestion/overview.md) eller källor:

| Typ av förtäring | Riktlinjer | Anteckningar |
| --- | --- | --- |
| Intag av data i sjön med hjälp av API för gruppinmatning | <ul><li>Du kan importera upp till 20 GB data per timme till en datasjön med hjälp av API:t för gruppinmatning.</li><li>Det högsta antalet filer per grupp är 1500.</li><li>Den maximala batchstorleken är 100 GB.</li><li>Det maximala antalet egenskaper eller fält per rad är 10000.</li><li>Det högsta antalet batchar per minut, per användare, är 138.</li></ul> |
| Intag av data i sjön med hjälp av batchkällor | <ul><li>Du kan inhämta upp till 200 GB data per timme till datasjön med hjälp av batchkällor som [!DNL Azure Blob], [!DNL Amazon S3]och [!DNL SFTP].</li><li>Batchstorleken bör vara mellan 256 MB och 100 GB. Detta gäller både okomprimerade och komprimerade data. När komprimerade data är okomprimerade i datasjön gäller dessa begränsningar.</li><li>Det högsta antalet filer per grupp är 1500.</li></ul> | Se [källöversikt](../sources/home.md) om du vill ha en katalog med källor som du kan använda för datainmatning. |
| Gruppinmatning till profil | <ul><li>Den största tillåtna storleken för en postklass är 100 kB (mjuk).</li><li>Den största tillåtna storleken för en ExperienceEvent-klass är 10 kB (mjuk).</li><li>Den största tillåtna storleken för en enstaka post är 1 MB.</li></ul> |
| Antal profiler eller ExperienceEvent-batchar som har importerats per dag | **Det högsta antalet profiler eller ExperienceEvent-batchar som har importerats per dag är 90.** Det innebär att den sammanlagda summan av de profiler och ExperienceEvent-batchar som hämtas varje dag inte får överstiga 90. Om ytterligare batchar registreras påverkas systemets prestanda. | Det här är en mjuk gräns. Det går att gå längre än en mjuk gräns, men mjuka gränser ger en rekommenderad vägledning för systemprestanda. |

## Gardrutor för direktuppspelad förtäring

Läs [översikt över direktuppspelning](./streaming-ingestion/overview.md) för information om skyddsräcken för direktuppspelning.

## Gardrutor för direktuppspelningskällor

I följande tabell visas skyddsutkast som du bör tänka på när du använder direktuppspelningskällor:

| Typ av förtäring | Riktlinjer | Anteckningar |
| --- | --- | --- |
| Direktuppspelningskällor | <ul><li>Den maximala poststorleken är 1 MB och den rekommenderade storleken är 10 kB.</li><li>Direktuppspelningskällor har stöd för mellan 4 000 och 5 000 begäranden per sekund när en ny källanslutning skapas. **Anteckning**: Det kan ta upp till 30 minuter för strömmande data att bearbetas helt till datasjön.</li><li>Du kan bearbeta mellan 4 000 och 5 000 begäranden per sekund till en Data Lake. **Anteckning**: Det kan ta upp till 30 minuter för strömmande data att bearbetas helt till datasjön.</li></ul> | Direktuppspelningskällor som [!DNL Kafka], [!DNL Azure Event Hubs]och [!DNL Amazon Kinesis] använd inte [!DNL Data Collection Core Service] (DCCS) och kan ha olika genomströmningsgränser. Se [källöversikt](../sources/home.md) om du vill ha en katalog med källor som du kan använda för datainmatning. |

## Nästa steg

Följande dokumentation innehåller mer information om andra Experience Platform-servicesäkrar, om total latenstid och licensinformation från Real-Time CDP produktbeskrivningsdokument:

* [Real-Time CDP skyddsräcken](/help/rtcdp/guardrails/overview.md)
* [Latensdiagram från början till slut](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/deployment/guardrails.html?lang=en#end-to-end-latency-diagrams) för olika Experience Platform-tjänster.
* [Real-time Customer Data Platform (B2C Edition - Prime- och Ultimate-paket)](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2c-edition-prime-and-ultimate-packages.html)
* [Real-time Customer Data Platform (B2P - Prime- och Ultimate-paket)](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2p-edition-prime-and-ultimate-packages.html)
* [Real-time Customer Data Platform (B2B - Prime- och Ultimate-paket)](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html)
