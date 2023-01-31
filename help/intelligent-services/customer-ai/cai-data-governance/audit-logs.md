---
keywords: insikter;customer ai;customer ai insights;CAI query service;customer ai queries;customer ai scores
feature: Customer AI audit logs
title: Översikt över granskningsloggar
description: Lär dig hur du visar och hanterar granskningsloggar i kundens AI.
source-git-commit: 3b1cc7ca710071df9de06428f7eed2993219ae1a
workflow-type: tm+mt
source-wordcount: '276'
ht-degree: 0%

---

# Granskningsloggar

För att öka insynen i och synligheten för aktiviteter som utförs i systemet, hämtas användaraktivitet i kundens AI-arbetsflöde nu in i granskningsloggar för att förstå användardrivna ändringar i kundens AI-modeller. Loggarna utgör en verifieringskedja som kan hjälpa till med felsökningsproblem och hjälper ditt företag att effektivt följa företagets policyer för datahantering och lagstadgade krav.  Om ni omfattas av HIPAA (Health Insurance Portability and Accounability Act) och skapar, tar emot, underhåller eller överför tillåtna känsliga personuppgifter via Attribution AI eller kundens AI är ni ansvariga för att genomföra en BAA med Adobe och licensiera vårdsköld.

I grundläggande bemärkelse anger en granskningslogg vem som utförde vilken åtgärd och när. Varje åtgärd som registreras i en logg innehåller metadata som anger åtgärdstyp, datum och tid, e-post-ID för användaren som utförde åtgärden samt ytterligare attribut som är relevanta för åtgärdstypen. Den spårar de åtgärder som användare utför i kundens AI för att skapa, uppdatera och ta bort.

[Granskningsloggarna som valts på arbetsytan för kundens AI](../../customer-ai/images/data-governance/audit-logs-cai.png)

## Åtkomst till granskningsloggar

När funktionen är aktiverad för din organisation samlas granskningsloggarna automatiskt in när aktiviteten inträffar. Du behöver inte aktivera loggsamling manuellt.

För att kunna visa och exportera granskningsloggar måste du ha beviljats åtkomstkontrollbehörighet för granskningsloggar i Adobe Console. Läs mer om hur du hanterar individuella behörigheter för AI-funktioner för kunder i [dokumentation om åtkomstkontroll](../../customer-ai/user-guide/access-controls.md).