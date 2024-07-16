---
solution: Experience Platform
title: Kända begränsningar för spelböcker
description: Läs mer om kända problem och vanliga problem med spelböcker och hur du felsöker dem
role: User, Developer, Admin
exl-id: 2604ce26-bcf9-46e1-bc10-30252a113159
source-git-commit: e24334bb4ac788770abe20ec2324efa1e64bc0e8
workflow-type: tm+mt
source-wordcount: '255'
ht-degree: 0%

---


# Kända begränsningar {#known-limitations}

Lär dig felsöka när du arbetar med Use Case Playbooks och förstå de kända begränsningarna i den allmänna tillgänglighetsreleasen.

## Kända begränsningar

Ett par kända begränsningar visas när du skapar en instans av en spelbok och genererar resurser.

* Om ett schema genereras i en instans av en spelningsbok och du redigerar det för genererade scheman, genereras inte *ett annat schema* om du aktiverar en annan instans av spelningsboken. Fortsätt i stället att använda det schema som du redigerade i instansen också.

* När du använder [dataidentifieringsfunktionen](/help/use-case-playbooks/playbooks/data-awareness.md) för att befordra schemat från den inspirerande sandlådan till utvecklingssandlådan kan du se några fel som liknar dem nedan:

![Fel som visas i arbetsflödet för schemamappning.](/help/use-case-playbooks/assets/playbooks/troubleshooting/schema-errors.png){width="1000" zoomable="yes"}

Detta beror på att vissa fält som genereras från ditt schema inte finns i schemat i den utvecklingssandlåda som du kopierar till. Se vad fälten är. Gå sedan tillbaka till utvecklingssandlådan där du kan:

* Skapa antingen en ny fältgrupp som innehåller dessa fält eller
* Inkludera en fördefinierad standardfältgrupp som innehåller de fält som saknas i schemat.

När du har inkluderat dessa fält i schemat i utvecklingssandlådan går du tillbaka till arbetsflödet och kopierar schemafälten från inspirationssandlådan till utvecklingssandlådan. Felen är nu borta.

Titta på videon nedan för att skapa schemafältgrupper om du vill ha mer information.

>[!VIDEO](https://video.tv.adobe.com/v/27013/?learn=on)
