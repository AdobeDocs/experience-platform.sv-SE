---
keywords: Experience Platform;hem;populära ämnen;schema;schema;XDM;ExperienceEvent;fields;schemas;Schema design;field group;iab;tcf;medgivande;
solution: Experience Platform
title: IAB TCF 2.0-sambandsfältgrupp för händelsescheman
description: Läs mer om schemafältgruppen IAB TCF 2.0 Consent för klassen XDM ExperienceEvent.
exl-id: c236d0d4-27bd-45d7-a912-d0e93a609254
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '221'
ht-degree: 0%

---

# Fältgrupp [!UICONTROL IAB TCF 2.0 Consent] för händelsescheman

>[!IMPORTANT]
>
>Det här dokumentet innehåller schemafältgruppen [!UICONTROL IAB TCF 2.0 Consent] för klassen XDM ExperienceEvent. Den här fältgruppen bör endast användas om du har för avsikt att följa upp händelser för tillståndsändring över tid.
>
>Observera att medgivandevärden som registrerats i händelsedata inte respekteras i automatiska arbetsflöden för verkställighet. För att automatisk verkställighet ska kunna ske måste värdena för samtycke anges i klassen XDM Individual Profile och aktiveras för kundprofilen i realtid.
>
>För fältgruppen som är avsedd för klassen XDM Individual Profile, se följande [dokument](../profile/iab.md) i stället.

[!UICONTROL IAB TCF 2.0 Consent] är en standardschemafältgrupp för den [[!DNL XDM ExperienceEvent] klass](../../classes/experienceevent.md) som används för att hämta en tidsstämplad serie IAB-medgivandesträngar, för att kunna spåra mönster för medgivandeändring över tid.

![](../../images/field-groups/iab-event.png)

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `consentStrings` | Matris med [medgivandesträngar](../../data-types/consent-string.md) | En array med strängvärden för samtycke som är associerade med händelsen. |

{style="table-layout:auto"}

Mer information om hur den här fältgruppen används finns i guiden [IAB TCF 2.0-stöd i Platform](../../../landing/governance-privacy-security/consent/iab/overview.md) . Mer information om själva fältgruppen finns i den offentliga XDM-databasen:

* [Populerat exempel](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-privacy.example.1.json)
* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-privacy.schema.json)
