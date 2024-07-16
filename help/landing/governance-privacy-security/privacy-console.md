---
title: Översikt över Integritetskonsolen
description: Lär dig övervaka dina sekretessrelaterade arbetsflöden i Adobe Experience Platform användargränssnitt.
source-git-commit: 1fac36a0fd767add92283cd256d8bcea783ecf3b
workflow-type: tm+mt
source-wordcount: '400'
ht-degree: 1%

---

# Översikt över Integritetskonsolen

Fliken [!UICONTROL Privacy Console] i Adobe Experience Platform UI innehåller en instrumentpanel med en översikt över dina sekretessrelaterade åtgärder i Platform, inklusive arbetsorder för datahygien, förfrågningar från Privacy Service och granskningsloggar för användaraktiviteter i plattformen.

Om du vill komma åt instrumentpanelen väljer du **[!UICONTROL Privacy Console]** i den vänstra navigeringen.

![Bild som visar att [!UICONTROL Privacy Console] har valts i den vänstra navigeringen i plattformsgränssnittet](../images/governance-privacy-security/privacy-console/left-nav.png)

Härifrån kan du granska de [övervakningswidgetar](#widgets) som finns tillgängliga i konsolen, eller utforska en av flera [fallguider](#use-case-guides) för plattformens sekretessfunktioner.

## Widgetar

[!UICONTROL Privacy Console] innehåller flera widgetar som kan hjälpa dig att övervaka dina sekretessåtgärder.

![Bild som visar att [!UICONTROL Privacy Console] har valts i den vänstra navigeringen i plattformsgränssnittet](../images/governance-privacy-security/privacy-console/widgets.png)

>[!NOTE]
>
>Beroende på vilka SKU:er din organisation har köpt kanske en del widgetar som nämns nedan inte är tillgängliga.

Funktionen för varje widget beskrivs nedan:

| Widget-namn | Beskrivning |
| --- | --- |
| Orderstatus för datahygien | Visar status för postborttagningsprocesser under [Datahygien](../../hygiene/home.md) för den valda tidsramen. Använd listrutan för att ändra tidsramen mellan de senaste 7 dagarna, 14 dagar och 30 dagarna. |
| Senaste arbetsorder för datahygien | Visar de senaste [datahygien](../../hygiene/home.md)-arbetsbeställningarna som bearbetas av systemet. Använd listrutan för att växla mellan nyligen skapade arbetsorder och nyligen uppdaterade arbetsorder. |
| De vanligaste åtgärderna | Visar de vanligaste åtgärderna på plattformen enligt [granskningsloggarna](./audit-logs/overview.md) för den valda tidsramen. Använd listrutan för att ändra tidsramen mellan de senaste 7 dagarna, 14 dagar och 30 dagarna. |
| De flesta aktiva användarna | Visar de mest aktiva plattformsanvändarna i organisationen enligt [granskningsloggarna](./audit-logs/overview.md) för den valda tidsramen. Använd listrutan för att ändra tidsramen mellan de senaste 7 dagarna, 14 dagar och 30 dagarna. |
| Personförfrågningar | Visar antalet förfrågningar från registrerade personer som skickats och slutförts av [Privacy Service](../../privacy-service/home.md) för en viss dag. |

{style="table-layout:auto"}

## Använda fallstödlinjer

Konsolen innehåller flera produktguider som presenterar vanliga sekretessarbetsflöden i Platform, inklusive kortfattade instruktioner om hur du konfigurerar en grundläggande implementering.

![Bild som visar att [!UICONTROL Privacy Console] har valts i den vänstra navigeringen i plattformsgränssnittet](../images/governance-privacy-security/privacy-console/use-case-guide.png)

## Nästa steg

Mer information om de olika plattformstjänsterna som är kopplade till fall av sekretessanvändning finns i följande dokumentation:

* [Attributbaserad åtkomstkontroll](../../access-control/abac/overview.md)
* [Granskningsloggar](./audit-logs/overview.md)
* [Datastyrning](../../data-governance/home.md)
* [Datahygien](../../hygiene/home.md)
* [Integritetstjänst](../../privacy-service/home.md)
