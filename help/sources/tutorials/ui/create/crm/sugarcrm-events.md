---
title: Skapa en källanslutning för SugarCRM-händelser i användargränssnittet
description: Lär dig hur du skapar en källanslutning för SugarCRM-händelser med hjälp av Adobe Experience Platform-gränssnittet.
exl-id: db346ec0-2c57-4b82-8a39-f15d4cd377d4
source-git-commit: 68c14d7b187075b4af6b019a8bd1ca2625beabde
workflow-type: tm+mt
source-wordcount: '627'
ht-degree: 0%

---

# Skapa en [!DNL SugarCRM Events]-källanslutning i användargränssnittet

I den här självstudien beskrivs hur du skapar en [!DNL SugarCRM Events]-källanslutning med Adobe Experience Platform-användargränssnittet.

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Experience Platform:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Det standardiserade ramverk som [!DNL Experience Platform] organiserar kundupplevelsedata med.
   * [Grundläggande om schemakomposition](../../../../../xdm/schema/composition.md): Lär dig mer om grundstenarna i XDM-scheman, inklusive nyckelprinciper och bästa metoder för schemakomposition.
   * [Schemaredigeraren, självstudiekurs](../../../../../xdm/tutorials/create-schema-ui.md): Lär dig hur du skapar anpassade scheman med hjälp av gränssnittet för Schemaredigeraren.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Tillhandahåller en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

Om du redan har ett giltigt [!DNL SugarCRM]-konto kan du hoppa över resten av det här dokumentet och gå vidare till självstudiekursen [Konfigurera ett dataflöde](../../dataflow/crm.md).

### Samla in nödvändiga inloggningsuppgifter

För att kunna ansluta [!DNL SugarCRM Events] till plattformen måste du ange värden för följande anslutningsegenskaper:

| Autentiseringsuppgifter | Beskrivning | Exempel |
| --- | --- | --- |
| `Host` | SugarCRM API-slutpunkten som källan ansluter till. | `developer.salesfusion.com` |
| `Username` | Användarnamn för ditt SugarCRM-utvecklarkonto. | `abc.def@example.com@sugarmarketdemo000.com` |
| `Password` | Lösenordet för ditt SugarCRM-utvecklarkonto. | `123456789` |

### Skapa ett plattformsschema för [!DNL SugarCRM]

Innan du skapar en [!DNL SugarCRM]-källanslutning måste du också se till att du först skapar ett plattformsschema som kan användas för källan. I självstudiekursen [Skapa ett plattformsschema](../../../../../xdm/schema/composition.md) finns mer information om hur du skapar ett schema.

![Skärmbild för plattformsgränssnitt som visar ett exempelschema för SugarCRM-händelser](../../../../images/tutorials/create/sugarcrm-events/sugarcrm-schema-events.png)

>[!WARNING]
>
>När du mappar schemat måste du också mappa de obligatoriska `event_id`- och `timestamp`-fälten som krävs av plattformen.

## Anslut ditt [!DNL SugarCRM Events]-konto

I plattformsgränssnittet väljer du **[!UICONTROL Sources]** i det vänstra navigeringsfältet för att komma åt arbetsytan i [!UICONTROL Sources]. På skärmen [!UICONTROL Catalog] visas en mängd olika källor som du kan använda för att skapa ett konto.

Du kan välja lämplig kategori i katalogen till vänster på skärmen. Du kan också hitta den källa du vill arbeta med med med sökalternativet.

Under kategorin *CRM* väljer du **[!UICONTROL SugarCRM Events]** och sedan **[!UICONTROL Add data]**.

![Skärmbild för plattformsgränssnitt för katalog med händelsekort för SugarCRM](../../../../images/tutorials/create/sugarcrm-events/catalog-sugarcrm-events.png)

Sidan **[!UICONTROL Connect SugarCRM Events account]** visas. På den här sidan kan du antingen använda nya autentiseringsuppgifter eller befintliga.

### Befintligt konto

Om du vill använda ett befintligt konto väljer du det [!DNL SugarCRM Events]-konto som du vill skapa ett nytt dataflöde med och väljer sedan **[!UICONTROL Next]** för att fortsätta.

![Skärmbild för plattformsgränssnitt för Connect SugarCRM Events-konto med ett befintligt konto](../../../../images/tutorials/create/sugarcrm-events/existing.png)

### Nytt konto

Om du skapar ett nytt konto väljer du **[!UICONTROL New account]** och anger sedan ett namn, en valfri beskrivning och dina autentiseringsuppgifter. När du är klar väljer du **[!UICONTROL Connect to source]** och tillåt sedan lite tid för att upprätta den nya anslutningen.

![Skärmbild för användargränssnittet för Connect SugarCRM-händelser med ett nytt konto](../../../../images/tutorials/create/sugarcrm-events/new.png)

## Nästa steg

Genom att följa den här självstudiekursen har du upprättat en anslutning till ditt [!DNL SugarCRM Events]-konto. Du kan nu fortsätta till nästa självstudiekurs och [konfigurera ett dataflöde för att hämta data till plattformen](../../dataflow/crm.md).

## Ytterligare resurser

Avsnitten nedan innehåller ytterligare resurser som du kan referera till när du använder källan [!DNL SugarCRM].

### Guardrails {#guardrails}

Begränsningsfrekvensen för [!DNL SugarCRM] API är 90 anrop per minut eller 2 000 anrop per dag, beroende på vilket som inträffar först. Begränsningen har dock kringgåtts genom att en parameter läggs till i anslutningsspecifikationen som fördröjer begärandetiden så att hastighetsgränsen aldrig uppnås.

### Validering {#validation}

Följ stegen nedan för att verifiera att du har konfigurerat källan och att [!DNL SugarCRM Events] data importeras korrekt:

* I plattformsgränssnittet väljer du **[!UICONTROL View Dataflows]** bredvid kortmenyn [!DNL SugarCRM Events] i källkatalogen. Välj sedan **[!UICONTROL Preview dataset]** för att verifiera de data som har importerats.

* Beroende på vilken objekttyp du arbetar med kan du verifiera aggregerade data mot antalet som visas på sidan [!DNL SugarMarket]-händelser nedan:

![Skärmbild från sidan SugarMarket-konton som visar en lista över konton](../../../../images/tutorials/create/sugarcrm-events/sugarmarket-events.png)

>[!NOTE]
>
>Sidorna [!DNL SugarMarket] innehåller inte antalet borttagna objekt. Data som hämtas via den här källan kommer dock även att innehålla det borttagna antalet, som markeras med en borttagen flagga.
