---
keywords: Experience Platform;hem;populära ämnen;schema;schema;XDM;Individuell profil;fält;scheman;scheman;schemadesign;fältgrupp;iab;tcf;medgivande;
solution: Experience Platform
title: IAB TCF 2.0-godkännandefältgrupp för profilscheman
description: Det här dokumentet innehåller en översikt över schemafältgruppen IAB TCF 2.0 Consent för klassen XDM Individual Profile.
exl-id: 52a4fee8-d7f4-4f27-8e26-0c132985eb84
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '327'
ht-degree: 0%

---

# [!UICONTROL IAB TCF 2.0 Consent] fältgrupp för profilscheman

>[!NOTE]
>
>Det här dokumentet innehåller [!UICONTROL IAB TCF 2.0 Consent] schemafältgrupp för klassen XDM Individual Profile. För fältgruppen som är avsedd för klassen XDM ExperienceEvent, se följande [dokument](../event/iab.md) i stället.

[!UICONTROL IAB TCF 2.0 Consent] är en standardgrupp för schemafält för [[!DNL XDM Individual Profile] class](../../classes/individual-profile.md) används för att fånga in tidsstämplade IAB-strängar för medgivande för att spåra mönster för samtyckesändringar över tid.

![](../../images/field-groups/iab-profile.png)

| Egenskap | Datatyp | Beskrivning |
| --- | --- | --- |
| `identityPrivacyInfo` | Mappa | Ett mappningsobjekt som associerar en kunds individuella identitetsvärden med olika TCF-medgivandesträngar. Ett exempel på objektets struktur ges nedan. |

{style="table-layout:auto"}

I följande JSON visas strukturen för `identityPrivacyInfo` karta.

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

Som exemplet visar är varje rotnivånyckel för `xdm:identityPrivacyInfo` motsvarar ett identitetsnamnutrymme som känns igen av identitetstjänsten. Varje namespace-egenskap måste i sin tur ha minst en underegenskap vars nyckel matchar kundens motsvarande identitetsvärde för namnutrymmet. I det här exemplet identifieras kunden med ett Experience Cloud-ID (`ECID`) värde för `13782522493631189`.

>[!NOTE]
>
>I exemplet ovan används ett namnutrymmes-/värdepar för att representera kundens identitet, men du kan lägga till ytterligare nycklar för andra namnutrymmen, och varje namnområde kan ha flera identitetsvärden, var och en med sin egen uppsättning inställningar för TCF-medgivande.

För varje identitetsvärde `identityIABConsent` egenskapen måste anges, vilket anger TCF-medgivandevärdet för identiteten. Värdet för den här egenskapen måste överensstämma med [[!UICONTROL Consent String] datatyp](../../data-types/consent-string.md).

Se guiden [Stöd för IAB TCF 2.0 i Platform](../../../landing/governance-privacy-security/consent/iab/overview.md) om du vill ha mer information om hur den här fältgruppen används. Mer information om själva fältgruppen finns i den offentliga XDM-databasen:

* [Populerat exempel](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-privacy.example.1.json)
* [Fullständigt schema](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-privacy.schema.json)
