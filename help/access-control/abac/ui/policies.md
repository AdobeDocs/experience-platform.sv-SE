---
keywords: Experience Platform;home;populära topics;access control;attribute-based access control;ABAC
title: Hantera åtkomstkontrollprinciper
description: Hantera åtkomstkontrollprinciper via gränssnittet Behörigheter i Adobe Experience Cloud.
exl-id: 66820711-2db0-4621-908d-01187771de14
source-git-commit: 2a26c8786adc412dc643c8a0c94b966e439e034b
workflow-type: tm+mt
source-wordcount: '725'
ht-degree: 0%

---

# Hantera åtkomstkontrollprinciper

Åtkomstkontrollprinciper är satser som sammanför attribut för att fastställa tillåtna och otillåtna åtgärder. Adobe tillhandahåller en standardprincip som kan aktiveras omedelbart eller när din organisation är redo att börja styra åtkomsten till specifika objekt baserat på [etiketter](./labels.md){target="_blank"}. Standardprincipen, **[!UICONTROL Default-Label-Based-Access-Control-Policy]**, utnyttjar etiketter som används på resurser för att neka åtkomst, såvida inte användarna har en roll med en matchande etikett.

>[!IMPORTANT]
>
>Åtkomstkontrollprinciper får inte blandas ihop med dataanvändningsprinciper, som styr hur data används i Adobe Experience Platform. Mer information finns i guiden om att skapa [dataanvändningsprinciper](../../../data-governance/policies/create.md){target="_blank"}.

## Konfigurera sandlådor för en princip {#configure-policy}

Principer tillämpas på sandlådenivå för att styra vilka sandlådor som tillämpar etikettbaserad åtkomstkontroll. Som standard är funktionen **[!UICONTROL Auto-include]** aktiverad, vilket innebär att alla aktuella och framtida sandlådor läggs till automatiskt i principen. När **[!UICONTROL Auto-include]** är inaktiverat omfattas endast de sandlådor som du lägger till manuellt av principens åtkomstkontrollsregler.

>[!NOTE]
>
>Principen **[!UICONTROL Default-Label-Based-Access-Control-Policy]** är för närvarande den enda som är tillgänglig för konfiguration.

Navigera till **[!UICONTROL Permissions]** i [Adobe Experience Cloud](https://experience.adobe.com/){target="_blank"} om du vill börja konfigurera en princips sandlådor. Välj **[!UICONTROL Policies]** i den vänstra panelen och välj sedan **[!UICONTROL Default-Label-Based-Access-Control-Policy]** i listan.

![Arbetsytan Principer visar en lista över befintliga profiler.](../../images/ui/policies/policies-home.png){zoomable="yes"}

Arbetsytan för information för profilen visas. Välj fliken **[!UICONTROL Sandboxes]** om du vill visa listan över sandlådor som är associerade med principen och få åtkomst till konfigurationsalternativen för sandlådan.

![Principens sandlådearbetsyta med en lista över associerade sandlådor.](../../images/ui/policies/policy-sandbox.png){zoomable="yes"}

### Hantera automatisk inkludering {#manage-auto-include}

>[!IMPORTANT]
>
>Som standard är **[!UICONTROL Auto-include]** aktiverad, vilket innebär att alla aktuella och framtida sandlådor läggs till automatiskt i principen.

Om du vill kontrollera vilka sandlådor som ingår i en profil kan du aktivera eller inaktivera funktionen **[!UICONTROL Auto-include]**. När du inaktiverar **[!UICONTROL Auto-include]** läggs framtida sandlådor inte automatiskt till i principen. Om du stänger av funktionen **tas inte** bort sandlådor som redan finns i principen.

![Principens sandlådeflik med alternativet för att ta med automatiskt markerat och i läget &quot;av&quot;.](../../images/ui/policies/policy-auto-include.png){zoomable="yes"}

Om du vill aktivera **[!UICONTROL Auto-include]** igen använder du växlingsknappen för att aktivera den igen. Dialogrutan **[!UICONTROL Enable Auto-include]** visas och du uppmanas att bekräfta ditt val. Välj **[!UICONTROL Enable]** för att slutföra konfigurationsinställningen.

>[!NOTE]
>
>När du återaktiverar **[!UICONTROL Auto-include]** läggs alla sandlådor som du tidigare har tagit bort från principen till igen.

![Dialogrutan Aktivera automatisk inkludering med alternativet Aktivera markerat.](../../images/ui/policies/policy-enable-auto-include.png){zoomable="yes"}

### Hantera sandlådor manuellt {#manually-manage-sandboxes}

När **[!UICONTROL Auto-include]**&#x200B;är inaktiverat kan du lägga till eller ta bort specifika sandlådor manuellt från profilen. Detta ger dig exakt kontroll över vilka sandlådor som tillämpar principens åtkomstkontrollsregler.

>[!NOTE]
>
>Om du vill lägga till eller ta bort sandlådor manuellt måste **[!UICONTROL Auto-include]**-växlingen **vara inaktiverad**.

**Så här lägger du till sandlådor:**

Välj **[!UICONTROL Add Sandboxes]** från principens sandlådearbetsyta.

![Principens arbetsyta med alternativet Lägg till sandlådor markerat.](../../images/ui/policies/policy-add-sandboxes.png){zoomable="yes"}

Dialogrutan **[!UICONTROL Add Sandboxes]** visas och ditt bibliotek med tillgängliga sandlådor visas. Markera de sandlådor som du vill lägga till i profilen och välj sedan **[!UICONTROL Save]**.

![Dialogrutan Lägg till sandlådor med en markerad sandlåda och alternativet Spara markerat.](../../images/ui/policies/policy-add-sandboxes-select.png){zoomable="yes"}

>[!NOTE]
>
>Om alla tillgängliga sandlådor redan ingår i profilen visas meddelandet&quot;Du har inget i biblioteket&quot; i dialogrutan.

**Så här tar du bort sandlådor:**

Hitta den sandlåda som du vill ta bort från listan och välj ikonen **X** bredvid namnet.

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
