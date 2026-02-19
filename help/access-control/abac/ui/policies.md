---
keywords: Experience Platform;home;populära topics;access control;attribute-based access control;ABAC
title: Hantera åtkomstkontrollprinciper
description: Hantera åtkomstkontrollprinciper via gränssnittet Behörigheter i Adobe Experience Cloud.
exl-id: 66820711-2db0-4621-908d-01187771de14
source-git-commit: b0094920720c54990953f79de32ab95c2a5c7e1c
workflow-type: tm+mt
source-wordcount: '625'
ht-degree: 0%

---

# Hantera åtkomstkontrollprinciper

Åtkomstkontrollprinciper är satser som sammanför attribut för att fastställa tillåtna och otillåtna åtgärder. Adobe tillhandahåller en standardprincip som kan aktiveras omedelbart eller när din organisation är redo att börja styra åtkomsten till specifika objekt baserat på [etiketter](./labels.md){target="_blank"}. Standardprincipen, **[!UICONTROL Default-Label-Based-Access-Control-Policy]**, utnyttjar etiketter som används på resurser för att neka åtkomst, såvida inte användarna har en roll med en matchande etikett.

>[!IMPORTANT]
>
>Åtkomstkontrollprinciper får inte blandas ihop med dataanvändningsprinciper, som styr hur data används i Adobe Experience Platform. Mer information finns i guiden om att skapa [dataanvändningsprinciper](../../../data-governance/policies/create.md){target="_blank"}.

## Konfigurera princip för en sandlåda {#configure-policy}

>[!NOTE]
>
>Principen **[!UICONTROL Default-Label-Based-Access-Control-Policy]** är för närvarande den enda som är tillgänglig för konfiguration.

Om du vill börja konfigurera en princip går du till **[!UICONTROL Permissions]** i [Adobe Experience Cloud](https://experience.adobe.com/){target="_blank"}. Välj **[!UICONTROL Policies]** i den vänstra panelen. Välj **[!UICONTROL Default-Label-Based-Access-Control-Policy]** i listan.

![Arbetsytan Principer visar en lista över befintliga profiler.](../../images/ui/policies/policies-home.png){zoomable="yes"}

Arbetsytan för information om profilen visas. Markera **[!UICONTROL Sandboxes]**. En lista över sandlådor som är associerade med profilen visas.

![Principens sandlådearbetsyta med en lista över associerade sandlådor.](../../images/ui/policies/policy-sandbox.png){zoomable="yes"}

### Lägg till princip i alla sandlådor {#add-policy-to-all}

>[!IMPORTANT]
>
>Som standard är **[!UICONTROL Auto-include]** aktiverad, vilket innebär att alla aktuella och framtida sandlådor läggs till automatiskt i principen.

Växla av funktionen **[!UICONTROL Auto-include]** om du inte vill att framtida sandlådor automatiskt ska läggas till i principen. Om du stänger av funktionen **tas inga sandlådor bort från principen.**

![Principens sandlådeflik med alternativet för att ta med automatiskt markerat och i läget &quot;av&quot;.](../../images/ui/policies/policy-auto-include.png){zoomable="yes"}

Om **[!UICONTROL Auto-include]** inte är aktiv i en princip kan du aktivera den igen med hjälp av växlingsknappen. Dialogrutan **[!UICONTROL Enable Auto-include]** visas och du uppmanas att bekräfta ditt val. Välj **[!UICONTROL Enable]** för att slutföra konfigurationsinställningen.

>[!NOTE]
>
>Alla sandlådor som du har tagit bort från principen när **[!UICONTROL Auto-include]** stängdes av läggs till igen.

![Dialogrutan Aktivera automatisk inkludering med alternativet Aktivera markerat.](../../images/ui/policies/policy-enable-auto-include.png){zoomable="yes"}

### Välj sandlådor manuellt för en profil {#manually-select-sandboxes}

Om du vill lägga till eller ta bort sandlådor manuellt i en princip måste **[!UICONTROL Auto-include]**-växlingen **vara inaktiverad**.

#### Lägga till sandlådor

Om du vill lägga till sandlådor i en profil väljer du **[!UICONTROL Add Sandboxes]**.

![Principens arbetsyta med alternativet Lägg till sandlådor markerat.](../../images/ui/policies/policy-add-sandboxes.png){zoomable="yes"}

Dialogrutan **[!UICONTROL Add Sandboxes]** visas. Markera de sandlådor som du vill lägga till i profilen och välj sedan **[!UICONTROL Save]**.

![Dialogrutan Lägg till sandlådor med en markerad sandlåda och alternativet Spara markerat.](../../images/ui/policies/policy-add-sandboxes-select.png){zoomable="yes"}

>[!NOTE]
>
>Om alla tillgängliga sandlådor redan har lagts till i profilen visas meddelandet&quot;Du har inget i biblioteket&quot; i dialogrutan.

#### Ta bort sandlådor

Om du vill ta bort sandlådor från en princip söker du efter den sandlåda du vill ta bort från listan och väljer sedan ikonen **X** .

![Principens sandlådelista med ett &quot;x&quot; markerat för att ta bort en sandlåda.](../../images/ui/policies/policy-remove-sandbox.png){zoomable="yes"}

En bekräftelsedialogruta visas. Välj **[!UICONTROL Confirm]** om du vill ta bort sandlådan från principen.

![En bekräftelsedialogruta för en sandlåda med alternativet Bekräfta markerat.](../../images/ui/policies/policy-remove-sandbox-confirmation.png){zoomable="yes"}

## Aktivera en profil {#activate-policy}

>[!CONTEXTUALHELP]
>id="platform_permissions_policies_about"
>title="Vad är policyer?"
>abstract="Profiler är satser som sammanför attribut för att fastställa tillåtna och otillåtna åtgärder. Alla organisationer har en standardprofil som du måste aktivera för att kunna styra åtkomsten till specifika objekt baserat på etiketter. Etiketter som används på resurser nekar åtkomst såvida inte användare tilldelas till en roll med en matchande etikett. Profiler kan inte redigeras eller tas bort, men de kan aktiveras eller inaktiveras."
>additional-url="https://experienceleague.adobe.com/sv/docs/experience-platform/access-control/abac/permissions-ui/labels" text="Hantera etiketter"

Om du vill aktivera en befintlig princip väljer du den på fliken **[!UICONTROL Policies]** i **[!UICONTROL Permissions]**. Principens aktiveringsstatus visas under avsnittet **[!UICONTROL Status]**.

![Arbetsytan för profiler med en profils status markerad.](../../images/ui/policies/policy-status.png){zoomable="yes"}

Arbetsytan Detaljer för profilen visas. Välj **[!UICONTROL Activate]**.

![Principens arbetsyta för detaljer med alternativet Aktivera markerat.](../../images/ui/policies/policy-activate.png){zoomable="yes"}

Dialogrutan **[!UICONTROL Activate Policy]** visas. Välj **[!UICONTROL Confirm]** för att slutföra aktiveringen av principen.

![Dialogrutan Aktivera princip med alternativet Bekräfta markerat.](../../images/ui/policies/policy-activate-confirm.png){zoomable="yes"}

## Nästa steg

När en profil är aktiverad kan du fortsätta till nästa steg för att [hantera behörigheter för en roll](permissions.md).

<!--Policies are applied at the sandbox level to control which sandboxes enforce label-based access control. By default, the **[!UICONTROL Auto-include]** feature is turned on, which means all current and future sandboxes are automatically added to the policy. When **[!UICONTROL Auto-include]** is turned off, only the sandboxes you manually add will be subject to the policy's access control rules.

To begin configuring a policy's sandboxes, navigate to **[!UICONTROL Permissions]** in [Adobe Experience Cloud](https://experience.adobe.com/){target="_blank"}. Select **[!UICONTROL Policies]** from the left panel, then select the **[!UICONTROL Default-Label-Based-Access-Control-Policy]** from the list.

The policy's details workspace appears. Select the **[!UICONTROL Sandboxes]** tab to view the list of sandboxes associated with the policy and access the sandbox configuration options.

### Manage Auto-include {#manage-auto-include}

To control which sandboxes are included in a policy, you can toggle the **[!UICONTROL Auto-include]** feature on or off. When you toggle off **[!UICONTROL Auto-include]**, future sandboxes will not be automatically added to the policy. However, toggling off the feature **will not** remove any sandboxes that are already included in the policy.

To re-enable **[!UICONTROL Auto-include]**, use the toggle to turn it back on. The **[!UICONTROL Enable Auto-include]** dialog appears prompting you to confirm your selection. Select **[!UICONTROL Enable]** to complete the configuration setting.

>[!NOTE]
>
>When you re-enable **[!UICONTROL Auto-include]**, any sandboxes you previously removed from the policy will be re-added.

### Manually manage sandboxes {#manually-manage-sandboxes}

When **[!UICONTROL Auto-include]**is turned off, you can manually add or remove specific sandboxes from the policy. This gives you precise control over which sandboxes enforce the policy's access control rules.

>[!NOTE]
>
>To manually add or remove sandboxes, the **[!UICONTROL Auto-include]** toggle **must** be off.

**To add sandboxes:**

Select **[!UICONTROL Add Sandboxes]** from the policy's sandbox workspace.

The **[!UICONTROL Add Sandboxes]** dialog appears, displaying your library of available sandboxes. Select the sandbox(es) you wish to add to the policy and then select **[!UICONTROL Save]**.

>[!NOTE]
>
>If all available sandboxes are already included in the policy, you will see a "You have nothing in your library" message within the dialog.

**To remove sandboxes:**

Find the sandbox you wish to remove from the list and select the **X** icon next to its name.

A confirmation dialog will appear. Select **[!UICONTROL Confirm]** to finish removing the sandbox from the policy.

-->