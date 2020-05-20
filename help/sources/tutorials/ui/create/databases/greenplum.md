---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Skapa en GreenPlum-källkoppling i användargränssnittet
topic: overview
translation-type: tm+mt
source-git-commit: a015d2612bc5a72004e15dc5706c7718617a0af4
workflow-type: tm+mt
source-wordcount: '483'
ht-degree: 0%

---


# Skapa en GreenPlum-källkoppling i användargränssnittet

> [!NOTE]
> GreenPlum-kopplingen är i betaversion. Funktionerna och dokumentationen kan komma att ändras.

Källkopplingar i Adobe Experience Platform gör det möjligt att importera externt källdata på schemalagd basis. I den här självstudiekursen beskrivs hur du skapar en GreenPlum-källanslutning med hjälp av användargränssnittet för plattformen.

## Komma igång

Den här självstudien kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [Experience Data Model (XDM) System](../../../../../xdm/home.md): Det standardiserade ramverk som Experience Platform använder för att organisera kundupplevelsedata.
   * [Grundläggande om schemakomposition](../../../../../xdm/schema/composition.md): Lär dig mer om de grundläggande byggstenarna i XDM-scheman, inklusive viktiga principer och bästa praxis när det gäller schemakomposition.
   * [Schemaredigeraren, genomgång](../../../../../xdm/tutorials/create-schema-ui.md): Lär dig hur du skapar anpassade scheman med hjälp av gränssnittet för Schemaredigeraren.
* [Kundprofil](../../../../../profile/home.md)i realtid: Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

Om du redan har en giltig GreenPlum-anslutning kan du hoppa över resten av det här dokumentet och gå vidare till självstudiekursen om hur du [konfigurerar ett dataflöde](../../dataflow/databases.md).

### Samla in nödvändiga inloggningsuppgifter

I följande avsnitt finns ytterligare information som du behöver känna till för att kunna ansluta till GreenPlum med API:t för Flow Service.

| Autentiseringsuppgifter | Beskrivning |
| ---------- | ----------- |
| `connectionString` | Anslutningssträngen som används för att ansluta till din GreenPlum-instans. Anslutningssträngsmönstret för GreenPlum är `HOST=<server>;PORT=<port>;DB=<database>;UID=<user name>;PWD=<password>` |

Mer information om hur du kommer igång finns i [det här GreenPlum-dokumentet](https://gpdb.docs.pivotal.io/580/security-guide/topics/Authenticate.html#topic_fzv_wb2_jr__config_ssl_client_conn).

## Anslut ditt GreenPlum-konto

När du har samlat in dina inloggningsuppgifter kan du följa stegen nedan för att skapa ett nytt GreenPlum-konto för att ansluta till plattformen.

Logga in på [Adobe Experience Platform](https://platform.adobe.com) och välj sedan **[!UICONTROL Sources]** i det vänstra navigeringsfältet för att komma åt *[!UICONTROL Sources]* arbetsytan. På *[!UICONTROL Catalog]* skärmen visas en mängd olika källor som du kan skapa ett inkommande konto för, och varje källa visar antalet befintliga konton och datauppsättningsflöden som är kopplade till dem.

Du kan välja lämplig kategori i katalogen till vänster på skärmen. Du kan också hitta den källa du vill arbeta med med med sökalternativet.

Under *[!UICONTROL Databases]* kategorin väljer du **[!UICONTROL GreenPlum]** att klicka **på +-ikonen (+)** för att skapa en ny GreenPlum-koppling.

![katalog](../../../../images/tutorials/create/greenplum/catalog.png)

Sidan visas *[!UICONTROL Connect to GreenPlum]* . På den här sidan kan du antingen använda nya autentiseringsuppgifter eller befintliga.

### Nytt konto

Om du använder nya autentiseringsuppgifter väljer du **[!UICONTROL New account]**. På indataformuläret som visas anger du en anslutning med ett namn, en valfri beskrivning och dina inloggningsuppgifter för GreenPlum. När du är klar väljer du **[!UICONTROL Connect]** och tillåt sedan en tid för det nya kontot att upprätta.

![koppla](../../../../images/tutorials/create/greenplum/new.png)

### Befintligt konto

Om du vill ansluta till ett befintligt konto väljer du det GreenPlum-konto som du vill ansluta till och fortsätter sedan **[!UICONTROL Next]** i det övre högra hörnet.

![befintlig](../../../../images/tutorials/create/greenplum/existing.png)

## Nästa steg

Genom att följa den här självstudiekursen har du upprättat en anslutning till ditt GreenPlum-konto. Du kan nu fortsätta med nästa självstudiekurs och [konfigurera ett dataflöde för att hämta data till plattformen](../../dataflow/databases.md).