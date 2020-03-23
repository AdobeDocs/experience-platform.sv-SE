---
title: Arbetsytan Destinationer
seo-title: Arbetsytan Destinationer
description: I Adobe Real-time Customer Data Platform väljer du Destinationer i det vänstra navigeringsfältet för att komma åt målarbetsytan.
seo-description: I Adobe Real-time Customer Data Platform väljer du Destinationer i det vänstra navigeringsfältet för att komma åt målarbetsytan.
translation-type: tm+mt
source-git-commit: 132bc9787a86045adba559c769b02927a6045b17

---


# Arbetsytan Destinationer {#destinations-workspace}

I Adobe Real-time Customer Data Platform väljer du **Destinationer** i det vänstra navigeringsfältet för att komma åt arbetsytan Destinationer.

Arbetsytan Destinationer består av fyra avsnitt, **Katalog**, **Bläddra**, **Konton** och **Dataflöden**, som beskrivs i avsnitten nedan.

![Destinationer - översikt](/help/rtcdp/destinations/assets/destinations-overview.png)

## Katalog {#catalog}

På fliken **[!UICONTROL Catalog]** visas en lista med alla destinationer som Adobe erbjuder och som du kan skicka data till. Välj ett mål i katalogen för att öppna den högra listen. Här kan du konfigurera en anslutning till målet (**anslutningsmålet**) eller läsa mer om varje mål i dokumentationen (**Visa dokumentation**).

![Alternativ för målkatalog](/help/rtcdp/destinations/assets/destination-ui-catalog-options.png)

Mer information om målkategorier och information om varje mål finns i [Målkatalog](/help/rtcdp/destinations/destinations-catalog.md).

## Bläddra {#browse}

På fliken **[!UICONTROL Browse]** visas de mål som du har upprättat en anslutning till. Destinationer med aktiverad växel aktiverad anger målet som aktivt och vice versa. Du kan också visa de mål där data flödar genom att välja **Segment > Bläddra** och välja ett segment som ska inspekteras. Se tabellen nedan för all information som finns för varje mål på fliken Bläddra:

![Fliken Bläddra](/help/rtcdp/destinations/assets/browse-tab.png)

| Element | Beskrivning |
---------|----------
| Målnamn | Namnet som du angav för aktiveringsflödet till den här destinationen. |
| Mål | Målplattformen som du valde för aktiveringsflödet. |
| Skapad | Datum och UTC-tid när aktiveringsflödet till målet skapades. |
| Anslutningstyp | *Endast* för e-postmarknadsföringsmål. Representerar anslutningstypen för lagringskassetten. Kan vara S3 eller FTP. |
| Användarnamn | De kontoautentiseringsuppgifter som du har valt för målflödet. |
| Segment | Antalet segment som aktiveras till det här målet. |
| Status | `Active` eller `Inactive`. Anger om data för närvarande aktiveras till det här målet. Information om hur du redigerar status finns i [Inaktivera aktivering](/help/rtcdp/destinations/activate-destinations.md#disable-activation). |

Klicka på en målrad för att visa mer information om målet i den högra listen.

![Klicka på målraden](/help/rtcdp/destinations/assets/click-destination-row.png)

Markera målnamnet om du vill visa information om de segment som har aktiverats för det här målet. Klicka **[!UICONTROL Edit activation]** för att ändra eller lägga till i de segment som skickas till det här målet.

## Konton {#accounts}

På fliken **[!UICONTROL Accounts]** kan du lära dig mer om anslutningar som du har upprättat med olika mål. Se tabellen nedan för all information du kan få på varje mål:

![Fliken Konton](/help/rtcdp/destinations/assets/accounts-tab.png)

| Element | Beskrivning |
---------|----------
| Plattform | Det mål som du har konfigurerat anslutningen för. |
| Användarnamn | Användarnamnet som du valde i [målguiden](/help/rtcdp/destinations/email-marketing-destinations.md#connect-destination)för anslutning. |
| Flöden | Representerar antalet unika lyckade målflöden som är kopplade till grundläggande information som skapats för ett mål. |
| Auktoriserad | Det datum då anslutningen till det här målet auktoriserades. |

## Dataflöden {#data-flows}

På **[!UICONTROL Data flows]** fliken visas en grafisk representation av de aktiveringsflöden som du har konfigurerat i kunddataplattformen i realtid.

![Data-flows1](/help/rtcdp/destinations/assets/data-flows1.png)

Välj något av de mål som visas på sidan och tryck på för **[!UICONTROL View flows]** att se information om alla dataflöden som du har ställt in för varje mål.

![Data-flows2](/help/rtcdp/destinations/assets/data-flows2.png)