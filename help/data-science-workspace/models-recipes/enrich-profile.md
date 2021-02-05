---
keywords: Experience Platform;maskininlärningsmodell;Data Science Workspace;Kundprofil i realtid;populära ämnen;maskininlärningsinsikter
solution: Experience Platform
title: Berika kundprofilen i realtid med insikt i maskininlärning
topic: tutorial
type: Tutorial
description: Det här dokumentet innehåller en guide om hur du kan förbättra kundprofilen i realtid med maskininlärningsinsikter.
translation-type: tm+mt
source-git-commit: 698639d6c2f7897f0eb4cce2a1f265a0f7bb57c9
workflow-type: tm+mt
source-wordcount: '640'
ht-degree: 0%

---


# Berika [!DNL Real-time Customer Profile] med maskininlärningsinsikter

Adobe Experience Platform [!DNL Data Science Workspace] innehåller verktyg och resurser för att skapa, utvärdera och använda maskininlärningsmodeller för att generera dataprognoser och insikter. När maskininlärningsinsikter hämtas in till en [!DNL Profile]-aktiverad datauppsättning, hämtas samma data även som [!DNL Profile]-poster som sedan kan segmenteras med [!DNL Adobe Experience Platform Segmentation Service]. När data från profil- och tidsserier hämtas bestämmer kundprofilen i realtid automatiskt att inkludera eller exkludera data från segment genom en pågående process som kallas direktuppspelningssegmentering, innan den sammanfogas med befintliga data och unionsvyn uppdateras. Resultatet blir att ni omedelbart kan utföra beräkningar och fatta beslut för att leverera förbättrade, individanpassade upplevelser till kunderna när de interagerar med ert varumärke.

Det här dokumentet innehåller länkar till självstudiekurser som gör att du kan förbättra [!DNL Real-time Customer Profile] med dina maskininlärningsuppgifter.

## Komma igång

För att kunna slutföra självstudiekurserna nedan måste du ha en fungerande förståelse för att hämta [!DNL Profile]-data och skapa segment. Innan du börjar med den här självstudiekursen bör du läsa dokumentationen för följande tjänster:

- [[!DNL Real-time Customer Profile]](../../profile/home.md): Ger en fullständig, enhetlig representation av varje enskild kund baserad på aggregerade data från flera källor.
- [[!DNL Identity Service]](../../identity-service/home.md): Möjliggör  [!DNL Real-time Customer Profile] genom att överbrygga identiteter från olika datakällor som importeras till Platform.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Det standardiserade ramverk som Platform använder för att organisera kundupplevelsedata.

Förutom de ovannämnda dokumenten rekommenderar vi att du även granskar följande handledningar för scheman och schemaläggningsprogrammet:

- [Grundläggande om schemakomposition](../../xdm/schema/composition.md): Beskriver XDM-scheman, byggstenar, principer och bästa praxis för dispositionsscheman som ska användas i  [!DNL Experience Platform].
- [Schemaredigeraren, genomgång](../../xdm/tutorials/create-schema-ui.md): Innehåller detaljerade anvisningar om hur du skapar scheman med Schemaredigeraren i  [!DNL Experience Platform].

## Skapa och konfigurera ett utdataschema och en datamängd {#create-an-output-schema-and-dataset}

Det första steget mot att berika [!DNL Real-time Customer Profile] med poängsättningsinsikter är att känna till vilket verkligt objekt (till exempel en person) som dina data definierar. Genom att förstå era data kan ni beskriva och utforma en struktur för att göra dem meningsfulla, ungefär som att utforma en relationsdatabas.

Dispositionen av ett schema börjar med att tilldela en klass. Klasser definierar de beteendeaspekter av data som schemat ska innehålla (post- eller tidsserie). Om du vill börja skapa egna scheman följer du stegen i självstudiekursen om att [skapa ett schema med Schemaredigeraren](../../xdm/tutorials/create-schema-ui.md). Observera, att innan du kan aktivera en datauppsättning för [!DNL Profile] måste du konfigurera datasetens schema så att det har ett primärt identitetsfält och sedan aktivera schemat för [!DNL Profile]. När data hämtas in till en [!DNL Profile]-aktiverad datauppsättning, hämtas samma data även som [!DNL Profile]-poster.

Om du hellre vill skapa ett schema med API:t [!DNL Schema Registry] börjar du med att läsa [[!DNL Schema Registry] utvecklarhandboken](../../xdm/api/getting-started.md) innan du försöker självstudiekursen om att [skapa ett schema med API](../../xdm/tutorials/create-schema-api.md).

När ditt schema och din datauppsättning har förberetts kan du generera och importera betygsdata till datauppsättningen genom att utföra betygskörningar med en lämplig modell.

## Skapa segment med [!DNL Segment Builder] {#create-segments-using-the-segment-builder}

När du har genererat och inhämtat dina poäng till din [!DNL Profile]-aktiverade datauppsättning kan du skapa dynamiska segment med [!DNL Segment Builder].

[!DNL Segment Builder] har en omfattande arbetsyta som du kan använda för att interagera med [!DNL Profile]-dataelement. Arbetsytan innehåller intuitiva kontroller för att skapa och redigera regler, till exempel dra-och-släpp-paneler som används för att representera dataegenskaper. Följ [[!DNL Segment Builder] användarhandboken](../../segmentation/ui/segment-builder.md) om du vill veta mer om:

- Skapa segmentdefinitioner med en kombination av attribut, händelser och befintliga målgrupper som byggstenar.
- Använda regelbyggarens arbetsyta och behållare för att styra i vilken ordning segmentreglerna körs.
- Visa uppskattningar av den potentiella målgruppen så att ni kan justera segmentdefinitionerna efter behov.
- Aktivera alla segmentdefinitioner för schemalagd segmentering.
- Aktiverar angivna segmentdefinitioner för direktuppspelningssegmentering.

## Nästa steg {#next-steps}

Mer information om segment och [!DNL Segment Builder] finns i [Översikt över segmenteringstjänsten](../../segmentation/home.md).

Läs [Översikt över kundprofilen i realtid](../../profile/home.md) om du vill veta mer om [!DNL Real-time Customer Profile]