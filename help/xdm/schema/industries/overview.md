---
solution: Experience Platform
title: Översikt över branschdatamodeller
topic-legacy: overview
description: Lär dig mer om standardiserade datamodeller för olika vertikala branscher som kan konstrueras med XDM-komponenter (Standard Experience Data Model).
exl-id: 8fa9a610-36b5-470f-ad63-f2a4a060e0f1
source-git-commit: d3f914cb4bcd18980e433c6fd17a663ad0fb5a84
workflow-type: tm+mt
source-wordcount: '347'
ht-degree: 0%

---

# Översikt över branschdatamodeller

Med Experience Data Model (XDM) kan ni skapa anpassningsbara scheman för att hämta viktiga kundupplevelsedata som är relaterade till ert företag. För att effektivisera processen med att modellera data så att de överensstämmer med XDM erbjuder Adobe Experience Platform en mångsidig uppsättning XDM-standardkomponenter, som samlar in koncept som ofta används i olika branscher.

>[!NOTE]
>
>Nya standard-XDM-komponenter släpps kontinuerligt för att passa konsumenternas behov. Om du vill se en lista över de senaste komponenterna kan du [utforska befintliga resurser i användargränssnittet](../../ui/explore.md) eller referera till [officiell XDM-databas](https://github.com/adobe/xdm/tree/master/components) på GitHub.

Beroende på vilken bransch som ert företag är verksam inom är vissa XDM-komponenter mer relevanta för era behov än andra. Dessutom varierar relationerna mellan XDM-scheman beroende på vilken bransch du arbetar i.

För att hjälpa er att vägleda er datamodelleringsstrategi baserat på just er bransch ger den här guiden en referens till ERD-diagram (Entity relationship chart) för flera vertikaler som stöds i branschen.

## Förutsättningar

För att kunna läsa de referensdokument för elektroniska avhandlingar som det hänvisas till i den här handboken måste du ha en fungerande förståelse för hur XDM-komponenterna interagerar med formulärscheman och hur XDM-scheman fungerar i Experience Platform som helhet. Kontrollera att du har läst följande översiktsdokumentation innan du fortsätter:

* [XDM - systemöversikt](../../home.md): Lär dig hur XDM fungerar i plattformens ekosystem.
* [Grunderna för schemakomposition](../../schema/composition.md): Lär dig hur XDM-komponenter (till exempel schemafältgrupper, klasser och datatyper) bidrar till strukturen i ett schema samt identitetsfältens roll.

Vi rekommenderar att du granskar [guide till bästa praxis för datamodellering](../../schema/best-practices.md) för allmänna riktlinjer om hur du mappar data till XDM.

## ERD för branschdatamodell {#erds}

ERD tillhandahålls för följande vertikala branscher:

* [[!UICONTROL Retail]](./retail.md)
* [[!UICONTROL Financial services]](./financial.md)
* [[!UICONTROL Healthcare]](./healthcare.md)
* [[!UICONTROL Telecommunications]](./telecom.md)
* [[!UICONTROL Travel and hospitality]](./travel-hospitality.md)

## Nästa steg

I det här dokumentet finns en översikt över de elektroniska avhandlingar som finns i branschdatamodellen och hur de ska tolkas. Om du vill visa en ERD-fil väljer du en i listan ovan.
