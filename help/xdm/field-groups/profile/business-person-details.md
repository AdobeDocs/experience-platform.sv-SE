---
title: Schemafältgrupp för XDM-affärspersonsinformation
description: Det här dokumentet innehåller en översikt över schemafältgruppen XDM Business Person Details.
source-git-commit: 319d508925d22e76a3d75ae473f6ea000b5c655b
workflow-type: tm+mt
source-wordcount: '537'
ht-degree: 3%

---


# [!UICONTROL XDM Business Person Details] schemafältgrupp

>[!NOTE]
>
>Den här fältgruppen är bara tillgänglig för organisationer som har tillgång till B2B-utgåvan av kunddataplattformen i realtid.

[!UICONTROL XDM Business Person Details] är en standardgrupp för schemafält för den  [[!DNL XDM Individual Profile] ](../../classes/individual-profile.md) klass som samlar in information om en enskild person i ett B2B-företag (business-to-business).

![](../../images/field-groups/business-person-details.png)

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `b2b` | Objekt | Ett objekt som hämtar de B2B-specifika uppgifterna om personen. |
| `b2b.accountKey` | [[!UICONTROL B2B Source]](../../data-types/b2b-source.md) | En sammansatt identifierare för det företagskonto som är relaterat till personen. |
| `b2b.convertedContactKey` | [[!UICONTROL B2B Source]](../../data-types/b2b-source.md) | En sammansatt identifierare för den associerade kontakten om leadet konverterades. |
| `b2b.personKey` | [[!UICONTROL B2B Source]](../../data-types/b2b-source.md) | En sammansatt identifierare för person- eller profilfragmentet. |
| `b2b.accountID` | Sträng | Ett unikt ID för det företagskonto som den här personen är kopplad till. |
| `b2b.blockedCause` | Sträng | Om personen är blockerad anger den här egenskapen varför. |
| `b2b.convertedContactID` | Sträng | Kontakt-ID om leadet konverterades. |
| `b2b.convertedDate` | DateTime | Datumet för konverteringen om leadet konverterades. |
| `b2b.isBlocked` | Boolean | Anger om personen är spärrad. |
| `b2b.isConverted` | Boolean | Anger om leadet konverteras. |
| `b2b.isMarketingSuspended` | Boolean | Anger om marknadsföringen har avbrutits för personen. |
| `b2b.marketingSuspendedCause` | Sträng | Om marknadsföringen avbryts för personen anger denna egenskap anledningen till detta. |
| `b2b.personGroupID` | Sträng | En gruppidentifierare för personen. |
| `b2b.personScore` | Dubbel | En poäng som genererats för personen av ett CRM-system. |
| `b2b.personSource` | Sträng | Källan som personuppgifterna togs emot från. |
| `b2b.personStatus` | Sträng | Personens aktuella marknadsförings- eller försäljningsstatus. |
| `b2b.personType` | Sträng | Typ av B2B-person. |
| `extSourceSystemAudit` | [Granskningsattribut för externt källsystem](../../data-types/external-source-system-audit-attributes.md) | Om affärspersonsrelationen kommer från ett externt källsystem hämtar det här objektet granskningsattribut för det systemet. |
| `extendedWorkDetails` | Objekt | Hämtar ytterligare arbetsrelaterad information om personen. |
| `extendedWorkDetails.assistantDetails` | Objekt | Hämtar följande attribut relaterade till personens assistent: <ul><li>`name`: ([personnamn](../../data-types/person-name.md)) Assistentens fullständiga namn.</li><li>`phone`: ([Telefonnummer](../../data-types/phone-number.md)) Assistentens telefonnummer.</li></ul> |
| `extendedWorkDetails.departments` | Array med strängar | En lista med avdelningsnamn där personen arbetar. |
| `extendedWorkDetails.jobTitle` | Sträng | Personens befattning. |
| `extendedWorkDetails.photoUrl` | Sträng | En URL till ett foto av personen. |
| `extendedWorkDetails.reportsToID` | Sträng | En identifierare för personens rapporthanterare. |
| `faxPhone` | [Telefonnummer](../../data-types/phone-number.md) | Personens faxnummer. |
| `homeAddress` | [Postadress](../../data-types/postal-address.md) | Personens hemadress. |
| `homePhone` | [Telefonnummer](../../data-types/phone-number.md) | Personens hemtelefonnummer. |
| `mobilePhone` | [Telefonnummer](../../data-types/phone-number.md) | Personens mobiltelefonnummer. |
| `otherAddress` | [Postadress](../../data-types/postal-address.md) | En alternativ adress för personen. |
| `otherPhone` | [Telefonnummer](../../data-types/phone-number.md) | Ett alternativt telefonnummer för personen. |
| `person` | [Person](../../data-types/person.md) | En enskild aktör, kontakt eller ägare. |
| `personalEmail` | [E-postadress](../../data-types/email-address.md) | Personens personliga e-postadress. |
| `workAddress` | [Postadress](../../data-types/postal-address.md) | Personens arbetsadress. |
| `workEmail` | [E-postadress](../../data-types/email-address.md) | Personens e-postadress till arbetet. |
| `workPhone` | [Telefonnummer](../../data-types/phone-number.md) | Personens telefonnummer till arbetet. |
| `identityMap` | Mappa | Ett kartfält som innehåller en uppsättning namngivna identiteter för personen. Det här fältet uppdateras automatiskt av systemet när identitetsdata hämtas. Om du vill använda det här fältet för [Kundprofil för realtid](../../../profile/home.md) ska du inte försöka uppdatera fältets innehåll manuellt i dataåtgärderna.<br /><br />Mer information om hur de används finns i avsnittet om identitetskartor i  [grunderna för ](../../schema/composition.md#identityMap) schemakompositioner. |
| `organizations` | Array med strängar | En lista med organisationsnamn där personen arbetar. |

{style=&quot;table-layout:auto&quot;}

Mer information om fältgruppen finns i den offentliga XDM-databasen:

* [Populerat exempel](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/b2b-person-details.example.1.json)
* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/b2b-person-details.schema.json)
