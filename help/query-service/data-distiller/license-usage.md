---
title: Övervaka användning av batchfrågelicens
description: Adobe Experience Platform användargränssnitt innehåller en kontrollpanel där du kan visa viktig information om hur din organisation använder din Data Distiller-licens.
exl-id: a1e365a0-cc65-4fd6-b36f-8d79b7d9ec7c
recommendations: noCatalog, display
source-git-commit: e55cada0975d771f225e829aeeeeeeb64b9acf4a
workflow-type: tm+mt
source-wordcount: '270'
ht-degree: 0%

---

# Övervaka användning av batchfrågelicens {#monitor-license-usage}

Kontrollpanelen för licensanvändning innehåller detaljerade rapporter om organisationens användning av frågetjänstlicenser och användningsstatistik för varje köpt produkt. Om du vill veta mer om tillgängliga mätvärden på kontrollpanelen går du till [kontrollpanel för licensanvändning](../../dashboards/guides/license-usage.md#available-metrics).

Kontrollpanelen tillhandahåller användningsstatistik för varje köpt produkt, konsoliderad användning av statistik i alla produktions- eller utvecklingssandlådor samt användningsstatistik från en viss sandlåda. Den information som visas här fångas in under en daglig ögonblicksbild av din Platform-instans.

>[!NOTE]
>
>Kontrollpanelen för licensanvändning är inte aktiverad som standard. Användarna måste beviljas behörigheten &quot;Visa kontrollpanel för licensanvändning&quot; för att kunna visa kontrollpanelen. Anvisningar om hur du beviljar åtkomstbehörigheter för att visa kontrollpanelen för licensanvändning finns i [behörighetsguide för instrumentpanel](../../dashboards/permissions.md).

## Beräkningstimmar {#compute-hours}

The [!UICONTROL Compute hours] Mätvärdet gäller endast för kunder som har Data Distiller-licens för batchfrågor. [!UICONTROL Compute hours] är den tid det tar för frågetjänstmotorerna att läsa, bearbeta och skriva in data i datasjön när en batchfråga körs.

>[!NOTE]
>
>**Data är tillgängliga med begränsningar**: Data börjar från 1 oktober 2023 utan några trender.<br>The **bakfyllning** data från avtalets startdatum är ett pågående arbete. Den förväntas vara tillgänglig i slutet av kalenderåret.

![Kontrollpanelen för licensanvändning med måttet för antal beräknade timmar markerat.](../images/data-distiller/compute-hours.png)

Mer information om vilka mätvärden som är tillgängliga för din organisation baserat på din organisations köpta licens finns i [kontrollpanel för licensanvändning](../../dashboards/guides/license-usage.md).
