---
keywords: Experience Platform;maskininlärningsmodell;Data Science Workspace;Kundprofil i realtid;populära ämnen;maskininlärningsinsikter
solution: Experience Platform
title: Berika kundprofilen i realtid med insikt i maskininlärning
topic-legacy: tutorial
type: Tutorial
description: Det här dokumentet innehåller en guide om hur du kan förbättra kundprofilen i realtid med maskininlärningsinsikter.
exl-id: 397023c9-383d-4a21-b58a-0f920631ac56
source-git-commit: 89a9b64f2fb238c08a281f29a035ce0b24b34804
workflow-type: tm+mt
source-wordcount: '577'
ht-degree: 0%

---

# Förfina [!DNL Real-time Customer Profile] med maskininlärningsinsikter

Adobe Experience Platform [!DNL Data Science Workspace] innehåller verktyg och resurser för att skapa, utvärdera och använda maskininlärningsmodeller för att generera dataprognoser och insikter. När maskininlärningsinsikter hämtas till en [!DNL Profile]-aktiverad datauppsättning, att samma data också hämtas som [!DNL Profile] poster som sedan kan segmenteras med [!DNL Adobe Experience Platform Segmentation Service].

Det här dokumentet innehåller länkar till självstudiekurser som gör att du kan utöka [!DNL Real-time Customer Profile] med inlärningsinsikter om din dator.

## Komma igång

För att kunna slutföra självstudiekurserna nedan måste du ha en fungerande förståelse för att kunna importera [!DNL Profile] data och skapa segment. Innan du börjar med den här självstudiekursen bör du läsa dokumentationen för följande tjänster:

- [[!DNL Real-time Customer Profile]](../../profile/home.md): Ger en fullständig, enhetlig representation av varje enskild kund baserad på aggregerade data från flera källor.
- [[!DNL Identity Service]](../../identity-service/home.md): Aktiverar [!DNL Real-time Customer Profile] genom att överbrygga identiteter från olika datakällor som hämtas in till Platform.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Det standardiserade ramverk som Platform använder för att organisera kundupplevelsedata.

Förutom de ovannämnda dokumenten rekommenderar vi att du även granskar följande handledningar för scheman och schemaläggningsprogrammet:

- [Grunderna för schemakomposition](../../xdm/schema/composition.md): Beskriver XDM-scheman, byggstenar, principer och bästa praxis för dispositionsscheman som ska användas i [!DNL Experience Platform].
- [Schemaredigeraren, genomgång](../../xdm/tutorials/create-schema-ui.md): Innehåller detaljerade anvisningar om hur du skapar scheman med Schemaredigeraren i [!DNL Experience Platform].

## Skapa och konfigurera ett utdataschema och en datauppsättning {#create-an-output-schema-and-dataset}

Det första steget mot berikning [!DNL Real-time Customer Profile] med insikt i poängsättningen är att veta vilket objekt i verkligheten (till exempel en person) era data definierar. Genom att förstå era data kan ni beskriva och utforma en struktur för att göra dem meningsfulla, ungefär som att utforma en relationsdatabas.

Dispositionen av ett schema börjar med att tilldela en klass. Klasser definierar de beteendeaspekter av data som schemat ska innehålla (post- eller tidsserie). Om du vill börja skapa egna scheman följer du instruktionerna i självstudiekursen om [skapa ett schema med Schemaredigeraren](../../xdm/tutorials/create-schema-ui.md). Observera att innan du kan aktivera en datauppsättning för [!DNL Profile]måste du konfigurera datauppsättningens schema så att det har ett primärt identitetsfält och sedan aktivera schemat för [!DNL Profile]. När data hämtas till en [!DNL Profile]-aktiverad datauppsättning, att samma data också hämtas som [!DNL Profile] poster.

Om du föredrar att skapa ett schema med [!DNL Schema Registry] API:t börjar i stället med att läsa [[!DNL Schema Registry] utvecklarhandbok](../../xdm/api/getting-started.md) innan du provar självstudiekursen på [skapa ett schema med API](../../xdm/tutorials/create-schema-api.md).

När ditt schema och din datauppsättning har förberetts kan du generera och importera betygsdata till datauppsättningen genom att utföra betygskörningar med en lämplig modell.

## Skapa segment med [!DNL Segment Builder] {#create-segments-using-the-segment-builder}

När du har genererat och inhämtat dina poäng till din [!DNL Profile]-aktiverad datauppsättning, kan du skapa dynamiska segment med [!DNL Segment Builder].

The [!DNL Segment Builder] innehåller en omfattande arbetsyta som du kan använda för att interagera med [!DNL Profile] dataelement. Arbetsytan innehåller intuitiva kontroller för att skapa och redigera regler, till exempel dra-och-släpp-paneler som används för att representera dataegenskaper. Följ [[!DNL Segment Builder] användarhandbok](../../segmentation/ui/segment-builder.md) om du vill veta mer om:

- Skapa segmentdefinitioner med en kombination av attribut, händelser och befintliga målgrupper som byggstenar.
- Använda regelbyggarens arbetsyta och behållare för att styra i vilken ordning segmentreglerna körs.
- Visa uppskattningar av den potentiella målgruppen så att ni kan justera segmentdefinitionerna efter behov.
- Aktivera alla segmentdefinitioner för schemalagd segmentering.
- Aktiverar angivna segmentdefinitioner för direktuppspelningssegmentering.

## Nästa steg {#next-steps}

Mer information om segment och [!DNL Segment Builder], läsa [Översikt över segmenteringstjänsten](../../segmentation/home.md).

Mer information om [!DNL Real-time Customer Profile], läsa [Översikt över kundprofiler i realtid](../../profile/home.md)
