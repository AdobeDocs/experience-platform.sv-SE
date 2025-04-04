---
title: Skapa ett dataflöde för Braze-data i användargränssnittet
description: Lär dig hur du skapar ett dataflöde för ditt Braze-konto med hjälp av användargränssnittet i Adobe Experience Platform.
last-substantial-update: 2024-01-30T00:00:00Z
badge: Beta
exl-id: 6e94414a-176c-4810-80ff-02cf9e797756
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '971'
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

## Skapa ett XDM-schema

>[!TIP]
>
>Du måste skapa ett XDM-schema (Experience Data Model) om det är första gången du skapar en [!DNL Braze Currents]-anslutning. Om du redan har skapat ett schema för [!DNL Braze Currents] kan du hoppa över det här steget och fortsätta med att [ansluta ditt konto till Experience Platform](#connect).

Använd den vänstra navigeringen i användargränssnittet för Experience Platform och välj sedan **[!UICONTROL Schemas]** för att komma åt arbetsytan i [!UICONTROL Schemas]. Välj sedan **[!UICONTROL Create schema]** och sedan **[!UICONTROL Experience Event]**. Välj **[!UICONTROL Next]** om du vill fortsätta.

![Ett slutfört schema.](../../../../images/tutorials/create/braze/schema.png)

Ange ett namn och en beskrivning för ditt schema. Använd sedan panelen [!UICONTROL Composition] för att konfigurera dina schemaattribut. Under [!UICONTROL Field groups] väljer du **[!UICONTROL Add]** och lägger till fältgruppen [!UICONTROL Braze Currents User Event]. När du är klar väljer du **[!UICONTROL Save]**.

Mer information om scheman finns i guiden för att [skapa scheman i användargränssnittet](../../../../../xdm/tutorials/create-schema-ui.md).

## Anslut ditt [!DNL Braze]-konto till Experience Platform {#connect}

I Experience Platform-gränssnittet väljer du **[!UICONTROL Sources]** i den vänstra navigeringen för att komma åt arbetsytan i [!UICONTROL Sources]. Du kan välja lämplig kategori i katalogen till vänster på skärmen. Du kan också hitta den källa du vill arbeta med med med sökalternativet.

Under kategorin *Marknadsföringsautomatisering* väljer du **[!UICONTROL Braze Currents]** och sedan **[!UICONTROL Add data]**.

![Källkatalogen i Experience Platform-användargränssnittet med källan Braze Currents markerad.](../../../../images/tutorials/create/braze/catalog.png)

Ladda sedan upp den tillhandahållna exempelfilen [Braze Currents](https://github.com/Appboy/currents-examples/blob/master/sample-data/Adobe/adobe_examples.json). Den här filen innehåller alla fält som Braze kan skicka som en del av en händelse.

![Skärmen Lägg till data.](../../../../images/tutorials/create/braze/select-data.png)

När filen har överförts måste du ange dataflödesinformation, inklusive information om datauppsättningen och det schema som du mappar till.  Om det här är första gången du ansluter en Braze Currents-källa skapar du en ny datauppsättning.  I annat fall kan du använda alla befintliga datauppsättningar som refererar till Braze-schemat.  Om du skapar en ny datauppsättning använder du det schema som vi skapade i föregående avsnitt.
![Skärmen &quot;Dataflödesdetaljer&quot; markerar &quot;Datauppsättningsdetaljer&quot;.](../../../../images/tutorials/create/braze/dataflow-detail.png)

Konfigurera sedan mappningen för dina data med mappningsgränssnittet.

![Skärmen Mappning.](../../../../images/tutorials/create/braze/mapping_errors.png)

Mappningen kommer att innehålla följande problem som behöver åtgärdas.

I källdata mappas *id* felaktigt till *_braze.appID*. Du måste ändra målmappningsfältet till *_id* på schemats rotnivå. Kontrollera sedan att *properties.is_amp* mappas till *_braze.messaging.email.isAMP*.

Ta sedan bort mappningen *time* till *timestamp*, markera ikonen Lägg till (`+`) och välj **[!UICONTROL Add calculated field]**. Ange *time \* 1000* i den angivna rutan och välj **[!UICONTROL Save]**.

När det nya beräknade fältet har lagts till väljer du **[!UICONTROL Map target field]** bredvid det nya källfältet och mappar det till *timestamp* på schemats rotnivå. Välj sedan **[!UICONTROL Validate]** för att se till att du inte har fler fel.

>[!IMPORTANT]
>
>Hjärntidsstämplar anges inte i millisekunder utan i sekunder. För att tidsstämplarna i Experience Platform ska kunna visas korrekt måste du skapa beräkningsfält i millisekunder. En beräkning av &quot;time * 1000&quot; konverteras korrekt till millisekunder, vilket är lämpligt för mappning till ett tidsstämpelfält i Experience Platform.
>
>![Skapar ett beräknat fält för tidsstämpel ](../../../../images/tutorials/create/braze/create-calculated-field.png)

![Mappningen utan fel.](../../../../images/tutorials/create/braze/completed_mapping.png)

När du är klar väljer du **[!UICONTROL Next]**. Använd granskningssidan för att bekräfta informationen om dataflödet och välj sedan **[!UICONTROL Finish]**.

### Samla in nödvändiga inloggningsuppgifter

När anslutningen har skapats måste du samla in följande inloggningsvärden som du sedan anger i Braze Dashboard för att skicka data till Experience Platform. Mer information finns i [!DNL Braze] [handboken om hur du navigerar till Valutor](https://www.braze.com/docs/user_guide/data_and_analytics/braze_currents/setting_up_currents/#step-2-navigate-to-currents).

| Fält | Beskrivning |
| --- | --- |
| Klient-ID | Klient-ID som är kopplat till din Experience Platform-källa. |
| Klienthemlighet | Klienthemligheten som är kopplad till din Experience Platform-källa. |
| Klient-ID | Det klient-ID som är kopplat till din Experience Platform-källa. |
| Namn på sandlåda | Sandlådan som är kopplad till din Experience Platform-källa. |
| Dataflödes-ID | Det dataflödes-ID som är kopplat till din Experience Platform-källa. |
| Slutpunkt för direktuppspelning | Den slutpunkt för direktuppspelning som är kopplad till din Experience Platform-källa. **Obs!**: [!DNL Braze] konverterar automatiskt detta till gruppströmningsslutpunkten. |

### Konfigurera [!DNL Braze Currents] att strömma data till datakällan

I [!DNL Braze Dashboard] går du till Partnerintegreringar **->** Dataexport och väljer **[!DNL Create New Current]**. Du uppmanas att ange ett namn för kopplingen, kontaktinformation för meddelanden om anslutningen och de autentiseringsuppgifter som anges ovan. Markera de händelser som du vill ta emot, konfigurera eventuellt önskade fältundantag/omvandlingar och välj sedan **[!DNL Launch Current]**.

## Nästa steg

Genom att följa den här självstudiekursen har du upprättat en anslutning till ditt [!DNL Braze]-konto. Du kan nu fortsätta med nästa självstudiekurs och [konfigurera ett dataflöde för att få in data från automatiseringssystemet för marknadsföring i [!DNL Experience Platform]](../../dataflow/marketing-automation.md).
