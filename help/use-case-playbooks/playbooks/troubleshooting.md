---
solution: Experience Platform
title: Kända begränsningar och felsökning av problem med spelböcker
description: Läs mer om kända problem och vanliga problem med spelböcker och hur du felsöker dem
role: User, Developer, Admin
exl-id: 2604ce26-bcf9-46e1-bc10-30252a113159
source-git-commit: ecce42e2c759bda31bc37d0aae1da2c7b3d141fc
workflow-type: tm+mt
source-wordcount: '395'
ht-degree: 0%

---


# Felsökning och kända begränsningar {#troubleshooting-known-limitations}

Lär dig felsöka när du arbetar med Use Case Playbooks och förstå de kända begränsningarna i den allmänna tillgänglighetsreleasen.

## Felsökning {#troubleshooting}

Visa felsökningsförslag för vanliga fel när du arbetar med Use Case Playbooks

### Adobe Journey Optimizer-ytor har inte konfigurerats

När du skapar en instans av en spelningsbok kan du se meddelandet nedan.

![Felsökning](/help/use-case-playbooks/assets/playbooks/troubleshooting/troubleshooting-ajo.png)

Detta beror på att Journey Optimizer spelböcker skapar meddelanden för e-post-, push- och SMS-kanaler. Läs [komma igång](/help/use-case-playbooks/playbooks/get-started.md#configure-sandbox-and-channel-surfaces-in-journey-optimizer) för att konfigurera olika ytor.

### Status *misslyckades* när en ny instans skapas

Om ett felmeddelande visas när du försöker skapa en instans kan det bero på att administratören inte har gett dig de användarbehörigheter som krävs. En spelningsbok innehåller många olika resurser och din användare behöver behörighet att skapa dessa resurser för att kunna skapa instansen av spelboken. Se [behörigheter](/help/use-case-playbooks/playbooks/get-started.md#grant-your-team-the-required-access-permissions) i den här handboken om hur du ställer in behörigheter.

## Kända begränsningar

Ett par kända begränsningar visas när du skapar en instans av en spelbok och genererar resurser.

* Om ett schema genereras i en instans av en spelningsbok och du redigerar det för genererade scheman, kommer ett annat schema *inte* genereras om du aktiverar en annan instans av spelboken. Fortsätt i stället att använda det schema som du redigerade i instansen också.

* När du använder [funktioner för datainlärning](/help/use-case-playbooks/playbooks/data-awareness.md) om du vill befordra schemat från den inspirerande sandlådan till utvecklingssandlådan kan du se några fel som liknar dem nedan:

![Fel som visas i arbetsflödet för schemamappning.](/help/use-case-playbooks/assets/playbooks/troubleshooting/schema-errors.png){width="1000" zoomable="yes"}

Detta beror på att vissa fält som genereras från ditt schema inte finns i schemat i den utvecklingssandlåda som du kopierar till. Se vad fälten är. Gå sedan tillbaka till utvecklingssandlådan där du kan:

* Skapa antingen en ny fältgrupp som innehåller dessa fält eller
* Inkludera en fördefinierad standardfältgrupp som innehåller de fält som saknas i schemat.

När du har inkluderat dessa fält i schemat i utvecklingssandlådan går du tillbaka till arbetsflödet och kopierar schemafälten från inspirationssandlådan till utvecklingssandlådan. Felen är nu borta.

Titta på videon nedan för att skapa schemafältgrupper om du vill ha mer information.

>[!VIDEO](https://video.tv.adobe.com/v/27013/?learn=on)
