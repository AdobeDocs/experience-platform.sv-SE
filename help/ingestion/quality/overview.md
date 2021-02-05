---
keywords: Experience Platform;hem;populära ämnen;Datakvalitet;Kvalitet;Validering;validering som stöds;validering;
solution: Experience Platform
title: Datakvalitet
topic: overview
description: Följande dokument innehåller en sammanfattning av de kontroller och valideringsbeteenden som stöds för import av grupper och direktuppspelning i Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: 089a4d517476b614521d1db4718966e3ebb13064
workflow-type: tm+mt
source-wordcount: '317'
ht-degree: 4%

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

Både batch- och direktuppspelningsinmatning förhindrar att felaktiga data flyttas längre ned genom att felaktiga data flyttas för hämtning och analys i [!DNL Data Lake]. Inmatning av data ger följande valideringar för inmatning av grupper och strömning.

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
| IMS-organisation | Ser till att den angivna IMS-organisationen är en giltig organisation. |
| Källnamn | Ser till att namnet på datakällan anges. |
| Datauppsättning | Ser till att datauppsättningen är angiven, aktiverad och inte har tagits bort. |
| Sidhuvud | Ser till att rubriken är angiven och giltig. |

Mer information om hur [!DNL Platform] övervakar och validerar data finns i [dokumentationen för övervakning av dataflöden](./monitor-data-ingestion.md).
