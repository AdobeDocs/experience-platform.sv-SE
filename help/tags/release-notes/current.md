---
title: Versionsinformation för taggar och vidarebefordran av händelser
description: Den senaste versionsinformationen om taggar och vidarebefordran av händelser i Adobe Experience Platform.
exl-id: 2ebeaa1e-64b8-48fd-b4e8-419663271a87
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '771'
ht-degree: 93%

---

# Versionsinformation för taggar och vidarebefordran av händelser

>[!IMPORTANT]
>
>I fortsättningen kommer versionsinformation om taggar och vidarebefordran av händelser inte längre att finnas på den här sidan. Se den senaste [versionsinformationen för Adobe Experience-plattformen](https://experienceleague.adobe.com/docs/experience-platform/release-notes/latest.html#data-collection) för detaljerade uppdateringar av taggar och vidarebefordran av händelser.

## 26 april 2023

* **OAuth JWT-hemlighet**: Med [OAuth JWT-hemlighet](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/secrets.html) kan kunder använda Adobe- och Google Service-tokens för att stödja server-till-server-interaktioner i vidarebefordran av händelser.

Följande nya tillägg har släppts:

* **[!DNL Pinterest Conversions API]tillägg**: Med tillägget för [[!DNL Pinterest Conversions API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/pinterest/overview.html) vidarebefordran av händelser kan du utnyttja data som samlats in i Adobe Experience-plattformens Edge Network och skicka dem till [!DNL Pinterest] i form av händelser på serversidan med hjälp av [!DNL Pinterest Conversions API].

## 29 mars 2023

**Snabbstartsarbetsflöden (Beta)**

Få tillgång till nya arbetsflöden för snabbstart under ”Komma igång” från startskärmen för datainsamling! Följande arbetsflöden finns nu tillgängliga för kunder som en publik Beta.
* **[Meta-konverteringar API](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/meta/overview.html#quick-start)**: Kunder med vidarebefordran av händelser kan snabbt samla in och vidarebefordra händelsedata från serversidan till Meta för annonskonverteringar med några enkla steg.
* **[Mobil SDK](https://developer.adobe.com/client-sdks/documentation/)**: Kunderna kan snabbt implementera mobil SDK och validera grundläggande mobilhändelser med några enkla steg.

Nya tillägg har släppts:

* **[!DNL Braze]Tillägget för vidarebefordran av händelser**: Med tillägget för vidarebefordran av händelser [[!DNL Braze Track Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/braze/overview.html) kan du utnyttja data som samlas in i Adobe Experience-plattformens Edge Network och skicka dem till [!DNL Braze] i form av händelser på serversidan med hjälp av API:erna för användarspår [!DNL Braze].
* Tillägget för vidarebefordran av händelser **[Epsilon-händelser-API]**: Med tillägget [[!DNL Epsilon Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/braze/overview.html) kan du utnyttja vidarebefordran av händelser för att samla in händelseinformation i Adobe Experience-plattformen Edge Network och skicka den till [!DNL Epsilon] med hjälp av [!DNL Epsilon] händelse-API:et.
* **[!DNL Mixpanel]Tillägg för vidarebefordran av händelser**: Med tillägget [[!DNL Mixpanel Track Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/braze/overview.html) kan du utnyttja vidarebefordran av händelser för att samla in händelseinformation i Adobe Experience-plattformens Edge Network och skicka den till [!DNL Mixpanel] med hjälp av API:et Spåra händelser.

## 25 januari 2023

* **Ny startsida**: Startsidan för datainsamlingsgränssnittet har uppdaterats och innehåller nu användbar information och länkar för att effektivisera produktiviteten. Detta inkluderar:
   1. Dokumentation och rekommenderade arbetsflöden för att komma igång
   1. Nya egenskaper, regler och dataelement
   1. Populära tillägg
   1. Nya tilläggsuppdateringar med en snabbinstallationsfunktion
* **Skicka data till [!DNL Google Ads] med hjälp av vidarebefodran av händelser**: Du kan nu använda [[!DNL Google Ads Enhanced Conversions] API-tillägget](../extensions/server/google-ads-enhanced-conversions/overview.md) för vidarebefodran av händelser i kombination med [Google Oauth 2-hemligheter](../ui/event-forwarding/secrets.md#google-oauth2) för att säkert skicka data på serversidan till [!DNL Google Ads] i realtid.

## 23 november 2022

* **[!DNL AWS]tillägg för vidarebefordran av händelser**: Du kan nu skicka data till [!DNL Amazon Web Services] ([!DNL AWS]) med hjälp av ett [tillägg för vidarebefordran av händelser](../../tags/ui/event-forwarding/overview.md). Se [[!DNL AWS] översikten över tillägg](../../tags/extensions/server/aws/overview.md) för mer information.
* **[!DNL Google Ads Enhanced Conversions]tillägg för vidarebefordran av händelser**: Du kan nu skicka konverteringsdata till [!DNL Google Ads] med hjälp av ett [tillägg för vidarebefordran av händelser](../../tags/ui/event-forwarding/overview.md). Se [[!DNL Google Ads Enhanced Conversions] översikten över tillägg](../../tags/extensions/server/google-ads-enhanced-conversions/overview.md) för mer information.
* **[!DNL Microsoft Azure]tillägg för vidarebefordran av händelser**: Du kan nu skicka data till [!DNL Microsoft Azure] med hjälp av tillägget för [vidarebefordran av händelser](../../tags/ui/event-forwarding/overview.md). Se [[!DNL Microsoft Azure] översikten över tillägg](../../tags/extensions/server/azure/overview.md) för mer information.

## 26 oktober 2022

* **Känslig datahantering för datastreams**: Datastreams utnyttjar nu flera Experience Platform-tekniker för att hantera känsliga data på lämpligt sätt, vilket regleras av bestämmelser som HIPAA (Health Insurance Portability and Accounability Act). Mer information finns i avsnittet om [hantering av känsliga data i dataströmmar](../../datastreams/overview.md#sensitive).
* **[!DNL Splunk]tillägg för vidarebefordran av händelser**: Du kan nu skicka data till [!DNL Splunk] med hjälp av ett tillägg för [vidarebefordran av händelser](../ui/event-forwarding/overview.md). Se [[!DNL Splunk] översikten över tillägg](../extensions/server/splunk/overview.md) för mer information.
* **[!DNL Zendesk]tillägg för vidarebefordran av händelser**: Du kan nu skicka data till [!DNL Zendesk] med hjälp av tillägget för [vidarebefordran av händelser](../ui/event-forwarding/overview.md). Se [[!DNL Zendesk] översikten över tillägg](../extensions/server/zendesk/overview.md) för mer information.

## 28 september 2022

* **Adobe Experience Platforms vänstra navigeringsintegration**: Alla funktioner som tidigare var exklusiva för datainsamlingsgränssnittet (inklusive taggar och vidarebefordran av händelser) är nu också tillgängliga via vänster navigering i Experience Platforms gränssnitt under kategorin **[!UICONTROL Data Collection]**. Detta eliminerar behovet av att växla mellan användargränssnitt när du arbetar med datainsamlingsfunktioner i Experience Platform.
* **Användartillskrivning i taggar och vidarebefordran av händelser**: När tillgängliga egenskaper listas i taggar och vidarebefordran av händelser, visas nu när den senast uppdaterades och av vem för varje listad egenskap.
* **[[!DNL Snap Conversions API] tillägg](https://exchange.adobe.com/apps/ec/108550) för vidarebefordran av händelser**: Du kan nu skicka data till [!DNL Snapchat Conversions API] med hjälp av ett tillägg för [vidarebefordran av händelser](../../tags/ui/event-forwarding/overview.md). Mer information om hur du autentiserar dig och använder API:et finns i [[!DNL Snapchat Marketing API] dokumentationen](https://marketingapi.snapchat.com/docs/conversion.html).

## 27 juli 2022

* Åtkomst till taggar och funktioner för vidarebefordran av händelser hanteras nu via Adobe Admin Console under kortet för datainsamling för Adobe Experience Platform. Mer information finns i guiden om [behörigheter för datainsamling](../../collection/permissions.md).
* Stöd för Internet Explorer 10 och 11 har [avskaffats](../ie-deprecation.md).

## 22 juni 2022

Nya tillägg har släppts:

* [Taggtillägg för Googles datalager](../extensions/client/google-data-layer/overview.md): Gör att du kan använda ett Google-datalager i din taggimplementering.
* [Google Ads förbättrade konverteringar-tillägg för vidarebefordran av händelser](https://partners.adobe.com/exchangeprogram/experiencecloud/exchange.details.108630.html): Gör att du kan förbättra dina Google Ads-konverteringar i realtid.
* [Tillägg för vidarebefordran av händelser från Mailchimp](../extensions/server/mailchimp/overview.md): Skickar händelser till Mailchimps marknadsförings-API som kan utlösa e-postmeddelanden för Mailchimp-marknadsföringskampanjer, resor eller transaktioner.