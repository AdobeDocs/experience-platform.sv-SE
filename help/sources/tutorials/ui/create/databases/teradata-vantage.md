---
keywords: Experience Platform;hem;populära ämnen;Teradata Vantage
title: Skapa en Teradata Vantage-källanslutning i användargränssnittet
description: Lär dig hur du skapar en Teradata Vantage-källanslutning med Adobe Experience Platform-gränssnittet.
exl-id: 3fdb09fa-128a-477b-9144-d4ef3ed18ea6
source-git-commit: 625a7959f48a0b16c3228d4555e046b5f67c51b7
workflow-type: tm+mt
source-wordcount: '394'
ht-degree: 1%

---

# Skapa en [!DNL Teradata Vantage] källanslutning i användargränssnittet

Den här självstudiekursen innehåller steg för att skapa en [!DNL Teradata Vantage] källanslutning med Adobe Experience Platform användargränssnitt.

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av följande plattformskomponenter:

* [Källor](../../../../home.md): Experience Platform tillåter att data kan hämtas från olika källor samtidigt som du kan strukturera, märka och förbättra inkommande data med hjälp av Experience Platform-tjänster.
* [Sandlådor](../../../../../sandboxes/home.md): Experience Platform tillhandahåller virtuella sandlådor som partitionerar en enda plattformsinstans i separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

### Samla in nödvändiga inloggningsuppgifter

För att få åtkomst till [!DNL Teradata Vantage] på Platform måste du ange följande autentiseringsvärde:

| Autentiseringsuppgifter | Beskrivning |
| ---------- | ----------- |
| Anslutningssträng | En anslutningssträng är en sträng som innehåller information om en datakälla och hur du kan ansluta till den. Anslutningssträngsmönstret för [!DNL Teradata Vantage] är `DBCName={SERVER};Uid={USERNAME};Pwd={PASSWORD}`. |

Mer information om hur du kommer igång finns i [[!DNL Teradata Vantage] dokument](https://docs.teradata.com/r/Teradata-VantageTM-Advanced-SQL-Engine-Security-Administration/July-2021/Setting-Up-the-Administrative-Infrastructure/Controlling-Access-to-the-Operating-System/Working-with-OS-Level-Security-Options).

## Koppla samman [!DNL Teradata Vantage] konto

Välj **[!UICONTROL Sources]** från vänster navigering för att komma åt [!UICONTROL Sources] arbetsyta. Du kan välja lämplig kategori i katalogen till vänster på skärmen. Du kan också hitta den källa du vill arbeta med med med sökalternativet.

Under [!UICONTROL Databases] kategori, välj **[!UICONTROL Teradata Vantage]** och sedan **[!UICONTROL Set up]**.

>[!TIP]
>
>Källor i källkatalogen visas **[!UICONTROL Set up]** när en viss källa ännu inte har något autentiserat konto. När det finns ett autentiserat konto ändras det här alternativet till **[!UICONTROL Add data]**.

![Källkatalogen med Teradata Vantage-källan markerad.](../../../../images/tutorials/create/teradata/catalog.png)

The **[!UICONTROL Connect to Teradata Vantage]** visas. På den här sidan kan du antingen använda nya autentiseringsuppgifter eller befintliga.

### Befintligt konto

Välj [!DNL Teradata Vantage] konto som du vill ansluta till och välj **[!UICONTROL Next]** för att fortsätta.

![Den befintliga kontosidan på arbetsytan för källor.](../../../../images/tutorials/create/teradata/existing.png)

### Nytt konto

Om du använder nya autentiseringsuppgifter väljer du **[!UICONTROL New account]**. Ange ett namn, en valfri beskrivning och din [!DNL Teradata Vantage] autentiseringsuppgifter. När du är klar väljer du **[!UICONTROL Connect]** och tillåt sedan lite tid för att upprätta den nya anslutningen.

![Det nya gränssnittet för att skapa konton i källarbetsytan.](../../../../images/tutorials/create/teradata/new.png)

## Nästa steg

Genom att följa den här självstudiekursen har du upprättat en anslutning till ditt Teradata Vantage-konto. Du kan nu fortsätta med nästa självstudiekurs och [konfigurera ett dataflöde för att hämta data till plattformen](../../dataflow/databases.md).
