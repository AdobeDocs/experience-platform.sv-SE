---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Skapa en direktuppspelningsanslutning med användargränssnittet
topic: tutorial
translation-type: tm+mt
source-git-commit: 181719e729748adcde62199c9406a97b7a807182

---


# Skapa en direktuppspelningsanslutning med användargränssnittet

Den här gränssnittshandboken hjälper dig att skapa en direktuppspelningsanslutning med Adobe Experience Platform.

## Komma igång

För att kunna starta direktuppspelning av data på Experience Platform måste du först skapa en direktuppspelad HTTP-anslutning. När du skapar en direktuppspelningsanslutning måste du ange nyckeldetaljer som till exempel källan för direktuppspelningsdata och om du tänker skicka data från en tillförlitlig (autentiserad) eller en otillförlitlig (ej autentiserad) källa eller inte.

När du har registrerat en direktuppspelningsanslutning får du en unik URL som kan användas för att strömma data till plattformen.

Observera att du måste ha tillgång till Adobe Experience Platform för att kunna slutföra den här guiden. Om du inte har tillgång till plattformen kontaktar du systemadministratören innan du fortsätter.

## Skapa en direktuppspelningsanslutning

När du har loggat in på Experience Platform-gränssnittet klickar du på **Källor** för att öppna fliken *Katalog* . På den här sidan visas tillgängliga källtyper som enskilda kort, där varje kort innehåller en bubbla som visar antalet dataflöden som har skapats från direktuppspelningsanslutningar till datauppsättningar.

![](../images/streaming-ingestion/ui/click-sources.png)

På sidan *Källor* klickar du på **HTTP API** och sedan på **Connect source**.

![](../images/streaming-ingestion/ui/click-connect-source.png)

Skärmen *Anslut till HTTP* visas. Ange både *namn* och en **beskrivning** för den nya direktuppspelningsanslutningen under **Tjänstinformation** .

Under *Kontoautentisering* väljer du följande konfigurationsegenskaper för din direktuppspelningsanslutning:

- **Autentisering:** Om direktuppspelningsanslutningen kräver autentisering eller inte. Autentisering säkerställer att data samlas in från betrodda källor. Vi rekommenderar att detta är aktiverat om det handlar om personligt identifierbar information (PII).
- **XDM-schemakompatibilitet:** Anger om den här direktuppspelningsanslutningen ska skicka händelser som är kompatibla med XDM-scheman eller inte. Som standard är den här egenskapen **aktiverad**.

När du har valt konfigurationsegenskaperna klickar du på **Anslut**. Din HTTP-direktuppspelningsanslutning har skapats och kan nu visas på fliken *Bläddra* på arbetsytan *Källor* .

![](../images/streaming-ingestion/ui/http-sources-details.png)

På fliken *Bläddra* kan du klicka på din nyligen skapade Streaming HTTP Connection och visa information om anslutningen.

![](../images/streaming-ingestion/ui/browse-sources.png)

Genom att klicka på hyperlänken för anslutningsnamnet kan du välja vilka data som ska visas genom att konfigurera vilken datauppsättning som ska anslutas genom att klicka på *Välj data*.

![](../images/streaming-ingestion/ui/select-data.png)

Du kan antingen [skapa en ny datauppsättning](#create-a-new-dataset) eller [använda en befintlig datauppsättning](#use-an-existing-dataset).

### Skapa en ny datauppsättning

Om du vill skapa en ny datauppsättning anger du **namn**, **beskrivning** och **målschema** för datauppsättningen.

![](../images/streaming-ingestion/ui/create-new-dataset.png)

När du infogar all information och klickar på **Nästa** kan du granska informationen innan du klickar på **Slutför** för att ansluta datauppsättningen till din HTTP-direktuppspelningsanslutning.

![](../images/streaming-ingestion/ui/review-create-new-dataset.png)

### Använd en befintlig datauppsättning

Om du vill använda en befintlig datauppsättning markerar du **namnet** på utdatauppsättningen.

![](../images/streaming-ingestion/ui/use-existing-dataset.png)

När du har klickat på **Nästa** kan du granska informationen innan du klickar på **Slutför** för att ansluta den markerade datauppsättningen till din HTTP-direktuppspelningsanslutning.

![](../images/streaming-ingestion/ui/review-existing-dataset.png)

## Nästa steg

Genom att följa den här självstudiekursen har du skapat en direktuppspelande HTTP-anslutning, så att du kan använda direktuppspelningsslutpunkten för att få tillgång till en mängd olika API:er för datainmatning. Instruktioner om hur du skapar en direktuppspelningsanslutning i API:t finns i självstudiekursen [Skapa en direktuppspelningsanslutning](../tutorials/create-streaming-connection.md).
