---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;fields;schemas;Schemas;fullName;xdm:fullName;person name;name;datatype;data-type;data type;
solution: Experience Platform
title: Datatyp för personnamn
topic: overview
description: Det här dokumentet innehåller en översikt över datatypen XDM för personnamn.
translation-type: tm+mt
source-git-commit: f5bddb39c16eb25e85297f56e331d3aa51510eb9
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 0%

---


# [!UICONTROL Person name] datatyp

[!UICONTROL Person name] är en standard-XDM-datatyp som beskriver en persons fullständiga namn. Eftersom konventionerna för namnstrukturer skiljer sig mycket åt mellan olika språk och kulturer bör namn alltid modelleras med den här datatypen.

Dessutom innehåller datatypen ett antal valfria egenskaper som kan användas i situationer där bara ett fragment av det fullständiga namnet måste användas, till exempel för att skapa en formell eller informell hälsning.

<img src="../images/data-types/person-name.png" width="500" /><br />

| Egenskap | Beskrivning |
| --- | --- |
| `courtesyTitle` | En förkortning av en persons titel, ära eller hälsningsfras (till exempel `Mr.`, `Miss.`eller `Dr.`). |
| `firstName` | Det första segmentet i namnet i den skrivordning som oftast används på namnet. |
| `fullName` | Personens fullständiga namn, i den skrivordning som är vanligast på namnet. |
| `lastName` | Det sista segmentet i namnet i den skrivordning som oftast används på namnet. |
| `middleName` | Mellannamn, alternativa namn eller ytterligare namn som anges mellan förnamnet och efternamnet. |
| `suffix` | En grupp bokstäver som anges efter en persons namn för att ge ytterligare information (till exempel `Jr.`, `Sr.`, `M.D.`, `PhD`, `I`, `II`, `III`osv.). |

Mer information om personnamnets datatyp finns i den offentliga XDM-databasen:

* [Populerat exempel](https://github.com/adobe/xdm/blob/master/components/datatypes/person-name.example.1.json)
* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/components/datatypes/person-name.schema.json)