---
keywords: Experience Platform;användarhandbok;attribuering;populära ämnen;åtkomstkontroller;skapa en modell;
feature: Attribution AI
title: Styrningsprinciper för attribuering av AI
description: Adobe Experience Platform tillhandahåller flera tjänster och verktyg som gör att du kan kontrollera dina insamlade upplevelsedata på ett säkert sätt.
exl-id: 448b10c8-8eac-41cb-9b77-66aa283c0a9d
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '194'
ht-degree: 0%

---

# Styrningspolitik inom AI för attribuering

När du har gått igenom arbetsflödet för att skapa en modell och skicka in modellens konfiguration, kontrollerar [policytillämpningen](../../../data-governance/enforcement/auto-enforcement.md) om det finns några överträdelser. Om en principöverträdelse inträffar visas en portfölj som anger att en eller flera profiler har överträtts. Detta för att säkerställa att datahanteringen och marknadsföringsåtgärderna inom Experience Platform är kompatibla med dataanvändningsprinciperna.

## Poängbrott - poäns

[En pover som visar information om principöverträdelsen](../../attribution-ai/images/data-governance/policy-violation-popover-aai.png).

Leverantören ger specifik information om överträdelsen. Du kan lösa dessa överträdelser med hjälp av principinställningar och andra åtgärder som inte är direkt relaterade till konfigurationsarbetsflödet. Du kan till exempel ändra etiketterna så att vissa fält kan användas i datavetenskapliga syften. Du kan också ändra själva modellkonfigurationen så att den inte använder något med en etikett på den. Mer information om hur du konfigurerar principer finns i dokumentationen.
