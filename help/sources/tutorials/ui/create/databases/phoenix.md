---
title: Anslut ditt Phoenix-konto med användargränssnittet i Experience Platform
description: Lär dig hur du ansluter ditt Phoenix-konto och överför data från din Phoenix-databas till Experience Platform via användargränssnittet.
exl-id: 2ed469bc-1c72-4f04-a5f0-6a0bb519a6c2
source-git-commit: b7e42eb180b8f16344afedadf763c33bcf22fa35
workflow-type: tm+mt
source-wordcount: '582'
ht-degree: 0%

---

# Anslut ditt [!DNL Phoenix]-konto till Experience Platform med användargränssnittet

I den här självstudien beskrivs hur du ansluter ditt [!DNL Phoenix]-konto och överför data från din [!DNL Phoenix]-databas till Experience Platform.

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Det standardiserade ramverk som Experience Platform använder för att ordna kundupplevelsedata.
   * [Grundläggande om schemakomposition](../../../../../xdm/schema/composition.md): Lär dig mer om grundstenarna i XDM-scheman, inklusive nyckelprinciper och bästa metoder för schemakomposition.
   * [Schemaredigeraren, självstudiekurs](../../../../../xdm/tutorials/create-schema-ui.md): Lär dig hur du skapar anpassade scheman med hjälp av gränssnittet för Schemaredigeraren.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Tillhandahåller en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

Om du redan har ett autentiserat [!DNL Phoenix]-konto kan du hoppa över resten av det här dokumentet och gå vidare till självstudiekursen [Konfigurera ett dataflöde för en databas](../../dataflow/databases.md).

### Samla in nödvändiga inloggningsuppgifter

För att få åtkomst till ditt [!DNL Phoenix]-konto på Experience Platform måste du ange följande värden:

| Autentiseringsuppgifter | Beskrivning |
| --- | --- |
| Värd | IP-adressen eller värdnamnet för servern [!DNL Phoenix]. |
| Port | TCP-porten som servern [!DNL Phoenix] använder för att avlyssna klientanslutningar. Om du ansluter till [!DNL Azure HDInsights] anger du porten som 443. Om den här parametern inte anges används standardvärdet 8765. |
| HTTP-sökväg | Den partiella URL som motsvarar servern [!DNL Phoenix]. Ange /hbasephoenix0 om du använder klustret [!DNL Azure HDInsights]. |
| Användarnamn | Användarnamnet som du använder för att komma åt servern [!DNL Phoenix]. |
| Lösenord | Lösenordet som motsvarar användaren. |
| Aktivera SSL | En växlingsknapp som anger om anslutningar till servern är krypterade med SSL. |

Mer information om hur du kommer igång finns i [det här [!DNL Phoenix] dokumentet](https://python-phoenixdb.readthedocs.io/en/latest/api.html).

När du har samlat in de nödvändiga inloggningsuppgifterna kan du följa stegen nedan för att ansluta ditt [!DNL Phoenix]-konto till Experience Platform.

## Anslut ditt [!DNL Phoenix]-konto

Välj **[!UICONTROL Sources]** i den vänstra navigeringen i plattformsgränssnittet för att komma åt källarbetsytan. På skärmen *[!UICONTROL Catalog]* visas en mängd olika källor som är tillgängliga i katalogen med Experience Platform-källor.

Du kan välja lämplig kategori i katalogen till vänster på skärmen. Du kan också söka efter en viss källa med sökalternativet.

Välj **[!UICONTROL Databases]** i listan över källkategorier och välj sedan **[!UICONTROL Add data]** från [!DNL Phoenix]-kortet.

>[!TIP]
>
>Källor i källkatalogen kan visa olika uppmaningar beroende på källans status.
> 
>* **[!UICONTROL Add data]** betyder att det finns befintliga autentiserade konton kopplade till den valda källan.
>
>* **[!UICONTROL Set up]** betyder att du måste ange autentiseringsuppgifter och autentisera ett nytt konto för att kunna använda den valda källan.

![Källkatalogen i användargränssnittet i Experience Platform med källkortet Phoenix markerat.](../../../../images/tutorials/create/phoenix/catalog.png)

Sidan **[!UICONTROL Connect to Phoenix]** visas. På den här sidan kan du antingen använda nya autentiseringsuppgifter eller befintliga.

>[!BEGINTABS]

>[!TAB Använd ett befintligt Phoenix-konto]

Om du vill använda ett befintligt konto väljer du [!UICONTROL Existing account] och sedan det konto som du vill använda i listan som visas. När du är klar väljer du [!UICONTROL Next] för att fortsätta.

![En lista över autentiserade Phoenix-databaskonton som redan finns i din organisation.](../../../../images/tutorials/create/phoenix/existing.png)

>[!TAB Skapa ett nytt Phoenix-konto]

Om du vill använda ett nytt konto väljer du [!UICONTROL New account] och anger ett namn, en beskrivning och autentiseringsuppgifter för [!DNL Phoenix]. När du är klar väljer du [!UICONTROL Connect to source] och tillåt några sekunder för att upprätta den nya anslutningen.

![Det nya kontogränssnittet där du kan ange autentiseringsuppgifter och skapa ett Phoenix-konto.](../../../../images/tutorials/create/phoenix/new.png)

>[!ENDTABS]

## Nästa steg

Genom att följa den här självstudiekursen har du upprättat en anslutning till ditt [!DNL Phoenix]-konto. Du kan nu fortsätta till nästa självstudiekurs och [konfigurera ett dataflöde så att data hämtas till Experience Platform](../../dataflow/databases.md).
