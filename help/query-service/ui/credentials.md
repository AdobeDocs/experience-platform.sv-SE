---
keywords: Experience Platform;home;populära topics;query service;Query service;query editor;Query Editor;Query editor;
solution: Experience Platform
title: Användargränssnittshandbok för frågetjänst
topic-legacy: guide
description: Adobe Experience Platform Query Service har ett användargränssnitt som kan användas för att skriva och köra frågor, visa frågor som har körts tidigare och få åtkomst till frågor som sparats av användare i din IMS-organisation.
exl-id: ea25fa32-809c-429c-b855-fcee5ee31b3e
source-git-commit: 696db8081ab8225d79cd468b7435770d407d3e3d
workflow-type: tm+mt
source-wordcount: '1102'
ht-degree: 0%

---

# Handbok för autentiseringsuppgifter

Med Adobe Experience Platform Query Service kan du ansluta till externa klienter. Du kan ansluta till dessa externa klienter genom att använda antingen utgångsdatum eller ej utgångsdatum.

## Utgående autentiseringsuppgifter

Du kan använda utgångsuppgifter för att snabbt konfigurera en anslutning till en extern klient.

![](../images/ui/credentials/expiring-credentials.png)

Avsnittet **[!UICONTROL Expiring credentials]** innehåller följande information:

- **[!UICONTROL Host]**: Namnet på värden som du ansluter till. Vid anslutning till frågetjänsten innehåller detta namnet på den IMS-organisation som du för närvarande använder.
- **[!UICONTROL Port]**: Portnumret för värddatorn som du ansluter till.
- **[!UICONTROL Database]**: Namnet på den databas som du ansluter till.
- **[!UICONTROL Username]**: Användarnamnet som du använder för att ansluta till frågetjänsten.
- **[!UICONTROL Password]**: Lösenordet som du ska använda för att ansluta till frågetjänsten.
- **[!UICONTROL PSQL command]**: Ett kommando som automatiskt har infogat all relevant information för att ansluta till frågetjänsten med PSQL på kommandoraden.
- **[!UICONTROL Expires]**: Utgångsdatumet för inloggningsuppgifterna. Autentiseringsuppgifterna går ut 24 timmar efter att de har skapats.

## Giltiga autentiseringsuppgifter

Du kan använda autentiseringsuppgifter som inte upphör att gälla för att konfigurera en mer permanent anslutning till en extern klient.

### Förutsättningar

Innan du kan generera autentiseringsuppgifter som inte förfaller måste du utföra följande steg i Adobe Admin Console:

1. Logga in på [Adobe Admin Console](https://adminconsole.adobe.com/) och välj relevant organisation i det övre navigeringsfältet.
2. [Välj en produktprofil.](../../access-control/ui/browse.md)
3. [Konfigurera både  **** sandlådor och  **Hantera** ](../../access-control/ui/permissions.md) frågetjänstintegreringsbehörigheter för produktprofilen.
4. [Lägg till en ny användare i en ](../../access-control/ui/users.md) produktprofil så att de får sina konfigurerade behörigheter.
5. [Lägg till användaren som ](https://helpx.adobe.com/enterprise/using/manage-product-profiles.html) administratör för en produktprofil så att ett konto kan skapas för en aktiv produktprofil.
6. [Lägg till användaren som ](https://helpx.adobe.com/enterprise/using/manage-developers.html) utvecklare av produktprofiler för att skapa en integrering.

Läs dokumentationen om [åtkomstkontroll](../../access-control/home.md) om du vill veta mer om hur du tilldelar behörigheter.

Alla nödvändiga behörigheter har nu konfigurerats i Adobe Developer Console så att användaren kan använda funktionen för förfallodatum för inloggningsuppgifter.

### Generera autentiseringsuppgifter

Om du vill skapa en uppsättning inloggningsuppgifter som inte upphör att gälla går du tillbaka till användargränssnittet för plattformen och väljer **[!UICONTROL Queries]** i den vänstra navigeringen för att komma åt arbetsytan [!UICONTROL Queries]. Välj sedan fliken **[!UICONTROL Credentials]** följt av **[!UICONTROL Generate credentials]**.

![](../images/ui/credentials/generate-credentials.png)

En dialogruta visas där du kan generera autentiseringsuppgifter. Om du vill skapa inloggningsuppgifter som inte förfaller måste du ange följande information:

- **[!UICONTROL Name]**: Namnet på de autentiseringsuppgifter som du genererar.
- **[!UICONTROL Description]**: (Valfritt) En beskrivning av de autentiseringsuppgifter som du genererar.
- **[!UICONTROL Assigned to]**: Användaren som autentiseringsuppgifterna ska tilldelas till. Värdet ska vara e-postadressen till den användare som skapar inloggningsuppgifterna.
- **[!UICONTROL Password]** (Valfritt) Ett valfritt lösenord för dina inloggningsuppgifter. Om lösenordet inte är inställt genererar Adobe automatiskt ett lösenord åt dig.

När du har angett all nödvändig information väljer du **[!UICONTROL Generate credentials]** för att generera dina autentiseringsuppgifter.

![](../images/ui/credentials/create-account.png)

>[!IMPORTANT]
>
>När du har valt knappen **[!UICONTROL Generate credentials]** hämtas en JSON-konfigurationsfil till den lokala datorn. Eftersom Adobe **inte** spelar in de genererade inloggningsuppgifterna, måste du lagra den hämtade filen på ett säkert sätt och spara en inloggningsuppgift.
>
>Om inloggningsuppgifterna inte används på 90 dagar kommer de dessutom att tas bort.

JSON-konfigurationsfilen innehåller information som namn på tekniskt konto, ID för tekniskt konto och autentiseringsuppgifter. Den tillhandahålls i följande format.

```json
{"technicalAccountName":"9F0A21EE-B8F3-4165-9871-846D3C8BC49E@TECHACCT.ADOBE.COM","credential":"3d184fa9e0b94f33a7781905c05203ee","technicalAccountId":"4F2611B8613AA3670A495E55"}
```

När du har sparat dina genererade inloggningsuppgifter väljer du **[!UICONTROL Close]**. Nu kan du se en lista över alla dina ej förfallna autentiseringsuppgifter.

![](../images/ui/credentials/list-credentials.png)

Du kan antingen redigera eller ta bort dina uppgifter som inte förfaller. Om du vill redigera en referens som inte upphör att gälla väljer du pennikonen (![](../images/ui/credentials/edit-icon.png)). Om du vill ta bort en autentiseringsuppgift som inte förfaller väljer du borttagningsikonen (![](../images/ui/credentials/delete-icon.png)).

När du redigerar en referens som inte förfaller visas ett modalt värde. Du kan uppdatera följande information:

- **[!UICONTROL Name]**: Namnet på de autentiseringsuppgifter som du genererar.
- **[!UICONTROL Description]**: (Valfritt) En beskrivning av de autentiseringsuppgifter som du genererar.
- **[!UICONTROL Assigned to]**: Användaren som autentiseringsuppgifterna ska tilldelas till. Värdet ska vara e-postadressen till den användare som skapar inloggningsuppgifterna.

![](../images/ui/credentials/update-credentials.png)

När du har angett all nödvändig information väljer du **[!UICONTROL Update account]** för att slutföra uppdateringen av dina autentiseringsuppgifter.

## Använda autentiseringsuppgifter för att ansluta till externa klienter

Du kan använda autentiseringsuppgifterna som förfaller eller inte förfaller för att ansluta till externa klienter, som Aqua Data Studio, Looker eller Power BI. Indatametoden för dessa autentiseringsuppgifter varierar beroende på den externa klienten. Mer information om hur du använder dessa autentiseringsuppgifter finns i den externa klientens dokumentation.

Bilden anger platsen för varje parameter som hittas i användargränssnittet, med undantag för lösenordet för de autentiseringsuppgifter som inte förfaller. Även om inloggningsuppgifter som inte förfaller anges av JSON-konfigurationsfilerna kan du visa dina förgående inloggningsuppgifter på fliken **Autentiseringsuppgifter** i användargränssnittet.

![](../images/ui/credentials/expiring-credentials.png)

Tabellen nedan visar de parametrar som vanligtvis krävs för att ansluta till externa klienter.

>[!NOTE]
>
>När du ansluter till en värd med autentiseringsuppgifter som inte upphör att gälla, är det fortfarande nödvändigt att använda alla parametrar som anges i [!UICONTROL EXPIRING CREDENTIALS]-avsnittet, förutom lösenordet och användarnamnet.

| Parameter | Beskrivning |
|---|---|
| Server/värd | Namnet på den server/värd som du ansluter till. <ul><li>Det här värdet används både för förfallodatum och icke-förfallande autentiseringsuppgifter och har formatet `server.adobe.io`. Värdet finns under **[!UICONTROL Host]** i avsnittet [!UICONTROL EXPIRING CREDENTIALS].</ul></li> |
| Port | Porten för den server/värd som du ansluter till. <ul><li>Det här värdet används både för förfallodatum och icke-förfallande autentiseringsuppgifter och finns under **[!UICONTROL Port]** i avsnittet [!UICONTROL EXPIRING CREDENTIALS]. Ett exempelvärde för porten skulle vara `80`.</ul></li> |
| Databas | Databasen som du ansluter till. <ul><li>Det här värdet används både för utgångsdatum och icke-utgångsdatum och finns under **[!UICONTROL Database]** i avsnittet [!UICONTROL EXPIRING CREDENTIALS]. Ett exempelvärde för databasen skulle vara `prod:all`.</ul></li> |
| Användarnamn | Användarnamnet för användaren som ansluter till den externa klienten. <ul><li>Om du använder utgångna autentiseringsuppgifter anges detta som en alfanumerisk sträng före `@AdobeOrg`. Det här värdet finns under **[!UICONTROL Username]**.</li><li>Om du använder inloggningsuppgifter som inte förfaller är detta en valfri sträng, men **kan inte** vara samma som `technicalAccountID`-värdet som finns i JSON-konfigurationsfilen.</li></ul> |
| Lösenord | Lösenordet för den användare som ansluter till den externa klienten. <ul><li>Om du använder inloggningsuppgifter som förfaller finns dessa under **[!UICONTROL Password]** i [!UICONTROL EXPIRING CREDENTIALS]-avsnittet.</li><li>Om du använder inloggningsuppgifter som inte upphör att gälla är det här värdet de sammanfogade argumenten från technicalAccountID och inloggningsuppgifterna från JSON-konfigurationsfilen. Lösenordsvärdet har följande format: `{technicalAccountId}:{credential}`.</li></ul> |

## Nästa steg

Nu när du förstår hur både förfallodatum och icke-utgångsdatum fungerar kan du använda dessa autentiseringsuppgifter för att ansluta till externa klienter. Mer information om externa klienter finns i [Ansluta klienter till frågetjänstguiden](../clients/overview.md).
