---
keywords: Experience Platform;identitet;identitetstjänst;felsökning;skyddsräcken;riktlinjer;gräns;
title: Gardrutor för identitetstjänsten
description: Det här dokumentet innehåller information om användning och hastighetsgränser för identitetstjänstens data som hjälper dig att optimera din användning av identitetsdiagrammet.
exl-id: bd86d8bf-53fd-4d76-ad01-da473a1999ab
source-git-commit: e6d0f0d0bc3de2f6da4e4269811d254db4fa3303
workflow-type: tm+mt
source-wordcount: '445'
ht-degree: 2%

---

# Guardrails för [!DNL Identity Service] data

Det här dokumentet innehåller information om användning och hastighetsbegränsningar för [!DNL Identity Service] data som hjälper dig att optimera användningen av identitetsdiagrammet. När du granskar följande skyddsutkast förutsätts det att du har modellerat data korrekt. Om du har frågor om hur du modellerar data kan du kontakta kundtjänstrepresentanten.

## Komma igång

Följande Experience Platform-tjänster är involverade i modellering av identitetsdata:

* [Identiteter](home.md): Överbrygga identiteter från olika datakällor när de hämtas till Platform.
* [[!DNL Real-time Customer Profile]](../profile/home.md): Skapa enhetliga kundprofiler med hjälp av data från flera källor.

## Begränsningar för datamodell

Tabellerna nedan innehåller riktlinjer för skyddsförslag för statiska gränser samt valideringsregler för identitetsnamnutrymmen.

### Statiska gränser

I följande tabell visas statiska gränser för identitetsdata.

| Guardrail | Gräns | Anteckningar |
| --- | --- | --- |
| Antal identiteter i ett diagram | 150 | Gränsen tillämpas på sandlådenivå. Identitetsdiagrammet uppdateras inte när gränsen har nåtts. |
| Antal identiteter i en XDM-post | 20 | Det minsta antalet XDM-poster som krävs är två. |
| Antal anpassade namnutrymmen | Ingen | Det finns inga gränser för hur många anpassade namnutrymmen du kan skapa. |
| Antal diagram | Ingen | Det finns inga gränser för hur många identitetsdiagram du kan skapa. |
| Antal tecken för ett namnområdes visningsnamn eller identitetssymbol | Ingen | Det finns inga gränser för hur många tecken ett namnområdes visningsnamn eller identitetssymbol får innehålla. |

### Validering av identitetsvärde

Följande tabell visar befintliga regler som du måste följa för att identitetsvärdet ska kunna valideras korrekt.

| Namnutrymme | Valideringsregel | Systembeteende när regeln bryts |
| --- | --- | --- |
| ECID | <ul><li>Identitetsvärdet för ett ECID måste vara exakt 38 tecken.</li><li>Identitetsvärdet för ett ECID får endast bestå av siffror.</li></ul> | <ul><li>Om identitetsvärdet för ECID inte är exakt 38 tecken hoppas posten över.</li><li>Om identitetsvärdet för ECID innehåller icke-numeriska tecken hoppas posten över.</li></ul> |
| Ej ECID | Identitetsvärdet får inte vara längre än 1 024 tecken. | Om identitetsvärdet är längre än 1 024 tecken hoppas posten över. |

### Inläsning av namnområde för identitet

Från och med 31 januari 2023 blockerar identitetstjänsten intag av Adobe Analytics ID (AAID) för nya kunder. Den här identiteten hämtas vanligtvis via [Adobe Analytics-källa](../sources/connectors/adobe-applications/analytics.md) och [Adobe Audience Manager-källa](../sources//connectors/adobe-applications/audience-manager.md) och är överflödigt eftersom ECID representerar samma webbläsare. Kontakta din kontoansvarige om du vill ändra den här standardkonfigurationen.

## Nästa steg

Mer information om [!DNL Identity Service]:

* [[!DNL Identity Service] översikt](home.md)
* [Identitetsdiagramvisningsprogram](ui/identity-graph-viewer.md)
