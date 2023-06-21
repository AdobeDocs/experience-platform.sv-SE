---
title: Översikt över källkoppling för blandpanel
description: Lär dig hur du ansluter Mixpanel till Adobe Experience Platform med API:er eller användargränssnittet.
last-substantial-update: 2023-06-21T00:00:00Z
exl-id: 7eb605f6-8580-40b7-a9b3-96b9c3444f5d
source-git-commit: 6f8abca8f0db8a559fe62e6c143f2d0506d3b886
workflow-type: tm+mt
source-wordcount: '449'
ht-degree: 0%

---

# [!DNL Mixpanel]

Med Adobe Experience Platform kan data hämtas från externa källor samtidigt som du kan strukturera, märka och förbättra inkommande data med hjälp av plattformstjänster. Du kan importera data från en mängd olika källor, till exempel Adobe-program, molnbaserad lagring, databaser och många andra.

Experience Platform har stöd för inhämtning av data från ett analysprogram från tredje part. Stöd för analysleverantörer innefattar [!DNL Mixpanel].

[[!DNL Mixpanel]](https://www.mixpanel.com) är ett produktanalysverktyg som gör det möjligt att samla in data om hur användarna interagerar med en digital produkt. Med Mixpanel kan du analysera produktdata med enkla, interaktiva rapporter som gör att du kan fråga och visualisera data med bara några klick.

Källor utnyttjar [Export-API för Mixpanel-händelse > Hämta](https://developer.mixpanel.com/reference/raw-event-export) för att ladda ned händelsedata när de tas emot och lagras i [!DNL Mixpanel], tillsammans med alla händelseegenskaper (inklusive `distinct_id`) och den exakta tidsstämpeln som händelsen skickades till Experience Platform. I Mixpanel används bearer-tokens som en autentiseringsmekanism för att kommunicera med API:t för händelsemport i Mixpanel.

## IP-adress tillåtelselista

En lista med IP-adresser måste läggas till tillåtelselista innan du kan arbeta med källanslutningar. Om du inte lägger till dina regionspecifika IP-adresser i tillåtelselista kan det leda till fel eller sämre prestanda när du använder källor. Se [IP-adress tillåtelselista](../../ip-address-allow-list.md) sida för mer information.

## Autentisera [!DNL Mixpanel] konto

I det här avsnittet beskrivs nödvändiga steg för att slutföra autentiseringen av ditt konto och för att ta med din [!DNL Mixpanel] data till plattformen.

För att skapa en [!DNL Mixpanel] källanslutning och dataflöde måste först ha ett giltigt [!DNL Mixpanel] konto. Om du inte har en giltig [!DNL Mixpanel] konto, se [Delpanelsregister](https://mixpanel.com/register/) sida för att skapa ditt konto.

När du har skapat en [!DNL Mixpanel] konto, navigera till [!DNL Project Details] i [!DNL Project Seettings] sidan på [!DNL Mixpanel] Gränssnitt för att hämta ditt projekt-ID och konfigurera din tidszon.

![mixpanel-project-settings](../../images/tutorials/create/mixpanel-export-events/mixpanel-project-settings.png)

Navigera sedan till [!DNL Service Accounts] i [!DNL Project Settings] sidan i [!DNL Mixpanel] Gränssnitt för att hämta autentiseringsuppgifter för ditt tjänstkonto.

>[!TIP]
>
>Välj ett tjänstkonto som [upphör inte att gälla](https://developer.mixpanel.com/reference/service-accounts#service-account-expiration).

![Tjänstkonto för blandpanel](../../images/tutorials/create/mixpanel-export-events/mixpanel-service-account.png)

Skapa slutligen en plattform [schema](../../../xdm/schema/composition.md) krävs för [!DNL Mixpanel Event Export API]. Mer information om vilka mappningar som krävs för ditt schema finns i handboken [skapa [!DNL Mixpanel] källanslutning i användargränssnittet](../../tutorials/ui/create/analytics/mixpanel.md#additional-resources).

![Skapa schema](../../images/tutorials/create/mixpanel-export-events/schema.png)

## Anslut [!DNL Mixpanel] till plattform med API:er

Dokumentationen nedan innehåller information om hur du ansluter [!DNL Mixpanel] till Plattform med API:er eller användargränssnittet:

* [Skapa en källanslutning och ett dataflöde för [!DNL Mixpanel] med API:t för Flow Service](../../tutorials/api/create/analytics/mixpanel.md)

## Anslut [!DNL Mixpanel] till plattform med användargränssnittet

* [Skapa en [!DNL Mixpanel] källanslutning i användargränssnittet](../../tutorials/ui/create/analytics/mixpanel.md)
* [Skapa ett dataflöde för en källanslutning till en lyckad kund i användargränssnittet](../../tutorials/ui/dataflow/analytics.md)
