---
solution: Experience Platform
title: Adobe Experience Platform multi-cloud - översikt
description: Lär dig vad skillnaden är mellan att köra Experience Platform på Microsoft Azure och Amazon Web Services.
source-git-commit: d3654573cec338f173d151fd5e62ef5c8b893c11
workflow-type: tm+mt
source-wordcount: '560'
ht-degree: 1%

---


# Adobe Experience Platform multi-cloud - översikt

Adobe Experience Platform är en produkt med flera moln som ger dig möjlighet att välja mellan att köra [[!DNL Microsoft Azure]](https://azure.microsoft.com/en-us) eller [[!DNL Amazon Web Services (AWS)]](https://aws.amazon.com/). Tack vare den här flexibiliteten kan du välja den som passar bäst för dina affärs- och tekniska behov.

>[!AVAILABILITY]
>
>Adobe Experience Platform som körs på Amazon Web Services (AWS) är för närvarande tillgängligt för ett begränsat antal kunder. Om du vill veta mer om Experience Platform på AWS kontaktar du kontoteamet för Adobe.

Den här sidan ger en översikt på hög nivå över de två tillgängliga molninfrastrukturerna och innehåller vägledning om hur du väljer rätt infrastruktur för ditt företag.

## Vilken molnimplementering passar mig? {#which-cloud-is-right}

Om du väljer mellan Experience Platform på Azure eller AWS beror på flera faktorer som är specifika för ditt företag:

* **Affärsbehov och tekniska behov**: Utvärdera organisationens krav och den långsiktiga molnstrategin.
* **Befintlig infrastruktur**: Ta hänsyn till din nuvarande molninfrastruktur och dina integreringsbehov.
* **Cloud-teknikberoende**: Om ditt företag är starkt beroende av Microsoft-tekniker kanske Azure passar bättre. Om du litar mer på Amazon tjänster kan AWS vara det bättre alternativet.
* **Överväganden om datastorlek**: Utvärdera kraven på datastorlek för din organisation och se till att den valda molnplattformen erbjuder regioner som uppfyller dessa regler.

Med tanke på ovanstående faktorer kan du använda det här förenklade beslutsträdet för att avgöra vilken molnimplementering som passar ditt företags behov.

![Bild som visar geografisk fördelning av värdplatser.](assets/multi-cloud/diagram-cloud.png){align="center" zoomable="yes"}

## Värdplatser {#available-cloud-regions}

Det är viktigt att du väljer rätt molnregion för att kunna uppfylla kraven på dataresistens och säkerställa optimala prestanda.

![Bild som visar geografisk fördelning av värdplatser.](assets/multi-cloud/hosting-locations-map.png){align="center" zoomable="yes"}

Experience Platform finns på sex Microsoft Azure-värdplatser, en Amazon Web Services-värdplats (AWS) och skickar data till Adobe-tjänster via sju [Edge Network-noder](../collection/home.md#edge) som distribueras över hela världen.

### Microsoft Azure-regioner {#azure-regions}

Tabellen nedan anger de Microsoft Azure-regioner där Experience Platform är värd.

| Land | Regionkod | Plats |
|---------|-------------|----------|
| Amerikas förenta stater | VA7 | Virginia |
| Förenade kungariket | GBR9 | London |
| Nederländerna | NDL2 | Amsterdam |
| Kanada | CAN2 | Toronto |
| Indien | IND2 | Maharashtra |
| Australien | AUS5 | New South Wales |

{style="table-layout:auto"}

### Amazon Web Services (AWS) {#aws-regions}

Tabellen nedan visar de AWS-regioner där Experience Platform är värd. Kontrollera regelbundet för att se om fler platser har lagts till.

| Land | Regionkod | Plats |
|---------|-------------|----------|
| Amerikas förenta stater | VA6 | Virginia |

{style="table-layout:auto"}

## Funktionsparitet {#feature-parity}

Adobe strävar efter att erbjuda funktionsparitet över olika molnplattformar för alla program som körs på Experience Platform, till exempel:

* [Plattform för kunddata i realtid](../rtcdp/home.md)
* [Adobe Journey Optimizer](https://experienceleague.adobe.com/sv/docs/journey-optimizer/using/ajo-home)
* [Customer Journey Analytics](https://experienceleague.adobe.com/sv/docs/analytics-platform/using/cja-landing)

Vissa funktioner kan dock skilja sig åt mellan Azure- och AWS-implementeringar. Dessa skillnader beskrivs i avsnittet nedan och i andra delar av produktdokumentationen, där så är tillämpligt.

### Skillnader mellan att köra Experience Platform på Microsoft Azure och AWS {#azure-aws-differences}

Tabellen nedan visar de största skillnaderna mellan att köra Experience Platform på Microsoft Azure och AWS.

| Funktion/Funktioner | Microsoft Azure | Amazon Web Services |
| --- | --- | --- |
| [HIPAA-kompatibilitet](https://www.adobe.com/trust/compliance/hipaa-ready.html) | Stöds | Stöds inte |
| [Katalog över källanslutningar](/help/sources/home.md) | Alla kopplingar i källkatalogen stöds | Ett begränsat antal källanslutningar är tillgängliga. Alla källkopplingar som är tillgängliga för AWS-implementeringar anropas i ett meddelande på den översta sidan på deras respektive dokumentationssidor. |

{style="table-layout:auto"}

<!-- To be determined if we need to add this part about the AI Assistant 

| [Experience Platform AI Assistant](/help/ai-assistant/home.md) | Supported | Not supported |

-->

## Slutsats {#conclusion}

Experience Platform erbjuder flexibilitet och valmöjligheter genom att ge dig möjlighet att köra på Microsoft Azure eller Amazon Web Services. Utvärdera era affärsbehov och befintlig infrastruktur för att fatta ett välgrundat beslut om vilken molnplattform ni ska använda.
