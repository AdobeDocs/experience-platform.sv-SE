---
solution: Experience Platform
title: Översikt över branschdatamodeller
topic: overview
description: Lär dig mer om standardiserade datamodeller för olika vertikala branscher som kan konstrueras med XDM-komponenter (Standard Experience Data Model).
translation-type: tm+mt
source-git-commit: 9862cbcb8d8c74c96dd6bf44c5fa416f4f42fe64
workflow-type: tm+mt
source-wordcount: '512'
ht-degree: 0%

---


# Översikt över branschdatamodeller

Med Experience Data Model (XDM) kan ni skapa anpassningsbara scheman för att hämta viktiga kundupplevelsedata som är relaterade till ert företag. För att effektivisera processen med att modellera data så att de överensstämmer med XDM erbjuder Adobe Experience Platform en mångsidig uppsättning XDM-standardkomponenter, som samlar in koncept som ofta används i olika branscher.

>[!NOTE]
>
>Nya standard-XDM-komponenter släpps kontinuerligt för att passa konsumenternas behov. Om du vill se en lista över de senaste komponenterna kan du [utforska befintliga resurser i användargränssnittet](../../ui/explore.md) eller hänvisa till [den officiella XDM-databasen](https://github.com/adobe/xdm/tree/master/components) på GitHub.

Beroende på vilken bransch som ert företag är verksam inom är vissa XDM-komponenter mer relevanta för era behov än andra. Dessutom varierar relationerna mellan XDM-scheman beroende på vilken bransch du arbetar i.

För att hjälpa er att vägleda er datamodelleringsstrategi baserat på just er bransch ger den här guiden en referens till ERD-diagram (Entity relationship chart) för flera vertikaler som stöds i branschen.

## Förutsättningar

För att kunna läsa de referensdokument för elektroniska avhandlingar som det hänvisas till i den här handboken måste du ha en fungerande förståelse för hur XDM-komponenterna interagerar med formulärscheman och hur XDM-scheman fungerar i Experience Platform som helhet. Kontrollera att du har läst följande översiktsdokumentation innan du fortsätter:

* [XDM - systemöversikt](../../home.md): Lär dig hur XDM fungerar i plattformens ekosystem.
* [Grundläggande om schemakomposition](../../schema/composition.md): Lär dig hur XDM-komponenter (till exempel mixiner, klasser och datatyper) bidrar till strukturen i ett schema samt rollen för identitetsfält.

Vi rekommenderar även att du läser [handboken om bästa praxis för datamodellering](../../schema/best-practices.md) för allmänna riktlinjer om hur du mappar data till XDM.

## Branschdatamodell:er {#erds}

De vertikala modeller i branschen som representeras av de elektroniska avhandlingar som beskrivs nedan skapas avsiktligt på ett avnormaliserat sätt och med hänsyn till hur data lagras i Platform.

För en given ERD baseras varje enhet som visas i på en underliggande XDM-klass. För en given entitet representerar varje rad som är markerad med **fet** en blandning eller en datatyp, med de relevanta fält som anges nedan i oförändrad text. De viktigaste fälten för en viss enhet markeras med rött.

>[!NOTE]
>
>Vissa entiteter kan innehålla ett &quot;_ID&quot;-fält. Detta representerar den unika identifierare (`_id`) som plattformen automatiskt tilldelar till händelse- eller profilobjekt när de hämtas. Du kan dock välja att använda dina egna unika ID-värden för det här fältet om du vill.

Alla egenskaper som kan användas för att identifiera enskilda kunder markeras som&quot;identitet&quot;, med en av dessa egenskaper markerad som&quot;primär identitet&quot;.

Enhetsrelationer markeras som icke-beroende eftersom cookie-baserade händelser ofta inte kan avgöra vem eller vilka personer som gjorde transaktionen.

ERD tillhandahålls för följande vertikala branscher:

* [[!UICONTROL Retail]](./retail.md)
* [[!UICONTROL Financial services]](./financial.md)
* [[!UICONTROL Travel and hospitality]](./travel-hospitality.md)

## Nästa steg

I det här dokumentet finns en översikt över de elektroniska avhandlingar som finns i branschdatamodellen och hur de ska tolkas. Om du vill visa en ERD-fil väljer du en i listan ovan.