---
title: Integritet, säkerhet och styrning i AI Assistant
description: Läs mer om sekretess-, säkerhets- och styrningsrutiner för AI Assistant.
hide: true
hidefromtoc: true
source-git-commit: 723638fcd580c81a84ffe6bf38c197c62fabc1f3
workflow-type: tm+mt
source-wordcount: '312'
ht-degree: 0%

---

# Integritet, säkerhet och styrning i AI Assistant

AI Assistant i Adobe Experience Platform har tagits fram med sekretess, säkerhet och styrning i framkanten.

Läs det här dokumentet om du vill veta mer om funktioner som är inriktade på kundförtroende och som du kan förvänta dig av AI Assistant:

* Inga personuppgifter används av AI Assistant idag, inte ens i utbildningssyfte.
* AI Assistant känner inte till konsumentdata.
* Alla befintliga [åtkomstkontroll](../access-control/home.md) profiler respekteras av AI Assistant.
   * Åtkomstkontroll på objektnivå stöds för objekt. Stöd för åtkomstkontroll på objektnivå för attribut kommer snart.
   * Alla nya attributbaserade åtkomstkontrollprinciper återspeglas i AI Assistant efter högst 24 timmar*
* Du måste ha explicit behörighet att interagera med AI Assistant.
   * Du kan ange olika behörigheter för Experience Platform och Journey Optimizer med [Behörighetsgränssnitt](../access-control/abac/ui/permissions.md) och du kan använda [Admin Console](../access-control/ui/browse.md) om du vill tilldela behörigheter till Customer Journey Analytics.
   * Behörigheterna är detaljerade och din sandlådeadministratör kan konfigurera vilka av dina användare som kan ställa olika frågekategorier (produktkunskapsbaserade frågor med AI Assistant eller frågor om driftsinsikter).
* AI Assistant är en HIPAA-klar funktion som uppfyller HIPAA-kraven för bearbetning och användning av PHI (Protected Health Information).
* Du kan visa en logg över dina tidigare interaktioner med AI Assistant med en 30-dagars bevarandeprincip.
* AI-assistenten omges av sandlådespecifika data och allmän Adobe-dokumentation när användaren besvarar uppmaningar. Data delas inte över sandlådor.
* Frågar som du anger för AI Assistant delas inte med andra kunder.


**Det innebär att om nya etiketter läggs till i fält och objekt eller om nya profiler skapas, tar det upp till 24 timmar för AI Assistant att efterleva dem. Under dessa 24 timmar har användare med nyligen begränsad åtkomst fortfarande åtkomst till dessa fält och objekt.*