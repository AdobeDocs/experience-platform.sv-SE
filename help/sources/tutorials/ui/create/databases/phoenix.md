---
title: Anslut ditt Phoenix-konto med användargränssnittet i Experience Platform
description: Lär dig hur du ansluter ditt Phoenix-konto och överför data från din Phoenix-databas till Experience Platform via användargränssnittet.
exl-id: 2ed469bc-1c72-4f04-a5f0-6a0bb519a6c2
source-git-commit: b7e42eb180b8f16344afedadf763c33bcf22fa35
workflow-type: tm+mt
source-wordcount: '584'
ht-degree: 1%

---

# Koppla samman [!DNL Phoenix] konto till Experience Platform med användargränssnittet

Den här självstudiekursen innehåller steg för hur du ansluter [!DNL Phoenix] ta fram data från [!DNL Phoenix] databas till Experience Platform.

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Det standardiserade ramverk som Experience Platform använder för att ordna kundupplevelsedata.
   * [Grunderna för schemakomposition](../../../../../xdm/schema/composition.md): Lär dig mer om de grundläggande byggstenarna i XDM-scheman, inklusive viktiga principer och bästa praxis när det gäller schemakomposition.
   * [Schemaredigeraren, genomgång](../../../../../xdm/tutorials/create-schema-ui.md): Lär dig hur du skapar anpassade scheman med hjälp av gränssnittet i Schemaredigeraren.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

Om du redan har en autentiserad [!DNL Phoenix] kan du hoppa över resten av dokumentet och gå vidare till självstudiekursen om [konfigurera ett dataflöde för en databas](../../dataflow/databases.md).

### Samla in nödvändiga inloggningsuppgifter

För att få åtkomst till [!DNL Phoenix] på Experience Platform måste du ange följande värden:

| Autentiseringsuppgifter | Beskrivning |
| --- | --- |
| Värd | IP-adressen eller värdnamnet för [!DNL Phoenix] server. |
| Port | TCP-porten som [!DNL Phoenix] servern använder för att avlyssna klientanslutningar. Om du ansluter till [!DNL Azure HDInsights]anger du porten som 443. Om den här parametern inte anges används standardvärdet 8765. |
| HTTP-sökväg | Den del av URL som motsvarar [!DNL Phoenix] server. Ange /hbasephoenix0 om du använder [!DNL Azure HDInsights] kluster. |
| Användarnamn | Användarnamnet som du använder för att få åtkomst till [!DNL Phoenix] server. |
| Lösenord | Lösenordet som motsvarar användaren. |
| Aktivera SSL | En växlingsknapp som anger om anslutningar till servern är krypterade med SSL. |

Mer information om hur du kommer igång finns i [this [!DNL Phoenix] dokument](https://python-phoenixdb.readthedocs.io/en/latest/api.html).

När du har samlat in dina inloggningsuppgifter kan du följa stegen nedan för att ansluta [!DNL Phoenix] konto till Experience Platform.

## Koppla samman [!DNL Phoenix] konto

Välj **[!UICONTROL Sources]** från vänster navigering för att komma åt källarbetsytan. The *[!UICONTROL Catalog]* På skärmen visas en mängd olika källor som finns i katalogen med Experience Platform-källor.

Du kan välja lämplig kategori i katalogen till vänster på skärmen. Du kan också söka efter en viss källa med sökalternativet.

Välj **[!UICONTROL Databases]** i listan över källkategorier och välj sedan **[!UICONTROL Add data]** från [!DNL Phoenix] kort.

>[!TIP]
>
>Källor i källkatalogen kan visa olika uppmaningar beroende på källans status.
> 
>* **[!UICONTROL Add data]** betyder att det finns befintliga autentiserade konton kopplade till den valda källan.
>
>* **[!UICONTROL Set up]** innebär att du måste ange inloggningsuppgifter och autentisera ett nytt konto för att kunna använda den valda källan.

![Källkatalogen i användargränssnittet i Experience Platform med källkortet Phoenix valt.](../../../../images/tutorials/create/phoenix/catalog.png)

The **[!UICONTROL Connect to Phoenix]** visas. På den här sidan kan du antingen använda nya autentiseringsuppgifter eller befintliga.

>[!BEGINTABS]

>[!TAB Använd ett befintligt Phoenix-konto]

Om du vill använda ett befintligt konto väljer du [!UICONTROL Existing account] och välj sedan det konto som du vill använda i listan som visas. När du är klar väljer du [!UICONTROL Next] för att fortsätta.

![En lista över autentiserade Phoenix-databaskonton som redan finns i din organisation.](../../../../images/tutorials/create/phoenix/existing.png)

>[!TAB Skapa ett nytt Phoenix-konto]

Om du vill använda ett nytt konto väljer du [!UICONTROL New account] och ange namn, beskrivning och [!DNL Phoenix] autentiseringsuppgifter. När du är klar väljer du [!UICONTROL Connect to source] och under några sekunder kan den nya anslutningen upprättas.

![Det nya kontogränssnittet där du kan ange autentiseringsuppgifter och skapa ett Phoenix-konto.](../../../../images/tutorials/create/phoenix/new.png)

>[!ENDTABS]

## Nästa steg

Genom att följa den här självstudien har du upprättat en anslutning till [!DNL Phoenix] konto. Du kan nu fortsätta med nästa självstudiekurs och [konfigurera ett dataflöde för att hämta data till Experience Platform](../../dataflow/databases.md).
