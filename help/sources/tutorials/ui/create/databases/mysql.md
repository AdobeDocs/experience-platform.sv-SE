---
keywords: Experience Platform;home;popular topics;mysql;MySQL
solution: Experience Platform
title: Skapa en MySQL-källkoppling i användargränssnittet
topic: overview
type: Tutorial
description: I den här självstudiekursen beskrivs hur du skapar en MySQL-källkoppling med hjälp av användargränssnittet för plattformen.
translation-type: tm+mt
source-git-commit: f86f7483e7e78edf106ddd34dc825389dadae26a
workflow-type: tm+mt
source-wordcount: '411'
ht-degree: 1%

---


# Skapa en [!DNL MySQL] källanslutning i användargränssnittet

>[!NOTE]
>
> Kopplingen [!DNL MySQL] är i betaversion. Mer information om hur du använder betatecknade anslutningar finns i [Källor-översikten](../../../../home.md#terms-and-conditions) .

Källkopplingar i Adobe Experience Platform gör det möjligt att importera externt källkodsdata på schemalagd basis. I den här självstudiekursen beskrivs hur du skapar en [!DNL MySQL] källanslutning med hjälp av användargränssnittet för plattformen.

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Det standardiserade ramverk som Experience Platform använder för att ordna kundupplevelsedata.
   * [Grundläggande om schemakomposition](../../../../../xdm/schema/composition.md): Lär dig mer om de grundläggande byggstenarna i XDM-scheman, inklusive viktiga principer och bästa praxis när det gäller schemakomposition.
   * [Schemaredigeraren, genomgång](../../../../../xdm/tutorials/create-schema-ui.md): Lär dig hur du skapar anpassade scheman med hjälp av gränssnittet för Schemaredigeraren.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

Om du redan har en [!DNL MySQL] anslutning kan du hoppa över resten av det här dokumentet och gå vidare till självstudiekursen om hur du [konfigurerar ett dataflöde](../../dataflow/databases.md).

### Samla in nödvändiga inloggningsuppgifter

För att få åtkomst till ditt [!DNL MySQL] konto [!DNL Platform]måste du ange följande värde:

| Autentiseringsuppgifter | Beskrivning |
| ---------- | ----------- |
| `connectionString` | Den [!DNL MySQL] anslutningssträng som är associerad med ditt konto. Anslutningssträngsmönstret är: [!DNL MySQL] `Server={SERVER};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}`. Du kan lära dig mer om anslutningssträngar och hur du hämtar dem genom att läsa [[!DNL MySQL] dokumentet](https://dev.mysql.com/doc/connector-net/en/connector-net-connections-string.html). |

## Anslut ditt [!DNL MySQL] konto

När du har samlat in dina inloggningsuppgifter kan du följa stegen nedan för att länka ditt [!DNL MySQL] konto till [!DNL Platform].

Logga in på [Adobe Experience Platform](https://platform.adobe.com) och välj sedan **[!UICONTROL Sources]** i det vänstra navigeringsfältet för att komma åt **[!UICONTROL Sources]** arbetsytan. På **[!UICONTROL Catalog]** skärmen visas en mängd olika källor som du kan skapa ett konto med.

Välj under **[!UICONTROL Databases]** kategorin **[!UICONTROL MySQL]**. Om det är första gången du använder den här kopplingen väljer du **[!UICONTROL Configure]**. Annars väljer du **[!UICONTROL Add data]** att skapa en ny [!DNL MySQL] koppling.

![](../../../../images/tutorials/create/my-sql/catalog.png)

Sidan visas **[!UICONTROL Connect to MySQL]** . På den här sidan kan du antingen använda nya autentiseringsuppgifter eller befintliga.

### Nytt konto

Om du använder nya autentiseringsuppgifter väljer du **[!UICONTROL New account]**. Ange ett namn, en valfri beskrivning och dina [!DNL MySQL] inloggningsuppgifter i det indataformulär som visas. När du är klar väljer du **[!UICONTROL Connect]** och tillåt sedan en tid för att upprätta den nya anslutningen.

![](../../../../images/tutorials/create/my-sql/new.png)

### Befintligt konto

Om du vill ansluta ett befintligt konto markerar du det [!DNL MySQL] konto du vill ansluta till och väljer sedan **[!UICONTROL Next]** att fortsätta.

![](../../../../images/tutorials/create/my-sql/existing.png)

## Nästa steg

Genom att följa den här självstudiekursen har du upprättat en anslutning till ditt MySQL-konto. Du kan nu fortsätta med nästa självstudiekurs och [konfigurera ett dataflöde för att hämta data till [!DNL Platform]](../../dataflow/databases.md).