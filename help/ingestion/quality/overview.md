---
keywords: Experience Platform;hem;populära ämnen;Datakvalitet;Kvalitet;Validering;validering som stöds;validering;
solution: Experience Platform
title: Datakvalitet
description: Följande dokument innehåller en sammanfattning av de kontroller och valideringsbeteenden som stöds för import av grupper och direktuppspelning i Adobe Experience Platform.
exl-id: 7ef40859-235a-4759-9492-c63e5fd80c8e
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '427'
ht-degree: 0%

---

# Datakvalitet i Adobe Experience Platform

Adobe Experience Platform ger väldefinierade garantier för fullständighet, exakthet och enhetlighet för alla data som överförs via både batch- och direktuppspelningsinmatning. Följande dokument innehåller en sammanfattning av de kontroller och valideringsbeteenden som stöds för import av grupper och direktuppspelning i [!DNL Experience Platform].

## Kontroller som stöds

|   | Batchintag | Direktuppspelningsinmatning |
| ------ | --------------- | ------------------- |
| Datatypskontroll | Ja | Ja |
| Uppräkningskontroll | Ja | Ja |
| Intervallkontroll (min, max) | Ja | Ja |
| Obligatorisk fältkontroll | Ja | Ja |
| Mönsterkontroll | Nej | Ja |
| Formatkontroll | Nej | Ja |

## Valideringsbeteenden som stöds

Inmatning av både batch- och direktuppspelning förhindrar att felaktiga data flyttas nedåt genom att felaktiga data flyttas för hämtning och analys i [!DNL Data Lake]. Inmatning av data ger följande valideringar för inmatning av grupper och strömning.

### Batchförtäring

Följande valideringar görs för batchförtäring:

| Valideringsområde | Beskrivning |
| --------------- | ----------- |
| Schema | Ser till att schemat är **inte** tomt och innehåller en referens till unionsschemat enligt följande: `"meta:immutableTags": ["union"]` |
| `identityField` | Ser till att alla giltiga identitetsbeskrivningar definieras. |
| `createdUser` | Ser till att användaren som importerade batchen tillåts importera batchen. |

### Direktinmatning

Följande valideringar görs för direktuppspelning:

| Valideringsområde | Beskrivning |
| --------------- | ----------- |
| Schema | Ser till att schemat är **inte** tomt och innehåller en referens till unionsschemat enligt följande: `"meta:immutableTags": ["union"]` |
| `identityField` | Ser till att alla giltiga identitetsbeskrivningar definieras. |
| JSON | Ser till att JSON är giltig. |
| Organisation | Ser till att den listade organisationen är en giltig organisation. |
| Source name | Ser till att namnet på datakällan anges. |
| Datauppsättning | Ser till att datauppsättningen anges, aktiveras och inte har tagits bort. |
| Sidhuvud | Ser till att rubriken är angiven och giltig. |

Mer information om hur [!DNL Platform] övervakar och validerar data finns i [dokumentationen för övervakning av dataflöden](./monitor-data-ingestion.md).

## Validering av identitetsvärde

Följande tabell visar befintliga regler som du måste följa för att identitetsvärdet ska kunna valideras korrekt.

| Namnutrymme | Valideringsregel | Systembeteende när regeln bryts |
| --- | --- | --- |
| ECID | <ul><li>Identitetsvärdet för ett ECID måste vara exakt 38 tecken.</li><li>Identitetsvärdet för ett ECID får endast bestå av siffror.</li></ul> | <ul><li>Om identitetsvärdet för ECID inte är exakt 38 tecken hoppas posten över.</li><li>Om identitetsvärdet för ECID innehåller icke-numeriska tecken hoppas posten över.</li></ul> |
| Ej ECID | Identitetsvärdet får inte vara längre än 1 024 tecken. | Om identitetsvärdet är längre än 1 024 tecken hoppas posten över. |

Mer information om [!DNL Identity Service] skyddsutkast finns i [[!DNL Identity Service] översikten över skyddsutkast](../../identity-service/guardrails.md).
