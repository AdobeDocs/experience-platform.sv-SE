---
keywords: Experience Platform;profile;real-time customer profile;user interface;UI;customization;profile dashboard;dashboard
title: Kontrollpanel för profil
description: 'I den här guiden beskrivs den datapanel för kundprofiler i realtid som finns i Adobe Experience Platform användargränssnitt. '
topic: guide
type: Documentation
translation-type: tm+mt
source-git-commit: 983b357f2f17aad273f0465dc9250240a062dcd2
workflow-type: tm+mt
source-wordcount: '619'
ht-degree: 0%

---


# (Alfa) [!DNL Real-time Customer Profile] -kontrollpanel {#profile-dashboard}

>[!IMPORTANT]
>
>Instrumentpanelsfunktionen som beskrivs i det här dokumentet är för närvarande alfavertiv och är inte tillgänglig för alla användare. Dokumentationen och funktionaliteten kan komma att ändras.

Adobe Experience Platform användargränssnitt (UI) är en kontrollpanel där du kan visa viktig information om dina [!DNL Real-time Customer Profile] data, som de tagits med vid en daglig ögonblicksbild. I den här handboken beskrivs hur du kommer åt och arbetar med [!DNL Profile] kontrollpanelen i användargränssnittet och den innehåller mer information om mätvärdena som visas på kontrollpanelen.

En översikt över alla profilfunktioner i användargränssnittet för Experience Platform finns i användargränssnittet för [kundprofiler i realtid](user-guide.md).

## Data för kontrollpanel för profil

På kontrollpanelen Profil visas en ögonblicksbild av attributdata (postdata) som din organisation har i profilarkivet i Experience Platform. Ögonblicksbilden innehåller inga händelsedata (tidsserier).

Attributdata i ögonblicksbilden visar data exakt som de visas vid den specifika tidpunkten när ögonblicksbilden togs. Ögonblicksbilden är alltså inte en uppskattning eller ett urval av data och kontrollpanelen för profiler uppdateras inte i realtid.

>[!NOTE]
>
>Ändringar eller uppdateringar som gjorts i data sedan ögonblicksbilden togs kommer inte att visas på kontrollpanelen förrän nästa ögonblicksbild tas.

De mätvärden som visas på profilkontrollpanelen baseras på organisationens standardpolicy för sammanslagning. Mer information om kopplingsprofiler och hur du väljer eller ändrar standardkopplingsprofilen finns i användargränssnittshandboken för [kopplingsprofiler](merge-policies.md).

## Utforska profilkontrollpanelen

Om du vill navigera till profilkontrollpanelen i plattformsgränssnittet väljer du **[!UICONTROL Profiles]** i den vänstra listen och sedan fliken som du vill visa kontrollpanelen på **[!UICONTROL Overview]** .

![](../images/profile-dashboard/dashboard-overview.png)

### Widgetar och mätvärden

Kontrollpanelen består av widgetar, som är skrivskyddade mått som ger viktig information om dina profildata. Datum och tid för den senaste uppdateringen av widgeten visas när den senaste ögonblicksbilden av data togs.

![](../images/profile-dashboard/dashboard-timestamp.png)

## Tillgängliga widgetar

Experience Platform tillhandahåller flera widgetar som du kan använda för att visualisera olika mått som relaterar till dina profildata. Välj namnet på en widget nedan om du vill veta mer:

* [[!UICONTROL Audience size]](#audience-size)
* [[!UICONTROL Profiles by namespace]](#profiles-by-namespace)

### [!UICONTROL Audience size] {#audience-size}

Widgeten visar det totala antalet sammanfogade profiler i datalagret Profil när ögonblicksbilden togs **[!UICONTROL Audience size]** . Det här numret är resultatet av att organisationens standardpolicy för sammanfogning tillämpas på dina profildata för att sammanfoga profilfragment till en enda profil för varje enskild person.

Mer information om fragment och sammanfogade profiler får du om du börjar med att läsa [profilfragmenten eller de sammanfogade profilerna](../home.md#profile-fragments-vs-merged-profiles) i [profilöversikten](../home.md).

![](../images/profile-dashboard/audience-size.png)

### [!UICONTROL Profiles by namespace] {#profiles-by-namespace}

Widgeten visar **[!UICONTROL Profiles by namespace]** uppdelningen av namnutrymmen i alla sammanfogade profiler i din profilbutik. Det totala antalet profiler per [!UICONTROL ID namespace] (med andra ord, om du lägger ihop värdena som visas för varje namnutrymme) kommer alltid att vara högre än det totala antalet sammanfogade profiler, eftersom en profil kan ha flera namnutrymmen kopplade till sig. Om en kund till exempel interagerar med varumärket i mer än en kanal kommer flera namnutrymmen att kopplas till den enskilda kunden.

Mer information om identitetsnamnutrymmen finns i dokumentationen [för](../../identity-service/home.md)Adobe Experience Platform Identity Service.

![](../images/profile-dashboard/profiles-by-namespace.png)

## Ytterligare instrumentpaneler

Plattformsgränssnittet innehåller ytterligare instrumentpaneler för att visa ögonblicksbilder av dina data i Experience Platform. Dessa instrumentpaneler omfattar segmentering och licensanvändning. Om du vill ha mer information om dessa ytterligare instrumentpaneler väljer du bland följande länkar:

* [Kontrollpanel för segment](../../segmentation/ui/segment-dashboard.md)
* [Kontrollpanel för licensanvändning](../../landing/license-usage-dashboard.md)

## Nästa steg

Genom att följa det här dokumentet bör du nu kunna hitta kontrollpanelen Profil och förstå mätvärdena som visas i de tillgängliga widgetarna. Mer information om hur du arbetar med [!DNL Profile] data i användargränssnittet i Experience Platform finns i [[!DNL Profile] användargränssnittshandboken](user-guide.md).