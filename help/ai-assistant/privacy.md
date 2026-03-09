---
title: Integritet, säkerhet och styrning i AI Assistant (äldre)
description: Läs mer om sekretess-, säkerhets- och styrningsrutiner för AI Assistant (äldre).
exl-id: 371e065d-c2dd-4233-b78e-a42757fce853
source-git-commit: 077c42f2190316a00168bbeca685c08677c2b13a
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 0%

---

# Integritet, säkerhet och styrning i AI Assistant (äldre)

AI Assistant (äldre) i Adobe Experience Platform har tagits fram med sekretess, säkerhet och styrning i framkanten.

Läs det här dokumentet om du vill veta mer om funktioner som är inriktade på kundförtroende och som du kan förvänta dig av AI Assistant (äldre):

* Inga personuppgifter används av AI Assistant (äldre) idag, inte ens i utbildningssyfte.
* AI Assistant (äldre) känner inte till konsumentdata.
* Alla befintliga [åtkomstkontrollprinciper](../access-control/home.md) respekteras av AI Assistant (äldre).
   * Alla nya attributbaserade åtkomstkontrollprinciper återspeglas i AI Assistant (äldre) efter högst 24 timmar*
* AI Assistant (äldre) är en HIPAA-klar funktion när den används i kombination med Adobe Experience Platform Healthcare Shield.
* Du kan visa en logg över dina tidigare interaktioner med AI Assistant (äldre) med en 30-dagars bevarandeprincip.
* AI Assistant (äldre) rundas av i sandlådespecifika data och i offentlig Adobe-dokumentation när användaren tillfrågas. Data delas inte över sandlådor.
* Frågar som du anger för AI Assistant (äldre) delas inte med andra kunder.

**Det innebär att om nya etiketter läggs till i fält och objekt eller om nya profiler skapas, tar det upp till 24 timmar för AI Assistant (äldre) att efterleva dem. Under dessa 24 timmar har användare med nyligen begränsad åtkomst fortfarande åtkomst till dessa fält och objekt.*
