---
title: Betalarklass
description: Det här dokumentet innehåller en översikt över klassen Payer i Experience Data Model (XDM).
source-git-commit: 3937963ceee8502b0669a3f007fd38ecf2824e9b
workflow-type: tm+mt
source-wordcount: '131'
ht-degree: 0%

---

# [!UICONTROL Payer] class

I Experience Data Model (XDM) är [!UICONTROL Payer] klassen innehåller den minsta uppsättning egenskaper som definierar ett betalarföretag som samlar in uppgifter som gäller försäkringsbolag (t.ex. sjukförsäkring).

![Klassstruktur](../images/classes/payer.png)

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `_id` | [!UICONTROL String] | En unik systemgenererad strängidentifierare för posten. Det här fältet används för att spåra en enskild posts unika karaktär, förhindra dubblering av data och för att söka efter posten i underordnade tjänster.<br><br>Eftersom det här fältet genereras av systemet, anges inget explicit värde vid datainmatning. Du kan dock välja att ange egna unika ID-värden om du vill. |
| `payerId` | [!UICONTROL String] | En unik identifierare för betalaren. |
| `payerName` | [!UICONTROL String] | Betalarens namn. |

{style=&quot;table-layout:auto&quot;}
