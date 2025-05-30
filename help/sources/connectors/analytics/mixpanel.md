---
title: Översikt över Source Connector med blandpanel
description: Lär dig hur du ansluter Mixpanel till Adobe Experience Platform med API:er eller användargränssnittet.
last-substantial-update: 2023-06-21T00:00:00Z
exl-id: 7eb605f6-8580-40b7-a9b3-96b9c3444f5d
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '445'
ht-degree: 0%

---

# [!DNL Mixpanel]

Med Adobe Experience Platform kan data hämtas från externa källor samtidigt som du kan strukturera, etikettera och förbättra inkommande data med hjälp av Experience Platform tjänster. Du kan importera data från en mängd olika källor, till exempel Adobe-program, molnbaserad lagring, databaser och många andra.

Experience Platform har stöd för inmatning av data från ett analysprogram från tredje part. Stöd för analysleverantörer inkluderar [!DNL Mixpanel].

[[!DNL Mixpanel]](https://www.mixpanel.com) är ett produktanalysverktyg som gör att du kan samla in data om hur användare interagerar med en digital produkt. Med Mixpanel kan du analysera produktdata med enkla, interaktiva rapporter som gör att du kan fråga och visualisera data med bara några klick.

Källor utnyttjar [API:t för export av händelser i panelen Mixpanel > Hämta](https://developer.mixpanel.com/reference/raw-event-export) för att hämta dina händelsedata när de tas emot och lagras i [!DNL Mixpanel], tillsammans med alla händelseegenskaper (inklusive `distinct_id`) och den exakta tidsstämpeln som händelsen skickades till Experience Platform. I Mixpanel används bearer-tokens som en autentiseringsmekanism för att kommunicera med API:t för händelsemport i Mixpanel.

## IP-adress tillåtelselista

En lista med IP-adresser måste läggas till tillåtelselista innan du kan arbeta med källanslutningar. Om du inte lägger till dina regionspecifika IP-adresser i tillåtelselista kan det leda till fel eller sämre prestanda när du använder källor. Mer information finns på sidan [IP-adress tillåtelselista](../../ip-address-allow-list.md).

## Autentisera ditt [!DNL Mixpanel]-konto

I det här avsnittet beskrivs nödvändiga steg som måste utföras för att autentisera ditt konto och överföra dina [!DNL Mixpanel]-data till Experience Platform.

Om du vill skapa en [!DNL Mixpanel]-källanslutning och ett dataflöde måste du först ha ett giltigt [!DNL Mixpanel]-konto. Om du inte har ett giltigt [!DNL Mixpanel]-konto kan du skapa ditt konto på sidan [Delpanelsregistrering](https://mixpanel.com/register/).

När du har skapat ett [!DNL Mixpanel]-konto går du till fliken [!DNL Project Details] på sidan [!DNL Project Seettings] i [!DNL Mixpanel]-gränssnittet för att hämta ditt projekt-ID och konfigurera din tidszon.

![mixpanel-project-settings](../../images/tutorials/create/mixpanel-export-events/mixpanel-project-settings.png)

Gå sedan till fliken [!DNL Service Accounts] på sidan [!DNL Project Settings] i användargränssnittet för [!DNL Mixpanel] för att hämta autentiseringsuppgifterna för ditt tjänstkonto.

>[!TIP]
>
>Välj ett tjänstkonto som [inte upphör](https://developer.mixpanel.com/reference/service-accounts#service-account-expiration) för att få bästa praxis.

![Tjänstkonto för blandpanel](../../images/tutorials/create/mixpanel-export-events/mixpanel-service-account.png)

Skapa slutligen ett Experience Platform [schema](../../../xdm/schema/composition.md) som krävs för [!DNL Mixpanel Event Export API]. Mer information om vilka mappningar som krävs för ditt schema finns i guiden om att [skapa en [!DNL Mixpanel] källanslutning i användargränssnittet](../../tutorials/ui/create/analytics/mixpanel.md#additional-resources).

![Skapa schema](../../images/tutorials/create/mixpanel-export-events/schema.png)

## Anslut [!DNL Mixpanel] till Experience Platform med API:er

Dokumentationen nedan innehåller information om hur du ansluter [!DNL Mixpanel] till Experience Platform med API:er eller användargränssnittet:

* [Skapa en källanslutning och ett dataflöde för  [!DNL Mixpanel] med API:t för Flow Service](../../tutorials/api/create/analytics/mixpanel.md)

## Anslut [!DNL Mixpanel] till Experience Platform med användargränssnittet

* [Skapa en  [!DNL Mixpanel] källanslutning i användargränssnittet](../../tutorials/ui/create/analytics/mixpanel.md)
* [Skapa ett dataflöde för en källanslutning till en lyckad kund i användargränssnittet](../../tutorials/ui/dataflow/analytics.md)
