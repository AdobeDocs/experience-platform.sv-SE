---
keywords: målinriktad personalisering, destination, mål för upplevelseplattform;adobe target destination;
title: Adobe Target-anslutning
description: Adobe Target är en applikation som innehåller AI-baserade personaliserings- och experimenteringsfunktioner i realtid för alla inkommande kundinteraktioner på webbplatser, i mobilappar med mera.
exl-id: 3e3c405b-8add-4efb-9389-5ad695bc9799
source-git-commit: 46e732dfc630ad1875a57289a6e6cf9c964b9547
workflow-type: tm+mt
source-wordcount: '740'
ht-degree: 0%

---

# Adobe Target-anslutning {#adobe-target-connection}

## Översikt {#overview}

Adobe Target är en applikation som innehåller AI-baserade personaliserings- och experimenteringsfunktioner i realtid för alla inkommande kundinteraktioner på webbplatser, i mobilappar med mera.

Adobe Target är en personaliseringsanslutning i Adobe Experience Platform.

## Förutsättningar {#prerequisites}

När Adobe Target-anslutningen konfigureras till [använd ett datastream-ID](#parameters)måste du ha [Adobe Experience Platform Web SDK](../../../edge/home.md) implementerat.

Om du konfigurerar Adobe Target-anslutningen utan att använda ett datastream-ID behöver du inte implementera Web SDK.

>[!IMPORTANT]
>
>Innan du skapar en [!DNL Adobe Target] anslutning, läs guiden om hur man [konfigurera anpassningsmål för personalisering på samma sida och nästa sida](../../ui/configure-personalization-destinations.md). Den här guiden tar dig igenom de nödvändiga konfigurationsstegen för användning av samma sida och nästa sida för personalisering, i flera Experience Platform-komponenter. För personalisering på samma sida och nästa sida krävs att du använder ett dataström-ID när du konfigurerar Adobe Target-anslutningen.

## Exportera typ och frekvens {#export-type-frequency}

Se tabellen nedan för information om exporttyp och frekvens för destinationen.

| Objekt | Typ | Anteckningar |
---------|----------|---------|
| Exporttyp | **[!DNL Profile request]** | Du begär alla segment som är mappade i Adobe Target-målet för en enskild profil. |
| Exportfrekvens | **[!UICONTROL Streaming]** | Direktuppspelningsmål är alltid på API-baserade anslutningar. Så snart en profil uppdateras i Experience Platform baserat på segmentutvärdering skickar kopplingen uppdateringen nedåt till målplattformen. Läs mer om [mål för direktuppspelning](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## Användningsfall {#use-cases}

**Anpassa en startsidesbanderoll**

Ett uthyrnings- och säljföretag vill skräddarsy sin hemsida med en banderoll som bygger på kundsegmentets kvalifikationer i Adobe Experience Platform. Företaget kan välja vilka målgrupper som ska få en personaliserad upplevelse och skicka dem till Adobe Target som målinriktningskriterier för sitt Target-erbjudande.

## Anslut till målet {#connect}

>[!CONTEXTUALHELP]
>id="platform_destinations_target_datastream"
>title="Om dataStream-ID"
>abstract="Det här alternativet avgör i vilket datainsamlingsdatastam segmenten inkluderas. I den nedrullningsbara menyn visas endast datastreams som har Target-konfigurationen aktiverad. Om du vill använda kantsegmentering måste du välja ett datastream-ID. Om du väljer Ingen inaktiveras alla användningsfall där kantsegmentering används."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/personalization/adobe-target-connection.html#parameters" text="Läs mer om att välja datastreams"

>[!IMPORTANT]
> 
>Om du vill ansluta till målet behöver du **[!UICONTROL Manage Destinations]** [åtkomstkontrollbehörighet](/help/access-control/home.md#permissions). Läs [åtkomstkontroll - översikt](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få de behörigheter som krävs.

Om du vill ansluta till det här målet följer du stegen som beskrivs i [självstudiekurs om destinationskonfiguration](../../ui/connect-destination.md).

Adobe Experience Platform ansluter automatiskt till ert företags Adobe Target-instans. Ingen autentisering krävs.

### Anslutningsparametrar {#parameters}

while [konfigurera](../../ui/connect-destination.md) Om du vill ange destinationen måste du ange följande information:

* **Namn**: Fyll i det önskade namnet för det här målet.
* **Beskrivning**: Ange en beskrivning för destinationen. Du kan till exempel ange vilken kampanj du använder det här målet för. Det här fältet är valfritt.
* **Datastream-ID**: Detta anger i vilken datainsamling som segmenten ska inkluderas. I den nedrullningsbara menyn visas endast datastreams som har målmålet aktiverat. Se [konfigurera ett datastream](../../../edge/datastreams/overview.md#target) om du vill ha mer information om hur du konfigurerar ett datastam för Adobe Target.
   * **[!UICONTROL None]**: Välj det här alternativet om du behöver konfigurera Adobe Target-personalisering men inte kan implementera [Experience Platform Web SDK](../../../edge/home.md). När du använder det här alternativet har segment som exporterats från Experience Platform till Target endast stöd för anpassning efter nästa session, och kantsegmentering är inaktiverat. Se tabellen nedan för mer information.

| Ingen datastream har valts | Datastream har valts |
|---|---|
| <ul><li>[Kantsegmentering](../../../segmentation/ui/edge-segmentation.md) stöds inte.</li><li>[Personalisering på samma sida och nästa sida](../../ui/configure-personalization-destinations.md) stöds inte.</li><li>Du kan bara dela segment till Adobe Target-anslutningen för produktionssandlådan.</li><li>Om du vill konfigurera nästa sessionspersonalisering utan att använda ett datastream-ID använder du [at.js](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/at-js/how-atjs-works.html?lang=en).</li></ul> | <ul><li>Kantsegmentering fungerar som förväntat.</li><li>[Personalisering på samma sida och nästa sida](../../ui/configure-personalization-destinations.md) stöds.</li><li>Segmentdelning stöds för andra sandlådor.</li></ul> |

## Aktivera segment till den här destinationen {#activate}

>[!IMPORTANT]
> 
>Om du vill aktivera data måste du ha **[!UICONTROL Manage Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** och **[!UICONTROL View Segments]** [behörigheter för åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontroll - översikt](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få de behörigheter som krävs.

Läs [Aktivera profiler och segment för att profilera mål för begäran](../../ui/activate-profile-request-destinations.md) om du vill ha instruktioner om hur du aktiverar målgruppssegment till det här målet.

## Exporterade data {#exported-data}

Adobe Target läser profildata från Adobe Experience Platform Edge Network så att inga data exporteras.

## Dataanvändning och styrning {#data-usage-governance}

Alla [!DNL Adobe Experience Platform] destinationerna är kompatibla med dataanvändningsprinciper när data hanteras. Detaljerad information om hur [!DNL Adobe Experience Platform] använder datastyrning, läs [Datastyrning - översikt](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html).
