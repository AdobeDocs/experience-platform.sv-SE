---
title: Versionsinformation för taggar och händelsevidarebefordran
description: Den senaste versionsinformationen om taggar och vidarebefordran av händelser i Adobe Experience Platform.
exl-id: 2ebeaa1e-64b8-48fd-b4e8-419663271a87
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '769'
ht-degree: 1%

---

# Versionsinformation om taggar och vidarebefordran av händelser

>[!IMPORTANT]
>
>Om du flyttar framåt taggar och versionsinformation för vidarebefordran av händelser kommer de inte längre att finnas på den här sidan. Läs den senaste [versionsinformationen för Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/release-notes/latest.html#data-collection) om du vill ha detaljerade taggar och uppdateringar för vidarebefordran av händelser.

## 26 april 2023

* **OAuth JWT-hemlighet**: Med [OAuth JWT-hemlighet](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/secrets.html) kan kunder använda Adobe- och Google-tjänsttoken för att ge stöd för server-till-server-interaktioner vid händelsevidarebefordran.

Följande nya tillägg har släppts:

* **[!DNL Pinterest Conversions API]tillägg**: Med tillägget [[!DNL Pinterest Conversions API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/pinterest/overview.html) för händelsevidarebefordran kan du utnyttja data som har samlats in i Adobe Experience Platform Edge Network och skicka det till [!DNL Pinterest] i form av händelser på serversidan med hjälp av [!DNL Pinterest Conversions API].

## 29 mars 2023

**Arbetsflöden för snabbstart (Beta)**

Kom åt nya snabbstartarbetsflöden via&quot;Komma igång&quot; från startskärmen för datainsamling! Följande arbetsflöden är nu tillgängliga för kunder som offentlig Beta.
* **[API:t för metakonvertering](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/meta/overview.html#quick-start)**: Kunder som vill vidarebefordra händelser kan snabbt samla in och vidarebefordra händelsedata, från serversidan till meta för annonskonverteringar i några enkla steg.
* **[Mobile SDK](https://developer.adobe.com/client-sdks/documentation/)**: Kunder kan snabbt implementera Mobile SDK och validera grundläggande mobilhändelser med bara några få enkla steg.

Nya tillägg har släppts:

* **[!DNL Braze]-tillägg för händelsevidarebefordring**: Med tillägget [[!DNL Braze Track Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/braze/overview.html) för händelsevidarebefordran kan du utnyttja data som samlats in i Adobe Experience Platform Edge Network och skicka det till [!DNL Braze] i form av händelser på serversidan med API:erna för användarspårning i [!DNL Braze].
* **[API:t för Epsilon-händelser] tillägg för händelsevidarebefordran**: Med tillägget [[!DNL Epsilon Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/braze/overview.html) kan du utnyttja händelsevidarebefordran för att hämta händelseinformation i Adobe Experience Platform Edge Network och skicka den till [!DNL Epsilon] med hjälp av händelse-API:t [!DNL Epsilon].
* **[!DNL Mixpanel]-tillägg för händelsevidarebefordran**: Med tillägget [[!DNL Mixpanel Track Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/braze/overview.html) kan du utnyttja händelsevidarebefordran för att samla in händelseinformation i Adobe Experience Platform Edge Network och skicka den till [!DNL Mixpanel] med API:t för spårningshändelser.

## 25 januari 2023

* **Ny hemskärm**: Startsidan för användargränssnittet för datainsamling har uppdaterats med praktisk startinformation och länkar för att effektivisera produktiviteten. Detta omfattar följande:
   1. Dokumentation och rekommenderade arbetsflöden för att komma igång
   1. Senaste egenskaper, regler och dataelement
   1. Populära tillägg
   1. Nya tilläggsuppdateringar med en snabbinstallationsfunktion
* **Skicka data till [!DNL Google Ads] med händelsevidarebefordran**: Nu kan du använda [[!DNL Google Ads Enhanced Conversions] API-tillägget](../extensions/server/google-ads-enhanced-conversions/overview.md) för händelsevidarebefordran, kombinerat med [Google Oauth 2-hemligheter](../ui/event-forwarding/secrets.md#google-oauth2), för att skicka data på serversidan säkert till [!DNL Google Ads] i realtid.

## 23 november 2022

* **[!DNL AWS]-tillägg för händelsevidarebefordran**: Nu kan du skicka data till [!DNL Amazon Web Services] ([!DNL AWS]) med ett [vidarebefordringstillägg](../../tags/ui/event-forwarding/overview.md). Mer information finns i [[!DNL AWS] tilläggsöversikten](../../tags/extensions/server/aws/overview.md).
* **[!DNL Google Ads Enhanced Conversions]-tillägg för vidarebefordran av händelser**: Du kan nu skicka konverteringsdata till [!DNL Google Ads] med ett [vidarebefordringstillägg för händelser](../../tags/ui/event-forwarding/overview.md). Mer information finns i [[!DNL Google Ads Enhanced Conversions] tilläggsöversikten](../../tags/extensions/server/google-ads-enhanced-conversions/overview.md).
* **[!DNL Microsoft Azure]-tillägg för vidarebefordran av händelser**: Du kan nu skicka data till [!DNL Microsoft Azure] med ett [vidarebefordringstillägg för händelser](../../tags/ui/event-forwarding/overview.md). Mer information finns i [[!DNL Microsoft Azure] tilläggsöversikten](../../tags/extensions/server/azure/overview.md).

## 26 oktober 2022

* **Känslig datahantering för datastreams**: Datastreams utnyttjar nu flera plattformstekniker för att hantera känsliga data på lämpligt sätt, vilket regleras av bestämmelser som HIPAA (Health Insurance Portability and Accounability Act). Mer information finns i avsnittet [Hantera känsliga data i dataströmmar](../../datastreams/overview.md#sensitive).
* **[!DNL Splunk]-tillägg för vidarebefordran av händelser**: Du kan nu skicka data till [!DNL Splunk] med ett [vidarebefordringstillägg för händelser](../ui/event-forwarding/overview.md). Mer information finns i [[!DNL Splunk] tilläggsöversikten](../extensions/server/splunk/overview.md).
* **[!DNL Zendesk]-tillägg för vidarebefordran av händelser**: Du kan nu skicka data till [!DNL Zendesk] med ett [vidarebefordringstillägg för händelser](../ui/event-forwarding/overview.md). Mer information finns i [[!DNL Zendesk] tilläggsöversikten](../extensions/server/zendesk/overview.md).

## 28 september 2022

* **Adobe Experience Platform vänsterintegrering för navigering**: Alla funktioner som tidigare var exklusiva för användargränssnittet för datainsamling (inklusive taggar och vidarebefordran av händelser) är nu även tillgängliga via den vänstra navigeringen i användargränssnittet för Experience Platform, under kategorin **[!UICONTROL Data Collection]**. Detta eliminerar behovet av att växla mellan användargränssnitt när du arbetar med datainsamlingsfunktioner i Platform.
* **Användarattribuering i taggar och händelsevidarebefordran**: När tillgängliga egenskaper listas i taggar och händelsevidarebefordran visas nu varje egenskap i listan när den senast uppdaterades och av vem.
* **[[!DNL Snap Conversions API] tillägg](https://exchange.adobe.com/apps/ec/108550) för vidarebefordran av händelser**: Du kan nu skicka data till [!DNL Snapchat Conversions API] med ett [vidarebefordrande](../../tags/ui/event-forwarding/overview.md)-tillägg. Mer information om hur du autentiserar och använder API:t finns i [[!DNL Snapchat Marketing API] dokumentationen](https://marketingapi.snapchat.com/docs/conversion.html).

## 27 juli 2022

* Tillgång till taggar och funktioner för vidarebefordran av händelser hanteras nu via Adobe Admin Console under kortet för Adobe Experience Platform Data Collection. Mer information finns i guiden om [behörighet för datainsamling](../../collection/permissions.md).
* Stöd för Internet Explorer 10 och 11 har [tagits bort](../ie-deprecation.md).

## 22 juni 2022

Nya tillägg har släppts:

* [Google datalagrets taggtillägg](../extensions/client/google-data-layer/overview.md): Gör att du kan använda ett Google-datalager i taggimplementeringen.
* [Google Ads Enhanced Conversions event forward extension](https://partners.adobe.com/exchangeprogram/experiencecloud/exchange.details.108630.html): Gör att du kan förbättra dina Google Ads-konverteringar i realtid.
* [Vidarebefordran av Mailchimp-händelse](../extensions/server/mailchimp/overview.md): Skickar händelser till Mailchimp Marketing API som kan utlösa e-postmeddelanden för marknadsföringskampanjer, resor eller transaktioner för Mailchimp.