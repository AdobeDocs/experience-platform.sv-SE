---
keywords: insikter;attribuering;attribueringsinsikter;AAI-frågetjänst;attribueringsfrågor;attribueringspoäng
title: Granskningsloggar i Attribution AI Översikt
description: Lär dig hur du visar och hanterar granskningsloggar i Attribution AI.
exl-id: 83c55dbc-f03d-4bda-ae07-68b7914483c8
source-git-commit: f28558d5939607cabf449cbc03b7e0f5406f6326
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 0%

---

# Granskningsloggar i Attribution AI

För att öka insynen i och synligheten för aktiviteter som utförs i systemet, hämtas användaraktiviteten i arbetsflödet nu in i granskningsloggar för att förstå användardrivna ändringar av Attribution AI. Loggarna utgör en verifieringskedja som kan hjälpa till med felsökningsproblem och hjälper ditt företag att effektivt följa företagets policyer för datahantering och lagstadgade krav.  Om ni omfattas av HIPAA (Health Insurance Portability and Accounability Act) och skapar, tar emot, underhåller eller överför tillåtna känsliga personuppgifter via Attribution AI eller kundens AI är ni ansvariga för att genomföra en BAA med Adobe och licensiera vårdsköld.

I grundläggande bemärkelse anger en granskningslogg vem som utförde vilken åtgärd och när. Varje åtgärd som registreras i en logg innehåller metadata som anger åtgärdstyp, datum och tid, e-post-ID för användaren som utförde åtgärden samt ytterligare attribut som är relevanta för åtgärdstypen. Den spårar de åtgärder som användare i Attribution AI utför för att skapa, uppdatera och ta bort.

<!-- [The audit logs selected in the Attribution AI workspace](../../../attribution-ai/aai-data-governance/images/data-governance/audit-logs-cai.png) -->

## Åtkomst till granskningsloggar

När funktionen är aktiverad för din organisation samlas granskningsloggarna automatiskt in när aktiviteten inträffar. Du behöver inte aktivera loggsamling manuellt.

För att kunna visa och exportera granskningsloggar måste du ha beviljats åtkomstkontrollbehörighet för granskningsloggar i Adobe Console. Mer information om hur du hanterar enskilda behörigheter för Attribution AI finns i [åtkomstkontrollsdokumentationen](../aai-data-governance/access-controls.md).
