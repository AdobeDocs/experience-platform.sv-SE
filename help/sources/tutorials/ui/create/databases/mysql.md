---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Skapa en MySQL-källkoppling i användargränssnittet
topic: overview
translation-type: tm+mt
source-git-commit: 4f7d7e2bf255afe1588dbe7cfb2ec055f2dcbf75
workflow-type: tm+mt
source-wordcount: '472'
ht-degree: 0%

---


# Skapa en MySQL-källkoppling i användargränssnittet

>[!NOTE]
> MySQL-kopplingen är i betaversion. Mer information om hur du använder betatecknade anslutningar finns i [Källor-översikten](../../../../home.md#terms-and-conditions) .

Källkopplingar i Adobe Experience Platform ger möjlighet att importera externt källdata på schemalagd basis. I den här självstudiekursen beskrivs hur du skapar en MySQL-källkoppling med Platform användargränssnitt.

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [Experience Data Model (XDM) System](../../../../../xdm/home.md): Det standardiserade ramverk som Experience Platform använder för att ordna kundupplevelsedata.
   * [Grundläggande om schemakomposition](../../../../../xdm/schema/composition.md): Lär dig mer om de grundläggande byggstenarna i XDM-scheman, inklusive viktiga principer och bästa praxis när det gäller schemakomposition.
   * [Schemaredigeraren, genomgång](../../../../../xdm/tutorials/create-schema-ui.md): Lär dig hur du skapar anpassade scheman med hjälp av gränssnittet för Schemaredigeraren.
* [Kundprofil](../../../../../profile/home.md)i realtid: Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

Om du redan har en MySQL-basanslutning kan du hoppa över resten av det här dokumentet och gå vidare till självstudiekursen om hur du [konfigurerar ett dataflöde](../../dataflow/databases.md).

### Samla in nödvändiga inloggningsuppgifter

För att få tillgång till ditt MySQL-konto [!DNL Platform]måste du ange följande värde:

| Autentiseringsuppgifter | Beskrivning |
| ---------- | ----------- |
| `connectionString` | Den MySQL-anslutningssträng som är associerad med ditt konto. Mönstret för MySQL-anslutningssträngen är: `Server={SERVER};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}`. |

Du kan lära dig mer om anslutningssträngar och hur du hämtar dem genom att läsa [MySQL-dokumentet](https://dev.mysql.com/doc/connector-net/en/connector-net-connections-string.html).

## Anslut ditt MySQL-konto

När du har samlat in dina inloggningsuppgifter kan du följa stegen nedan för att skapa en ny inkommande basanslutning som du kan länka ditt MySQL-konto till [!DNL Platform].

Logga in på <a href="https://platform.adobe.com" target="_blank">Adobe Experience Platform</a> och välj sedan **[!UICONTROL Sources]** i det vänstra navigeringsfältet för att komma åt *[!UICONTROL Sources]* arbetsytan. På *katalogskärmen* visas en mängd olika källor som du kan skapa inkommande basanslutningar för, och varje källa visar antalet befintliga basanslutningar som är kopplade till dem.

Under *[!UICONTROL Databases]* kategorin väljer du **[!UICONTROL MySQL]** att visa ett informationsfält till höger på skärmen. Informationsfältet innehåller en kort beskrivning av den valda källan samt alternativ för att ansluta till källan eller visa dess dokumentation. Om du vill skapa en ny inkommande basanslutning väljer du **[!UICONTROL Connect source]**.

![](../../../../images/tutorials/create/my-sql/catalog.png)

Sidan visas *[!UICONTROL Connect to MySQL]* . På den här sidan kan du antingen använda nya autentiseringsuppgifter eller befintliga.

### Nytt konto

Om du använder nya autentiseringsuppgifter väljer du **[!UICONTROL New account]**. På indataformuläret som visas anger du basanslutningen med ett namn, en valfri beskrivning och dina MySQL-autentiseringsuppgifter. När du är klar väljer du **[!UICONTROL Connect]** och tillåt sedan lite tid för att upprätta den nya basanslutningen.

![](../../../../images/tutorials/create/my-sql/new.png)

### Befintligt konto

Om du vill ansluta ett befintligt konto väljer du det MySQL-konto som du vill ansluta till och väljer sedan **[!UICONTROL Next]** att fortsätta.

![](../../../../images/tutorials/create/my-sql/existing.png)

## Nästa steg

Genom att följa den här självstudiekursen har du upprättat en basanslutning till ditt MySQL-konto. Du kan nu fortsätta med nästa självstudiekurs och [konfigurera ett dataflöde för att hämta data till Platform](../../dataflow/databases.md).