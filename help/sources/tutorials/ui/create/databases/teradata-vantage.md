---
keywords: Experience Platform;home;populära topics;Teradata Vantage
title: Skapa en Teradata Vantage Source-anslutning i användargränssnittet
description: Lär dig hur du skapar en Teradata Vantage-källanslutning med Adobe Experience Platform-gränssnittet.
exl-id: 3fdb09fa-128a-477b-9144-d4ef3ed18ea6
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '399'
ht-degree: 0%

---

# Skapa en [!DNL Teradata Vantage]-källanslutning i användargränssnittet

I den här självstudiekursen beskrivs hur du skapar en [!DNL Teradata Vantage]-källanslutning med Adobe Experience Platform-användargränssnittet.

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Experience Platform:

* [Källor](../../../../home.md): Med Experience Platform kan data hämtas från olika källor samtidigt som du kan strukturera, etikettera och förbättra inkommande data med hjälp av Experience Platform tjänster.
* [Sandlådor](../../../../../sandboxes/home.md): Experience Platform tillhandahåller virtuella sandlådor som partitionerar en enda Experience Platform-instans till separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

### Samla in nödvändiga inloggningsuppgifter

För att få åtkomst till ditt [!DNL Teradata Vantage]-konto på Experience Platform måste du ange följande autentiseringsvärde:

| Autentiseringsuppgifter | Beskrivning |
| ---------- | ----------- |
| Anslutningssträng | En anslutningssträng är en sträng som innehåller information om en datakälla och hur du kan ansluta till den. Anslutningssträngsmönstret för [!DNL Teradata Vantage] är `DBCName={SERVER};Uid={USERNAME};Pwd={PASSWORD}`. |

Mer information om hur du kommer igång finns i det här [[!DNL Teradata Vantage] dokumentet](https://docs.teradata.com/r/Teradata-VantageTM-Advanced-SQL-Engine-Security-Administration/July-2021/Setting-Up-the-Administrative-Infrastructure/Controlling-Access-to-the-Operating-System/Working-with-OS-Level-Security-Options).

## Anslut ditt [!DNL Teradata Vantage]-konto

I Experience Platform-gränssnittet väljer du **[!UICONTROL Sources]** i den vänstra navigeringen för att komma åt arbetsytan i [!UICONTROL Sources]. Du kan välja lämplig kategori i katalogen till vänster på skärmen. Du kan också hitta den källa du vill arbeta med med med sökalternativet.

Under kategorin [!UICONTROL Databases] väljer du **[!UICONTROL Teradata Vantage]** och sedan **[!UICONTROL Set up]**.

>[!TIP]
>
>Källor i källkatalogen visar alternativet **[!UICONTROL Set up]** när en angiven källa ännu inte har något autentiserat konto. När det finns ett autentiserat konto ändras det här alternativet till **[!UICONTROL Add data]**.

![Källkatalogen med Teradata Vantage-källan vald.](../../../../images/tutorials/create/teradata/catalog.png)

Sidan **[!UICONTROL Connect to Teradata Vantage]** visas. På den här sidan kan du antingen använda nya autentiseringsuppgifter eller befintliga.

### Befintligt konto

Om du vill ansluta ett befintligt konto markerar du det [!DNL Teradata Vantage]-konto du vill ansluta till och väljer sedan **[!UICONTROL Next]** för att fortsätta.

![Den befintliga kontosidan på arbetsytan för källor.](../../../../images/tutorials/create/teradata/existing.png)

### Nytt konto

Om du använder nya autentiseringsuppgifter väljer du **[!UICONTROL New account]**. Ange ett namn, en valfri beskrivning och dina [!DNL Teradata Vantage]-inloggningsuppgifter på det indataformulär som visas. När du är klar väljer du **[!UICONTROL Connect]** och tillåt sedan lite tid för att upprätta den nya anslutningen.

![Det nya gränssnittet för att skapa konto i källarbetsytan.](../../../../images/tutorials/create/teradata/new.png)

## Nästa steg

Genom att följa den här självstudiekursen har du upprättat en anslutning till ditt Teradata Vantage-konto. Du kan nu fortsätta till nästa självstudiekurs och [konfigurera ett dataflöde för att hämta data till Experience Platform](../../dataflow/databases.md).
