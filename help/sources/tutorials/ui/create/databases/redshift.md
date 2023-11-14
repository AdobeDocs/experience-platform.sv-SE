---
title: Skapa en Amazon Redshift-källanslutning i användargränssnittet
description: Lär dig hur du skapar en Amazon Redshift-källanslutning med Adobe Experience Platform-gränssnittet.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 4faf3200-673b-4a20-8f94-d049e800444b
source-git-commit: a7c2c5e4add5c80e0622d5aeb766cec950d79dbb
workflow-type: tm+mt
source-wordcount: '475'
ht-degree: 1%

---

# Koppla samman [!DNL Amazon Redshift] konto med hjälp av källarbetsytan

>[!IMPORTANT]
>
>The [!DNL Amazon Redshift] Källan är tillgänglig i källkatalogen för användare som har köpt Real-time Customer Data Platform Ultimate.

Den här självstudiekursen innehåller steg för hur du ansluter [!DNL Amazon Redshift] (nedan kallad[!DNL Redshift]&quot;) till Adobe Experience Platform via användargränssnittet.

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Experience Platform:

- [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Det standardiserade ramverk som Experience Platform använder för att ordna kundupplevelsedata.
   - [Grunderna för schemakomposition](../../../../../xdm/schema/composition.md): Lär dig mer om de grundläggande byggstenarna i XDM-scheman, inklusive viktiga principer och bästa praxis när det gäller schemakomposition.
   - [Schemaredigeraren, genomgång](../../../../../xdm/tutorials/create-schema-ui.md): Lär dig hur du skapar anpassade scheman med hjälp av gränssnittet i Schemaredigeraren.
- [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

Om du redan har en giltig [!DNL Redshift] kan du hoppa över resten av dokumentet och gå vidare till självstudiekursen om [konfigurera ett dataflöde](../../dataflow/databases.md).

### Samla in nödvändiga inloggningsuppgifter

För att få åtkomst till [!DNL Redshift] på Experience Platform måste du ange följande värden:

| **Autentiseringsuppgifter** | **Beskrivning** |
| -------------- | --------------- |
| Server | Servern som är kopplad till din [!DNL Redshift] konto. |
| Port | TCP-porten som [!DNL Redshift] servern använder för att avlyssna klientanslutningar. |
| Användarnamn | Användarnamnet som är associerat med din [!DNL Redshift] konto. |
| Lösenord | Lösenordet som är kopplat till [!DNL Redshift] konto. |
| Databas | The [!DNL Redshift] databas som du använder. |

Mer information om hur du kommer igång finns i [this [!DNL Redshift] dokument](https://docs.aws.amazon.com/redshift/latest/gsg/getting-started.html).

När du har samlat in dina inloggningsuppgifter kan du följa stegen nedan för att länka dina [!DNL Redshift] konto till Experience Platform.

## Koppla samman [!DNL Redshift] konto

>[!NOTE]
>
>Standardkodningsstandard för [!DNL Redshift] är Unicode. Detta kan inte ändras.

Logga in på [Adobe Experience Platform](https://platform.adobe.com) och sedan **[!UICONTROL Sources]** från det vänstra navigeringsfältet för att komma åt **[!UICONTROL Sources]** arbetsyta. The **[!UICONTROL Catalog]** I visas en mängd olika källor som du kan skapa ett konto med.

Du kan välja lämplig kategori i katalogen till vänster på skärmen. Du kan också hitta den källa du vill arbeta med med med sökalternativet.

Under **[!UICONTROL Databases]** kategori, välj **[!UICONTROL Amazon Redshift]**. Om det här är första gången du använder den här kopplingen väljer du **[!UICONTROL Configure]**. Annars väljer du **[!UICONTROL Add data]** för att skapa en ny [!DNL Redshift] koppling.

![](../../../../images/tutorials/create/redshift/catalog.png)

The **[!UICONTROL Connect to Amazon Redshift]** visas. På den här sidan kan du antingen använda nya autentiseringsuppgifter eller befintliga.

### Nytt konto

Om du använder nya autentiseringsuppgifter väljer du **[!UICONTROL New account]**. Ange ett namn, en valfri beskrivning och din [!DNL Redshift] autentiseringsuppgifter. När du är klar väljer du **[!UICONTROL Connect]** och tillåt sedan lite tid för att upprätta den nya anslutningen.

![](../../../../images/tutorials/create/redshift/new.png)

### Befintligt konto

Välj [!DNL Redshift] konto som du vill ansluta till och välj **[!UICONTROL Next]** för att fortsätta.

![](../../../../images/tutorials/create/redshift/existing.png)

## Nästa steg

Genom att följa den här självstudien har du upprättat en anslutning till [!DNL Redshift] konto. Du kan nu fortsätta med nästa självstudiekurs och [konfigurera ett dataflöde för att hämta data till Experience Platform](../../dataflow/databases.md).
