---
title: Braze Currents Source Overview
description: Lär dig hur du direktuppspelar data från Braze Currents till Experience Platform.
badge: Beta
source-git-commit: 64975ccb6a44730489427cef745f3dbce5bcedf1
workflow-type: tm+mt
source-wordcount: '357'
ht-degree: 1%

---

# [!DNL Braze Currents]

>[!NOTE]
>
>The [!DNL Braze Currents] källan är i betaversion. Läs [källöversikt](../../home.md#terms-and-conditions) om du vill ha mer information om hur du använder betamärkta källor.

Med Adobe Experience Platform kan data hämtas från externa källor samtidigt som du kan strukturera, märka och förbättra inkommande data med hjälp av plattformstjänster. Du kan importera data från en mängd olika källor, till exempel Adobe-program, molnbaserad lagring, databaser och många andra.

Experience Platform har stöd för inmatning av data från direktuppspelningsprogram. Stöd för direktuppspelningsleverantörer innefattar [!DNL Braze Currents].

[!DNL Braze] möjliggör kundcentrerad interaktion mellan konsumenter och varumärken i realtid. [!DNL Braze Currents] är ett dataflöde i realtid av engagemangshändelser från Braze-plattformen som är den mest robusta men detaljerade exporten från [!DNL Braze] plattform.

## Förutsättningar

För att kunna slutföra stegen i den här handboken behöver du:

* En inloggning på [Adobe Experience Platform](https://platform.adobe.com) och behörighet att skapa en ny direktuppspelningskällanslutning.
* En inloggning på [[!DNL Braze] kontrollpanel](https://dashboard.braze.com/sign_in), en oanvänd [Aktuell anslutningslicens](https://www.braze.com/docs/user_guide/data_and_analytics/braze_currents)och behörigheter för att skapa en koppling. Mer information finns i [krav för att ställa in [!DNL Currents]](https://www.braze.com/docs/user_guide/data_and_analytics/braze_currents/setting_up_currents/#requirements).

### Samla in nödvändiga inloggningsuppgifter

Skicka [!DNL Braze Currents] data till Experience Platform måste du ange följande uppgifter för Experience Platform i [!DNL Braze] Kontrollpanel för användargränssnitt.

| Fält | Beskrivning |
| --- | --- |
| Klient-ID | Klient-ID som är kopplat till Experience Platform-källan. |
| Klienthemlighet | Klienthemligheten som är kopplad till Experience Platform-källan. |
| Klient-ID | Klient-ID som är kopplat till Experience Platform-källan. |
| Namn på sandlåda | Sandlådan som är associerad med Experience Platform-källan. |
| Dataflödes-ID | Det dataflödes-ID som är kopplat till Experience Platform-källan. |
| Slutpunkt för direktuppspelning | Den slutpunkt för direktuppspelning som är kopplad till Experience Platform-källan. **Anteckning**: [!DNL Braze] konverterar automatiskt detta till gruppströmningsslutpunkten. |

Mer information om hur du hämtar dessa värden finns i guiden [komma igång med plattforms-API:er](../../../landing/api-authentication.md). Mer information om hur du använder [!DNL Braze] kontrollpanelen, läs [!DNL Braze] guide om hur [Navigera till Aktuellt](https://www.braze.com/docs/user_guide/data_and_analytics/braze_currents/setting_up_currents/#step-2-navigate-to-currents).

## Nästa steg

Genom att läsa det här dokumentet har du slutfört de nödvändiga inställningarna för att kunna strömma data från [!DNL Braze Currents] konto till Experience Platform. Du kan nu fortsätta med guiden på [koppla [!DNL Braze Currents] till Experience Platform via användargränssnittet](../../tutorials/ui/create/marketing-automation/braze.md).