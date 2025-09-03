---
title: Versionsinformation om Adobe Content Analytics Extension
description: Den senaste versionsinformationen om taggtillägget Content Analytics i Adobe Experience Platform.
exl-id: 37b34915-655b-40de-b17b-43028c579e37
source-git-commit: 77d19ab813f881cd3c48c27ed4a9ac02e268e23f
workflow-type: tm+mt
source-wordcount: '282'
ht-degree: 0%

---

# Versionsinformation om Adobe Content Analytics-tillägg

Nedan följer en lista över versionsinformation för Content Analytics-taggtillägget.

| Version | Datum | Korrigeringar |
|---|---|---|
| 1.0.48 | 25 augusti 2025 | <ul><li>Lägger till stöd för att spåra resurser i ett dokuments skuggrots-DOM-element.</li></ul> |
| 1.0.47 | 23 juli 2025 | <ul><li>Korrigerade ett fel som inträffade när upplevelser inte aktiverades, vilket gjorde att det reguljära uttrycket inte kunde kontrollera upplevelser. Detta förhindrar att Content Analytics data samlas in.</li><li>Ett problem med standardspråkinställningen som hindrade användargränssnittet för taggar från att visas för vissa användare som inte hade sitt primära standardspråk i Experience Cloud har åtgärdats.</li></ul> |
| 1.0.46 | 18 juni 2025 | <ul><li>Ett popup-meddelande lades till när tilläggskonfigurationen skulle sparas, om det inte finns något produktionsdatastream.</li><li>Korrigera tillfälligt synlighetsproblemet för Content Analytics-nyttolasten genom att placera det stringifierade nyttolastinnehållet i konsolen i stället.</li><li>Stöd för lokalisering har lagts till i tilläggsgränssnittet.</li><li>Ett CSS-problem som orsakade extra utfyllnad runt gränssnittsinnehållet i tillägget har delvis åtgärdats.</li></ul> |
| 1.0.45 | 14 apr 2025 | <ul><li>Flera fel i konfigurationsinställningarna som rör att hålla kvar Content Analytics-händelser i väntan på sidvisningshändelser har åtgärdats. Content Analytics väntar nu som standard på att utlösa händelser tills den första sidvisningshändelsen inträffar.</li></ul> |
| 1.0.44 | 31 mars 2025 | <ul><li>Den första upprepningen av AppMeasurement-integreringen.</li><li>Den här versionen stöder ännu inte filtrering av specifika begäranden (t.ex. sidvyer), men den här funktionen kan läggas till i en framtida uppdatering. Den använder för närvarande den första AppMeasurement-instansen som finns på sidan.</li></ul> |
| 1.0.43 | 10 mars 2025 | <ul><li>Ursprunglig tilläggsversion.</li></ul> |
