---
title: Fältgrupp för skrivarschema
description: Lär dig mer om schemafältgruppen för operatorn.
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: e01a6cd4cf42338f87222a5e2871cd6c3683309a
workflow-type: tm+mt
source-wordcount: '340'
ht-degree: 0%

---

# Schemafältgruppen [!UICONTROL Practioner]

[!UICONTROL Practioner] är en standardschemafältgrupp för [[!DNL XDM Individual Profile] klassen](../../classes/individual-profile.md) och [[!DNL Provider class]](../../classes/provider.md). Det tillhandahåller ett enskilt objekttypsfält `healthcarePractioner` som innehåller information om en person som är direkt eller indirekt involverad i etableringen av hälso- och sjukvårdstjänster eller relaterade tjänster.

![Fältgruppsstruktur](../../images/field-groups/healthcare-practitioner/practitioner.png)

| Visningsnamn | Egenskap | Datatyp | Beskrivning |
| --- | --- | --- | --- |
| [!UICONTROL Address] | `address` | Array med [[!UICONTROL Address]](../../data-types/healthcare/address.md) | Adress(er) till den eller de verkställande som befinner sig utanför arbetsplatsen, t.ex. en hemadress. |
| [!UICONTROL Communication] | `communication` | Array med objekt | Ett språk som kan användas för att kommunicera med behandlaren. Mer information finns i avsnittet [nedan](#communication) |
| [!UICONTROL Identifier] | `identifier` | Array med [[!UICONTROL Identifier]](../../data-types/healthcare/identifier.md) | En identifierare som gäller för den här personen i den här rollen. |
| [!UICONTROL Name] | `name` | Array med [[!UICONTROL Human Name]](../../data-types/healthcare/human-name.md) | Namnet/namnen som är kopplade till behandlaren. |
| [!UICONTROL Qualification] | `qualification` | Array med objekt | De officiella kvalifikationer, certifieringar, ackrediteringar, utbildning, licenser eller liknande som ger rätt till eller på annat sätt gäller läkarens vård. Mer information finns i avsnittet [nedan](#qualification). |
| [!UICONTROL Contact Details] | `telecom` | Array med [[!UICONTROL Contact Point]](../../data-types/healthcare/contact-point.md) | Kontaktuppgifter till läkaren. |
| [!UICONTROL Active] | `active` | Boolean | Anger om praktikpersonens register används aktivt. |
| [!UICONTROL Birth Date] | `birthDate` | Datum | Dag för läkarens födelse. |
| [!UICONTROL Deceased Indicator] | `deceasedBoolean` | Boolean | Anger om yrkesutövaren är avliden. |
| [!UICONTROL Deceased Date Time] | `deceasedDateTime` | DateTime | Datum och tid för läkarens död. |
| [!UICONTROL Gender] | `gender` | Sträng | Personens könsidentitet. Värdet för den här egenskapen måste vara lika med ett av följande kända enum-värden. <li> `female` </li> <li> `male` </li> <li> `other` </li> <li> `unknown`</li> |

{style="table-layout:auto"}

Mer information om fältgruppen finns i den offentliga XDM-databasen:

* [Populerat exempel](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/practitioner.example.1.json)
* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/practitioner.schema.json)

## `communication` {#communication}

`communication` tillhandahålls som en array med objekt. Strukturen för varje objekt beskrivs nedan.

![kommunikationsstruktur](../../images/field-groups/healthcare-practitioner/communication.png)

| Visningsnamn | Egenskap | Datatyp | Beskrivning |
| --- | --- | --- | --- |
| [!UICONTROL Language] | `language` | [[!UICONTROL Codeable Concept]](../../data-types/healthcare/codeable-concept.md) | Det språk som kan användas för att kommunicera med personen om deras hälsa. |
| [!UICONTROL Is Preferred Language] | `preferred` | Boolean | Anger om språket är det språk de föredrar eller inte. |

{style="table-layout:auto"}

## `qualification` {#qualification}

`qualification` tillhandahålls som en array med objekt. Strukturen för varje objekt beskrivs nedan.

![kvalificeringsstruktur](../../images/field-groups/healthcare-practitioner/qualification.png)

| Visningsnamn | Egenskap | Datatyp | Beskrivning |
| --- | --- | --- | --- |
| [!UICONTROL Code] | `code` | [[!UICONTROL Codeable Concept]](../../data-types/healthcare/codeable-concept.md) | Den kodade representationen av kvalifikationen. |
| [!UICONTROL Identifier] | `identifier` | Array med [[!UICONTROL Identifier]](../../data-types/healthcare/identifier.md) | En identifierare för kvalificeringen. |
| [!UICONTROL Issuer] | `issuer` | [[!UICONTROL Reference]](../../data-types/healthcare/reference.md) | Organisationen som reglerar och utfärdar kvalifikationen. |
| [!UICONTROL Period] | `period` | [[!UICONTROL Period]](../../data-types/healthcare/period.md) | Den period under vilken kvalificeringen är giltig. |

{style="table-layout:auto"}
