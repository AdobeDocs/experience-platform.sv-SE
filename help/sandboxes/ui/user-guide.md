---
keywords: Experience Platform;home;populära topics;sandbox user guide;sandbox guide
solution: Experience Platform
title: Användargränssnittshandbok för sandlådan
description: Det här dokumentet innehåller steg om hur du utför olika åtgärder relaterade till sandlådor i Adobe Experience Platform användargränssnitt.
exl-id: b258c822-5182-4217-9d1b-8196d889740f
source-git-commit: b9b00f41f146b34a1326c4c2ac104c022a416dc9
workflow-type: tm+mt
source-wordcount: '1085'
ht-degree: 0%

---

# Användargränssnittshandbok för sandlådan

Det här dokumentet innehåller steg om hur du utför olika åtgärder relaterade till sandlådor i Adobe Experience Platform användargränssnitt.

## Visa sandlådor

I Experience Platform-gränssnittet väljer du **[!UICONTROL Sandboxes]** i den vänstra navigeringen och sedan fliken **[!UICONTROL Browse]** för att öppna kontrollpanelen [!UICONTROL Sandboxes]. På kontrollpanelen visas alla tillgängliga sandlådor för din organisation, inklusive deras respektive typer (produktion eller utveckling).

![Kontrollpanelen för sandlådor med fliken Bläddra markerad, som visar en lista över tillgängliga sandlådor.](../images/ui/view-sandboxes.png)

## Växla mellan sandlådor

Sandlådeindikatorn finns i det övre huvudet i plattformsgränssnittet och visar titeln på den sandlåda som du för närvarande befinner dig i, dess region och dess typ.

![Kontrollpanelen för sandlådor med indikatorn för sandlådan markerad.](../images/ui/sandbox-indicator.png)

Om du vill växla mellan sandlådor markerar du sandlådeindikatorn och väljer sedan önskad sandlåda i listrutan. Du kan också söka efter den önskade sandlådan med hjälp av sökfunktionen i listrutan.

![Listrutan för sandlådeindikator visas med en lista över sandlådor som du har åtkomst till.](../images/ui/switcher-interface.png)

När en sandlåda är markerad uppdateras skärmen och uppdateras till den sandlåda du har markerat.

![Kontrollpanelen för sandlådan med den ändrade sandlådeindikatorn markerad.](../images/ui/sandbox-switched.png)

## Skapa en ny sandlåda {#create}

>[!CONTEXTUALHELP]
>id="platform_sandboxes_sandboxname"
>title="Namn på sandlåda"
>abstract="Sandlådenamnet är den text som används i bakänden för att skapa ett unikt ID för den här sandlådan."

>[!CONTEXTUALHELP]
>id="platform_sandboxes_sandboxtitle"
>title="Sandlådetitel"
>abstract="Sandlådans titel är det visningsnamn som representerar sandlådan i menyer och listrutor i hela Experience Platform användargränssnitt."

>[!WARNING]
>
>Om du vill skapa en ny sandlåda måste du lägga till den i en roll i [[!UICONTROL Permissions]](../../access-control/abac/ui/permissions.md) innan du kan börja använda den. Mer information om hur du etablerar en sandlåda för en roll finns i [dokumentationen för att hantera sandlådor för en roll](../../access-control/abac/ui/permissions.md#managing-sandboxes-for-role).

I följande video får du en snabb översikt över hur du använder sandlådor i Experience Platform.

>[!VIDEO](https://video.tv.adobe.com/v/29838/?quality=12&learn=on)

Om du vill skapa en ny sandlåda väljer du **[!UICONTROL Create sandbox]** i skärmens övre högra hörn.

![create-sandbox](../images/ui/create-sandbox.png)

Dialogrutan **[!UICONTROL Create sandbox]** visas. Markera listrutan **[!UICONTROL Type]** och välj sandlådetypen [!UICONTROL Development] eller [!UICONTROL Production].

![Dialogrutan Skapa sandlåda med sandlådetypväljaren markerad.](../images/ui/sandbox-type.png)

När du har valt typen anger du ett namn för sandlådan i fältet **[!UICONTROL Name]**. Sandlådans namn är en helgemen identifierare som ska användas i API-anrop och ska därför vara unikt och koncist. Namnet på sandlådan måste börja med en bokstav, ha högst 256 tecken och bestå endast av alfanumeriska tecken och bindestreck (-). Ange sedan en titel för din sandlåda i fältet **[!UICONTROL Title]**. Titeln ska vara läsbar för människor och ska vara tillräckligt beskrivande för att vara lätt att identifiera.

När du är klar väljer du **[!UICONTROL Create]**.

![Dialogrutan Skapa sandlåda med namnet och titeln ifylld och alternativet Skapa markerat.](../images/ui/sandbox-info.png)

När du har skapat sandlådan uppdaterar du sidan och den nya sandlådan visas på kontrollpanelen **[!UICONTROL Sandboxes]** med statusen [!UICONTROL Creating]. Det tar ca 30 sekunder att etablera nya sandlådor av systemet. Därefter ändras deras status till [!UICONTROL Active].

![Kontrollpanelen för sandlådor med den nyligen skapade sandlådan markerad.](../images/ui/new-sandbox.png)

## Återställ en sandlåda

>[!WARNING]
>
>Nedan följer en lista med undantag som kan hindra dig från att återställa standardproduktionssandlådan eller en användarskapad produktionssandlåda:
>
>* En användarskapad produktionssandlåda som används för dubbelriktad segmentdelning med Adobe Audience Manager eller Audience Core Service kan återställas efter ett varningsmeddelande.
>* Innan du initierar en sandlådeåterställning måste du ta bort dina kompositioner manuellt för att se till att de associerade målgruppsdata rensas ordentligt.
>* Sandbox-ID:t ändras när återställningen är klar.
>* För [Journey Optimizer B2B edition](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/guide-overview) stöds **inte återställning av sandlådor**. Om du återställer eller tar bort en sandlåda som är mappad till Journey Optimizer B2B edition kan data i Journey Optimizer B2B edition gå förlorade permanent och en ny Journey Optimizer B2B edition-instans kan behöva etableras.

### Ta bort målgruppskompositioner

Målgruppskomposition är för närvarande inte integrerat med funktionen för återställning av sandlådor, så målgrupper måste tas bort manuellt innan de kan utföra återställningen av sandlådan.

Välj **[!UICONTROL Audiences]** i avsnittet **[!UICONTROL Customers]** i den vänstra navigeringen och välj sedan fliken **[!UICONTROL Compositions]**.

![Kontrollpanelen Publiker med fliken Dispositioner markerad och markerad.](../images/ui/audiences.png)

Markera sedan ellipsen (`...`) bredvid den första målgruppen och välj **[!UICONTROL Delete]**.

![Målgruppsmenyn som markerar alternativet [!UICONTROL Delete].](../images/ui/delete-composition.png)

En bekräftelse på att borttagningen lyckades visas och du återgår till fliken **[!UICONTROL Compositions]**.

Upprepa stegen ovan med alla kompositioner. Detta tar bort alla målgrupper från målgruppslagret. När alla målgrupper har tagits bort kan du fortsätta att återställa sandlådan.

### Återställa en sandlåda

Om du återställer en produktions- eller utvecklingssandlåda tas alla resurser som är kopplade till den sandlådan (scheman, datauppsättningar o.s.v.) bort, samtidigt som sandlådans namn och associerade behörigheter behålls. Den här&quot;rena&quot; sandlådan är fortfarande tillgänglig under samma namn för användare som har åtkomst till den.

Markera den sandlåda som du vill återställa i listan över sandlådor. Välj **[!UICONTROL Sandbox reset]** i den högra navigeringspanelen som visas.

![Kontrollpanelen för sandlådan med vald sandlåda och alternativet för återställning av sandlåda markerat.](../images/ui/reset.png)

En dialogruta visas med en uppmaning om att bekräfta ditt val. Välj **[!UICONTROL Continue]** om du vill fortsätta.

![Återställningsdialogrutan visas med alternativet Fortsätt markerat.](../images/ui/reset-warning.png)

I det sista bekräftelsefönstret anger du namnet på sandlådan i dialogrutan och väljer **[!UICONTROL Reset]**.

![Återställningsdialogrutan med bekräftelsefältet och återställningsalternativet markerat.](../images/ui/reset-confirm.png)

## Ta bort en sandlåda

>[!WARNING]
>
>Du kan inte ta bort standardproduktionssandlådan. Alla användarskapade produktionssandlådor som används för dubbelriktad segmentdelning med [!DNL Audience Manager] eller [!DNL Audience Core Service] kan dock tas bort efter ett varningsmeddelande.

Om du tar bort en produktions- eller utvecklingssandlåda permanent tas alla resurser som är associerade med den sandlådan bort, inklusive behörigheter.

Markera den sandlåda som du vill ta bort i listan över sandlådor. Välj **[!UICONTROL Delete]** i den högra navigeringspanelen som visas.

![Kontrollpanelen för sandlådan med vald sandlåda och alternativet Ta bort markerat.](../images/ui/delete.png)

En dialogruta visas med en uppmaning om att bekräfta ditt val. Välj **[!UICONTROL Continue]** om du vill fortsätta.

![Dialogrutan Ta bort visas med alternativet Fortsätt markerat.](../images/ui/delete-warning.png)

I det sista bekräftelsefönstret anger du namnet på sandlådan i dialogrutan och väljer **[!UICONTROL Continue]**.

![Dialogrutan för borttagning med bekräftelsefältet och alternativet för att fortsätta är markerat.](../images/ui/delete-confirm.png)

## Nästa steg

Det här dokumentet visar hur du hanterar sandlådor i Experience Platform-gränssnittet. Nu när du vet hur du hanterar sandlådor kan du lära dig att förbättra konfigurationsnoggrannheten i sandlådor och sömlöst exportera och importera sandlådekonfigurationer mellan sandlådor med [sandlådeverktygen](./sandbox-tooling.md) .

Mer information om hur du hanterar sandlådor med hjälp av API:t för sandlådan finns i [utvecklarhandboken för sandlådan](../api/getting-started.md).
