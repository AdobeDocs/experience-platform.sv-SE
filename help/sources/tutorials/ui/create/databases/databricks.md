---
title: Anslut Azure-databaser till Experience Platform med användargränssnittet
description: Lär dig hur du ansluter Azure-databaser till Experience Platform med användargränssnittet.
badgeUltimate: label="Ultimate" type="Positive"
badgeBeta: label="Beta" type="Informative"
source-git-commit: 2bd16d5a55c5bbeedbc6a6012d9f0229eee8433a
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 1%

---

# Anslut [!DNL Azure Databricks] till Experience Platform i användargränssnittet

>[!AVAILABILITY]
>
>* Källan [!DNL Azure Databricks] är tillgänglig i källkatalogen för användare som har köpt Real-Time CDP Ultimate.
>
>* Källan [!DNL Azure Databricks] är i betaversion. Läs [villkoren](../../../../home.md#terms-and-conditions) i källresursöversikten om du vill ha mer information om hur du använder betatecknade källor.

Läs den här vägledningen när du vill lära dig hur du ansluter ditt [!DNL Azure Databricks]-konto till Adobe Experience Platform med hjälp av källarbetsytan i användargränssnittet.

## Kom igång

Handboken kräver en fungerande förståelse av följande komponenter i Experience Platform:

* [Källor](../../../../home.md): Med Experience Platform kan data hämtas från olika källor samtidigt som du kan strukturera, etikettera och förbättra inkommande data med hjälp av Experience Platform tjänster.
* [Sandlådor](../../../../../sandboxes/home.md): Experience Platform tillhandahåller virtuella sandlådor som partitionerar en enda Experience Platform-instans till separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser.

### Samla in nödvändiga inloggningsuppgifter

Ange värden för följande autentiseringsuppgifter för att ansluta [!DNL Azure Databricks] till Experience Platform.

| Autentiseringsuppgifter | Beskrivning |
| --- | --- |
| Domän | URL-adressen till din [!DNL Azure Databricks]-arbetsyta. Exempel: `https://adb-1234567890123456.7.azuredatabricks.net`. |
| Kluster-ID | ID för ditt kluster i [!DNL Azure Databricks]. Det här klustret måste redan vara ett befintligt kluster och bör vara ett interaktivt kluster. |
| Åtkomsttoken | Åtkomsttoken som autentiserar ditt [!DNL Azure Databricks]-konto. Du kan generera din åtkomsttoken med arbetsytan [!DNL Azure Databricks]. |
| Databas | Namnet på databasen i deltasjön. |

Mer information finns i [[!DNL Azure Databricks] översikten](../../../../connectors/databases/databricks.md).

## Navigera i källkatalogen

I Experience Platform-gränssnittet väljer du **[!UICONTROL Sources]** i den vänstra navigeringen för att komma åt arbetsytan i *[!UICONTROL Sources]*. Välj en kategori eller använd sökfältet för att hitta källan.

Om du vill ansluta till [!DNL Azure Databricks] går du till kategorin *[!UICONTROL Databases]*, markerar **[!UICONTROL Azure Databricks]**-källkortet och väljer **[!UICONTROL Set up]**.

>[!TIP]
>
>Källor i källkatalogen visar alternativet **[!UICONTROL Set up]** när en angiven källa ännu inte har något autentiserat konto. När ett autentiserat konto har skapats ändras alternativet till **[!UICONTROL Add data]**.

![Källkatalogen med källkortet för Azure-databaser har valts.](../../../../images/tutorials/create/databricks/catalog.png)

### Använd ett befintligt konto

Om du vill använda ett befintligt konto väljer du **[!UICONTROL Existing account]** och sedan det [!DNL Azure Databricks]-konto som du vill använda.

![Det befintliga kontogränssnittet i källarbetsflödet med &quot;Befintligt konto&quot; valt.](../../../../images/tutorials/create/databricks/existing.png)

### Skapa ett nytt konto

Om du vill skapa ett nytt konto väljer du **[!UICONTROL New account]** och anger ett namn och kan lägga till en beskrivning för ditt konto. Ange sedan värden för följande autentiseringsuppgifter:

* Domän
* Kluster-ID
* Åtkomsttoken
* Databas

![Det nya kontogränssnittet i källarbetsflödet med ett kontonamn och en valfri beskrivning har angetts.](../../../../images/tutorials/create/databricks/new.png)

Dessutom måste du kopiera och klistra in dina [!UICONTROL Staging SAS URI]-inloggningsuppgifter i din [!DNL Azure Databricks]-miljö. När du är klar väljer du **[!UICONTROL Connect to source]** och tillåt en stund så att anslutningen kan upprättas.

![SAS-URI:ns mellanlagringsuppgifter.](../../../../images/tutorials/create/databricks/sas-uri.png)

## Skapa ett dataflöde för [!DNL Azure Databricks] data

Nu när du har anslutit ditt [!DNL Azure Databricks]-konto kan du [skapa ett dataflöde och importera data från din databas till Experience Platform](../../dataflow/databases.md).
