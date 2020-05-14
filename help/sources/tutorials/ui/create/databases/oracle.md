---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Skapa en Oracle DB-källanslutning i användargränssnittet
topic: overview
translation-type: tm+mt
source-git-commit: 2162c66b1664ecaaf0b609fe3f7ccf58c4a5d31d
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 0%

---


# Skapa en Oracle-källanslutning i användargränssnittet

> [!NOTE]
> Oracle-kopplingen är i betaversion. Funktionerna och dokumentationen kan komma att ändras.

Källkopplingar i Adobe Experience Platform gör det möjligt att importera externt källdata på schemalagd basis. I den här självstudiekursen beskrivs hur du skapar en Oracle-källanslutning med hjälp av användargränssnittet för plattformen.

## Komma igång

Den här självstudien kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [Experience Data Model (XDM) System](../../../../../xdm/home.md): Det standardiserade ramverk som Experience Platform använder för att organisera kundupplevelsedata.
   * [Grundläggande om schemakomposition](../../../../../xdm/schema/composition.md): Lär dig mer om de grundläggande byggstenarna i XDM-scheman, inklusive viktiga principer och bästa praxis när det gäller schemakomposition.
   * [Schemaredigeraren, genomgång](../../../../../xdm/tutorials/create-schema-ui.md): Lär dig hur du skapar anpassade scheman med hjälp av gränssnittet för Schemaredigeraren.
* [Kundprofil](../../../../../profile/home.md)i realtid: Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

Om du redan har en giltig Oracle DB-anslutning kan du hoppa över resten av det här dokumentet och gå vidare till självstudiekursen om hur du [konfigurerar ett dataflöde](../../dataflow/databases.md).

### Samla in nödvändiga inloggningsuppgifter

För att få åtkomst till ditt Oracle-konto på Platform måste du ange följande värden:

| Autentiseringsuppgifter | Beskrivning |
| ---------- | ----------- |
| `connectionString` | Anslutningssträngen som används för att ansluta till Oracle. Oracles anslutningssträngsmönster är: `Host=<host>;Port=<port>;Sid=<sid>;User Id=<username>;Password=<password>`. |
| `connectionSpec.id` | Den unika identifierare som krävs för att skapa en anslutning. Anslutningsspecifikations-ID för Oracle är `d6b52d86-f0f8-475f-89d4-ce54c8527328`. |

Mer information om hur du kommer igång finns i [det här Oracle-dokumentet](https://docs.oracle.com/database/121/ODPNT/featConnecting.htm#ODPNT199).

## Anslut ditt Oracle-konto

När du har samlat in dina inloggningsuppgifter kan du följa stegen nedan för att skapa ett nytt Oracle-konto för att ansluta till Platform.

Logga in på [Adobe Experience Platform](https://platform.adobe.com) och välj sedan **[!UICONTROL Sources]** i det vänstra navigeringsfältet för att komma åt *[!UICONTROL Sources]* arbetsytan. På *[!UICONTROL Catalog]* skärmen visas en mängd olika källor som du kan skapa inkommande konto för, och varje källa visar antalet befintliga konton och datauppsättningsflöden som är kopplade till dem.

Du kan välja lämplig kategori i katalogen till vänster på skärmen. Du kan också hitta den källa du vill arbeta med med med sökalternativet.

Under kategorin *Databaser* väljer du **[!UICONTROL Oracle DB]** och klickar **på +-ikonen (+)** för att skapa en ny Oracle-koppling.

![katalog](../../../../images/tutorials/create/oracle/catalog.png)

Sidan visas *[!UICONTROL Connect to Oracle DB]* . På den här sidan kan du antingen använda nya autentiseringsuppgifter eller befintliga.

### Nytt konto

Om du använder nya autentiseringsuppgifter väljer du **[!UICONTROL New account]**. På indataformuläret som visas anger du en anslutning med ett namn, en valfri beskrivning och dina Oracle-autentiseringsuppgifter. När du är klar väljer du **[!UICONTROL Connect]** och tillåt sedan en tid för det nya kontot att upprätta.

![koppla](../../../../images/tutorials/create/oracle/new.png)

### Befintligt konto

Om du vill ansluta ett befintligt konto väljer du det Oracle-konto som du vill ansluta till och väljer sedan **[!UICONTROL Next]** att fortsätta.

![befintlig](../../../../images/tutorials/create/oracle/existing.png)

## Nästa steg

Genom att följa den här självstudiekursen har du upprättat en anslutning till ditt Oracle-konto. Du kan nu fortsätta med nästa självstudiekurs och [konfigurera ett dataflöde för att hämta data till plattformen](../../dataflow/databases.md).