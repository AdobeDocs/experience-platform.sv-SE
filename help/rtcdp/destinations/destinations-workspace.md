---
keywords: RTCDP;rtcdp
title: Arbetsytan Destinationer
seo-title: Arbetsytan Destinationer
description: I Adobe Real-time Customer Data Platform väljer du Destinationer i det vänstra navigeringsfältet för att komma åt målarbetsytan.
seo-description: I Adobe Real-time Customer Data Platform väljer du Destinationer i det vänstra navigeringsfältet för att komma åt målarbetsytan.
translation-type: tm+mt
source-git-commit: ac9c629e8c83d3e056ba94b30d978edbda274923
workflow-type: tm+mt
source-wordcount: '746'
ht-degree: 1%

---


# Arbetsytan Destinationer {#destinations-workspace}

I Adobe Real-time Customer Data Platform väljer du **[!UICONTROL Destinations]** från det vänstra navigeringsfältet för att komma åt [!UICONTROL Destinations] arbetsytan.

Arbetsytan består [!UICONTROL Destinations] av fyra avsnitt, **[!UICONTROL Catalog]**, **[!UICONTROL Browse]**, **[!UICONTROL Accounts]** och **[!UICONTROL System View]**, som beskrivs i avsnitten nedan.

![Destinationer - översikt](/help/rtcdp/destinations/assets/destinations-overview.png)

## [!UICONTROL Catalog] {#catalog}

På fliken **[!UICONTROL Catalog]** visas en lista med alla mål som är tillgängliga i CDP i realtid i Adobe som du kan skicka data till.

Användargränssnittet för CDP i realtid i Adobe innehåller ett antal sök- och filteralternativ på katalogsidan för mål:

* Använd sökfunktionen på sidan för att hitta ett specifikt mål.
* Filtrera mål med hjälp av **[!UICONTROL Categories]** kontrollen.
* Växla mellan **[!UICONTROL All destinations]** och **[!UICONTROL My destinations]**. När **[!UICONTROL All destinations]** är markerat visas alla tillgängliga CDP-mål i realtid i Adobe. När **[!UICONTROL My destinations]** är markerat kan du bara se de mål som du har upprättat en anslutning till.
* Välj för att visa **[!UICONTROL Connections]** och/eller **[!UICONTROL Extensions]**. Mer information om skillnaden mellan de två kategorierna finns i [Måltyper och kategorier](/help/rtcdp/destinations/destination-types.md).

![målgruppsfiltrering och sökdemo](/help/rtcdp/destinations/assets/destinations-search-and-filter.gif)

Målkorten innehåller antingen en **[!UICONTROL Configure]** eller en **[!UICONTROL Activate]** kontroll och en sekundär kontroll som visar fler alternativ. Dessa beskrivs nedan:

| Kontroll | Beskrivning |
---------|----------
| [!UICONTROL Configure] | Gör att du kan skapa en anslutning till målet. |
| [!UICONTROL Activate] | När du har upprättat en anslutning till målet kan du aktivera segment. |
| [!UICONTROL View account] | Visa konton som du har anslutit för ett mål. |
| [!UICONTROL View dataflows] | Visa dataaktiveringsflödena som finns för ett mål. |
| [!UICONTROL View documentation] | Öppnar en länk till dokumentationssidan för det specifika målet, för mer information och för att hjälpa dig att konfigurera det. |

![Kontroll av destinationskortet](/help/rtcdp/destinations/assets/destination-card-options.png)

Välj ett målkort i katalogen för att öppna den högra listen.  Här visas en beskrivning av målet. Högerspåret har samma kontroller som beskrivs i tabellen ovan, samt en beskrivning av destinationen och en indikation på destinationskategori och typ.

![Alternativ för målkatalog](/help/rtcdp/destinations/assets/destination-right-rail.png)

Mer information om målkategorier och information om varje mål finns i [Målkatalog](/help/rtcdp/destinations/destinations-catalog.md) och [Måltyper och -kategorier](/help/rtcdp/destinations/destination-types.md).

## [!UICONTROL Browse] {#browse}

På fliken **[!UICONTROL Browse]** visas de mål som du har upprättat en anslutning till. Destinationer med **[!UICONTROL enabled]** växlingsknappen aktiverad anger målet som aktivt och vice versa. Du kan också visa de mål där data flödar genom att välja **[!UICONTROL Segments]** > **[!UICONTROL Browse]** och markera ett segment som ska inspekteras. Se tabellen nedan för all information som finns för varje mål på fliken Bläddra:

![Fliken Bläddra](/help/rtcdp/destinations/assets/browse-tab.png)

| Element | Beskrivning |
---------|----------
| Namn | Namnet som du angav för aktiveringsflödet till den här destinationen. |
| [!UICONTROL Destination] | Målplattformen som du valde för aktiveringsflödet. |
| [!UICONTROL Connection Type] | Representerar anslutningstypen för din lagringsbucket eller destination. <ul><li>För e-postmarknadsföringsmål: Kan vara S3 eller FTP.</li><li>För reklamdestinationer i realtid: Server-till-server</li></ul> |
| [!UICONTROL Username] | De kontoautentiseringsuppgifter som du har valt för målflödet. |
| [!UICONTROL Segments] | Antalet segment som aktiveras till det här målet. |
| [!UICONTROL Created] | Datum och UTC-tid när aktiveringsflödet till målet skapades. |
| [!UICONTROL Status] | `Active` eller `Inactive`. Anger om data för närvarande aktiveras till det här målet. Information om hur du redigerar status finns i [Inaktivera aktivering](/help/rtcdp/destinations/activate-destinations.md#disable-activation). |

Klicka på en målrad för att visa mer information om målet i den högra listen.

![Klicka på målraden](/help/rtcdp/destinations/assets/click-destination-row.png)

Markera målnamnet om du vill visa information om de segment som har aktiverats för det här målet. Klicka **[!UICONTROL Edit activation]** för att ändra eller lägga till i de segment som skickas till det här målet.

## [!UICONTROL Accounts] {#accounts}

På fliken **[!UICONTROL Accounts]** kan du lära dig mer om anslutningar som du har upprättat med olika mål. Se tabellen nedan för all information du kan få på varje mål:

![Fliken Konton](/help/rtcdp/destinations/assets/accounts-tab.png)

| Element | Beskrivning |
---------|----------
| [!UICONTROL Platform] | Det mål som du har konfigurerat anslutningen för. |
| [!UICONTROL Connection Type] | Representerar anslutningstypen för din lagringsbucket eller destination. <ul><li>För e-postmarknadsföringsmål: Kan vara S3 eller FTP.</li><li>För reklamdestinationer i realtid: Server-till-server</li><li>För molnlagringsmål för Amazon S3: Åtkomstnyckel </li><li>För SFTP-molnlagringsmål: Grundläggande autentisering för SFTP</li></ul> |
| [!UICONTROL Username] | Användarnamnet som du valde i [målguiden](/help/rtcdp/destinations/email-marketing-destinations.md#connect-destination)för anslutning. |
| [!UICONTROL Data Flows] | Representerar antalet unika lyckade målflöden som är kopplade till grundläggande information som skapats för ett mål. |
| [!UICONTROL Authorized] | Det datum då anslutningen till det här målet auktoriserades. |
| [!UICONTROL Status] | `Active` eller `Inactive`. Anger om data för närvarande aktiveras till det här målet. Information om hur du redigerar status finns i [Inaktivera aktivering](/help/rtcdp/destinations/activate-destinations.md#disable-activation). |

## [!UICONTROL System View] {#system-view}

På **[!UICONTROL System View]** fliken visas en grafisk representation av de aktiveringsflöden som du har konfigurerat i kunddataplattformen i realtid.

![Data-flows1](/help/rtcdp/destinations/assets/data-flows1.png)

Välj något av de mål som visas på sidan och tryck på för **[!UICONTROL View flows]** att se information om alla anslutningar som du har konfigurerat för varje mål.

![Data-flows2](/help/rtcdp/destinations/assets/data-flows2.png)