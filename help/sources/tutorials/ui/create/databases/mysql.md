---
keywords: Experience Platform;home;populära topics;mysql;MySQL
solution: Experience Platform
title: Skapa en MySQL Source-anslutning i användargränssnittet
type: Tutorial
description: Lär dig hur du skapar en MySQL-källanslutning med Adobe Experience Platform-gränssnittet.
exl-id: 75e74bde-6199-4970-93d2-f95ec3a59aa5
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '396'
ht-degree: 1%

---

# Skapa en [!DNL MySQL]-källanslutning i användargränssnittet

Source-anslutningar i Adobe Experience Platform gör det möjligt att importera externa data på schemalagd basis. I den här självstudiekursen beskrivs hur du skapar en [!DNL MySQL]-källanslutning med Adobe Experience Platform-gränssnittet.

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Det standardiserade ramverk som Experience Platform använder för att ordna kundupplevelsedata.
   * [Grundläggande om schemakomposition](../../../../../xdm/schema/composition.md): Lär dig mer om grundstenarna i XDM-scheman, inklusive nyckelprinciper och bästa metoder för schemakomposition.
   * [Schemaredigeraren, självstudiekurs](../../../../../xdm/tutorials/create-schema-ui.md): Lär dig hur du skapar anpassade scheman med hjälp av gränssnittet för Schemaredigeraren.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Tillhandahåller en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

Om du redan har en [!DNL MySQL]-anslutning kan du hoppa över resten av det här dokumentet och gå vidare till självstudiekursen [Konfigurera ett dataflöde](../../dataflow/databases.md).

### Samla in nödvändiga inloggningsuppgifter

För att få åtkomst till ditt [!DNL MySQL]-konto på [!DNL Experience Platform] måste du ange följande värde:

| Autentiseringsuppgifter | Beskrivning |
| ---------- | ----------- |
| `connectionString` | Anslutningssträngen [!DNL MySQL] som är associerad med ditt konto. Anslutningssträngsmönstret [!DNL MySQL] är: `Server={SERVER};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}`. Du kan lära dig mer om anslutningssträngar och hur du hämtar dem genom att läsa [[!DNL MySQL] dokumentet](https://dev.mysql.com/doc/connector-net/en/connector-net-connections-string.html). |

## Anslut ditt [!DNL MySQL]-konto

När du har samlat in dina nödvändiga inloggningsuppgifter kan du följa stegen nedan för att länka ditt [!DNL MySQL]-konto till [!DNL Experience Platform].

Logga in på [Adobe Experience Platform](https://platform.adobe.com) och välj sedan **[!UICONTROL Sources]** i det vänstra navigeringsfältet för att komma åt arbetsytan i **[!UICONTROL Sources]**. På skärmen **[!UICONTROL Catalog]** visas en mängd olika källor som du kan skapa ett konto med.

Välj **[!UICONTROL MySQL]** under kategorin **[!UICONTROL Databases]**. Om det här är första gången du använder den här kopplingen väljer du **[!UICONTROL Configure]**. Annars väljer du **[!UICONTROL Add data]** för att skapa en ny [!DNL MySQL]-koppling.

![](../../../../images/tutorials/create/my-sql/catalog.png)

Sidan **[!UICONTROL Connect to MySQL]** visas. På den här sidan kan du antingen använda nya autentiseringsuppgifter eller befintliga.

### Nytt konto

Om du använder nya autentiseringsuppgifter väljer du **[!UICONTROL New account]**. Ange ett namn, en valfri beskrivning och dina [!DNL MySQL]-inloggningsuppgifter på det indataformulär som visas. När du är klar väljer du **[!UICONTROL Connect]** och tillåt sedan lite tid för att upprätta den nya anslutningen.

![](../../../../images/tutorials/create/my-sql/new.png)

### Befintligt konto

Om du vill ansluta ett befintligt konto markerar du det [!DNL MySQL]-konto du vill ansluta till och väljer sedan **[!UICONTROL Next]** för att fortsätta.

![](../../../../images/tutorials/create/my-sql/existing.png)

## Nästa steg

Genom att följa den här självstudiekursen har du upprättat en anslutning till ditt MySQL-konto. Du kan nu fortsätta till nästa självstudiekurs och [konfigurera ett dataflöde för att hämta data till [!DNL Experience Platform]](../../dataflow/databases.md).
