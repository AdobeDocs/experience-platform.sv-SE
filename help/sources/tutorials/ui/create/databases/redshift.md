---
title: Skapa en Amazon Redshift Source Connection i användargränssnittet
description: Lär dig hur du skapar en Amazon Redshift-källanslutning med Adobe Experience Platform-gränssnittet.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 4faf3200-673b-4a20-8f94-d049e800444b
source-git-commit: a7c2c5e4add5c80e0622d5aeb766cec950d79dbb
workflow-type: tm+mt
source-wordcount: '469'
ht-degree: 0%

---

# Anslut ditt [!DNL Amazon Redshift]-konto med hjälp av källarbetsytan

>[!IMPORTANT]
>
>Källan [!DNL Amazon Redshift] är tillgänglig i källkatalogen för användare som har köpt Real-time Customer Data Platform Ultimate.

I den här självstudien beskrivs hur du ansluter ditt [!DNL Amazon Redshift]-konto (kallas nedan [!DNL Redshift]) till Adobe Experience Platform via användargränssnittet.

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Experience Platform:

- [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Det standardiserade ramverk som Experience Platform använder för att ordna kundupplevelsedata.
   - [Grundläggande om schemakomposition](../../../../../xdm/schema/composition.md): Lär dig mer om grundstenarna i XDM-scheman, inklusive nyckelprinciper och bästa metoder för schemakomposition.
   - [Schemaredigeraren, självstudiekurs](../../../../../xdm/tutorials/create-schema-ui.md): Lär dig hur du skapar anpassade scheman med hjälp av gränssnittet för Schemaredigeraren.
- [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Tillhandahåller en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

Om du redan har en giltig [!DNL Redshift]-anslutning kan du hoppa över resten av det här dokumentet och gå vidare till självstudiekursen [Konfigurera ett dataflöde](../../dataflow/databases.md).

### Samla in nödvändiga inloggningsuppgifter

För att få åtkomst till ditt [!DNL Redshift]-konto på Experience Platform måste du ange följande värden:

| **Autentiseringsuppgifter** | **Beskrivning** |
| -------------- | --------------- |
| Server | Servern som är associerad med ditt [!DNL Redshift]-konto. |
| Port | TCP-porten som en [!DNL Redshift]-server använder för att avlyssna klientanslutningar. |
| Användarnamn | Användarnamnet som är associerat med ditt [!DNL Redshift]-konto. |
| Lösenord | Lösenordet som är kopplat till ditt [!DNL Redshift]-konto. |
| Databas | Databasen [!DNL Redshift] som du använder. |

Mer information om hur du kommer igång finns i [det här [!DNL Redshift] dokumentet](https://docs.aws.amazon.com/redshift/latest/gsg/getting-started.html).

När du har samlat in de nödvändiga inloggningsuppgifterna kan du följa stegen nedan för att länka ditt [!DNL Redshift]-konto till Experience Platform.

## Anslut ditt [!DNL Redshift]-konto

>[!NOTE]
>
>Standardkodningsstandarden för [!DNL Redshift] är Unicode. Detta kan inte ändras.

Logga in på [Adobe Experience Platform](https://platform.adobe.com) och välj sedan **[!UICONTROL Sources]** i det vänstra navigeringsfältet för att komma åt arbetsytan i **[!UICONTROL Sources]**. På skärmen **[!UICONTROL Catalog]** visas en mängd olika källor som du kan skapa ett konto med.

Du kan välja lämplig kategori i katalogen till vänster på skärmen. Du kan också hitta den källa du vill arbeta med med med sökalternativet.

Välj **[!UICONTROL Amazon Redshift]** under kategorin **[!UICONTROL Databases]**. Om det här är första gången du använder den här kopplingen väljer du **[!UICONTROL Configure]**. Annars väljer du **[!UICONTROL Add data]** för att skapa en ny [!DNL Redshift]-koppling.

![](../../../../images/tutorials/create/redshift/catalog.png)

Sidan **[!UICONTROL Connect to Amazon Redshift]** visas. På den här sidan kan du antingen använda nya autentiseringsuppgifter eller befintliga.

### Nytt konto

Om du använder nya autentiseringsuppgifter väljer du **[!UICONTROL New account]**. Ange ett namn, en valfri beskrivning och dina [!DNL Redshift]-inloggningsuppgifter på det indataformulär som visas. När du är klar väljer du **[!UICONTROL Connect]** och tillåt sedan lite tid för att upprätta den nya anslutningen.

![](../../../../images/tutorials/create/redshift/new.png)

### Befintligt konto

Om du vill ansluta ett befintligt konto markerar du det [!DNL Redshift]-konto du vill ansluta till och väljer sedan **[!UICONTROL Next]** för att fortsätta.

![](../../../../images/tutorials/create/redshift/existing.png)

## Nästa steg

Genom att följa den här självstudiekursen har du upprättat en anslutning till ditt [!DNL Redshift]-konto. Du kan nu fortsätta till nästa självstudiekurs och [konfigurera ett dataflöde så att data hämtas till Experience Platform](../../dataflow/databases.md).
