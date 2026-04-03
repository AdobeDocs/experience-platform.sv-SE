---
title: Stöd för enhetlig identitet i datainsamling
description: Läs om hur det enhetliga identitetsstödet samlar förstahandspersonens beständighet och tredjepartsaktivering i webbdatainsamlingen.
hide: true
hidefromtoc: true
badge: Beta
source-git-commit: 32c2565d31eed4eda28195afaf82aac6f04a6f8a
workflow-type: tm+mt
source-wordcount: '1029'
ht-degree: 2%

---

# Stöd för enhetlig identitet i datainsamling

>[!AVAILABILITY]
>
>Den här funktionen är för närvarande i betaversion. Tillgänglighet, beteende och dokumentation kan ändras.

Tack vare stödet för enhetliga identiteter kan Edge Network arbeta med både egna och externa identitetskontexter. Den sammanför beständig förstapartidentifiering av ägda egendomar med aktiveringsarbetsflöden från tredje part i webbläsare som stöder cookies från tredje part. Bakgrund om hur Web SDK hanterar ECID:n, FPID:n och andra identitetssignaler finns i [Identitet i datainsamling](./overview.md).

Med stöd för enhetlig identitet kan ni

* **Maximera målgruppens räckvidd**: Aktivera dina Experience Platform-målgrupper på tredjepartsmål (DSP, SSP och nätverk) för en större andel av trafiken.
* **Behåll mätnoggrannheten**: Håll besökaridentifieringen konsekvent över ägda fastigheter och annonsplattformar.
* **Framtidssäkra implementeringen**: Använd enhets-ID:n från första part som grund samtidigt som du behåller kompatibiliteten med arbetsflöden för aktivering från tredje part.

När en besökare anländer till er webbplats utvärderar Edge Network tillgängliga identitetssignaler - länkar automatiskt första parts- och tredjepartssammanhang när villkoren tillåter det. Webbläsare som blockerar cookies från tredje part fortsätter att fungera i förstahandsläge utan att implementeringen avbryts.

## Så fungerar det

Edge Network genererar ECID:n genom att utvärdera tillgängliga identitetssignaler i följande prioritetsordning:

| Prioritet | Källa | Kontext | Beteende |
| --- | --- | --- | --- |
| 1 | **Demdex-ID** | Tredje part | Om det finns ett Demdex-ID dirigeras ECID från det. Denna fras ger ett konsekvent ECID i alla domäner som delar samma cookie från tredje part. |
| 2 | **FPID** | Förste part | Om det inte finns något Demdex-ID men det finns ett FPID, dirigeras ECID från FPID och ett Demdex-ID härleds från det. |
| 3 | **Random** | Förste part | Om varken ett Demdex-ID eller ett FPID är tillgängligt genereras ett nytt slumpmässigt ECID och ett Demdex-ID härleds från det. |

ECID och Demdex ID är kryptografiskt länkade genom en deterministisk algoritm, vilket innebär att ett kan härledas från det andra. Detta är en relation som gör det möjligt för Edge Network att översätta mellan identitetskontexter från första part och tredje part utan att det krävs någon separat logik för besökshantering i implementeringen.

Eftersom relationen är deterministisk kan målgrupper som bygger på ECID:n från första part aktiveras via tredjepartsinfrastruktur när motsvarande Demdex ID är tillgängligt.

För besökare som redan har ett FPID-härlett ECID kan Edge Network automatiskt länka sin förstapartidentitet till tredjepartsidentitetskontexten. Detta sker transparent när webbläsaren stöder cookies från tredje part och inte kräver några ändringar i implementeringen. När automatisk länkning sker:

1. Edge Network upptäcker att besökarens ECID inte härletts från ett Demdex-ID.
1. Om besökarens webbläsare stöder cookies från tredje part aktiveras en enkel identitetssynkronisering.
1. Systemet skapar en länk mellan besökarens första part-ECID och deras tredje parts identitet.
1. Länken lagras i identitetsbutiken, vilket möjliggör målgruppsaktivering på tredjepartsdestinationer.

Automatisk länkning bevarar befintliga ECID:n och förhindrar att besökaren klipper av. Med tiden blir fler av er målgrupp successivt berättigade till tredjepartsaktivering när besökarna kommer tillbaka och länkar uppstår.

Aktivering av målgrupp från tredje part kräver ID-synkronisering (ID-synkronisering). När Edge Network upprättar eller uppdaterar en tredje parts identitet returneras synkroniseringsinstruktioner i svaret. Dessa instruktioner instruerar webbläsaren att synkronisera besökarens identitet med partnerdomäner (DSP, annonsnätverk och andra aktiveringsplattformar) så att era Experience Platform-målgrupper kan matchas och levereras på dessa plattformar.

## Förutsättningar

Stöd för enhetlig identitet kräver följande:

* Webbplatsen använder datainsamling från första part på en domän som du kontrollerar.
* Implementeringen använder FPID:n eller någon annan förstapartsstrategi som grund.
* Cookies från tredje part aktiveras i din Web SDK-konfiguration.
* Synkronisering av tredjeparts-ID har aktiverats för datastream.
* Besökaren använder en webbläsare som tillåter cookies från tredje part (se [Webbläsarkompatibilitet](#browser-compatibility) nedan).

## Konfiguration

1. **Aktivera cookies från tredje part i Web SDK**: Aktivera inställningen **Använd cookies från tredje part** i Web SDK-implementeringen. Aktivera **[!UICONTROL Use third-party cookies]** i [Identitetskonfigurationsinställningar](/help/tags/extensions/client/web-sdk/configure/identity.md#use-third-party-cookies) om du använder taggtillägget. Om du använder JavaScript-biblioteket anger du [`thirdPartyCookiesEnabled`](/help/collection/js/commands/configure/thirdpartycookiesenabled.md) till `true`.

1. **Aktivera synkronisering av ID från tredje part i datastream**: Aktivera alternativet **[!UICONTROL Third-Party ID Sync]** i datastreams avancerade inställningar. Se [Skapa och konfigurera datastreams](/help/datastreams/configure.md#advanced-options).

1. **Kontrollera att förstapartsbeständighet finns**: Bekräfta att din förstapartsstrategi för beständighet (som FPID) redan har distribuerats till din ägda domän. Se [ID:n för första part i datainsamlingen](fpid.md).

## Validering

Så här kontrollerar du att stöd för enhetlig identitet fungerar:

1. Öppna webbläsarens utvecklarverktyg och gå till fliken **Nätverk**.
1. Rensa befintliga förfrågningar och utlösa en Web SDK-händelse (sidinläsning eller anpassad händelse) i en ny eller inkog session.
1. Hitta Edge Network-svaret (sök efter anrop till `adobedc.demdex.net` och din första samlingens slutpunkt).
1. Kontrollera svarsnyttolasten för instruktioner om ID-synkronisering.

När det finns instruktioner för synkronisering av ID, innehåller svaret en `identity:exchange`-referens som liknar följande:

```json
{
  "handle": [
    {
      "type": "identity:exchange",
      "payload": [
        {
          "type": "url",
          "id": 411,
          "spec": {
            "url": "https://example.com/...",
            "hideReferrer": false,
            "ttlMinutes": 10080
          }
        },
        {
          "type": "url",
          "id": 89,
          "spec": {
            "url": "https://example.org/...",
            "hideReferrer": true,
            "ttlMinutes": 10080
          }
        }
      ]
    }
  ]
}
```

| Element | Beskrivning |
| --- | --- |
| `type: "identity:exchange"` | Anger att det finns instruktioner för synkronisering av ID. |
| `payload`-matris | Lista över synkroniserings-URL:er för partner-ID. |
| `url` värden | Omdirigera URL:er till partnerdomäner för synkronisering av ID. |
| `id` värden | Partneridentifierare. |

>[!TIP]
>
>Om du inte ser handtaget `identity:exchange` i svaret:
>
>* Kontrollera att du testar med en ny eller inkognitiv webbläsarsession. Befintliga identiteter utlöser inte nya synkroniseringar.
>* Kontrollera att inställningarna för både datastream och Web SDK är korrekt konfigurerade.
>* Bekräfta att du använder en webbläsare som stöder cookies från tredje part (se tabellen nedan).

När synkroniseringsaktiviteten har bekräftats validerar du följande:

* Första parts identitet kvarstår som förväntat över sidinläsning på din ägda domän.
* Aktiverings- och rapporteringsflöden fungerar som förväntat i de miljöer du stöder.

## Webbläsarkompatibilitet {#browser-compatibility}

Identitetsfunktioner från tredje part är beroende av webbläsarstöd för cookies från tredje part. I följande tabell sammanfattas det förväntade beteendet:

| Webbläsare | Stöd för cookies från tredje part | Demdex finns | Identitetsbeteende |
| --- | --- | --- | --- |
| Google Chrome | Stöds | Ja | Demdex → ECID (konsekvent mellan domäner) |
| Microsoft Edge | Stöds som standard | Ja | Demdex → ECID (konsekvent mellan domäner) |
| Mozilla Firefox | Blockerad som standard (ETP) | Nej (som standard) | FPID → ECID (per domän) |
| Apple Safari | Blockerad (ITP) | Nej | FPID → ECID (per domän) |

För webbläsare som blockerar cookies från tredje part fortsätter identifieringen av första part att fungera som vanligt. Aktiveringsfunktioner från tredje part är bara tillgängliga när webbläsaren tillåter cookies från tredje part.

## Begränsningar

* Identitetsbeteendet hos tredje part beror helt på besökarens webbläsare som tillåter cookies från tredje part. Det finns ingen reservlösning för tredjepartsaktivering i webbläsare som blockerar dem.
* Automatisk länkning kräver att besökaren återvänder till webbplatsen. Andelen av er målgrupp som är berättigad till aktivering från tredje part ökar gradvis med tiden.
