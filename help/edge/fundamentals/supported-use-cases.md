---
title: Användningsexempel som stöds av Adobe Experience Platform Web SDK
description: Lär dig vilka användningsområden som stöds i Adobe Experience Platform Web SDK.
keywords: web sdk;användningsfall
source-git-commit: e012e12a8cadb8c13781b0380d84652c23567180
workflow-type: tm+mt
source-wordcount: '565'
ht-degree: 8%

---


# Användningsexempel som stöds

På den här sidan visas de användningsfall som stöds för Web SDK, med länkar till ytterligare information.

## Allmänt

| Användningsfall | Mer information |
| --- | --- |
| Enkelt strömlinjeformat SDK |  |
| Nätverk för global datainsamling |  |
| Givet samtycke |  |
| IAB 2.0 medgivandesträngar | [Stöd för IAB TCF 2.0](https://experienceleague.adobe.com/docs/experience-platform/edge/consent/iab-tcf/overview.html?lang=en#consent) |
| Samla in detaljerat samtycke | [Integrera Web SDK med Adobe 2.0-medgivande](https://experienceleague.adobe.com/docs/experience-platform/landing/governance-privacy-security/consent/adobe/sdk.html#prerequisites) |
| ECID-stöd | Mer information om hur du hämtar ECID finns i vår dokumentation [här](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html?lang=en#first-party-identity) och [här](https://experienceleague.adobe.com/docs/experience-platform/edge/extension/accessing-the-ecid.html?lang=en#extension) |
| Samla in flera enheter |  |
| Stöd för Device Graph (offentlig/privat) | [Dokumentation](https://experienceleague.adobe.com/docs/analytics/components/cda/device-graph.html?lang=en) |
| Skicka data till flera organ på sidan | [Dokumentation](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/interacting-with-multiple-properties.html?lang=en#fundamentals) |
| Detaljerad felrapportering och loggar |  |
| Spåra begäranden på klientsidan och serversidan |  |
| taggtillägg | [Tilläggsdokument för Web SDK](../../tags/extensions/web/sdk/overview.md) |
| Tillgängliga felsökningsverktyg | [Felsökningstillägg ](https://experienceleague.adobe.com/docs/debugger-learn/tutorials/experience-platform-debugger/introduction-to-the-experience-platform-debugger.html?lang=en) och  [Griffon](https://aep-sdks.gitbook.io/docs/beta/project-griffon) |

{style=&quot;table-layout:auto&quot;}

## Adobe Experience Platform

| Användningsfall | Mer information |
| --- | --- |
| Skicka upplevelsehändelser |  |
| offer decisioning | [Dokumentation](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/offer-decisioning/offer-decisioning-overview.html?lang=en#personalization) |
| Om datauppsättningen är aktiverad för profilen kan du skicka data till kunddataprofilen i realtid |  |
| Skicka data till Customer Journey Analytics i realtid |  |
| Skriv samtycke till profil | [Dokumentation](https://experienceleague.adobe.com/docs/experience-platform/landing/governance-privacy-security/consent/adobe/sdk.html?lang=en) |
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
| Körklara variabler | [Automatiskt mappade variabler](https://experienceleague.adobe.com/docs/experience-platform/edge/data-collection/adobe-analytics/automatically-mapped-vars.html?lang=en#data-collection) |
| VISTA-regler/bearbetningsregler |  |
| Stöd för besökarattribut |  |
| Stöd för att avsluta länkar |  |
| Anpassade länkar/hämtningslänkar |  |
| Tillstånd och åtgärdsspårning |  |
| Händelseserialisering för standardhändelser |  |
| Variabeln Produkter | [Dokumentation](https://experienceleague.adobe.com/docs/experience-platform/edge/data-collection/collect-commerce-data.html?lang=en#actions-related-to-products) |

{style=&quot;table-layout:auto&quot;}

## Adobe Target

| Användningsfall | Mer information |
| --- | --- |
| Alla aktivitetstyper |  |
| Inbyggt och SPA stöd för Visual Experience Composer | [Dokumentation](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/spa-implementation.html?lang=en#personalization) |
| Formulärbaserad disposition |  |
| Stöd för global mbox | [Dokumentation](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/rendering-personalization-content.html?lang=en#automatically-rendering-content) |
| Anpassade mbox | [Dokumentation](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/rendering-personalization-content.html?lang=en#manually-rendering-content) |
| Analyser för mål (A4T) |  |
| Miljö |  |
| Stöd för arbetsytor |  |
| QA-länkar i Adobe Target |  |
| Mål baserat på geo/enhet i Adobe Target |  |
| Stöd för besökarattribut |  |
| Profilskript |  |
| XDM blir mbox-parametrar |  |
| Omdirigeringserbjudanden stöds i A4T-rapporter | [Dokumentation](https://experienceleague.adobe.com/docs/target/using/experiences/offers/offer-redirect.html?lang=en) |
| Uppdaterar målprofilen | [Dokumentation](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/target-overview.html?lang=en#single-profile-update) |
| Rekommendationer |  |
| mBox Tredje parts-ID |  |
| Svarstoken | [Dokumentation](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/accessing-response-tokens.html?lang=en) |

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
