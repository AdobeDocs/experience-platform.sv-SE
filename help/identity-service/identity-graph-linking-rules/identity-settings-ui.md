---
title: Användargränssnitt för identitetsinställningar
description: Lär dig hur du använder användargränssnittet för identitetsinställningar.
hide: true
hidefromtoc: true
badge: Beta
source-git-commit: 605aa5ed2db2bfd7f787f2dff9fa00cee2afbce6
workflow-type: tm+mt
source-wordcount: '465'
ht-degree: 0%

---

# Användargränssnitt för identitetsinställning

>[!AVAILABILITY]
>
>Den här funktionen är inte tillgänglig ännu. Betaprogrammet för länkningsregler för identitetsdiagram förväntas starta i juli för utvecklingssandlådor. Kontakta ditt Adobe-kontoteam för att få information om deltagandekriterierna.

Identitetsinställningar är en funktion i användargränssnittet för Adobe Experience Platform Identity Service som du kan använda för att ange unika namnutrymmen och konfigurera namnområdesprioritet.

Läs den här vägledningen när du vill lära dig hur du använder verktyget för identitetsinställningar.

## Förutsättning

Läs följande dokument innan du börjar arbeta med identitetsinställningar:

* [Identitetsoptimeringsalgoritm](./identity-optimization-algorithm.md)
* [Namnområdesprioritet](./namespace-priority.md)
* [Diagramsimulering](./graph-simulation.md)

## Konfigurera dina identitetsinställningar

Om du vill komma åt identitetsinställningarna går du till arbetsytan för identitetstjänsten i Adobe Experience Platform-användargränssnittet och väljer sedan **[!UICONTROL Settings]**.

![Knappen för identitetsinställningar har valts.](../images/rules/identity-ui.png)

Sidan med identitetsinställningar visas och du får ett bekräftelsemeddelande som påminner dig om att först testa och validera dina identitetsinställningar i en utvecklingssandlåda innan du slutför konfigurationer i en produktionssandlåda.

![Sidan med identitetsinställningar.](../images/rules/identity-settings.png)

Sidan med identitetsinställningar är uppdelad i två avsnitt: [!UICONTROL Person namespaces] och [!UICONTROL Device or cookie namespaces]. Personnamnutrymmen är identifierare för enskilda personer. De kan vara enhets-ID, e-postadresser och telefonnummer. Namnutrymmen för enheter och cookies är identifierare för enheter och webbläsare och kan inte ges en högre prioritet än namnutrymmen för personer. Du kan inte heller ange att namnutrymmet för en enhet eller cookie ska vara ett unikt namnutrymme.

### Ange ditt unika namnutrymme

Välj [!UICONTROL Unique per graph] kryssruta som motsvarar namnutrymmet. Du kan välja mer än ett unikt namnutrymme för konfigurationen av identitetsinställningarna.

![Två unika namnutrymmen är markerade.](../images/rules/unique-namespaces.png)

När de unika namnutrymmena har skapats kan diagram inte längre ha flera identiteter som innehåller ett unikt namnutrymme. Om du till exempel angav Anpassat Analytics-ID som ett unikt namnutrymme, kan ett diagram bara ha en identitet med namnutrymmet Anpassat ID för Analytics. Mer information finns i [Översikt över algoritmen för identitetsoptimering](./identity-optimization-algorithm.md#unique-namespace).

### Konfigurera namnområdesprioritet

Om du vill konfigurera namnområdesprioriteten väljer du ett namnutrymme på menyn för identitetsinställningar och drar och släpper sedan namnutrymmet i den ordning som du vill ha det. Placera ett namnutrymme högre upp i listan för att ge det högre prioritet och tvärtom placera ett namnutrymme längre ned i listan för att ge det lägre prioritet. Det namnutrymme som har högst prioritet bör också anges som ett unikt namnutrymme.

När du är klar med konfigurationerna väljer du **[!UICONTROL Next]**. Ett bekräftelsemeddelande visas. Använd tillfället för att verifiera att dina konfigurationer är korrekta och välj sedan **[!UICONTROL Finish]**.

![Valideringssidan.](../images/rules/validate.png)

Det visas en varning om att dina nya inställningar inte kommer att påverka befintliga länkar i ett identitetsdiagram och påverka händelseprofilfragment som redan har importerats. Bekräfta att du angett namnet på sandlådan och välj sedan **[!UICONTROL Confirm]**.

![Bekräftelsefönstret.](../images/rules/confirm.png)