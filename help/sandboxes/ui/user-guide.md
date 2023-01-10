---
keywords: Experience Platform;hem;populära ämnen;användarhandbok för sandlådan;sandlådeguide
solution: Experience Platform
title: Användargränssnittshandbok för sandlådan
description: Det här dokumentet innehåller steg om hur du utför olika åtgärder relaterade till sandlådor i Adobe Experience Platform användargränssnitt.
exl-id: b258c822-5182-4217-9d1b-8196d889740f
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '796'
ht-degree: 2%

---

# Användargränssnittshandbok för sandlådan

Det här dokumentet innehåller steg om hur du utför olika åtgärder relaterade till sandlådor i Adobe Experience Platform användargränssnitt.

## Visa sandlådor

Välj **[!UICONTROL Sandboxes]** i den vänstra navigeringen och sedan väljer **[!UICONTROL Browse]** för att öppna [!UICONTROL Sandboxes] kontrollpanel. På kontrollpanelen visas alla tillgängliga sandlådor för din organisation, inklusive deras respektive typer (produktion eller utveckling).

![view-sandbox](../images/ui/view-sandboxes.png)

## Växla mellan sandlådor

Sandlådeindikatorn finns i det övre huvudet i plattformsgränssnittet och visar titeln på den sandlåda som du för närvarande befinner dig i, dess region och dess typ.

![sandlådeindikator](../images/ui/sandbox-indicator.png)

Om du vill växla mellan sandlådor markerar du sandlådeindikatorn och väljer önskad sandlåda i listrutan.

![växlargränssnitt](../images/ui/switcher-interface.png)

När en sandlåda har valts uppdateras skärmen och uppdateras till den sandlåda du har valt.

![sandlådeväxlad](../images/ui/sandbox-switched.png)

## Skapa en ny sandlåda {#create}

>[!CONTEXTUALHELP]
>id="platform_sandboxes_sandboxname"
>title="Namn på sandlåda"
>abstract="Sandlådenamnet är den text som används i bakänden för att skapa ett unikt ID för den här sandlådan."

>[!CONTEXTUALHELP]
>id="platform_sandboxes_sandboxtitle"
>title="Sandlådetitel"
>abstract="Sandlådans titel är det visningsnamn som representerar sandlådan i menyer och listrutor i hela användargränssnittet i Experience Platform."

>[!NOTE]
>
>När en ny sandlåda skapas måste du först lägga till den nya sandlådan i din produktprofil i [Adobe Admin Console](https://adminconsole.adobe.com/) innan du kan börja använda den nya sandlådan. Läs dokumentationen om [hantera behörigheter för en produktprofil](../../access-control/ui/permissions.md) om du vill ha information om hur du distribuerar en sandlåda till en produktprofil.

Använd följande video för en snabb översikt över hur du använder sandlådor i Experience Platform.

>[!VIDEO](https://video.tv.adobe.com/v/29838/?quality=12&learn=on)

Om du vill skapa en ny sandlåda väljer du **[!UICONTROL Create sandbox]** i skärmens övre högra hörn.

![create-sandbox](../images/ui/create-sandbox.png)

The **[!UICONTROL Create sandbox]** visas. Om du skapar en utvecklingssandlåda väljer du **[!UICONTROL Development]** i listrutepanelen. Om du vill skapa en ny produktionssandlåda väljer du **[!UICONTROL Production]**.

![sandlådetyp](../images/ui/sandbox-type.png)

När du har valt typen anger du ett namn och en titel i sandlådan. Titeln ska vara läsbar för människor och ska vara tillräckligt beskrivande för att vara lätt att identifiera. Sandlådans namn är en helgemen identifierare som ska användas i API-anrop och ska därför vara unikt och koncist. Namnet på sandlådan måste börja med en bokstav, ha högst 256 tecken och bestå endast av alfanumeriska tecken och bindestreck (-).

När du är klar väljer du **[!UICONTROL Create]**.

![sandbox-info](../images/ui/sandbox-info.png)

När du har skapat sandlådan uppdaterar du sidan och den nya sandlådan visas i **[!UICONTROL Sandboxes]** kontrollpanel med statusen &quot;[!UICONTROL Creating]&quot;. Det tar ca 30 sekunder att tilldela nya sandlådor via systemet, varefter deras status ändras till[!UICONTROL Active]&quot;.

![new-sandbox](../images/ui/new-sandbox.png)

## Återställ en sandlåda

>[!WARNING]
>
>Nedan följer en lista med undantag som kan hindra dig från att återställa standardproduktionssandlådan eller en användarskapad produktionssandlåda: <ul><li>Standardproduktionssandlådan kan inte återställas om identitetsdiagrammet som finns i sandlådan också används av Adobe Analytics för [CDA (Cross Device Analytics)](https://experienceleague.adobe.com/docs/analytics/components/cda/overview.html?lang=sv) -funktion.</li><li>Standardproduktionssandlådan kan inte återställas om identitetsdiagrammet som finns i sandlådan också används av Adobe Audience Manager för [Personbaserade mål (PBD)](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/people-based/people-based-destinations-overview.html?lang=sv).</li><li>Standardproduktionssandlådan kan inte återställas om den innehåller data för både CDA- och PBD-funktioner.</li><li>En användarskapad produktionssandlåda som används för dubbelriktad segmentdelning med Adobe Audience Manager eller Audience Core Service kan återställas efter ett varningsmeddelande.</li></ul>

Om du återställer en produktions- eller utvecklingssandlåda tas alla resurser som är kopplade till den sandlådan (scheman, datauppsättningar o.s.v.) bort, samtidigt som sandlådans namn och associerade behörigheter behålls. Den här&quot;rena&quot; sandlådan är fortfarande tillgänglig under samma namn för användare som har åtkomst till den.

Markera den sandlåda som du vill återställa i listan över sandlådor. Välj **[!UICONTROL Sandbox reset]**.

![återställ](../images/ui/reset.png)

En dialogruta visas med en uppmaning om att bekräfta ditt val. Välj **[!UICONTROL Continue]** för att fortsätta.

![reset-warning](../images/ui/reset-warning.png)

I det sista bekräftelsefönstret anger du namnet på sandlådan i dialogrutan och väljer **[!UICONTROL Reset]**.

![reset-confirm](../images/ui/reset-confirm.png)

## Ta bort en sandlåda

>[!WARNING]
>
>Du kan inte ta bort standardproduktionssandlådan. Alla användarskapade produktionssandlådor som används för dubbelriktad segmentdelning med [!DNL Audience Manager] eller [!DNL Audience Core Service] kan tas bort efter ett varningsmeddelande.

Om du tar bort en produktions- eller utvecklingssandlåda permanent tas alla resurser som är associerade med den sandlådan bort, inklusive behörigheter.

Markera den sandlåda som du vill ta bort i listan över sandlådor. Välj **[!UICONTROL Delete]**.

![delete](../images/ui/delete.png)

En dialogruta visas med en uppmaning om att bekräfta ditt val. Välj **[!UICONTROL Continue]** för att fortsätta.

![delete-warning](../images/ui/delete-warning.png)

I det sista bekräftelsefönstret anger du namnet på sandlådan i dialogrutan och väljer  **[!UICONTROL Continue]**.

![delete-confirm](../images/ui/delete-confirm.png)

## Nästa steg

Det här dokumentet visar hur du hanterar sandlådor i användargränssnittet för Experience Platform. Mer information om hur du hanterar sandlådor med hjälp av API:t för sandlådan finns i [utvecklarguide för sandlådor](../api/getting-started.md).
