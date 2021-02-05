---
keywords: Experience Platform;hem;populära ämnen;schema;schema;XDM;ExperienceEvent;fields;schemas;Schema design;mixin;mixin;enduserids;end user;ids;
solution: Experience Platform
title: Blandning av information om slutanvändar-ID
topic: overview
description: Det här dokumentet innehåller en översikt över den blandning av information om slutanvändar-ID som används.
translation-type: tm+mt
source-git-commit: f2238d35f3e2a279fbe8ef8b581282102039e932
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 0%

---


# [!UICONTROL End User ID Details] blanda

>[!NOTE]
>
>Namnen på flera blandningar har ändrats. Mer information finns i dokumentet om [uppdateringar av blandnamn](../name-updates.md).

[!UICONTROL End User ID Details] är en standardblandning för  [[!DNL XDM ExperienceEvent] klassen](../../classes/individual-profile.md) som används för att beskriva en individs identitetsinformation i flera Adobe-program. Mixin tillhandahåller ett `endUserIDs`-objekt på rotnivå, som i sin tur innehåller ett skrivskyddat `_experience`-fält vars värden uppdateras automatiskt när data importeras.

<img src="../../images/mixins/enduserids.png" width="700" /><br />

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `aacustomid` | [Identitet](../../data-types/identity.md) | Anpassade användar-ID för Adobe Analytics Cloud. |
| `aaid` | [Identitet](../../data-types/identity.md) | Slutanvändar-ID för Adobe Analytics Cloud. |
| `acid` | [Identitet](../../data-types/identity.md) | Slutanvändar-ID för Adobe Campaign. |
| `adcloud` | [Identitet](../../data-types/identity.md) | Slutanvändar-ID för Adobe Advertising Cloud. |
| `emailid` | [Identitet](../../data-types/identity.md) | E-postadress-ID:n. |
| `mcid` | [Identitet](../../data-types/identity.md) | Adobe Marketing Cloud ID. |
| `phonenumberid` | [Identitet](../../data-types/identity.md) | Telefonnummer-ID. |
| `tntid` | [Identitet](../../data-types/identity.md) | Slutanvändar-ID för Adobe Target. |

Mer information om blandningen finns i den offentliga XDM-databasen:

* [Populerat exempel](https://github.com/adobe/xdm/blob/master/components/mixins/experience-event/experienceevent-enduserids.example.1.json)
* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/components/mixins/experience-event/experienceevent-enduserids.schema.json)
