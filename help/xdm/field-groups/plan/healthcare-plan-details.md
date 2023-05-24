---
title: Schemafältgrupp för information om vårdplan
description: Det här dokumentet innehåller en översikt över schemafältgruppen för information om vårdplan.
exl-id: 5a480c5b-74f8-48dd-858a-5cf2628dc7f0
source-git-commit: 2fd35c4ac29f43391f9dc03c636d20558b701be7
workflow-type: tm+mt
source-wordcount: '209'
ht-degree: 2%

---

# [!UICONTROL Healthcare Plan Details] schemafältgrupp

[!UICONTROL Healthcare Plan Details] är en standardgrupp för schemafält för [[!UICONTROL Plan] class](../../classes/plan.md). Det innehåller ett enda objekttypsfält `healthcarePlanDetails` som hämtar egenskaper som hör till en medicinsk plan.

![](../../images/field-groups/plan/healthcare-plan-details.png)

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `networkDetails` | Array med objekt | Visar detaljerad information om det eller de försäkringsdefinierade nätverk av leverantörer som stödmottagaren kan vända sig till för att få behandling och som kommer att täckas med nätverkstaxan. Varje objekt innehåller följande egenskaper: <ul><li>`networkID`: (String) Nätverkets försäkringsspecifika ID.</li><li>`networkName`: (String) Nätverkets försäkringsspecifika namn.</li></ul> |
| `affiliations` | Array med strängar | En lista över affärsenheter som är kopplade till planen. |
| `coverageType` | Sträng | Planens disponeringstyp. Godkända värden är:<ul><li>`medical`</li><li>`dental`</li><li>`vision`</li><li>`accident`</li></ul> |
| `isActive` | Boolean | Anger om planen är aktiv. |
| `lastVerificationDate` | DateTime | Det datum då planen senast verifierades. |
| `payerID` | Sträng | Den unika identifieraren för betalaren (med andra ord försäkringsgivaren för planen). |
| `planLevel` | Sträng | Anger plannivån. Godkända värden är:<ul><li>`primary`</li><li>`secondary`</li><li>`tertiary`</li><li>`quaternary`</li></ul> |
| `planType` | Sträng | Anger plantypen. Godkända värden är:<ul><li>`hmo`</li><li>`epo`</li><li>`pos`</li><li>`hdhp`</li></ul> |
| `targetOwnerType` | Sträng | Den typ av ägare som en plan är avsedd för. Exemplen omfattar individ, grupp, organisation och så vidare. |

{style="table-layout:auto"}

Mer information om fältgruppen finns i [publik XDM-databas](https://github.com/adobe/xdm/blob/master/docs/reference/fieldgroups/plan/healthcare-plan-details.schema.json).
