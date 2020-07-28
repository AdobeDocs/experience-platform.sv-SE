---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Skapa en allmän OData-källanslutning i användargränssnittet
topic: overview
translation-type: tm+mt
source-git-commit: 4f7d7e2bf255afe1588dbe7cfb2ec055f2dcbf75
workflow-type: tm+mt
source-wordcount: '483'
ht-degree: 0%

---


# Skapa en [!DNL Generic OData] källanslutning i användargränssnittet

>[!NOTE]
> Kopplingen [!DNL Generic OData] är i betaversion. Mer information om hur du använder betatecknade anslutningar finns i [Källor-översikten](../../../../home.md#terms-and-conditions) .

Källkopplingar i Adobe Experience Platform ger möjlighet att importera externt källdata på schemalagd basis. I den här självstudiekursen beskrivs hur du skapar en allmän källkoppling för ett öppet dataprotokoll (nedan kallat OData) med [!DNL Platform] användargränssnittet.

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [Experience Data Model (XDM) System](../../../../../xdm/home.md): Det standardiserade ramverket som [!DNL Experience Platform] organiserar kundupplevelsedata.
   * [Grundläggande om schemakomposition](../../../../../xdm/schema/composition.md): Lär dig mer om de grundläggande byggstenarna i XDM-scheman, inklusive viktiga principer och bästa praxis när det gäller schemakomposition.
   * [Schemaredigeraren, genomgång](../../../../../xdm/tutorials/create-schema-ui.md): Lär dig hur du skapar anpassade scheman med hjälp av gränssnittet för Schemaredigeraren.
* [Kundprofil](../../../../../profile/home.md)i realtid: Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

Om du redan har en giltig OData-anslutning kan du hoppa över resten av det här dokumentet och fortsätta med självstudiekursen om hur du [konfigurerar ett protokolldatauppsättningsflöde](../../dataflow/protocols.md)

### Samla in nödvändiga inloggningsuppgifter

Du måste ange följande värden för att få åtkomst till ditt [!DNL OData] konto i [!DNL Platform]:

| Autentiseringsuppgifter | Beskrivning |
| ---------- | ----------- |
| `url` | URL-adressen till [!DNL OData] tjänsten. |

Mer information om hur du kommer igång finns i [detta OData-dokument](https://www.odata.org/getting-started/basic-tutorial/).

## Anslut ditt [!DNL OData] konto

När du har samlat in dina inloggningsuppgifter kan du följa stegen nedan för att skapa ett nytt [!DNL OData] konto att ansluta till [!DNL Platform].

Logga in på <a href="https://platform.adobe.com" target="_blank">Adobe Experience Platform</a> och välj sedan **[!UICONTROL Sources]** i det vänstra navigeringsfältet för att komma åt *[!UICONTROL Sources]* arbetsytan. På *[!UICONTROL Catalog]* skärmen visas en mängd olika källor som du kan skapa inkommande konto för. Varje källa visar antalet befintliga konton och datauppsättningsflöden som är kopplade till dem.

Du kan välja lämplig kategori i katalogen till vänster på skärmen. Du kan också hitta den källa du vill arbeta med med med sökalternativet.

Under *[!UICONTROL Protocols]* kategorin väljer du **[!UICONTROL Generic OData]** att visa ett informationsfält till höger på skärmen. Informationsfältet innehåller en kort beskrivning av den valda källan samt alternativ för att ansluta till källan eller visa dess dokumentation. Om du vill skapa en ny inkommande anslutning väljer du **[!UICONTROL Connect source]**.

![katalog](../../../../images/tutorials/create/odata/catalog.png)

Sidan visas *[!UICONTROL Connect to Generic OData]* . På den här sidan kan du antingen använda nya autentiseringsuppgifter eller befintliga.

### Nytt konto

Om du använder nya autentiseringsuppgifter väljer du **[!UICONTROL New account]**. Ange ett namn, en valfri beskrivning och dina [!DNL OData] inloggningsuppgifter på det indataformulär som visas. När du är klar väljer du **[!UICONTROL Connect]** och tillåt sedan en tid för det nya kontot att upprätta.

![koppla](../../../../images/tutorials/create/odata/connect.png)

### Befintligt konto

Om du vill ansluta ett befintligt konto markerar du det [!DNL OData] konto du vill ansluta till och väljer sedan **[!UICONTROL Next]** att fortsätta.

![befintlig](../../../../images/tutorials/create/odata/existing.png)

## Nästa steg

Genom att följa den här självstudiekursen har du upprättat en anslutning till ditt [!DNL OData] konto. Du kan nu fortsätta med nästa självstudiekurs och [konfigurera ett datauppsättningsflöde för att hämta protokolldata till Platform](../../dataflow/protocols.md).