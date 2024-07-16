---
title: Skapa ett dataflöde för Braze-data i användargränssnittet
description: Lär dig hur du skapar ett dataflöde för ditt Braze-konto med hjälp av användargränssnittet i Adobe Experience Platform.
last-substantial-update: 2024-01-30T00:00:00Z
badge: Beta
exl-id: 6e94414a-176c-4810-80ff-02cf9e797756
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '683'
ht-degree: 0%

---

# Skapa en [!DNL Braze Currents]-källanslutning i användargränssnittet

>[!NOTE]
>
>Källan [!DNL Braze Currents] är i betaversion. Läs [källöversikten](../../../../home.md#terms-and-conditions) om du vill ha mer information om hur du använder betatecknade källor.

[!DNL Braze] driver kundcentrerad interaktion mellan konsumenter och varumärken i realtid. [!DNL Braze Currents] är en dataström i realtid av engagemangshändelser från Braze-plattformen som är den mest robusta men detaljerade exporten från [!DNL Braze] -plattformen.

Läs följande självstudiekurs om du vill veta mer om hur du kan skicka interaktionshändelsedata från ditt [!DNL Braze]-konto till Adobe Experience Platform i användargränssnittet.

## Förhandskrav

För att kunna slutföra stegen i den här handboken behöver du:

* En inloggning på [Adobe Experience Platform](https://platform.adobe.com) och behörighet att skapa en ny direktuppspelningskällanslutning.
* En inloggning på din [[!DNL Braze] instrumentpanel](https://dashboard.braze.com/sign_in), en oanvänd [Aktuell anslutningslicens](https://www.braze.com/docs/user_guide/data_and_analytics/braze_currents) och behörigheter för att skapa en koppling. Mer information finns i [kraven för  [!DNL Currents]](https://www.braze.com/docs/user_guide/data_and_analytics/braze_currents/setting_up_currents/#requirements).

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Det standardiserade ramverk som [!DNL Experience Platform] organiserar kundupplevelsedata med.
   * [Grundläggande om schemakomposition](../../../../../xdm/schema/composition.md): Lär dig mer om grundstenarna i XDM-scheman, inklusive nyckelprinciper och bästa metoder för schemakomposition.
   * [Schemaredigeraren, självstudiekurs](../../../../../xdm/tutorials/create-schema-ui.md): Lär dig hur du skapar anpassade scheman med hjälp av gränssnittet för Schemaredigeraren.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Tillhandahåller en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

Den här självstudiekursen kräver också en fungerande förståelse för [[!DNL Braze] Aktuella](https://www.braze.com/docs/user_guide/data_and_analytics/braze_currents).

Om du redan har en [!DNL Braze]-anslutning kan du hoppa över resten av det här dokumentet och gå vidare till självstudiekursen [Konfigurera ett dataflöde](../../dataflow/marketing-automation.md).

## Anslut ditt [!DNL Braze]-konto till Experience Platform

I plattformsgränssnittet väljer du **[!UICONTROL Sources]** i den vänstra navigeringen för att komma åt arbetsytan i [!UICONTROL Sources]. Du kan välja lämplig kategori i katalogen till vänster på skärmen. Du kan också hitta den källa du vill arbeta med med med sökalternativet.

Under kategorin *Marknadsföringsautomatisering* väljer du **[!UICONTROL Braze Currents]** och sedan **[!UICONTROL Add data]**.

![Källkatalogen i användargränssnittet i Experience Platform med källan för Braze Currents markerad.](../../../../images/tutorials/create/braze/catalog.png)

Ladda sedan upp den tillhandahållna exempelfilen [Braze Currents](https://github.com/Appboy/currents-examples/blob/master/sample-data/Adobe/adobe_examples.json). Den här filen innehåller alla fält som Braze kan skicka som en del av en händelse.

![Skärmen Lägg till data.](../../../../images/tutorials/create/braze/select-data.png)

När filen har överförts måste du ange dataflödesinformation, inklusive information om datauppsättningen och det schema som du mappar till.
![Skärmen &quot;Dataflödesdetaljer&quot; markerar &quot;Datauppsättningsdetaljer&quot;.](../../../../images/tutorials/create/braze/dataflow-detail.png)

Konfigurera sedan mappningen för dina data med mappningsgränssnittet.

![Skärmen Mappning.](../../../../images/tutorials/create/braze/mapping.png)

>[!IMPORTANT]
>
>Hjärntidsstämplar anges inte i millisekunder utan i sekunder. För att tidsstämplarna i Experience Platform ska visas korrekt måste du skapa beräkningsfält i millisekunder. En beräkning av &quot;time * 1000&quot; konverteras korrekt till millisekunder, vilket är lämpligt för mappning till ett tidsstämpelfält i Experience Platform.
>
>![Skapar ett beräknat fält för tidsstämpel ](../../../../images/tutorials/create/braze/create-calculated-field.png)

### Samla in nödvändiga inloggningsuppgifter

När anslutningen har skapats måste du samla in följande värden för autentiseringsuppgifter, som du sedan anger i Braze Dashboard för att skicka data till Experience Platform. Mer information finns i [!DNL Braze] [handboken om hur du navigerar till Valutor](https://www.braze.com/docs/user_guide/data_and_analytics/braze_currents/setting_up_currents/#step-2-navigate-to-currents).

| Fält | Beskrivning |
| --- | --- |
| Klient-ID | Klient-ID som är kopplat till Experience Platform-källan. |
| Klienthemlighet | Klienthemligheten som är kopplad till Experience Platform-källan. |
| Klient-ID | Klient-ID som är kopplat till Experience Platform-källan. |
| Namn på sandlåda | Sandlådan som är associerad med Experience Platform-källan. |
| Dataflödes-ID | Det dataflödes-ID som är kopplat till Experience Platform-källan. |
| Slutpunkt för direktuppspelning | Den slutpunkt för direktuppspelning som är kopplad till Experience Platform-källan. **Obs!**: [!DNL Braze] konverterar automatiskt detta till gruppströmningsslutpunkten. |

### Konfigurera [!DNL Braze Currents] att strömma data till datakällan

I [!DNL Braze Dashboard] går du till Partnerintegreringar **->** Dataexport och väljer **[!DNL Create New Current]**. Du uppmanas att ange ett namn för kopplingen, kontaktinformation för meddelanden om anslutningen och de autentiseringsuppgifter som anges ovan. Markera de händelser som du vill ta emot, konfigurera eventuellt önskade fältundantag/omvandlingar och välj sedan **[!DNL Launch Current]**.

## Nästa steg

Genom att följa den här självstudiekursen har du upprättat en anslutning till ditt [!DNL Braze]-konto. Du kan nu fortsätta med nästa självstudiekurs och [konfigurera ett dataflöde för att få in data från automatiseringssystemet för marknadsföring i [!DNL Platform]](../../dataflow/marketing-automation.md).
