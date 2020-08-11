---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Skapa en Amazon Redshift-källanslutning i användargränssnittet
topic: overview
translation-type: tm+mt
source-git-commit: 598b29f681ac930a4e1781f7f298608c8344d807
workflow-type: tm+mt
source-wordcount: '467'
ht-degree: 1%

---


# Skapa en [!DNL Amazon Redshift] källanslutning i användargränssnittet

>The [!NOTE]
>Kopplingen [!DNL Amazon Redshift] är i betaversion. Mer information om hur du använder betatecknade anslutningar finns i [Källor-översikten](../../../../home.md#terms-and-conditions) .

Källkopplingar i Adobe Experience Platform gör det möjligt att importera externt källkodsdata på schemalagd basis. I den här självstudiekursen beskrivs hur du skapar en [!DNL Amazon Redshift] källkoppling (nedan kallad[!DNL Redshift]) med hjälp av [!DNL Platform] användargränssnittet.

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

- [Experience Data Model (XDM) System](../../../../../xdm/home.md): Det standardiserade ramverket som [!DNL Experience Platform] organiserar kundupplevelsedata.
   - [Grundläggande om schemakomposition](../../../../../xdm/schema/composition.md): Lär dig mer om de grundläggande byggstenarna i XDM-scheman, inklusive viktiga principer och bästa praxis när det gäller schemakomposition.
   - [Schemaredigeraren, genomgång](../../../../../xdm/tutorials/create-schema-ui.md): Lär dig hur du skapar anpassade scheman med hjälp av gränssnittet för Schemaredigeraren.
- [Kundprofil](../../../../../profile/home.md)i realtid: Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

Om du redan har en [!DNL Redshift] basanslutning kan du hoppa över resten av det här dokumentet och gå vidare till självstudiekursen om hur du [konfigurerar ett dataflöde](../../dataflow/databases.md).

### Samla in nödvändiga inloggningsuppgifter

För att få åtkomst till ditt [!DNL Redshift] konto [!DNL Platform]måste du ange följande värden:

| **Autentiseringsuppgifter** | **Beskrivning** |
| -------------- | --------------- |
| `server` | Servern som är kopplad till ditt [!DNL Redshift] konto. |
| `username` | Användarnamnet som är associerat med ditt [!DNL Redshift] konto. |
| `password` | Lösenordet som är kopplat till ditt [!DNL Redshift] konto. |
| `database` | Den [!DNL Redshift] databas du använder. |

Mer information om hur du kommer igång finns i [detta Redshift-dokument](https://docs.aws.amazon.com/redshift/latest/gsg/getting-started.html).

## Anslut ditt [!DNL Redshift] konto

När du har samlat in dina inloggningsuppgifter kan du följa stegen nedan för att skapa en ny inkommande basanslutning som du kan länka ditt [!DNL Redshift] konto till [!DNL Platform].

Logga in på [Adobe Experience Platform](https://platform.adobe.com) och välj sedan **[!UICONTROL Sources]** i det vänstra navigeringsfältet för att komma åt *[!UICONTROL Sources]* arbetsytan. På *[!UICONTROL Catalog]* skärmen visas en mängd olika källor som du kan skapa inkommande basanslutningar med, och varje källa visar antalet befintliga basanslutningar som är kopplade till dem.

Under *[!UICONTROL Databases]* kategorin väljer du **[!UICONTROL Amazon Redshift]** att visa ett informationsfält till höger på skärmen. Informationsfältet innehåller en kort beskrivning av den valda källan samt alternativ för att ansluta till källan eller visa dess dokumentation. Om du vill skapa en ny inkommande basanslutning väljer du **[!UICONTROL Add data]**.

![](../../../../images/tutorials/create/redshift/catalog.png)

Sidan visas *[!UICONTROL Connect to Amazon Redshift]* . På den här sidan kan du antingen använda nya autentiseringsuppgifter eller befintliga.

### Nytt konto

Om du använder nya autentiseringsuppgifter väljer du **[!UICONTROL New account]**. På det indataformulär som visas anger du ett namn, en valfri beskrivning och dina [!DNL Redshift] inloggningsuppgifter för basanslutningen. När du är klar väljer du **[!UICONTROL Connect]** och tillåt sedan lite tid för att upprätta den nya basanslutningen.

![](../../../../images/tutorials/create/redshift/new.png)

### Befintligt konto

Om du vill ansluta ett befintligt konto markerar du det [!DNL Redshift] konto du vill ansluta till och väljer sedan **[!UICONTROL Next]** att fortsätta.

![](../../../../images/tutorials/create/redshift/existing.png)

## Nästa steg

Genom att följa den här självstudiekursen har du upprättat en basanslutning till ditt [!DNL Redshift] konto. Du kan nu fortsätta med nästa självstudiekurs och [konfigurera ett dataflöde för att hämta data till plattformen](../../dataflow/databases.md).