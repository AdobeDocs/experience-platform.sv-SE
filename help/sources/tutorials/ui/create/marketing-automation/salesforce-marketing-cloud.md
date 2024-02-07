---
title: Anslut ditt Salesforce Marketing Cloud-konto till Experience Platform via användargränssnittet
description: Lär dig hur du ansluter ditt Salesforce Marketing Cloud-konto till Experience Platform via användargränssnittet.
exl-id: 1d9bde60-31e0-489c-9c1c-b6471e0ea554
source-git-commit: 30f1e8a0424ee0f81d8e98fb24886ad1480b270c
workflow-type: tm+mt
source-wordcount: '476'
ht-degree: 1%

---

# Koppla samman [!DNL Salesforce Marketing Cloud] konto till Experience Platform via användargränssnittet

>[!IMPORTANT]
>
>Inmatning av anpassade objekt stöds för närvarande inte av [!DNL Salesforce Marketing Cloud] källintegration.

Den här självstudiekursen innehåller steg för hur du ansluter [!DNL Salesforce Marketing Cloud] via användargränssnittet.

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Experience Platform:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Det standardiserade ramverk som [!DNL Experience Platform] organiserar kundupplevelsedata.
   * [Grunderna för schemakomposition](../../../../../xdm/schema/composition.md): Lär dig mer om de grundläggande byggstenarna i XDM-scheman, inklusive viktiga principer och bästa praxis när det gäller schemakomposition.
   * [Schemaredigeraren, genomgång](../../../../../xdm/tutorials/create-schema-ui.md): Lär dig hur du skapar anpassade scheman med hjälp av gränssnittet i Schemaredigeraren.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

Om du redan har en [!DNL Salesforce Marketing Cloud] kan du hoppa över resten av dokumentet och gå vidare till självstudiekursen om [för automatiserad marknadsföring till Experience Platform med hjälp av användargränssnittet](../../dataflow/marketing-automation.md).

### Samla in nödvändiga inloggningsuppgifter

För att få åtkomst till [!DNL Salesforce Marketing Cloud] på Platform måste du ange följande värden:

| Autentiseringsuppgifter | Beskrivning |
| ---------- | ----------- |
| Värd | Programmets värdserver. Detta är ofta din underdomän. **Obs!** När du anger `host` måste du ange `{subdomain}.rest.marketingcloudapis.com`. Om din värd-URL till exempel är `https://acme-ab12c3d4e5fg6hijk7lmnop8qrst.auth.marketingcloudapis.com/`måste du ange `acme-ab12c3d4e5fg6hijk7lmnop8qrst.rest.marketingcloudapis.com/` som värdvärde. |
| Klient-ID | Klient-ID som är kopplat till din [!DNL Salesforce Marketing Cloud] program. |
| Klienthemlighet | Klienthemligheten som är kopplad till din [!DNL Salesforce Marketing Cloud] program. |

Mer information om autentisering för [!DNL Salesforce Marketing Cloud], går till [[!DNL Salesforce] autentiseringsdokumentation](https://developer.salesforce.com/docs/atlas.en-us.mc-apis.meta/mc-apis/authentication.htm).

## Koppla samman [!DNL Salesforce Marketing Cloud] konto

Välj **[!UICONTROL Sources]** från vänster navigering för att komma åt [!UICONTROL Sources] arbetsyta. The [!UICONTROL Catalog] visar en mängd olika källor som stöds av Experience Platform.

Du kan välja lämplig kategori i listan med kategorier. Du kan också använda sökfältet för att filtrera efter en viss källa.

Under [!UICONTROL Marketing automation] kategori, välj **[!UICONTROL Salesforce Marketing Cloud]** och sedan **[!UICONTROL Set up]**.

![Källkatalogen med Salesforce Marketing Cloud-källan markerad.](../../../../images/tutorials/create/salesforce-marketing-cloud/catalog.png)

The **[!UICONTROL Connect to Salesforce Marketing Cloud]** visas. På den här sidan kan du antingen skapa ett nytt konto eller använda ett befintligt konto.

### Nytt konto

Om du vill skapa ett nytt konto väljer du **[!UICONTROL New account]** och ange ett namn för ditt konto, en valfri beskrivning och autentiseringsuppgifter som motsvarar dina [!DNL Salesforce Marketing Cloud] konto.

När du är klar väljer du **[!UICONTROL Connect to source]** och tillåt sedan lite tid för att upprätta den nya anslutningen.

![Det nya kontogränssnittet där du kan autentisera ett nytt konto för Salesforce Marketing Cloud.](../../../../images/tutorials/create/salesforce-marketing-cloud/new.png)

### Befintligt konto

Om du redan har ett befintligt konto väljer du **[!UICONTROL Existing account]** och välj sedan det konto som du vill använda i listan som visas.

![Det befintliga kontogränssnittet där du kan välja från en lista med befintliga Salesforce Marketing Cloud-konton.](../../../../images/tutorials/create/salesforce-marketing-cloud/existing.png)

## Nästa steg

Genom att följa den här självstudiekursen har du upprättat en anslutning mellan [!DNL Salesforce Marketing Cloud] konto och Experience Platform. Du kan nu fortsätta med nästa självstudiekurs och [skapa ett dataflöde för att ta in data för automatiserad marknadsföring i Experience Platform](../../dataflow/marketing-automation.md).
