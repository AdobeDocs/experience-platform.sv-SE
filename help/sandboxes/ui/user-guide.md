---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Handbok för sandlådeanvändare
topic: user guide
translation-type: tm+mt
source-git-commit: 397f08efa276f7885e099a0a8d9dc6d23fe0e8cc
workflow-type: tm+mt
source-wordcount: '505'
ht-degree: 0%

---


# Handbok för sandlådeanvändare

Det här dokumentet innehåller steg om hur du utför olika åtgärder relaterade till sandlådor i Adobe Experience Platform användargränssnitt.

## Visa sandlådor

I användargränssnittet för Experience Platform klickar du **[!UICONTROL Sandboxes]** i den vänstra navigeringen för att öppna **[!UICONTROL Sandboxes]** instrumentpanelen. På kontrollpanelen visas alla tillgängliga sandlådor för din organisation, inklusive sandlådetyp (produktion eller utveckling) och tillstånd (aktiv, skapa, borttagen eller misslyckades).

![](../images/ui/sandboxes-tab.png)

## Växla mellan sandlådor

Kontrollen för **sandlådeväxlaren** längst upp till vänster på skärmen visar den aktiva sandlådan.

![](../images/ui/sandbox-selector.png)

Om du vill växla mellan sandlådor klickar du på sandlådeväxlaren och väljer önskad sandlåda i listrutan.

![](../images/ui/switch-sandbox.png)

När en sandlåda har valts uppdateras skärmen med den valda sandlådan i sandlådeväxlaren.

![](../images/ui/sandbox-switched.png)

## Skapa en ny sandlåda

Använd följande video för en snabb översikt över hur du använder sandlådor i Experience Platform.

>[!VIDEO](https://video.tv.adobe.com/v/29838/?quality=12&learn=on)

Om du vill skapa en ny sandlåda i användargränssnittet klickar du **[!UICONTROL Sandboxes]** i den vänstra navigeringen och sedan på **[!UICONTROL Create Sandbox]**.

![](../images/ui/create-sandbox-button.png)

Dialogrutan visas och du uppmanas att ange en visningsrubrik och ett namn för sandlådan. **[!UICONTROL Create Sandbox]** Visningsrubriken **** är avsedd att vara läsbar för människor och bör vara tillräckligt beskrivande för att vara lätt att identifiera. Sandlådan **[!UICONTROL Name]** är en helgemen identifierare som ska användas i API-anrop och ska därför vara unik och koncis.

Klicka på **[!UICONTROL Create]** när du är klar.

![](../images/ui/create-sandbox-dialog.png)

>[!NOTE]
>
>Eftersom du endast är begränsad till att skapa icke-produktionssandlådtyper är alternativet låst vid &quot;Ej produktion&quot; och kan inte ändras. **[!UICONTROL type]**

När du är klar med att skapa sandlådan uppdaterar du sidan och den nya sandlådan visas på **[!UICONTROL Sandboxes]** instrumentpanelen med statusen&quot;[!UICONTROL Creating]&quot;. Nya sandlådor tar ca 15 minuter att etablera av systemet, varefter deras status ändras till&quot;[!UICONTROL Active]&quot;.

![](../images/ui/sandbox-created.png)

## Återställ en sandlåda

>[!NOTE]
>
>Den här funktionen är bara tillgänglig för icke-produktionssandlådor. Det går inte att återställa produktionssandlådor.

Om du återställer en icke-produktionssandlåda tas alla resurser som är associerade med den sandlådan (scheman, datauppsättningar o.s.v.) bort, samtidigt som sandlådans namn och associerade behörigheter behålls. Den här&quot;rena&quot; sandlådan är fortfarande tillgänglig under samma namn för användare som har åtkomst till den.

Om du vill återställa en sandlåda i användargränssnittet klickar du **[!UICONTROL Sandboxes]** i den vänstra navigeringen och sedan på den sandlåda som du vill återställa. Klicka på i dialogrutan som visas till höger på skärmen **[!UICONTROL Reset Sandbox]**.

![](../images/ui/reset-sandbox-button.png)

En dialogruta visas där du uppmanas att bekräfta ditt val. Klicka **[!UICONTROL Reset]** för att fortsätta.

<img src="../images/ui/reset-are-you-sure.png" width="350"><br>

Ett bekräftelsemeddelande visas och sandlådans läge ändras till &quot;[!UICONTROL Resetting]&quot;. När det har etablerats av systemet uppdateras dess tillstånd till &quot;[!UICONTROL Active]&quot; eller &quot;[!UICONTROL Failed]&quot;.

![](../images/ui/sandbox-resetting.png)

## Ta bort en sandlåda

>[!NOTE]
>
>Den här funktionen är bara tillgänglig för icke-produktionssandlådor. Det går inte att ta bort produktionssandlådor.

Om du tar bort en icke-produktionssandlåda permanent tas alla resurser som är associerade med den sandlådan bort, inklusive behörigheter.

Om du vill ta bort en sandlåda i användargränssnittet klickar du **[!UICONTROL Sandboxes]** i den vänstra navigeringen och sedan på den sandlåda som du vill ta bort. Klicka på i dialogrutan som visas till höger på skärmen **[!UICONTROL Delete Sandbox]**.

![](../images/ui/delete-sandbox-button.png)

En dialogruta visas där du uppmanas att bekräfta ditt val. Klicka **[!UICONTROL Delete]** för att fortsätta.

<img src="../images/ui/delete-are-you-sure.png" width="350"><br>

Ett bekräftelsemeddelande visas och sandlådan tas bort från **[!UICONTROL Sandboxes]** arbetsytan.

## Nästa steg

Det här dokumentet visar hur du hanterar sandlådor i användargränssnittet för Experience Platform. Mer information om hur du hanterar sandlådor med hjälp av API:t för sandlådan finns i [utvecklarhandboken](../api/getting-started.md)för sandlådan.