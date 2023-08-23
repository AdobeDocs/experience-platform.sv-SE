---
title: Skapa en källanslutning för SugarCRM-händelser i användargränssnittet
description: Lär dig hur du skapar en källanslutning för SugarCRM-händelser med hjälp av Adobe Experience Platform-gränssnittet.
exl-id: db346ec0-2c57-4b82-8a39-f15d4cd377d4
source-git-commit: 68c14d7b187075b4af6b019a8bd1ca2625beabde
workflow-type: tm+mt
source-wordcount: '625'
ht-degree: 1%

---

# Skapa en [!DNL SugarCRM Events] källanslutning i användargränssnittet

Den här självstudiekursen innehåller steg för att skapa en [!DNL SugarCRM Events] källanslutning med Adobe Experience Platform användargränssnitt.

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Experience Platform:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Det standardiserade ramverk som [!DNL Experience Platform] organiserar kundupplevelsedata.
   * [Grunderna för schemakomposition](../../../../../xdm/schema/composition.md): Lär dig mer om de grundläggande byggstenarna i XDM-scheman, inklusive viktiga principer och bästa praxis när det gäller schemakomposition.
   * [Schemaredigeraren, genomgång](../../../../../xdm/tutorials/create-schema-ui.md): Lär dig hur du skapar anpassade scheman med hjälp av gränssnittet i Schemaredigeraren.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

Om du redan har en giltig [!DNL SugarCRM] kan du hoppa över resten av dokumentet och gå vidare till självstudiekursen om [konfigurera ett dataflöde](../../dataflow/crm.md).

### Samla in nödvändiga inloggningsuppgifter

För att kunna ansluta [!DNL SugarCRM Events] till Platform måste du ange värden för följande anslutningsegenskaper:

| Autentiseringsuppgifter | Beskrivning | Exempel |
| --- | --- | --- |
| `Host` | SugarCRM API-slutpunkten som källan ansluter till. | `developer.salesfusion.com` |
| `Username` | Användarnamn för ditt SugarCRM-utvecklarkonto. | `abc.def@example.com@sugarmarketdemo000.com` |
| `Password` | Lösenordet för ditt SugarCRM-utvecklarkonto. | `123456789` |

### Skapa ett plattformsschema för [!DNL SugarCRM]

Innan du skapar [!DNL SugarCRM] källanslutning måste du också se till att du först skapar ett plattformsschema som kan användas för källan. Se självstudiekursen om [skapa ett plattformsschema](../../../../../xdm/schema/composition.md) om du vill ha omfattande anvisningar om hur du skapar ett schema.

![Skärmbild för användargränssnittet för plattformen visar ett exempelschema för SugarCRM-händelser](../../../../images/tutorials/create/sugarcrm-events/sugarcrm-schema-events.png)

>[!WARNING]
>
>När du mappar schemat måste du också mappa det obligatoriska `event_id` och `timestamp` fält som krävs av Platform.

## Koppla samman [!DNL SugarCRM Events] konto

Välj **[!UICONTROL Sources]** från det vänstra navigeringsfältet för att komma åt [!UICONTROL Sources] arbetsyta. The [!UICONTROL Catalog] visas en mängd olika källor som du kan använda för att skapa ett konto.

Du kan välja lämplig kategori i katalogen till vänster på skärmen. Du kan också hitta den källa du vill arbeta med med med sökalternativet.

Under *CRM* kategori, välj **[!UICONTROL SugarCRM Events]** och sedan markera **[!UICONTROL Add data]**.

![Skärmbild för plattformsgränssnitt för katalog med händelsekort för SugarCRM](../../../../images/tutorials/create/sugarcrm-events/catalog-sugarcrm-events.png)

The **[!UICONTROL Connect SugarCRM Events account]** visas. På den här sidan kan du antingen använda nya autentiseringsuppgifter eller befintliga.

### Befintligt konto

Välj [!DNL SugarCRM Events] konto som du vill skapa ett nytt dataflöde med och sedan välja **[!UICONTROL Next]** för att fortsätta.

![Skärmbild för användargränssnittet för Connect SugarCRM Events-konto med ett befintligt konto](../../../../images/tutorials/create/sugarcrm-events/existing.png)

### Nytt konto

Om du skapar ett nytt konto väljer du **[!UICONTROL New account]** och ange sedan ett namn, en valfri beskrivning och dina uppgifter. När du är klar väljer du **[!UICONTROL Connect to source]** och tillåt sedan lite tid för att upprätta den nya anslutningen.

![Skärmbild för användargränssnittet för Connect SugarCRM Events-konto med ett nytt konto](../../../../images/tutorials/create/sugarcrm-events/new.png)

## Nästa steg

Genom att följa den här självstudien har du upprättat en anslutning till [!DNL SugarCRM Events] konto. Du kan nu fortsätta med nästa självstudiekurs och [konfigurera ett dataflöde för att hämta data till plattformen](../../dataflow/crm.md).

## Ytterligare resurser

I avsnitten nedan finns ytterligare resurser som du kan använda när du använder [!DNL SugarCRM] källa.

### Guardrails {#guardrails}

The [!DNL SugarCRM] API-begränsningsfrekvensen är 90 anrop per minut eller 2 000 anrop per dag, beroende på vilket som inträffar först. Begränsningen har dock kringgåtts genom att en parameter läggs till i anslutningsspecifikationen som fördröjer begärandetiden så att hastighetsgränsen aldrig uppnås.

### Validering {#validation}

För att verifiera att du har konfigurerat källan och [!DNL SugarCRM Events] data importeras, följ stegen nedan:

* Välj **[!UICONTROL View Dataflows]** bredvid [!DNL SugarCRM Events] kortmenyn i källkatalogen. Nästa, välj **[!UICONTROL Preview dataset]** för att verifiera de data som har importerats.

* Beroende på vilken objekttyp du arbetar med kan du verifiera aggregerade data mot antalet som visas på [!DNL SugarMarket] Händelsesida nedan:

![Skärmbild från sidan SugarMarket-konton med en lista över konton](../../../../images/tutorials/create/sugarcrm-events/sugarmarket-events.png)

>[!NOTE]
>
>The [!DNL SugarMarket] Sidorna innehåller inte antalet borttagna objekt. Data som hämtas via den här källan kommer dock även att innehålla det borttagna antalet, som markeras med en borttagen flagga.
