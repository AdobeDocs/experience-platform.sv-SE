---
keywords: insikter;customer ai;customer ai insights;CAI query service;customer ai queries;customer ai scores
title: Granskningsloggsöversikt i kundens AI
description: Lär dig hur du visar och hanterar granskningsloggar i kundens AI.
exl-id: f5b2d0b0-b6ae-4ccc-b4c9-ac9cc6078d81
source-git-commit: f28558d5939607cabf449cbc03b7e0f5406f6326
workflow-type: tm+mt
source-wordcount: '282'
ht-degree: 0%

---

# Granskningsloggar i kundens AI

För att öka insynen i och synligheten för aktiviteter som utförs i systemet, hämtas användaraktivitet i kundens AI-arbetsflöde nu in i granskningsloggar för att förstå användardrivna ändringar i kundens AI-modeller. Loggarna utgör en verifieringskedja som kan hjälpa till med felsökningsproblem och hjälper ditt företag att effektivt följa företagets policyer för datahantering och lagstadgade krav.  Om ni omfattas av HIPAA (Health Insurance Portability and Accounability Act) och skapar, tar emot, underhåller eller överför tillåtna känsliga personuppgifter via Attribution AI eller kundens AI är ni ansvariga för att genomföra en BAA med Adobe och licensiera vårdsköld.

I grundläggande bemärkelse anger en granskningslogg vem som utförde vilken åtgärd och när. Varje åtgärd som registreras i en logg innehåller metadata som anger åtgärdstyp, datum och tid, e-post-ID för användaren som utförde åtgärden samt ytterligare attribut som är relevanta för åtgärdstypen. Den spårar de åtgärder som användare utför i kundens AI för att skapa, uppdatera och ta bort.

[Granskningsloggarna som valts på arbetsytan för kundens AI](../../customer-ai/images/data-governance/audit-logs-cai.png)

## Åtkomst till granskningsloggar

När funktionen är aktiverad för din organisation samlas granskningsloggarna automatiskt in när aktiviteten inträffar. Du behöver inte aktivera loggsamling manuellt.

För att kunna visa och exportera granskningsloggar måste du ha beviljats åtkomstkontrollbehörighet för granskningsloggar i Adobe Console. Information om hur du hanterar individuella behörigheter för kundens AI-funktioner finns i [åtkomstkontrollsdokumentationen](../cai-data-governance/access-controls.md).
