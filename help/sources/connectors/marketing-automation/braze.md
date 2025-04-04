---
title: Braze Currents Source Overview
description: Lär dig hur du direktuppspelar data från Braze Currents till Experience Platform.
badge: Beta
exl-id: dd304e10-26e5-4586-ab39-8fe3294b19c9
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '359'
ht-degree: 0%

---

# [!DNL Braze Currents]

>[!NOTE]
>
>Källan [!DNL Braze Currents] är i betaversion. Läs [källöversikten](../../home.md#terms-and-conditions) om du vill ha mer information om hur du använder betatecknade källor.

Med Adobe Experience Platform kan data hämtas från externa källor samtidigt som du kan strukturera, etikettera och förbättra inkommande data med hjälp av Experience Platform tjänster. Du kan importera data från en mängd olika källor, till exempel Adobe-program, molnbaserad lagring, databaser och många andra.

Experience Platform har stöd för inmatning av data från direktuppspelningsprogram. Stöd för direktuppspelningsproviders omfattar [!DNL Braze Currents].

[!DNL Braze] driver kundcentrerad interaktion mellan konsumenter och varumärken i realtid. [!DNL Braze Currents] är en dataström i realtid av engagemangshändelser från Braze-plattformen som är den mest robusta men detaljerade exporten från [!DNL Braze] -plattformen.

## Förhandskrav

För att kunna slutföra stegen i den här handboken behöver du:

* En inloggning på [Adobe Experience Platform](https://platform.adobe.com) och behörighet att skapa en ny direktuppspelningskällanslutning.
* En inloggning på din [[!DNL Braze] instrumentpanel](https://dashboard.braze.com/sign_in), en oanvänd [Aktuell anslutningslicens](https://www.braze.com/docs/user_guide/data_and_analytics/braze_currents) och behörigheter för att skapa en koppling. Mer information finns i [kraven för  [!DNL Currents]](https://www.braze.com/docs/user_guide/data_and_analytics/braze_currents/setting_up_currents/#requirements).

### Samla in nödvändiga inloggningsuppgifter

Om du vill skicka dina [!DNL Braze Currents]-data till Experience Platform måste du ange följande Experience Platform-autentiseringsuppgifter i [!DNL Braze] UI-instrumentpanelen.

| Fält | Beskrivning |
| --- | --- |
| Klient-ID | Klient-ID som är kopplat till din Experience Platform-källa. |
| Klienthemlighet | Klienthemligheten som är kopplad till din Experience Platform-källa. |
| Klient-ID | Det klient-ID som är kopplat till din Experience Platform-källa. |
| Namn på sandlåda | Sandlådan som är kopplad till din Experience Platform-källa. |
| Dataflödes-ID | Det dataflödes-ID som är kopplat till din Experience Platform-källa. |
| Slutpunkt för direktuppspelning | Den slutpunkt för direktuppspelning som är kopplad till din Experience Platform-källa. **Obs!**: [!DNL Braze] konverterar automatiskt detta till gruppströmningsslutpunkten. |

Mer information om hur du hämtar dessa värden finns i guiden [Komma igång med Experience Platform API:er](../../../landing/api-authentication.md). Mer information om hur du använder kontrollpanelen [!DNL Braze] finns i [!DNL Braze]-handboken om hur du [navigerar till aktuell information](https://www.braze.com/docs/user_guide/data_and_analytics/braze_currents/setting_up_currents/#step-2-navigate-to-currents).

## Nästa steg

Genom att läsa det här dokumentet har du slutfört de nödvändiga inställningarna för att kunna strömma data från ditt [!DNL Braze Currents]-konto till Experience Platform. Du kan nu fortsätta med guiden om att [ansluta [!DNL Braze Currents] till Experience Platform via användargränssnittet](../../tutorials/ui/create/marketing-automation/braze.md).
