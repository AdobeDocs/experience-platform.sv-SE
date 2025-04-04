---
title: Hantering av händelseduplicering i Experience Platform
description: Läs om hur Adobe Experience Platform hanterar händelseduplicering
exl-id: ac8c3ee8-52cf-459c-b283-16ed32d2976d
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '443'
ht-degree: 0%

---

# Hantering av händelseduplicering i Adobe Experience Platform

Adobe Experience Platform är ett distribuerat system som utformats för att maximera tillförlitligheten och samtidigt skalas till allt större datavolymer.

För datainsamling i realtid samlas [Experience Events](../xdm/classes/experienceevent.md) in via [Edge Network](../web-sdk/home.md#edge-network) från källor på klientsidan, till exempel [Web SDK](../web-sdk/home.md) eller [Mobile SDK](https://developer.adobe.com/client-sdks/home/), och levereras till Experience Platform bearbetnings- och lagringslager. Dessa lager utgör lösningar som Experience Platform, [Real-Time CDP](../rtcdp/home.md), [Customer Journey Analytics](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-overview/cja-overview.html) och [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html).

För att minimera Experience Event-förluster förväntar sig SDK:er på klientsidan och den interna Experience Platform-leveranstjänsten en bekräftelse på att en händelse har samlats in.

Om bekräftelsen inte tas emot utlöser SDK:n på klientsidan eller den interna Experience Platform-leveranstjänsten ett nytt försök och Experience Event skickas igen.

Detta är en bra metod för hantering av tillfälliga fel. Biverkningen är möjligheten att införa dubbletthändelser.

Mer information om hur du hanterar tillfälliga fel finns i den här artikeln om [tillfällig felhantering](https://learn.microsoft.com/en-us/azure/architecture/best-practices/transient-faults).

## Scenarier för händelseduplicering {#scenarios}

Händelseduplicering kan inträffa i olika scenarier, till exempel, men inte begränsat till:

* Nätverksrelaterade problem mellan SDK:er på klientsidan och [!DNL Edge Network]. Dessa problem kan bero på fel i Internet-leverantören, förlust av mobilsignaler eller andra nätverksfel, eftersom anslutningen mellan kunden och Edge Network sker via det offentliga Internet.
* Interna Experience Platform-händelser för autoskalning. Data kan ibland balanseras på nytt på grund av molninfrastrukturens instabilitet.

Adobe Experience Platform datainsamlingslager har utformats för att stödja &quot;minst en gång&quot;-bearbetning. Följaktligen kan duplicering av händelser inträffa i begränsade, sällsynta situationer.

Mer information om minst en gång-bearbetning finns i den här artikeln om [leveransgarantier](https://docs.confluent.io/kafka/design/delivery-semantics.html).

## Alternativ för deduplicering av händelser {#deduplication}

För affärsscenarier som är känsliga för duplicerade händelser använder Experience Platform flera metoder för borttagning av dubbletter i sina lagringssystem längre fram i kedjan, till exempel de som beskrivs nedan.

* Real-Time CDP Profile Store släpper händelser om det redan finns en händelse med samma `_id` i [!DNL Profile store]. Mer information finns i dokumentationen om [XDM ExperienceEvent-klassen](../xdm/classes/experienceevent.md).
* Customer Journey Analytics tillåter användare att konfigurera ett mätvärde så att endast värden räknas icke-repetitivt. Mer information om hur du gör detta finns i dokumentationen om komponentinställningarna för [metrisk deduplicering](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-dataviews/component-settings/metric-deduplication.html?lang=en).
* Experience Platform Query Service stöder datadeduplicering när det krävs att en hel rad tas bort från en beräkning eller att en viss uppsättning fält ignoreras eftersom endast en del av data i raden är dubblettinformation. Mer information finns i dokumentationen om [datadeduplicering i frågetjänsten](../query-service/key-concepts/deduplication.md).

>[!NOTE]
>
>Om du stöter på problem med duplicering av händelser utanför de användningsfall som beskrivs ovan, kontakta din Adobe-representant och lämna detaljerad information om ditt användningsfall.
