---
title: Sjukvårdsleverantörens schemafältgrupp
description: Läs mer om schemafältgruppen för vårdgivare.
exl-id: e39b4082-4b66-47b3-a8e2-951d8a96f742
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '239'
ht-degree: 0%

---

# [!UICONTROL Healthcare Provider] schemafältgrupp

[!UICONTROL Healthcare Provider] är en standardgrupp för schemafält för [[!UICONTROL Provider] class](../../classes/provider.md). Det innehåller ett enda objekttypsfält `healthcareProvider` som innehåller egendomar som är knutna till en enskild hälso- och sjukvårdspersonal eller en sjukvårdsorganisation som är licensierad att tillhandahålla hälso- och sjukvårdsdiagnos och behandlingstjänster.

![](../../images/field-groups/healthcare-provider.png)

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `addressDetails` | Array med objekt | Visar adressinformation för providern. Varje objekt innehåller följande egenskaper: <ul><li>`address`: ([[!UICONTROL Postal address]](../../data-types/postal-address.md)): Leverantörens postadress.</li><li>`addressType`: (String) Adresstypen som anger var leverantören tillhandahåller tjänster.</li></ul> |
| `emailAddress` | [[!UICONTROL Email address]](../../data-types/email-address.md) | Leverantörens e-postadress. |
| `fax` | [[!UICONTROL Phone number]](../../data-types/phone-number.md) | Leverantörens faxnummer. |
| `phoneNumber` | [[!UICONTROL Phone number]](../../data-types/phone-number.md) | Leverantörens telefonnummer. |
| `qualifications` | Array med objekt | Visar en lista över certifikat, licenser eller utbildning som gäller vård. Varje objekt innehåller följande egenskaper: <ul><li>`issuer`: ([[!UICONTROL Account details]](../../data-types/account-details.md)): Organisationen som reglerar och utfärdar kvalifikationen.</li><li>`activePeriod`: (heltal) Det år till vilket kvalificeringen är giltig.</li><li>`code`: (String) En kodad representation av kvalificeringen.</li></ul> |
| `classification` | Sträng | Tjänsteleverantörens klassificering baserad på klass eller kategori (t.ex. patientvård, annan vård osv.). |
| `isActive` | Boolean | Anger om providern är aktiv. |
| `languages` | Array med strängar | En lista med språk som providern utför åtgärder under. |
| `practiceGroupName` | Sträng | Tjänstleverantörens namn på övningsgruppen. |
| `practiceGroupType` | Sträng | Typ av övningsgrupp för tjänsteleverantören. |
| `practiceType` | Sträng | Praktiktypen för tjänsteleverantören. |
| `specialties` | Array med strängar | En lista över specialerbjudanden från den här leverantören. |

{style="table-layout:auto"}

Mer information om fältgruppen finns i [publik XDM-databas](https://github.com/adobe/xdm/blob/master/components/fieldgroups/provider/healthcare-provider-details.schema.json).
