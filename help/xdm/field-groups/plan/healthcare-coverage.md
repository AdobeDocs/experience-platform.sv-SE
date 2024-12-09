---
title: Fältgrupp för täckningsschema
description: Lär dig mer om fältgruppen Täckningsschema.
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: 7d33c5474629b2b02c19e752cdf2cb0a2ba19f19
workflow-type: tm+mt
source-wordcount: '679'
ht-degree: 0%

---

# Schemafältgruppen [!UICONTROL Coverage]

[!UICONTROL Coverage] är en standardschemafältgrupp för [[!DNL Plan] klassen](../../classes/plan.md). Det tillhandahåller ett enda fält av objekttyp `healthcareCoverage` som är avsett att tillhandahålla identifierare och beskrivare på hög nivå för en försäkringsplan, vanligtvis den information som skulle finnas på ett försäkringskort, som kan användas för att delvis eller helt betala för tillhandahållande av hälso- och sjukvårdsprodukter och -tjänster.

![Fältgruppsstruktur](../../images/field-groups/healthcare-coverage/coverage.png)

| Visningsnamn | Egenskap | Datatyp | Beskrivning |
| --- | --- | --- | --- |
| [!UICONTROL Plan Beneficiary] | `beneficiary` | [[!UICONTROL Reference]](../../data-types/healthcare/reference.md) | Den part som drar nytta av försäkringsskyddet och patienten när produkter eller tjänster tillhandahålls. |
| [!UICONTROL Class] | `class` | Array med objekt | En serie med underskriftsspecifika klassificerare. Mer information finns i avsnittet [nedan](#class). |
| [!UICONTROL Contact] | `contract` | Array med [[!UICONTROL Reference]](../../data-types/healthcare/reference.md) | Försäkringar som utgör denna försäkring. |
| [!UICONTROL Cost To Beneficiary] | `costToBeneficiary` | Array med objekt | En uppsättning koder som anger kostnadskategori och tillhörande belopp som har beskrivits i policyn och som kan ha inkluderats på hälsokortet. Mer information finns i avsnittet [nedan](#cost-to-beneficiary). |
| [!UICONTROL Exception] | `exception` | Array med objekt | En uppsättning koder som anger undantag eller minskningar av patientkostnader och deras giltighetsperioder. Mer information finns i avsnittet [nedan](#exception). |
| [!UICONTROL Identifier] | `identifier` | Array med [[!UICONTROL Identifier]](../../data-types/healthcare/identifier.md) | Identifieraren för försäkringsskyddet som det utfärdats av försäkringsgivaren. |
| [!UICONTROL Insurance Plan] | `insurancePlan` | [[!UICONTROL Reference]](../../data-types/healthcare/reference.md) | Försäkringsplanens detaljer, förmåner och kostnader som utgör denna försäkring. |
| [!UICONTROL Insurer] | `insurer` | [[!UICONTROL Reference]](../../data-types/healthcare/reference.md) | Det program eller den plan som är underskribent, betalare eller försäkringsbolag. |
| [!UICONTROL Payment By] | `paymentBy` | Array med objekt | Länken till den betalande parten och, om så önskas, vad de ska betala. Mer information finns i avsnittet [nedan](#payment-by). |
| [!UICONTROL Coverage Start And End Dates] | `period` | [[!UICONTROL Period]](../../data-types/healthcare/period.md) | Den tidsperiod under vilken täckningen är aktiv. Ett saknat startdatum anger att startdatumet inte är känt, ett saknat slutdatum innebär att disponeringen pågår. |
| [!UICONTROL Policy Holder] | `policyHolder` | [[!UICONTROL Reference]](../../data-types/healthcare/reference.md) | Den part som har försäkringsavtalet. |
| [!UICONTROL Beneficiary Relationship] | `relationship` | [[!UICONTROL Codeable Concept]](../../data-types/healthcare/codeable-concept.md) | Mottagarens förhållande till abonnenten. |
| [!UICONTROL Subscriber] | `subscriber` | [[!UICONTROL Reference]](../../data-types/healthcare/reference.md) | Den part som har avtalsförhållandet till policyn. |
| [!UICONTROL Subscriber Identifier] | `subscriberId` | Array med [[!UICONTROL Identifier]](../../data-types/healthcare/identifier.md) | Abonnentens ID har tilldelats av försäkringsgivaren. |
| [!UICONTROL Type] | `type` | [[!UICONTROL Codeable Concept]](../../data-types/healthcare/codeable-concept.md) | Typ av täckning. |
| [!UICONTROL Dependent Number] | `dependent` | Sträng | Designern för ett beroende under täckningen. |
| [!UICONTROL Kind] | `kind` | Sträng | Typ av täckning. Värdet för den här egenskapen måste vara lika med ett av följande kända enum-värden. <li> `insurance` </li> <li> `self-pay` </li> <li> `other` </li> |
| [!UICONTROL Insurer Network] | `network` | Sträng | Nätverket av leverantörer som stödmottagaren kan ansöka om behandling som omfattas av näträntan, i annat fall gäller villkor som inte är nätbaserade. |
| [!UICONTROL Coverage Order] | `order` | Heltal | Den relativa ordningen för disponeringen, med ett lägsta värde på `0`. |
| [!UICONTROL Status] | `status` | Sträng | Status för disponeringen. Värdet för den här egenskapen måste vara lika med ett av följande kända enum-värden. <li> `active` </li> <li> `cancelled` </li> <li> `draft` </li> <li> `entered-in-error` </li> |
| [!UICONTROL Subrogation] | `subrogation` | Boolean | När `true` har den här försäkringsinstansen inkluderats, inte för bedömning, utan för att ge försäkringsbolagen de uppgifter de behöver för att få ersättning för kostnader. |

Mer information om fältgruppen finns i den offentliga XDM-databasen:

* [Populerat exempel](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/coverage.example.1.json)
* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/coverage.schema.json)

## `class` {#class}

`class` tillhandahålls som en array med objekt. Strukturen för varje objekt beskrivs nedan.

![Klassstruktur](../../images/field-groups/healthcare-coverage/class.png)

| Visningsnamn | Egenskap | Datatyp | Beskrivning |
| --- | --- | --- | --- |
| [!UICONTROL Type] | `type` | Array med [[!UICONTROL Codeable Concept]](../../data-types/healthcare/codeable-concept.md) | Den typ av klassificering som en försäkringsgivarspecifik klassetikett, eller ett nummer och valfritt namn, anges för. Typ kan till exempel användas för att identifiera en klass av täckning, arbetsgivargrupp, policy eller plan. |
| [!UICONTROL Value] | `value` | [[!UICONTROL Identifier]](../../data-types/healthcare/identifier.md) | Den alfanumeriska identifierare som är associerad med den etikett som försäkringsgivaren utfärdat. |
| [!UICONTROL Name] | `name` | Sträng | En kort beskrivning av klassen. |

## `costToBeneficiary` {#cost-to-beneficiary}

`costToBeneficiary` tillhandahålls som en array med objekt. Strukturen för varje objekt beskrivs nedan.

![Kostnad för mottagarstruktur](../../images/field-groups/healthcare-coverage/cost-to-beneficiary.png)

| Visningsnamn | Egenskap | Datatyp | Beskrivning |
| --- | --- | --- | --- |
| [!UICONTROL Category] | `category` | [[!UICONTROL Codeable Concept]](../../data-types/healthcare/codeable-concept.md) | Koden för att identifiera den allmänna typen av förmåner som produkter och tjänster tillhandahålls under. |
| [!UICONTROL Network] | `network` | [[!UICONTROL Codeable Concept]](../../data-types/healthcare/codeable-concept.md) | Koden som anger om förmånerna avser leverantörer i nätverket eller utanför nätverket. |
| [!UICONTROL Term] | `term` | [[!UICONTROL Codeable Concept]](../../data-types/healthcare/codeable-concept.md) | Löptiden för värdena, till exempel den maximala livstidsförmånen. |
| [!UICONTROL Type] | `type` | [[!UICONTROL Codeable Concept]](../../data-types/healthcare/codeable-concept.md) | Kategorin patientcentrerade kostnader för behandlingen. |
| [!UICONTROL Unit] | `unit` | [[!UICONTROL Codeable Concept]](../../data-types/healthcare/codeable-concept.md) | Anger om förmånerna gäller för en individ eller för familjen. |

## `exception` {#exception}

`exception` tillhandahålls som en array med objekt. Strukturen för varje objekt beskrivs nedan.

![Undantagsstruktur](../../images/field-groups/healthcare-coverage/exception.png)

| Visningsnamn | Egenskap | Datatyp | Beskrivning |
| --- | --- | --- | --- |
| [!UICONTROL Type] | `type` | [[!UICONTROL Codeable Concept]](../../data-types/healthcare/codeable-concept.md) | Koden för det specifika undantaget. |
| [!UICONTROL Period] | `period` | [[!UICONTROL Period]](../../data-types/healthcare/period.md) | Tidsramen som undantaget är aktivt. |

## `paymentBy` {#payment-by}

`paymentBy` tillhandahålls som en array med objekt. Strukturen för varje objekt beskrivs nedan.

![Betalning med struktur](../../images/field-groups/healthcare-coverage/payment-by.png)

| Visningsnamn | Egenskap | Datatyp | Beskrivning |
| --- | --- | --- | --- |
| [!UICONTROL Party] | `party` | [[!UICONTROL Reference]](../../data-types/healthcare/reference.md) | Förteckningen över parter som tillhandahåller icke-försäkringsbetalningar för behandlingskostnaderna. |
| [!UICONTROL Responsibility] | `responsibility` | Sträng | Beskrivning av det ekonomiska ansvaret. |
