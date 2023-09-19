---
keywords: Experience Platform;utvecklarguide;Data Science Workspace;populära topics;Real time Machine Learning;
solution: Experience Platform
title: Machine Learning-översikt i realtid
description: Maskininlärning i realtid kan dramatiskt öka relevansen i ert innehåll för digitala upplevelser för era slutanvändare. Detta är möjligt genom att utnyttja realtidsinterferenser och kontinuerlig inlärning i Experience Platform Edge-nätverket.
exl-id: 23eb1877-1bdf-4982-b58c-cfb58467035a
source-git-commit: 3272db15283d427eb4741708dffeb8141f61d5ff
workflow-type: tm+mt
source-wordcount: '550'
ht-degree: 1%

---

# Maskininlärningsöversikt i realtid (alfa)

>[!IMPORTANT]
>
>Maskininlärning i realtid är inte tillgängligt för alla användare ännu. Den här funktionen är alfabet och testas fortfarande. Dokumentet kan komma att ändras.

Maskininlärning i realtid kan dramatiskt öka relevansen i ert innehåll för digitala upplevelser för era slutanvändare. Detta blir möjligt genom att man utnyttjar realtidskonferenser och kontinuerlig inlärning på [!DNL Experience Platform Edge Network].

En kombination av sömlös beräkning på både hubben och [!DNL Edge] minskar dramatiskt den latens som traditionellt används för att skapa personaliserade upplevelser som är både relevanta och responsiva. Maskininlärning i realtid ger därmed en otroligt låg latens för synkront beslutsfattande. Exempel på detta är återgivning av anpassat webbsidesinnehåll eller visning av ett erbjudande eller en rabatt för att minska bortfallet och öka antalet konverteringar i en webbutik.

## Maskininlärningsarkitektur i realtid {#architecture}

I följande diagram finns en översikt över maskininlärningsarkitekturen i realtid. För närvarande har alfa en mer förenklad version.

![alfagra](../images/rtml/alpha-arch.png)

![Förenklad översikt](../images/rtml/end-to-end-arch.png)

## Arbetsflöde för maskininlärning i realtid

I följande arbetsflöde beskrivs de vanliga stegen och resultaten för att skapa och använda en Machine Learning-modell i realtid.

### Intag av data och preparat

Data importeras och omvandlas med [!DNL Experience Data Model] (XDM) på Adobe Experience Platform. Dessa data används för modellutbildning. Mer information om XDM finns på [XDM - översikt](../../xdm/home.md).

### Redigering

Skapa en maskininlärningsmodell i realtid genom att skapa den från grunden eller ta in den som en förutbildad serialiserad ONNX-modell i Adobe Experience Platform Jupyter Notebooks.

### Distribution

Distribuera din modell till [!DNL Edge Network] för att skapa en Machine Learning-tjänst i realtid i [!UICONTROL Service Gallery] med API-slutpunkten för förutsägelse.

### Inledning

Använd REST API-slutpunkten för förutsägelse för att generera maskininlärningsinsikter i realtid.

### Leverans

Marknadsförarna kan sedan definiera segment och regler som mappar Machine Learning-resultat i realtid till upplevelser med Adobe Target. På så sätt kan besökare på ert varumärkes webbplats i realtid få en hyper-personaliserad upplevelse på samma eller nästa sida.

## Aktuell funktionalitet

Maskininlärning i realtid är för närvarande alfavärdet. Funktionerna som beskrivs nedan kan ändras när fler funktioner och noder blir tillgängliga.

>[!NOTE]
>
> Alfabegränsningar:
> - För närvarande stöds endast ONNX-baserade modeller.
> - Funktioner som används i noder kan inte serialiseras. En lambda-funktion används till exempel i en Pandarod.
> - Det finns en 20-sekunders sömn efter [!DNL Edge] distributionen görs manuellt.
> - För djupgående inlärning måste data skickas på ett sådant sätt att när `df.values` anropas och returnerar en array som accepteras av DL-modellen. Detta beror på att ONNX-modellens poängnod använder `df.values` och skickar utdata som ska poängsättas mot modellen.


### Funktioner:

| | Alfa (maj) |
| --- | --- |
| **Funktioner** | - Med RTML-mallen för bärbara datorer kan du skapa, testa och distribuera en anpassad maskininlärningsmodell. <br> - Import av förutbildade maskininlärningsmodeller. <br> - Machine Learning SDK i realtid. <br> - Startuppsättning med redigeringsnoder. <br> - Distribueras till Adobe Experience Platform Hub. |
| **Tillgänglighet** | Nordamerika |
| **Redigeringsnoder** | - Pandor <br> - ScikitLearn <br> - ONNXNode <br> - Dela <br> - ModelUpload <br> - OneHotEncoder |
| **Körtider för poäng** | ONNX |

## Nästa steg

Du kan börja med att följa [komma igång](./getting-started.md) guide. I den här guiden får du hjälp med att konfigurera alla nödvändiga förutsättningar för att skapa en maskininlärningsmodell i realtid.
