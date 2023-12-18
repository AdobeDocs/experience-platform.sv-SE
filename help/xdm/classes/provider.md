---
title: Providerklass
description: Läs mer om klassen Provider i Experience Data Model (XDM).
exl-id: acb9b8a3-f911-49c5-9d2a-3a0d6aeebef9
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '138'
ht-degree: 0%

---

# [!UICONTROL Provider] class

I Experience Data Model (XDM) är [!UICONTROL Provider] klassen fångar upp den minsta uppsättning egenskaper som definierar en tjänsteleverantörs affärsenhet (t.ex. en vårdgivare eller försäkringsleverantör).

![Klassstruktur](../images/classes/provider.png)

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `providerName` | [[!UICONTROL Person name]](../data-types/person-name.md) | Namnet på providern. |
| `_id` | [!UICONTROL String] | En unik systemgenererad strängidentifierare för posten. Det här fältet används för att spåra en enskild posts unika karaktär, förhindra dubblering av data och för att söka efter posten i underordnade tjänster.<br><br>Eftersom det här fältet genereras av systemet, anges inget explicit värde vid datainmatning. Du kan dock välja att ange egna unika ID-värden om du vill. |
| `providerId` | [!UICONTROL String] | En unik identifierare för providern. |

{style="table-layout:auto"}

Klassen kan utökas med [[!UICONTROL Healthcare Provider] fältgrupp](../field-groups/provider/healthcare-provider.md) Beskriv mer ingående information om en vårdgivare.
