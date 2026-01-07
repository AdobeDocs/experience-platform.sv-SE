---
keywords: Experience Platform;home;populära topics;access control;attribute-based access control;ABAC
title: Attributbaserad åtkomstkontroll Hantera sandlådor
description: Hantera sandlådor via gränssnittet Behörigheter i Adobe Experience Cloud.
exl-id: c21eb319-fc0d-442a-b778-bbfa2d6bb22d
source-git-commit: 8c9503c9923372ef919d485d4ec0e3ebda5a2413
workflow-type: tm+mt
source-wordcount: '304'
ht-degree: 0%

---

# Hantera sandlådor {#mange-sandboxes}

>[!CONTEXTUALHELP]
>id="platform_permissions_sandboxes_about"
>title="Vad är sandlådor?"
>abstract="Sandlådor är virtuella partitioner i en enda instans av Experience Platform. Allt innehåll och alla åtgärder som vidtas i en sandlåda begränsas till den sandlådan och påverkar inte andra sandlådor. Åtkomst till sandlådor hanteras via roller."
>additional-url="https://experienceleague.adobe.com/sv/docs/experience-platform/sandbox/home" text="Översikt över sandlådor"

Sandlådor är virtuella partitioner i en enda instans av Adobe Experience Platform som smidigt integrerar utvecklingsprocessen i era program för digitala upplevelser. Allt innehåll och alla åtgärder som vidtas i en sandlåda begränsas till enbart den sandlådan och påverkar inte några andra sandlådor. Mer information om sandlådor finns i [Översikt över sandlådor](../../../sandboxes/home.md).

## Utforska sandlådor {#explore-sandboxes}

Om du vill visa information om en sandlåda och associerade roller går du till **[!UICONTROL Permissions]** i [Adobe Experience Cloud](https://experience.adobe.com/){target="_blank"}. Välj **[!UICONTROL Sandboxes]** i avsnittet **[!UICONTROL Resources]** i den vänstra panelen.

En lista över organisationens sandlådor visas. Välj den sandlåda som du vill visa i listan. Du kan också söka efter en sandlåda genom att ange sandlådans namn i sökfältet, eller filtrera sandlådor efter typ, genom att markera filterikonen (![Filterikon](../../../images/icons/filter.png)) och använda listrutan **[!UICONTROL Sandbox Type]** .

![Sandlådans arbetsytor i behörigheter.](../../images/ui/sandboxes/sandboxes-overview.png){zoomable="yes"}

>[!NOTE]
>
>Sandlådearbetsytan i Behörigheter tillåter inte några åtgärder för sandlådehantering. Om du vill hantera sandlådor väljer du alternativet **[!UICONTROL Open sandbox manager]** längst upp till höger på arbetsytan.

Fliken **[!UICONTROL Details]** innehåller en översikt över sandlådan. I översikten visas **[!UICONTROL Title]**, **[!UICONTROL Sandbox Name]**, **[!UICONTROL Type]**, **[!UICONTROL Region]**, **[!UICONTROL Modified]** date, **[!UICONTROL Modified by]** och **[!UICONTROL Status]** för sandlådan.

![Arbetsytan Detaljer i sandlådan.](../../images/ui/sandboxes/sandbox-details.png){zoomable="yes"}

Välj fliken **[!UICONTROL Roles]** för att visa de roller som sandlådan är tilldelad till. Om du väljer en roll kommer du till rollens arbetsyta.

<!-- To manage the role's sandboxes, follow the [](./roles.md) guide. -->

![Arbetsytan Roller i sandlådan.](../../images/ui/sandboxes/sandbox-roles.png){zoomable="yes"}


## Nästa steg

Nu vet du hur du visar information och roller för en sandlåda. Mer information om attributbaserad åtkomstkontroll finns i [attributbaserad åtkomstkontroll](../overview.md).
