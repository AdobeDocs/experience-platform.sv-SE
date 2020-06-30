---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Skapa en Apache Hive på Azure HDInsights-källkopplingen i gränssnittet
topic: overview
translation-type: tm+mt
source-git-commit: d3c725c4760acb3857a67d0d30b24732c963a030
workflow-type: tm+mt
source-wordcount: '497'
ht-degree: 0%

---


# Skapa en [!DNL Apache Hive] på [!DNL Azure HDInsights] källkopplingen i användargränssnittet

> [!NOTE]
> På- [!DNL Apache Hive] [!DNL Azure HDInsights] kontakten finns i beta. Mer information om hur du använder betatecknade anslutningar finns i [Källor-översikten](../../../../home.md#terms-and-conditions) .

Källkopplingar i Adobe Experience Platform ger möjlighet att importera externt källdata på schemalagd basis. I den här självstudiekursen beskrivs hur du skapar en [!DNL Apache Hive] källanslutning [!DNL Azure HDInsights] med hjälp av [!DNL Platform] användargränssnittet.

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [Experience Data Model (XDM) System](../../../../../xdm/home.md): Det standardiserade ramverket som [!DNL Experience Platform] organiserar kundupplevelsedata.
   * [Grundläggande om schemakomposition](../../../../../xdm/schema/composition.md): Lär dig mer om de grundläggande byggstenarna i XDM-scheman, inklusive viktiga principer och bästa praxis när det gäller schemakomposition.
   * [Schemaredigeraren, genomgång](../../../../../xdm/tutorials/create-schema-ui.md): Lär dig hur du skapar anpassade scheman med hjälp av gränssnittet för Schemaredigeraren.
* [Kundprofil](../../../../../profile/home.md)i realtid: Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

Om du redan har en giltig [!DNL Hive] anslutning kan du hoppa över resten av det här dokumentet och gå vidare till självstudiekursen om [att konfigurera ett dataflöde](../../dataflow/databases.md)

### Samla in nödvändiga inloggningsuppgifter

För att få åtkomst till ditt [!DNL Hive] konto [!DNL Platform]måste du ange följande värden:

| Autentiseringsuppgifter | Beskrivning |
| ---------- | ----------- |
| `host` | IP-adressen eller värdnamnet för [!DNL Hive] servern. |
| `username` | Användarnamnet som du använder för att komma åt [!DNL Hive] servern. |
| `password` | Lösenordet som motsvarar användaren. |

Mer information om hur du kommer igång finns i [det här Hive-dokumentet](https://cwiki.apache.org/confluence/display/Hive/Tutorial#Tutorial-GettingStarted).

## Anslut ditt [!DNL Hive] konto

När du har samlat in dina inloggningsuppgifter kan du följa stegen nedan för att skapa ett nytt [!DNL Hive] konto att ansluta till [!DNL Platform].

Logga in på <a href="https://platform.adobe.com" target="_blank">Adobe Experience Platform</a> och välj sedan **[!UICONTROL Sources]** i det vänstra navigeringsfältet för att komma åt *[!UICONTROL Sources]* arbetsytan. På *[!UICONTROL Catalog]* skärmen visas en mängd olika källor som du kan skapa inkommande konto för, och varje källa visar antalet befintliga konton och datauppsättningsflöden som är kopplade till dem.

Du kan välja lämplig kategori i katalogen till vänster på skärmen. Du kan också hitta den källa du vill arbeta med med med sökalternativet.

Under *[!UICONTROL Databases]* kategorin väljer du **[!UICONTROL Hive]** att visa ett informationsfält till höger på skärmen. Informationsfältet innehåller en kort beskrivning av den valda källan samt alternativ för att ansluta till källan eller visa dess dokumentation. Om du vill skapa en ny inkommande anslutning väljer du **[!UICONTROL Connect source]**.

![katalog](../../../../images/tutorials/create/hive/catalog.png)

Sidan visas *[!UICONTROL Connect to Hive]* . På den här sidan kan du antingen använda nya autentiseringsuppgifter eller befintliga.

### Nytt konto

Om du använder nya autentiseringsuppgifter väljer du **[!UICONTROL New account]**. Ange ett namn, en valfri beskrivning och dina [!DNL Hive] inloggningsuppgifter på det indataformulär som visas. När du är klar väljer du **[!UICONTROL Connect]** och tillåt sedan en tid för det nya kontot att upprätta.

![koppla](../../../../images/tutorials/create/hive/new.png)

### Befintligt konto

Om du vill ansluta ett befintligt konto markerar du det [!DNL Hive] konto du vill ansluta till och väljer sedan **[!UICONTROL Next]** att fortsätta.

![befintlig](../../../../images/tutorials/create/hive/existing.png)

## Nästa steg

Genom att följa den här självstudiekursen har du upprättat en anslutning till ditt [!DNL Hive] konto. Du kan nu fortsätta med nästa självstudiekurs och [konfigurera ett dataflöde för att hämta data till Platform](../../dataflow/databases.md).