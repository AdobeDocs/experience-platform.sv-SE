---
title: Sjukvårdsdatamodell V2
description: Läs mer om några vanliga användningsfall inom hälso- och sjukvården och de bästa klasserna, relaterade fältgrupper och datatyper som kan användas.
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: a796b58b-b36f-4277-870b-0d3939af8061
source-git-commit: 36f1a443eda47917d5b6bd84d4765ff044b5093a
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
      <td><a href="./field-groups/patient.md">Patient</a></td>
      <td>
        <li><a href="../../classes/individual-profile.md">Individuell XDM-profil</a></li>
      </td>
    </tr>
    <tr>
      <td rowspan="6"><strong>Vaccinering</strong>: Underlättar vaccinationsprocessen, hanterar patientimmuniseringsposter och integrerar EMR med Vaccinationshanteringssystem.</td>
      <td><a href="./field-groups/immunization.md">Immunisering</a></td>
      <td>
        <li><a href="../../classes/experienceevent.md">XDM Experience Event</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="./field-groups/patient.md">Patient</a></td>
      <td>
        <li><a href="../../classes/individual-profile.md">Individuell XDM-profil</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="./field-groups/location.md">Plats</a></td>
      <td>
        <li><a href="./classes/location.md">Plats</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="./field-groups/medication.md">Medicin</a></td>
      <td>
        <li><a href="../../classes/medication.md">Medicin</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="./field-groups/medication-dispense.md">Medicinsk befrielse</a></td>
      <td>
        <li><a href="../../classes/medication.md">Medicin</a></li>
        <li><a href="../../classes/individual-profile.md">Individuell XDM-profil</a></li>
        <li><a href="../../classes/provider.md">Provider</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="./field-groups/medication-request.md">Begäran om medicinering</a></td>
      <td>
        <li><a href="../../classes/medication.md">Medicin</a></li>
        <li><a href="../../classes/individual-profile.md">Individuell XDM-profil</a></li>
        <li><a href="../../classes/provider.md">Provider</a></li>
      </td>
    </tr>
    <tr>
      <td rowspan="4"><strong>Efterhandsföljsamhet</strong>: Motiverar patienter och vårdgivare till att slutföra sina behandlingsplaner och minska remitteringsgraden.</td>
      <td><a href="./field-groups/patient.md">Patient</a></td>
      <td>
        <li><a href="../../classes/individual-profile.md">Individuell XDM-profil</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="./field-groups/location.md">Plats</a></td>
      <td>
        <li><a href="./classes/location.md">Plats</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="./field-groups/care-plan.md">Vårdplan</a></td>
      <td>
        <li><a href="../../classes/individual-profile.md">Individuell XDM-profil</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="./field-groups/goal.md">Mål</a></td>
      <td>
        <li><a href="../../classes/individual-profile.md">Individuell XDM-profil</a></li>
        <li><a href="../../classes/provider.md">Provider</a></li>
      </td>
    </tr>
    <tr>
      <td rowspan="7"><strong>Konsumentupplevelse för försäkringar</strong>: Förbättra digitala förvärv och upplevelser bland konsumenter som handlar för försäkringar. Exempel: 
        <li> Förstå konsumenternas beteende när det gäller att skicka reklamannonser eller riktade tredjepartsannonser till personer som kommer åt sidor som innehåller allmän information (t.ex. planer, plannamn/nivåer, medicinskt stöd eller välhetsprogram)
        </li> 
        <li> Skicka vaccinrelaterad information om hjärtat för att skapa varumärkeskänslighet eller förfrågningar om att schemalägga vacciner till personer som söker efter information om hjärthälsa och vaccin.
        </li>
      </td>
      <td><a href="./field-groups/patient.md">Patient</a></td>
      <td>
        <li><a href="../../classes/individual-profile.md">Individuell XDM-profil</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="./field-groups/coverage.md">Täckning</a></td>
      <td>
        <li><a href="../../classes/plan.md">Plan</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="./field-groups/account.md">Konto</a></td>
      <td>
        <li><a href="../../classes/individual-profile.md">Individuell XDM-profil</a></li>
        <li><a href="../../classes/provider.md">Provider</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="./field-groups/location.md">Plats</a></td>
      <td>
        <li><a href="./classes/location.md">Plats</a></li>
      </td>
    </tr>
      <tr>
      <td><a href="./field-groups/medication.md">Medicin</a></td>
      <td>
        <li><a href="../../classes/medication.md">Medicin</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="./field-groups/medication-dispense.md">Medicinsk befrielse</a></td>
      <td>
        <li><a href="../../classes/medication.md">Medicin</a></li>
        <li><a href="../../classes/individual-profile.md">Individuell XDM-profil</a></li>
        <li><a href="../../classes/provider.md">Provider</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="./field-groups/medication-request.md">Begäran om medicinering</a></td>
      <td>
        <li><a href="../../classes/medication.md">Medicin</a></li>
        <li><a href="../../classes/individual-profile.md">Individuell XDM-profil</a></li>
        <li><a href="../../classes/provider.md">Provider</a></li>
      </td>
    </tr>
    <tr>
      <td rowspan="5"><strong>Förbättrad providerupplevelse</strong>: Använder providerdata från EMR-systemet för att föreslå alternativa providrar baserat på tillgänglighet, plats och specialitet för avtalade tider. <br> <br>Förbättrar providersökningar för att visa resultat med önskad tillgänglighet, verifiera att den valda providern är en del av betalarnätverket och tillhandahålla kostnadsberäkningar.
      </td>
      <td><a href="./field-groups/patient.md">Patient</a></td>
      <td>
        <li><a href="../../classes/individual-profile.md">Individuell XDM-profil</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="./field-groups/location.md">Plats</a></td>
      <td>
        <li><a href="./classes/location.md">Plats</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="./field-groups/organization.md">Organisation</a></td>
      <td>
        <li><a href="../../classes/individual-profile.md">Individuell XDM-profil</a></li>
        <li><a href="../../classes/provider.md">Provider</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="./field-groups/practioner.md">Yrkesverksamma</a></td>
      <td>
        <li><a href="../../classes/individual-profile.md">Individuell XDM-profil</a></li>
        <li><a href="../../classes/provider.md">Provider</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="./field-groups/schedule.md">Schema</a></td>
      <td>
        <li><a href="../../classes/individual-profile.md">Individuell XDM-profil</a></li>
        <li><a href="../../classes/provider.md">Provider</a></li>
      </td>
    </tr>
  </tbody>
</table>

## Datatyper {#data-types}

I följande tabell visas de datatyper som skapats enligt specifikationerna för [!DNL HL7 FHIR Release 5].

| Namn | Beskrivning |
| --- | --- |
| [[!UICONTROL Address]](./data-types/address.md) | Beskriver en adress som uttrycks enligt postkonventioner (till skillnad från GPS eller andra platsdefinitionsformat). |
| [[!UICONTROL Annotation]](./data-types/annotation.md) | En textnod med attribut till författaren. |
| [[!UICONTROL Availability]](./data-types/availability.md) | Tillgänglighetsdata för ett objekt. |
| [[!UICONTROL Codeable Concept]](./data-types/codeable-concept.md) | En referens från en resurs till en annan. |
| [[!UICONTROL Codeable Reference]](./data-types/codeable-reference.md) | En referens till en resurs eller ett koncept. |
| [[!UICONTROL Coding]](./data-types/coding.md) | En referens till en kod som definieras av ett terminologiskt system. |
| [[!UICONTROL Contact Point]](./data-types/contact-point.md) | Kontaktuppgifter för en person. |
| [[!UICONTROL Dosage]](./data-types/dosage.md) | Hur läkemedlet tas/ tas eller bör tas. |
| [[!UICONTROL Duration]](./data-types/duration.md) | En lång tid. |
| [[!UICONTROL Extended Contact Details]](./data-types/extended-contact-detail.md) | En utökad kontakts information. |
| [[!UICONTROL Human Name]](./data-types/human-name.md) | Information om namnet på en mänsklig eller annan levande enhet. |
| [[!UICONTROL Identifier]](./data-types/identifier.md) | En identifierare som är avsedd för beräkning. |
| [[!UICONTROL Money]](./data-types/money.md) | Ett ekonomiskt nyttobelopp i en viss erkänd valuta. |
| [[!UICONTROL Period]](./data-types/period.md) | En tidsperiod som definieras av ett start- och slutdatum/tid. |
| [[!UICONTROL Person]](./data-types/person.md) | Information om en allmän personpost. |
| [[!UICONTROL Quantity]](./data-types/quantity.md) | Ett uppmätt eller mätbart belopp. |
| [[!UICONTROL Range]](./data-types/range.md) | En uppsättning värden som är bundna av låga och höga värden. |
| [[!UICONTROL Ratio]](./data-types/ratio.md) | En kvot på två [[!UICONTROL Quantity]](./data-types/quantity.md)-värden genom en täljare och en nämnare. |
| [[!UICONTROL Reference]](./data-types/reference.md) | En referens från en resurs till en annan. |
| [[!UICONTROL Repeat]](./data-types/repeat.md) | En uppsättning regler som beskriver när en händelse schemaläggs. |
| [[!UICONTROL Simple Quantity]](./data-types/simple-quantity.md) | Ett uppmätt eller mätbart belopp. |
| [[!UICONTROL Timing]](./data-types/timing.md) | Information om en händelse som kan inträffa flera gånger. |
| [[!UICONTROL Virtual Service Detail]](./data-types/virtual-service-detail.md) | Kontaktinformation för virtuell tjänst. |
