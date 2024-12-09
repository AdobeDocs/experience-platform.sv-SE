---
title: Sjukvårdsdatamodell V2
description: Läs mer om några vanliga användningsfall inom hälso- och sjukvården och de bästa klasserna, relaterade fältgrupper och datatyper som kan användas.
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: a796b58b-b36f-4277-870b-0d3939af8061
source-git-commit: 4d4e68376af914fbfcb005ad950e643f9407ad47
workflow-type: tm+mt
source-wordcount: '536'
ht-degree: 1%

---

# [!UICONTROL Healthcare] Datamodell V2

## Fältgrupper och klasser {#field-groups}

I följande tabell beskrivs de rekommenderade klasserna och schemafältgrupperna för flera vanliga hälsoanvändningsfall.

<table>
  <thead>
    <tr>
      <th>Användningsfall</th>
      <th>Fältgrupper</th>
      <th>Kompatibla klasser</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><strong>Skapa/uppdatera patient</strong>: När en patient anländer till sjukhusets skrivbord skapas en patientpost, med bland annat demografisk information som identifierare (valfritt), patientens namn, födelsedatum, kön och adress. Detta är en viktig del av IT inom hälso- och sjukvården.</td>
      <td><a href="../field-groups/profile/healthcare-patient.md">Patient</a></td>
      <td>
        <li><a href="../classes/individual-profile.md">Individuell XDM-profil</a></li>
      </td>
    </tr>
    <tr>
      <td rowspan="6"><strong>Vaccinering</strong>: Underlättar vaccinationsprocessen, hanterar patientimmuniseringsposter och integrerar EMR med Vaccinationshanteringssystem.</td>
      <td><a href="../field-groups/event/healthcare-immunization.md">Immunisering</a></td>
      <td>
        <li><a href="../classes/experienceevent.md">XDM Experience Event</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="../field-groups/profile/healthcare-patient.md">Patient</a></td>
      <td>
        <li><a href="../classes/individual-profile.md">Individuell XDM-profil</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="../field-groups/location/healthcare-location.md">Plats</a></td>
      <td>
        <li><a href="../classes/location.md">Plats</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="../field-groups/medication/healthcare-medication-v2.md">Medicin</a></td>
      <td>
        <li><a href="../classes/medication.md">Medicin</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="../field-groups/medication/healthcare-medication-dispense.md">Medicinsk befrielse</a></td>
      <td>
        <li><a href="../classes/medication.md">Medicin</a></li>
        <li><a href="../classes/individual-profile.md">Individuell XDM-profil</a></li>
        <li><a href="../classes/provider.md">Provider</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="../field-groups/medication/healthcare-medication-request.md">Begäran om medicinering</a></td>
      <td>
        <li><a href="../classes/medication.md">Medicin</a></li>
        <li><a href="../classes/individual-profile.md">Individuell XDM-profil</a></li>
        <li><a href="../classes/provider.md">Provider</a></li>
      </td>
    </tr>
    <tr>
      <td rowspan="4"><strong>Efterhandsföljsamhet</strong>: Motiverar patienter och vårdgivare till att slutföra sina behandlingsplaner och minska remitteringsgraden.</td>
      <td><a href="../field-groups/profile/healthcare-patient.md">Patient</a></td>
      <td>
        <li><a href="../classes/individual-profile.md">Individuell XDM-profil</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="../field-groups/location/healthcare-location.md">Plats</a></td>
      <td>
        <li><a href="../classes/location.md">Plats</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="../field-groups/profile/healthcare-care-plan.md">Vårdplan</a></td>
      <td>
        <li><a href="../classes/individual-profile.md">Individuell XDM-profil</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="../field-groups/profile/healthcare-goal.md">Mål</a></td>
      <td>
        <li><a href="../classes/individual-profile.md">Individuell XDM-profil</a></li>
        <li><a href="../classes/provider.md">Provider</a></li>
      </td>
    </tr>
    <tr>
      <td rowspan="7"><strong>Konsumentupplevelse för försäkringar</strong>: Förbättra digitala förvärv och upplevelser bland konsumenter som handlar för försäkringar. Exempel: 
        <li> Förstå konsumenternas beteende när det gäller att skicka reklamannonser eller riktade tredjepartsannonser till personer som kommer åt sidor som innehåller allmän information (t.ex. planer, plannamn/nivåer, medicinskt stöd eller välhetsprogram)
        </li> 
        <li> Skicka vaccinrelaterad information om hjärtat för att skapa varumärkeskänslighet eller förfrågningar om att schemalägga vacciner till personer som söker efter information om hjärthälsa och vaccin.
        </li>
      </td>
      <td><a href="../field-groups/profile/healthcare-patient.md">Patient</a></td>
      <td>
        <li><a href="../classes/individual-profile.md">Individuell XDM-profil</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="../field-groups/plan/healthcare-coverage.md">Täckning</a></td>
      <td>
        <li><a href="../classes/plan.md">Plan</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="../field-groups/profile/healthcare-account.md">Konto</a></td>
      <td>
        <li><a href="../classes/individual-profile.md">Individuell XDM-profil</a></li>
        <li><a href="../classes/provider.md">Provider</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="../field-groups/location/healthcare-location.md">Plats</a></td>
      <td>
        <li><a href="../classes/location.md">Plats</a></li>
      </td>
    </tr>
      <tr>
      <td><a href="../field-groups/medication/healthcare-medication-v2.md">Medicin</a></td>
      <td>
        <li><a href="../classes/medication.md">Medicin</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="../field-groups/medication/healthcare-medication-dispense.md">Medicinsk befrielse</a></td>
      <td>
        <li><a href="../classes/medication.md">Medicin</a></li>
        <li><a href="../classes/individual-profile.md">Individuell XDM-profil</a></li>
        <li><a href="../classes/provider.md">Provider</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="../field-groups/medication/healthcare-medication-request.md">Begäran om medicinering</a></td>
      <td>
        <li><a href="../classes/medication.md">Medicin</a></li>
        <li><a href="../classes/individual-profile.md">Individuell XDM-profil</a></li>
        <li><a href="../classes/provider.md">Provider</a></li>
      </td>
    </tr>
    <tr>
      <td rowspan="5"><strong>Förbättrad providerupplevelse</strong>: Använder providerdata från EMR-systemet för att föreslå alternativa providrar baserat på tillgänglighet, plats och specialitet för avtalade tider. <br> <br>Förbättrar providersökningar för att visa resultat med önskad tillgänglighet, verifiera att den valda providern är en del av betalarnätverket och tillhandahålla kostnadsberäkningar.
      </td>
      <td><a href="../field-groups/profile/healthcare-patient.md">Patient</a></td>
      <td>
        <li><a href="../classes/individual-profile.md">Individuell XDM-profil</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="../field-groups/location/healthcare-location.md">Plats</a></td>
      <td>
        <li><a href="../classes/location.md">Plats</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="../field-groups/profile/healthcare-organization.md">Organisation</a></td>
      <td>
        <li><a href="../classes/individual-profile.md">Individuell XDM-profil</a></li>
        <li><a href="../classes/provider.md">Provider</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="../field-groups/profile/healthcare-practioner.md">Yrkesverksamma</a></td>
      <td>
        <li><a href="../classes/individual-profile.md">Individuell XDM-profil</a></li>
        <li><a href="../classes/provider.md">Provider</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="../field-groups/profile/healthcare-schedule.md">Schema</a></td>
      <td>
        <li><a href="../classes/individual-profile.md">Individuell XDM-profil</a></li>
        <li><a href="../classes/provider.md">Provider</a></li>
      </td>
    </tr>
  </tbody>
</table>

## Datatyper {#data-types}

I följande tabell visas de datatyper som skapats enligt specifikationerna för [!DNL HL7 FHIR Release 5].

| Namn | Beskrivning |
| --- | --- |
| [[!UICONTROL Address]](../data-types/healthcare/address.md) | Beskriver en adress som uttrycks enligt postkonventioner (till skillnad från GPS eller andra platsdefinitionsformat). |
| [[!UICONTROL Annotation]](../data-types/healthcare/annotation.md) | En textnod med attribut till författaren. |
| [[!UICONTROL Availability]](../data-types/healthcare/availability.md) | Tillgänglighetsdata för ett objekt. |
| [[!UICONTROL Codeable Concept]](../data-types/healthcare/codeable-concept.md) | En referens från en resurs till en annan. |
| [[!UICONTROL Codeable Reference]](../data-types/healthcare/codeable-reference.md) | En referens till en resurs eller ett koncept. |
| [[!UICONTROL Coding]](../data-types/healthcare/coding.md) | En referens till en kod som definieras av ett terminologiskt system. |
| [[!UICONTROL Contact Point]](../data-types/healthcare/contact-point.md) | Kontaktuppgifter för en person. |
| [[!UICONTROL Dosage]](../data-types/healthcare/dosage.md) | Hur läkemedlet tas/ tas eller bör tas. |
| [[!UICONTROL Duration]](../data-types/healthcare/duration.md) | En lång tid. |
| [[!UICONTROL Extended Contact Details]](../data-types/healthcare/extended-contact-detail.md) | En utökad kontakts information. |
| [[!UICONTROL Human Name]](../data-types/healthcare/human-name.md) | Information om namnet på en mänsklig eller annan levande enhet. |
| [[!UICONTROL Identifier]](../data-types/healthcare/identifier.md) | En identifierare som är avsedd för beräkning. |
| [[!UICONTROL Money]](../data-types/healthcare/money.md) | Ett ekonomiskt nyttobelopp i en viss erkänd valuta. |
| [[!UICONTROL Period]](../data-types/healthcare/period.md) | En tidsperiod som definieras av ett start- och slutdatum/tid. |
| [[!UICONTROL Person]](../data-types/healthcare/person.md) | Information om en allmän personpost. |
| [[!UICONTROL Quantity]](../data-types/healthcare/quantity.md) | Ett uppmätt eller mätbart belopp. |
| [[!UICONTROL Range]](../data-types/healthcare/range.md) | En uppsättning värden som är bundna av låga och höga värden. |
| [[!UICONTROL Ratio]](../data-types/healthcare/ratio.md) | En kvot på två [[!UICONTROL Quantity]](../data-types/healthcare/quantity.md)-värden genom en täljare och en nämnare. |
| [[!UICONTROL Reference]](../data-types/healthcare/reference.md) | En referens från en resurs till en annan. |
| [[!UICONTROL Repeat]](../data-types/healthcare/repeat.md) | En uppsättning regler som beskriver när en händelse schemaläggs. |
| [[!UICONTROL Simple Quantity]](../data-types/healthcare/simple-quantity.md) | Ett uppmätt eller mätbart belopp. |
| [[!UICONTROL Timing]](../data-types/healthcare/timing.md) | Information om en händelse som kan inträffa flera gånger. |
| [[!UICONTROL Virtual Service Detail]](../data-types/healthcare/virtual-service-detail.md) | Kontaktinformation för virtuell tjänst. |
