---
keywords: Experience Platform;hem;populära ämnen;schema;schema;XDM;Individuell profil;fält;scheman;scheman;schemadesign;fältgrupp;iab;tcf;medgivande;
solution: Experience Platform
title: IAB TCF 2.0-godkännandefältgrupp för profilscheman
description: Lär dig mer om schemafältgruppen IAB TCF 2.0 Consent för klassen XDM Individual Profile.
exl-id: 52a4fee8-d7f4-4f27-8e26-0c132985eb84
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '307'
ht-degree: 0%

---

# Fältgrupp [!UICONTROL IAB TCF 2.0 Consent] för profilscheman

>[!NOTE]
>
>Det här dokumentet innehåller schemafältgruppen [!UICONTROL IAB TCF 2.0 Consent] för klassen XDM Individual Profile. För fältgruppen som är avsedd för klassen XDM ExperienceEvent, se följande [dokument](../event/iab.md) i stället.

[!UICONTROL IAB TCF 2.0 Consent] är en standardschemafältgrupp för den [[!DNL XDM Individual Profile] klass](../../classes/individual-profile.md) som används för att hämta en tidsstämplad serie IAB-medgivandesträngar, för att kunna spåra mönster för medgivandeändring över tid.

![](../../images/field-groups/iab-profile.png)

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `identityPrivacyInfo` | Karta | Ett mappningsobjekt som associerar en kunds individuella identitetsvärden med olika TCF-medgivandesträngar. Ett exempel på objektets struktur ges nedan. |

{style="table-layout:auto"}

I följande JSON visas strukturen för kartan `identityPrivacyInfo`.

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

Som exemplet visar motsvarar varje rotnivånyckel på `xdm:identityPrivacyInfo` ett identitetsnamnområde som identifieras av identitetstjänsten. Varje namespace-egenskap måste i sin tur ha minst en underegenskap vars nyckel matchar kundens motsvarande identitetsvärde för namnutrymmet. I det här exemplet identifieras kunden med ett Experience Cloud-ID (`ECID`) på `13782522493631189`.

>[!NOTE]
>
>I exemplet ovan används ett namnutrymmes-/värdepar för att representera kundens identitet, men du kan lägga till ytterligare nycklar för andra namnutrymmen, och varje namnområde kan ha flera identitetsvärden, var och en med sin egen uppsättning inställningar för TCF-medgivande.

För varje identitetsvärde måste en `identityIABConsent`-egenskap anges, som tillhandahåller TCF-medgivandevärdet för identiteten. Värdet för den här egenskapen måste överensstämma med datatypen [[!UICONTROL Consent String] ](../../data-types/consent-string.md).

Mer information om hur den här fältgruppen används finns i guiden [IAB TCF 2.0-stöd i Platform](../../../landing/governance-privacy-security/consent/iab/overview.md) . Mer information om själva fältgruppen finns i den offentliga XDM-databasen:

* [Populerat exempel](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-privacy.example.1.json)
* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-privacy.schema.json)
