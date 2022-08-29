---
title: Bläddra bland arbetsorder för datahygien
description: Lär dig hur du visar och hanterar befintliga arbetsbeställningar för datahygien i Adobe Experience Platform användargränssnitt.
exl-id: 76d4a809-cc2c-434d-90b1-23d88f29c022
source-git-commit: 80f9f0c64f2af2c7ceea59bddab9a5d6b57bc882
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Bläddra bland arbetsorder för datahygien {#browse-work-orders}

>[!CONTEXTUALHELP]
>id="platform_hygiene_workorders"
>title="ID för arbetsorder"
>abstract="När en begäran om datahygien skickas till systemet skapas en arbetsorder för att utföra den begärda uppgiften. En arbetsorder representerar med andra ord en specifik datahygienprocess, som omfattar dess aktuella status och andra relaterade detaljer. Varje arbetsorder tilldelas automatiskt ett eget unikt ID när den skapas."
>text="See the data hygiene UI guide to learn more."

>[!IMPORTANT]
>
>Datahygien i Adobe Experience Platform är för närvarande endast tillgänglig för organisationer som har köpt skölden.

När en begäran om datahygien skickas till systemet skapas en arbetsorder för att utföra den begärda uppgiften. En arbetsorder representerar en specifik datahygienprocess, t.ex. ett schemalagt utgångsdatum för datauppsättningen, som inkluderar dess aktuella status och andra relaterade detaljer.

Den här guiden beskriver hur du visar och hanterar befintliga arbetsorder i Adobe Experience Platform användargränssnitt.

## Visa och filtrera befintliga arbetsorder

När du först öppnar **[!UICONTROL Data Hygiene]** i användargränssnittet visas en lista över befintliga arbetsorder tillsammans med deras grundläggande information.

![Bilden visar [!UICONTROL Data Hygiene] arbetsytan i plattformsgränssnittet](../images/ui/browse/work-order-list.png)

<!-- The list only shows work orders for one category at a time. Select **[!UICONTROL Consumer]** to view a list of consumer deletion tasks, and **[!UICONTROL Dataset]** to view a list of scheduled dataset expirations.

![Image showing the [!UICONTROL Dataset] tab](../images/ui/browse/dataset-tab.png) -->

Markera trattecknet (![Bild av trattsymbolen](../images/ui/browse/funnel-icon.png)) om du vill visa en lista med filter för de arbetsorder som visas.

![Bild på de arbetsorderfilter som visas](../images/ui/browse/filters.png)

| Filter | Beskrivning |
| --- | --- |
| [!UICONTROL Status] | Filtrera baserat på arbetsorderns aktuella status:<ul><li>**[!UICONTROL Completed]**: Jobbet har slutförts.</li><li>**[!UICONTROL Pending]**: Jobbet har skapats men har inte körts än. A [förfallobegäran för datauppsättning](./dataset-expiration.md) antar denna status före det schemalagda raderingsdatumet. När borttagningsdatumet har passerats uppdateras statusen till [!UICONTROL Executing] om inte jobbet har avbrutits i förväg.</li><li>**[!UICONTROL Executing]**: Datauppsättningens förfallobegäran har startats och bearbetas för närvarande.</li><li>**[!UICONTROL Cancelled]**: Jobbet har avbrutits som en del av en manuell användarbegäran.</li></ul> |
| [!UICONTROL Date created] | Filtrera baserat på när arbetsordern skapades. |
| [!UICONTROL Expiration date] | Förfrågningar om förfallodatum för filterdatauppsättningen baserat på det schemalagda raderingsdatumet för den aktuella datauppsättningen. |
| [!UICONTROL Date updated] | Förfrågningar om förfallodatum för filterdatauppsättning baserat på när arbetsordern senast uppdaterades. Skapanden och förfallodatum räknas som uppdateringar. |

{style=&quot;table-layout:auto&quot;}

## Visa information om en arbetsorder {#view-details}

>[!CONTEXTUALHELP]
>id="platform_hygiene_statusbyservice"
>title="Status per tjänst"
>abstract="Förfrågningar om datahygien behandlas oberoende av olika Experience Platform-tjänster. I det här avsnittet beskrivs den aktuella bearbetningsstatusen för begäran för varje tjänst. Mer information finns i användargränssnittshandboken för datahygien."

Markera ID:t för en listad arbetsorder om du vill visa information om den.

![Bild som visar ett arbetsorders-ID som markeras](../images/ui/browse/select-work-order.png)

<!-- Depending on the type of work order selected, different information and controls are provided. These are covered in the sections below.

### Consumer delete details

>[!CONTEXTUALHELP]
>id="platform_hygiene_responsemessages"
>title="Consumer delete response"
>abstract="When a consumer deletion process receives a response from the system, these messages are displayed under the **[!UICONTROL Result]** section. If a problem occurs while a work order is processing, any relevant error messages will appear in this section to help you troubleshoot the issue. To learn more, see the data hygiene UI guide."


The details of a consumer delete request are read-only, displaying its basic attributes such as its current status and the time elapsed since the request was made.

![Image showing the details page for a consumer delete work order](../images/ui/browse/consumer-delete-details.png)

### Dataset expiration details -->

Detaljsidan för en datauppsättnings förfallodatum innehåller information om dess grundläggande attribut, inklusive det schemalagda förfallodatumet på de dagar som återstår innan borttagningen sker. I den högra listen kan du använda kontroller för att redigera eller avbryta förfallotiden.

![Bild som visar informationssidan för en arbetsorder för förfallodatum för datauppsättning](../images/ui/browse/ttl-details.png)

## Nästa steg

I den här guiden beskrivs hur du visar och hanterar befintliga arbetsbeställningar för datahygien i användargränssnittet för plattformen. Mer information om hur du skapar egna arbetsorder finns i guiden [schemalägga förfallodatum för en datauppsättning](./dataset-expiration.md).
