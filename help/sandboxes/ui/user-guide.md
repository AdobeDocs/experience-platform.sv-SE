---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Handbok för sandlådeanvändare
topic: user guide
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '514'
ht-degree: 0%

---


# Handbok för sandlådeanvändare

Det här dokumentet innehåller steg om hur du utför olika åtgärder som rör sandlådor i användargränssnittet i Adobe Experience Platform.

## Visa sandlådor

I användargränssnittet för Experience Platform klickar du på **Sandlådor** i den vänstra navigeringen för att öppna kontrollpanelen för _sandlådor_ . På kontrollpanelen visas alla tillgängliga sandlådor för din organisation, inklusive sandlådetyp (produktion eller utveckling) och tillstånd (aktiv, skapa, borttagen eller misslyckades).

![](../images/ui/sandboxes-tab.png)

## Växla mellan sandlådor

Kontrollen för **sandlådeväxlaren** längst upp till vänster på skärmen visar den aktiva sandlådan.

![](../images/ui/sandbox-selector.png)

Om du vill växla mellan sandlådor klickar du på sandlådeväxlaren och väljer önskad sandlåda i listrutan.

![](../images/ui/switch-sandbox.png)

När en sandlåda har valts uppdateras skärmen med den valda sandlådan i sandlådeväxlaren.

![](../images/ui/sandbox-switched.png)

## Skapa en ny sandlåda

Om du vill skapa en ny sandlåda i användargränssnittet klickar du på **Sandlådor** i den vänstra navigeringen och sedan på **Skapa sandlåda**.

![](../images/ui/create-sandbox-button.png)

Dialogrutan _Skapa sandlåda_ visas och du uppmanas att ange en visningsrubrik och ett namn för sandlådan. Visningsrubriken **** är avsedd att vara läsbar för människor och bör vara tillräckligt beskrivande för att vara lätt att identifiera. Sandlådans **namn** är en helgemen identifierare som ska användas i API-anrop och ska därför vara unikt och koncist.

När du är klar klickar du på **Skapa**.

![](../images/ui/create-sandbox-dialog.png)

>[!NOTE]
>
>Eftersom du endast är begränsad till att skapa icke-produktionssandlådtyper, är **typalternativet** låst till &quot;Ej produktion&quot; och kan inte ändras.

När du har skapat sandlådan uppdaterar du sidan och den nya sandlådan visas på _kontrollpanelen för sandlådor_ med statusen&quot;Skapar&quot;. Nya sandlådor tar ca 15 minuter att etablera av systemet, varefter deras status ändras till&quot;Aktiv&quot;.

![](../images/ui/sandbox-created.png)

## Återställ en sandlåda

>[!NOTE]
>
>Den här funktionen är bara tillgänglig för icke-produktionssandlådor. Det går inte att återställa produktionssandlådor.

Om du återställer en icke-produktionssandlåda tas alla resurser som är associerade med den sandlådan (scheman, datauppsättningar o.s.v.) bort, samtidigt som sandlådans namn och associerade behörigheter behålls. Den här&quot;rena&quot; sandlådan är fortfarande tillgänglig under samma namn för användare som har åtkomst till den.

Om du vill återställa en sandlåda i användargränssnittet klickar du på **Sandlådor** till vänster och sedan på den sandlåda du vill återställa. I dialogrutan som visas till höger på skärmen klickar du på **Återställ sandlåda**.

![](../images/ui/reset-sandbox-button.png)

En dialogruta visas där du uppmanas att bekräfta ditt val. Klicka på **Återställ** för att fortsätta.

<img src="../images/ui/reset-are-you-sure.png" width="350"><br>

Ett bekräftelsemeddelande visas och sandlådans tillstånd ändras till &quot;Resetting&quot;. När det har etablerats av systemet uppdateras dess tillstånd till &quot;Aktiv&quot; eller &quot;Misslyckades&quot;.

![](../images/ui/sandbox-resetting.png)

## Ta bort en sandlåda

>[!NOTE]
>
>Den här funktionen är bara tillgänglig för icke-produktionssandlådor. Det går inte att ta bort produktionssandlådor.

Om du tar bort en icke-produktionssandlåda permanent tas alla resurser som är associerade med den sandlådan bort, inklusive behörigheter.

Om du vill ta bort en sandlåda i användargränssnittet klickar du på **Sandlådor** i den vänstra navigeringen och sedan på den sandlåda du vill ta bort. Klicka på **Ta bort sandlåda** i den dialogruta som visas till höger på skärmen.

![](../images/ui/delete-sandbox-button.png)

En dialogruta visas där du uppmanas att bekräfta ditt val. Klicka på **Ta bort** för att fortsätta.

<img src="../images/ui/delete-are-you-sure.png" width="350"><br>

Ett bekräftelsemeddelande visas och sandlådan tas bort från arbetsytan i _Sandlådor_ .

## Nästa steg

Det här dokumentet visar hur du hanterar sandlådor i användargränssnittet för Experience Platform. Mer information om hur du hanterar sandlådor med hjälp av API:t för sandlådan finns i [utvecklarhandboken](../api/getting-started.md)för sandlådan.