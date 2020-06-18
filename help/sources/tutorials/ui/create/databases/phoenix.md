---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Skapa en Phoenix-källanslutning i användargränssnittet
topic: overview
translation-type: tm+mt
source-git-commit: 5ad763d2167c68f3293a2813248efaee22230a52
workflow-type: tm+mt
source-wordcount: '574'
ht-degree: 0%

---


# Skapa en Phoenix-källanslutning i användargränssnittet

> [!NOTE]
> Phoenix-kontakten är i betaversion. Mer information om hur du använder betatecknade anslutningar finns i [Källor-översikten](../../../../home.md#terms-and-conditions) .

Källkopplingar i Adobe Experience Platform ger möjlighet att importera externt källdata på schemalagd basis. I den här självstudiekursen beskrivs hur du skapar en Phoenix-källanslutning med Platform användargränssnitt.

## Komma igång

Den här självstudiekursen kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [Experience Data Model (XDM) System](../../../../../xdm/home.md): Det standardiserade ramverk som Experience Platform använder för att ordna kundupplevelsedata.
   * [Grundläggande om schemakomposition](../../../../../xdm/schema/composition.md): Lär dig mer om de grundläggande byggstenarna i XDM-scheman, inklusive viktiga principer och bästa praxis när det gäller schemakomposition.
   * [Schemaredigeraren, genomgång](../../../../../xdm/tutorials/create-schema-ui.md): Lär dig hur du skapar anpassade scheman med hjälp av gränssnittet för Schemaredigeraren.
* [Kundprofil](../../../../../profile/home.md)i realtid: Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

Om du redan har en giltig Phoenix-anslutning kan du hoppa över resten av det här dokumentet och gå vidare till självstudiekursen om hur du [konfigurerar ett dataflöde](../../dataflow/databases.md)

### Samla in nödvändiga inloggningsuppgifter

För att få tillgång till ditt Phoenix-konto på Platform måste du ange följande värden:

| Autentiseringsuppgifter | Beskrivning |
| ---------- | ----------- |
| `host` | Phoenix-serverns IP-adress eller värdnamn. |
| `port` | Den TCP-port som Phoenix-servern använder för att lyssna efter klientanslutningar. Om du ansluter till Azure HDInsights anger du porten som 443. |
| `httpPath` | Den del av URL:en som motsvarar Phoenix-servern. Ange /hbasephoenix0 om du använder Azure HDInsights-klustret. |
| `username` | Användarnamnet som du använder för att komma åt Phoenix-servern. |
| `password` | Lösenordet som motsvarar användaren. |
| `enableSsl` | En växel som anger om anslutningarna till servern är krypterade med SSL. |

Mer information om hur du kommer igång finns i [det här Phoenix-dokumentet](https://python-phoenixdb.readthedocs.io/en/latest/api.html).

## Anslut ditt Phoenix-konto

När du har samlat in dina inloggningsuppgifter kan du följa stegen nedan för att skapa ett nytt Phoenix-konto för att ansluta till Platform.

Logga in på <a href="https://platform.adobe.com" target="_blank">Adobe Experience Platform</a> och välj sedan **Källor** i det vänstra navigeringsfältet för att komma åt arbetsytan *Källor* . På *katalogskärmen* visas en mängd olika källor som du kan skapa inkommande konto för, och varje källa visar antalet befintliga konton och datauppsättningsflöden som är kopplade till dem.

Du kan välja lämplig kategori i katalogen till vänster på skärmen. Du kan också hitta den källa du vill arbeta med med med sökalternativet.

Under kategorin *Databaser* väljer du **Phoenix** för att visa ett informationsfält till höger på skärmen. Informationsfältet innehåller en kort beskrivning av den valda källan samt alternativ för att ansluta till källan eller visa dess dokumentation. Om du vill skapa en ny inkommande anslutning väljer du **Anslut källa**.

![katalog](../../../../images/tutorials/create/phoenix/catalog.png)

Sidan *Anslut till Phoenix* visas. På den här sidan kan du antingen använda nya autentiseringsuppgifter eller befintliga.

### Nytt konto

Om du använder nya autentiseringsuppgifter väljer du **Nytt konto**. På indataformuläret som visas anger du en anslutning med ett namn, en valfri beskrivning och dina Phoenix-autentiseringsuppgifter. När du är klar väljer du **Anslut** och tillåt sedan en tid för det nya kontot att upprätta.

![koppla](../../../../images/tutorials/create/phoenix/new.png)

### Befintligt konto

Om du vill ansluta till ett befintligt konto väljer du det Phoenix-konto som du vill ansluta till och väljer sedan **Nästa** för att fortsätta.

![befintlig](../../../../images/tutorials/create/phoenix/existing.png)

## Nästa steg

Genom att följa den här självstudiekursen har du upprättat en anslutning till ditt Phoenix-konto. Du kan nu fortsätta med nästa självstudiekurs och [konfigurera ett dataflöde för att hämta data till Platform](../../dataflow/databases.md).