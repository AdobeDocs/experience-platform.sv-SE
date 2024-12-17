---
title: Fältgrupp för avtalat schema
description: Lär dig mer om schemafältgruppen Möte.
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: 2a58f6f1663e95c1c7576cd4909fa937b41ae099
workflow-type: tm+mt
source-wordcount: '1089'
ht-degree: 0%

---

# Schemafältgruppen [!UICONTROL Appointment]

[!UICONTROL Appointment] är en standardschemafältgrupp för [[!DNL XDM Individual Profile] klassen](../../../classes/individual-profile.md) och [[!DNL Provider class]](../../../classes/provider.md). Det innehåller ett enda fält av objekttyp `healthcareAppointment` som innehåller information om att boka en hälso- och sjukvårdshändelse bland patienter, läkare, närstående personer och/eller enheter för ett visst datum och tid.

![Ett schemadiagram över gruppstrukturen för det avtalade fältet.](../../../images/healthcare/field-groups/appointment/appointment.png)

| Visningsnamn | Egenskap | Datatyp | Beskrivning |
| --- | --- | --- | --- |
| [!UICONTROL Account] | `account` | Array med [[!UICONTROL Reference]](../data-types/reference.md) | Den uppsättning konton som förväntas användas för fakturering. |
| [!UICONTROL Appointment Type] | `appointmentType` | [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md) | Den typ av avtalad tid eller patient som har bokats i platsen (inte tjänstetyp). |
| [!UICONTROL Based On] | `basedOn` | Array med [[!UICONTROL Reference]](../data-types/reference.md) | Begäran som den avtalade tiden avser att bedöma, t.ex. en begäran om förfarande. |
| [!UICONTROL Cancellation Reason] | `cancellationReason` | Array med [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md) | Den kodade orsaken till den avtalade tiden annulleras. Detta används ofta vid rapportering, fakturering eller bearbetning för att avgöra om ytterligare åtgärder krävs eller om särskilda avgifter tillämpas. |
| [!UICONTROL Class] | `class` | Array med [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md) | Concepts som representerar klassificeringen av en patient stöter på t.ex. ambulatorisk, öppen patient, inpatient eller akut. |
| [!UICONTROL Identifier] | `identifier` | Array med [[!UICONTROL Identifier]](../data-types/identifier.md) | En lista med unika identifierare som är länkade till den avtalade tiden. Dessa identifierare tilldelas baserat på affärsregler eller när en direkt URL-länk till den avtalade tiden inte är lämplig. |
| [!UICONTROL Note] | `note` | Array med [[!UICONTROL Annotation]](../data-types/annotation.md) | Ytterligare anteckningar eller kommentarer om den avtalade tiden. |
| [!UICONTROL Originating Appointment] | `originatingAppointment` | [[!UICONTROL Reference]](../data-types/reference.md) | Den ursprungliga avtalade tiden i en återkommande uppsättning med relaterade avtalade tider. |
| [!UICONTROL Participant] | `participant` | Array med objekt | En lista över deltagare som deltar i den avtalade tiden. Mer information finns i avsnittet [nedan](#participant). |
| [!UICONTROL Patient Instruction] | `patientInstruction` | Array med [[!UICONTROL Codeable Reference]](../data-types/reference.md) | Diagnosen som är relevant för den avtalade tiden. |
| [!UICONTROL Previous Appointment] | `previousAppointment` | [[!UICONTROL Reference]](../data-types/reference.md) | Den föregående avtalade tiden i en serie relaterade avtalade tider. |
| [!UICONTROL Priority] | `priority` | [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md) | Prioriteten för den avtalade tiden som kan användas för att fatta välgrundade beslut om utnämningar behöver omprioriteras. iCal-standarden anger `0` som odefinierad, `1` som högsta prioritet och `9` som lägsta prioritet. |
| [!UICONTROL Reason] | `reason` | Array med [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md) | Orsaken till att den avtalade tiden schemaläggs, vilket vanligtvis är ett villkor eller en procedur. |
| [!UICONTROL Reccurence Template] | `recurrenceTemplate` | Array med objekt | Innehåller information om det återkommande mönster eller den mall som används för att skapa återkommande avtalade tider.  Mer information finns i avsnittet [nedan](#recurrence). |
| [!UICONTROL Replaces] | `replaces` | Array med [[!UICONTROL Reference]](../data-types/reference.md) | Den avtalade tid som ersätts av den här avtalade tiden. I de fall där det finns en annullering finns information om annulleringen i egenskapen `cancellationReason` för den refererade resursen. |
| [!UICONTROL Requested Period] | `requestedPeriod` | Array med [[!UICONTROL Period]](../data-types/period.md) | En uppsättning datumintervall (eventuellt inklusive tider) under vilka den avtalade tiden ska schemaläggas. |
| [!UICONTROL Service Category] | `serviceCategory` | Array med [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md) | En bred kategorisering av den tjänst som ska utföras under mötet. |
| [!UICONTROL Service Type] | `serviceType` | Array med [[!UICONTROL Codeable Reference]](../data-types/codeable-reference.md) | Den specifika tjänst som ska utföras under den avtalade tiden. |
| [!UICONTROL Slot] | `slot` | Array med [[!UICONTROL Reference]](../data-types/reference.md) | Tidsperioder från deltagarnas tidsplaner som ska fyllas i av den avtalade tiden. |
| [!UICONTROL Speciality] | `speciality` | Array med [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md) | Specialiteten för en yrkesutövare som är skyldig att utföra den tjänst som begärs i denna tid. |
| [!UICONTROL Subject] | `subject` | Array med [[!UICONTROL Reference]](../data-types/reference.md) | Patienten eller gruppen som är associerad med den avtalade tiden. |
| [!UICONTROL Supporting Information] | `supportingInformation` | Array med [[!UICONTROL Reference]](../data-types/reference.md) | Ytterligare information lämnades när mötet tillsattes för att stödja det. |
| [!UICONTROL Virtual Service] | `virtualService` | Array med [[!UICONTROL Virtual Service Detail]](../data-types/virtual-service-detail.md) | Anslutningsinformation för en virtuell tjänst, till exempel ett konferenssamtal. |
| [!UICONTROL Cancellation Date] | `cancellationDate` | DateTime | Datum och tid då den avtalade tiden annullerades. |
| [!UICONTROL Created] | `created` | DateTime | Datum och tid då den avtalade tiden skapades. |
| [!UICONTROL Description] | `description` | Sträng | En kort beskrivning av den avtalade tiden. Detaljerad eller utökad information ska placeras i fältet `note`. |
| [!UICONTROL End] | `end` | DateTime | Datum och tid då den avtalade tiden avslutas. |
| [!UICONTROL Minutes Duration] | `minutesDuration` | Heltal | Antalet minuter som den avtalade tiden ska ta. Detta kan vara mindre än längden mellan start- och sluttider. Det lägsta tillåtna värdet är `0`. |
| [!UICONTROL Occurence Changed] | `occurenceChanged` | Boolean | En flagga som anger om den här avtalade tiden skiljer sig från det återkommande mönstret. |
| [!UICONTROL RecurrenceId] | `RecurrenceId` | Heltal | Sekvensnumret som identifierar en viss avtalad tid i ett återkommande mönster. Det minsta värdet är `0`. |
| [!UICONTROL Start] | `start` | DateTime | Datum och tid då den avtalade tiden ska äga rum. |
| [!UICONTROL Status] | `status` | Sträng | Status för den avtalade tiden. Värdet för den här egenskapen måste vara lika med ett av följande kända enum-värden: <li> `proposed` </li> <li> `pending` </li> <li> `booked` </li> <li> `arrived` </li> <li> `fulfilled` </li> <li> `cancelled` </li> <li> `noshow` </li> <li> `entered-in-error` </li> <li> `checked-in` </li> <li> `waitlist` </li> |


Mer information om fältgruppen finns i den offentliga XDM-databasen:

* [Populerat exempel](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/appointment.example.1.json)
* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/appointment.schema.json)

## `participant` {#participant}

`participant` tillhandahålls som en array med objekt. Strukturen för varje objekt beskrivs nedan.

![Ett schemadiagram över deltagarobjektstrukturen.](../../../images/healthcare/field-groups/appointment/participant.png)

| Visningsnamn | Egenskap | Datatyp | Beskrivning |
| --- | --- | --- | --- |
| [!UICONTROL Actor] | `actor` | [[!UICONTROL Reference]](../data-types/reference.md) | Personen, enheten, platsen eller tjänsten som deltar i den avtalade tiden. |
| [!UICONTROL Period] | `period` | [[!UICONTROL Period]](../data-types/period.md) | Den tidsperiod under vilken deltagaren (aktören) deltar i utnämningen. |
| [!UICONTROL Type] | `type` | Array med [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md) | Deltagarens (aktörens) roll i den avtalade tiden. |
| [!UICONTROL Required] | `required` | Boolean | Anger om den här deltagaren måste vara närvarande. |
| [!UICONTROL status] | `status` | Sträng | Deltagarens godkännandestatus. Värdet för den här egenskapen måste vara lika med ett av följande kända enum-värden: <li> `accepted` </li> <li> `declined` </li> <li> `tentative` </li> <li> `needs-action` </li> |

## `recurrenceTemplate` {#recurrence}

`recurrenceTemplate` tillhandahålls som en array med objekt. Strukturen för varje objekt beskrivs nedan.

![Ett schemadiagram över objektstrukturen för upprepningsmallen.](../../../images/healthcare/field-groups/appointment/recurrence-template.png)

| Visningsnamn | Egenskap | Datatyp | Beskrivning |
| --- | --- | --- | --- |
| [!UICONTROL Monthly Template] | `monthlyTemplate` | Array med objekt | Information om återkommande avtalade tider varje månad. Mer information finns i avsnittet [nedan](#monthly-template). |
| [!UICONTROL Recurrence Type] | `recurrenceType` | [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md) | Hur ofta serien med avtalade tider ska upprepas, till exempel varje vecka, månad eller år. |
| [!UICONTROL Timezone] | `timezone` | [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md) | Tidszonen för den återkommande avtalade tiden. |
| [!UICONTROL Weekly Template] | `weeklyTemplate` | Array med objekt | Information om återkommande möten varje vecka. Mer information finns i avsnittet [nedan](#weekly-template). |
| [!UICONTROL Yearly Template] | `yearlyTemplate` | Objekt | Information om återkommande avtalade tider. Innehåller en egenskap, `yearInterval`, som innehåller ett heltalsvärde som anger varje månad som den avtalade tiden botas. |
| [!UICONTROL Excluding Date] | `excludingDate` | Datummatris | Eventuella datum, t.ex. helger, som ska uteslutas från upprepningen. |
| [!UICONTROL Excluding Recurrence Id] | `excludingRecurrenceId` | Array med heltal | Eventuella upprepnings-ID som ska uteslutas från upprepningen. Det här är ett alternativ till `excludingDate` där du anger `reccurenceID` för den avtalade tiden som ska uteslutas. |
| [!UICONTROL Last Occurence Date] | `lastOccurenceDate` | Datum | Det datum efter vilket inga ytterligare återkommande avtalade tider kommer att schemaläggas. |
| [!UICONTROL Occurence Count] | `occurenceCount` | Heltal | Hur många avtalade tider som planeras i återkommande aktiviteter. Det minsta värdet är `0`. |
| [!UICONTROL Occurence Date] | `occurenceDate` | Datummatris | En lista med specifika datum för schemalagda möten. |

## `weeklyTemplate` {#weekly-template}

`weeklyTemplate` tillhandahålls som en array med objekt. Strukturen för varje objekt beskrivs nedan.

![Ett schemadiagram över veckomallsobjektstrukturen.](../../../images/healthcare/field-groups/appointment/weekly-template.png)

| Visningsnamn | Egenskap | Datatyp | Beskrivning |
| --- | --- | --- | --- |
| [!UICONTROL Friday] | `friday` | Boolean | Anger att återkommande avtalade tider ska äga rum på fredag. |
| [!UICONTROL Monday] | `monday` | Boolean | Anger att återkommande avtalade tider ska inträffa på måndagar. |
| [!UICONTROL Saturday] | `saturday` | Boolean | Anger att återkommande avtalade tider ska inträffa på lördagar. |
| [!UICONTROL Sunday] | `sunday` | Boolean | Anger att återkommande avtalade tider ska äga rum på söndagar. |
| [!UICONTROL Thursday] | `thursday` | Boolean | Anger att återkommande avtalade tider ska äga rum på torsdagar. |
| [!UICONTROL Tuesday] | `tuesday` | Boolean | Anger att återkommande avtalade tider ska äga rum på tisdagar. |
| [!UICONTROL Wednesday] | `wednesday` | Boolean | Anger att återkommande avtalade tider ska äga rum på onsdagar. |
| [!UICONTROL Week Interval] | `weekInterval` | Heltal | Anger hur ofta avtalade tider återkommer, uttryckt i antal varje vecka. Standardvärdet är varje vecka, så det typiska värdet är 2 eller högre. |

## `monthlyTemplate` {#monthly-template}

`monthlyTemplate` tillhandahålls som en array med objekt. Strukturen för varje objekt beskrivs nedan.

![Ett schemadiagram över den månatliga mallobjektstrukturen.](../../../images/healthcare/field-groups/appointment/monthly-template.png)

| Visningsnamn | Egenskap | Datatyp | Beskrivning |
| --- | --- | --- | --- |
| [!UICONTROL Day Of Week] | `dayOfWeek` | [[!UICONTROL Coding]] | Anger att avtalade tider ska äga rum på den här specifika veckodagen. |
| [!UICONTROL nth Week Of Month] | `nthWeekOfMonth` | [[!UICONTROL Coding]](../data-types/coding.md) | Anger den n:e veckan i månaden som den avtalade tiden ska återkomma. |
| [!UICONTROL Day Of Month] | `dayOfMonth` | Heltal | Anger att avtalade tider ska äga rum den här specifika dagen i månaden. |
| [!UICONTROL Month Interval] | `monthInterval` | Heltal | Anger att återkommande avtalade tider ska inträffa varje månad. |
