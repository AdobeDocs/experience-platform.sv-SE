---
title: Användningsexempel som stöds av Adobe Experience Platform Web SDK
description: Lär dig vilka användningsområden som stöds i Adobe Experience Platform Web SDK.
keywords: web sdk;användningsfall
exl-id: e0643c2c-ceb3-4ea2-aafa-1e18e0c66453
source-git-commit: ed092b85d74eaa0fdc29f3a8d28f84fe81ccca17
workflow-type: tm+mt
source-wordcount: '445'
ht-degree: 10%

---

# Användningsexempel som stöds

På den här sidan visas de användningsfall som stöds för Web SDK, med länkar till ytterligare information.

## Allmänt

| Användningsfall | Mer information |
| --- | --- |
| Enkelt strömlinjeformat SDK |  |
| Nätverk för global datainsamling |  |
| Givet samtycke |  |
| Samla in kundens samtycke enligt olika standarder | <ul><li>[Stöd för Adobe Container 2.0](../../landing/governance-privacy-security/consent/adobe/overview.md)</li><li>[Stöd för IAB TCF 2.0](../../landing/governance-privacy-security/consent/iab/overview.md)</li><li>[Integrera SDK för att skicka medgivandesignaler till Edge Network](../../landing/governance-privacy-security/consent/sdk.md)</li></ul> |
| ECID-stöd | Mer information om hur du hämtar ECID finns i vår dokumentation [här](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html?lang=en#first-party-identity) och [här](https://experienceleague.adobe.com/docs/experience-platform/edge/extension/accessing-the-ecid.html?lang=en#extension) |
| Samla in flera enheter |  |
| Stöd för Device Graph (offentlig/privat) | [Dokumentation](https://experienceleague.adobe.com/docs/analytics/components/cda/device-graph.html?lang=en) |
| Skicka data till flera organ på sidan | [Dokumentation](./interacting-with-multiple-properties.md) |
| Detaljerad felrapportering och loggar |  |
| Spåra begäranden på klientsidan och serversidan |  |
| taggtillägg | [Tilläggsdokument för Web SDK](../../tags/extensions/web/sdk/overview.md) |
| Tillgängliga felsökningsverktyg | [Felsökningstillägg ](https://experienceleague.adobe.com/docs/debugger-learn/tutorials/experience-platform-debugger/introduction-to-the-experience-platform-debugger.html?lang=en) och  [Griffon](https://aep-sdks.gitbook.io/docs/beta/project-griffon) |

{style=&quot;table-layout:auto&quot;}

## Adobe Experience Platform

| Användningsfall | Mer information |
| --- | --- |
| Skicka upplevelsehändelser |  |
| offer decisioning | [Dokumentation](../personalization/offer-decisioning/offer-decisioning-overview.md) |
| Om datauppsättningen är aktiverad för profilen kan du skicka data till kunddataprofilen i realtid |  |
| Skicka data till Customer Journey Analytics i realtid |  |
| Skriv samtycke till profil | [Dokumentation](../../landing/governance-privacy-security/consent/sdk.md) |
| Vidarebefordra data på serversidan i realtid till tredje part | [Dokumentation](../../tags/ui/event-forwarding/overview.md) |
| Stöd för identitetsnamnutrymmen |  |

{style=&quot;table-layout:auto&quot;}

## Adobe Analytics

| Användningsfall | Mer information |
| --- | --- |
| Analyser för mål (A4T) |  |
| Ingen analys för målfördröjning (A4T) |  |
| Taggar för flera programsviter |  |
| Punktfiltrering |  |
| Props, eVars och events |  |
| ListVar-stöd för Adobe Analytics |  |
| OS- och webbläsarversion |  |
| Körklara variabler | [Automatiskt mappade variabler](../data-collection/adobe-analytics/automatically-mapped-vars.md) |
| VISTA-regler/bearbetningsregler |  |
| Stöd för besökarattribut |  |
| Stöd för att avsluta länkar |  |
| Anpassade länkar/hämtningslänkar |  |
| Tillstånd och åtgärdsspårning |  |
| Händelseserialisering för standardhändelser |  |
| Variabeln Produkter | [Dokumentation](../data-collection/collect-commerce-data.md#actions-related-to-products) |

{style=&quot;table-layout:auto&quot;}

## Adobe Target

| Användningsfall | Mer information |
| --- | --- |
| Alla aktivitetstyper |  |
| Inbyggt och SPA stöd för Visual Experience Composer | [Dokumentation](../personalization/adobe-target/spa-implementation.md) |
| Formulärbaserad disposition |  |
| Stöd för global mbox | [Dokumentation](../personalization/rendering-personalization-content.md#automatically-rendering-content) |
| Anpassade mbox | [Dokumentation](../personalization/rendering-personalization-content.md#manually-rendering-content) |
| Analyser för mål (A4T) |  |
| Miljö |  |
| Stöd för arbetsytor |  |
| QA-länkar i Adobe Target |  |
| Mål baserat på geo/enhet i Adobe Target |  |
| Stöd för besökarattribut |  |
| Profilskript |  |
| XDM blir mbox-parametrar |  |
| Omdirigeringserbjudanden stöds i A4T-rapporter | [Dokumentation](https://experienceleague.adobe.com/docs/target/using/experiences/offers/offer-redirect.html?lang=en) |
| Uppdaterar målprofilen | [Dokumentation](../personalization/adobe-target/target-overview.md#single-profile-update) |
| Rekommendationer |  |
| mBox Tredje parts-ID |  |
| Svarstoken | [Dokumentation](../personalization/adobe-target/accessing-response-tokens.md) |

{style=&quot;table-layout:auto&quot;}

## Adobe Audience Manager

| Användningsfall | Mer information |
| --- | --- |
| Audience Analytics |  |
| Segmentdelning till Adobe Analytics |  |
| Stöd för besökarattribut |  |
| Partnersynkroniseringar |  |
| URL-mål |  |
| Cookie-destinationer |  |
| Miljö |  |
| Synkronisera Adobe Experience Platform-namnutrymmen med datakällor i Audience Manager |  |
| Autentiserade eller kända ID:n |  |

{style=&quot;table-layout:auto&quot;}
