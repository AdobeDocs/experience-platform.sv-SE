---
keywords: plattform;mål;målarbetsyta;arbetsyta;ui;destinationer ui;katalog;destinationskatalog;
title: Arbetsytan Destinationer
description: 'Arbetsytan Destinationer består av fyra avsnitt: Katalog, Bläddra, Konton och Systemvy. De beskrivs i avsnitten nedan.'
seo-description: In Adobe Experience Platform, select Destinations from the left navigation bar to access the destinations workspace.
exl-id: 0f46f08d-0fe3-441d-933a-86bc146c0f19
source-git-commit: f4721d3f114357b25517e4e66f1f626f82621c34
workflow-type: tm+mt
source-wordcount: '774'
ht-degree: 0%

---

# Arbetsytan Destinationer {#destinations-workspace}

I Adobe Experience Platform väljer du **[!UICONTROL Destinations]** i det vänstra navigeringsfältet för att komma åt arbetsytan [!UICONTROL Destinations].

Arbetsytan [!UICONTROL Destinations] består av fem avsnitt, [!UICONTROL Overview], [!UICONTROL Catalog], [!UICONTROL Browse], [!UICONTROL Accounts] och [!UICONTROL System View], som beskrivs i avsnitten nedan.

![Destinationer - översikt](../assets/ui/workspace/destinations-overview.png)

## [!UICONTROL Overview] {#overview}

På fliken **[!UICONTROL Overview]** visas kontrollpanelen [!UICONTROL Destinations] med viktiga mått för organisationens måldata. Mer information finns i handboken [[!UICONTROL Destinations] för kontrollpanelen](../../dashboards/guides/destinations.md).

>[!NOTE]
>
>Om din organisation är ny för Experience Platform och ännu inte har några aktiva mål visas inte kontrollpanelen [!UICONTROL Destinations] och fliken [!UICONTROL Overview]. Om du i stället väljer [!UICONTROL Destinations] i den vänstra navigeringen visas fliken [[!UICONTROL Catalog]](#catalog).

![](../../dashboards/images/destinations/dashboard-overview.png)

## [!UICONTROL Catalog] {#catalog}

På fliken **[!UICONTROL Catalog]** visas en lista med alla mål som är tillgängliga i [!DNL Platform] som du kan skicka data till.

[!DNL Platform]-användargränssnittet innehåller flera sök- och filteralternativ på målkatalogsidan:

* Använd sökfunktionen på sidan för att hitta ett specifikt mål.
* Filtrera mål med kontrollen [!UICONTROL Categories].
* Växla mellan [!UICONTROL All destinations] och [!UICONTROL My destinations]. När du väljer **[!UICONTROL All destinations]** visas alla tillgängliga [!DNL Platform]-mål. När du väljer **[!UICONTROL My destinations]** kan du bara se de mål som du har upprättat en anslutning till.
* Välj om du vill visa **[!UICONTROL Connections]** och/eller **[!UICONTROL Extensions]**. Mer information om skillnaden mellan de två kategorierna finns i [Måltyper och kategorier](../destination-types.md).

![Katalog](../assets/ui/workspace/catalog.png)

Målkorten innehåller antingen en **[!UICONTROL Set up]**- eller en **[!UICONTROL Activate segments]**-kontroll och en sekundär kontroll som visar fler alternativ. Dessa kontroller beskrivs nedan:

| Kontroll | Beskrivning |
|---------|----------|
| [!UICONTROL Set up] | Gör att du kan skapa en anslutning till målet. |
| [!UICONTROL Activate segments] | När du har upprättat en anslutning till målet kan du aktivera segment. |
| [!UICONTROL View account] | Visa konton som du har anslutit för ett mål. |
| [!UICONTROL View dataflows] | Visa dataaktiveringsflödena som finns för ett mål. |
| [!UICONTROL View documentation] | Öppnar en länk till dokumentationssidan för det specifika målet, för mer information och för att hjälpa dig att konfigurera det. |

{style=&quot;table-layout:auto&quot;}

![Kontroll av destinationskortet](../assets/ui/workspace/destination-card-options.png)

Välj ett målkort i katalogen för att öppna den högra listen. Här visas en beskrivning av målet. Högerspåret har samma kontroller som beskrivs i tabellen ovan, inklusive en beskrivning av destinationen och en indikation på destinationskategori och typ.

![Alternativ för målkatalog](../assets/ui/workspace/destination-right-rail.png)

Mer information om målkategorier och information om varje mål finns i [målkatalogen](../catalog/overview.md) och [Måltyper och -kategorier](../destination-types.md).

## [!UICONTROL Accounts] {#accounts}

På fliken **[!UICONTROL Accounts]** visas information om de anslutningar du har upprättat med olika mål. Du kan även uppdatera befintlig anslutningsinformation. Mer information finns i [Uppdatera konton](update-accounts.md).

## [!UICONTROL Browse] {#browse}

På fliken **[!UICONTROL Browse]** visas de mål som du har upprättat en anslutning till. Destinationer med växeln **[!UICONTROL Enabled/Disabled]** aktiverad anger målet som aktivt respektive inaktivt. Du kan också visa de mål där data flödar genom att välja **[!UICONTROL Segments]** > **[!UICONTROL Browse]** och välja ett segment som ska inspekteras. Se tabellen nedan för all information som finns för varje mål på fliken Bläddra:

>[!TIP]
>
> * Markera de tre punkterna i kolumnen [!UICONTROL Name] och använd knappen ![Lägg till segment ](../assets/ui/workspace/add-data-symbol.png)**[!UICONTROL Activate segments]**för att skicka segment till det målet.
> * Markera de tre punkterna i kolumnen [!UICONTROL Name] och använd knappen ![Ta bort mål ](../assets/ui/workspace/delete-destination-symbol.png)**[!UICONTROL Delete]**för att [ta bort en befintlig anslutning till ett mål.](delete-destinations.md)


![Fliken Bläddra](../assets/ui/workspace/browse-tab.png)

| Element | Beskrivning |
|---------|----------|
| Namn | Namnet som du angav för aktiveringsflödet till den här destinationen. Samma kolumn innehåller två kontroller: [!UICONTROL Activate ] och [!UICONTROL Delete destination]. |
| [!UICONTROL Last Flow Run Status] | Status för den senaste dataflödeskörningen. Mer information om dataflöden finns i [Visa målinformation](destination-details-page.md). |
| [!UICONTROL Last Flow Run Date] | Tid och datum då den senaste dataflödeskörningen inträffade. Mer information om dataflöden finns i [Visa målinformation](destination-details-page.md). |
| [!UICONTROL Destination] | Målplattformen som du valde för aktiveringsflödet. |
| [!UICONTROL Connection Type] | Representerar anslutningstypen för din lagringsbucket eller destination. <ul><li>För e-postmarknadsföringsmål: Kan vara S3, FTP eller [!DNL Azure Blob].</li><li>För reklamdestinationer i realtid: Server-till-server.</li><li>För direktuppspelningsmål: Kan vara [!DNL Azure Event Hubs] eller [!DNL Amazon Kinesis].</li></ul> |
| [!UICONTROL Username] | De kontoautentiseringsuppgifter som du har valt för målflödet. |
| [!UICONTROL Activation Data] | Anger antalet segment som aktiveras till det här målet. Välj den här kontrollen om du vill veta mer om de aktiverade segmenten. Se [Aktiveringsdata](/help/destinations/ui/destination-details-page.md#activation-data) på sidan med målinformation för mer information om de aktiverade segmenten. |
| [!UICONTROL Created] | Datum och UTC-tid när aktiveringsflödet till målet skapades. |
| [!UICONTROL Status] | `Active` eller `Inactive`. Anger om data aktiveras till det här målet. |

Klicka på en målrad för att visa mer information om målet i den högra listen.

![Klicka på målraden](../assets/ui/workspace/click-destination-row.png)

Markera målnamnet om du vill visa information om de segment som har aktiverats för det här målet. Klicka på **[!UICONTROL Edit activation]** om du vill ändra eller lägga till i de segment som skickas till det här målet.

## [!UICONTROL System View] {#system-view}

På fliken **[!UICONTROL System View]** visas en grafisk representation av de aktiveringsflöden som du har konfigurerat i Adobe Experience Platform.

![Data-flows1](../assets/ui/workspace/data-flows1.png)

Välj något av de mål som visas på sidan och klicka på **[!UICONTROL View dataflows]** för att se information om alla anslutningar som du har konfigurerat för varje mål.

![Dataflöden2](../assets/ui/workspace/data-flows2.png)
