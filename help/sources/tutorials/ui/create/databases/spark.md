---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Skapa en Apache Spark på Azure HDInsights-källkoppling i gränssnittet
topic: overview
translation-type: tm+mt
source-git-commit: 5ad763d2167c68f3293a2813248efaee22230a52
workflow-type: tm+mt
source-wordcount: '537'
ht-degree: 0%

---


# Skapa en Apache Spark på Azure HDInsights-källkoppling i gränssnittet

> [!NOTE]
> Apache Spark på Azure HDInsights-kontakten är i betaversion. Mer information om hur du använder betatecknade anslutningar finns i [Källor-översikten](../../../../home.md#terms-and-conditions) .

Källkopplingar i Adobe Experience Platform ger möjlighet att importera externt källdata på schemalagd basis. I den här självstudiekursen beskrivs hur du skapar en Apache Spark på Azure HDInsights-källkontakten med Platform användargränssnitt.

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [Experience Data Model (XDM) System](../../../../../xdm/home.md): Det standardiserade ramverk som Experience Platform använder för att ordna kundupplevelsedata.
   * [Grundläggande om schemakomposition](../../../../../xdm/schema/composition.md): Lär dig mer om de grundläggande byggstenarna i XDM-scheman, inklusive viktiga principer och bästa praxis när det gäller schemakomposition.
   * [Schemaredigeraren, genomgång](../../../../../xdm/tutorials/create-schema-ui.md): Lär dig hur du skapar anpassade scheman med hjälp av gränssnittet för Schemaredigeraren.
* [Kundprofil](../../../../../profile/home.md)i realtid: Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

Om du redan har en giltig Spark-anslutning kan du hoppa över resten av det här dokumentet och fortsätta med självstudiekursen om [att konfigurera ett dataflöde](../../dataflow/databases.md)

### Samla in nödvändiga inloggningsuppgifter

För att få åtkomst till ditt Spark-konto på Platform måste du ange följande värden:

| Autentiseringsuppgifter | Beskrivning |
| ---------- | ----------- |
| `host` | Spark-serverns IP-adress eller värdnamn. |
| `username` | Användarnamnet som du använder för att komma åt Spark-servern. |
| `password` | Lösenordet som motsvarar användaren. |

Mer information om hur du kommer igång finns i [Spark-dokumentet](https://docs.microsoft.com/en-us/azure/hdinsight/spark/apache-spark-overview).

## Anslut ditt Spark-konto

När du har samlat in dina inloggningsuppgifter kan du följa stegen nedan för att skapa ett nytt Spark-konto för att ansluta till Platform.

Logga in på <a href="https://platform.adobe.com" target="_blank">Adobe Experience Platform</a> och välj sedan **Källor** i det vänstra navigeringsfältet för att komma åt arbetsytan *Källor* . På *katalogskärmen* visas en mängd olika källor som du kan skapa inkommande konto för, och varje källa visar antalet befintliga konton och datauppsättningsflöden som är kopplade till dem.

Du kan välja lämplig kategori i katalogen till vänster på skärmen. Du kan också hitta den källa du vill arbeta med med med sökalternativet.

Under kategorin *Databaser* väljer du **Spark** för att visa ett informationsfält till höger på skärmen. Informationsfältet innehåller en kort beskrivning av den valda källan samt alternativ för att ansluta till källan eller visa dess dokumentation. Om du vill skapa en ny inkommande anslutning väljer du **Anslut källa**.

![katalog](../../../../images/tutorials/create/spark/catalog.png)

Sidan *Anslut till Spark* visas. På den här sidan kan du antingen använda nya autentiseringsuppgifter eller befintliga.

### Nytt konto

Om du använder nya autentiseringsuppgifter väljer du **Nytt konto**. På indataformuläret som visas anger du ett namn, en valfri beskrivning och dina Spark-autentiseringsuppgifter för anslutningen. När du är klar väljer du **Anslut** och tillåt sedan en tid för det nya kontot att upprätta.

![new](../../../../images/tutorials/create/spark/new.png)

### Befintligt konto

Om du vill ansluta ett befintligt konto väljer du Spark-kontot som du vill ansluta till och sedan väljer du **Nästa** för att fortsätta.

![befintlig](../../../../images/tutorials/create/spark/existing.png)

## Nästa steg

Genom att följa den här självstudiekursen har du upprättat en anslutning till ditt Spark-konto. Du kan nu fortsätta med nästa självstudiekurs och [konfigurera ett dataflöde för att hämta data till Platform](../../dataflow/databases.md).