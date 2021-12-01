---
keywords: Experience Platform;hemmabruk;populära ämnen; varningar
description: Du kan prenumerera på aviseringar när du skapar ett dataflöde för att få varningsmeddelanden om status, lyckade eller misslyckade flödeskörningar.
title: Prenumerera på varningar i sitt sammanhang i användargränssnittet
hide: true
hidefromtoc: true
source-git-commit: a81d21f615206e644044c2f0f546a458d1aebbf3
workflow-type: tm+mt
source-wordcount: '282'
ht-degree: 0%

---

# Prenumerera på varningsmeddelanden för att övervaka källans dataflöden i användargränssnittet

Med Adobe Experience Platform kan du prenumerera på händelsebaserade aviseringar om Adobe Experience Platform-aktiviteter. Varningar minskar eller eliminerar behovet av att ringa [[!DNL Observability Insights] API](../../../observability/api/overview.md) för att kontrollera om ett jobb har slutförts, om en viss milstolpe i ett arbetsflöde har nåtts eller om några fel har uppstått.

Du kan prenumerera på aviseringar när du skapar ett dataflöde för att få varningsmeddelanden om status, lyckade eller misslyckade flödeskörningar.

Det här dokumentet innehåller anvisningar om hur du prenumererar på aviseringar och får varningsmeddelanden för flödeskörningar.

## Komma igång

Dokumentet kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [Källor](../../home.md): [!DNL Experience Platform] tillåter att data hämtas från olika källor samtidigt som du kan strukturera, etikettera och förbättra inkommande data med [!DNL Platform] tjänster.
* [Observationer](../../../observability/home.md): [!DNL Observability Insights] gör att ni kan övervaka plattformsaktiviteter med hjälp av statistiska värden och händelsemeddelanden.
   * [Varningar](../../../observability/alerts/overview.md): När en viss uppsättning villkor för plattformsåtgärder har nåtts (t.ex. ett potentiellt problem när systemet överskrider ett tröskelvärde) kan Platform leverera varningsmeddelanden till alla användare i organisationen som har prenumererat på dem.

## Prenumerera på aviseringar i användargränssnittet {#subscribe-sources-alerts}

>[!CONTEXTUALHELP]
>id="platform_sources_alerts_subscribe"
>title="Prenumerera på källvarningar"
>abstract="Med varningar kan du ta emot meddelanden baserat på statusen för källans dataflöden. Du kan ange varningsmeddelanden för att få uppdateringar om dataflödet har startats, har misslyckats, eller om inga data har importerats."
>text="Learn more in documentation"
