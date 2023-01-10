---
keywords: Experience Platform;hem;populära ämnen;schema;schema;XDM;fält;scheman;scheman;fullständigt namn;xdm:fullständigtNamn;personnamn;datatyp;datatyp;datatyp;datatyp;
solution: Experience Platform
title: Datatyp för personnamn
description: Det här dokumentet innehåller en översikt över datatypen XDM för personnamn.
exl-id: 5cf55fb1-b6b0-4d1c-93c3-7e2b7766599e
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '252'
ht-degree: 0%

---

# [!UICONTROL Person name] datatyp

[!UICONTROL Person name] är en standard-XDM-datatyp som beskriver en persons fullständiga namn. Eftersom konventionerna för namnstrukturer skiljer sig mycket åt mellan olika språk och kulturer bör namn alltid modelleras med den här datatypen.

Dessutom innehåller datatypen ett antal valfria egenskaper som kan användas i situationer där bara ett fragment av det fullständiga namnet måste användas, till exempel för att skapa en formell eller informell hälsning.

<img src="../images/data-types/person-name.png" width="500" /><br />

| Egenskap | Beskrivning |
| --- | --- |
| `courtesyTitle` | En förkortning av en persons titel, ära eller hälsningsfras (t.ex. `Mr.`, `Miss.`, eller `Dr.`). |
| `firstName` | Det första segmentet i namnet i den skrivordning som oftast används på namnet. |
| `fullName` | Personens fullständiga namn, i den skrivordning som är vanligast på namnet. |
| `lastName` | Det sista segmentet i namnet i den skrivordning som oftast används på namnet. |
| `middleName` | Mellannamn, alternativa namn eller ytterligare namn som anges mellan förnamnet och efternamnet. |
| `suffix` | En grupp bokstäver efter en persons namn som ger ytterligare information (t.ex. `Jr.`, `Sr.`, `M.D.`, `PhD`, `I`, `II`, `III`och så vidare). |

{style=&quot;table-layout:auto&quot;}

Mer information om personnamnets datatyp finns i den offentliga XDM-databasen:

* [Populerat exempel](https://github.com/adobe/xdm/blob/master/components/datatypes/person/person-name.example.1.json)
* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/components/datatypes/person/person-name.schema.json)
