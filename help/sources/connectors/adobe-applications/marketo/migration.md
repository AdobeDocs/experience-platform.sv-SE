---
title: Migrera ECID-mappning från människa till aktivitet med hjälp av Marketo Engage-källan
description: Lär dig hur du migrerar din ECID-mappning från persondatauppsättningen till aktivitetsdatauppsättningen med hjälp av Marketo Engage-källan.
source-git-commit: 0c695e11e7d7c14ef7e047cd007668e1099bf127
workflow-type: tm+mt
source-wordcount: '537'
ht-degree: 0%

---

# Migrera ECID-mappning från [!DNL Person] datauppsättning till [!DNL Activity] datauppsättning

Du kan migrera din ECID-mappning från [!DNL Marketo Engage Person] datauppsättning för [!DNL Activity] datauppsättning för att ge ett mer stabilt beteende för datainhämtning och identitetshantering. Den här migreringen åtgärdar dessutom följande:

| Problem | Lösning |
| --- | --- |
| När [!DNL Marketo Person] datauppsättningen har länkar till flera ECID, datainmatningen misslyckas när [det totala antalet identiteter i en XDM-post (Experience Data Model) överskrider 20](../../../../identity-service/guardrails.md). | Genom att migrera ECID-fältmappningen till [!DNL Activity]kan du se till att antalet identiteter från [!DNL Marketo Person] dataflödet ligger inom gränsen och gör att dataimporten kan lyckas. |
| Varje gång [!DNL Marketo Person] datauppsättningen importeras med ECID:n, tidsstämpeln för alla ECID:n från [!DNL Marketo Person] datauppsättningen uppdateras med den senaste uppdaterade tidsstämpeln för personposten. Detta kan leda till att [felaktig borttagning av senare identiteter från identitetsdiagrammet](../../../../identity-service/guardrails.md#understanding-the-deletion-logic-when-an-identity-graph-at-capacity-is-updated). | Genom att migrera ECID-fältkopplingar till [!DNL Activity], kan identitetstjänsten korrekt återspegla tidsstämpeln för ECID:n och den första-in-och-ut-mekanismen i identitetstjänsten kommer att ge ett mer stabilt beteende. |
| När ECID:n hämtas igenom [!DNL Marketo Person] dataflöde, nyligen tillagda ECID:n hämtas inte in i Experience Platform såvida det inte finns uppdateringar i [!DNL Person] posta i [!DNL Marketo]. | När ett nytt ECID är länkat till [!DNL Person] posta i [!DNL Marketo]kan du importera ECID-data via en [!DNL Marketo Activity] dataflöde och omedelbart föreslå en uppdatering av identitetsdiagrammet på Experience Platform. |

I grund och botten måste du

* Uppdatera dina [!DNL Marketo Activity] dataflöde.
* Uppdatera dina [!DNL Marketo Person] dataflöde.

## Uppdatera [!DNL Marketo Activity] dataflöde {#update-activity-dataflow}

Följ stegen nedan för att uppdatera [!DNL Marketo Activity] dataflöde:

* I användargränssnittet för Experience Platform går du till *Källor* arbetsyta och hitta ditt befintliga dataflöde för [!DNL Marketo Activity] data.
* Om dataflödet är aktiverat väljer du ellipserna (`...`) bredvid dataflödets namn och välj **[!UICONTROL Update dataflow]**.
* Välj sedan **[!UICONTROL Next]** tills du når *Mappning* gränssnitt.
* I *Mappning* gränssnitt, välja **[!UICONTROL New field]** och sedan **[!UICONTROL Add calculated field]**. Här måste du lägga till följande:

| Källdatauppsättning | XDM-målfält |
| --- | --- |
| `iif(${web\.ecid} != null, to_object('ECID', arrays_to_objects('id', explode(last(split(${web\.ecid}, ":")), " "))), null)` | `identityMap` |

>[!NOTE]
>
>Om din uppdatering till en befintlig [!DNL Marketo] Dataflödet består endast av att lägga till eller ta bort ECID-mappningsfältet, och dataflödet hoppar automatiskt över det historiska backfill-jobbet. Ny dataöverföring sker endast när aktivitetstyper som &quot;besök på webbsida&quot; och &quot;klicka på webbsida&quot; inträffar.

## Uppdatera [!DNL Marketo Person] dataflöde {#update-person-dataflow}

Följ stegen nedan för att uppdatera [!DNL Marketo Person] dataflöde:

* I användargränssnittet för Experience Platform går du till *Källor* arbetsyta och hitta ditt befintliga dataflöde för [!DNL Marketo Person] data.
* Om dataflödet är aktiverat väljer du ellipserna (`...`) bredvid dataflödets namn och välj **[!UICONTROL Update dataflow]**.
* Välj sedan **[!UICONTROL Next]** tills du når *Mappning* gränssnitt.
* I *Mappning* gränssnitt, ta bort beräkningsfältet som mappar till `identityMap` och sedan **[!UICONTROL Next]** och **[!UICONTROL Save & Ingest]**.

>[!NOTE]
>
>Om din uppdatering till en befintlig [!DNL Marketo] Dataflödet består endast av att lägga till eller ta bort ECID-mappningsfältet, och dataflödet hoppar automatiskt över det historiska backfill-jobbet. Tidsstämpeln för ECID:n som tidigare har importerats förblir densamma. De kommer endast att uppdateras när nya data som motsvarar befintliga ECID:n hämtas.

## Nästa steg

Genom att läsa det här dokumentet kan du nu migrera din ECID-mappning från [!DNL Marketo Person] datauppsättning till [!DNL Marketo Activity] datauppsättning. Mer information finns i följande [!DNL Marketo] dokument:

* [Skapa ett dataflöde att importera [!DNL Marketo] data till Experience Platform](../../../tutorials/ui/create/adobe-applications/marketo.md).
* [Fältmappningsguide](../mapping/marketo.md).