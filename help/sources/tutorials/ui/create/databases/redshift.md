---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Skapa en källanslutning till Amazon Redshift i användargränssnittet
topic: overview
translation-type: tm+mt
source-git-commit: 5ad763d2167c68f3293a2813248efaee22230a52
workflow-type: tm+mt
source-wordcount: '506'
ht-degree: 0%

---


# Skapa en källanslutning till Amazon Redshift i användargränssnittet

>The [!NOTE]
>Amazon Redshift-kopplingen är i betaversion. Mer information om hur du använder betatecknade anslutningar finns i [Källor-översikten](../../../../home.md#terms-and-conditions) .

Källkopplingar i Adobe Experience Platform ger möjlighet att importera externt källdata på schemalagd basis. I den här självstudiekursen beskrivs hur du skapar en källkoppling för Amazon Redshift (nedan kallad Redshift) med hjälp av Platform användargränssnitt.

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

- [Experience Data Model (XDM) System](../../../../../xdm/home.md): Det standardiserade ramverk som Experience Platform använder för att ordna kundupplevelsedata.
   - [Grundläggande om schemakomposition](../../../../../xdm/schema/composition.md): Lär dig mer om de grundläggande byggstenarna i XDM-scheman, inklusive viktiga principer och bästa praxis när det gäller schemakomposition.
   - [Schemaredigeraren, genomgång](../../../../../xdm/tutorials/create-schema-ui.md): Lär dig hur du skapar anpassade scheman med hjälp av gränssnittet för Schemaredigeraren.
- [Kundprofil](../../../../../profile/home.md)i realtid: Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

Om du redan har en Redshift-basanslutning kan du hoppa över resten av det här dokumentet och gå vidare till självstudiekursen om hur du [konfigurerar ett dataflöde](../../dataflow/databases.md).

### Samla in nödvändiga inloggningsuppgifter

Du måste ange följande värden för att komma åt ditt Redshift-konto på Platform:

| **Autentiseringsuppgifter** | **Beskrivning** |
| -------------- | --------------- |
| `server` | Den server som är associerad med ditt Redshift-konto. |
| `username` | Användarnamnet som är associerat med ditt Redshift-konto. |
| `password` | Lösenordet som är kopplat till ditt Redshift-konto. |
| `database` | Databasen för Redshift som du använder. |

Mer information om hur du kommer igång finns i [detta Redshift-dokument](https://docs.aws.amazon.com/redshift/latest/gsg/getting-started.html).

## Anslut ditt Redshift-konto

När du har samlat in dina inloggningsuppgifter kan du följa stegen nedan för att skapa en ny inkommande basanslutning som länkar ditt Redshift-konto till Platform.

Logga in på <a href="https://platform.adobe.com" target="_blank">Adobe Experience Platform</a> och välj sedan **Källor** i det vänstra navigeringsfältet för att komma åt arbetsytan *Källor* . På *katalogskärmen* visas en mängd olika källor som du kan skapa inkommande basanslutningar för, och varje källa visar antalet befintliga basanslutningar som är kopplade till dem.

Under kategorin *Databaser* väljer du **Amazon Redshift** för att visa ett informationsfält till höger på skärmen. Informationsfältet innehåller en kort beskrivning av den valda källan samt alternativ för att ansluta till källan eller visa dess dokumentation. Om du vill skapa en ny inkommande basanslutning väljer du **Anslut källa**.

![](../../../../images/tutorials/create/redshift/catalog.png)

Sidan *Anslut till Amazon Redshift* visas. På den här sidan kan du antingen använda nya autentiseringsuppgifter eller befintliga.

### Nytt konto

Om du använder nya autentiseringsuppgifter väljer du **Nytt konto**. På indataformuläret som visas anger du ett namn, en valfri beskrivning och dina uppgifter för Redshift. När du är klar väljer du **Anslut** och tillåt sedan en tid för att upprätta den nya basanslutningen.

![](../../../../images/tutorials/create/redshift/new.png)

### Befintligt konto

Om du vill ansluta ett befintligt konto väljer du det konto för växling av ändringar som du vill ansluta till och sedan väljer du **Nästa** för att fortsätta.

![](../../../../images/tutorials/create/redshift/existing.png)

## Nästa steg

Genom att följa den här självstudiekursen har du upprättat en basanslutning till ditt Redshift-konto. Du kan nu fortsätta med nästa självstudiekurs och [konfigurera ett dataflöde för att hämta data till Platform](../../dataflow/databases.md).