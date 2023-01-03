---
keywords: Experience Platform;hemmabruk;populära ämnen;[!DNL PostgreSQL];[!DNL PostgreSQL];PostgreSQL
solution: Experience Platform
title: Skapa en PostgreSQL-källanslutning i användargränssnittet
topic-legacy: overview
type: Tutorial
description: Lär dig hur du skapar en PostgreSQL-källanslutning med Adobe Experience Platform-gränssnittet.
exl-id: e556d867-a1eb-4900-b8a9-189666a4f3f1
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '485'
ht-degree: 1%

---

# Skapa en [!DNL PostgreSQL] källanslutning i användargränssnittet

Källkopplingar i Adobe Experience Platform gör det möjligt att importera externt källkodsdata på schemalagd basis. Den här självstudiekursen innehåller steg för att skapa en [!DNL PostgreSQL] källkoppling med [!DNL Platform] användargränssnitt.

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Det standardiserade ramverk som [!DNL Experience Platform] organiserar kundupplevelsedata.
   * [Grunderna för schemakomposition](../../../../../xdm/schema/composition.md): Lär dig mer om de grundläggande byggstenarna i XDM-scheman, inklusive viktiga principer och bästa praxis när det gäller schemakomposition.
   * [Schemaredigeraren, genomgång](../../../../../xdm/tutorials/create-schema-ui.md): Lär dig hur du skapar anpassade scheman med hjälp av gränssnittet för Schemaredigeraren.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

Om du redan har en giltig [!DNL PostgreSQL] kan du hoppa över resten av dokumentet och gå vidare till självstudiekursen om [konfigurera ett dataflöde](../../dataflow/databases.md).

### Samla in nödvändiga inloggningsuppgifter

För att komma åt [!DNL PostgreSQL] konto på [!DNL Platform]måste du ange följande värde:

| Autentiseringsuppgifter | Beskrivning |
| ---------- | ----------- |
| `connectionString` | Anslutningssträngen som är associerad med din [!DNL PostgreSQL] konto. The [!DNL PostgreSQL] anslutningssträngsmönstret är: `Server={SERVER};Database={DATABASE};Port={PORT};UID={USERNAME};Password={PASSWORD}`. |

Mer information om hur du kommer igång finns i [[!DNL PostgreSQL] dokument](https://www.postgresql.org/docs/9.2/app-psql.html).

#### Aktivera SSL-kryptering för anslutningssträngen

Du kan aktivera SSL-kryptering för din [!DNL PostgreSQL] anslutningssträng genom att lägga till anslutningssträngen med följande egenskaper:

| Egenskap | Beskrivning | Exempel |
| --- | --- | --- |
| `EncryptionMethod` | Gör att du kan aktivera SSL-kryptering på din [!DNL PostgreSQL] data. | <uL><li>`EncryptionMethod=0`(Inaktiverat)</li><li>`EncryptionMethod=1`(Aktiverad)</li><li>`EncryptionMethod=6`(RequestSSL)</li></ul> |
| `ValidateServerCertificate` | Validerar certifikat som skickats av din [!DNL PostgreSQL] databas när `EncryptionMethod` används. | <uL><li>`ValidationServerCertificate=0`(Inaktiverat)</li><li>`ValidationServerCertificate=1`(Aktiverad)</li></ul> |

Följande är ett exempel på en [!DNL PostgreSQL] anslutningssträng tillagd med SSL-kryptering: `Server={SERVER};Database={DATABASE};Port={PORT};UID={USERNAME};Password={PASSWORD};EncryptionMethod=1;ValidateServerCertificate=1`.

## Koppla samman [!DNL PostgreSQL] konto

När du har samlat in dina inloggningsuppgifter kan du följa stegen nedan för att länka dina [!DNL PostgreSQL] konto till [!DNL Platform].

Logga in på [Adobe Experience Platform](https://platform.adobe.com) och sedan markera **[!UICONTROL Sources]** från det vänstra navigeringsfältet för att komma åt **[!UICONTROL Sources]** arbetsyta. The **[!UICONTROL Catalog]** I visas en mängd olika källor som du kan skapa ett konto med.

Du kan välja lämplig kategori i katalogen till vänster på skärmen. Du kan också hitta den källa du vill arbeta med med med sökalternativet.

Under **[!UICONTROL Databases]** kategori, välj **[!UICONTROL PostgreSQL DB]**. Om det är första gången du använder den här kopplingen väljer du **[!UICONTROL Configure]**. Annars väljer du **[!UICONTROL Add data]** för att skapa en ny [!DNL PostgreSQL] koppling.

![](../../../../images/tutorials/create/postgresql/catalog.png)

The **[!UICONTROL Connect to [!DNL PostgreSQL]]** visas. På den här sidan kan du antingen använda nya autentiseringsuppgifter eller befintliga.

### Nytt konto

Om du använder nya autentiseringsuppgifter väljer du **[!UICONTROL New account]**. Ange ett namn, en valfri beskrivning och din [!DNL PostgreSQL] autentiseringsuppgifter. När du är klar väljer du **[!UICONTROL Connect]** och tillåt sedan lite tid för att upprätta den nya anslutningen.

![](../../../../images/tutorials/create/postgresql/new.png)

### Befintligt konto

Om du vill ansluta ett befintligt konto väljer du [!DNL PostgreSQL] konto som du vill ansluta till och välj **[!UICONTROL Next]** för att fortsätta.

![](../../../../images/tutorials/create/postgresql/existing.png)

## Nästa steg

Genom att följa den här självstudiekursen har du upprättat en anslutning till [!DNL PostgreSQL] konto. Du kan nu fortsätta med nästa självstudiekurs och [konfigurera ett dataflöde för att hämta data till [!DNL Platform]](../../dataflow/databases.md).
