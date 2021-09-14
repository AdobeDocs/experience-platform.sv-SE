---
keywords: Experience Platform;home;populära topics;query service;Query service;query editor;Query Editor;Query editor;
solution: Experience Platform
title: Användargränssnittshandbok för frågetjänst
topic-legacy: guide
description: Adobe Experience Platform Query Service har ett användargränssnitt som kan användas för att skriva och köra frågor, visa frågor som har körts tidigare och få åtkomst till frågor som sparats av användare i din IMS-organisation.
exl-id: ea25fa32-809c-429c-b855-fcee5ee31b3e
source-git-commit: af122e5064fc5618266948d46c438d1776cdd0cf
workflow-type: tm+mt
source-wordcount: '1259'
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

Innan du kan skapa autentiseringsuppgifter som inte förfaller måste du konfigurera både **sandlådorna** och **Hantera frågetjänstintegrering** för din organisation i Adobe Admin Console.

Logga in på [Adobe Admin Console](https://adminconsole.adobe.com/) och välj relevant organisation i det övre navigeringsfältet.

I avsnittet [!UICONTROL Products and services] i [!UICONTROL Overview] väljer du **Adobe Experience Platform**.

![Adobe Admin Console Dashboard](../images/ui/credentials/adobe-admin-console-dashboard.png)

Sidan Information om Adobe Experience Platform visas. Skapa sedan en ny profil. Välj [!UICONTROL **Ny profil**].

![Adobe Experience Platform Details page](../images/ui/credentials/aep-details.png)

Dialogrutan där du skapar en profil visas. Ange ett beskrivande namn för den nya profilen och välj [!UICONTROL **Spara**]. Sidan [!UICONTROL Settings] för din nya profil visas. Välj fliken [!UICONTROL **Behörigheter**] bland de tillgängliga alternativen.

### Aktivera behörigheterna för frågetjänsten

Kontrollera att rätt behörighetsinställningar för frågetjänsten har aktiverats för din organisation genom att söka efter och välja kategorin [!UICONTROL **frågetjänst**] i listan.

![Frågetjänstkategorin Behörigheter är markerad](../images/ui/credentials/permissions-tab-query-service-category.png)

Arbetsytan [!UICONTROL Edit Permissions] för frågetjänsten visas. Välj plusikonen (**+**) för [!UICONTROL **Hantera frågor**] och [!UICONTROL **Hantera frågetjänstintegrering**] för att lägga till dem i kolumnen [!UICONTROL Included Permission Items]. Välj sedan [!UICONTROL **Spara**] för att bekräfta ändringarna.

![Spara inkluderade behörighetsobjekt](../images/ui/credentials/edit-permissions-for-query-service-profile.png)

Du kommer nu tillbaka till fliken Inställningar > Behörigheter.

### Aktivera sandlådebehörigheter

Om du vill vara säker på att rätt sandlåda är markerad för din organisation söker du efter och väljer kategorin [!UICONTROL **Sandlådor**] i listan.

![Fliken Behörigheter, kategorin Sandlådor är markerad](../images/ui/credentials/permissions-tab-sandboxes-category.png)

Arbetsytan Sandlådor visas. I [!UICONTROL Available Permission Items] hittar du den relevanta sandlådan, i den här bilden är det sandlådan Prod. Markera plusikonen (**+**) om du vill lägga till den i [!UICONTROL Included Permission Items]. Välj sedan [!UICONTROL **Spara**] för att bekräfta ändringarna.

![Lägg till tillstånd för Prod Sandbox](../images/ui/credentials/prod-sandbox.png)

Du kommer nu tillbaka till fliken Inställningar > Behörigheter.

Det krävs ytterligare tre steg för att ge en användare åtkomst till kontofunktionen som inte förfaller.

- Lägg till en ny användare som du vill ge de nya behörigheterna till. Välj fliken [!UICONTROL **Användare**] följt av [!UICONTROL **Lägg till användare**].

![Fliken Användare Lägg till användare markerad](../images/ui/credentials/users-tab-new-user.png)

Dialogrutan Skapa användare visas. Ange ett namn och en e-postadress för den nya användaren och välj [!UICONTROL **Spara**].

- Användaren måste sedan läggas till som administratör för att kunna skapa ett konto för en aktiv produktprofil. Lägga till den nyskapade användaren som administratör. Välj fliken [!UICONTROL **Administratörer**] följt av [!UICONTROL **Lägg till administratörer**].

![Fliken Administratör Lägg till administratör markerad](../images/ui/credentials/admins-tab-add-admin.png)

Dialogrutan Lägg till administratör visas. Ange den nya administratörens information i textfälten och välj [!UICONTROL **Spara**].

- Användaren måste sedan läggas till som utvecklare för att en integrering ska kunna skapas. Välj fliken **Utvecklare**, följt av **Lägg till utvecklare**.

![Fliken Utvecklare, knappen Lägg till utvecklare markerad](../images/ui/credentials/developers-tab-add-developer.png)

Dialogrutan Lägg till utvecklare visas. Ange information om den nya utvecklaren i textfälten och välj **Spara**.

Läs dokumentationen om [Åtkomstkontroll](../../access-control/home.md) om du vill veta mer om hur du tilldelar behörigheter.

Alla behörigheter som krävs har nu konfigurerats i Adobe Developer Console så att användaren kan använda funktionen för förfallodatum för inloggningsuppgifter.

Om du vill skapa en uppsättning med autentiseringsuppgifter som inte förfaller väljer du **[!UICONTROL Generate credentials]** på arbetsytan Frågor och autentiseringsuppgifter.

![](../images/ui/credentials/generate-credentials.png)

Genereringen av autentiseringsuppgifter modal visas. Om du vill skapa inloggningsuppgifter som inte förfaller måste du ange följande information:

- **[!UICONTROL Name]**: Namnet på de autentiseringsuppgifter som du genererar.
- **[!UICONTROL Description]**: (Valfritt) En beskrivning av de autentiseringsuppgifter som du genererar.
- **[!UICONTROL Assigned to]**: Användaren som autentiseringsuppgifterna ska tilldelas. Värdet ska vara e-postadressen till den användare som skapar inloggningsuppgifterna.
- **[!UICONTROL Password]** (Valfritt) Ett valfritt lösenord för dina inloggningsuppgifter. Om lösenordet inte är inställt genererar Adobe automatiskt ett lösenord åt dig.

När du har angett all nödvändig information väljer du **[!UICONTROL Generate credentials]** för att generera dina autentiseringsuppgifter.

![](../images/ui/credentials/create-account.png)

>[!IMPORTANT]
>
>När du har valt knappen **[!UICONTROL Generate credentials]** hämtas en JSON-konfigurationsfil till den lokala datorn. Eftersom Adobe **inte** spelar in de genererade autentiseringsuppgifterna måste du **lagra den hämtade filen säkert och spara en inloggningsuppgift.**
>
>Om inloggningsuppgifterna inte används på 90 dagar rensas de också.

JSON-konfigurationsfilen innehåller information som namn på tekniskt konto, ID för tekniskt konto och autentiseringsuppgifter. Den tillhandahålls i följande format.

```json
{"technicalAccountName":"9F0A21EE-B8F3-4165-9871-846D3C8BC49E@TECHACCT.ADOBE.COM","credential":"3d184fa9e0b94f33a7781905c05203ee","technicalAccountId":"4F2611B8613AA3670A495E55"}
```

Nu när du har sparat dina genererade autentiseringsuppgifter väljer du **[!UICONTROL Close]**. Nu kan du se en lista över alla dina ej förfallna autentiseringsuppgifter.

![](../images/ui/credentials/list-credentials.png)

Du kan antingen redigera eller ta bort dina uppgifter som inte förfaller. Om du vill redigera en referens som inte upphör att gälla väljer du pennikonen (![](../images/ui/credentials/edit-icon.png)). Om du vill ta bort en autentiseringsuppgift som inte förfaller väljer du borttagningsikonen (![](../images/ui/credentials/delete-icon.png)).

När du redigerar en referens som inte förfaller visas ett modalt värde. Du kan uppdatera följande information:

- **[!UICONTROL Name]**: Namnet på de autentiseringsuppgifter som du genererar.
- **[!UICONTROL Description]**: (Valfritt) En beskrivning av de autentiseringsuppgifter som du genererar.
- **[!UICONTROL Assigned to]**: Användaren som autentiseringsuppgifterna ska tilldelas. Värdet ska vara e-postadressen till den användare som skapar inloggningsuppgifterna.

![](../images/ui/credentials/update-credentials.png)

När du har angett all nödvändig information väljer du **[!UICONTROL Update account]** för att slutföra uppdateringen av dina autentiseringsuppgifter.

## Använda autentiseringsuppgifter för att ansluta till externa klienter

Du kan använda autentiseringsuppgifterna som förfaller eller inte förfaller för att ansluta till externa klienter, som Aqua Data Studio, Looker eller Power BI.

Tabellen nedan innehåller en lista med parametrar och deras beskrivning, som vanligtvis krävs för att ansluta till externa klienter.

>[!NOTE]
>
>När du ansluter till en värd med autentiseringsuppgifter som inte upphör att gälla, är det fortfarande nödvändigt att använda alla parametrar som listas i [!UICONTROL EXPIRING CREDENTIALS]-avsnittet förutom lösenordet.

| Parameter | Beskrivning |
|---|---|
| **Server/värd** | Namnet på den server/värd som du ansluter till. Värdet har formen `server.adobe.io` och finns under **[!UICONTROL Host]**. |
| **Port** | Porten för den server/värd som du ansluter till. Det här värdet finns under **[!UICONTROL Port]**. Ett exempelvärde för porten skulle vara `80`. |
| **Databas** | Databasen som du ansluter till. Det här värdet finns under **[!UICONTROL Database]**. Ett exempelvärde för databasen skulle vara `prod:all`. |
| **Användarnamn** | Användarnamnet för användaren som ansluter till den externa klienten. Detta tar formen av en alfanumerisk sträng före `@AdobeOrg`. Det här värdet finns under **[!UICONTROL Username]**. |
| **Lösenord** | Lösenordet för den användare som ansluter till den externa klienten. <ul><li>Om du använder inloggningsuppgifter som förfaller finns dessa under **[!UICONTROL Password]** i avsnittet med inloggningsuppgifter som förfaller.</li><li>Om du använder autentiseringsuppgifter som inte upphör att gälla, består det här värdet av argumenten från technicalAccountID och de autentiseringsuppgifter som hämtas från JSON-konfigurationsfilen. Lösenordsvärdet har följande format: `{technicalAccountId}:{credential}`.</li></ul> |

## Nästa steg

Nu när du förstår hur både förfallodatum och icke-utgångsdatum fungerar kan du använda dessa autentiseringsuppgifter för att ansluta till externa klienter. Mer information om externa klienter finns i [Ansluta klienter till frågetjänstguiden](../clients/overview.md).
