---
keywords: Experience Platform;maskininlärningsmodell;Data Science Workspace;Kundprofil i realtid;populära ämnen;maskininlärningsinsikter
solution: Experience Platform
title: Berika kundprofilen i realtid med insikt i maskininlärning
type: Tutorial
description: Det här dokumentet innehåller en guide om hur du kan förbättra kundprofilen i realtid med maskininlärningsinsikter.
exl-id: 397023c9-383d-4a21-b58a-0f920631ac56
source-git-commit: afa27069c7490848398c92973dd77810564b5993
workflow-type: tm+mt
source-wordcount: '630'
ht-degree: 0%

---

# Berika [!DNL Real-Time Customer Profile] med maskininlärningsinsikter

Adobe Experience Platform [!DNL Data Science Workspace] innehåller verktyg och resurser för att skapa, utvärdera och använda maskininlärningsmodeller för att generera dataprognoser och insikter. När maskininlärningsinsikter hämtas in till en [!DNL Profile]-aktiverad datauppsättning, hämtas samma data även som [!DNL Profile]-poster som sedan kan segmenteras med [!DNL Adobe Experience Platform Segmentation Service].

Segmenteringsprocessen beror på vilken metod publiken använder. Om en målgrupp har konfigurerats som **direktuppspelning** bearbetas alla nya uppdateringar som skrivits av modellen till profilen i realtid. Om en målgrupp har konfigurerats för **batch**-utvärdering utvärderas dock de nya värdena i nästa grupp.

Det här dokumentet innehåller länkar till självstudiekurser som gör att du kan förbättra [!DNL Real-Time Customer Profile] med dina maskininlärningsinsikter.

## Komma igång

För att kunna slutföra självstudiekurserna nedan måste du ha en fungerande förståelse för att importera [!DNL Profile]-data och skapa målgrupper. Innan du börjar med den här självstudiekursen bör du läsa dokumentationen för följande tjänster:

- [[!DNL Real-Time Customer Profile]](../../profile/home.md): Tillhandahåller en fullständig, enhetlig representation av varje enskild kund baserat på aggregerade data från flera källor.
- [[!DNL Identity Service]](../../identity-service/home.md): Aktiverar [!DNL Real-Time Customer Profile] genom att brygga identiteter från olika datakällor som hämtas till plattformen.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Det standardiserade ramverk som Platform använder för att organisera kundupplevelsedata.

Förutom de ovannämnda dokumenten rekommenderar vi att du även granskar följande handböcker om scheman och schemaläggningsprogrammet:

- [Grundläggande om schemakomposition](../../xdm/schema/composition.md): Beskriver XDM-scheman, byggstenar, principer och bästa tillvägagångssätt för att komponera scheman som ska användas i [!DNL Experience Platform].
- [Schemaredigeraren, självstudiekurs](../../xdm/tutorials/create-schema-ui.md): Tillhandahåller detaljerade anvisningar för hur du skapar scheman med Schemaredigeraren i [!DNL Experience Platform].

## Skapa och konfigurera ett utdataschema och en datauppsättning {#create-an-output-schema-and-dataset}

Det första steget mot att berika [!DNL Real-Time Customer Profile] med poängsättningsinsikter är att känna till vilket objekt i verkligheten (till exempel en person) som dina data definierar. Genom att förstå era data kan ni beskriva och utforma en struktur för att göra dem meningsfulla, ungefär som att utforma en relationsdatabas.

Dispositionen av ett schema börjar med att tilldela en klass. Klasser definierar de beteendeaspekter av data som schemat ska innehålla (post- eller tidsserie). Om du vill börja skapa egna scheman följer du stegen i självstudiekursen om hur du [skapar ett schema med Schemaredigeraren](../../xdm/tutorials/create-schema-ui.md). Observera, att innan du kan aktivera en datauppsättning för [!DNL Profile] måste du konfigurera datasetens schema så att det har ett primärt identitetsfält och sedan aktivera schemat för [!DNL Profile]. När data hämtas in till en [!DNL Profile]-aktiverad datauppsättning, hämtas samma data även som [!DNL Profile]-poster.

Om du hellre vill skapa ett schema med [!DNL Schema Registry] API:t börjar du med att läsa [[!DNL Schema Registry] utvecklarhandboken](../../xdm/api/getting-started.md) innan du försöker med självstudiekursen om hur du [skapar ett schema med API:t](../../xdm/tutorials/create-schema-api.md).

När ditt schema och din datauppsättning har förberetts kan du generera och importera betygsdata till datauppsättningen genom att utföra betygskörningar med en lämplig modell.

## Skapa målgrupper med [!DNL Segment Builder] {#create-audiences-using-the-segment-builder}

När du har genererat och inhämtat dina poäng till din [!DNL Profile]-aktiverade datauppsättning kan du skapa dynamiska målgrupper med [!DNL Segment Builder].

[!DNL Segment Builder] innehåller en omfattande arbetsyta som du kan använda för att interagera med [!DNL Profile]-dataelement. Arbetsytan innehåller intuitiva kontroller för att skapa och redigera regler, till exempel dra-och-släpp-paneler som används för att representera dataegenskaper. Följ [[!DNL Segment Builder] användarhandboken](../../segmentation/ui/segment-builder.md) om du vill veta mer om:

- Skapa segmentdefinitioner med en kombination av attribut, händelser och befintliga målgrupper som byggstenar.
- Använda regelbyggarens arbetsyta och behållare för att styra i vilken ordning målgruppsregler körs.
- Visa uppskattningar av den potentiella målgruppen, så att ni kan justera segmentdefinitionerna efter behov.
- Aktivera alla segmentdefinitioner för schemalagd segmentering.
- Aktivera angivna segmentdefinitioner för direktuppspelningssegmentering.

## Nästa steg {#next-steps}

Läs [Översikt över segmenteringstjänsten](../../segmentation/home.md) om du vill veta mer om målgrupper och [!DNL Segment Builder].

Mer information om [!DNL Real-Time Customer Profile] finns i [Översikt över kundprofiler i realtid](../../profile/home.md)
