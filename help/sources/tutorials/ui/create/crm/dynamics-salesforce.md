---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Skapa en Microsoft Dynamics- eller Salesforce-källkoppling i användargränssnittet
topic: overview
translation-type: tm+mt
source-git-commit: f09ff4d1b159a6989868c5cfc35b361cfb640a99

---


# Skapa en Microsoft Dynamics- eller Salesforce-källkoppling i användargränssnittet

Källkopplingar i Adobe Experience Platform gör det möjligt att importera externt källkodsdata i CRM på schemalagd basis. I den här självstudiekursen beskrivs hur du skapar en Microsoft Dynamics- (nedan kallad Dynamics) eller Salesforce-källkoppling med hjälp av användargränssnittet för plattformen.

## Komma igång

Den här självstudien kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [Experience Data Model (XDM) System](../../../../../xdm/home.md): Det standardiserade ramverk som Experience Platform använder för att organisera kundupplevelsedata.
   * [Grundläggande om schemakomposition](../../../../../xdm/schema/composition.md): Lär dig mer om de grundläggande byggstenarna i XDM-scheman, inklusive viktiga principer och bästa praxis när det gäller schemakomposition.
   * [Schemaredigeraren, genomgång](../../../../../xdm/tutorials/create-schema-ui.md): Lär dig hur du skapar anpassade scheman med hjälp av gränssnittet för Schemaredigeraren.
* [Kundprofil](../../../../../profile/home.md)i realtid: Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

Om du redan har en Microsoft Dynamics- eller Salesforce-basanslutning kan du hoppa över resten av det här dokumentet och gå vidare till självstudiekursen om [att konfigurera ett dataflöde](../../dataflow/crm.md).

### Samla in nödvändiga inloggningsuppgifter

För att få åtkomst till ditt Dynamics-konto på Platform måste du ange en **tjänst-URI**, **användarnamn** och **lösenord**.

På samma sätt måste du ange en **miljöadress**, **användarnamn**, **lösenord** och **säkerhetstoken** för att få tillgång till ditt Salesforce-konto på Platform.

## Anslut ditt Dynamics- eller Salesforce-konto

Med CRM-systemets autentiseringsuppgifter klara kan du följa stegen nedan för att skapa en ny inkommande basanslutning som länkar ditt Dynamics- eller Salesforce-konto till plattformen.

Logga in på <a href="https://platform.adobe.com" target="_blank">Adobe Experience Platform</a> och välj sedan **Källor** i det vänstra navigeringsfältet för att komma åt källarbetsytan. På *katalogskärmen* visas en mängd olika källor som du kan skapa inkommande basanslutningar för, och varje källa visar antalet befintliga basanslutningar som är kopplade till dem.

Under kategorin *CRM* väljer du antingen **Microsoft Dynamics** eller **Salesforce** för att visa ett informationsfält till höger på skärmen. Informationsfältet innehåller en kort beskrivning av den valda källan samt alternativ för att visa dess dokumentation eller ansluta till källan. Om du vill skapa en ny inkommande basanslutning klickar du på **Anslut källa**.

![](../../../../images/tutorials/create/salesforce/sf_sources_catalog.png)

På indataformuläret anger du basanslutningen med ett namn, en valfri beskrivning och dina Dynamics- eller Salesforce-inloggningsuppgifter. Klicka slutligen på **Anslut** och tillåt lite tid för att upprätta den nya basanslutningen.

![](../../../../images/tutorials/create/salesforce/sf_credentials.png)

När du har upprättat en basanslutning till CRM-systemet kan du fortsätta till nästa avsnitt och konfigurera ett dataflöde för att överföra CRM-data till plattformen.

## Nästa steg

Genom att följa den här självstudiekursen har du upprättat en basanslutning till ditt Dynamics- eller Salesforce-konto. Du kan nu fortsätta med nästa självstudiekurs och [konfigurera ett dataflöde för att hämta data till plattformen](../../dataflow/crm.md).