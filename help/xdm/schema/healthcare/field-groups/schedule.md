---
title: Fältgrupp för schema
description: Läs mer om schemafältgruppen Schema.
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: fcabef50-203c-4239-81b4-210aaf5b26ca
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 0%

---

# Schemafältgruppen [!UICONTROL Schedule]

[!UICONTROL Schedule] är en standardschemafältgrupp för [[!DNL XDM Individual Profile] klassen](../../../classes/individual-profile.md) och [[!DNL Provider class]](../../../classes/provider.md). Det tillhandahåller ett enskilt objekttypsfält `healthcareSchedule` som är en behållare för tidsperioder som kan vara tillgängliga för bokning av avtalade tider.

![Fältgruppsstruktur](../../../images/healthcare/field-groups/schedule.png)

| Visningsnamn | Egenskap | Datatyp | Beskrivning |
| --- | --- | --- | --- |
| [!UICONTROL Actor] | `actor` | Array med [[!UICONTROL Reference]](../data-types/reference.md) | Kortplatserna som refererar till det här schemat och som tillhandahåller tillgänglighetsinformation för dessa refererade resurser. |
| [!UICONTROL Identifier] | `identifier` | Array med [[!UICONTROL Identifier]](../data-types/identifier.md) | Externa identifierare för schemat. |
| [!UICONTROL Planning Horizon] | `planningHorizon` | [[!UICONTROL Period]](../data-types/period.md) | Den tidsperiod som de fack som refererar till det här schemat täcker, även om det inte finns någon. |
| [!UICONTROL Service Category] | `serviceCategory` | Array med [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md) | En bred kategorisering av den tjänst som ska utföras under mötet. |
| [!UICONTROL Service Type] | `serviceType` | Array med [[!UICONTROL Codeable Reference]](../data-types/codeable-reference.md) | Den specifika tjänst som ska utföras under den avtalade tiden. |
| [!UICONTROL Speciality] | `specialty` | Array med [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md) | Specialiteten hos den befattningsutövare som skulle behöva utföra den tjänst som begärdes i utnämningen. |
| [!UICONTROL Active] | `active` | Boolean | Anger om schemaposten används. |
| [!UICONTROL Comment] | `comment` | Sträng | Kommentarer om tillgängligheten i syfte att beskriva eventuell utökad information, t.ex. anpassade begränsningar för kortplatserna. |
| [!UICONTROL Name] | `name` | Sträng | Beskrivningen av schemat så som det skulle visas för en konsument vid sökning. |

Mer information om fältgruppen finns i den offentliga XDM-databasen:

* [Populerat exempel](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/schedule.example.1.json)
* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/schedule.schema.json)
