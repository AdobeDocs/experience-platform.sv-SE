---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Skapa en allmän OData-källanslutning i användargränssnittet
topic: overview
translation-type: tm+mt
source-git-commit: 8c67ba710b486501374020ab505b04931f327c0f

---


# Skapa en allmän OData-källanslutning i användargränssnittet

Källkopplingar i Adobe Experience Platform gör det möjligt att importera externt källdata på schemalagd basis. I den här självstudiekursen beskrivs hur du skapar en allmän källkoppling för Open Data Protocol (nedan kallad OData) med hjälp av användargränssnittet för plattformen.

## Komma igång

Den här självstudien kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [Experience Data Model (XDM) System](../../../../../xdm/home.md): Det standardiserade ramverk som Experience Platform använder för att organisera kundupplevelsedata.
   * [Grundläggande om schemakomposition](../../../../../xdm/schema/composition.md): Lär dig mer om de grundläggande byggstenarna i XDM-scheman, inklusive viktiga principer och bästa praxis när det gäller schemakomposition.
   * [Schemaredigeraren, genomgång](../../../../../xdm/tutorials/create-schema-ui.md): Lär dig hur du skapar anpassade scheman med hjälp av gränssnittet för Schemaredigeraren.
* [Kundprofil](../../../../../profile/home.md)i realtid: Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

Om du redan har en giltig OData-anslutning kan du hoppa över resten av det här dokumentet och fortsätta med självstudiekursen om hur du [konfigurerar ett protokolldatauppsättningsflöde](../../dataflow/protocols.md)

### Samla in nödvändiga inloggningsuppgifter

För att få tillgång till ditt OData-konto i Platform måste du ange följande värden:

| Autentiseringsuppgifter | Beskrivning |
| ---------- | ----------- |
| `url` | rot-URL:en för OData-tjänsten. |

Mer information om hur du kommer igång finns i [detta OData-dokument](https://www.odata.org/getting-started/basic-tutorial/).

## Anslut ditt OData-konto

När du har samlat in dina inloggningsuppgifter kan du följa stegen nedan för att skapa ett nytt OData-konto för att ansluta till plattformen.

Logga in på <a href="https://platform.adobe.com" target="_blank">Adobe Experience Platform</a> och välj sedan **Källor** i det vänstra navigeringsfältet för att komma åt arbetsytan *Källor* . På *katalogskärmen* visas en mängd olika källor som du kan skapa inkommande konto för. Varje källa visar antalet befintliga konton och datauppsättningsflöden som är kopplade till dem.

Du kan välja lämplig kategori i katalogen till vänster på skärmen. Du kan också hitta den källa du vill arbeta med med med sökalternativet.

Under kategorin *Protokoll* väljer du **Allmän OData** för att visa ett informationsfält till höger på skärmen. Informationsfältet innehåller en kort beskrivning av den valda källan samt alternativ för att ansluta till källan eller visa dess dokumentation. Om du vill skapa en ny inkommande anslutning väljer du **Anslut källa**.

![katalog](../../../../images/tutorials/create/odata/catalog.png)

Sidan *Anslut till allmän OData* visas. På den här sidan kan du antingen använda nya autentiseringsuppgifter eller befintliga.

### Nytt konto

Om du använder nya autentiseringsuppgifter väljer du **Nytt konto**. På indataformuläret som visas anger du anslutningen med ett namn, en valfri beskrivning och dina OData-autentiseringsuppgifter. När du är klar väljer du **Anslut** och tillåt sedan en tid för det nya kontot att upprätta.

![koppla](../../../../images/tutorials/create/odata/connect.png)

### Befintligt konto

Om du vill ansluta ett befintligt konto väljer du det OData-konto som du vill ansluta till och sedan väljer du **Nästa** för att fortsätta.

![befintlig](../../../../images/tutorials/create/odata/existing.png)

## Nästa steg

Genom att följa den här självstudiekursen har du upprättat en anslutning till ditt OData-konto. Du kan nu fortsätta med nästa självstudiekurs och [konfigurera ett datauppsättningsflöde för att hämta protokolldata till plattformen](../../dataflow/protocols.md).