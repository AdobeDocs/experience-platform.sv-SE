---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Skapa en ServiceNow-källkoppling i användargränssnittet
topic: overview
translation-type: tm+mt
source-git-commit: 75ba0bce7ce070af851bbf7e220dbf08febc4c20
workflow-type: tm+mt
source-wordcount: '519'
ht-degree: 0%

---


# Skapa en ServiceNow-källkoppling i användargränssnittet

>[!NOTE]
>ServiceNow-kopplingen är i betaversion. Funktionerna och dokumentationen kan komma att ändras.

Källkopplingar i Adobe Experience Platform gör det möjligt att importera externt källdata på schemalagd basis. I den här självstudiekursen beskrivs hur du skapar en ServiceNow-källkoppling med hjälp av användargränssnittet för plattformen.

## Komma igång

Den här självstudien kräver en fungerande förståelse av följande komponenter i Adobe Experience Platform:

* [Experience Data Model (XDM) System](../../../../../xdm/home.md): Det standardiserade ramverk som Experience Platform använder för att organisera kundupplevelsedata.
   * [Grundläggande om schemakomposition](../../../../../xdm/schema/composition.md): Lär dig mer om de grundläggande byggstenarna i XDM-scheman, inklusive viktiga principer och bästa praxis när det gäller schemakomposition.
   * [Schemaredigeraren, genomgång](../../../../../xdm/tutorials/create-schema-ui.md): Lär dig hur du skapar anpassade scheman med hjälp av gränssnittet för Schemaredigeraren.
* [Kundprofil](../../../../../profile/home.md)i realtid: Ger en enhetlig konsumentprofil i realtid baserad på aggregerade data från flera källor.

Om du redan har en ServiceNow-anslutning kan du hoppa över resten av det här dokumentet och gå vidare till självstudiekursen om hur du [konfigurerar ett dataflöde](../../dataflow/customer-success.md)

### Samla in nödvändiga inloggningsuppgifter

För att få åtkomst till ditt ServiceNow-konto på Platform måste du ange följande värden:

| Autentiseringsuppgifter | Beskrivning |
| ---------- | ----------- |
| `endpoint` | Slutpunkten för ServiceNow-servern. |
| `username` | Användarnamnet som används för att ansluta till ServiceNow-servern för autentisering. |
| `password` | Lösenordet för att ansluta till ServiceNow-servern för autentisering. |

Mer information om hur du kommer igång finns i [det här ServiceNow-dokumentet](https://developer.servicenow.com/app.do#!/rest_api_doc?v=newyork&amp;id=r_TableAPI-GET).

## Anslut ditt ServiceNow-konto

När du har samlat in de nödvändiga inloggningsuppgifterna kan du följa stegen nedan för att skapa ett nytt ServiceNow-konto för att ansluta till plattformen.

Logga in på <a href="https://platform.adobe.com" target="_blank">Adobe Experience Platform</a> och välj sedan **Källor** i det vänstra navigeringsfältet för att komma åt arbetsytan *Källor* . På *katalogskärmen* visas en mängd olika källor som du kan skapa ett konto för, och varje källa visar antalet befintliga konton och datauppsättningsflöden som är kopplade till dem.

Du kan välja lämplig kategori i katalogen till vänster på skärmen. Du kan också hitta den källa du vill arbeta med med med sökalternativet.

Under kategorin *Customer Success* väljer du **ServiceNow** för att visa ett informationsfält till höger på skärmen. Informationsfältet innehåller en kort beskrivning av den valda källan samt alternativ för att ansluta till källan eller visa dess dokumentation. Om du vill skapa ett nytt konto väljer du **Anslut källa**.

![](../../../../images/tutorials/create/servicenow/catalog.png)

Sidan *Anslut till ServiceNow* visas. På den här sidan kan du antingen använda nya autentiseringsuppgifter eller befintliga.

### Nytt konto

Om du använder nya autentiseringsuppgifter väljer du **Nytt konto**. På indataformuläret som visas anger du ett namn, en valfri beskrivning och dina ServiceNow-autentiseringsuppgifter. När du är klar väljer du **Anslut** och tillåt sedan en tid för det nya kontot att upprätta.

![](../../../../images/tutorials/create/servicenow/new.png)

### Befintligt konto

Om du vill ansluta ett befintligt konto väljer du det ServiceNow-konto som du vill ansluta till och sedan väljer du **Nästa** .

![](../../../../images/tutorials/create/servicenow/existing.png)

## Nästa steg

Genom att följa den här självstudiekursen har du upprättat en anslutning till ditt ServiceNow-konto. Du kan nu fortsätta med nästa självstudiekurs och [konfigurera ett dataflöde för att hämta data till plattformen](../../dataflow/customer-success.md).
