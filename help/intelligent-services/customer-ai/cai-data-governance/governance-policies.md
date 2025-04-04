---
keywords: Experience Platform;användarhandbok;kundhandbok;populära ämnen;åtkomstkontroller;skapa modell;
feature: Customer AI
title: Styrningsprinciper för AI för kunder
description: Adobe Experience Platform tillhandahåller flera tjänster och verktyg som gör att du kan kontrollera dina insamlade upplevelsedata på ett säkert sätt.
exl-id: be3eca3a-0ea1-4b84-9454-675a4f9ac71e
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 0%

---

# Styrningspolicyer i kundens AI

När du har slutfört arbetsflödet för att skapa en modell och skicka modellens konfiguration, kontrollerar [policytillämpningen](/help/data-governance/enforcement/auto-enforcement.md) om det finns några överträdelser. Om en principöverträdelse inträffar visas en portfölj som anger att en eller flera profiler har överträtts. Detta för att säkerställa att datahanteringen och marknadsföringsåtgärderna inom Experience Platform är kompatibla med dataanvändningsprinciperna.

![En pover som visar information om principöverträdelsen](../images/user-guide/policy-violation-popover-cai.png).

Leverantören ger specifik information om överträdelsen. Du kan lösa dessa överträdelser med hjälp av principinställningar och andra åtgärder som inte är direkt relaterade till konfigurationsarbetsflödet. Du kan till exempel ändra etiketterna så att vissa fält kan användas i datavetenskapliga syften. Du kan också ändra själva modellkonfigurationen så att den inte använder något med en etikett på den. Mer information om hur du konfigurerar [profiler](/help/data-governance/policies/overview.md) finns i dokumentationen.
