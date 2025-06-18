---
title: Anslut ditt Salesforce Marketing Cloud-konto till Experience Platform via användargränssnittet
description: Lär dig hur du ansluter ditt Salesforce Marketing Cloud-konto till Experience Platform via användargränssnittet.
exl-id: 1d9bde60-31e0-489c-9c1c-b6471e0ea554
source-git-commit: 0c6a51d06e57eb6de063a350bd4b17022555a0b4
workflow-type: tm+mt
source-wordcount: '555'
ht-degree: 0%

---

# Anslut ditt [!DNL Salesforce Marketing Cloud]-konto till Experience Platform via användargränssnittet

>[!WARNING]
>
>[!DNL Salesforce Marketing Cloud]-källan kommer att bli inaktuell i januari 2026. En ny källa kommer att släppas senare i år som ett alternativ. När den nya källan har släppts måste du planera migreringen till den nya källan genom att skapa nya kontoanslutningar och dataflöden före utgången av januari 2026.

Läs den här vägledningen när du vill lära dig hur du ansluter ditt [!DNL Salesforce Marketing Cloud]-konto till Adobe Experience Platform med hjälp av källarbetsytan i Experience Platform användargränssnitt.

## Kom igång

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Experience Platform:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Det standardiserade ramverk som [!DNL Experience Platform] organiserar kundupplevelsedata med.
   * [Grundläggande om schemakomposition](../../../../../xdm/schema/composition.md): Lär dig mer om grundstenarna i XDM-scheman, inklusive nyckelprinciper och bästa metoder för schemakomposition.
   * [Schemaredigeraren, självstudiekurs](../../../../../xdm/tutorials/create-schema-ui.md): Lär dig hur du skapar anpassade scheman med hjälp av gränssnittet för Schemaredigeraren.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Tillhandahåller en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

Om du redan har ett [!DNL Salesforce Marketing Cloud]-konto kan du hoppa över resten av det här dokumentet och gå vidare till självstudiekursen om hur du [skickar data för automatiserad marknadsföring till Experience Platform med användargränssnittet](../../dataflow/marketing-automation.md).

### Samla in nödvändiga inloggningsuppgifter

Läs [[!DNL Salesforce Marketing Cloud] översikten](../../../../connectors/marketing-automation/salesforce-marketing-cloud.md#prerequisites) om du vill ha information om autentisering.

## Navigera i källkatalogen

>[!IMPORTANT]
>
>Inläsning av anpassade objekt stöds för närvarande inte av källintegreringen [!DNL Salesforce Marketing Cloud].


I Experience Platform-gränssnittet väljer du **[!UICONTROL Sources]** i den vänstra navigeringen för att komma åt arbetsytan i *[!UICONTROL Sources]*. Välj en kategori eller använd sökfältet för att hitta källan.

Om du vill ansluta till [!DNL Salesforce Marketing Cloud] går du till kategorin *[!UICONTROL Marketing Automation]*, markerar **[!UICONTROL Salesforce Marketing Cloud]**-källkortet och väljer **[!UICONTROL Set up]**.

>[!TIP]
>
>Källor i källkatalogen visar alternativet **[!UICONTROL Set up]** när en angiven källa ännu inte har något autentiserat konto. När ett autentiserat konto har skapats ändras alternativet till **[!UICONTROL Add data]**.

![Källkatalogen med källkortet för Salesforce Marketing Cloud har valts.](../../../../images/tutorials/create/salesforce-marketing-cloud/catalog.png)

## Använd ett befintligt konto {#existing}

Om du vill använda ett befintligt konto väljer du **[!UICONTROL Existing account]** och sedan det [!DNL Salesforce Marketing Cloud]-konto som du vill använda.

![Det befintliga kontogränssnittet i källarbetsflödet med &quot;Befintligt konto&quot; valt.](../../../../images/tutorials/create/salesforce-marketing-cloud/existing.png)

## Skapa ett nytt konto {#new}

Du kan använda källan [!DNL Salesforce Marketing Cloud] för att ansluta till Experience Platform på [!DNL Azure] eller [!DNL Amazon Web Services] (AWS).

### Anslut till Experience Platform på [!DNL Azure] {#azure}

Om du vill ansluta till Experience Platform på [!DNL Azure] anger du ett kontonamn, en valfri beskrivning och autentiseringsuppgifter för ditt [konto](../../../../connectors/marketing-automation/salesforce-marketing-cloud.md#azure). När du är klar väljer du **[!UICONTROL Connect to source]** och tillåt en stund så att anslutningen kan upprättas.

![Det nya kontogränssnittet i källarbetsflödet för anslutning till Experience Platform på Azure.](../../../../images/tutorials/create/salesforce-marketing-cloud/new-azure.png)

### Ansluta till Experience Platform på Amazon Web Services (AWS) {#aws}

>[!AVAILABILITY]
>
>Detta avsnitt gäller implementeringar av Experience Platform som körs på Amazon Web Services (AWS). Experience Platform som körs på AWS är för närvarande tillgängligt för ett begränsat antal kunder. Mer information om den Experience Platform-infrastruktur som stöds finns i [Experience Platform översikt över flera moln](../../../../../landing/multi-cloud.md).

Om du vill ansluta till Experience Platform på [!DNL AWS] kontrollerar du att du befinner dig i en VA6-sandlåda och anger ett kontonamn, en valfri beskrivning och autentiseringsuppgifter för [kontot](../../../../connectors/marketing-automation/salesforce-marketing-cloud.md#aws). När du är klar väljer du **[!UICONTROL Connect to source]** och tillåt en stund så att anslutningen kan upprättas.

![Det nya kontogränssnittet i källarbetsflödet för anslutning till Experience Platform på AWS](../../../../images/tutorials/create/salesforce-marketing-cloud/new-aws.png)

## Skapa ett dataflöde för [!DNL Salesforce Marketing Cloud] data

Nu när du har anslutit din [!DNL Salesforce Marketing Cloud] kan du [skapa ett dataflöde och importera data från din leverantör av automatiserad marknadsföring till Experience Platform](../../dataflow/marketing-automation.md).
