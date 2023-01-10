---
keywords: Experience Platform;hem;populära ämnen;schema;schema;XDM;individual profile;fields;schemas;schemas;loyalty details;Schema design;field group;Field group;
solution: Experience Platform
title: Fältgrupp för förmånsdetaljschema
description: Det här dokumentet innehåller en översikt över schemafältgruppen för bonusdetaljer.
exl-id: 12c9fef5-4f9e-49b5-894f-f4938bb95c23
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '301'
ht-degree: 1%

---

# [!UICONTROL Loyalty Details] schemafältgrupp

>[!NOTE]
>
>Namnen på flera schemafältgrupper har ändrats. Visa dokumentet på [uppdaterar fältgruppnamn](../name-updates.md) för mer information.

[!UICONTROL Loyalty Details] är en standardgrupp för schemafält för [[!DNL XDM Individual Profile] class](../../classes/individual-profile.md). Fältgruppen innehåller ett enda fält av objekttyp, `loyalty`, som samlar in information om en persons medlemskap i ett kundlojalitetsprogram.

![](../../images/field-groups/loyalty-details.png)

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `pointsExpiration` | Array med objekt | Visar en lista över eventuella förmånspoäng (eller grupper av förmånspoäng) som kommer att förfalla och de datum som de förfaller den. Varje arrayobjekt måste vara ett objekt som innehåller följande två egenskaper: <ul><li>`pointsExpirationDate`: En ISO 8601-datetime som anger när punkterna upphör att gälla.</li><li>`pointsExpiring`: Punktsaldot som förfaller från det associerade förfallodatumet.</li></ul> |
| `joinDate` | DateTime | En ISO 8601-datetime för när personen anslöt till lojalitetsprogrammet. |
| `loyaltyID` | Array med strängar | Representerar ID:n för förmånsprogram som är kopplade till medlemmen i bonusprogrammet. |
| `points` | Dubbel | Den aktuella balansen mellan förmånspoäng eller utmärkelser för lojalitetsmedlemmen. |
| `pointsRedeemed` | Dubbel | Belopp för poäng som lojalitetsmedlemmen har ansökt om vid ett köp eller på annat sätt har lösts in. |
| `program` | Sträng | Namnet på det bonusprogram där personen är registrerad. |
| `status` | Sträng | Aktuell status för personens lojalitetsmedlemskap, t.ex. `active`, `disabled`, eller `suspended`. |
| `tier` | Sträng | Hämtar den lojalitetsprogramnivå som personen är registrerad i. |
| `upgradeDate` | Sträng | Det datum då förmånsmedlemmen uppgraderades till sin senaste nivånivå. |

{style=&quot;table-layout:auto&quot;}

Mer information om fältgruppen finns i den offentliga XDM-databasen:

* [Populerat exempel](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-loyalty-details.example.1.json)
* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-loyalty-details.schema.json)
