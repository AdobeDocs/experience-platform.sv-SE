---
title: Pinterest målmigrering till nytt API. Kundåtgärd krävs.
description: Pinterest har ersatt v4-annonserings-API:t som används av Pinterest-målet i Real-Time CDP. Förstå era åtgärdsobjekt för att smidigt gå över till det nya API:t utan avbrott i era Pinterest-kampanjer.
hide: true
hidefromtoc: true
exl-id: c965235c-4208-4c28-9ac5-eb4c0061515d
source-git-commit: 3968c8e2a0ebd2084a7047fb41e2b85c5da7a6e7
workflow-type: tm+mt
source-wordcount: '657'
ht-degree: 0%

---

# Pinterest måluppgradering till nytt API. Kundåtgärd krävs senast 18 januari 2024.

>[!IMPORTANT]
>
>Kundens åtgärder på den här sidan gäller dig om din organisation har konfigurerat dataflöden för att exportera data till Pinterest före den 16 november 2023, det datum då den nya **[!UICONTROL Pinterest]** mål, med det senaste Pinterest-API:t, lades till i målkatalogen.

## Vad händer?

Pinterest har ersatt v4-annonserings-API:t som användes av [Pinterest destination](/help/destinations/catalog/advertising/pinterest.md) i Real-Time CDP. Adobe har uppdaterat destinationen så att den använder [API för v5-annonsering](https://developers.pinterest.com/docs/getting-started/migration/). Läs den här sidan om du vill veta mer om vad du gör för att smidigt gå över till det nya API:t utan att störa era Pinterest-kampanjer.

## Varför meddelas jag?

Vi har identifierat att din organisation har aktiva dataflöden som aktiverar målgrupper för Pinterest.

## Vad är planen?

Adobe släpper ett nytt Pinterest-målkort som utnyttjar Pinterest API v5 och bevarar dina befintliga dataflöden i den nya anslutningen.

## Behöver jag göra något för att mina aktiverade målgrupper ska fungera?

Ja, före 18 januari 2024 måste du autentisera till det nya Pinterest-målet med ditt Pinterest-annonskonto i Real-Time CDP. Se de detaljerade instruktionerna nedan.

### Återautentisera till Pinterest {#reauthenticate}

1. Gå till **[!UICONTROL Destinations > Accounts]** och använda filtret på skärmen för att filtrera Pinterest-målet.
   ![Filtrera endast Pinterest-konton](/help/destinations/assets/catalog/advertising/pinterest-migration/filter-pinterest-acconts-only.png)
2. På **Pinterest** välj symbolen för tre punkter ... och välj **[!UICONTROL Edit details]**.
   ![Välj redigeringsinformation](/help/destinations/assets/catalog/advertising/pinterest-migration/edit-details-pinterest.png)
3. Välj **[!UICONTROL Reconnect OAuth]** och logga in på ditt Pinterest-konto.
   ![Välj Koppla OAuth](/help/destinations/assets/catalog/advertising/pinterest-migration/reconnect-oauth-pinterest.png)
4. Gå vidare till åtgärdsobjektet i avsnittet nedan

### Aktivera flöden till nytt mål {#disable-old-enable-new-flows}

Sedan måste du aktivera dataflödena till det nya kortet **[!UICONTROL (New) Pinterest]**.

1. Gå till **[!UICONTROL Destinations > Browse]** och använda filtret på skärmen för att filtrera **[!UICONTROL Pinterest]** endast målet.
   ![Filtrera endast Pinterest-dataflöden på fliken Bläddra](/help/destinations/assets/catalog/advertising/pinterest-migration/filter-pinterest-browse.png)
2. Markera namnet på den hyperlänkade anslutningen (lojalitetskampanjen i skärmbildsexemplet ovan) till **[!UICONTROL Pinterest]** mål och växla **[!UICONTROL Enable]** växla till **på**.
   ![Aktivera/inaktivera för nya anslutningar och för gamla anslutningar](/help/destinations/assets/catalog/advertising/pinterest-migration/enable-disable-toggle-new-destination.png)

<!--

While no disruption to your campaigns is expected, remember to check in the Pinterest UI that everything works as expected.

-->

## Kan du dela vissa högnivåtidslinjer?

Ja, se nedan:

**Senast 16 november 2023**: Det nya målet är klart och du bör se två Pinterest-kort sida vid sida i katalogen tills Pinterest slutar stödja det gamla v4 API:t. Alla befintliga dataflöden till det aktuella Pinterest-kortet kopieras till det nya målet.

![Gammalt och nytt Pinterest-mål sida vid sida](/help/destinations/assets/catalog/advertising/pinterest-migration/pinterest-two-cards-side-by-side.png)

>[!IMPORTANT]
>
>Efter 16 november 2023 markeras det gamla Pinterest-målet **[!UICONTROL Deprecating]**. <span class="preview">Alla ändringar som du gör i dataflöden till Pinterest-destinationen (borttagen) efter den 16 november kommer att *not* överförs automatiskt till det nya Pinterest-målet. </span>
>Vi *rekommendera inte* som ni kan aktivera nya målgrupper för den gamla målgruppen efter den 16 november. Om du gör det måste du då följa [vanliga aktiveringssteg](/help/destinations/ui/activate-segment-streaming-destinations.md) för att lägga till målgruppen på den nya målplatsen när kundens åtgärder har vidtagits.

**Senast 15 december 2023**: <span class="preview">Kundåtgärd 1</span>. Du måste autentisera dig på nytt för Pinterest så att det nya kortet är anslutet till Pinterest. Visa fullständiga instruktioner i [det här avsnittet](#reauthenticate).

<span class="preview">Kundåtgärd 2</span>Du måste sedan inaktivera dataflödena till Pinterest på det gamla kortet och aktivera dataflödena på det nya kortet. Visa fullständiga instruktioner i [det här avsnittet](#disable-old-enable-new-flows).

<!--

>[!IMPORTANT]
>
>After December 15th, 2023, Adobe does not guarantee the integrity of dataflows to the old **[!UICONTROL (Deprecating) Pinterest]** destination.

-->

**Efter 18 januari 2024**: <span class="preview">Pinterest har stängt av åtkomsten till V4-annonsörens API. Alla Real-Time CDP-kunder som inte har uppgraderat till den nya destinationen kommer nu att upptäcka att dataflödena till Pinterest-destinationen inte fungerar. [Återautentisera till Pinterest](#reauthenticate) och [aktivera dataflödena](#disable-old-enable-new-flows) till den uppgraderade destinationen för att återuppta era kampanjer till Pinterest</span>.

## Övriga punkter att notera

När du har aktiverat dataflödena på det nya destinationskortet och inaktiverat dataflödena på de gamla destinationskorten, bör du inte märka några avbrott i kampanjerna eller i antalet kvalificerade profiler i de målgrupper som kommer från Adobe Real-Time CDP.
