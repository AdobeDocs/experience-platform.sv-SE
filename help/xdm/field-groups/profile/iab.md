---
keywords: Experience Platform;hem;populära ämnen;schema;schema;XDM;Individuell profil;fält;scheman;scheman;schemadesign;fältgrupp;iab;tcf;medgivande;
solution: Experience Platform
title: Fältgrupp för IAB TCF 2.0-samtycke
topic-legacy: overview
description: Det här dokumentet innehåller en översikt över schemafältgruppen IAB TCF 2.0 Consent för klassen XDM Individual Profile.
source-git-commit: 9b75a69cc6e31ea0ad77048a6ec1541df2026f27
workflow-type: tm+mt
source-wordcount: '326'
ht-degree: 0%

---


# [!UICONTROL IAB TCF 2.0 Consent] schemafältgrupp

>[!NOTE]
>
>Det här dokumentet innehåller schemafältgruppen [!UICONTROL IAB TCF 2.0 Consent] för klassen XDM Individual Profile. För fältgruppen som är avsedd för klassen XDM ExperienceEvent, se följande [dokument](../event/iab.md) i stället.

[!UICONTROL IAB TCF 2.0 Consent] är en standardgrupp för schemafält för den  [[!DNL XDM Individual Profile] ](../../classes/individual-profile.md) klass som används för att fånga in en tidsstämplad serie IAB-medgivandesträngar, för att spåra mönster för samtyckesändringar över tid.

![](../../images/field-groups/iab-profile.png)

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `identityPrivacyInfo` | Mappa | Ett mappningsobjekt som associerar en kunds individuella identitetsvärden med olika TCF-medgivandesträngar. Ett exempel på objektets struktur ges nedan. |

{style=&quot;table-layout:auto&quot;}

I följande JSON visas strukturen för `identityPrivacyInfo`-kartan.

```json
{
  "identityPrivacyInfo": {
    "ECID": {
      "13782522493631189": {
        "identityIABConsent": {
          "consentTimestamp": "2020-04-11T05:05:05Z",
          "consentString": {
            "consentStandard": "IAB TCF",
            "consentStandardVersion": "2.0",
            "consentStringValue": "BObdrPUOevsguAfDqFENCNAAAAAmeAAA.PVAfDObdrA.DqFENCAmeAENCDA",
            "gdprApplies": true,
            "containsPersonalData": false
          }
        }
      }
    }
  }
}
```

Som exemplet visar motsvarar varje rotnivånyckel på `xdm:identityPrivacyInfo` ett identitetsnamnutrymme som identifieras av identitetstjänsten. Varje namespace-egenskap måste i sin tur ha minst en underegenskap vars nyckel matchar kundens motsvarande identitetsvärde för namnutrymmet. I det här exemplet identifieras kunden med ett Experience Cloud-ID (`ECID`)-värde på `13782522493631189`.

>[!NOTE]
>
>I exemplet ovan används ett namnutrymmes-/värdepar för att representera kundens identitet, men du kan lägga till ytterligare nycklar för andra namnutrymmen, och varje namnområde kan ha flera identitetsvärden, var och en med sin egen uppsättning inställningar för TCF-medgivande.

För varje identitetsvärde måste en `identityIABConsent`-egenskap anges, som anger TCF-medgivandevärdet för identiteten. Värdet för den här egenskapen måste överensstämma med datatypen [[!UICONTROL Consent String]](../../data-types/consent-string.md).

Mer information om hur den här fältgruppen används finns i guiden [IAB TCF 2.0-stöd i Platform](../../../landing/governance-privacy-security/consent/iab/overview.md). Mer information om själva fältgruppen finns i den offentliga XDM-databasen:

* [Populerat exempel](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-privacy.example.1.json)
* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-privacy.schema.json)
