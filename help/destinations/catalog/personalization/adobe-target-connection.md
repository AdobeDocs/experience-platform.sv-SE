---
keywords: målinriktad personalisering, destination, mål för upplevelseplattform;adobe target destination;
title: Adobe Target-anslutning (beta)
description: Adobe Target är en applikation som innehåller personalisering och experimenterande i realtid, 1:1, och AI-driven i alla inkommande kundinteraktioner på webbplatser, i mobilappar med mera.
exl-id: 3e3c405b-8add-4efb-9389-5ad695bc9799
source-git-commit: fae3d9a5aff3e84354831026e9724e1c85d32b5c
workflow-type: tm+mt
source-wordcount: '453'
ht-degree: 0%

---

# Adobe Target-anslutning (beta) {#adobe-target-connection}

## Översikt {#overview}

>[!IMPORTANT]
>
>Adobe Target-anslutningen i Adobe Experience Platform är för närvarande i Beta. Dokumentationen och funktionerna kan komma att ändras.

Adobe Target är en applikation som ger personalisering och experimenterande i realtid, 1:1, i AI, i alla kundinteraktioner, på webbplatser, i mobilappar med mera.

Adobe Target är en personaliseringsanslutning i Adobe Experience Platform.

## Förutsättningar {#prerequisites}

Den här integreringen drivs av [Adobe Experience Platform Web SDK](../../../edge/home.md). Du måste använda denna SDK för att kunna använda den här destinationen.

## Exporttyp {#export-type}

**Profilbegäran** - du begär alla segment som är mappade i Adobe Target-målet för en enda profil.

## Användningsfall {#use-cases}

**Anpassa en startsidesbanderoll**

Ett uthyrnings- och säljföretag vill skräddarsy sin hemsida med en banderoll som bygger på kundsegmentets kvalifikationer i Adobe Experience Platform. Företaget kan välja vilka målgrupper som ska få en personaliserad upplevelse och skicka dem till Adobe Target som målinriktningskriterier för sitt Target-erbjudande.

## Anslut till målet {#connect}

>[!CONTEXTUALHELP]
>id="platform_destinations_target_datastream"
>title="Om dataStream-ID"
>abstract="Med det här alternativet anger du i vilken datainsamlingsdatastam segmenten ska inkluderas i svaret på sidan. I den nedrullningsbara menyn visas endast datastreams som har målkonfigurationen aktiverad. Du måste konfigurera ett datastream innan du kan konfigurera målet."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html?lang=en" text="Lär dig hur du konfigurerar ett datastream."

Om du vill ansluta till det här målet följer du stegen som beskrivs i [självstudiekurs om destinationskonfiguration](../../ui/connect-destination.md).

Adobe Experience Platform ansluter automatiskt till ert företags Adobe Target-instans. Ingen autentisering krävs.

### Anslutningsparametrar {#parameters}

while [konfigurera](../../ui/connect-destination.md) Om du vill ange destinationen måste du ange följande information:

* **Namn**: Fyll i det önskade namnet för det här målet.
* **Beskrivning**: Ange en beskrivning för destinationen. Du kan till exempel ange vilken kampanj du använder det här målet för. Det här fältet är valfritt.
* **Datastream-ID**: Detta anger i vilken datainsamlingsdatastam segmenten ska inkluderas i svaret på sidan. I den nedrullningsbara menyn visas endast datastreams som har målkonfigurationen aktiverad. Se [Konfigurera ett datastream](../../../edge/fundamentals/datastreams.md) för mer information.

## Aktivera segment till den här destinationen {#activate}

Läs [Aktivera profiler och segment för att profilera mål för begäran](../../ui/activate-profile-request-destinations.md) om du vill ha instruktioner om hur du aktiverar målgruppssegment till det här målet.

## Exporterade data {#exported-data}

Adobe Target läser profildata från Adobe Experience Platform Edge Network så att inga data exporteras.

## Dataanvändning och styrning {#data-usage-governance}

Alla [!DNL Adobe Experience Platform] destinationerna är kompatibla med dataanvändningsprinciper när data hanteras. Detaljerad information om hur [!DNL Adobe Experience Platform] använder datastyrning, läs [Datastyrning - översikt](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html).
