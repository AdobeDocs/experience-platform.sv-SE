---
title: Fältgrupp för kontoschema
description: Läs mer om fältgruppen för kontoschema.
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: 376716bd-f79f-421d-b163-0f0e50876b48
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '847'
ht-degree: 0%

---

# Schemafältgruppen [!UICONTROL Account]

[!UICONTROL Account] är en standardschemafältgrupp för [[!DNL XDM Individual Profile] klassen](../../../classes/individual-profile.md) och [[!DNL Provider class]](../../../classes/provider.md). Det tillhandahåller ett enda objekttypsfält `healthcareAccount` som används för att registrera transaktioner, tjänster och annan ekonomisk information som rör hälso- och sjukvårdstjänster som tillhandahålls en patient eller en grupp individer (t.ex. för en försäkring eller faktureringsändamål).

![Fältgruppsstruktur](../../../images/healthcare/field-groups/account/account.png)

| Visningsnamn | Egenskap | Datatyp | Beskrivning |
| --- | --- | --- | --- |
| [!UICONTROL Balance] | `balance` | Array med objekt | Kontosaldon som beräknas och behandlas av finanssystemet. Mer information finns i avsnittet [nedan](#balances). |
| [!UICONTROL Billing Status] | `billingStatus` | [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md) | Detta spårar kontots livscykel genom faktureringsprocessen. Den visar hur transaktioner behandlas när de tilldelas till kontot. |
| [!UICONTROL Coverage] | `coverage` | Array med objekt | Den eller de parter som ansvarar för att täcka kostnaderna för detta konto och i vilken ordning de ska tillämpas. Mer information finns i avsnittet [nedan](#coverage). |
| [!UICONTROL Currency] | `currency` | [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md) | Standardvalutan för kontot. |
| [!UICONTROL Diagnosis] | `diagnosis` | Array med objekt | De diagnoser som är relevanta för fakturering lagras här på kontot där de kan sekventieras korrekt före bearbetning för att skapa krav. Mer information finns i avsnittet [nedan](#diagnosis). |
| [!UICONTROL Guarantor] | `guarantor` | Array med objekt | De parter som ansvarar för att balansera kontot om andra betalningsalternativ är otillräckliga. Mer information finns i avsnittet [nedan](#guarantor). |
| [!UICONTROL Identifier] | `identifier` | Array med [[!UICONTROL Identifier]](../data-types/identifier.md) | En unik identifierare som används för att referera till kontot. Den får vara avsedd för användning på människor (t.ex. kreditkortsnummer). |
| [!UICONTROL Owner] | `owner` | [[!UICONTROL Reference]](../data-types/reference.md) | Anger serviceområde, sjukhus, avdelning osv. med ansvar för att hantera kontot. |
| [!UICONTROL Procedure] | `procedure` | Array med objekt | De förfaranden som är relevanta för fakturering lagras här på det konto där de kan sekventieras korrekt före bearbetning för att framställa krav. Mer information finns i avsnittet [nedan](#procedure). |
| [!UICONTROL Related Account] | `relatedAccount` | Array med objekt | Andra associerade konton som hör till det här kontot. Mer information finns i avsnittet [nedan](#related-account). |
| [!UICONTROL Service Period] | `servicePeriod` | [[!UICONTROL Period]](../data-types/period.md) | Datumintervallet för tjänster som är associerade med det här kontot. |
| [!UICONTROL Subject] | `subject` | Array med [[!UICONTROL Reference]](../data-types/reference.md) | Identifierar det företag som ådrar sig utgifterna. Även om de omedelbara mottagarna av tjänster eller varor kan vara enheter med anknytning till föremålet, åsamkades kostnaderna av föremålet för kontot. |
| [!UICONTROL Type] | `type` | [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md) | Kategoriserar kontot för rapportering och sökning. |
| [!UICONTROL Calculated At] | `calculatedAt` | DateTime | Den tidpunkt då saldot beräknades. |
| [!UICONTROL Description] | `description` | Sträng | Ger ytterligare information om vad kontot spårar och hur det används. |
| [!UICONTROL Name] | `name` | Sträng | Kontots namn. |
| [!UICONTROL Status] | `status` | Sträng | Kontots status. Värdet för den här egenskapen måste vara lika med ett av följande kända enum-värden. <li> `active` </li> <li> `inactive` </li> <li> `entered-in-error` </li> <li> `on-hold` </li> <li> `unknown`</li> |

Mer information om fältgruppen finns i den offentliga XDM-databasen:

* [Populerat exempel](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/account.example.1.json)
* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/account.schema.json)

## `balances` {#balances}

`balances` tillhandahålls som en array med objekt. Strukturen för varje objekt beskrivs nedan.

![saldostruktur](../../../images/healthcare/field-groups/account/balance.png)

| Visningsnamn | Egenskap | Datatyp | Beskrivning |
| --- | --- | --- | --- |
| [!UICONTROL Aggregate] | `aggregate` | [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md) | Vem förväntas betala denna del av saldot. |
| [!UICONTROL Amount] | `amount` | [[!UICONTROL Money]](../data-types/money.md) | Det faktiska saldot som beräknas för den ålder som definieras i termen egenskap. |
| [!UICONTROL Term] | `term` | [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md) | Kontots löptid. |
| [!UICONTROL Estimate] | `estimate` | Boolean | Om beloppet är ett uppskattat värde. |

## `coverage` {#coverage}

`coverage` tillhandahålls som en array med objekt. Strukturen för varje objekt beskrivs nedan.

![täckningsstruktur](../../../images/healthcare/field-groups/account/coverage.png)

| Visningsnamn | Egenskap | Datatyp | Beskrivning |
| --- | --- | --- | --- |
| [!UICONTROL Coverage] | `coverage` | [[!UICONTROL Reference]](../data-types/reference.md) | Den eller de parter som ansvarar för att täcka kostnaderna för detta konto och i vilken ordning de ska tillämpas. |
| [!UICONTROL Priority] | `priority` | Heltal | Täckningens prioritet i kontexten för det här kontot, med ett minimivärde på `0`. |

## `diagnosis` {#diagnosis}

`diagnosis` tillhandahålls som en array med objekt. Strukturen för varje objekt beskrivs nedan.

![diagnosstruktur](../../../images/healthcare/field-groups/account/diagnosis.png)

| Visningsnamn | Egenskap | Datatyp | Beskrivning |
| --- | --- | --- | --- |
| [!UICONTROL Condition] | `condition` | [[!UICONTROL Codeable Reference]](../data-types/codeable-reference.md) | Den diagnos som är relevant för kontot. |
| [!UICONTROL Package Code] | `packageCode` | Array med [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md) | Paketkoden kan användas för att gruppera diagnoser som kan prissättas eller levereras som en enskild produkt (t.ex. DRG). |
| [!UICONTROL Type] | `type` | Array med [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md) | Typ av diagnos som är relevant för kontot (t.ex. registrering, fakturering, utskrivning ...). |
| [!UICONTROL Date Of Diagnosis] | `dateOfDiagnosis` | DateTime | Datum för diagnosen (vid kodad diagnos). |
| [!UICONTROL On Admission] | `onAdmission` | Boolean | Anger om diagnosen fanns vid anslutningen. |
| [!UICONTROL Squence] | `sequence` | Heltal | Diagnostikrankningen (för varje typ), med ett minimivärde på `0`. |

## `guarantor` {#guarantor}

`guarantor` tillhandahålls som en array med objekt. Strukturen för varje objekt beskrivs nedan.

![garantigivarstruktur](../../../images/healthcare/field-groups/account/guarantor.png)

| Visningsnamn | Egenskap | Datatyp | Beskrivning |
| --- | --- | --- | --- |
| [!UICONTROL Party] | `party` | [[!UICONTROL Reference]](../data-types/reference.md) | Den enhet som är ansvarig. |
| [!UICONTROL Period] | `period` | [[!UICONTROL Period]](../data-types/period.md) | Den tidsram inom vilken borgensmannen tar ansvar för kontot. |
| [!UICONTROL On Hold] | `onHold` | Boolean | En borgensman kan spärra krediten eller på annat sätt tillfälligt upphäva sin roll. |

## `procedure` {#procedure}

`procedure` tillhandahålls som en array med objekt. Strukturen för varje objekt beskrivs nedan.

![procedurstruktur](../../../images/healthcare/field-groups/account/procedure.png)

| Visningsnamn | Egenskap | Datatyp | Beskrivning |
| --- | --- | --- | --- |
| [!UICONTROL Code] | `code` | [[!UICONTROL Codeable Reference]](../data-types/codeable-reference.md) | Det förfarande som är relevant för kontot. |
| [!UICONTROL Device] | `device` | Array med [[!UICONTROL Reference]](../data-types/reference.md) | Alla enheter som var kopplade till proceduren som är relevant för kontot. |
| [!UICONTROL Type] | `type` | Array med [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md) | Hur procedurvärdet ska användas vid debitering av kontot. |
| [!UICONTROL Package Code] | `packageCode` | Array med [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md) | Paketkoden kan användas för att gruppera procedurer som kan prissättas eller levereras som en enskild produkt (t.ex. DRG). |
| [!UICONTROL Date Of Service] | `dateOfService` | DateTime | Datumet när en kodad procedur används. Om en hänvisning till ett förfarande används, skall datumet för förfarandet användas. |
| [!UICONTROL Sequence] | `sequence` | Heltal | Rankning av proceduren (för varje typ), med ett minsta värde på `0`. |

## `relatedAccount` {#related-account}

`relatedAccount` tillhandahålls som en array med objekt. Strukturen för varje objekt beskrivs nedan.

![relatedAccount-struktur](../../../images/healthcare/field-groups/account/related-account.png)

| Visningsnamn | Egenskap | Datatyp | Beskrivning |
| --- | --- | --- | --- |
| [!UICONTROL Account] | `account` | [[!UICONTROL Reference]](../data-types/reference.md) | Referens till ett associerat konto. |
| [!UICONTROL Relationship] | `relationship` | [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md) | Relation för det associerade kontot. |
