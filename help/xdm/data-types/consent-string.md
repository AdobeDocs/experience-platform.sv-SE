---
solution: Experience Platform
title: Samtyckessträngens datatyp
topic-legacy: overview
description: Det här dokumentet innehåller en översikt över datatypen Consent String XDM.
source-git-commit: 7a0ac3970713e95438c6f0fdbd6175545ea7fdd0
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 2%

---

# [!UICONTROL Consent String] datatyp

[!UICONTROL Consent String] är en standard-XDM-datatyp som beskriver ett strängvärde som representerar kundens samtycke. Den innehåller sammanhangsberoende information som standarden för medgivandesträngen (t.ex. [IAB Transparency och Consent Framework (TCF) 2.0](../field-groups/profile/iab.md)).

![](../images/data-types/consent-string.png)

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `consentStandard` | Sträng | Standardvärdet för medgivandesträngen. Detta hjälper till att fastställa formatet för medgivandesträngen enligt de olika tjänsterna för hantering av samtycke. |
| `consentStandardVersion` | Sträng | Den version av medgivandestandarden som används för att korrekt definiera formatet för medgivandesträngen enligt de tjänster som tillhandahålls av samtyckeshantering. |
| `consentStringValue` | Sträng | Den fullständiga medgivandesträngen som tillhandahålls av tjänsten för hantering av samtycke. `consentStandard` och  `consentStandardVersion` hjälp för att definiera hur strängen ska tolkas. |
| `containsPersonalData` | Boolean | När det här fältet är sant betyder det att den här medgivandesträngen måste bearbetas för att medgivandet ska kunna verkställas. |
| `gdprApplies` | Boolean | När det här fältet är sant innebär det att samtycke kommer med personuppgifter. |

{style=&quot;table-layout:auto&quot;}

Mer information om datatypen finns i den offentliga XDM-databasen:

* [Populerat exempel](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/consentstring.example.1.json)
* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/consentstring.schema.json)
