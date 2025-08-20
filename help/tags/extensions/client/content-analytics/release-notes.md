---
title: Versionsinformation om Adobe Content Analytics Extension
description: Den senaste versionsinformationen om taggtillägget Content Analytics i Adobe Experience Platform.
source-git-commit: 24ff17af89bc882f08ec0f331ebae53b61f35d78
workflow-type: tm+mt
source-wordcount: '265'
ht-degree: 0%

---

# Versionsinformation om Adobe Content Analytics-tillägg

Nedan följer en lista över versionsinformation för Content Analytics-taggtillägget.

| Version | Datum | Korrigeringar |
|---|---|---|
| <p>1.0.47</p> | <p>23 juli 2025</p> | <ul><li>Korrigerar det fel som en kund råkade ut för när upplevelserna inte var aktiverade och den reguljära uttryckskontrollen för upplevelser misslyckades. Detta gör att Content Analytics-data inte samlas in.</li><li>Korrigerar standardspråksfelet som förhindrade att användargränssnittet för taggar visades för vissa användare om deras primära standardspråk inte hade angetts i Experience Cloud.</li></ul> |
| <p>1.0.46</p> | <p>18 juni 2025</p> | <ul><li>Lägger till ett popup-meddelande om det inte finns något produktionsdatastream när du försöker spara tilläggskonfigurationen.</li><li>Korrigerar tillfälligt att Content Analytics-nyttolasten är synlig, men placerar det strängade Content Analytics-nyttolastinnehållet i konsolen.</li><li>Lägger till lokalisering i tilläggsgränssnittet.</li><li>Åtgärdar delvis ett CSS-problem med extra utfyllnad runt gränssnittsinnehållet i tillägget.</li></ul> |
| <p>1.0.45</p> | <p>14 apr 2025</p> | <ul><li>Åtgärdar några fel i konfigurationsinställningarna när du håller ned Content Analytics-händelser i väntan på sidvisningshändelser. Nu väntar Content Analytics som standard på att utlösa händelser tills den första sidvisningshändelsen inträffar.</li></ul> |
| <p>1.0.44</p> | <p>31 mars 2025</p> | <ul><li>Den första upprepningen av AppMeasurement-integreringen.</li><li>Den här versionen stöder inte filtrering på specifika begäranden (till exempel sidvyer), men kan läggas till vid ett senare datum.  Detta använder även den första AppMeasurement-instansen som finns på sidan.</li></ul> |
| <p>1.0.43</p> | <p>10 mars 2025</p> | <ul><li>Ursprunglig tilläggsversion.</li></ul> |

