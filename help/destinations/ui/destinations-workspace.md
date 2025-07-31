---
keywords: plattform;mål;målarbetsyta;arbetsyta;ui;destinationer ui;katalog;destinationskatalog;
title: Arbetsytan Destinationer
description: 'Arbetsytan Destinationer består av fem avsnitt: Översikt, Katalog, Bläddra, Konton och Systemvy. De beskrivs i avsnitten nedan.'
exl-id: 0f46f08d-0fe3-441d-933a-86bc146c0f19
source-git-commit: 80ceb279e943037fb4507419b7818575b4a84fe5
workflow-type: tm+mt
source-wordcount: '1251'
ht-degree: 0%

---

# Arbetsytan Destinationer {#destinations-workspace}

I Adobe Experience Platform väljer du **[!UICONTROL Destinations]** i det vänstra navigeringsfältet för att komma åt arbetsytan i [!UICONTROL Destinations].

Arbetsytan [!UICONTROL Destinations] består av fem avsnitt, [!UICONTROL Overview], [!UICONTROL Catalog], [!UICONTROL Browse], [!UICONTROL Accounts] och [!UICONTROL System View], som beskrivs i avsnitten nedan.

![Målöversiktspanelen med tre widgetar.](../assets/ui/workspace/destinations-overview.png)

## [!UICONTROL Overview] {#overview}

Fliken **[!UICONTROL Overview]** visar kontrollpanelen [!UICONTROL Destinations] med nyckelmått för organisationens måldata. Mer information finns i [[!UICONTROL Destinations]-handboken för instrumentpanelen ](../../dashboards/guides/destinations.md).

>[!NOTE]
>
>Om din organisation är ny för Experience Platform och ännu inte har aktiva mål visas inte kontrollpanelen [!UICONTROL Destinations] och fliken [!UICONTROL Overview]. Om du i stället väljer [!UICONTROL Destinations] i den vänstra navigeringen visas fliken [[!UICONTROL Catalog] ](#catalog).

![Fliken Översikt över kontrollpanelen Destinationer.](../../dashboards/images/destinations/dashboard-overview.png)

## [!UICONTROL Catalog] {#catalog}

Fliken **[!UICONTROL Catalog]** visar en lista över alla mål som är tillgängliga i [!DNL Experience Platform] och som du kan skicka data till.

Användargränssnittet [!DNL Experience Platform] innehåller flera sök- och filteralternativ på målkatalogsidan:

* Använd sökfunktionen på sidan för att hitta ett specifikt mål.
* Filtrera mål med kontrollen [!UICONTROL Categories].
* Växla mellan [!UICONTROL All destinations] och [!UICONTROL My destinations]. När du väljer **[!UICONTROL All destinations]** visas alla tillgängliga [!DNL Experience Platform]-mål. När du väljer **[!UICONTROL My destinations]** kan du bara se de mål som du har upprättat en anslutning med.
* Välj detta om du vill visa typerna **[!UICONTROL Connections]** och/eller **[!UICONTROL Extensions]**. Läs [Måltyper och kategorier](../destination-types.md) om du vill veta skillnaden mellan de två kategorierna.

![Målkatalogen visar några annonser och molnlagringsmål.](../assets/ui/workspace/catalog.png)

Målkorten innehåller alternativ för primär och sekundär kontroll. De primära kontrollerna är [!UICONTROL Set up], [!UICONTROL Activate], [!UICONTROL Activate audiences] eller [!UICONTROL Export datasets]. De sekundära kontrollerna tillåter visningsalternativ. Dessa kontroller beskrivs nedan:

| Kontroll | Beskrivning |
|---------|----------|
| [!UICONTROL Set up] | Gör att du kan skapa en anslutning till målet. |
| [!UICONTROL Activate] | När du har upprättat en anslutning till målet kan du aktivera målgrupper eller exportera datauppsättningar till det här målet. |
| [!UICONTROL Activate audiences] | När du har upprättat en anslutning till målet kan du aktivera målgrupper till det här målet. |
| [!UICONTROL Export datasets] | När du har upprättat en anslutning till målet kan du exportera datauppsättningar till det här målet. |
| [!UICONTROL View account] | Visa konton som du har anslutit för ett mål. |
| [!UICONTROL View dataflows] | Visa dataaktiveringsflödena som finns för ett mål. |
| [!UICONTROL View documentation] | Öppnar en länk till dokumentationssidan för det specifika målet, för mer information och för att hjälpa dig att konfigurera det. |

{style="table-layout:auto"}

![Kontroller för målkortet](../assets/ui/workspace/destination-card-options.png)

Välj ett målkort i katalogen för att öppna den högra listen. Här visas en beskrivning av målet. Högerspåret har samma kontroller som beskrivs i tabellen ovan, inklusive en beskrivning av destinationen och en indikation på destinationskategori och typ.

![Alternativ för målkatalog](../assets/ui/workspace/destination-right-rail.png)

Mer information om målkategorier och information om varje mål finns i [målkatalogen](../catalog/overview.md) och [måltyperna och -kategorierna](../destination-types.md).

## [!UICONTROL Accounts] {#accounts}

Fliken **[!UICONTROL Accounts]** visar information om anslutningar som du har upprättat med olika destinationer och gör att du kan uppdatera eller ta bort befintlig kontoinformation. Se tabellen nedan för all information som du kan få för varje destinationskonto.

>[!TIP]
>
> * Markera ellipsen (`...`) i kolumnen [!UICONTROL Platform] och använd kontrollen ![Aktivera kontroll ](/help/images/icons/data-add.png)**[!UICONTROL Activate]**/**[!UICONTROL Activate audiences]**/**[!UICONTROL Export datasets]**&#x200B;för att exportera målgrupper eller datauppsättningar till det målet.
> * Markera ellipsen (`...`) i kolumnen [!UICONTROL Platform] och använd kontrollen ![Redigera information ](/help/images/icons/edit.png)**[!UICONTROL Edit details]**&#x200B;för att [uppdatera](update-accounts.md) informationen för ett befintligt målkonto.
> * Markera ellipsen (`...`) i kolumnen [!UICONTROL Platform] och använd kontrollen ![Ta bort ](/help/images/icons/delete.png)**[!UICONTROL Delete]**&#x200B;för att [ta bort](delete-destination-account.md) ett befintligt målkonto.

![Fliken Konton](../assets/ui/workspace/destination-account-options.png)

| Element | Beskrivning |
|---|---|
| [!UICONTROL Name] | Namnet som du tilldelade målkontot när [konfigurerade](connect-destination.md#authenticate) målet. |
| [!UICONTROL Destination] | Målkopplingen som du har konfigurerat anslutningen för. |
| [!UICONTROL Connection Type] | Representerar kontoanslutningstypen för din lagringsbucket eller destination. Beroende på målet är autentiseringsalternativen: <ul><li>För e-postmarknadsföringsmål: Kan vara S3, FTP eller Azure Blob.</li><li>För reklamdestinationer i realtid: server till server</li><li>För Amazon S3-molnlagringsmål: Åtkomstnyckel </li><li>För SFTP-molnlagringsmål: Grundläggande autentisering för SFTP</li><li>OAuth 1- eller OAuth 2-autentisering</li><li>Autentisering av innehavartoken</li></ul> |
| [!UICONTROL Username] | Användarnamnet som du valde i [målarbetsflödet för anslutning](../catalog/email-marketing/overview.md#connect-destination). |
| [!UICONTROL Connections] | Representerar antalet unika slutförda måldataflöden som är kopplade till grundläggande information som skapats för ett mål. |
| [!UICONTROL Authorization date] | Det datum då anslutningen till det här målet auktoriserades. |
| [!UICONTROL Expiration date] | Det datum då anslutningsauktoriseringen till det här målet upphör. <br>**Viktigt**: Den här kolumnen är för närvarande bara tillgänglig för [Facebook](../catalog/social/facebook.md)-anslutningen. |

{style="table-layout:auto"}

## [!UICONTROL Browse] {#browse}

Fliken **[!UICONTROL Browse]** visar de mål som du har upprättat en anslutning till. Destinationer med växeln **[!UICONTROL Enabled/Disabled]** aktiverad anger målet som aktivt respektive inaktivt. Du kan också visa de mål där data flödar genom att välja **[!UICONTROL Audiences]** > **[!UICONTROL Browse]** och välja en målgrupp att inspektera. Se tabellen nedan för all information som anges för varje mål på fliken [!UICONTROL Browse]:

>[!TIP]
>
> * Markera ellipsen (`...`) i kolumnen [!UICONTROL Name] och använd kontrollen ![Aktivera målgrupper](/help/images/icons/data-add.png) **[!UICONTROL Activate audiences]** för att exportera målgrupper eller datauppsättningar till det målet.
> * Markera ellipsen (`...`) i kolumnen [!UICONTROL Name] och använd kontrollen ![Redigera målkontroll ](/help/images/icons/edit.png)**[!UICONTROL Edit destination]**&#x200B;för att redigera befintliga målanslutningar. Mer information finns i självstudiekursen [Redigera mål](/help/destinations/ui/edit-destination.md).
> * Markera ellipsen (`...`) i kolumnen [!UICONTROL Name] och använd kontrollen ![Redigera marknadsföringsåtgärder](/help/images/icons/edit-marketing-actions.svg) **[!UICONTROL Edit marketing actions]** för att [ändra marknadsföringsåtgärderna](/help/destinations/ui/edit-activation.md#edit-marketing-actions) för det valda målet.
> * Markera ellipsen (`...`) i kolumnen [!UICONTROL Name] och använd kontrollen ![Ta bort](/help/images/icons/delete.png) **[!UICONTROL Delete]** för att [ta bort](delete-destinations.md) en befintlig anslutning till ett mål.
> * Markera ellipsen (`...`) i kolumnen [!UICONTROL Name] och använd kontrollen ![Visa i övervakningskontroll](/help/images/icons/monitoring.png) **[!UICONTROL View in monitoring]** för att visa aktiveringsinformation för det här målet på kontrollpanelen [för övervakning](/help/dataflows/ui/monitor-destinations.md#monitoring-destinations-dashboard).
> * Markera ellipsen (`...`) i kolumnen [!UICONTROL Name] och använd kontrollen ![Prenumerera på aviseringar ](/help/images/icons/alert-add.png) **[!UICONTROL Subscribe to alerts]** för att prenumerera på aviseringar om måldataflöde. Du kan prenumerera på aviseringar för att få meddelanden om status, lyckade eller misslyckade flödeskörningar. Se [Prenumerera på destinationsvarningar i sitt sammanhang](alerts.md) om du vill ha mer information om måldataflödesvarningar.

![Fliken Bläddra](../assets/ui/workspace/browse-tab.png)

| Element | Beskrivning |
|---------|----------|
| Namn | Namnet som du angav för aktiveringsflödet till den här destinationen. |
| Datatyp | Den typ av data som stöds av målanslutningen. Datatyper som stöds: <ul><li>**[!UICONTROL Customers]**</li><li>**[!UICONTROL Prospects]**</li><li>**[!UICONTROL Accounts]**</li><li>**[!UICONTROL Datasets]**</li></ul> |
| [!UICONTROL Last Dataflow Run Status] | Status för den senaste dataflödeskörningen. Mer information om dataflödeskörningar finns i [Visa målinformation](destination-details-page.md). |
| [!UICONTROL Last Dataflow Run Date] | Tid och datum då den senaste dataflödeskörningen inträffade. Mer information om dataflödeskörningar finns i [Visa målinformation](destination-details-page.md). |
| [!UICONTROL Destination] | Målplattformen som du valde för aktiveringsflödet. |
| [!UICONTROL Account Expiration Date] | Det datum då anslutningsauktoriseringen till det här målet upphör. <br>**Viktigt**: Den här kolumnen är för närvarande bara tillgänglig för [Facebook](../catalog/social/facebook.md)-anslutningen. |
| [!UICONTROL Connection Type] | Representerar anslutningstypen för din lagringsbucket eller destination. <ul><li>För e-postmarknadsföringsmål: Kan vara S3, FTP eller [!DNL Azure Blob].</li><li>För reklamdestinationer i realtid: server till server.</li><li>För direktuppspelningsmål: Kan vara [!DNL Azure Event Hubs] eller [!DNL Amazon Kinesis].</li></ul> |
| [!UICONTROL Username] | De kontoautentiseringsuppgifter som du har valt för målflödet. |
| [!UICONTROL Activation Data] | Anger antalet målgrupper som aktiveras till det här målet. Välj den här kontrollen om du vill veta mer om de aktiverade målgrupperna. Mer information om aktiverade målgrupper finns på sidan [Aktiveringsdata](/help/destinations/ui/destination-details-page.md#activation-data) i målinformationssidan. |
| [!UICONTROL Created] | Datum och UTC-tid när aktiveringsflödet till målet skapades. Välj uppåt-/nedåtpilen för att sortera aktiveringsflödena efter det senaste först eller det äldsta först. |
| [!UICONTROL Status] | `Enabled` eller `Disabled`. Anger om data aktiveras till det här målet. |
| [!UICONTROL Access labels] | Visar alla åtkomstetiketter som har lagts till i måldataflödet. Läs mer om att [använda åtkomstetiketter i måldataflöden](/help/access-control/abac/apply-access-labels-destinations.md). |

Klicka på en målrad för att visa mer information om målet i den högra listen, t.ex. mål-ID, beskrivning, antal aktiva målgrupper med mera.

![Klicka på målraden](../assets/ui/workspace/click-destination-row.png)

Välj målnamnet för att visa information om målgrupper som har aktiverats för det här målet. Klicka på **[!UICONTROL Edit activation]** om du vill ändra eller lägga till i målgrupperna som skickas till det här målet.

## [!UICONTROL System View] {#system-view}

På fliken **[!UICONTROL System View]** visas en grafisk representation av de aktiveringsflöden som du har konfigurerat i Adobe Experience Platform.

![Data-flows1](../assets/ui/workspace/data-flows1.png)

Välj något av de mål som visas på sidan och klicka på **[!UICONTROL View dataflows]** för att visa information om alla anslutningar som du har konfigurerat för varje mål.

![Data-flows2](../assets/ui/workspace/data-flows2.png)
