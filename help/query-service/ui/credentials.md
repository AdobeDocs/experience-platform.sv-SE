---
keywords: Experience Platform;home;populära topics;query service;Query service;query editor;Query Editor;Query editor;Query editor;
solution: Experience Platform
title: Handbok för autentiseringsuppgifter för frågetjänst
topic-legacy: guide
description: Adobe Experience Platform Query Service har ett användargränssnitt som kan användas för att skriva och köra frågor, visa frågor som har körts tidigare och få åtkomst till frågor som sparats av användare i din IMS-organisation.
exl-id: ea25fa32-809c-429c-b855-fcee5ee31b3e
source-git-commit: e4526b515dc6f480136615f3aa78f38f3e43a60f
workflow-type: tm+mt
source-wordcount: '1158'
ht-degree: 0%

---

# Handbok för autentiseringsuppgifter

Med Adobe Experience Platform Query Service kan du ansluta till externa klienter. Du kan ansluta till dessa externa klienter genom att använda antingen utgångsdatum eller ej utgångsdatum.

## Utgående autentiseringsuppgifter

Du kan använda utgångsuppgifter för att snabbt konfigurera en anslutning till en extern klient.

![Fliken Autentiseringsuppgifter för kontrollpanelen Frågor med avsnittet Utgångsuppgifter markerat.](../images/ui/credentials/expiring-credentials.png)

The **[!UICONTROL Expiring credentials]** innehåller följande information:

- **[!UICONTROL Host]**: Namnet på värden som du ansluter till. Vid anslutning till frågetjänsten innehåller detta namnet på den IMS-organisation som du för närvarande använder.
- **[!UICONTROL Port]**: Portnumret för värddatorn som du ansluter till.
- **[!UICONTROL Database]**: Namnet på den databas som du ansluter till.
- **[!UICONTROL Username]**: Användarnamnet som du använder för att ansluta till frågetjänsten.
- **[!UICONTROL Password]**: Lösenordet som du ska använda för att ansluta till frågetjänsten.
- **[!UICONTROL PSQL command]**: Ett kommando som automatiskt har infogat all relevant information för att ansluta till frågetjänsten med PSQL på kommandoraden.
- **[!UICONTROL Expires]**: Utgångsdatumet för inloggningsuppgifterna. Autentiseringsuppgifterna går ut 24 timmar efter att de har skapats.

## Giltiga autentiseringsuppgifter {#non-expiring-credentials}

Du kan använda autentiseringsuppgifter som inte upphör att gälla för att konfigurera en mer permanent anslutning till en extern klient.

### Förutsättningar

Innan du kan generera autentiseringsuppgifter som inte förfaller måste du utföra följande steg i Adobe Admin Console:

1. Logga in [Adobe Admin Console](https://adminconsole.adobe.com/) och välj relevant organisation i det övre navigeringsfältet.
2. [Välj en produktprofil.](../../access-control/ui/browse.md)
3. [Konfigurera båda **Sandlådor** och **Hantera integrering av frågetjänst** behörigheter](../../access-control/ui/permissions.md) för produktprofilen.
4. [Lägga till en ny användare i en produktprofil](../../access-control/ui/users.md) så att de får sina konfigurerade behörigheter.
5. [Lägg till användaren som produktprofiladministratör](https://helpx.adobe.com/enterprise/using/manage-product-profiles.html) för att tillåta att konton skapas för alla aktiva produktprofiler.
6. [Lägg till användaren som produktprofilutvecklare](https://helpx.adobe.com/enterprise/using/manage-developers.html) för att skapa en integrering.

Mer information om hur du tilldelar behörigheter finns i dokumentationen om [åtkomstkontroll](../../access-control/home.md).

Alla behörigheter som krävs har nu konfigurerats i Adobe Developer Console så att användaren kan använda funktionen för förfalloinloggningsuppgifter.

### Generera autentiseringsuppgifter

Om du vill skapa en uppsättning med autentiseringsuppgifter som inte upphör att gälla går du tillbaka till användargränssnittet för plattformen och väljer **[!UICONTROL Queries]** från vänster navigering för att komma åt [!UICONTROL Queries] arbetsyta. Välj sedan **[!UICONTROL Credentials]** följt av **[!UICONTROL Generate credentials]**.

![Kontrollpanelen Frågor med fliken Autentiseringsuppgifter och Generera autentiseringsuppgifter markerade.](../images/ui/credentials/generate-credentials.png)

En dialogruta visas där du kan generera autentiseringsuppgifter. Om du vill skapa inloggningsuppgifter som inte förfaller måste du ange följande information:

- **[!UICONTROL Name]**: Namnet på de autentiseringsuppgifter som du genererar.
- **[!UICONTROL Description]**: (Valfritt) En beskrivning av de autentiseringsuppgifter som du genererar.
- **[!UICONTROL Assigned to]**: Användaren som autentiseringsuppgifterna ska tilldelas till. Värdet ska vara e-postadressen till den användare som skapar inloggningsuppgifterna.
- **[!UICONTROL Password]** (Valfritt) Ett valfritt lösenord för dina inloggningsuppgifter. Om lösenordet inte är inställt genererar Adobe automatiskt ett lösenord åt dig.

När du har angett all nödvändig information väljer du **[!UICONTROL Generate credentials]** för att generera dina autentiseringsuppgifter.

![Dialogrutan Generera inloggningsuppgifter är markerad.](../images/ui/credentials/create-account.png)

>[!IMPORTANT]
>
>När **[!UICONTROL Generate credentials]** väljs hämtas en konfigurations-JSON-fil till den lokala datorn. Eftersom Adobe gör det **not** spela in de genererade inloggningsuppgifterna, måste du lagra den hämtade filen på ett säkert sätt och spara en inloggningsuppgift.
>
>Om inloggningsuppgifterna inte används på 90 dagar kommer de dessutom att tas bort.

JSON-konfigurationsfilen innehåller information som namn på tekniskt konto, ID för tekniskt konto och autentiseringsuppgifter. Den tillhandahålls i följande format.

```json
{"technicalAccountName":"9F0A21EE-B8F3-4165-9871-846D3C8BC49E@TECHACCT.ADOBE.COM","credential":"3d184fa9e0b94f33a7781905c05203ee","technicalAccountId":"4F2611B8613AA3670A495E55"}
```

När du har sparat dina genererade inloggningsuppgifter väljer du **[!UICONTROL Close]**. Nu kan du se en lista över alla dina ej förfallna autentiseringsuppgifter.

![Fliken Autentiseringsuppgifter för kontrollpanelen Frågor med avsnittet Ej förfallande autentiseringsuppgifter markerat.](../images/ui/credentials/list-credentials.png)

Du kan antingen redigera eller ta bort dina uppgifter som inte förfaller. Om du vill redigera en referens som inte förfaller väljer du pennikonen (![En pennikon.](../images/ui/credentials/edit-icon.png)). Om du vill ta bort en autentiseringsuppgift som inte upphör att gälla väljer du ikonen Ta bort (![En papperskorgsikon.](../images/ui/credentials/delete-icon.png)).

När du redigerar en referens som inte förfaller visas ett modalt värde. Du kan uppdatera följande information:

- **[!UICONTROL Name]**: Namnet på de autentiseringsuppgifter som du genererar.
- **[!UICONTROL Description]**: (Valfritt) En beskrivning av de autentiseringsuppgifter som du genererar.
- **[!UICONTROL Assigned to]**: Användaren som autentiseringsuppgifterna ska tilldelas till. Värdet ska vara e-postadressen till den användare som skapar inloggningsuppgifterna.

![Dialogrutan Uppdatera konto.](../images/ui/credentials/update-credentials.png)

När du har angett all nödvändig information väljer du **[!UICONTROL Update account]** för att slutföra uppdateringen av dina autentiseringsuppgifter.

## Använda autentiseringsuppgifter för att ansluta till externa klienter

Du kan använda autentiseringsuppgifterna som förfaller eller inte förfaller för att ansluta till externa klienter, som Aqua Data Studio, Looker eller Power BI. Indatametoden för dessa autentiseringsuppgifter varierar beroende på den externa klienten. Mer information om hur du använder dessa autentiseringsuppgifter finns i den externa klientens dokumentation.

Bilden anger platsen för varje parameter som hittas i användargränssnittet, med undantag för lösenordet för de autentiseringsuppgifter som inte förfaller. Även om inloggningsuppgifterna som inte förfaller anges i JSON-konfigurationsfilerna kan du visa dina förfallande inloggningsuppgifter under **Autentiseringsuppgifter** i användargränssnittet.

![Fliken Autentiseringsuppgifter för arbetsytan Frågor med avsnittet Utgångsuppgifter markerat.](../images/ui/credentials/expiring-credentials.png)

Tabellen nedan visar de parametrar som vanligtvis krävs för att ansluta till externa klienter.

>[!NOTE]
>
>När du ansluter till en värd med autentiseringsuppgifter som inte upphör att gälla, är det fortfarande nödvändigt att använda alla parametrar som anges i [!UICONTROL EXPIRING CREDENTIALS] utom för lösenordet och användarnamnet.
>Formatet för att ange ditt användarnamn och lösenord använder kolonavgränsade värden som visas i det här exemplet `username:{your_username}` och `password:{password_string}`.

| Parameter | Beskrivning |
|---|---|
| **Server/värd** | Namnet på den server/värd som du ansluter till. <ul><li>Det här värdet används både för utgångsdatum och icke-utgångsdatum och har formen av `server.adobe.io`. Värdet finns under **[!UICONTROL Host]** i [!UICONTROL EXPIRING CREDENTIALS] -avsnitt.</ul></li> |
| **Port** | Porten för den server/värd som du ansluter till. <ul><li>Det här värdet används både för utgångsdatum och icke-utgångsdatum och finns under **[!UICONTROL Port]** i [!UICONTROL EXPIRING CREDENTIALS] -avsnitt. Ett exempelvärde för porten skulle vara `80`.</ul></li> |
| **Databas** | Databasen som du ansluter till. <ul><li>Det här värdet används både för utgångsdatum och icke-utgångsdatum för inloggningsuppgifter och finns under **[!UICONTROL Database]** i [!UICONTROL EXPIRING CREDENTIALS] -avsnitt. Ett exempelvärde för databasen skulle vara `prod:all`.</ul></li> |
| **Användarnamn** | Användarnamnet för användaren som ansluter till den externa klienten. <ul><li>Det här värdet används både för utgångsdatum och icke-utgångsdatum. Det tar formen av en alfanumerisk sträng före `@AdobeOrg`. Detta värde finns under **[!UICONTROL Username]**.</li></ul> |
| **Lösenord** | Lösenordet för den användare som ansluter till den externa klienten. <ul><li>Om du använder inloggningsuppgifter som förfaller finns dessa under **[!UICONTROL Password]** inom [!UICONTROL EXPIRING CREDENTIALS] -avsnitt.</li><li>Om du använder inloggningsuppgifter som inte upphör att gälla är det här värdet de sammanfogade argumenten från technicalAccountID och inloggningsuppgifterna från JSON-konfigurationsfilen. Lösenordsvärdet har följande format: `{technicalAccountId}:{credential}`.</li></ul> |

## Nästa steg

Nu när du förstår hur både förfallodatum och icke-utgångsdatum fungerar kan du använda dessa autentiseringsuppgifter för att ansluta till externa klienter. Mer information om externa klienter finns i [ansluta klienter till frågetjänstguiden](../clients/overview.md).
