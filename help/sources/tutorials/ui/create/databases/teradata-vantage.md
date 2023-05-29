---
keywords: Experience Platform;hem;populära ämnen;Teradata Vantage
title: Skapa en Teradata Vantage-källanslutning i användargränssnittet
description: Lär dig hur du skapar en Teradata Vantage-källanslutning med Adobe Experience Platform-gränssnittet.
exl-id: 3fdb09fa-128a-477b-9144-d4ef3ed18ea6
source-git-commit: e37c00863249e677f1645266859bf40fe6451827
workflow-type: tm+mt
source-wordcount: '378'
ht-degree: 1%

---

# (Beta) Skapa en [!DNL Teradata Vantage] källanslutning i användargränssnittet

>[!NOTE]
>
> The [!DNL Teradata Vantage] källan är i betaversion. Se [Översikt över källor](../../../../home.md#terms-and-conditions) om du vill ha mer information om hur du använder betamärkta källor.

Den här självstudiekursen innehåller steg för att skapa en [!DNL Teradata Vantage] källanslutning med Adobe Experience Platform användargränssnitt.

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av följande plattformskomponenter:

* [Källor](../../../../home.md): Experience Platform tillåter att data kan hämtas från olika källor samtidigt som du kan strukturera, märka och förbättra inkommande data med hjälp av Experience Platform-tjänster.
* [Sandlådor](../../../../../sandboxes/home.md): Experience Platform tillhandahåller virtuella sandlådor som partitionerar en enda plattformsinstans i separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

### Samla in nödvändiga inloggningsuppgifter

För att komma åt [!DNL Teradata Vantage] på Platform måste du ange följande autentiseringsvärde:

| Autentiseringsuppgifter | Beskrivning |
| ---------- | ----------- |
| Anslutningssträng | En anslutningssträng är en sträng som innehåller information om en datakälla och hur du kan ansluta till den. Anslutningssträngsmönstret för [!DNL Teradata Vantage] är `DBCName={SERVER};Uid={USERNAME};Pwd={PASSWORD}`. |

Mer information om hur du kommer igång finns i [[!DNL Teradata Vantage] dokument](https://docs.teradata.com/r/Teradata-VantageTM-Advanced-SQL-Engine-Security-Administration/July-2021/Setting-Up-the-Administrative-Infrastructure/Controlling-Access-to-the-Operating-System/Working-with-OS-Level-Security-Options).

## Koppla samman [!DNL Teradata Vantage] konto

Välj **[!UICONTROL Sources]** från vänster navigering för att komma åt [!UICONTROL Sources] arbetsyta. The [!UICONTROL Catalog] I visas en mängd olika källor som du kan skapa ett konto med.

Du kan välja lämplig kategori i katalogen till vänster på skärmen. Du kan också använda sökfältet till att hitta den källa du vill arbeta med.

Under [!UICONTROL Databases] kategori, välj **[!UICONTROL Teradata Vantage]** och sedan markera **[!UICONTROL Add data]**.

![](../../../../images/tutorials/create/teradata/catalog.png)

The **[!UICONTROL Connect to Teradata Vantage]** visas. På den här sidan kan du antingen använda nya autentiseringsuppgifter eller befintliga.

### Befintligt konto

Om du vill ansluta ett befintligt konto väljer du [!DNL Teradata Vantage] konto som du vill ansluta till och välj **[!UICONTROL Next]** för att fortsätta.

![](../../../../images/tutorials/create/teradata/existing.png)

### Nytt konto

Om du använder nya autentiseringsuppgifter väljer du **[!UICONTROL New account]**. Ange ett namn, en valfri beskrivning och din [!DNL Teradata Vantage] autentiseringsuppgifter. När du är klar väljer du **[!UICONTROL Connect]** och tillåt sedan lite tid för att upprätta den nya anslutningen.

![](../../../../images/tutorials/create/teradata/new.png)

## Nästa steg

Genom att följa den här självstudiekursen har du upprättat en anslutning till ditt Teradata Vantage-konto. Du kan nu fortsätta med nästa självstudiekurs och [konfigurera ett dataflöde för att hämta data till plattformen](../../dataflow/databases.md).
