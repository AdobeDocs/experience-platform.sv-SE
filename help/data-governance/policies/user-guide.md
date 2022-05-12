---
keywords: Experience Platform;hem;populära ämnen;datastyrning;användarhandbok för dataanvändningspolicy
solution: Experience Platform
title: Manage Data Usage Policies in the UI
topic-legacy: policies
description: Adobe Experience Platform Data Governance provides a user interface that allows you to create and manage data usage policies. Det här dokumentet innehåller en översikt över de åtgärder som du kan utföra på arbetsytan Profiler i användargränssnittet för Experience Platform.
exl-id: 29434dc1-02c2-4267-a1f1-9f73833e76a0
source-git-commit: 1c0685e7acb594829795674f859f76f229ecee61
workflow-type: tm+mt
source-wordcount: '1268'
ht-degree: 0%

---

# Hantera dataanvändningsprinciper i användargränssnittet

Adobe Experience Platform Data Governance provides a user interface that allows you to create and manage data usage policies. This document provides an overview of the actions that you can perform in the **Policies** workspace in the [!DNL Experience Platform] user interface.

>[!IMPORTANT]
>
>Alla dataanvändningsprinciper (inklusive huvudprinciper som tillhandahålls av Adobe) inaktiveras som standard. För att en enskild princip ska kunna användas för verkställighet måste du manuellt aktivera den principen. Se avsnittet om [aktivera principer](#enable) för steg om hur du gör detta i användargränssnittet.

## Förutsättningar

This guide requires a working understanding of the following [!DNL Experience Platform] concepts:

* [Datastyrning](../home.md)
* [Dataanvändningspolicyer](./overview.md)

## View existing policies {#view-policies}

I [!DNL Experience Platform] Gränssnitt, välj **[!UICONTROL Policies]** för att öppna **[!UICONTROL Policies]** arbetsyta. In the **[!UICONTROL Browse]** tab, you can see a list of available policies, including their associated labels, marketing actions, and status.

![](../images/policies/browse-policies.png)

Om du har åtkomst till profiler för samtycke (för närvarande i betaversion) väljer du **[!UICONTROL Consent policies]** växla för att visa dem i [!UICONTROL Browse] -fliken.

![](../images/policies/consent-policy-toggle.png)

Select a listed policy to view its description and type. Om du väljer en anpassad profil visas ytterligare kontroller för att redigera, ta bort eller [aktivera/inaktivera profilen](#enable).

![](../images/policies/policy-details.png)

## Skapa en anpassad profil {#create-policy}

Om du vill skapa en ny anpassad dataanvändningsprincip väljer du **[!UICONTROL Create policy]** i det övre högra hörnet av **[!UICONTROL Browse]** i **[!UICONTROL Policies]** arbetsyta.

![](../images/policies/create-policy-button.png)

Beroende på om du är en del av betatestningspolicyn för samtycke, händer något av följande:

* If you are not part of the beta, you are immediately brought to the workflow for [creating a data governance policy](#create-governance-policy).
* Om du är en del av betaversionen visas en dialogruta med ett extra alternativ för att [skapa en medgivandeprincip](#consent-policy).
   ![](../images/policies/choose-policy-type.png)

### Create a data governance policy {#create-governance-policy}

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

The **[!UICONTROL Browse]** tab reappears, which now lists the newly created policy in &quot;Draft&quot; status. Om du vill aktivera profilen går du till nästa avsnitt.

![](../images/policies/created-policy.png)

### Skapa en medgivandeprincip (beta) {#consent-policy}

>[!IMPORTANT]
>
>Samtyckesprofiler är för närvarande betaversioner och din organisation har kanske inte åtkomst till dem än.

Om du väljer att skapa en profil för samtycke visas en ny skärm där du kan konfigurera den nya principen.

![](../images/policies/consent-policy-dialog.png)

In order to make use of consent policies, you must have consent attributes present in your profile data. Se guiden [behandling av samtycke i Experience Platform](../../landing/governance-privacy-security/consent/adobe/overview.md) för detaljerade steg om hur du inkluderar de nödvändiga attributen i ditt unionsschema.

Samtyckesprinciper består av två logiska komponenter:

* **[!UICONTROL If]**: Villkoret som utlöser principkontrollen. Detta kan baseras på en viss marknadsföringsåtgärd som utförs, förekomsten av vissa dataanvändningsetiketter eller en kombination av de två.
* **[!UICONTROL Then]**: The consent attributes that must be present for a profile to be included in the action that triggered the policy.

#### Konfigurera villkor

Under **[!UICONTROL If]** väljer du de marknadsföringsåtgärder och/eller dataanvändningsetiketter som ska utlösa den här principen. Select **[!UICONTROL View all]** and **[!UICONTROL Select labels]** to view the full lists of available marketing actions and labels, respectively.

När du har lagt till minst ett villkor kan du välja **[!UICONTROL Add condition]** om du vill fortsätta lägga till ytterligare villkor efter behov, väljer du lämplig villkorstyp i listrutan.

![](../images/policies/add-condition.png)

Om du markerar mer än ett villkor kan du använda ikonen som visas mellan dem för att växla den villkorliga relationen mellan &quot;AND&quot; och &quot;OR&quot;.

![](../images/policies/and-or-selection.png)

#### Välj medgivandeattribut

Under **[!UICONTROL Then]** väljer du minst ett medgivandeattribut från unionsschemat. Det här är attributet som måste finnas för att profiler ska kunna inkluderas i åtgärden som styrs av den här principen. Du kan välja något av alternativen i listan eller välja **[!UICONTROL View all]** för att välja attributet direkt från unionsschemat.

När du väljer medgivandeattributet väljer du värdena för attributet som du vill att den här principen ska söka efter.

![](../images/policies/select-schema-field.png)

När du har valt minst ett medgivandeattribut, **[!UICONTROL Policy properties]** Panelen uppdateras för att visa det uppskattade antalet profiler som tillåts enligt den här principen, inklusive procentandelen av det totala profilarkivet. This estimation automatically updates as you adjust the policy configuration.

![](../images/policies/audience-preview.png)

Om du vill lägga till fler medgivandeattribut till profilen väljer du **[!UICONTROL Add result]**.

![](../images/policies/add-result.png)

You can continue adding and adjusting conditions and consent attributes to the policy as needed. När du är nöjd med konfigurationen anger du ett namn och en valfri beskrivning för profilen innan du väljer **[!UICONTROL Save]**.

![](../images/policies/name-and-save.png)

Medgivandeprincipen skapas nu och dess status anges till [!UICONTROL Disabled] som standard. To enable the policy right away, select the **[!UICONTROL Status]** toggle in the right rail.

![](../images/policies/enable-consent-policy.png)

#### Verify policy enforcement

När du har skapat och aktiverat en medgivandeprincip kan du förhandsgranska hur den påverkar de godkända målgrupperna när du aktiverar segment till mål. Se avsnittet om [utvärdering av godkännandepolicy](../enforcement/auto-enforcement.md#consent-policy-evaluation) för mer information.

## Aktivera eller inaktivera en profil {#enable}

Alla dataanvändningsprinciper (inklusive huvudprinciper som tillhandahålls av Adobe) inaktiveras som standard. För att en enskild princip ska kunna användas måste du manuellt aktivera den principen via API:t eller användargränssnittet.

Du kan aktivera eller inaktivera profiler på **[!UICONTROL Browse]** i **[!UICONTROL Policies]** arbetsyta. Välj en anpassad profil i listan för att visa informationen till höger. Under **[!UICONTROL Status]**, select the toggle button to enable or disable the policy.

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
>Endast anpassade marknadsföringsåtgärder som definieras av din organisation kan redigeras. Marketing actions defined by Adobe cannot be changed or deleted.

I **[!UICONTROL Policies]** arbetsyta väljer du **[!UICONTROL Marketing actions]** för att visa en lista över tillgängliga marknadsföringsåtgärder som definieras av Adobe och din egen organisation. Select a custom marketing action from the list, then used the provided fields in the right-hand section to edit the marketing action&#39;s details.

![](../images/policies/edit-marketing-action.png)

Om marknadsföringsåtgärden inte används av någon befintlig användarprofil kan du ta bort den genom att välja **[!UICONTROL Delete marketing action]**.

>[!NOTE]
>
>Om du försöker ta bort en marknadsföringsåtgärd som används av en befintlig princip visas ett felmeddelande som anger att borttagningsförsöket misslyckades.

![](../images/policies/delete-marketing-action.png)

## Nästa steg

Det här dokumentet innehåller en översikt över hur du hanterar dataanvändningsprinciper i [!DNL Experience Platform] Gränssnitt. For steps on how to manage policies using the [!DNL Policy Service API], see the [developer guide](../api/getting-started.md). Information om hur du tillämpar dataanvändningsprinciper finns i [genomgång av policytillämpning](../enforcement/overview.md).

The following video provides a demonstration of how to work with usage policies in the [!DNL Experience Platform] UI:

>[!VIDEO](https://video.tv.adobe.com/v/32977?quality=12&learn=on)
