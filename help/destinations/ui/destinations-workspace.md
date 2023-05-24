---
keywords: plattform;mål;målarbetsyta;arbetsyta;ui;destinationer ui;katalog;destinationskatalog;
title: Arbetsytan Destinationer
description: 'Arbetsytan Destinationer består av fem avsnitt: Översikt, Katalog, Bläddra, Konton och Systemvy. De beskrivs i avsnitten nedan.'
exl-id: 0f46f08d-0fe3-441d-933a-86bc146c0f19
source-git-commit: 69e1f065cb3b302c4b144f39c84179075379f648
workflow-type: tm+mt
source-wordcount: '1102'
ht-degree: 0%

---

# Arbetsytan Destinationer {#destinations-workspace}

I Adobe Experience Platform väljer du **[!UICONTROL Destinations]** från det vänstra navigeringsfältet för att komma åt [!UICONTROL Destinations] arbetsyta.

The [!UICONTROL Destinations] arbetsytan består av fem avsnitt, [!UICONTROL Overview], [!UICONTROL Catalog], [!UICONTROL Browse], [!UICONTROL Accounts]och [!UICONTROL System View]som beskrivs i avsnitten nedan.

![Målöversiktspanelen med tre widgetar.](../assets/ui/workspace/destinations-overview.png)

## [!UICONTROL Overview] {#overview}

The **[!UICONTROL Overview]** -fliken visar [!UICONTROL Destinations] kontrollpanel, med nyckeltal relaterade till organisationens måldata. Mer information finns på [[!UICONTROL Destinations] instrumentpanelsguide](../../dashboards/guides/destinations.md).

>[!NOTE]
>
>Om din organisation är ny i Experience Platform och ännu inte har några aktiva destinationer är [!UICONTROL Destinations] kontrollpanel och [!UICONTROL Overview] -fliken visas inte. Välj i stället [!UICONTROL Destinations] från vänster navigering visas [[!UICONTROL Catalog] tab](#catalog).

![Fliken Översikt över kontrollpanelen Destinationer.](../../dashboards/images/destinations/dashboard-overview.png)

## [!UICONTROL Catalog] {#catalog}

The **[!UICONTROL Catalog]** -fliken visar en lista över alla destinationer som är tillgängliga i [!DNL Platform]som du kan skicka data till.

The [!DNL Platform] I användargränssnittet finns flera sök- och filteralternativ på målkatalogsidan:

* Använd sökfunktionen på sidan för att hitta ett specifikt mål.
* Filtrera mål med [!UICONTROL Categories] kontroll.
* Växla mellan [!UICONTROL All destinations] och [!UICONTROL My destinations]. När du väljer **[!UICONTROL All destinations]**, alla tillgängliga [!DNL Platform] mål visas. När du väljer **[!UICONTROL My destinations]** kan du bara se de mål som du har upprättat en anslutning till.
* Markera för att visa **[!UICONTROL Connections]** och/eller **[!UICONTROL Extensions]** typer. Om du vill förstå skillnaden mellan de två kategorierna läser du [Måltyper och -kategorier](../destination-types.md).

![Destinationskatalogen med ett fåtal annons- och molnlagringsdestinationer.](../assets/ui/workspace/catalog.png)

Målkorten innehåller alternativ för primär och sekundär kontroll. De primära kontrollerna är [!UICONTROL Set up], [!UICONTROL Activate], [!UICONTROL Activate segments], eller [!UICONTROL Export datasets]. De sekundära kontrollerna tillåter visningsalternativ. Dessa kontroller beskrivs nedan:

| Kontroll | Beskrivning |
|---------|----------|
| [!UICONTROL Set up] | Gör att du kan skapa en anslutning till målet. |
| [!UICONTROL Activate] | När du har upprättat en anslutning till målet kan du aktivera segment eller exportera datauppsättningar till det här målet. |
| [!UICONTROL Activate segments] | När du har upprättat en anslutning till målet kan du aktivera segment till det här målet. |
| [!UICONTROL Export datasets] | När du har upprättat en anslutning till målet kan du exportera datauppsättningar till det här målet. |
| [!UICONTROL View account] | Visa konton som du har anslutit för ett mål. |
| [!UICONTROL View dataflows] | Visa dataaktiveringsflödena som finns för ett mål. |
| [!UICONTROL View documentation] | Öppnar en länk till dokumentationssidan för det specifika målet, för mer information och för att hjälpa dig att konfigurera det. |

{style="table-layout:auto"}

![Kontroll av destinationskortet](../assets/ui/workspace/destination-card-options.png)

Välj ett målkort i katalogen för att öppna den högra listen. Här visas en beskrivning av målet. Högerspåret har samma kontroller som beskrivs i tabellen ovan, inklusive en beskrivning av destinationen och en indikation på destinationskategori och typ.

![Alternativ för målkatalog](../assets/ui/workspace/destination-right-rail.png)

Mer information om målkategorier och information om varje mål finns i [Målkatalog](../catalog/overview.md) och [Måltyper och -kategorier](../destination-types.md).

## [!UICONTROL Accounts] {#accounts}

The **[!UICONTROL Accounts]** På -fliken visas information om anslutningar som du har upprättat med olika destinationer, och där kan du uppdatera eller ta bort befintlig kontoinformation. Se tabellen nedan för all information som du kan få för varje destinationskonto.

>[!TIP]
>
> * Markera ellipsen (`...`) i [!UICONTROL Platform] kolumn och använd ![Aktivera kontroll ](../assets/ui/workspace/add-data-symbol.png)**[!UICONTROL Activate]**/**[!UICONTROL Activate segments]**/**[!UICONTROL Export datasets]**kontroll för att exportera segment eller datauppsättningar till det målet.
> * Markera ellipsen (`...`) i [!UICONTROL Platform] kolumn och använd ![Redigera informationskontroll ](../assets/ui/workspace/pencil-icon.png)**[!UICONTROL Edit details]**styra till [uppdatera](update-accounts.md) Information om ett befintligt destinationskonto.
> * Markera ellipsen (`...`) i [!UICONTROL Platform] kolumn och använd ![Ta bort kontroll ](../assets/ui/workspace/delete-destination-symbol.png)**[!UICONTROL Delete]**styra till [delete](delete-destination-account.md) ett befintligt destinationskonto.


![Fliken Konton](../assets/ui/workspace/destination-account-options.png)

| Element | Beskrivning |
|---|---|
| [!UICONTROL Platform] | Det mål som du har konfigurerat anslutningen för. |
| [!UICONTROL Connection Type] | Representerar kontoanslutningstypen för din lagringsbucket eller destination. Beroende på målet är autentiseringsalternativen: <ul><li>För e-postmarknadsföringsmål: Kan vara S3, FTP eller Azure Blob.</li><li>För reklamdestinationer i realtid: Server-till-server</li><li>För molnlagringsmål för Amazon S3: Åtkomstnyckel </li><li>För SFTP-molnlagringsmål: Grundläggande autentisering för SFTP</li><li>OAuth 1- eller OAuth 2-autentisering</li><li>Autentisering av innehavartoken</li></ul> |
| [!UICONTROL Username] | Användarnamnet som du valde i dialogrutan [guide för anslutningsmål](../catalog/email-marketing/overview.md#connect-destination). |
| [!UICONTROL Destinations] | Representerar antalet unika slutförda måldataflöden som är kopplade till grundläggande information som skapats för ett mål. |
| [!UICONTROL Authorized] | Det datum då anslutningen till det här målet auktoriserades. |

{style="table-layout:auto"}

## [!UICONTROL Browse] {#browse}

The **[!UICONTROL Browse]** -fliken visar de mål som du har upprättat en anslutning till. Destinationer med **[!UICONTROL Enabled/Disabled]** för att växla aktiverat anger målet som aktivt respektive inaktivt. Du kan också visa de mål där data flödar genom att välja **[!UICONTROL Segments]** > **[!UICONTROL Browse]** och välja ett segment som ska inspekteras. Se tabellen nedan för all information som finns för varje mål i [!UICONTROL Browse] tab:

>[!TIP]
>
> * Markera ellipsen (`...`) i [!UICONTROL Name] kolumn och använd ![Aktivera segmentkontroll ](../assets/ui/workspace/add-data-symbol.png)**[!UICONTROL Activate]**kontroll för att exportera segment eller datauppsättningar till det målet.
> * Markera ellipsen (`...`) i [!UICONTROL Name] kolumn och använd ![Ta bort kontroll ](../assets/ui/workspace/delete-destination-symbol.png)**[!UICONTROL Delete]**styra till [ta bort](delete-destinations.md) en befintlig anslutning till ett mål.
> * Markera ellipsen (`...`) i [!UICONTROL Name] kolumn och använd ![Visa i övervakningskontroll ](../assets/ui/workspace/monitoring-icon.png)**[!UICONTROL View in monitoring]**för att visa aktiveringsinformation för destinationen i [kontrollpanel](/help/dataflows/ui/monitor-destinations.md#monitoring-destinations-dashboard).
> * Markera ellipsen (`...`) i [!UICONTROL Name] kolumn och använd ![Prenumerera på aviseringar ](../assets/ui/workspace/alerts-icon.png)**[!UICONTROL Subscribe to alerts]**för att prenumerera på aviseringar om måldataflöde. Du kan prenumerera på aviseringar för att få meddelanden om status, lyckade eller misslyckade flödeskörningar. Se [Prenumerera på aviseringar om destinationer i sitt sammanhang](alerts.md) om du vill ha detaljerad information om aviseringar om måldataflöde.


![Fliken Bläddra](../assets/ui/workspace/browse-tab.png)

| Element | Beskrivning |
|---------|----------|
| Namn | Namnet som du angav för aktiveringsflödet till den här destinationen. Samma kolumn innehåller två kontroller: [!UICONTROL Activate ] och [!UICONTROL Delete destination]. |
| [!UICONTROL Last Flow Run Status] | Status för den senaste dataflödeskörningen. Se [Visa målinformation](destination-details-page.md) för mer information om dataflödeskörningar. |
| [!UICONTROL Last Flow Run Date] | Tid och datum då den senaste dataflödeskörningen inträffade. Se [Visa målinformation](destination-details-page.md) för mer information om dataflödeskörningar. |
| [!UICONTROL Destination] | Målplattformen som du valde för aktiveringsflödet. |
| [!UICONTROL Connection Type] | Representerar anslutningstypen för din lagringsbucket eller destination. <ul><li>För e-postmarknadsföringsmål: Kan vara S3, FTP eller [!DNL Azure Blob].</li><li>För reklamdestinationer i realtid: Server-till-server.</li><li>För direktuppspelningsmål: Kan [!DNL Azure Event Hubs] eller [!DNL Amazon Kinesis].</li></ul> |
| [!UICONTROL Username] | De kontoautentiseringsuppgifter som du har valt för målflödet. |
| [!UICONTROL Activation Data] | Anger antalet segment som aktiveras till det här målet. Välj den här kontrollen om du vill veta mer om de aktiverade segmenten. Se [Aktiveringsdata](/help/destinations/ui/destination-details-page.md#activation-data) på sidan med målinformation om du vill ha mer information om de aktiverade segmenten. |
| [!UICONTROL Created] | Datum och UTC-tid när aktiveringsflödet till målet skapades. Välj uppåt-/nedåtpilen för att sortera aktiveringsflödena efter det senaste först eller det äldsta först. |
| [!UICONTROL Status] | `Enabled` eller `Disabled`. Anger om data aktiveras till det här målet. |

Klicka på en målrad för att visa mer information om målet i den högra listen.

![Klicka på målraden](../assets/ui/workspace/click-destination-row.png)

Markera målnamnet om du vill visa information om de segment som har aktiverats för det här målet. Klicka **[!UICONTROL Edit activation]** om du vill ändra eller lägga till i de segment som skickas till det här målet.

## [!UICONTROL System View] {#system-view}

The **[!UICONTROL System View]** I visas en grafisk representation av de aktiveringsflöden som du har konfigurerat i Adobe Experience Platform.

![Data-flows1](../assets/ui/workspace/data-flows1.png)

Välj något av de mål som visas på sidan och klicka på **[!UICONTROL View dataflows]** om du vill visa information om alla anslutningar som du har konfigurerat för varje mål.

![Data-flows2](../assets/ui/workspace/data-flows2.png)
