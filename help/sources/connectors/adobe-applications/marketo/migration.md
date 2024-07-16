---
title: Migrera ECID-mappning från människa till aktivitet med hjälp av Marketo Engage-källan
description: Lär dig hur du migrerar din ECID-mappning från persondatauppsättningen till aktivitetsdatauppsättningen med hjälp av Marketo Engage-källan.
exl-id: bcc91c53-aeca-4d7c-89b5-cf025d0357a0
source-git-commit: d03fcf06fb63ad2484ded3b85fc11ae45661babc
workflow-type: tm+mt
source-wordcount: '537'
ht-degree: 0%

---

# Migrera ECID-mappning från datauppsättningen [!DNL Person] till datauppsättningen [!DNL Activity]

Du kan migrera din ECID-mappning från din [!DNL Marketo Engage Person]-datauppsättning till din [!DNL Activity]-datauppsättning för att få ett stabilare beteende för datainhämtning och identitetshantering. Den här migreringen åtgärdar dessutom följande:

| Problem | Lösning |
| --- | --- |
| När din [!DNL Marketo Person]-datauppsättning har länkar till flera ECID:n misslyckas datainmatningen när det [totala antalet identiteter i en XDM-post (Experience Data Model) överskrider 20](../../../../identity-service/guardrails.md). | Genom att migrera ECID-fältmappningen till [!DNL Activity] kan du se till att antalet identiteter från [!DNL Marketo Person]-dataflödet hålls inom gränsen och på så sätt möjliggöra att datainmatningen lyckas. |
| Varje gång [!DNL Marketo Person]-datauppsättningen importeras med ECID:n uppdateras tidsstämpeln för alla ECID:n från [!DNL Marketo Person]-datauppsättningen med den senaste uppdaterade tidsstämpeln för personposten. Detta kan leda till att [felaktiga identiteter tas bort från identitetsdiagrammet](../../../../identity-service/guardrails.md#understanding-the-deletion-logic-when-an-identity-graph-at-capacity-is-updated). | Genom att migrera ECID-fältmappningar till [!DNL Activity] kan identitetstjänsten korrekt återspegla tidsstämpeln för ECID:n och den första-in-och-ut-mekanismen i identitetstjänsten ger ett stabilare beteende. |
| När ECID:n hämtas via [!DNL Marketo Person]-dataflöde kapslas inte nyligen tillagda ECID:n in i Experience Platform om det inte finns uppdateringar för [!DNL Person]-posten i [!DNL Marketo]. | När ett nytt ECID är länkat till posten [!DNL Person] i [!DNL Marketo] kan du importera ECID-data via ett [!DNL Marketo Activity]-dataflöde och omedelbart föreslå en uppdatering av identitetsdiagrammet på Experience Platform. |

I grund och botten måste du

* Uppdatera [!DNL Marketo Activity]-dataflödet.
* Uppdatera [!DNL Marketo Person]-dataflödet.

## Uppdatera [!DNL Marketo Activity]-dataflöde {#update-activity-dataflow}

Uppdatera [!DNL Marketo Activity]-dataflödet genom att följa stegen nedan:

* Gå till arbetsytan *Källor* i användargränssnittet för Experience Platform och hitta ditt befintliga dataflöde för [!DNL Marketo Activity]-data.
* Eftersom dataflödet är aktiverat väljer du ellipserna (`...`) bredvid dataflödets namn och sedan **[!UICONTROL Update dataflow]**.
* Välj sedan **[!UICONTROL Next]** tills du når *mappningsgränssnittet*.
* I gränssnittet *Mappning* väljer du **[!UICONTROL New field]** och sedan **[!UICONTROL Add calculated field]**. Här måste du lägga till följande:

| Source dataset | XDM-målfält |
| --- | --- |
| `iif(${web\.ecid} != null, to_object('ECID', arrays_to_objects('id', explode(last(split(${web\.ecid}, ":")), " "))), null)` | `identityMap` |

>[!NOTE]
>
>Om din uppdatering av ett befintligt [!DNL Marketo]-dataflöde består av att endast lägga till eller ta bort ECID-mappningsfältet, hoppar dataflödet automatiskt över det historiska backfill-jobbet. Ny dataöverföring sker endast när aktivitetstyper som &quot;besök på webbsida&quot; och &quot;klicka på webbsida&quot; inträffar.

## Uppdatera [!DNL Marketo Person]-dataflöde {#update-person-dataflow}

Uppdatera [!DNL Marketo Person]-dataflödet genom att följa stegen nedan:

* Gå till arbetsytan *Källor* i användargränssnittet för Experience Platform och hitta ditt befintliga dataflöde för [!DNL Marketo Person]-data.
* Eftersom dataflödet är aktiverat väljer du ellipserna (`...`) bredvid dataflödets namn och sedan **[!UICONTROL Update dataflow]**.
* Välj sedan **[!UICONTROL Next]** tills du når *mappningsgränssnittet*.
* I gränssnittet *Mappning* tar du bort det beräknade fältet som mappar till `identityMap` och väljer sedan **[!UICONTROL Next]** och **[!UICONTROL Save & Ingest]**.

>[!NOTE]
>
>Om din uppdatering av ett befintligt [!DNL Marketo]-dataflöde består av att endast lägga till eller ta bort ECID-mappningsfältet, hoppar dataflödet automatiskt över det historiska backfill-jobbet. Tidsstämpeln för ECID:n som tidigare har importerats förblir densamma. De kommer endast att uppdateras när nya data som motsvarar befintliga ECID:n hämtas.

## Nästa steg

Genom att läsa det här dokumentet vet du nu hur du migrerar din ECID-mappning från [!DNL Marketo Person]-datauppsättningen till [!DNL Marketo Activity]-datauppsättningen. Mer information finns i följande [!DNL Marketo]-dokument:

* [Skapa ett dataflöde för att importera [!DNL Marketo] data till Experience Platform](../../../tutorials/ui/create/adobe-applications/marketo.md).
* [Fältmappningsguide](../mapping/marketo.md).
