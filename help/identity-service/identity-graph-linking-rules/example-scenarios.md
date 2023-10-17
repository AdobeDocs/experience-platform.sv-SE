---
title: Exempelscenarier för konfiguration av identitetsinställningar
description: Lär dig mer om exempelscenarier för konfigurering av identitetsinställningar.
hide: true
hidefromtoc: true
source-git-commit: bde6c96bf72bb948c149bf5dc8d35591f2586887
workflow-type: tm+mt
source-wordcount: '416'
ht-degree: 0%

---

# Exempelscenarier för konfiguration av länkningsregler för identitetsdiagram

Det här dokumentet innehåller exempel på scenarier som du kan överväga när du konfigurerar länkningsregler för identitetsdiagram.


## Delad enhet

Det finns instanser där flera inloggningar kan förekomma på en enda enhet:

| Delad enhet | Beskrivning |
| --- | --- |
| Familjedatorer och surfplattor | Man och hustru loggar båda in på sina respektive bankkonton. |
| Publik kiosk | Resenärer på en flygplats som loggar in med sitt lojalitets-ID för att checka in väskor och skriva ut boardingkort. |
| Callcenter | Anställda på kundtjänst loggar in på en enda enhet för kunder som ringer kundsupport för att lösa problem. |

![shared-devices](../images/identity-settings/shared-devices.png)

I dessa fall kommer ett enda ECID att länkas till flera CRM-ID:n från en diagramsynvinkel utan att några begränsningar är aktiverade.

Med länkningsregler för identitetsdiagram kan du:

* Konfigurera det ID som används för inloggning som unik identifierare. Du kan t.ex. begränsa ett diagram så att endast en identitet lagras med ett CRM ID-namnutrymme och därmed definiera CRM-ID:t som den unika identifieraren för en delad enhet.
   * På så sätt kan du se till att CRM-ID:n inte sammanfogas med ECID:t.

## Ogiltiga e-post-/telefonscenarier

Det finns även instanser av användare som anger falska värden som telefonnummer och/eller e-postadresser när de registrerar sig. I dessa fall, om begränsningar inte är aktiverade, kommer telefon-/e-postrelaterade identiteter att länkas till flera olika CRM-ID:n.

![invalid-email-phone](../images/identity-settings/invalid-email-phone.png)

Med länkningsregler för identitetsdiagram kan du:

* Konfigurera antingen CRM-ID, telefonnummer eller e-postadress som den unika identifieraren och begränsa därmed en person till endast ett CRM-ID, telefonnummer och/eller e-postadress som är kopplad till deras konto.

## Felaktiga eller felaktiga identitetsvärden

Det finns fall där icke-unika, felaktiga identitetsvärden är inkapslade i systemet, oavsett namnutrymme. Exempel:

* IDFA-namnutrymme med identitetsvärdet &quot;user_null&quot;.
   * IDFA-identitetsvärden ska innehålla 36 tecken: 32 alfanumeriska tecken och fyra bindestreck.
* Namnområde för telefonnummer med identitetsvärdet &quot;ej angivet&quot;.
   * Telefonnummer får inte innehålla några alfabet.

Dessa identiteter kan resultera i följande diagram, där flera CRM-ID:n sammanfogas med den felaktiga identiteten:

![felaktiga data](../images/identity-settings/bad-data.png)

Med länkningsregler för identitetsdiagram kan du konfigurera CRM-ID:t som den unika identifieraren för att förhindra att oönskade profiler komprimeras på grund av den här typen av data.

## Nästa steg

Mer information om regler för länkning av identitetsdiagram finns i följande dokumentation:

* [Översikt över regler för länkning av identitetsdiagram](./overview.md)
* [Identitetstjänst och kundprofil i realtid](identity-and-profile.md)
* [Identitetslänkningslogik](./identity-linking-logic.md)