---
title: Skapa en källanslutning till SugarCRM-konton och kontakter i användargränssnittet
description: Lär dig hur du skapar en källanslutning till SugarCRM-konton och kontakter med hjälp av Adobe Experience Platform användargränssnitt.
source-git-commit: d4b5c3b897371eea591925d071afc120a3f246d7
workflow-type: tm+mt
source-wordcount: '756'
ht-degree: 1%

---

# (Beta) Skapa en [!DNL SugarCRM Accounts & Contacts] källanslutning i användargränssnittet

>[!NOTE]
>
>The [!DNL SugarCRM Accounts & Contacts] källan är i betaversion. Se [källöversikt](../../../../home.md#terms-and-conditions) om du vill ha mer information om hur du använder betamärkta källor.

Den här självstudiekursen innehåller steg för att skapa en [!DNL SugarCRM Accounts & Contacts] källanslutning med Adobe Experience Platform användargränssnitt.

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Experience Platform:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Det standardiserade ramverk som [!DNL Experience Platform] organiserar kundupplevelsedata.
   * [Grunderna för schemakomposition](../../../../../xdm/schema/composition.md): Lär dig mer om de grundläggande byggstenarna i XDM-scheman, inklusive viktiga principer och bästa praxis när det gäller schemakomposition.
   * [Schemaredigeraren, genomgång](../../../../../xdm/tutorials/create-schema-ui.md): Lär dig hur du skapar anpassade scheman med hjälp av gränssnittet för Schemaredigeraren.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

Om du redan har en giltig [!DNL SugarCRM] kan du hoppa över resten av dokumentet och gå vidare till självstudiekursen om [konfigurera ett dataflöde](../../dataflow/crm.md).

### Samla in nödvändiga inloggningsuppgifter

För att kunna ansluta [!DNL SugarCRM Accounts & Contacts] till Platform måste du ange värden för följande anslutningsegenskaper:

| Autentiseringsuppgifter | Beskrivning | Exempel |
| --- | --- | --- |
| `Host` | SugarCRM API-slutpunkten som källan ansluter till. | `developer.salesfusion.com` |
| `Username` | Användarnamn för ditt SugarCRM-utvecklarkonto. | `abc.def@example.com@sugarmarketdemo000.com` |
| `Password` | Lösenordet för ditt SugarCRM-utvecklarkonto. | `123456789` |

### Skapa ett plattformsschema

Innan du skapar en [!DNL SugarCRM] källanslutning måste du också se till att du först skapar ett plattformsschema som kan användas för källan. Se självstudiekursen om [skapa ett plattformsschema](../../../../../xdm/schema/composition.md) om du vill ha omfattande anvisningar om hur du skapar ett schema.

The [!DNL SugarCRM Accounts & Contacts] har stöd för flera API:er. Det innebär att du måste skapa ett separat schema, beroende på vilken objekttyp du använder. Se exemplen nedan för både konton och kontaktkartor:

>[!BEGINTABS]

>[!TAB Konton]

![Skärmbild av användargränssnittet för plattformen med ett exempelschema för konton](../../../../images/tutorials/create/sugarcrm-accounts-contacts/sugarcrm-schema-accounts.png)

>[!TAB Kontakter]

![Skärmbild för plattformsgränssnitt som visar ett exempelschema för kontakter](../../../../images/tutorials/create/sugarcrm-accounts-contacts/sugarcrm-schema-contacts.png)

>[!ENDTABS]

## Koppla samman [!DNL SugarCRM Accounts & Contacts] konto

Välj **[!UICONTROL Sources]** från det vänstra navigeringsfältet för att komma åt [!UICONTROL Sources] arbetsyta. The [!UICONTROL Catalog] visas en mängd olika källor som du kan använda för att skapa ett konto.

Du kan välja lämplig kategori i katalogen till vänster på skärmen. Du kan också hitta den källa du vill arbeta med med med sökalternativet.

Under *CRM* kategori, välj **[!UICONTROL SugarCRM Accounts & Contacts]** och sedan markera **[!UICONTROL Add data]**.

![Skärmbild för användargränssnitt för plattform för katalog med SugarCRM-kort för konton och kontakter](../../../../images/tutorials/create/sugarcrm-accounts-contacts/catalog-sugarcrm-accounts-contacts.png)

The **[!UICONTROL Connect SugarCRM Accounts & Contacts account]** visas. På den här sidan kan du antingen använda nya autentiseringsuppgifter eller befintliga.

### Befintligt konto

Om du vill använda ett befintligt konto väljer du [!DNL SugarCRM Accounts & Contacts] konto som du vill skapa ett nytt dataflöde med och sedan välja **[!UICONTROL Next]** för att fortsätta.

![Skärmbild för användargränssnittet för Connect SugarCRM-konton och kontaktkonton med ett befintligt konto](../../../../images/tutorials/create/sugarcrm-accounts-contacts/existing.png)

### Nytt konto

Om du skapar ett nytt konto väljer du **[!UICONTROL New account]** och ange sedan ett namn, en valfri beskrivning och dina uppgifter. När du är klar väljer du **[!UICONTROL Connect to source]** och tillåt sedan lite tid för att upprätta den nya anslutningen.

![Skärmbild för användargränssnittet för Connect SugarCRM-konton och kontaktkonton med ett nytt konto](../../../../images/tutorials/create/sugarcrm-accounts-contacts/new.png)

### Markera data

Slutligen måste du välja den objekttyp som du vill importera till plattformen.

| Objekttyp | Beskrivning |
| --- | --- |
| `Accounts` | De företag som din organisation har en relation med. |
| `Contacts` | De enskilda personer som din organisation har en etablerad relation med. |

>[!BEGINTABS]

>[!TAB Konton]

![Skärmbild för användargränssnittet för SugarCRM-konton och kontakter som visar konfigurationen med alternativet Konto valt](../../../../images/tutorials/create/sugarcrm-accounts-contacts/configuration-accounts.png)

>[!TAB Kontakter]

![Skärmbild för användargränssnitt för plattform för SugarCRM-konton och kontakter som visar konfigurationen med alternativet Kontakter valt](../../../../images/tutorials/create/sugarcrm-accounts-contacts/configuration-contacts.png)

>[!ENDTABS]

## Nästa steg

Genom att följa den här självstudiekursen har du upprättat en anslutning till [!DNL SugarCRM Accounts & Contacts] konto. Du kan nu fortsätta med nästa självstudiekurs och [konfigurera ett dataflöde för att hämta data till plattformen](../../dataflow/crm.md).

## Ytterligare resurser

I avsnitten nedan finns ytterligare resurser som du kan använda när du använder [!DNL SugarCRM] källa.

### Guardrails {#guardrails}

The [!DNL SugarCRM] API-begränsningsfrekvensen är 90 anrop per minut eller 2 000 anrop per dag, beroende på vilket som inträffar först. Begränsningen har dock kringgåtts genom att en parameter läggs till i anslutningsspecifikationen som fördröjer begärandetiden så att hastighetsgränsen aldrig uppnås.

### Validering {#validation}

För att verifiera att du har konfigurerat källan och [!DNL SugarCRM Accounts & Contacts] data importeras, följ stegen nedan:

* Välj **[!UICONTROL View Dataflows]** bredvid [!DNL SugarCRM Accounts & Contacts] kortmenyn i källkatalogen. Nästa, välj **[!UICONTROL Preview dataset]** för att verifiera de data som har importerats.

* Beroende på vilken objekttyp du arbetar med kan du verifiera aggregerade data mot antalet som visas på [!DNL SugarMarket] Konton eller Kontakter nedan:

>[!BEGINTABS]

>[!TAB Konton]

![Skärmbild från sidan SugarMarket-konton med en lista över konton](../../../../images/tutorials/create/sugarcrm-accounts-contacts/sugarmarket-accounts.png)

>[!TAB Kontakter]

![Skärmbild från sidan SugarMarket Contacts med en lista över kontakter](../../../../images/tutorials/create/sugarcrm-accounts-contacts/sugarmarket-contacts.png)

>[!ENDTABS]

>[!NOTE]
>
>The [!DNL SugarMarket] sidor innehåller inte antalet borttagna objekt. Data som hämtas via den här källan kommer dock även att innehålla det borttagna antalet, som markeras med en borttagen flagga.