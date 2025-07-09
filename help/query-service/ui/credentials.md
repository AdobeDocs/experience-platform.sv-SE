---
keywords: Experience Platform;home;populära topics;query service;Query service;query editor;Query Editor;Query editor;
solution: Experience Platform
title: Handbok för autentiseringsuppgifter för frågetjänst
description: Adobe Experience Platform Query Service har ett användargränssnitt som kan användas för att skriva och köra frågor, visa frågor som har körts tidigare samt få åtkomst till frågor som har sparats av användare i organisationen.
exl-id: ea25fa32-809c-429c-b855-fcee5ee31b3e
source-git-commit: 60b9fd250ba1a3e2da374681b78f0375f75dc87e
workflow-type: tm+mt
source-wordcount: '1911'
ht-degree: 0%

---

# Handbok för autentiseringsuppgifter

Med Adobe Experience Platform Query Service kan du ansluta till externa klienter. Du kan ansluta till dessa externa klienter genom att använda antingen utgångsdatum eller ej utgångsdatum.

>[!NOTE]
>
>Autentiseringspanelen är inte automatiskt tillgänglig för alla användare. Kontakta ditt Adobe-kontoteam för att begära att fliken [!UICONTROL Credentials] ska ingå i arbetsytan för frågetjänsten om du behöver det. Om det efterfrågas sker ändringen i hela organisationen och genomförs av Adobe tekniker. Det är inte en inställning som styrs av användare.

## Utgående autentiseringsuppgifter {#expiring-credentials}

>[!CONTEXTUALHELP]
>id="platform_queryservice_credentials_expiringcredentials"
>title="Klientens SSL-läge"
>abstract="SSL måste vara aktiverat i klienter som är anslutna till Query Service. Kontrollera att SSL-läget är inställt på &quot;require&quot;."

Du kan använda utgångsuppgifter för att snabbt konfigurera en anslutning till en extern klient.

![Fliken Autentiseringsuppgifter för kontrollpanelen Frågor med avsnittet Utgående autentiseringsuppgifter markerat.](../images/ui/credentials/expiring-credentials.png)

Avsnittet **[!UICONTROL Expiring credentials]** innehåller följande information:

- **[!UICONTROL Host]**: Namnet på värddatorn som klienten ska anslutas till. Det innehåller namnet på din organisation så som det visas på den övre menyfliken i Experience Platform användargränssnitt.
- **[!UICONTROL Port]**: Portnumret för den värd som ska anslutas.
- **[!UICONTROL Database]**: Namnet på databasen som en klient ska anslutas till.
- **[!UICONTROL Username]**: Användarnamnet som används för att ansluta till frågetjänsten.
- **[!UICONTROL Password]**: Lösenordet som används för att ansluta till frågetjänsten. Lösenord i användargränssnittet har hashats av säkerhetsskäl. Välj kopieringsikonen (![Kopieringsikonen.](/help/images/icons/copy.png)) om du vill kopiera dina fullständiga, ohashade autentiseringsuppgifter till Urklipp.
- **[!UICONTROL PSQL command]**: Ett kommando som automatiskt har infogat all relevant information så att du kan ansluta till frågetjänsten med PSQL på kommandoraden.
- **[!UICONTROL Expires]**: Utgångsdatum och förfallotid för autentiseringsuppgifterna. Standardlängden för token är 24 timmar, men den kan ändras i de avancerade inställningarna för Admin Console.

>[!TIP]
>
>Om du vill ändra sessionstiden för din utgående inloggningsanslutning till frågetjänsten går du till [Admin Console](https://adminconsole.adobe.com/) och väljer följande på skärmen: **Inställningar** > **Sekretess och säkerhet** > **Autentiseringsinställningar** > **Avancerade inställningar** > **Maximal sessionstid**.
>
>![Fliken Admin Console-inställningar med sekretess och säkerhet, autentiseringsinställningar och maximal sessionstid markerade.](../images/ui/credentials/max-session-life.png)
>
>Mer information om de [avancerade inställningarna](https://helpx.adobe.com/se/enterprise/using/authentication-settings.html#advanced-settings) som Admin Console erbjuder finns i hjälpdokumentationen för Adobe.

### Ansluta Customer Journey Analytics-data i frågesessioner {#connect-to-customer-journey-analytics}

Använd Customer Journey Analytics BI-tillägget med Power BI eller Tableau för att komma åt dina [datavyer](https://experienceleague.adobe.com/sv/docs/analytics-platform/using/cja-dataviews/data-views) från Customer Journey Analytics med SQL. Genom att integrera frågetjänsten med BI-tillägget kan du komma åt dina datavyer direkt i sessioner med frågetjänsten. Den här integreringen effektiviserar funktionaliteten för BI-verktyg som använder Query Service som PostgreSQL-gränssnitt. Den här funktionen eliminerar behovet av att duplicera datavyer i BI-verktyg, säkerställer enhetlig rapportering på olika plattformar och förenklar integreringen av Customer Journey Analytics-data med andra källor i BI-plattformar.

Läs dokumentationen för att lära dig hur du [ansluter frågetjänsten till ett antal klientprogram för stationära datorer](../clients/overview.md), till exempel [Power BI](../clients/power-bi.md) eller [Tableau](../clients/tableau.md)

>[!IMPORTANT]
>
>Det krävs ett Customer Journey Analytics-arbetsyteprojekt och en datavy för att den här funktionen ska kunna användas.

Om du vill få tillgång till dina Customer Journey Analytics-data i antingen Power BI eller Tablet PC väljer du listrutan [!UICONTROL Database] och sedan `prod:cja` bland de tillgängliga alternativen. Kopiera sedan dina [!DNL Postgres]-autentiseringsparametrar (värd, port, databas, användarnamn med flera) för användning i din Power BI- eller Tableau-konfiguration.

![Fliken med autentiseringsuppgifter för frågetjänsten med listrutan för databas markerad.](../images/ui/credentials/database-dropdown.png)

>[!NOTE]
>
>När du ansluter Power BI eller Tableau till Customer Journey Analytics förbrukas behörigheten för frågetjänsten &#39;concurrent sessions&#39;. Om ytterligare sessioner och frågor krävs kan ytterligare ett tillägg för ad hoc-frågeanvändarpaket köpas för att erhålla ytterligare fem samtidiga sessioner och ytterligare en samtidiga fråga.

Du kan även komma åt dina Customer Journey Analytics-data direkt från Frågeredigeraren eller Postgres CLI. Om du vill göra det refererar du till databasen `cja` när du skriver din fråga. Mer information om hur du skriver, kör och sparar frågor finns i frågeredigeraren [frågeredigeringsguiden](./user-guide.md#query-authoring).

I [BI-tilläggsguiden](https://experienceleague.adobe.com/sv/docs/analytics-platform/using/cja-dataviews/bi-extension) finns fullständiga anvisningar om hur du får åtkomst till dina Customer Journey Analytics-datavyer med SQL.

## Ej förfallande autentiseringsuppgifter {#non-expiring-credentials}

>[!CONTEXTUALHELP]
>id="platform_queryservice_credentials_migratenonexpiringcredentials"
>title="Migrera till autentiseringsuppgifter för OAuth Server-till-server"
>abstract="Migreringen krävs eftersom JWT-autentiseringsuppgifterna slutar att fungera efter 30 juni 2025. Det tar cirka 30-40 sekunder och kan inte avbrytas när programmet har startats. Alla befintliga jobb och integreringar fortsätter att fungera med OAuth efter migrering. Du kan lämna den här skärmen och returnera när som helst för att kontrollera statusen."

Du kan använda autentiseringsuppgifter som inte upphör att gälla för att konfigurera en mer permanent anslutning till en extern klient.

>[!NOTE]
>
>Giltiga autentiseringsuppgifter har följande begränsningar:
>
>- Användare måste logga in med sitt användarnamn och lösenord i formatet `{technicalAccountId}:{credential}`. Mer information finns i avsnittet [Generera autentiseringsuppgifter](#generate-credentials).
>- Som standard ges autentiseringsuppgifter som inte förfaller behörighet att endast köra `SELECT`-frågor. Om du vill köra `CTAS`- eller `ITAS`-frågor lägger du manuellt till behörigheterna Hantera datauppsättning och Hantera scheman i rollen som är kopplad till de autentiseringsuppgifter som inte förfaller. Behörigheten Hantera scheman finns under avsnittet Datamodellering och behörigheten Hantera datauppsättningar finns under avsnittet Datahantering i [Adobe Developer Console](<https://developer.adobe.com/console/>).
>- Tredjepartsklienter kan fungera annorlunda än väntat när frågeobjekt listas. Vissa tredjepartsklienter, till exempel [!DNL DB Visualizer], visar inte vynamnet på den vänstra panelen. Visningsnamnet är dock tillgängligt om det anropas i en `SELECT`-fråga. På samma sätt kanske [!DNL PowerUI] inte listar de tillfälliga vyer som har skapats via SQL för val när kontrollpaneler skapas.

### Förhandskrav

Innan du kan generera autentiseringsuppgifter som inte förfaller måste du utföra följande steg i Adobe Admin Console:

1. Logga in på [Adobe Admin Console](https://adminconsole.adobe.com/) och välj relevant organisation i det övre navigeringsfältet.
2. [Välj en produktprofil.](../../access-control/ui/browse.md)
3. [Konfigurera både **sandlådor** och **Hantera frågetjänstintegration** ](../../access-control/ui/permissions.md) för produktprofilen.
4. [Lägg till en ny användare i en produktprofil](../../access-control/ui/users.md) så att de får sina konfigurerade behörigheter.
5. [Lägg till användaren som produktprofiladministratör](https://helpx.adobe.com/se/enterprise/using/manage-product-profiles.html) om du vill tillåta att ett konto skapas för en aktiv produktprofil.
6. [Lägg till användaren som produktprofilutvecklare](https://helpx.adobe.com/se/enterprise/using/manage-developers.html) för att skapa en integrering.

Efter dessa steg konfigureras de nödvändiga behörigheterna i [Adobe Developer Console](https://developer.adobe.com/console/) så att du kan generera autentiseringsuppgifter för OAuth Server-till-Server och använda funktionerna för förfallande eller ej förfallande autentiseringsuppgifter.

Mer information om att tilldela behörigheter finns i [åtkomstkontrollsdokumentationen](../../access-control/home.md).

### Generera autentiseringsuppgifter {#generate-credentials}

Om du vill skapa en uppsättning med autentiseringsuppgifter som inte upphör att gälla går du tillbaka till användargränssnittet i Experience Platform och väljer **[!UICONTROL Queries]** i den vänstra navigeringen för att komma åt arbetsytan i [!UICONTROL Queries]. Välj sedan fliken **[!UICONTROL Credentials]** följt av **[!UICONTROL Generate credentials]**.

![Kontrollpanelen Frågor med fliken Autentiseringsuppgifter och Generera autentiseringsuppgifter markerade.](../images/ui/credentials/generate-credentials.png)

En dialogruta visas där du kan generera autentiseringsuppgifter. Om du vill skapa inloggningsuppgifter som inte förfaller måste du ange följande information:

- **[!UICONTROL Name]**: Namnet på de autentiseringsuppgifter som du genererar.
- **[!UICONTROL Description]**: (Valfritt) En beskrivning av de autentiseringsuppgifter som du genererar.
- **[!UICONTROL Assigned to]**: Den användare som autentiseringsuppgifterna ska tilldelas till. Värdet ska vara e-postadressen till den användare som skapar inloggningsuppgifterna.
- **[!UICONTROL Password]** (Valfritt) Ett valfritt lösenord för dina autentiseringsuppgifter. Om lösenordet inte är inställt genererar Adobe automatiskt ett lösenord åt dig.

När du har angett all nödvändig information väljer du **[!UICONTROL Generate credentials]** för att generera dina autentiseringsuppgifter.

![Dialogrutan Generera autentiseringsuppgifter är markerad.](../images/ui/credentials/create-account.png)

>[!IMPORTANT]
>
>När **[!UICONTROL Generate credentials]** har valts hämtas en konfigurations-JSON-fil till den lokala datorn. Eftersom Adobe **inte** spelar in de genererade inloggningsuppgifterna måste du lagra den hämtade filen på ett säkert sätt och registrera inloggningsuppgifterna.
>
>Om inloggningsuppgifterna inte används på 90 dagar kommer de dessutom att tas bort.

JSON-konfigurationsfilen innehåller information som namn på tekniskt konto, ID för tekniskt konto och autentiseringsuppgifter. Den tillhandahålls i följande format.

```json
{"technicalAccountName":"9F0A21EE-B8F3-4165-9871-846D3C8BC49E@TECHACCT.ADOBE.COM","credential":"3d184fa9e0b94f33a7781905c05203ee","technicalAccountId":"4F2611B8613AA3670A495E55"}
```

När du har sparat dina genererade autentiseringsuppgifter väljer du **[!UICONTROL Close]**. Nu kan du se en lista över alla dina ej förfallna autentiseringsuppgifter.

![Fliken Autentiseringsuppgifter för kontrollpanelen Frågor med avsnittet Ej förfallande autentiseringsuppgifter markerat.](../images/ui/credentials/list-credentials.png)

Du kan antingen redigera eller ta bort dina uppgifter som inte förfaller. Om du vill redigera en referens som inte upphör att gälla väljer du pennikonen (![En pennikon.](/help/images/icons/edit.png)). Om du vill ta bort en autentiseringsuppgift som inte upphör att gälla väljer du borttagningsikonen (![En papperskorgsikon.](/help/images/icons/delete.png)).

När du redigerar en referens som inte upphör att gälla visas ett modalt värde. Du kan uppdatera följande information:

- **[!UICONTROL Name]**: Namnet på de autentiseringsuppgifter som du genererar.
- **[!UICONTROL Description]**: (Valfritt) En beskrivning av de autentiseringsuppgifter som du genererar.
- **[!UICONTROL Assigned to]**: Den användare som autentiseringsuppgifterna ska tilldelas till. Värdet ska vara e-postadressen till den användare som skapar inloggningsuppgifterna.

![Dialogrutan Uppdatera konto.](../images/ui/credentials/update-credentials.png)

När du har angett all nödvändig information väljer du **[!UICONTROL Update account]** för att slutföra uppdateringen av dina autentiseringsuppgifter.

### Migrera autentiseringsuppgifter till OAuth {#migrate-credentials}

Om du använder JWT-autentiseringsuppgifter som inte upphör att gälla måste du migrera var och en till OAuth Server-till-Server före 30 juni 2025 för att undvika avbrott i tjänsten.

>[!IMPORTANT]
>
>JWT-inloggningsuppgifterna slutar att fungera efter 30 juni 2025. Du måste slutföra migreringen manuellt för att behålla auktoriseringen.

Mer information om hur du identifierar påverkade autentiseringsuppgifter och slutför migreringen finns i handboken [Migrate from JWT to OAuth Server-to-Server credentials](./migrate-jwt-to-oauth.md).

Vanliga frågor finns i [Vanliga frågor om migrering](./migrate-jwt-to-oauth.md#faq).

## Använd autentiseringsuppgifter för att ansluta till externa klienter {#use-credential-to-connect}

Du kan använda autentiseringsuppgifterna som förfaller eller inte förfaller för att ansluta till externa klienter, som Aqua Data Studio, Looker eller Power BI. Indatametoden för dessa autentiseringsuppgifter varierar beroende på den externa klienten. Mer information om hur du använder dessa autentiseringsuppgifter finns i den externa klientens dokumentation.

Bilden anger platsen för varje parameter som hittas i användargränssnittet, med undantag för lösenordet för de autentiseringsuppgifter som inte förfaller. Även om autentiseringsuppgifter som inte förfaller anges av deras JSON-konfigurationsfiler, kan du visa dina förfallande autentiseringsuppgifter på fliken **Autentiseringsuppgifter** i användargränssnittet.

![Fliken Autentiseringsuppgifter för arbetsytan Frågor med avsnittet Förfallande autentiseringsuppgifter markerat.](../images/ui/credentials/expiring-credentials.png)

Tabellen nedan visar de parametrar som vanligtvis krävs för att ansluta till externa klienter.

>[!NOTE]
>
>När du ansluter till en värd med autentiseringsuppgifter som inte upphör att gälla, är det fortfarande nödvändigt att använda alla parametrar som anges i avsnittet [!UICONTROL EXPIRING CREDENTIALS] förutom lösenordet och användarnamnet.
>&#x200B;>Formatet för att ange ditt användarnamn och lösenord använder kolonavgränsade värden som visas i det här exemplet `username:{your_username}` och `password:{password_string}`.

| Parameter | Beskrivning | Exempel |
|---|---|---|
| **Server/värd** | Namnet på den server/värd som du ansluter till. <ul><li>Det här värdet används både för utgångsdatum och icke-utgångsdatum och har formen `server.adobe.io`. Värdet finns under **[!UICONTROL Host]** i avsnittet [!UICONTROL EXPIRING CREDENTIALS].</ul></li> | `acme.platform.adobe.io` |
| **Port** | Porten för den server/värd som du ansluter till. <ul><li>Det här värdet används både för förfallodatum och icke-förfallande autentiseringsuppgifter och finns under **[!UICONTROL Port]** i avsnittet [!UICONTROL EXPIRING CREDENTIALS].</ul></li> | `80` |
| **Databas** | Databasen som du ansluter till. <ul><li>Det här värdet används både för förfallodatum och icke-förfallande autentiseringsuppgifter och finns under **[!UICONTROL Database]** i avsnittet [!UICONTROL EXPIRING CREDENTIALS]. </ul></li> | `prod:all` |
| **Användarnamn** | Användarnamnet för användaren som ansluter till den externa klienten. <ul><li>Det här värdet används både för utgångsdatum och icke-utgångsdatum. Det har formen av en alfanumerisk sträng före `@AdobeOrg`. Det här värdet finns under **[!UICONTROL Username]**.</li></ul> | `ECBB80245ECFC73E8A095EC9@AdobeOrg` |
| **Lösenord** | Lösenordet för den användare som ansluter till den externa klienten. <ul><li>Om du använder förfalloinloggningsuppgifter finns dessa under **[!UICONTROL Password]** i avsnittet [!UICONTROL EXPIRING CREDENTIALS].</li><li>Om du använder inloggningsuppgifter som inte upphör att gälla är det här värdet de sammanfogade argumenten från technicalAccountID och inloggningsuppgifterna från JSON-konfigurationsfilen. Lösenordsvärdet har formatet: `{technicalAccountId}:{credential}`.</li></ul> | <ul><li>Ett lösenord för att ange förfallodatum är längre än tusen alfanumeriska tecken. Inget exempel kommer att ges.</li><li>Ett lösenord för autentiseringsuppgifter som inte förfaller är följande:<br>`4F2611B8613DK3670V495N55:3d182fa9e0b54f33a7881305c06203ee`</li></ul> |

{style="table-layout:auto"}

## Nästa steg

Nu när du förstår hur både förfallodatum och icke-utgångsdatum fungerar kan du använda dessa autentiseringsuppgifter för att ansluta till externa klienter. Mer information om externa klienter finns i guiden [Ansluta klienter till frågetjänsten](../clients/overview.md).
