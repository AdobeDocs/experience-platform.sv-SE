---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Felsökningsguide för sandlådor
topic: troubleshooting guide
translation-type: tm+mt
source-git-commit: f15049ca917818d325b5783c70faaa53ba669aba
workflow-type: tm+mt
source-wordcount: '487'
ht-degree: 0%

---


# Felsökningsguide för sandlådor

Det här dokumentet innehåller svar på vanliga frågor om sandlådor i Adobe Experience Platform. För frågor och felsökning som rör andra Platform-tjänster, se felsökningsguiden för [Experience Platform](../landing/troubleshooting.md).

Sandlådor delar en enda Platform-instans i separata virtuella miljöer för att utveckla och utveckla program för digitala upplevelser. Mer information finns i översikten över [](home.md) sandlådor.

## Vad är en sandlåda?

Sandlådor är virtuella partitioner i en enda instans av Experience Platform. Varje sandlåda har ett eget oberoende bibliotek med Platform-resurser (inklusive scheman, datauppsättningar, profiler och så vidare). Allt innehåll och alla åtgärder som vidtas i en sandlåda begränsas till enbart den sandlådan och påverkar inte några andra sandlådor. Mer information finns i översikten över [](home.md) sandlådor.

## Vilka typer av sandlådor är tillgängliga och vilka är skillnaderna?

Det finns två typer av sandlådor i Experience Platform:

* Produktionssandlåda
* Icke-produktionssandlåda

Experience Platform har en enda **produktionssandlåda** som inte kan tas bort eller återställas. Det får bara finnas en produktionssandlåda för en enda Platform-instans.

Däremot kan flera **icke-produktionssandlådor** skapas av sandlådeadministratörer för en enda Platform-instans. Med icke-produktionssandlådor kan du testa funktioner, köra experiment och göra anpassade konfigurationer utan att påverka din produktionssandlåda. Dessutom har icke-produktionssandlådor en återställningsfunktion som tar bort alla kundskapade resurser från sandlådan. Det går inte att konvertera icke-produktionssandlådor till produktionssandlådor.

Mer information finns i översikten över [](./home.md) sandlådor.

## Kan jag få åtkomst till en resurs från mer än en sandlåda?

Sandlådor är isolerade partitioner av en enda Platform-instans, där varje sandlåda underhåller ett eget oberoende resursbibliotek. En resurs som finns i en sandlåda kan inte nås från någon annan sandlåda, oavsett sandlådetyp (produktion eller icke-produktion).

## Hur många produktionssandlådor kan jag ha?

Experience Platform har endast stöd för en produktionssandlåda per IMS-organisation, som medföljer. Även om det går att byta namn på produktionssandlådan kan den inte tas bort eller återställas. Användare med administratörsbehörighet för sandlådan kan bara skapa, återställa och ta bort sandlådor som inte är produktionssandlådor.

## Hur många icke-produktionssandlådor kan jag ha?

Experience Platform tillåter för närvarande att upp till 15 icke-produktionssandlådor är aktiva inom en enda IMS-organisation.

## Jag skapade just en sandlåda. Hur anger jag behörigheter för de användare som ska arbeta med den här sandlådan?

Adobe Admin Console länkar användare till sandlådor och behörigheter genom att använda **produktprofiler**. När du har skapat en ny sandlåda går du till fliken _Behörigheter_ i produktprofilen som du vill ge åtkomst till och klickar sedan på **Sandlådor**. Härifrån kan du lägga till eller ta bort åtkomst till den nya sandlådan på samma sätt som andra behörigheter.

Om du vill lägga till unika behörigheter för användare av en viss sandlåda kan du behöva skapa en ny produktprofil med rätt sandlådor och behörigheter tillämpade, och tilldela dessa användare till den profilen.

Mer information om hur du hanterar sandlådor och behörigheter i Admin Console finns i användarhandboken [för](../access-control/ui/overview.md) åtkomstkontroll.