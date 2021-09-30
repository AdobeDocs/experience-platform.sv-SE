---
keywords: målinriktad personalisering, destination, mål för upplevelseplattform;adobe target destination;
title: Adobe Target-anslutning
description: Adobe Target är en applikation som innehåller personalisering och experimenterande i realtid, 1:1, och AI-driven i alla inkommande kundinteraktioner på webbplatser, i mobilappar med mera.
source-git-commit: caccd096c9165139d9b966bbfcb311456276192a
workflow-type: tm+mt
source-wordcount: '391'
ht-degree: 1%

---


# Adobe Target-anslutning (beta) {#adobe-target-connection}

## Översikt {#overview}

>[!IMPORTANT]
>
>Adobe Target-anslutningen i Adobe Experience Platform är för närvarande i Beta. Dokumentationen och funktionerna kan komma att ändras.

Adobe Target är en applikation som ger personalisering och experimenterande i realtid, 1:1, i AI, i alla kundinteraktioner, på webbplatser, i mobilappar med mera.

Adobe Target är en personaliseringsanslutning i Adobe Experience Platform.

## Förutsättningar {#prerequisites}

Integrationen drivs av [Adobe Experience Platform Web SDK](../../../edge/home.md). Du måste använda denna SDK för att kunna använda den här destinationen.

## Exporttyp {#export-type}

**Profilbegäran**  - du begär alla segment som är mappade i Adobe Target-målet för en enda profil.

## Användningsfall {#use-cases}

**Anpassa en startsidesbanderoll**

Ett uthyrnings- och säljföretag vill skräddarsy sin hemsida med en banderoll som bygger på kundsegmentets kvalifikationer i Adobe Experience Platform. Företaget kan välja vilka målgrupper som ska få en personaliserad upplevelse och skicka dem till Adobe Target som målinriktningskriterier för sitt Target-erbjudande.

## Anslut till målet {#connect}

Om du vill ansluta till det här målet följer du stegen som beskrivs i självstudiekursen [för målkonfiguration](../../ui/connect-destination.md).

Adobe Experience Platform ansluter automatiskt till ert företags Adobe Target-instans. Ingen autentisering krävs.

### Anslutningsparametrar {#parameters}

När du [konfigurerar](../../ui/connect-destination.md) det här målet måste du ange följande information:

* **Namn**: Fyll i det önskade namnet för det här målet.
* **Beskrivning**: Ange en beskrivning för destinationen. Du kan till exempel ange vilken kampanj du använder det här målet för. Det här fältet är valfritt.
* **Datastream-ID**: Detta anger i vilken datainsamlingsdatastam segmenten ska inkluderas i svaret på sidan. I den nedrullningsbara menyn visas endast datastreams som har målkonfigurationen aktiverad. Mer information finns i [Konfigurera en datastream](../../../edge/fundamentals/datastreams.md).

## Aktivera segment till den här destinationen {#activate}

Läs [Aktivera profiler och segment för att profilera mål för begäran](../../ui/activate-profile-request-destinations.md) om du vill ha instruktioner om hur du aktiverar målgruppssegment för den här destinationen.

## Exporterade data {#exported-data}

Adobe Target läser profildata från Adobe Experience Platform Edge Network så att inga data exporteras.

## Dataanvändning och styrning {#data-usage-governance}

Alla [!DNL Adobe Experience Platform]-mål är kompatibla med dataanvändningsprinciper när data hanteras. Mer information om hur [!DNL Adobe Experience Platform] framtvingar datastyrning finns i [översikten över datastyrning](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html).
