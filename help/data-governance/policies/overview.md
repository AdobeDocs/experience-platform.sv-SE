---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Översikt över policyer för dataanvändning
topic: policies
translation-type: tm+mt
source-git-commit: d08f06b3c2bdb21e0f4935bbcb6f163892ab9842

---


# Översikt över policyer för dataanvändning

För att dataanvändningsetiketter effektivt ska stödja regelefterlevnad måste dataanvändningsprinciper implementeras. Dataanvändningspolicyer är regler som beskriver den typ av marknadsföringsåtgärder som du tillåts eller begränsas från att utföra på data i Experience Platform.

Ett exempel på en marknadsföringsåtgärd kan vara en önskan att exportera en datauppsättning till en tredjepartstjänst. Om det finns en policy som säger att vissa typer av data, t.ex. PII (Personally Identiitable Information), inte kan exporteras och att ID-etiketten (Identity data) har tillämpats på datauppsättningen, får du ett svar från principtjänsten som säger att en dataanvändningspolicy har överträtts.

## Skapa och arbeta med dataanvändningspolicyer

När dataanvändningsetiketter har tillämpats kan datafördelningar skapa principer med API:t för [DULE Policy Service](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml).

Som ett datasegment kan du använda API:t för principtjänst för att hantera och utvärdera principer som relaterar till marknadsföringsåtgärder som vidtas på data som innehåller DULE-etiketter. Med API:t kan du skapa och uppdatera principer, fastställa en profils status och arbeta med marknadsföringsåtgärder för att utvärdera om en viss åtgärd bryter mot en dataanvändningspolicy.

I Policy Service API kallas alla policyer och marknadsföringsåtgärder antingen `core` eller `custom` resurser. `core` resurser definieras och underhålls av Adobe, medan `custom` resurser skapas och underhålls av enskilda kunder. Resurserna är därför unika och synliga endast för den organisation som skapade dem. `custom`

Mer information om hur du utför nyckelåtgärder som tillhandahålls av API:t för DULE Policy Service finns i utvecklarhandboken för [Policy Service](../api/getting-started.md). Stegvisa instruktioner om hur du arbetar med DULE-profiler finns i självstudiekursen om hur du [skapar och utvärderar DULE-profiler](create.md).