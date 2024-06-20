---
solution: Experience Platform
title: Kända begränsningar och felsökning av problem med spelböcker
description: Läs mer om kända problem och vanliga problem med spelböcker och hur du felsöker dem
role: User, Developer, Admin
exl-id: 2604ce26-bcf9-46e1-bc10-30252a113159
source-git-commit: 0faf3187c0b32e0be70033e501939412ade37d7e
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 0%

---


# Felsökning {#troubleshooting}

Visa felsökningsförslag för vanliga fel när du arbetar med Use Case Playbooks

## Adobe Journey Optimizer-ytor har inte konfigurerats {#surfaces-not-configured}

När du skapar en instans av en spelningsbok kan du se meddelandet nedan.

![Felsökning](/help/use-case-playbooks/assets/playbooks/troubleshooting/troubleshooting-ajo.png)

Detta beror på att Journey Optimizer spelböcker skapar meddelanden för e-post-, push- och SMS-kanaler. Läs [komma igång](/help/use-case-playbooks/playbooks/get-started.md#configure-sandbox-and-channel-surfaces-in-journey-optimizer) för att konfigurera olika ytor.

## Status *misslyckades* när en ny instans skapas {#status-failed}

Om ett felmeddelande visas när du försöker skapa en instans kan det bero på att administratören inte har gett dig de användarbehörigheter som krävs. En spelningsbok innehåller många olika resurser och din användare behöver behörighet att skapa dessa resurser för att kunna skapa instansen av spelboken. Se [behörigheter](/help/use-case-playbooks/playbooks/get-started.md#grant-your-team-the-required-access-permissions) i den här handboken om hur du ställer in behörigheter.

## Importen misslyckades {#import-failure}

Kunderna arbetar i olika testmiljöer och ibland kan det misslyckas om en instans importeras från sin miljö till sandlådan Adobe. Om du vill visa status för dessa importer väljer du Sandlåda i den vänstra navigeringen och väljer sedan Jobb. Här kan du se all information om de importerade filerna. Välj en fil med en misslyckad status och välj sedan Visa jobbinformation. En modal visas. Välj Visa JSON-fil och rulla nedåt och kopiera felmeddelandet som visas under&quot;meddelanden&quot;. Det är helt möjligt att flera felmeddelanden visas, så se till att kopiera alla. Skicka dem till ditt Adobe team medan du försöker logga en buggbiljett. Detta snabbar upp lösningsprocessen och ger teamet mer kontext om vad som händer.
