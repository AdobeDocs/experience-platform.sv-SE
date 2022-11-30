---
title: Översikt över Integritetskonsolen
description: Lär dig övervaka dina sekretessrelaterade arbetsflöden i Adobe Experience Platform användargränssnitt.
source-git-commit: 1fac36a0fd767add92283cd256d8bcea783ecf3b
workflow-type: tm+mt
source-wordcount: '394'
ht-degree: 1%

---

# Översikt över Integritetskonsolen

The [!UICONTROL Privacy Console] På fliken Adobe Experience Platform UI finns en kontrollpanel med information om dina sekretessrelaterade åtgärder i Platform, inklusive arbetsorder för datahygien, förfrågningar från Privacy Service och granskningsloggar för plattformsanvändaraktiviteter.

Välj **[!UICONTROL Privacy Console]** i den vänstra navigeringen.

![Bildvisning [!UICONTROL Privacy Console] väljs i den vänstra navigeringen i plattformsgränssnittet](../images/governance-privacy-security/privacy-console/left-nav.png)

Härifrån kan du granska de tillgängliga [övervakningswidgetar](#widgets) från konsolen eller så kan du utforska ett av flera [använd fallstödlinjer](#use-case-guides) på plattformens sekretessfunktioner.

## Widgetar

[!UICONTROL Privacy Console] innehåller flera widgetar som kan hjälpa dig att övervaka sekretessåtgärder.

![Bildvisning [!UICONTROL Privacy Console] väljs i den vänstra navigeringen i plattformsgränssnittet](../images/governance-privacy-security/privacy-console/widgets.png)

>[!NOTE]
>
>Beroende på vilka SKU:er din organisation har köpt kanske en del widgetar som nämns nedan inte är tillgängliga.

Funktionen för varje widget beskrivs nedan:

| Widget-namn | Beskrivning |
| --- | --- |
| Orderstatus för datahygien | Visar status för postborttagningsprocesser under [Datahygien](../../hygiene/home.md) för den markerade tidsramen. Använd listrutan för att ändra tidsramen mellan de senaste 7 dagarna, 14 dagar och 30 dagarna. |
| Senaste arbetsorder för datahygien | Visar de senaste [Datahygien](../../hygiene/home.md) arbetsorder som bearbetas av systemet. Använd listrutan för att växla mellan nyligen skapade arbetsorder och nyligen uppdaterade arbetsorder. |
| De vanligaste åtgärderna | Visar de vanligaste åtgärderna på plattformen enligt [granskningsloggar](./audit-logs/overview.md) för den markerade tidsramen. Använd listrutan för att ändra tidsramen mellan de senaste 7 dagarna, 14 dagar och 30 dagarna. |
| De flesta aktiva användarna | Visar de mest aktiva plattformsanvändarna i organisationen enligt [granskningsloggar](./audit-logs/overview.md) för den markerade tidsramen. Använd listrutan för att ändra tidsramen mellan de senaste 7 dagarna, 14 dagar och 30 dagarna. |
| Personförfrågningar | Visar antalet förfrågningar från registrerade som skickats in och fyllts i av [Privacy Service](../../privacy-service/home.md) för en viss dag. |

{style=&quot;table-layout:auto&quot;}

## Använda fallstödlinjer

Konsolen innehåller flera produktguider som presenterar vanliga sekretessarbetsflöden i Platform, inklusive kortfattade instruktioner om hur du konfigurerar en grundläggande implementering.

![Bildvisning [!UICONTROL Privacy Console] väljs i den vänstra navigeringen i plattformsgränssnittet](../images/governance-privacy-security/privacy-console/use-case-guide.png)

## Nästa steg

Mer information om de olika plattformstjänsterna som är kopplade till fall av sekretessanvändning finns i följande dokumentation:

* [Attributbaserad åtkomstkontroll](../../access-control/abac/overview.md)
* [Granskningsloggar](./audit-logs/overview.md)
* [Datastyrning](../../data-governance/home.md)
* [Datahygien](../../hygiene/home.md)
* [Privacy Service](../../privacy-service/home.md)
