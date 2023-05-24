---
keywords: Experience Platform;hem;populära ämnen;schema;schema;XDM;individuell profil;fält;scheman;scheman;telecom;prenumeration;telekom;telekom;schemadesign;fältgrupp;fältgrupp;
solution: Experience Platform
title: Fältgrupp för telekom-prenumerationsschema
description: Det här dokumentet innehåller en översikt över schemafältgruppen Telecom Subscription.
exl-id: 00c20081-09d0-425c-9894-0f957558bd43
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '698'
ht-degree: 1%

---

# [!UICONTROL Telecom Subscription] schemafältgrupp

>[!NOTE]
>
>Namnen på flera schemafältgrupper har ändrats. Visa dokumentet på [uppdaterar fältgruppnamn](../name-updates.md) för mer information.

[!UICONTROL Telecom Subscription] är en standardgrupp för schemafält för [[!DNL XDM Individual Profile] class](../../classes/individual-profile.md) som beskriver en kunds prenumerationsplan för telekom, inklusive priser, paket och enskilda produktprenumerationer.

Fältgruppen innehåller ett enda fält av objekttyp, `telecomSubscription`, vars egenskaper beskrivs nedan.

![Telecom Subscription structure](../../images/field-groups/telecom-subscription/structure.png)

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `internetSubscription` | Array med objekt | Beskriver information om prenumerationsplaner för Internet, t.ex. databegränsning, anslutningstyp och hastighetsinformation. Se [avsnitt nedan](#internetSubscription) för mer information. |
| `landlineSubscription` | Array med objekt | Beskriver information om prenumeration på fast linje, inklusive valda funktioner, minuter och uppringningsplaner. Se [avsnitt nedan](#landlineSubscription) för mer information. |
| `mediaSubscription` | Array med objekt | Beskriver information om prenumerationsplaner för media, inklusive antalet kanaler och inkluderade direktuppspelningstjänster. Se [avsnitt nedan](#mediaSubscription) för mer information. |
| `mobileSubscription` | Array med objekt | Beskriver information om prenumerationsplaner för mobila enheter, inklusive antal rader, datahastigheter, kostnad och mycket mer. Se [avsnitt nedan](#mobileSubscription) för mer information. |
| `primarySubscriber` | [[!UICONTROL Person]](../../data-types/person.md) | Beskriver prenumerationens ägare. |
| `bundleName` | Sträng | Hämtar namnet på alla typer av prenumerationspaket där kunden är registrerad, till exempel `Internet + Media`. |
| `primaryPartyID` | Sträng | En identifierare för den primära person som ansvarar för prenumerationen, som vanligtvis kan vara enhetens telefonnummer. |

{style="table-layout:auto"}

Mer information om fältgruppen finns i den offentliga XDM-databasen:

* [Populerat exempel](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-personal-details.example.1.json)
* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-personal-details.schema.json)

## `internetSubscription` {#internetSubscription}

`internetSubscription` anges som en array med objekt. Strukturen för varje objekt beskrivs nedan.

![internetSubscription](../../images/field-groups/telecom-subscription/internetSubscription.png)

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `subscriptionDetails` | [[!UICONTROL Telecom Subscription]](../../data-types/telecom-subscription.md) | Beskriver allmän information om prenumerationen, inklusive prenumerationslängd, avgifter, status med mera. Beskriver allmän information om prenumerationen, inklusive prenumerationslängd, avgifter, status med mera. |
| `connectionType` | Sträng | Prenumerationens anslutningstyp. |
| `dataCap` | Heltal | Kontots gräns för datahastighet i MB. |
| `downloadSpeed` | Heltal | Den maximala hämtningshastigheten för prenumerationen, i MB. |
| `selfSetup` | Boolean | Anger om en kund är berättigad till internetinstallation utan att ha besökt en tekniker. |
| `uploadSpeed` | Heltal | Den maximala överföringshastigheten för prenumerationen, i MB. |

{style="table-layout:auto"}

## `landlineSubscription` {#landlineSubscription}

`landlineSubscription` anges som en array med objekt. Strukturen för varje objekt beskrivs nedan.

![landlineSubscription](../../images/field-groups/telecom-subscription/landlineSubscription.png)

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `phoneNumber` | [[!UICONTROL Phone Number]](../../data-types/telecom-subscription.md) | Det telefonnummer som är tilldelat den här prenumerationen. |
| `subscriptionDetails` | [[!UICONTROL Telecom Subscription]](../../data-types/telecom-subscription.md) | Beskriver allmän information om prenumerationen, inklusive prenumerationslängd, avgifter, status med mera. |
| `callBlocking` | Boolean | Anger om det finns samtalsblockering i fasta prenumerationer. |
| `callForwarding` | Boolean | Anger om onlineprenumerationen innehåller vidarekoppling av samtal. |
| `callWaiting` | Boolean | Anger om telefonabonnemangsfunktionerna inkluderar telefonsamtal som väntar. |
| `callerID` | Boolean | Anger om prenumerationsfunktionerna för fasta nätverk innehåller anroparens ID. |
| `internationalCalling` | Boolean | Anger om landnätsprenumerationen innehåller internationella telefonsamtal. |
| `minutes` | Heltal | Antalet månatliga minuter som är tillgängliga i prenumerationen. |
| `threeWayCalling` | Boolean | Anger om landnätsprenumerationen innehåller trevägssamtal. |
| `unlimitedDomesticLongDistance` | Boolean | Anger om landnätsprenumerationen innehåller ett obegränsat antal samtal på lång distans inom landet. |
| `unlimitedLocalCalling` | Boolean | Anger om landnätsprenumerationen har ett obegränsat antal lokala telefonsamtal. |
| `voicemail` | Boolean | Anger om funktionen för fasta prenumerationer innehåller röstmeddelanden. |

{style="table-layout:auto"}

## `mediaSubscription` {#mediaSubscription}

`mediaSubscription` anges som en array med objekt. Strukturen för varje objekt beskrivs nedan.

![mediaSubscription](../../images/field-groups/telecom-subscription/mediaSubscription.png)

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `streamingServices` | Array med objekt | En lista över alla direktuppspelningstjänster som ingår i prenumerationen. Varje arrayobjekt innehåller följande egenskaper: <ul><li>`promotionLength`: Kampanjens längd, i månader, om direktuppspelningstjänsten lades till som en del av en kampanj.</li><li>`promotionalAddition`: Anger om direktuppspelningstjänsten lades till som en del av en befordran.</li><li>`serviceName`: Namnet på direktuppspelningstjänsten.</li></ul> |
| `subscriptionDetails` | [[!UICONTROL Telecom Subscription]](../../data-types/telecom-subscription.md) | Beskriver allmän information om prenumerationen, inklusive prenumerationslängd, avgifter, status med mera. |
| `channels` | Heltal | Antalet kanaler som ingår i medieprenumerationen. |

{style="table-layout:auto"}

## `mobileSubscription` {#mobileSubscription}

`mobileSubscription` anges som en array med objekt. Strukturen för varje objekt beskrivs nedan.

![mobileSubscription](../../images/field-groups/telecom-subscription/mobileSubscription.png)

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `phoneNumber` | [[!UICONTROL Phone Number]](../../data-types/telecom-subscription.md) | Det telefonnummer som är tilldelat den här prenumerationen. |
| `subscriptionDetails` | [[!UICONTROL Telecom Subscription]](../../data-types/telecom-subscription.md) | Beskriver allmän information om prenumerationen, inklusive prenumerationslängd, avgifter, status med mera. |
| `earlyUpgradeEnrollment` | Boolean | Anger om kunden väljer att uppgradera tidigt. |
| `planLevel` | Sträng | Namnet på den mobilplan som har tilldelats den här prenumerationen. |
| `portedNumber` | Boolean | Anger om kunden portar sitt nummer från en annan leverantör. |

{style="table-layout:auto"}
