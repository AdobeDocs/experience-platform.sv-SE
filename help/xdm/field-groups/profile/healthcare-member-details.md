---
title: Informationsschemagrupp för sjukvårdsmedlemmar
description: Det här dokumentet innehåller en översikt över schemafältgruppen för information om sjukvårdsmedlemmar.
exl-id: 43ba025e-2acf-4cb7-8487-e6c7c7240867
source-git-commit: 2fd35c4ac29f43391f9dc03c636d20558b701be7
workflow-type: tm+mt
source-wordcount: '630'
ht-degree: 1%

---

# [!UICONTROL Healthcare Member Details] schemafältgrupp

[!UICONTROL Healthcare Member Details] är en standardgrupp för schemafält för [[!DNL XDM Individual Profile] class](../../classes/individual-profile.md) som innehåller uppgifter om en person som har eller kommer att få vård eller vård, såsom kontaktinformation, primärvårdsläkare och planinformation.

![Fältgruppstruktur](../../images/field-groups/healthcare-member-details/structure.png)

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `billingAddress` | [[!UICONTROL Postal address]](../../data-types/postal-address.md) | Personens faktureringsadress. |
| `faxPhone` | [[!UICONTROL Phone number]](../../data-types/phone-number.md) | Personens faxnummer. |
| `homeAddress` | [[!UICONTROL Postal address]](../../data-types/postal-address.md) | Personens hemadress. |
| `homePhone` | [[!UICONTROL Phone number]](../../data-types/phone-number.md) | Personens hemtelefonnummer. |
| `mailingAddress` | [[!UICONTROL Postal address]](../../data-types/postal-address.md) | Personens postadress. |
| `memberDetails` | Objekt | Ett objekt som innehåller detaljerad information om personens vårdrelaterade attribut och relationer. Se [underavsnitt nedan](#memberDetails) om du vill ha mer information om objektets struktur. |
| `mobilePhone` | [[!UICONTROL Phone number]](../../data-types/phone-number.md) | Personens mobiltelefonnummer. |
| `person` | [[!UICONTROL Person]](../../data-types/person.md) | En enskild aktör, kontakt eller ägare som är kopplad till personens medlemskap i hälso- och sjukvården. |
| `personalEmail` | [[!UICONTROL Email address]](../../data-types/email-address.md) | Personens personliga e-postadress. |
| `shippingAddress` | [[!UICONTROL Postal address]](../../data-types/postal-address.md) | Personens leveransadress. |

{style="table-layout:auto"}

## `memberDetails` {#memberDetails}

`memberDetails` är ett objekt som innehåller detaljerad information om personens hälsorelaterade attribut och relationer. Strukturen för `memberDetails` beskrivs nedan.

![memberDetails-struktur](../../images/field-groups/healthcare-member-details/memberDetails.png)

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `emergencyContact` | Objekt | Hämtar följande kontaktuppgifter för nödsituationer för personen: <ul><li>`fullName`: (String) Det fullständiga namnet på nödkontakten.</li><li>`phone`: (String) Telefonnumret till nödkontakten.</li><li>`relationshipToMember`: (String) Nödkontakten har en relation till personen.</li></ul> |
| `medications` | Array med objekt | Visar information om aktuella och tidigare läkemedel som är associerade med personen. Varje arrayobjekt är ett objekt som fångar följande information: <ul><li>`refillLocation`: ([[!UICONTROL Postal address]](../../data-types/postal-address.md)) Återfyllningsplatsen för medicineringen.</li><li>`ID`: (String) Medication-ID.</li><li>`isCurrent`: (Boolean) Anger om medicineringen är pågående eller förbi.</li><li>`numberOfRefills`: (Heltal) Antal påfyllningar som föreskrivs av läkemedelsleverantören.</li><li>`startDate`: (DateTime) Det datum då personen började ta medicinen.</li></ul> |
| `multipleBirth` | Objekt | Hämtar information om flera födslar: <ul><li>`isMultipleBirth`: (Boolean) Anger om personen har fött flera personer.</li><li>`multipleBirthNumber`: (heltal) Antalet spädbarn som föds om `isMultipleBirth` är sant.</li></ul> |
| `plans` | Array med objekt | Visar information om aktuella och tidigare medicinska planer som är kopplade till personen. Varje arrayobjekt är ett objekt som fångar följande information: <ul><li>`coverageEndDate`: (DateTime) Det datum då plandisponeringen upphör.</li><li>`coverageStartDate`: (DateTime) Det datum då plandisponeringen börjar.</li><li>`isActive`: (Boolean) Anger om planen är aktiv.</li><li>`planId`: (String) Planens ID.</li></ul> |
| `primaryCarePhysicians` | Array med objekt | Visar information om förste vårdläkare som är associerad med personen. Varje arrayobjekt är ett objekt som fångar följande information: <ul><li>`endDate`: (DatumTid) Det datum då den primära läkaren avslutade sin vård för personen.</li><li>`fullname`: (String) Läkarens fullständiga namn.</li><li>`providerId`: (String) En unik identifierare för läkaren.</li><li>`startDate`: (DateTime) Det datum då den förste omvårdnadsläkaren började vårda personen.</li></ul> |
| `specialists` | Array med objekt | Visar information om hälso- och sjukvårdsspecialister som är associerade med personen. Varje arrayobjekt är ett objekt som fångar följande information: <ul><li>`fullname`: (String) Det fullständiga namnet på specialisten.</li><li>`providerId`: (String) En unik identifierare för specialisten.</li><li>`specialty`: (String) Leverantörens specialitet (t.ex. anestesiologi, urologi, radiologi, dermatologi).</li></ul> |
| `beneficiaryRelationship` | Sträng | Förmånsförhållandet till vårdmedlemmen om personen är beroende (exempel är sig själv, make, barn, osv.). |
| `billingAccountID` | Sträng | En unik identifierare för personens faktureringskonto. |
| `dateAgeCollected` | DateTime | Datumet då personens ålder samlades in. |
| `deceasedDate` | DateTime | Datumet då personen dog om de avled. |
| `isDeceased` | Boolean | Anger om personen är avliden. |
| `isDependent` | Boolean | Anger om personen är beroende. |
| `nationality` | Sträng | Det rättsliga förhållandet mellan personen och deras stat, representerat med ISO 3166-1 Alpha-2-koden. |
| `preferredAvailability` | Sträng | Personens önskade tillgänglighet för dag och tid för en avtalad tid. |
| `primaryMemberID` | Sträng | En unik identifierare för den primära prenumeranten om personen är beroende. |

{style="table-layout:auto"}

Mer information om fältgruppen finns i den offentliga XDM-databasen:

* [Populerat exempel](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-healthcare-member.example.1.json)
* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-healthcare-member.schema.json)

Mer information om hur den här fältgruppen kan användas för att hantera vanliga funktioner finns i dokumentationen till branschschemat. [användningsfall inom hälso- och sjukvården](../../schema/industries/healthcare.md).
