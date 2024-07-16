---
title: Informationsschemagrupp för sjukvårdsmedlemmar
description: Läs mer om schemafältgruppen för information om sjukvårdsmedlemmar.
exl-id: 43ba025e-2acf-4cb7-8487-e6c7c7240867
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '610'
ht-degree: 0%

---

# Schemafältgruppen [!UICONTROL Healthcare Member Details]

[!UICONTROL Healthcare Member Details] är en standardschemafältgrupp för [[!DNL XDM Individual Profile] klassen](../../classes/individual-profile.md) som samlar in information om en person som har eller kommer att få vård eller vård, t.ex. kontaktinformation, primärvårdsläkare och planinformation.

![Fältgruppsstruktur](../../images/field-groups/healthcare-member-details/structure.png)

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `billingAddress` | [[!UICONTROL Postal address]](../../data-types/postal-address.md) | Personens faktureringsadress. |
| `faxPhone` | [[!UICONTROL Phone number]](../../data-types/phone-number.md) | Personens faxnummer. |
| `homeAddress` | [[!UICONTROL Postal address]](../../data-types/postal-address.md) | Personens hemadress. |
| `homePhone` | [[!UICONTROL Phone number]](../../data-types/phone-number.md) | Personens hemtelefonnummer. |
| `mailingAddress` | [[!UICONTROL Postal address]](../../data-types/postal-address.md) | Personens postadress. |
| `memberDetails` | Objekt | Ett objekt som innehåller detaljerad information om personens vårdrelaterade attribut och relationer. Mer information om objektets struktur finns i [underavsnittet nedan](#memberDetails). |
| `mobilePhone` | [[!UICONTROL Phone number]](../../data-types/phone-number.md) | Personens mobiltelefonnummer. |
| `person` | [[!UICONTROL Person]](../../data-types/person.md) | En enskild aktör, kontakt eller ägare som är kopplad till personens medlemskap i hälsovård. |
| `personalEmail` | [[!UICONTROL Email address]](../../data-types/email-address.md) | Personens personliga e-postadress. |
| `shippingAddress` | [[!UICONTROL Postal address]](../../data-types/postal-address.md) | Personens leveransadress. |

{style="table-layout:auto"}

## `memberDetails` {#memberDetails}

`memberDetails` är ett objekt som innehåller detaljerad information om personens hälsorelaterade attribut och relationer. Strukturen för `memberDetails` beskrivs nedan.

![MemberDetails-struktur](../../images/field-groups/healthcare-member-details/memberDetails.png)

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `emergencyContact` | Objekt | Hämtar följande kontaktuppgifter för nödsituationer för personen: <ul><li>`fullName`: (String) Det fullständiga namnet på nödkontakten.</li><li>`phone`: (String) Telefonnumret för nödkontakten.</li><li>`relationshipToMember`: (Sträng) Den nödlidande kontaktens relation till personen.</li></ul> |
| `medications` | Array med objekt | Visar information om aktuella och tidigare läkemedel som är associerade med personen. Varje arrayobjekt är ett objekt som fångar följande information: <ul><li>`refillLocation`: ([[!UICONTROL Postal address]](../../data-types/postal-address.md)) Återfyllningsplatsen för medicineringen.</li><li>`ID`: (Sträng) Medicin-ID.</li><li>`isCurrent`: (Boolean) Anger om medicineringen är aktuell eller förbi.</li><li>`numberOfRefills`: (heltal) Antal påfyllningar som föreskrivs av leverantören av det här läkemedlet.</li><li>`startDate`: (DateTime) Det datum då personen började ta medicinen.</li></ul> |
| `multipleBirth` | Objekt | Hämtar information om flera födslar: <ul><li>`isMultipleBirth`: (Boolean) Anger om personen gav flera födslar.</li><li>`multipleBirthNumber`: (heltal) Antalet spädbarn som föds om `isMultipleBirth` är sant.</li></ul> |
| `plans` | Array med objekt | Visar information om aktuella och tidigare medicinska planer som är kopplade till personen. Varje arrayobjekt är ett objekt som fångar följande information: <ul><li>`coverageEndDate`: (DateTime) Det datum då plandisponeringen upphör.</li><li>`coverageStartDate`: (DateTime) Det datum då plandisponeringen börjar.</li><li>`isActive`: (Boolean) Anger om planen är aktiv.</li><li>`planId`: (Sträng) Planens ID.</li></ul> |
| `primaryCarePhysicians` | Array med objekt | Visar information om förste vårdläkare som är associerad med personen. Varje arrayobjekt är ett objekt som fångar följande information: <ul><li>`endDate`: (DateTime) Det datum då den primära vårdläkaren slutade ta hand om personen.</li><li>`fullname`: (String) Det fullständiga namnet på läkaren.</li><li>`providerId`: (String) En unik identifierare för läkaren.</li><li>`startDate`: (DateTime) Det datum då den primära vårdläkaren började ta hand om personen.</li></ul> |
| `specialists` | Array med objekt | Visar information om hälso- och sjukvårdsspecialister som är associerade med personen. Varje arrayobjekt är ett objekt som fångar följande information: <ul><li>`fullname`: (String) Det fullständiga namnet på specialisten.</li><li>`providerId`: (String) En unik identifierare för specialisten.</li><li>`specialty`: (String) Leverantörens specialitet (t.ex. anestesiologi, urologi, radiologi, dermatologi).</li></ul> |
| `beneficiaryRelationship` | Sträng | Förmånsförhållandet till vårdmedlemmen om personen är beroende (exempel är sig själv, make, barn, osv.). |
| `billingAccountID` | Sträng | En unik identifierare för personens faktureringskonto. |
| `dateAgeCollected` | DateTime | Datumet då personens ålder samlades in. |
| `deceasedDate` | DateTime | Datumet då personen dog om de avled. |
| `isDeceased` | Boolean | Anger om personen är avliden. |
| `isDependent` | Boolean | Anger om personen är beroende. |
| `nationality` | Sträng | Det rättsliga förhållandet mellan personen och deras stat, representerat med ISO 3166-1 Alpha-2-koden. |
| `preferredAvailability` | Sträng | Personens önskade tillgänglighet för dag och tid för ett möte. |
| `primaryMemberID` | Sträng | En unik identifierare för den primära prenumeranten om personen är beroende. |

{style="table-layout:auto"}

Mer information om fältgruppen finns i den offentliga XDM-databasen:

* [Populerat exempel](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-healthcare-member.example.1.json)
* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-healthcare-member.schema.json)

Mer information om hur den här fältgruppen kan användas för att hantera vanliga [användningsfall inom hälso- och sjukvården](../../schema/industries/healthcare.md) finns i dokumentationen till branschschemat.
