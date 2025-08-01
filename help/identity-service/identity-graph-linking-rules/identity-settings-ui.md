---
title: Användargränssnitt för identitetsinställningar
description: Lär dig hur du använder användargränssnittet för identitetsinställningar.
exl-id: 738b7617-706d-46e1-8e61-a34855ab976e
source-git-commit: 7596a87309105897a2727faa8e22b06cdf5547c3
workflow-type: tm+mt
source-wordcount: '647'
ht-degree: 0%

---

# Användargränssnitt för identitetsinställningar

>[!IMPORTANT]
>
>[!DNL Identity Graph Linking Rules] är nu allmänt tillgänglig. Kontakta Adobe Account Team eller Adobe Support om du har en befintlig sandlåda som kräver att komprimerade diagram inte är komprimerade (&quot;fasta&quot;) när du har aktiverat identitetsinställningarna.

Identitetsinställningar är en funktion i användargränssnittet för Adobe Experience Platform Identity Service som du kan använda för att ange unika namnutrymmen och konfigurera namnområdesprioritet.

Titta på följande video om du vill ha mer information om hur du använder gränssnittet [!DNL Graph Simulation] på arbetsytan i identitetstjänstens gränssnitt:

>[!VIDEO](https://video.tv.adobe.com/v/3458487/?learn=on&enablevpops)

Läs den här vägledningen när du vill lära dig hur du konfigurerar dina identitetsinställningar i användargränssnittet.

## Förhandskrav

Läs följande dokument innan du börjar arbeta med identitetsinställningar:

* [[!DNL Identity Graph Linking Rules]](./overview.md)
* [Optimeringsalgoritm för identitet](./identity-optimization-algorithm.md)
* [Implementeringsguide](./implementation-guide.md)
* [Exempel på diagramkonfigurationer](./example-configurations.md)
* [Namnområdesprioritet](./namespace-priority.md)
* [Diagramsimulering](./graph-simulation.md)

### Ange behörigheter {#set-permissions}

Därefter måste du se till att ditt konto har följande behörigheter:

* **[!UICONTROL View Identity Settings]**: Använd den här behörigheten för att kunna visa unika namnutrymmen och namnområdesprioritet på ID-namnutrymmets bläddringssida.
* **[!UICONTROL Edit Identity Settings]**: Använd den här behörigheten för att kunna redigera och spara dina identitetsinställningar.

Kontakta administratören om du inte har dessa behörigheter. Mer information finns i [behörighetshandboken](../../access-control/abac/ui/permissions.md).

## Konfigurera dina identitetsinställningar

Om du vill komma åt identitetsinställningarna går du till identitetstjänstens arbetsyta i Adobe Experience Platform-gränssnittet och väljer **[!UICONTROL Settings]**.

![Gränssnittet på kontrollpanelen för identitet med knappen Inställningar markerad.](../images/rules/dashboard.png)

Sidan med identitetsinställningar är uppdelad i två avsnitt: [!UICONTROL Person namespaces] och [!UICONTROL Device or cookie namespaces]. Personnamnutrymmen är identifierare för enskilda personer. De kan vara enhets-ID, e-postadresser och telefonnummer. Namnutrymmen för enheter och cookies är identifierare för enheter och webbläsare och kan inte ges en högre prioritet än namnutrymmen för personer. Du kan inte heller ange en enhets- eller cookie-namnrymd som ett unikt namnutrymme.

### Konfigurera namnområdesprioritet

Om du vill konfigurera namnområdesprioriteten väljer du ett namnutrymme på menyn för identitetsinställningar och drar och släpper sedan namnutrymmet i den ordning som du vill ha det. Placera ett namnutrymme högre upp i listan för att ge det högre prioritet och tvärtom placera ett namnutrymme längre ned i listan för att ge det lägre prioritet. Det namnutrymme som har högst prioritet bör också anges som ett unikt namnutrymme.

![Arbetsytan för identitetsinställningar med ett personnamnområde markerat.](../images/rules/namespace-priority.png)

### Ange ditt unika namnutrymme

Om du vill ange ett unikt namnutrymme markerar du kryssrutan [!UICONTROL Unique per graph] som motsvarar det namnutrymmet. Du kan välja **upp till högst tre unika namnutrymmen** för konfigurationen av identitetsinställningarna.

När de unika namnutrymmena har skapats kan diagram inte längre ha flera identiteter som innehåller ett unikt namnutrymme. Om du till exempel har angett CRMID som ett unikt namnutrymme, kan ett diagram bara ha en identitet med CRMID-namnutrymmet. Mer information finns i [Översikt över algoritmen för identitetsoptimering](./identity-optimization-algorithm.md#unique-namespace).

När du är klar med dina konfigurationer väljer du **[!UICONTROL Next]** för att fortsätta.

![Två namnutrymmen har markerats och definierats som unika.](../images/rules/unique-namespace.png)

Här måste du bekräfta följande innan du fortsätter till det sista steget:

1. De markerade unika namnutrymmena.
2. Identiteten med det högsta prioriterade unika namnutrymmet i varje känd profil.
3. Ordningen för namnområdesprioriteten.

![Ett bekräftelsefönster med knappen &quot;bekräfta&quot; markerad.](../images/rules/confirmation.png)

### Bekräfta inställningarna {#confirm-your-settings}

>[!IMPORTANT]
>
>* Det sista steget är ett annat bekräftelsemeddelande som anger att befintliga diagram bara påverkas av diagramalgoritmen **om diagrammen uppdateras efter att du har sparat dina inställningar** och att den primära identiteten för händelsefragment i kundprofilen i realtid inte uppdateras även efter att namnområdesprioriteten har ändrats.
>
>* Det tar upp till **24 timmar** innan de nya eller uppdaterade inställningarna börjar gälla. Bekräfta genom att ange namnet på din sandlåda och sedan välja **[!UICONTROL Confirm]**.
>
>* Inga ändringar görs i dina data förrän du sparar dina identitetsinställningar.

![Bekräftelsefönstret som visar en varning om en 24-timmars fördröjning innan konfigurationer bearbetas.](../images/rules/complete.png)

## Nästa steg

Mer information om [!DNL Identity Graph Linking Rules] finns i följande dokumentation:

* [[!DNL Identity Graph Linking Rules] översikt](./overview.md)
* [Optimeringsalgoritm för identitet](./identity-optimization-algorithm.md)
* [Implementeringsguide](./implementation-guide.md)
* [Exempel på diagramkonfigurationer](./example-configurations.md)
* [Felsökning och vanliga frågor](./troubleshooting.md)
* [Namnområdesprioritet](./namespace-priority.md)
* [Gränssnitt för diagramsimulering](./graph-simulation.md)