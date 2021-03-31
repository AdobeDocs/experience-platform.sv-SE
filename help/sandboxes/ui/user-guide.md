---
keywords: Experience Platform;hem;populära ämnen;användarhandbok för sandlådan;sandlådeguide
solution: Experience Platform
title: Användargränssnittshandbok för sandlådan
topic: användarhandbok
description: Det här dokumentet innehåller steg om hur du utför olika åtgärder relaterade till sandlådor i Adobe Experience Platform användargränssnitt.
translation-type: tm+mt
source-git-commit: ee2fb54ba59f22a1ace56a6afd78277baba5271e
workflow-type: tm+mt
source-wordcount: '602'
ht-degree: 0%

---


# Användargränssnittshandbok för sandlådan

Det här dokumentet innehåller steg om hur du utför olika åtgärder relaterade till sandlådor i Adobe Experience Platform användargränssnitt.

## Visa sandlådor

I användargränssnittet för Experience Platform väljer du **[!UICONTROL Sandboxes]** i den vänstra navigeringen för att öppna kontrollpanelen **[!UICONTROL Sandboxes]**. På kontrollpanelen visas alla tillgängliga sandlådor för din organisation, inklusive sandlådetyp (produktion eller utveckling) och tillstånd (aktiv, skapa, borttagen eller misslyckades).

![](../images/ui/view-sandboxes.png)

## Växla mellan sandlådor

Kontrollen **sandlådeväxlaren** längst upp till vänster på skärmen visar den aktiva sandlådan.

![](../images/ui/sandbox-switcher.png)

Om du vill växla mellan sandlådor markerar du sandlådeväxlaren och väljer önskad sandlåda i listrutan.

![](../images/ui/switcher-menu.png)

När en sandlåda har valts uppdateras skärmen med den valda sandlådan i sandlådeväxlaren.

![](../images/ui/switched.png)

## Söka efter en sandlåda

Du kan navigera i listan med tillgängliga sandlådor med hjälp av sökfunktionen på sandlådeväxlarmenyn. Ange namnet på den sandlåda som du vill använda för att filtrera genom alla sandlådor som är tillgängliga för din organisation.

![](../images/ui/sandbox-search.png)

## Skapa en ny sandlåda

>[!NOTE]
>
>Funktionen Flera produktionssandlådor är i betaversion.

Använd följande video för en snabb översikt över hur du använder sandlådor i Experience Platform.

>[!VIDEO](https://video.tv.adobe.com/v/29838/?quality=12&learn=on)

Om du vill skapa en ny sandlåda väljer du knappen **[!UICONTROL Create Sandbox]** längst upp till höger på skärmen.

![](../images/ui/create-sandbox.png)

Dialogrutan **[!UICONTROL Create Sandbox]** visas där du uppmanas att ange typ, titel och namn för sandlådan. Om du skapar en utvecklingssandlåda väljer du **[!UICONTROL Development]** i listrutepanelen som visas. Om du skapar en produktionssandlåda väljer du **[!UICONTROL Production]**.

Titeln ska vara läsbar för människor och ska vara tillräckligt beskrivande för att vara lätt att identifiera. Sandlådans namn är en helgemen identifierare som ska användas i API-anrop och ska därför vara unikt och koncist. Namnet på sandlådan får bara bestå av alfanumeriska tecken och bindestreck (`-`), måste börja med en bokstav och får innehålla högst 256 tecken.

När du är klar väljer du **[!UICONTROL Create]**.

![](../images/ui/create-dialog.png)

När du har skapat sandlådan uppdaterar du sidan och den nya sandlådan visas på kontrollpanelen **[!UICONTROL Sandboxes]** med statusen [!UICONTROL Creating]. Det tar ca 15 minuter att etablera nya sandlådor av systemet, varefter deras status ändras till [!UICONTROL Active].

## Återställ en sandlåda

>[!NOTE]
>
>Du kan återställa alla produktions- eller utvecklingssandlådor i organisationen, förutom standardproduktionssandlådan.

Om du återställer en produktions- eller utvecklingssandlåda tas alla resurser som är kopplade till den sandlådan (scheman, datauppsättningar o.s.v.) bort, samtidigt som sandlådans namn och associerade behörigheter behålls. Den här&quot;rena&quot; sandlådan är fortfarande tillgänglig under samma namn för användare som har åtkomst till den.

Markera den sandlåda som du vill återställa i listan över sandlådor. Välj **[!UICONTROL Sandbox reset]** i den högra navigeringspanel som visas.

![](../images/ui/reset-sandbox.png)

En dialogruta visas där du uppmanas att bekräfta ditt val. Välj **[!UICONTROL Continue]** för att fortsätta.

![](../images/ui/reset-confirm.png)

I det sista bekräftelsefönstret anger du namnet på sandlådan i dialogrutan och väljer **[!UICONTROL Reset]**

![](../images/ui/reset-final-confirm.png)

## Ta bort en sandlåda

>[!NOTE]
>
>Du kan ta bort alla produktions- eller utvecklingssandlådor i organisationen, förutom standardproduktionssandlådan.

Om du tar bort en produktions- eller utvecklingssandlåda permanent tas alla resurser som är associerade med den sandlådan bort, inklusive behörigheter.

Markera den sandlåda som du vill ta bort i listan över sandlådor. Välj **[!UICONTROL Delete]** i den högra navigeringspanel som visas.

![](../images/ui/delete-sandbox.png)

En dialogruta visas där du uppmanas att bekräfta ditt val. Välj **[!UICONTROL Continue]** för att fortsätta.

![](../images/ui/delete-confirm.png)

I det sista bekräftelsefönstret anger du namnet på sandlådan i dialogrutan och väljer **[!UICONTROL Delete]**

![](../images/ui/delete-final-confirm.png)

## Nästa steg

Det här dokumentet visar hur du hanterar sandlådor i användargränssnittet för Experience Platform. Mer information om hur du hanterar sandlådor med hjälp av API:t för sandlådan finns i [utvecklarhandboken för sandlådan](../api/getting-started.md).