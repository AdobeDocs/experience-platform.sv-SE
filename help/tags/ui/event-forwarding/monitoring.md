---
title: Övervaka aktiviteter i händelsevidarebefordran
description: Lär dig hur du övervakar användning, fel och beräkningstid i egenskaperna för vidarebefordran av händelser.
feature: Event Forwarding
exl-id: 9d8572a3-816e-4b66-afe6-344fe8a15f22
source-git-commit: 9313ebe6d51d5ef42915d154def9cb0612407439
workflow-type: tm+mt
source-wordcount: '535'
ht-degree: 0%

---

# Övervaka aktiviteter i händelsevidarebefordran (beta)

>[!IMPORTANT]
>
>Den här funktionen är för närvarande i betaversion och din organisation har kanske inte åtkomst till den än. Funktionen och dokumentationen kan komma att ändras.

The **[!UICONTROL Monitoring]** I användargränssnittet för datainsamling kan du övervaka användningsmönster, fel och beräkningstid för egenskaper för vidarebefordran av händelser. Den här guiden ger en översikt på hög nivå över hur du visar och förstår de rapporter som visas på fliken.

![Bild som visar övervakningsfliken i användargränssnittet för datainsamling](../../images/ui/event-forwarding/monitoring/monitoring-tab.png)

## Förutsättningar

Den här guiden förutsätter att du har köpt vidarebefordran av händelser och att du har en fungerande förståelse för hur vidarebefordran av händelser fungerar. Se [händelsevidarebefordring - översikt](./overview.md) för mer information.

## Videoöversikt

I följande video visas en översikt över övervakningsfunktionen på hög nivå:

>[!VIDEO](https://video.tv.adobe.com/v/343999?quality=12&learn=on)

## Välja egenskaper och miljöer

Du kan visa mätvärden i en enskild miljö och egendom, eller i alla egenskaper och miljöer som ägs av organisationen.

Om du vill visa mätvärden för en enskild egenskap väljer du egenskapens listruta och väljer den egenskap som är av intresse i listan. När du har valt en egenskap kan du också använda listrutan för att välja en miljö som är av intresse.

![Bild som visar rullgardinsmenyerna för egenskapsmiljön i användargränssnittet](../../images/ui/event-forwarding/monitoring/property-environment.png)

## [!UICONTROL Usage]

The **[!UICONTROL Usage]** rapporten visar inkommande och utgående samtal för en viss tidsperiod. Inkommande samtal representerar data som skickas till händelsevidarebefordran. Utgående anrop representerar data som skickas från händelsevidarebefordran. The **[!UICONTROL Total events]** talet i den vänstra rutan är summan av inkommande och utgående samtal för den angivna tidsperioden.

## [!UICONTROL Error Events]

The **[!UICONTROL Error Events]** rapporten visar fel i sammanställningen och som bryts ned av HTTP-svarskoden när du håller markören över linjediagrammet. De fel som visas kommer från utgående samtal och svarskoderna kommer från slutpunkten som händelsevidarebefordran interagerar med.

Felen visas för en viss tidsperiod, som kan justeras i den angivna listrutan.

![Bild som visar listrutan för tidsperioden för felhändelserapporten](../../images/ui/event-forwarding/monitoring/error-time.png)

Med sökrutan för felhändelsen kan du fråga efter vidarebefordran av händelser för att förstå felen för en viss slutpunktsdomän. Du måste ange den exakta domänen eftersom sökfunktionen inte accepterar approximationer eller&quot;luddiga&quot; träffar. När du har angett en exakt domän för vilken det finns utgående feldata trycker du på Retur och rapporten uppdateras för att visa utgående fel för den domänen. Om du till exempel vill se fel från Facebook Conversion API-slutpunkten ska domänen skrivas som `https://graph.facebook.com`.

## [!UICONTROL Compute Time]

The **[!UICONTROL Compute Time]** rapporten visar beräkningstiden för alla regler för händelsevidarebefordringsservrar.

>[!NOTE]
>
>De tider som visas representerar inte fördröjning från början till slut. Vidarebefordran av händelser har en tidsbegränsning på 50 millisekunder. Om den här gränsen överskrids kommer relaterade data att tas bort.

Följande faktorer påverkar beräkningstiden:

1. Antalet regler
2. Reglernas komplexitet, som vanligtvis styrs av mängden anpassad JavaScript som körs

Om till exempel en åtgärd i en händelsevidarebefordring träffar en slutpunkt och slutpunkten tar två sekunder att svara, kommer denna fördröjning inte att räknas mot beräkningstiden eftersom händelsevidarebefordran bara väntar och inte aktivt beräknar någonting. Svarstiden får inte vara längre än 30 sekunder, annars kommer data att tas bort.
