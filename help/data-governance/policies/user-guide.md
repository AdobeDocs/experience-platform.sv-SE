---
keywords: Experience Platform;hem;populära ämnen;datastyrning;användarhandbok för dataanvändningspolicy
solution: Experience Platform
title: Hantera dataanvändningsprinciper i användargränssnittet
topic-legacy: policies
description: Adobe Experience Platform Data Governance har ett användargränssnitt där du kan skapa och hantera dataanvändningspolicyer. Det här dokumentet innehåller en översikt över de åtgärder du kan utföra på arbetsytan Profiler i användargränssnittet i Experience Platform.
exl-id: 29434dc1-02c2-4267-a1f1-9f73833e76a0
source-git-commit: 03e7863f38b882a2fbf6ba0de1755e1924e8e228
workflow-type: tm+mt
source-wordcount: '735'
ht-degree: 0%

---

# Hantera dataanvändningsprinciper i användargränssnittet

Adobe Experience Platform Data Governance har ett användargränssnitt där du kan skapa och hantera dataanvändningspolicyer. Det här dokumentet innehåller en översikt över de åtgärder du kan utföra i **Profiler** arbetsytan i [!DNL Experience Platform] användargränssnitt.

>[!IMPORTANT]
>
>Alla dataanvändningsprinciper (inklusive huvudprinciper som tillhandahålls av Adobe) inaktiveras som standard. För att en enskild princip ska kunna användas för verkställighet måste du manuellt aktivera den principen. Se avsnittet om [aktivera principer](#enable) för steg om hur du gör detta i användargränssnittet.

## Förutsättningar

Handboken kräver en fungerande förståelse av följande [!DNL Experience Platform] begrepp:

- [Datastyrning](../home.md)
- [Dataanvändningspolicyer](./overview.md)

## Visa befintliga profiler {#view-policies}

I [!DNL Experience Platform] Gränssnitt, välj **[!UICONTROL Policies]** för att öppna **[!UICONTROL Policies]** arbetsyta. I **[!UICONTROL Browse]** kan du se en lista över tillgängliga profiler, inklusive tillhörande etiketter, marknadsföringsåtgärder och status.

![](../images/policies/browse-policies.png)

Välj en listad profil för att visa dess beskrivning och typ. Om du väljer en anpassad profil visas ytterligare kontroller för att redigera, ta bort eller [aktivera/inaktivera profilen](#enable).

![](../images/policies/policy-details.png)

## Skapa en anpassad profil {#create-policy}

Om du vill skapa en ny anpassad dataanvändningsprincip väljer du **[!UICONTROL Create policy]** i det övre högra hörnet av **[!UICONTROL Browse]** i **[!UICONTROL Policies]** arbetsyta.

![](../images/policies/create-policy-button.png)

The **[!UICONTROL Create policy]** arbetsflödet visas. Börja med att ange ett namn och en beskrivning för den nya principen.

![](../images/policies/create-policy-description.png)

Välj sedan de dataanvändningsetiketter som profilen ska baseras på. När du väljer flera etiketter kan du välja om informationen ska innehålla alla etiketter eller bara en av dem för att profilen ska kunna användas. Välj **[!UICONTROL Next]** när du är klar.

![](../images/policies/add-labels.png)

The **[!UICONTROL Select marketing actions]** visas. Välj lämpliga marknadsföringsåtgärder i listan och välj sedan **[!UICONTROL Next]** för att fortsätta.

>[!NOTE]
>
>När man väljer flera marknadsföringsåtgärder tolkas de som en &quot;OR&quot;-regel. Med andra ord gäller regeln om **alla** av de valda marknadsföringsåtgärderna genomförs.

![](../images/policies/add-marketing-actions.png)

The **[!UICONTROL Review]** visas så att du kan granska informationen om den nya profilen innan du skapar den. När du är nöjd väljer du **[!UICONTROL Finish]** för att skapa profilen.

![](../images/policies/policy-review.png)

The **[!UICONTROL Browse]** -fliken visas igen, där den nya principen nu visas med statusen Utkast. Om du vill aktivera profilen går du till nästa avsnitt.

![](../images/policies/created-policy.png)

## Aktivera eller inaktivera en profil {#enable}

Alla dataanvändningsprinciper (inklusive huvudprinciper som tillhandahålls av Adobe) inaktiveras som standard. För att en enskild princip ska kunna användas måste du manuellt aktivera den principen via API:t eller användargränssnittet.

Du kan aktivera eller inaktivera profiler på **[!UICONTROL Browse]** i **[!UICONTROL Policies]** arbetsyta. Välj en anpassad profil i listan för att visa informationen till höger. Under **[!UICONTROL Status]** markerar du knappen för att aktivera eller inaktivera profilen.

![](../images/policies/enable-policy.png)

## Visa marknadsföringsaktiviteter {#view-marketing-actions}

I **[!UICONTROL Policies]** arbetsyta väljer du **[!UICONTROL Marketing actions]** för att visa en lista över tillgängliga marknadsföringsåtgärder som definieras av Adobe och din egen organisation.

![](../images/policies/marketing-actions.png)

## Skapa en marknadsföringsåtgärd {#create-marketing-action}

Om du vill skapa en ny anpassad marknadsföringsåtgärd väljer du **[!UICONTROL Create marketing action]** i det övre högra hörnet av **[!UICONTROL Marketing actions]** i **[!UICONTROL Policies]** arbetsyta.

![](../images/policies/create-marketing-action.png)

The **[!UICONTROL Create marketing action]** visas. Ange ett namn och en beskrivning för marknadsföringsåtgärden och välj sedan **[!UICONTROL Create]**.

![](../images/policies/create-marketing-action-details.png)

Den nyligen skapade åtgärden visas i dialogrutan **[!UICONTROL Marketing actions]** -fliken. Nu kan du använda marknadsföringsåtgärden när [skapa nya dataanvändningsprinciper](#create-policy).

![](../images/policies/created-marketing-action.png)

## Redigera eller ta bort en marknadsföringsåtgärd {#edit-delete-marketing-action}

>[!NOTE]
>
>Endast anpassade marknadsföringsåtgärder som definieras av din organisation kan redigeras. Marknadsföringsåtgärder som definieras av Adobe kan inte ändras eller tas bort.

I **[!UICONTROL Policies]** arbetsyta väljer du **[!UICONTROL Marketing actions]** för att visa en lista över tillgängliga marknadsföringsåtgärder som definieras av Adobe och din egen organisation. Välj en anpassad marknadsföringsåtgärd i listan och använd sedan fälten i den högra delen för att redigera information om marknadsföringsåtgärden.

![](../images/policies/edit-marketing-action.png)

Om marknadsföringsåtgärden inte används av någon befintlig användarprofil kan du ta bort den genom att välja **[!UICONTROL Delete marketing action]**.

>[!NOTE]
>
>Om du försöker ta bort en marknadsföringsåtgärd som används av en befintlig princip visas ett felmeddelande som anger att borttagningsförsöket misslyckades.

![](../images/policies/delete-marketing-action.png)

## Nästa steg

Det här dokumentet innehåller en översikt över hur du hanterar dataanvändningsprinciper i [!DNL Experience Platform] Gränssnitt. För steg om hur du hanterar profiler med [!DNL Policy Service API], se [utvecklarhandbok](../api/getting-started.md). Information om hur du tillämpar dataanvändningsprinciper finns i [genomgång av policytillämpning](../enforcement/overview.md).

I följande video visas hur du arbetar med användarprofiler i [!DNL Experience Platform] Gränssnitt:

>[!VIDEO](https://video.tv.adobe.com/v/32977?quality=12&learn=on)
