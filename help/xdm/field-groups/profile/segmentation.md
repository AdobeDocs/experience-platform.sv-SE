---
solution: Experience Platform
title: Schemafältgrupp för information om segmentmedlemskap
description: Lär dig mer om schemafältgruppen Segmentmedlemsdetaljer.
exl-id: 4d463f3a-2247-4307-8afe-9527e7fd72a7
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '392'
ht-degree: 0%

---


# Schemafältgruppen [!UICONTROL Segment Membership Details]

>[!NOTE]
>
>Namnen på flera schemafältgrupper har ändrats. Mer information finns i dokumentet om [uppdatering av fältgruppnamn](../name-updates.md).

[!UICONTROL Segment Membership Details] är en standardschemafältgrupp för [[!DNL XDM Individual Profile] klassen](../../classes/individual-profile.md). Fältgruppen innehåller ett enda kartfält som samlar in information om segmentmedlemskap, inklusive vilka segment den enskilda personen tillhör, senaste kvalificeringstid och när medlemskapet är giltigt till.

>[!WARNING]
>
>Fältet `segmentMembership` måste läggas till manuellt i ditt profilschema med den här fältgruppen, men du bör inte försöka fylla i eller uppdatera det här fältet manuellt. Systemet uppdaterar automatiskt kartan `segmentMembership` för varje profil när segmenteringsjobb utförs.

<img src="../../images/data-types/profile-segmentation.png" width="400" /><br />

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `segmentMembership` | Karta | Ett kartobjekt som beskriver personens segmentmedlemskap. Objektets struktur beskrivs i detalj nedan. |

{style="table-layout:auto"}

Följande är ett exempel på `segmentMembership`-mappning som systemet har fyllt i för en viss profil. Segmentmedlemskap sorteras efter namnutrymme, vilket anges av objektets rotnivånycklar. De enskilda nycklarna under varje namnutrymme representerar i sin tur ID:n för de segment som profilen är medlem i. Varje segmentobjekt innehåller flera underfält med mer information om medlemskapet:

```json
{
  "xdm:segmentMembership": {
    "AAM": {
      "04a81716-43d6-4e7a-a49c-f1d8b3129ba9": {
        "xdm:version": "15",
        "xdm:lastQualificationTime": "2018-04-26T15:52:25+00:00",
        "xdm:validUntil": "2019-04-26T15:52:25+00:00",
        "xdm:status": "realized",
        "xdm:payload": {
          "xdm:payloadBooleanValue": true,
          "xdm:payloadType": "boolean"
        }
      },
      "53cba6b2-a23b-454a-8069-fc41308f1c0f": {
        "xdm:version": "3",
        "xdm:lastQualificationTime": "2018-04-26T15:52:25+00:00",
        "xdm:validUntil": "2018-04-27T15:52:25+00:00",
        "xdm:status": "realized",
        "xdm:payload": {
          "xdm:payloadPropensityValue": 0.5,
          "xdm:payloadType": "propensity"
        }
      }
    },
    "Email": {
      "abcd@adobe.com": {
        "xdm:version": "1",
        "xdm:lastQualificationTime": "2017-09-26T15:52:25+00:00",
        "xdm:validUntil": "2017-12-26T15:52:25+00:00",
        "xdm:status": "exited"
      }
    }
  }
}
```

| Egenskap | Beskrivning |
| --- | --- |
| `xdm:version` | Den version av segmentet som den här profilen är kvalificerad för. |
| `xdm:lastQualificationTime` | En tidsstämpel från den senaste gången profilen kvalificerades för segmentet. |
| `xdm:validUntil` | En tidsstämpel som anger när segmentmedlemskapet inte längre ska antas vara giltigt. Om det här fältet inte har angetts för externa målgrupper behålls segmentmedlemskapet endast i 30 dagar från `lastQualificationTime`. |
| `xdm:status` | Ett strängfält som anger om segmentmedlemskapet har realiserats som en del av den aktuella begäran. Följande värden accepteras: <ul><li>`realized`: Profilen kvalificerar för segmentet.</li><li>`exited`: Profilen avslutar segmentet som en del av den aktuella begäran.</li></ul> |
| `xdm:payload` | Vissa segmentmedlemskap innehåller en nyttolast som beskriver ytterligare värden som är direkt relaterade till medlemskapet. Endast en nyttolast av en viss typ kan anges för varje medlemskap. `xdm:payloadType` anger typen av nyttolast (`boolean`, `number`, `propensity` eller `string`), medan dess jämställda egenskap anger värdet för nyttolasttypen. |

{style="table-layout:auto"}

>[!NOTE]
>
>Alla segmentmedlemskap som har statusen `exited` i mer än 30 dagar, baserat på `lastQualificationTime`, kan tas bort.

Mer information om fältgruppen finns i den offentliga XDM-databasen:

* [Populerat exempel](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-personal-details.example.1.json)
* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-personal-details.schema.json)
