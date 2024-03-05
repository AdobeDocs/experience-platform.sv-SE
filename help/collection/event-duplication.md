---
title: Hantering av händelseduplicering i Experience Platform
description: Läs om hur Adobe Experience Platform hanterar händelseduplicering
source-git-commit: bc3ae849bd7fd8a9f50ba98528adc43d7282df90
workflow-type: tm+mt
source-wordcount: '442'
ht-degree: 0%

---


# Hantering av händelseduplicering i Adobe Experience Platform

Adobe Experience Platform är ett distribuerat system som utformats för att maximera tillförlitligheten och samtidigt skalas till allt större datavolymer.

För datainsamling i realtid [Experience Events](../xdm/classes/experienceevent.md) samlas in via [Edge Network](../web-sdk/home.md#edge-network)från källor på klientsidan, som [Web SDK](../web-sdk/home.md) eller [Mobile SDK](https://developer.adobe.com/client-sdks/home/)och levereras till Experience Platform och lager för bearbetning och lagring. Dessa lager utgör lösningar som Experience Platform, [Real-Time CDP](../rtcdp/home.md), [Customer Journey Analytics](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-overview/cja-overview.html)och [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html).

För att minimera Experience Event-förluster förväntar sig SDK:er på klientsidan och den interna Experience Platform-leveranstjänsten en bekräftelse på att en händelse har samlats in.

Om den bekräftelsen inte tas emot utlöser SDK:n på klientsidan eller den interna plattformsleveranstjänsten ett nytt försök och Experience Event skickas igen.

Detta är en bra metod för hantering av tillfälliga fel. Biverkningen är möjligheten att införa dubbletthändelser.

Mer information om hur du hanterar tillfälliga fel finns i den här artikeln om [tillfällig felhantering](https://learn.microsoft.com/en-us/azure/architecture/best-practices/transient-faults).

## Scenarier för händelseduplicering {#scenarios}

Händelseduplicering kan inträffa i olika scenarier, till exempel, men inte begränsat till:

* Nätverksrelaterade problem mellan SDK:er på klientsidan och [!DNL Edge Network]. Dessa problem kan bero på fel i Internet-leverantören, förlust av mobilsignaler eller andra nätverksfel eftersom anslutningen mellan kunden och Edge Network görs via det offentliga Internet.
* Interna Experience Platform-händelser för autoskalning. Data kan ibland balanseras på nytt på grund av molninfrastrukturens instabilitet.

Adobe Experience Platform datainsamlingslager har utformats för att stödja &quot;minst en gång&quot;-bearbetning. Följaktligen kan duplicering av händelser inträffa i begränsade, sällsynta situationer.

Mer information om &quot;minst en gång&quot;-bearbetning finns i den här artikeln om [leveransgarantier](https://docs.confluent.io/kafka/design/delivery-semantics.html).

## Alternativ för deduplicering av händelser {#deduplication}

För affärsscenarier som är känsliga för duplicerade händelser använder Experience Platform flera metoder för borttagning av dubbletter i sina lagringssystem längre fram i kedjan, till exempel de som beskrivs nedan.

* Real-Time CDP Profile Store släpper händelser om en händelse med samma `_id` finns redan i [!DNL Profile Store]. Läs dokumentationen om [Klassen XDM ExperienceEvent](../xdm/classes/experienceevent.md) för mer information.
* Customer Journey Analytics tillåter användare att konfigurera ett mätvärde så att endast värden räknas icke-repetitivt. Om du vill veta hur du gör det läser du i dokumentationen om [komponentinställningar för metrisk deduplicering](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-dataviews/component-settings/metric-deduplication.html?lang=en).
* Experience Platform Query Service stöder datadeduplicering när det krävs att en hel rad tas bort från en beräkning eller att en viss uppsättning fält ignoreras eftersom endast en del av data i raden är dubblettinformation. Läs dokumentationen om [datadeduplicering i frågetjänsten](../query-service/key-concepts/deduplication.md) för mer information.

>[!NOTE]
>
>Om du stöter på problem med händelseduplicering utanför de användningsfall som beskrivs ovan, kontakta din Adobe-representant och lämna detaljerad information om ditt användningsfall.