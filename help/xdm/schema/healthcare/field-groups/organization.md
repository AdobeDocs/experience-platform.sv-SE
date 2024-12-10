---
title: Fältgrupp för organisationsschema
description: Läs mer om fältgruppen Organisationsschema.
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: b0698d36-ebc3-4b76-adcc-1deb2cbb1564
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '282'
ht-degree: 0%

---

# Schemafältgruppen [!UICONTROL Organization]

[!UICONTROL Organization] är en standardschemafältgrupp för [[!DNL XDM Individual Profile] klassen](../../../classes/individual-profile.md) och [[!DNL Provider class]](../../../classes/provider.md). Det tillhandahåller ett enskilt objekttypsfält `healthcareOrganization` som innehåller information om grupperingar av personer eller organisationer med ett gemensamt syfte.

![Fältgruppsstruktur](../../../images/healthcare/field-groups/organization/organization.png)

| Visningsnamn | Egenskap | Datatyp | Beskrivning |
| ---| --- | --- | --- |
| [!UICONTROL Contact Details] | `contact` | Array med [[!UICONTROL Extended Contact Details]](../data-types/extended-contact-detail.md) | Kontaktuppgifter för kommunikationsenheter som är tillgängliga för den specifika organisationen. Det kan vara adresser, telefonnummer, faxnummer, mobilnummer, e-postadresser och webbplatser. |
| [!UICONTROL End Point] | `endpoint` | Array med [[!UICONTROL Reference]](../data-types/reference.md) | Tekniska slutpunkter som ger tillgång till tjänster som organisationen tillhandahåller. |
| [!UICONTROL Identifier] | `indentifier` | Array med [[!UICONTROL Identifier]](../data-types/identifier.md) | Den identifierare som används för att identifiera organisationen i flera olika system. |
| [!UICONTROL Part Of Organization] | `partOf` | [[!UICONTROL Reference]](../data-types/reference.md) | Organisationen som den här organisationen ingår i. |
| [!UICONTROL Qualification] | `qualification` | Array med objekt | De officiella certifieringar, ackrediteringar, utbildning, beteckningar och licenser som ger rätt till och/eller på annat sätt stöder organisationens tillhandahållande av vård. Mer information finns i avsnittet [nedan](#qualification). |
| [!UICONTROL Type] | `type` | Array med [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md) | Vilken typ av organisation det är. |
| [!UICONTROL Active] | `active` | Boolean | Anger om organisationens register fortfarande används. |
| [!UICONTROL Alias] | `alias` | Array med strängar | En lista med alternativa namn som organisationen kallas eller tidigare var känd som. |
| [!UICONTROL Description] | `description` | Sträng | Beskrivning av organisationen som hjälper till att tillhandahålla en allmän kontext för att säkerställa att rätt organisation väljs. |
| [!UICONTROL Name] | `name` | Sträng | Namnet som är associerat med organisationen. |

Mer information om fältgruppen finns i den offentliga XDM-databasen:

* [Populerat exempel](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/coverage.example.1.json)
* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/coverage.schema.json)

## `qualification` {#qualification}

`qualification` tillhandahålls som en array med objekt. Strukturen för varje objekt beskrivs nedan.

![kvalificeringsstruktur](../../../images/healthcare/field-groups/organization/qualification.png)

| Visningsnamn | Egenskap | Datatyp | Beskrivning |
| --- | --- | --- | --- |
| [!UICONTROL Code] | `code` | [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md) | Kodad representation av kvalifikationen. |
| [!UICONTROL Identifier] | `identifier` | Array med [[!UICONTROL Identifier]](../data-types/identifier.md) | En identifierare som tilldelats den här kvalifikationen för den här organisationen. |
| [!UICONTROL Issuer] | `issuer` | [[!UICONTROL Reference]](../data-types/reference.md) | Organisation som reglerar och utfärdar kvalifikationen. |
| [!UICONTROL Period] | `period` | [[!UICONTROL Period]](../data-types/period.md) | Period under vilken kvalificeringen är giltig. |
