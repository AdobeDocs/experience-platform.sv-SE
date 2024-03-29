---
keywords: Experience Platform;home;populära topics;query service;Query service;query editor;Query Editor;Query editor;Query editor;
solution: Experience Platform
title: Handbok för autentiseringsuppgifter för frågetjänst
description: Adobe Experience Platform Query Service har ett användargränssnitt som kan användas för att skriva och köra frågor, visa frågor som har körts tidigare samt få åtkomst till frågor som har sparats av användare i organisationen.
exl-id: ea25fa32-809c-429c-b855-fcee5ee31b3e
source-git-commit: 74e3dc2fa5fc84b5ce4b09e2adb0093ecb94bd82
workflow-type: tm+mt
source-wordcount: '1457'
ht-degree: 0%

---

# Handbok för autentiseringsuppgifter

Med Adobe Experience Platform Query Service kan du ansluta till externa klienter. Du kan ansluta till dessa externa klienter genom att använda antingen utgångsdatum eller ej utgångsdatum.

>[!NOTE]
>
>Autentiseringspanelen är inte automatiskt tillgänglig för alla användare. Kontakta ditt Adobe-kontoteam för att be om [!UICONTROL Credentials] som ska inkluderas i arbetsytan för frågetjänsten om du behöver det. Om så krävs är denna förändring i hela organisationen och genomförs av Adobe ingenjörsteam. Det är inte en inställning som styrs av användare.

## Utgående autentiseringsuppgifter {#expiring-credentials}

>[!CONTEXTUALHELP]
>id="platform_queryservice_credentials_expiringcredentials"
>title="Klientens SSL-läge"
>abstract="SSL måste vara aktiverat i klienter som är anslutna till Query Service. Kontrollera att SSL-läget är inställt på &quot;require&quot;."

Du kan använda utgångsuppgifter för att snabbt konfigurera en anslutning till en extern klient.

![Fliken Autentiseringsuppgifter för kontrollpanelen Frågor med avsnittet Utgångsuppgifter markerat.](../images/ui/credentials/expiring-credentials.png)

The **[!UICONTROL Expiring credentials]** innehåller följande information:

- **[!UICONTROL Host]**: Namnet på den värd som klienten ska anslutas till. Det innehåller namnet på din organisation så som det visas på den översta menyfliken i användargränssnittet för plattformen.
- **[!UICONTROL Port]**: Portnumret för den värd som ska anslutas till.
- **[!UICONTROL Database]**: Namnet på den databas som en klient ska anslutas till.
- **[!UICONTROL Username]**: Det användarnamn som används för att ansluta till frågetjänsten.
- **[!UICONTROL Password]**: Lösenordet som används för att ansluta till frågetjänsten. Lösenord i användargränssnittet har hashats av säkerhetsskäl. Markera kopieringsikonen (![Kopieringsikonen.](../images/ui/credentials/copy-icon.png)) om du vill kopiera kompletta, ohashad inloggningsuppgifter till Urklipp.
- **[!UICONTROL PSQL command]**: Ett kommando som automatiskt har infogat all relevant information så att du kan ansluta till frågetjänsten med PSQL på kommandoraden.
- **[!UICONTROL Expires]**: Giltighetsdatum och -tid för förfalloinformationen. Standardlängden för token är 24 timmar, men den kan ändras i de avancerade inställningarna för Admin Console.

>[!TIP]
>
>Om du vill ändra sessionstiden för dina utgående inloggningsuppgifter som är kopplade till frågetjänsten går du till [Admin Console](https://adminconsole.adobe.com/) och välj följande på skärmen: **Inställningar** > **Integritet och säkerhet** > **Autentiseringsinställningar** > **Avancerade inställningar** > **Maximal sessionstid**.
>
>![Inställningsfliken på Admin Console med sekretess och säkerhet, autentiseringsinställningar och maximal sessionstid markerade.](../images/ui/credentials/max-session-life.png)
>
>Mer information om Adobe finns i hjälpdokumentationen [Avancerade inställningar](https://helpx.adobe.com/enterprise/using/authentication-settings.html#advanced-settings) som finns i Admin Console.

## Ej förfallande autentiseringsuppgifter {#non-expiring-credentials}

Du kan använda autentiseringsuppgifter som inte upphör att gälla för att konfigurera en mer permanent anslutning till en extern klient.

>[!NOTE]
>
>Giltiga autentiseringsuppgifter har följande begränsningar:<br><ul><li>Användarna måste logga in med sitt användarnamn och lösenord som består av `{technicalAccountId}:{credential}`. Mer information finns i [Generera autentiseringsuppgifter](#generate-credentials) -avsnitt.</li><li>När inloggningsuppgifterna skapas skapas en ny roll med en uppsättning grundläggande behörigheter som gör att användare kan visa scheman och datauppsättningar. Behörigheten för att hantera frågor har även tilldelats den här rollen för användning med frågetjänsten.</li><li>Tredjepartsklienter kan fungera annorlunda än väntat när frågeobjekt listas. Vissa tredjepartsklienter, som [!DNL DB Visualizer] I visas inte vynamnet i den vänstra panelen. Visningsnamnet är dock tillgängligt om det anropas i en SELECT-fråga. På samma sätt [!DNL PowerUI] kanske inte visar de temporära vyer som har skapats via SQL som ska väljas för att skapa instrumentpaneler.</li></ul>

### Förutsättningar

Innan du kan generera autentiseringsuppgifter som inte förfaller måste du utföra följande steg i Adobe Admin Console:

1. Logga in [Adobe Admin Console](https://adminconsole.adobe.com/) och välj relevant organisation i det övre navigeringsfältet.
2. [Välj en produktprofil.](../../access-control/ui/browse.md)
3. [Konfigurera båda **Sandlådor** och **Hantera integrering av frågetjänster** behörigheter](../../access-control/ui/permissions.md) för produktprofilen.
4. [Lägga till en ny användare i en produktprofil](../../access-control/ui/users.md) så att de får sina konfigurerade behörigheter.
5. [Lägg till användaren som produktprofiladministratör](https://helpx.adobe.com/enterprise/using/manage-product-profiles.html) för att tillåta att konton skapas för alla aktiva produktprofiler.
6. [Lägg till användaren som produktprofilutvecklare](https://helpx.adobe.com/se/enterprise/using/manage-developers.html) för att skapa en integrering.

Läs dokumentationen om hur du tilldelar behörigheter [åtkomstkontroll](../../access-control/home.md).

Alla behörigheter som krävs har nu konfigurerats i Adobe Developer Console så att användaren kan använda funktionen för förfalloinloggningsuppgifter.

### Generera autentiseringsuppgifter {#generate-credentials}

Om du vill skapa en uppsättning med autentiseringsuppgifter som inte upphör att gälla går du tillbaka till användargränssnittet för plattformen och väljer **[!UICONTROL Queries]** från vänster navigering för att komma åt [!UICONTROL Queries] arbetsyta. Nästa steg är att välja **[!UICONTROL Credentials]** följt av **[!UICONTROL Generate credentials]**.

![Kontrollpanelen Frågor med fliken Autentiseringsuppgifter och Generera autentiseringsuppgifter markerade.](../images/ui/credentials/generate-credentials.png)

En dialogruta visas där du kan generera autentiseringsuppgifter. Om du vill skapa inloggningsuppgifter som inte förfaller måste du ange följande information:

- **[!UICONTROL Name]**: Namnet på de autentiseringsuppgifter som du genererar.
- **[!UICONTROL Description]**: (Valfritt) En beskrivning av de autentiseringsuppgifter som du genererar.
- **[!UICONTROL Assigned to]**: Den användare som autentiseringsuppgifterna ska tilldelas till. Värdet ska vara e-postadressen till den användare som skapar inloggningsuppgifterna.
- **[!UICONTROL Password]** (Valfritt) Ett valfritt lösenord för dina inloggningsuppgifter. Om lösenordet inte är inställt genererar Adobe automatiskt ett lösenord åt dig.

När du har angett all nödvändig information väljer du **[!UICONTROL Generate credentials]** för att generera dina autentiseringsuppgifter.

![Dialogrutan Generera inloggningsuppgifter är markerad.](../images/ui/credentials/create-account.png)

>[!IMPORTANT]
>
>När **[!UICONTROL Generate credentials]** väljs hämtas en konfigurations-JSON-fil till den lokala datorn. Eftersom Adobe gör **not** spela in de genererade inloggningsuppgifterna, måste du lagra den hämtade filen på ett säkert sätt och spara en inloggningsuppgift.
>
>Om inloggningsuppgifterna inte används på 90 dagar kommer de dessutom att tas bort.

JSON-konfigurationsfilen innehåller information som namn på tekniskt konto, ID för tekniskt konto och autentiseringsuppgifter. Den tillhandahålls i följande format.

```json
{"technicalAccountName":"9F0A21EE-B8F3-4165-9871-846D3C8BC49E@TECHACCT.ADOBE.COM","credential":"3d184fa9e0b94f33a7781905c05203ee","technicalAccountId":"4F2611B8613AA3670A495E55"}
```

När du har sparat dina genererade inloggningsuppgifter väljer du **[!UICONTROL Close]**. Nu kan du se en lista över alla dina ej förfallna autentiseringsuppgifter.

![Fliken Autentiseringsuppgifter för kontrollpanelen Frågor med avsnittet Ej förfallande autentiseringsuppgifter markerat.](../images/ui/credentials/list-credentials.png)

Du kan antingen redigera eller ta bort dina uppgifter som inte förfaller. Om du vill redigera en referens som inte förfaller väljer du pennikonen (![En pennikon.](../images/ui/credentials/edit-icon.png)). Om du vill ta bort en autentiseringsuppgift som inte upphör att gälla väljer du ikonen Ta bort (![En papperskorgsikon.](../images/ui/credentials/delete-icon.png)).

När du redigerar en referens som inte upphör att gälla visas ett modalt värde. Du kan uppdatera följande information:

- **[!UICONTROL Name]**: Namnet på de autentiseringsuppgifter som du genererar.
- **[!UICONTROL Description]**: (Valfritt) En beskrivning av de autentiseringsuppgifter som du genererar.
- **[!UICONTROL Assigned to]**: Den användare som autentiseringsuppgifterna ska tilldelas till. Värdet ska vara e-postadressen till den användare som skapar inloggningsuppgifterna.

![Dialogrutan Uppdatera konto.](../images/ui/credentials/update-credentials.png)

När du har angett all nödvändig information väljer du **[!UICONTROL Update account]** för att slutföra uppdateringen av dina autentiseringsuppgifter.

## Använd autentiseringsuppgifter för att ansluta till externa klienter {#use-credential-to-connect}

Du kan använda autentiseringsuppgifterna som förfaller eller inte förfaller för att ansluta till externa klienter, som Aqua Data Studio, Looker eller Power BI. Indatametoden för dessa autentiseringsuppgifter varierar beroende på den externa klienten. Mer information om hur du använder dessa autentiseringsuppgifter finns i den externa klientens dokumentation.

Bilden anger platsen för varje parameter som hittas i användargränssnittet, med undantag för lösenordet för de autentiseringsuppgifter som inte förfaller. Även om inloggningsuppgifterna som inte förfaller anges i JSON-konfigurationsfilerna kan du visa dina förfallande inloggningsuppgifter under **Referenser** i användargränssnittet.

![Fliken Autentiseringsuppgifter för arbetsytan Frågor med avsnittet Utgångsuppgifter markerat.](../images/ui/credentials/expiring-credentials.png)

Tabellen nedan visar de parametrar som vanligtvis krävs för att ansluta till externa klienter.

>[!NOTE]
>
>När du ansluter till en värd med autentiseringsuppgifter som inte upphör att gälla, är det fortfarande nödvändigt att använda alla parametrar som anges i [!UICONTROL EXPIRING CREDENTIALS] utom för lösenordet och användarnamnet.
>Formatet för att ange ditt användarnamn och lösenord använder kolonavgränsade värden som visas i det här exemplet `username:{your_username}` och `password:{password_string}`.

| Parameter | Beskrivning | Exempel |
|---|---|---|
| **Server/värd** | Namnet på den server/värd som du ansluter till. <ul><li>Det här värdet används både för utgångsdatum och icke-utgångsdatum och har formen av `server.adobe.io`. Värdet finns under **[!UICONTROL Host]** i [!UICONTROL EXPIRING CREDENTIALS] -avsnitt.</ul></li> | `acme.platform.adobe.io` |
| **Port** | Porten för den server/värd som du ansluter till. <ul><li>Det här värdet används både för utgångsdatum och icke-utgångsdatum och finns under **[!UICONTROL Port]** i [!UICONTROL EXPIRING CREDENTIALS] -avsnitt.</ul></li> | `80` |
| **Databas** | Databasen som du ansluter till. <ul><li>Det här värdet används både för utgångsdatum och icke-utgångsdatum för inloggningsuppgifter och finns under **[!UICONTROL Database]** i [!UICONTROL EXPIRING CREDENTIALS] -avsnitt. </ul></li> | `prod:all` |
| **Användarnamn** | Användarnamnet för användaren som ansluter till den externa klienten. <ul><li>Det här värdet används både för utgångsdatum och icke-utgångsdatum. Det tar formen av en alfanumerisk sträng före `@AdobeOrg`. Det här värdet finns under **[!UICONTROL Username]**.</li></ul> | `ECBB80245ECFC73E8A095EC9@AdobeOrg` |
| **Lösenord** | Lösenordet för den användare som ansluter till den externa klienten. <ul><li>Om du använder inloggningsuppgifter som förfaller finns dessa under **[!UICONTROL Password]** inom [!UICONTROL EXPIRING CREDENTIALS] -avsnitt.</li><li>Om du använder inloggningsuppgifter som inte upphör att gälla är det här värdet de sammanfogade argumenten från technicalAccountID och inloggningsuppgifterna från JSON-konfigurationsfilen. Lösenordsvärdet har följande format: `{technicalAccountId}:{credential}`.</li></ul> | <ul><li>Ett lösenord för att ange förfallodatum är längre än tusen alfanumeriska tecken. Inget exempel kommer att ges.</li><li>Ett lösenord som inte förfaller är följande:<br>`4F2611B8613DK3670V495N55:3d182fa9e0b54f33a7881305c06203ee`</li></ul> |

{style="table-layout:auto"}

## Nästa steg

Nu när du förstår hur både förfallodatum och icke-utgångsdatum fungerar kan du använda dessa autentiseringsuppgifter för att ansluta till externa klienter. Mer information om externa klienter finns i [ansluta klienter till frågetjänstguiden](../clients/overview.md).
