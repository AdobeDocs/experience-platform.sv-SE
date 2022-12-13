---
keywords: Experience Platform;hem;populära ämnen;datastyrning;användarhandbok för dataanvändningspolicy
solution: Experience Platform
title: Hantera dataanvändningsprinciper i användargränssnittet
topic-legacy: policies
description: Adobe Experience Platform Data Governance har ett användargränssnitt där du kan skapa och hantera dataanvändningspolicyer. Det här dokumentet innehåller en översikt över de åtgärder som du kan utföra på arbetsytan Profiler i användargränssnittet för Experience Platform.
exl-id: 29434dc1-02c2-4267-a1f1-9f73833e76a0
source-git-commit: 38447348bc96b2f3f330ca363369eb423efea1c8
workflow-type: tm+mt
source-wordcount: '1347'
ht-degree: 0%

---

# Hantera dataanvändningsprinciper i användargränssnittet

Det här dokumentet innehåller information om hur du använder **[!UICONTROL Policies]** i Adobe Experience Platform användargränssnitt för att skapa och hantera dataanvändningsprinciper.

>[!NOTE]
>
>Information om hur du hanterar åtkomstkontrollprinciper i användargränssnittet finns i [användargränssnittshandbok för attributbaserad åtkomstkontroll](../../access-control/abac/ui/policies.md) i stället.

>[!IMPORTANT]
>
>Alla dataanvändningsprinciper (inklusive huvudprinciper som tillhandahålls av Adobe) inaktiveras som standard. För att en enskild princip ska kunna användas för verkställighet måste du manuellt aktivera den principen. Se avsnittet om [aktivera principer](#enable) för steg om hur du gör detta i användargränssnittet.

## Förutsättningar

Handboken kräver en fungerande förståelse av följande [!DNL Experience Platform] begrepp:

* [Datastyrning](../home.md)
* [Dataanvändningspolicyer](./overview.md)

## Visa befintliga profiler {#view-policies}

I [!DNL Experience Platform] Gränssnitt, välj **[!UICONTROL Policies]** för att öppna **[!UICONTROL Policies]** arbetsyta. I **[!UICONTROL Browse]** kan du se en lista över tillgängliga profiler, inklusive tillhörande etiketter, marknadsföringsåtgärder och status.

![](../images/policies/browse-policies.png)

Om du har åtkomst till profiler för samtycke väljer du **[!UICONTROL Consent policies]** växla för att visa dem i [!UICONTROL Browse] -fliken.

![](../images/policies/consent-policy-toggle.png)

Välj en listad profil för att visa dess beskrivning och typ. Om du väljer en anpassad profil visas ytterligare kontroller för att redigera, ta bort eller [aktivera/inaktivera profilen](#enable).

![](../images/policies/policy-details.png)

## Skapa en anpassad profil {#create-policy}

Om du vill skapa en ny anpassad dataanvändningsprincip väljer du **[!UICONTROL Create policy]** i det övre högra hörnet av **[!UICONTROL Browse]** i **[!UICONTROL Policies]** arbetsyta.

![](../images/policies/create-policy-button.png)

Beroende på om du är en del av betatestningspolicyn för samtycke, händer något av följande:

* Om du inte är en del av betaversionen kommer du omedelbart till arbetsflödet för [skapa en datastyrningspolicy](#create-governance-policy).
* Om du är en del av betaversionen visas en dialogruta med ett extra alternativ för att [skapa en medgivandeprincip](#consent-policy).
   ![](../images/policies/choose-policy-type.png)

### Skapa en datastyrningspolicy {#create-governance-policy}

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

### Skapa en medgivandeprincip {#consent-policy}

>[!IMPORTANT]
>
>Samtyckesprofiler är bara tillgängliga för organisationer som har köpt **Adobe Healthcare Shield** eller **Adobe Privacy &amp; Security Shield**.

Om du väljer att skapa en profil för samtycke visas en ny skärm där du kan konfigurera den nya principen.

![](../images/policies/consent-policy-dialog.png)

Om du vill kunna använda profiler för samtycke måste du ha attribut för samtycke i dina profildata. Se guiden [behandling av samtycke i Experience Platform](../../landing/governance-privacy-security/consent/adobe/overview.md) för detaljerade steg om hur du inkluderar de nödvändiga attributen i ditt unionsschema.

Samtyckesprinciper består av två logiska komponenter:

* **[!UICONTROL If]**: Villkoret som utlöser principkontrollen. Detta kan baseras på en viss marknadsföringsåtgärd som utförs, förekomsten av vissa dataanvändningsetiketter eller en kombination av de två.
* **[!UICONTROL Then]**: Medgivandeattributen som måste finnas för en profil som ska inkluderas i åtgärden som utlöste policyn.

#### Konfigurera villkor {#consent-conditions}

>[!CONTEXTUALHELP]
>id="platform_governance_policies_consentif"
>title="Om villkor"
>abstract="Börja med att definiera villkoren som utlöser principkontrollen. Villkoren kan omfatta vissa marknadsföringsåtgärder som vidtas, vissa datastyrningsetiketter finns eller en kombination av båda."

Under **[!UICONTROL If]** väljer du de marknadsföringsåtgärder och/eller dataanvändningsetiketter som ska utlösa den här principen. Välj **[!UICONTROL View all]** och **[!UICONTROL Select labels]** för att få en fullständig lista över tillgängliga marknadsföringsåtgärder och etiketter.

När du har lagt till minst ett villkor kan du välja **[!UICONTROL Add condition]** om du vill fortsätta lägga till ytterligare villkor efter behov, väljer du lämplig villkorstyp i listrutan.

![](../images/policies/add-condition.png)

Om du markerar mer än ett villkor kan du använda ikonen som visas mellan dem för att växla den villkorliga relationen mellan &quot;AND&quot; och &quot;OR&quot;.

![](../images/policies/and-or-selection.png)

#### Välj medgivandeattribut {#consent-attributes}

>[!CONTEXTUALHELP]
>id="platform_governance_policies_consentthen"
>title="Villkor"
>abstract="När ditt If-villkor har definierats kan du använda sektionen &#39;then&#39; för att välja minst ett medgivandeattribut från unionsschemat. Det här är attributet som måste finnas för att profiler ska kunna inkluderas i åtgärden som styrs av den här principen."

Under **[!UICONTROL Then]** väljer du minst ett medgivandeattribut från unionsschemat. Det här är attributet som måste finnas för att profiler ska kunna inkluderas i åtgärden som styrs av den här principen. Du kan välja något av alternativen i listan eller välja **[!UICONTROL View all]** för att välja attributet direkt från unionsschemat.

När du väljer medgivandeattributet väljer du värdena för attributet som du vill att den här principen ska söka efter.

![](../images/policies/select-schema-field.png)

När du har valt minst ett medgivandeattribut, **[!UICONTROL Policy properties]** Panelen uppdateras för att visa det uppskattade antalet profiler som tillåts enligt den här principen, inklusive procentandelen av det totala profilarkivet. Den här uppskattningen uppdateras automatiskt när du justerar principkonfigurationen.

![](../images/policies/audience-preview.png)

Om du vill lägga till fler medgivandeattribut till profilen väljer du **[!UICONTROL Add result]**.

![](../images/policies/add-result.png)

Du kan fortsätta lägga till och justera villkor och medgivandeattribut i profilen efter behov. När du är nöjd med konfigurationen anger du ett namn och en valfri beskrivning för profilen innan du väljer **[!UICONTROL Save]**.

![](../images/policies/name-and-save.png)

Medgivandeprincipen skapas nu och dess status anges till [!UICONTROL Disabled] som standard. Om du vill aktivera profilen direkt väljer du **[!UICONTROL Status]** till höger.

![](../images/policies/enable-consent-policy.png)

#### Verifiera policytillämpning

När du har skapat och aktiverat en medgivandeprincip kan du förhandsgranska hur den påverkar de godkända målgrupperna när du aktiverar segment till mål. Se avsnittet om [utvärdering av godkännandepolicy](../enforcement/auto-enforcement.md#consent-policy-evaluation) för mer information.

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
