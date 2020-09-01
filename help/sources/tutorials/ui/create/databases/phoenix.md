---
keywords: Experience Platform;home;popular topics;Phoenix;phoenix
solution: Experience Platform
title: Skapa en Phoenix-källanslutning i användargränssnittet
topic: overview
description: I den här självstudiekursen beskrivs hur du skapar en Phoenix-källanslutning med hjälp av användargränssnittet för plattformen.
translation-type: tm+mt
source-git-commit: f82dfee2c75a0b8b2ec1615266780b309152ead4
workflow-type: tm+mt
source-wordcount: '504'
ht-degree: 0%

---


# Skapa en [!DNL Phoenix] källanslutning i användargränssnittet

>[!NOTE]
>
> Kopplingen [!DNL Phoenix] är i betaversion. Mer information om hur du använder betatecknade anslutningar finns i [Källor-översikten](../../../../home.md#terms-and-conditions) .

Källkopplingar i Adobe Experience Platform gör det möjligt att importera externt källkodsdata på schemalagd basis. I den här självstudiekursen beskrivs hur du skapar en [!DNL Phoenix] källkoppling med [!DNL Platform] användargränssnittet.

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [[!DNL Experience Data Model] (XDM) System](../../../../../xdm/home.md): Det standardiserade ramverket som [!DNL Experience Platform] organiserar kundupplevelsedata.
   * [Grundläggande om schemakomposition](../../../../../xdm/schema/composition.md): Lär dig mer om de grundläggande byggstenarna i XDM-scheman, inklusive viktiga principer och bästa praxis när det gäller schemakomposition.
   * [Schemaredigeraren, genomgång](../../../../../xdm/tutorials/create-schema-ui.md): Lär dig hur du skapar anpassade scheman med hjälp av gränssnittet för Schemaredigeraren.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

Om du redan har en giltig [!DNL Phoenix] anslutning kan du hoppa över resten av det här dokumentet och gå vidare till självstudiekursen om [att konfigurera ett dataflöde](../../dataflow/databases.md)

### Samla in nödvändiga inloggningsuppgifter

För att få åtkomst till ditt [!DNL Phoenix] konto [!DNL Platform]måste du ange följande värden:

| Autentiseringsuppgifter | Beskrivning |
| ---------- | ----------- |
| `host` | IP-adressen eller värdnamnet för [!DNL Phoenix] servern. |
| `port` | Den TCP-port som servern använder för att avlyssna klientanslutningar. [!DNL Phoenix] avlyssning. Om du ansluter till [!DNL Azure HDInsights]anger du porten som 443. |
| `httpPath` | Den del av URL som motsvarar [!DNL Phoenix] servern. Ange /hbasephoenix0 om du använder [!DNL Azure HDInsights] klustret. |
| `username` | Användarnamnet som du använder för att komma åt [!DNL Phoenix] servern. |
| `password` | Lösenordet som motsvarar användaren. |
| `enableSsl` | En växel som anger om anslutningarna till servern är krypterade med SSL. |

Mer information om hur du kommer igång finns i [ [!DNL Phoenix] det här dokumentet](https://python-phoenixdb.readthedocs.io/en/latest/api.html).

## Anslut ditt [!DNL Phoenix] konto

När du har samlat in dina inloggningsuppgifter kan du följa stegen nedan för att länka ditt [!DNL Phoenix] konto till [!DNL Platform].

Logga in på [Adobe Experience Platform](https://platform.adobe.com) och välj sedan **[!UICONTROL Sources]** i det vänstra navigeringsfältet för att komma åt **[!UICONTROL Sources]** arbetsytan. På **[!UICONTROL Catalog]** skärmen visas en mängd olika källor som du kan skapa ett konto med.

Du kan välja lämplig kategori i katalogen till vänster på skärmen. Du kan också hitta den källa du vill arbeta med med med sökalternativet.

Välj under **[!UICONTROL Databases]** kategorin **[!UICONTROL Phoenix]**. Om det är första gången du använder den här kopplingen väljer du **[!UICONTROL Configure]**. Annars väljer du **[!UICONTROL Add data]** att skapa ett nytt [!DNL Phoenix] konto.

![katalog](../../../../images/tutorials/create/phoenix/catalog.png)

Sidan visas **[!UICONTROL Connect to Phoenix]** . På den här sidan kan du antingen använda nya autentiseringsuppgifter eller befintliga.

### Nytt konto

Om du använder nya autentiseringsuppgifter väljer du **[!UICONTROL New account]**. Ange ett namn, en valfri beskrivning och dina [!DNL Phoenix] inloggningsuppgifter i det indataformulär som visas. När du är klar väljer du **[!UICONTROL Connect]** och tillåt sedan en tid för att upprätta den nya anslutningen.

![koppla](../../../../images/tutorials/create/phoenix/new.png)

### Befintligt konto

Om du vill ansluta ett befintligt konto markerar du det [!DNL Phoenix] konto du vill ansluta till och väljer sedan **[!UICONTROL Next]** att fortsätta.

![befintlig](../../../../images/tutorials/create/phoenix/existing.png)

## Nästa steg

Genom att följa den här självstudiekursen har du upprättat en anslutning till ditt [!DNL Phoenix] konto. Du kan nu fortsätta med nästa självstudiekurs och [konfigurera ett dataflöde för att hämta data till [!DNL Platform]](../../dataflow/databases.md).