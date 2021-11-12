---
title: XDM Business Person Components Schemafältgrupp
description: Det här dokumentet innehåller en översikt över schemafältgruppen XDM Business Person Components.
exl-id: 965b89f4-59f5-43f4-8778-3549e15b44d4
source-git-commit: edf7afc5db219430232a3226dc691570b50a32bd
workflow-type: tm+mt
source-wordcount: '390'
ht-degree: 2%

---

# [!UICONTROL XDM Business Person Components] schemafältgrupp

[!UICONTROL XDM Business Person Components] är en standardgrupp för schemafält för [[!DNL XDM Individual Profile] class](../../classes/individual-profile.md) som samlar in flera källposter för en person och andra attribut som krävs för personsegmentering.

När en profil skapas för en person via [Kundprofil i realtid](../../../profile/home.md) i B2B-utgåvan av CDP i realtid kan informationen som används för att skapa profilen komma från många källposter. Om en person till exempel arbetar för två olika företag skulle många CRM-system skapa en avsiktligt duplicerad kopia av den personen så att den ena kopian är länkad till företag A, medan den andra är länkad till företag B. När du hämtar dessa data till Adobe Experience Platform används den här fältgruppen för att sammanfoga de olika källposterna till en enda representation.

Fältgruppen har en rotnivå `personComponents` field, som är en array med objekt. Varje objekt i arrayen representerar en annan källpost.

![](../../images/field-groups/business-person-components.png)

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `sourceAccountKey` | [[!UICONTROL B2B Source]](../../data-types/b2b-source.md) | En sammansatt identifierare för det konto som är associerat med personen. |
| `sourceConvertedContactKey` | [[!UICONTROL B2B Source]](../../data-types/b2b-source.md) | En sammansatt identifierare för den relaterade kontakten om denna lead konverterades. |
| `sourceExternalKey` | [[!UICONTROL B2B Source]](../../data-types/b2b-source.md) | En sammansatt identifierare för det källsystem som persondata kommer från. |
| `sourcePersonKey` | [[!UICONTROL B2B Source]](../../data-types/b2b-source.md) | En sammansatt identifierare för personen. |
| `workEmail` | [[!UICONTROL Email address]](../../data-types/b2b-source.md) | Personens e-postadress till arbetet. |
| `personGroupID` | Sträng | En gruppidentifierare för personen. |
| `personScore` | Sträng | En poäng som genererats för personen av ett CRM-system. |
| `personSource` | Sträng | En unik strängbaserad identifierare för det källsystem som persondata härstammar från. |
| `personStatus` | Sträng | Personens aktuella marknadsförings- eller försäljningsstatus. |
| `personType` | Sträng | Typ av person i ett B2B-sammanhang. |
| `sourceAccountID` | Sträng | En unik strängbaserad identifierare för kontot i det källsystem som är associerat med personen. Det här fältet används som en sekundärnyckel av systemet för att hitta de olika företag som den här personen arbetar för. |
| `sourceConvertedContactID` | Sträng | En unik strängbaserad identifierare för den relaterade kontakten om denna lead konverterades. |
| `sourceExternalID` | Sträng | En unik strängbaserad identifierare för det källsystem som persondata härstammar från. |
| `sourcePersonID` | Sträng | En unik strängbaserad identifierare för personen. |

{style=&quot;table-layout:auto&quot;}

Mer information om fältgruppen finns i den offentliga XDM-databasen:

* [Populerat exempel](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/b2b-person-components.example.1.json)
* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/b2b-person-components.schema.json)
