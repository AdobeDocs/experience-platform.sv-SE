---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Användarhandbok för dataanvändningsprinciper
topic: policies
translation-type: tm+mt
source-git-commit: af7fa6048fa60392a98975fe6fc36e8302355a05
workflow-type: tm+mt
source-wordcount: '417'
ht-degree: 0%

---


# Användarhandbok för dataanvändningsprinciper

Med Adobe Experience Platform Data Governance får ni ett användargränssnitt där ni kan skapa och hantera dataanvändningspolicyer. Det här dokumentet innehåller en översikt över de åtgärder du kan utföra på arbetsytan _Profiler_ i användargränssnittet för Experience Platform.

## Förutsättningar

Den här guiden kräver en fungerande förståelse av följande Experience Platform-koncept:

- [Datastyrning](../home.md)
- [Dataanvändningspolicyer](./overview.md)

## Visa dataanvändningspolicyer

I Experience Platform-gränssnittet klickar du **[!UICONTROL Policies]** för att öppna *[!UICONTROL Policies]* arbetsytan. På fliken **[!UICONTROL Browse]** kan du se en lista över tillgängliga profiler, inklusive tillhörande etiketter, marknadsföringsåtgärder och status.

![](../images/policies/browse-policies.png)

Klicka på en listad profil för att visa dess beskrivning och typ. Om du väljer en anpassad profil visas ytterligare kontroller för att redigera, ta bort eller [aktivera/inaktivera profilen](#enable).

![](../images/policies/policy-details.png)

## Skapa en anpassad dataanvändningsprincip

Om du vill skapa en ny anpassad dataanvändningsprincip klickar du **[!UICONTROL Create policy]** i det övre högra hörnet på arbetsytan *Profiler* .

![](../images/policies/create-policy-button.png)

Arbetsflödet *[!UICONTROL Create policy]* visas. Börja med att ange ett namn och en beskrivning för den nya principen.

![](../images/policies/create-policy-description.png)

Välj sedan de dataanvändningsetiketter som profilen ska baseras på. När du väljer flera etiketter kan du välja om informationen ska innehålla alla etiketter eller bara en av dem för att profilen ska kunna användas. Klicka **[!UICONTROL Next]** när du är klar.

![](../images/policies/add-labels.png)

Steget *[!UICONTROL Select marketing actions]* visas. Välj lämpliga marknadsföringsåtgärder i listan och klicka sedan på **[!UICONTROL Next]** för att fortsätta.

>[!NOTE] När man väljer flera marknadsföringsåtgärder tolkas de som en &quot;OR&quot;-regel. Med andra ord gäller policyn om _någon_ av de valda marknadsföringsåtgärderna utförs.

![](../images/policies/add-marketing-actions.png)

Steget visas så att du kan granska informationen om den nya profilen innan du skapar den. *[!UICONTROL Review]* När du är nöjd klickar du på **[!UICONTROL Finish]** för att skapa profilen.

![](../images/policies/policy-review.png)

Fliken visas igen, där den nya principen visas med statusen Utkast. *[!UICONTROL Browse]* Om du vill aktivera profilen går du till nästa avsnitt.

![](../images/policies/created-policy.png)

## Aktivera eller inaktivera en dataanvändningsprincip {#enable}

Du kan aktivera eller inaktivera anpassade principer för dataanvändning på *[!UICONTROL Browse]* fliken på *[!UICONTROL Policies]* arbetsytan. Välj en anpassad profil i listan för att visa informationen till höger. Under *[!UICONTROL Status]* markerar du knappen för att aktivera eller inaktivera profilen.

![](../images/policies/enable-policy.png)

## Nästa steg

I det här dokumentet finns en översikt över hur du hanterar dataanvändningsprinciper i användargränssnittet för Experience Platform. Anvisningar om hur du hanterar principer med DULE Policy API finns i [utvecklarhandboken](../api/getting-started.md). Mer information om hur du tillämpar dataanvändningsprinciper finns i [policyefterlevnadsöversikten](../enforcement/overview.md).

I följande video visas hur du arbetar med användarprofiler i användargränssnittet för Experience Platform:

>[!VIDEO](https://video.tv.adobe.com/v/32977?quality=12&learn=on)