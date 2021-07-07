---
keywords: Experience Platform;hem;populära ämnen;schema;schema;XDM;individual profile;fields;schemas;schemas;loyalty details;Schema design;field group;Field group;
solution: Experience Platform
title: Fältgrupp för förmånsdetaljschema
topic-legacy: overview
description: Det här dokumentet innehåller en översikt över schemafältgruppen för bonusdetaljer.
source-git-commit: afe748d443aad7b6da5b348cd569c9e806e4419b
workflow-type: tm+mt
source-wordcount: '301'
ht-degree: 1%

---


# [!UICONTROL Loyalty Details] schemafältgrupp

>[!NOTE]
>
>Namnen på flera schemafältgrupper har ändrats. Mer information finns i dokumentet om [uppdatering av fältgruppnamn](../name-updates.md).

[!UICONTROL Loyalty Details] är en standardgrupp för schemafält för  [[!DNL XDM Individual Profile] klassen](../../classes/individual-profile.md). Fältgruppen innehåller ett enskilt fält av objekttyp, `loyalty`, som samlar in information som rör en persons medlemskap i ett kundlojalitetsprogram.

![](../../images/field-groups/loyalty-details.png)

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `pointsExpiration` | Array med objekt | Visar en lista över eventuella förmånspoäng (eller grupper av förmånspoäng) som kommer att förfalla och de datum som de förfaller den. Varje arrayobjekt måste vara ett objekt som innehåller följande två egenskaper: <ul><li>`pointsExpirationDate`: En ISO 8601-datetime som anger när punkterna upphör att gälla.</li><li>`pointsExpiring`: Punktsaldot som förfaller från det associerade förfallodatumet.</li></ul> |
| `joinDate` | DateTime | En ISO 8601-datetime för när personen anslöt till lojalitetsprogrammet. |
| `loyaltyID` | Array med strängar | Representerar ID:n för förmånsprogram som är kopplade till medlemmen i bonusprogrammet. |
| `points` | Dubbel | Den aktuella balansen mellan förmånspoäng eller utmärkelser för lojalitetsmedlemmen. |
| `pointsRedeemed` | Dubbel | Belopp för poäng som lojalitetsmedlemmen har ansökt om vid ett köp eller på annat sätt har lösts in. |
| `program` | Sträng | Namnet på det bonusprogram där personen är registrerad. |
| `status` | Sträng | Aktuell status för personens lojalitetsmedlemskap, till exempel `active`, `disabled` eller `suspended`. |
| `tier` | Sträng | Hämtar den lojalitetsprogramnivå som personen är registrerad i. |
| `upgradeDate` | Sträng | Det datum då förmånsmedlemmen uppgraderades till sin senaste nivånivå. |

{style=&quot;table-layout:auto&quot;}

Mer information om fältgruppen finns i den offentliga XDM-databasen:

* [Populerat exempel](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-loyalty-details.example.1.json)
* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-loyalty-details.schema.json)
