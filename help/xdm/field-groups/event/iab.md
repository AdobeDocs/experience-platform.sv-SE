---
keywords: Experience Platform;hem;populära ämnen;schema;schema;XDM;ExperienceEvent;fields;schemas;Schema design;field group;iab;tcf;medgivande;
solution: Experience Platform
title: Fältgrupp för IAB TCF 2.0-samtycke
topic-legacy: overview
description: Det här dokumentet innehåller en översikt över schemafältgruppen IAB TCF 2.0 Consent för klassen XDM ExperienceEvent.
source-git-commit: 7a0ac3970713e95438c6f0fdbd6175545ea7fdd0
workflow-type: tm+mt
source-wordcount: '240'
ht-degree: 0%

---


# [!UICONTROL IAB TCF 2.0 Consent] schemafältgrupp

>[!IMPORTANT]
>
>Det här dokumentet innehåller schemafältgruppen [!UICONTROL IAB TCF 2.0 Consent] för klassen XDM ExperienceEvent. Den här fältgruppen bör endast användas om du har för avsikt att följa upp händelser för tillståndsändring över tid.
>
>Observera att medgivandevärden som registrerats i händelsedata inte respekteras i automatiska arbetsflöden för verkställighet. För att automatisk verkställighet ska kunna ske måste värdena för samtycke anges i klassen XDM Individual Profile och aktiveras för kundprofil i realtid.
>
>För fältgruppen som är avsedd för klassen XDM Individual Profile, se följande [dokument](../profile/iab.md) i stället.

[!UICONTROL IAB TCF 2.0 Consent] är en standardgrupp för schemafält för den  [[!DNL XDM ExperienceEvent] ](../../classes/experienceevent.md) klass som används för att fånga in en tidsstämplad serie IAB-medgivandesträngar, för att spåra mönster för samtyckesändringar över tid.

![](../../images/field-groups/iab-event.png)

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `consentStrings` | Array med [Consent Strings](../../data-types/consent-string.md) | En array med strängvärden för samtycke som är associerade med händelsen. |

{style=&quot;table-layout:auto&quot;}

Mer information om hur den här fältgruppen används finns i guiden [IAB TCF 2.0-stöd i Platform](../../../landing/governance-privacy-security/consent/iab/overview.md). Mer information om själva fältgruppen finns i den offentliga XDM-databasen:

* [Populerat exempel](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-privacy.example.1.json)
* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-privacy.schema.json)
