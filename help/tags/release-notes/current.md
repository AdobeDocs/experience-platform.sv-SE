---
title: Versionsinformation för taggar och händelsevidarebefordran
description: Den senaste versionsinformationen om taggar och vidarebefordran av händelser i Adobe Experience Platform.
exl-id: 2ebeaa1e-64b8-48fd-b4e8-419663271a87
source-git-commit: 626330395c2d6b813d5d2157e92ada77ab4f96b1
workflow-type: tm+mt
source-wordcount: '839'
ht-degree: 2%

---

# Versionsinformation om taggar och vidarebefordran av händelser

>[!IMPORTANT]
>
>Om du flyttar framåt taggar och versionsinformation för vidarebefordran av händelser kommer de inte längre att finnas på den här sidan. Läs den senaste [Versionsinformation för Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/release-notes/latest.html?lang=en#data-collection) för detaljerade taggar och uppdateringar för händelsevidarebefordran.

## 26 april 2023

* **OAuth JWT Secret**: The [OAuth JWT Secret](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/secrets.html?lang=en) gör att kunder kan använda Adobe och Google Service Token för att stödja interaktioner mellan server och server vid händelsevidarebefordran.

Följande nya tillägg har släppts:

* **[!DNL Pinterest Conversions API]extension**: The [[!DNL Pinterest Conversions API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/pinterest/overview.html) tillägg för händelsevidarebefordran gör att du kan utnyttja data som samlats in i Adobe Experience Platform Edge Network och skicka dem till [!DNL Pinterest] i form av händelser på serversidan med [!DNL Pinterest Conversions API].

## 29 mars 2023

**Arbetsflöden för snabbstart (beta)**

Kom åt nya snabbstartarbetsflöden via&quot;Komma igång&quot; från startskärmen för datainsamling! Följande arbetsflöden är nu tillgängliga för kunder som betaversion.
* **[Meta Conversions API](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/meta/overview.html?lang=en#quick-start)**: Med Event Forwarding kan man snabbt samla in och vidarebefordra händelsedata, från serversidan till Meta för annonskonverteringar i några enkla steg.
* **[Mobile SDK](https://developer.adobe.com/client-sdks/documentation/)**: Kunderna kan snabbt implementera Mobile SDK och validera grundläggande mobilevent med bara några få enkla steg.

Nya tillägg har släppts:

* **[!DNL Braze]tillägg för händelsevidarebefordran**: The [[!DNL Braze Track Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/braze/overview.html) tillägg för händelsevidarebefordran gör att du kan utnyttja data som samlats in i Adobe Experience Platform Edge Network och skicka dem till [!DNL Braze] i form av händelser på serversidan med [!DNL Braze] API:er för användarspårning.
* **[API för Epsilon-händelser] tillägg för händelsevidarebefordran**: The [[!DNL Epsilon Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/braze/overview.html) kan du utnyttja händelsevidarebefordran för att samla in händelseinformation i Adobe Experience Platform Edge Network och skicka den till [!DNL Epsilon] med [!DNL Epsilon] Händelse-API.
* **[!DNL Mixpanel]tillägg för händelsevidarebefordran**: The [[!DNL Mixpanel Track Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/braze/overview.html) kan du utnyttja händelsevidarebefordran för att samla in händelseinformation i Adobe Experience Platform Edge Network och skicka den till [!DNL Mixpanel] med API:t för spårningshändelser.

## 25 januari 2023

* **Ny hemskärm**: Startsidan för användargränssnittet för datainsamling har uppdaterats med information om introduktion och länkar som effektiviserar produktiviteten. Det inkluderar:
   1. Dokumentation och rekommenderade arbetsflöden för att komma igång
   1. Senaste egenskaper, regler och dataelement
   1. Populära tillägg
   1. Nya tilläggsuppdateringar med en snabbinstallationsfunktion
* **Skicka data till [!DNL Google Ads] använda händelsevidarebefordran**: Nu kan du använda [[!DNL Google Ads Enhanced Conversions] API-tillägg](../extensions/server/google-ads-enhanced-conversions/overview.md) för vidarebefordran av händelser, i kombination med [Google Oauth 2 - hemligheter](../ui/event-forwarding/secrets.md#google-oauth2)för att på ett säkert sätt skicka data på serversidan till [!DNL Google Ads] i realtid.

## 23 november 2022

* **[!DNL AWS]tillägg för händelsevidarebefordran**: Nu kan du skicka data till [!DNL Amazon Web Services] ([!DNL AWS]) med [händelsevidarebefordran](../../tags/ui/event-forwarding/overview.md) tillägg. Se [[!DNL AWS] tilläggsöversikt](../../tags/extensions/server/aws/overview.md) för mer information.
* **[!DNL Google Ads Enhanced Conversions]tillägg för händelsevidarebefordran**: Nu kan du skicka konverteringsdata till [!DNL Google Ads] med [händelsevidarebefordran](../../tags/ui/event-forwarding/overview.md) tillägg. Se [[!DNL Google Ads Enhanced Conversions] tilläggsöversikt](../../tags/extensions/server/google-ads-enhanced-conversions/overview.md) för mer information.
* **[!DNL Microsoft Azure]tillägg för händelsevidarebefordran**: Nu kan du skicka data till [!DNL Microsoft Azure] med [händelsevidarebefordran](../../tags/ui/event-forwarding/overview.md) tillägg. Se [[!DNL Microsoft Azure] tilläggsöversikt](../../tags/extensions/server/azure/overview.md) för mer information.

## 26 oktober 2022

* **Känslig datahantering för datastreams**: Datastreams utnyttjar nu flera plattformstekniker för att hantera känsliga data på ett lämpligt sätt, i enlighet med bestämmelser som HIPAA (Health Insurance Portability and Accounability Act). Se avsnittet om [hantera känsliga data i dataströmmar](../../edge/datastreams/overview.md#sensitive) för mer information.
* **[!DNL Splunk]tillägg för händelsevidarebefordran**: Nu kan du skicka data till [!DNL Splunk] med [händelsevidarebefordran](../ui/event-forwarding/overview.md) tillägg. Se [[!DNL Splunk] tilläggsöversikt](../extensions/server/splunk/overview.md) för mer information.
* **[!DNL Zendesk]tillägg för händelsevidarebefordran**: Nu kan du skicka data till [!DNL Zendesk] med [händelsevidarebefordran](../ui/event-forwarding/overview.md) tillägg. Se [[!DNL Zendesk] tilläggsöversikt](../extensions/server/zendesk/overview.md) för mer information.

## 28 september 2022

* **Integrering med vänster navigering i Adobe Experience Platform**: Alla funktioner som tidigare var exklusiva för användargränssnittet för datainsamling (inklusive taggar och vidarebefordran av händelser) finns nu även tillgängliga via den vänstra navigeringen i användargränssnittet för Experience Platform, under kategorin **[!UICONTROL Data Collection]**. Detta eliminerar behovet av att växla mellan användargränssnitt när du arbetar med datainsamlingsfunktioner i Platform.
* **Användarattribuering i taggar och händelsevidarebefordran**: När tillgängliga egenskaper listas i taggar och händelsevidarebefordring visas nu alla angivna egenskaper när de senast uppdaterades och av vem.
* **[[!DNL Snap Conversions API] extension](https://exchange.adobe.com/apps/ec/108550) för vidarebefordran av händelser**: Nu kan du skicka data till [!DNL Snapchat Conversions API] med [händelsevidarebefordran](../../tags/ui/event-forwarding/overview.md) tillägg. Mer information om hur du autentiserar och använder API:t finns i [[!DNL Snapchat Marketing API] dokumentation](https://marketingapi.snapchat.com/docs/conversion.html).

## 27 juli 2022

* Tillgång till taggar och funktioner för vidarebefordran av händelser hanteras nu via Adobe Admin Console under kortet för Adobe Experience Platform Data Collection. Se guiden [behörigheter för datainsamling](../../collection/permissions.md) för mer information.
* Stöd för Internet Explorer 10 och 11 har lagts till [föråldrad](../ie-deprecation.md).

## 22 juni 2022

Nya tillägg har släppts:

* [Google Data Layer-taggtillägg](../extensions/client/google-data-layer/overview.md): Gör att du kan använda ett Google-datalager i taggimplementeringen.
* [Google Ads Enhanced Conversions event forward extension](https://partners.adobe.com/exchangeprogram/experiencecloud/exchange.details.108630.html): Gör att du kan förbättra dina Google Ads-konverteringar i realtid.
* [Vidarekoppling av händelse för Mailchimp](../extensions/server/mailchimp/overview.md): Skickar händelser till Mailchimp Marketing API som kan utlösa e-postmeddelanden för marknadsföringskampanjer, resor eller transaktioner för Mailchimp.