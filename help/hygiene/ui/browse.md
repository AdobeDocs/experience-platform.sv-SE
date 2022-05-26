---
title: Bläddra bland arbetsorder för datahygien
description: Lär dig hur du visar och hanterar befintliga arbetsbeställningar för datahygien i Adobe Experience Platform användargränssnitt.
exl-id: 76d4a809-cc2c-434d-90b1-23d88f29c022
hide: true
hidefromtoc: true
source-git-commit: e539ee73b04230ac6e3dc4801ce0f8446bec8de6
workflow-type: tm+mt
source-wordcount: '540'
ht-degree: 0%

---

# Bläddra bland arbetsorder för datahygien

>[!CONTEXTUALHELP]
>id="platform_hygiene_workorders"
>title="ID för arbetsorder"
>abstract="När en begäran om datahygien skickas till systemet skapas en arbetsorder för att utföra den begärda uppgiften. En arbetsorder representerar med andra ord en specifik datahygienprocess, som omfattar dess aktuella status och andra relaterade detaljer. Varje arbetsorder tilldelas automatiskt ett eget unikt ID när den skapas."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/hygiene/ui/browse.html" text="Mer information finns i användargränssnittsguiden för datahygien."

>[!IMPORTANT]
>
>Datahygien i Adobe Experience Platform är för närvarande endast tillgänglig för organisationer som har köpt Adobe Shield for Healthcare.

När en begäran om datahygien skickas till systemet skapas en arbetsorder för att utföra den begärda uppgiften. En arbetsorder representerar en särskild datahygienprocess (t.ex. att ta bort konsumentdata), som omfattar dess aktuella status och andra relaterade detaljer.

Den här guiden beskriver hur du visar och hanterar befintliga arbetsorder i Adobe Experience Platform användargränssnitt.

## Visa och filtrera befintliga arbetsorder

När du först öppnar **[!UICONTROL Data Hygiene]** i användargränssnittet visas en lista över befintliga arbetsorder tillsammans med deras grundläggande information.

![Bilden visar [!UICONTROL Data Hygiene] arbetsytan i plattformsgränssnittet](../images/ui/browse/work-order-list.png)

I listan visas endast arbetsorder för en kategori i taget. Välj **[!UICONTROL Consumer]** för att visa en lista över uppgifter som rör borttagning av konsumenter, och **[!UICONTROL Dataset]** om du vill visa en lista med TTL-scheman (time-to-live) för datauppsättningar.

![Bilden visar [!UICONTROL Dataset] tab](../images/ui/browse/dataset-tab.png)

Markera trattecknet (![Bild av trattsymbolen](../images/ui/browse/funnel-icon.png)) om du vill visa en lista med filter för de arbetsorder som visas.

![Bild på de arbetsorderfilter som visas](../images/ui/browse/filters.png)

Beroende på vilken flik du visar finns olika filter:

| Filter | Kategori | Beskrivning |
| --- | --- | --- |
| [!UICONTROL Status] | [!UICONTROL Consumer] &amp; [!UICONTROL Dataset] | Filtrera baserat på arbetsorderns aktuella status. |
| [!UICONTROL Date created] | [!UICONTROL Consumer] | Filtrera baserat på när konsumentborttagningsbegäran gjordes. |
| [!UICONTROL Date created] | [!UICONTROL Dataset] | Filtrera baserat på när konsumentborttagningsbegäran gjordes. |
| [!UICONTROL Deletion date] | [!UICONTROL Dataset] | Filtrera baserat på det borttagningsdatum som TTL har schemalagts. |
| [!UICONTROL Date updated] | [!UICONTROL Dataset] | Filtrera baserat på när datamängden TTL senast uppdaterades. TTL-skapelser och förfallodatum räknas som uppdateringar. |

{style=&quot;table-layout:auto&quot;}

## Visa information om en arbetsorder

Markera ID:t för en listad arbetsorder om du vill visa information om den.

![Bild som visar ett arbetsorders-ID som markeras](../images/ui/browse/select-work-order.png)

Beroende på vilken typ av arbetsordning du har valt visas olika information och kontroller. Dessa beskrivs i avsnitten nedan.

### Information om borttagning av kund

<!-- (Not available for initial release)
>[!CONTEXTUALHELP]
>id="platform_hygiene_responsemessages"
>title="Consumer delete response"
>abstract="When a consumer deletion process receives a response from the system, these messages are displayed under the **[!UICONTROL Result]** section. If a problem occurs while a work order is processing, any relevant error messages will appear in this section to help you troubleshoot the issue. To learn more, see the data hygiene UI guide."
-->

Detaljerna för en begäran om att ta bort en kund är skrivskyddade och visar dess grundläggande attribut, till exempel dess aktuella status och den tid som gått sedan begäran gjordes.

![Bild som visar informationssidan för en arbetsorder som ska tas bort av en kund](../images/ui/browse/consumer-delete-details.png)

### TTL-information för datauppsättning

Detaljsidan för en datauppsättnings-TTL innehåller information om dess grundläggande attribut, inklusive det schemalagda förfallodatumet på de dagar som återstår innan borttagningen sker. I den högra listen kan du använda kontroller för att redigera eller avbryta TTL-värdet.

![Bild som visar informationssidan för en TTL-arbetsorder för datauppsättning](../images/ui/browse/ttl-details.png)

## Nästa steg

I den här guiden beskrivs hur du visar och hanterar befintliga arbetsbeställningar för datahygien i användargränssnittet för plattformen. Mer information om hur du skapar egna arbetsorder finns i följande dokumentation:

* [Ta bort en konsument](./delete-consumer.md)
* [Schemalägg en datamängd-TTL](./ttl.md)
