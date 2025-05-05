---
keywords: målanpassning; mål; mål för upplevelseplattform; mål för upplevelseplattform; adobe target destination;
title: Adobe Target
description: Adobe Target är en applikation som innehåller AI-baserade personaliserings- och experimenteringsfunktioner i realtid för alla inkommande kundinteraktioner på webbplatser, i mobilappar med mera.
exl-id: 3e3c405b-8add-4efb-9389-5ad695bc9799
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '1740'
ht-degree: 0%

---

# Adobe Target {#adobe-target-connection}

## Destinationsändringslogg {#changelog}

| Releasamånad | Uppdateringstyp | Beskrivning |
|---|---|---|
| April 2024 | Funktioner och dokumentation | När du ansluter till målmålet och använder ett datastream-ID behöver du *inte* för att nödvändigtvis aktivera datastream för kantsegmentering. Det innebär att måldestinationen fungerar med grupper och direktuppspelade målgrupper, även om de användningsfall som du kan uppnå skiljer sig åt. Visa tabellen i avsnittet [anslutningsparametrar](#parameters) om du vill ha mer information. |
| Januari 2024 | Funktioner och dokumentation | Nu kan du dela målgrupper och profilattribut med Adobe Target-anslutningen för standardproduktionssandlådan och andra icke-standardsandlådor. |
| Juni 2023 | Funktioner och dokumentation | Från och med juni 2023 kan du välja den Adobe Target-arbetsyta som du vill dela målgrupper med när du konfigurerar en ny Adobe Target-målanslutning. Mer information finns i avsnittet [anslutningsparametrar](#parameters). Dessutom finns självstudiekursen [Konfigurera arbetsytor](https://experienceleague.adobe.com/docs/target-learn/tutorials/administration/set-up-workspaces.html?lang=sv-SE) i Adobe Target för mer information om arbetsytor. |
| Maj 2023 | Funktioner och dokumentation | Från om med maj 2023 har anslutningen **[!UICONTROL Adobe Target]** stöd för [attributbaserad anpassning](../../ui/activate-edge-personalization-destinations.md#map-attributes) och är allmänt tillgänglig för alla kunder. |

{style="table-layout:auto"}

## Översikt {#overview}

Adobe Target är en applikation som innehåller AI-baserade personaliserings- och experimenteringsfunktioner i realtid för alla inkommande kundinteraktioner på webbplatser, i mobilappar med mera.

Adobe Target är en personaliseringsanslutning i Adobe Experience Platform destinationskatalog.

## Videoöversikt {#video-overview}

Se videon nedan för en kort översikt över hur du konfigurerar Adobe Target-anslutningen i Experience Platform.

>[!VIDEO](https://video.tv.adobe.com/v/3418799/?quality=12&learn=on)

## Användningsexempel som stöds baserat på implementeringstyp {#supported-use-cases}

Tabellen nedan visar de användningsfall som stöds för Adobe Target-destinationen, baserat på din implementeringstyp, med eller utan [Web SDK](/help/web-sdk/home.md) och med eller utan [kantsegmentering](/help/segmentation/home.md#edge) aktiverat.

| Adobe Target-implementering *utan* Web SDK | Adobe Target-implementering *med* Web SDK | Adobe Target-implementering *med* Web SDK *och* kantsegmentering inaktiverat |
|---|---|---|
| <ul><li>Datastream krävs inte. Adobe Target kan distribueras med implementeringsmetoderna [ at.js](https://experienceleague.adobe.com/docs/target-dev/developer/client-side/at-js-implementation/overview.html?lang=sv-SE), [server-side](https://experienceleague.adobe.com/docs/target-dev/developer/overview.html?lang=sv-SE#server-side-implementation) eller [hybrid](https://experienceleague.adobe.com/docs/target-dev/developer/overview.html?lang=sv-SE#hybrid-implementation).</li><li>[Edge-segmentering](../../../segmentation/methods/edge-segmentation.md) stöds inte.</li><li>[Anpassning av samma sida och nästa sida](../../ui/activate-edge-personalization-destinations.md) stöds inte.</li><li>Du kan dela målgrupper och profilattribut till Adobe Target-anslutningen för *standardproduktionssandlådan* och icke-standardsandlådor.</li><li>Använd [at.js](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/at-js/how-atjs-works.html?lang=sv-SE) om du vill konfigurera nästa sessionspersonalisering utan att använda ett datastream-ID.</li></ul> | <ul><li>Det krävs ett datastream med Adobe Target och Experience Platform konfigurerade som tjänster.</li><li>Edge segmentering fungerar som förväntat.</li><li>[Anpassning för samma sida och nästa sida](../../ui/activate-edge-personalization-destinations.md#use-cases) stöds.</li><li>Det finns stöd för att dela målgrupper och profilattribut från andra sandlådor.</li></ul> | <ul><li>Det krävs ett datastream med Adobe Target och Experience Platform konfigurerade som tjänster.</li><li>Markera inte kryssrutan **Edge-segmentering** när [dataströmmen](/help/destinations/ui/activate-edge-personalization-destinations.md#configure-datastream) konfigureras.</li><li>[Nästa sessionspersonalisering](../../ui/activate-edge-personalization-destinations.md#next-session) stöds.</li><li>Det finns stöd för att dela målgrupper och profilattribut från andra sandlådor.</li></ul> |


## Förhandskrav {#prerequisites}

### Dataström-ID {#datastream-id}

När du konfigurerar Adobe Target-anslutningen till [använd ett datastream-ID](#parameters) måste du ha [Adobe Experience Platform Web SDK](/help/web-sdk/home.md) implementerat.

Om du konfigurerar Adobe Target-anslutningen utan att använda ett datastream-ID behöver du inte implementera Web SDK.

>[!IMPORTANT]
>
>Innan du skapar en [!DNL Adobe Target]-anslutning bör du läsa guiden om hur du [konfigurerar anpassningsmål för samma sida och nästa sida ](../../ui/activate-edge-personalization-destinations.md). Den här guiden tar dig igenom de nödvändiga konfigurationsstegen för användning av samma sida och nästa sida för personalisering, i flera Experience Platform-komponenter. Om du vill använda samma sida och nästa sida som personalisering måste du använda ett datastream-ID när du konfigurerar Adobe Target-anslutningen.

### Förutsättningar i Adobe Target {#prerequisites-in-adobe-target}

I Adobe Target ska du kontrollera att din användare har:

* Åtkomst till [standardarbetsytan](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/property-channel.html?lang=sv-SE#default-workspace);
* **Godkännaren** [roll](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/property-channel.html?lang=sv-SE#roles-and-permissions).

Läs mer om att bevilja behörigheter för [Target Premium](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/properties-overview.html?lang=sv-SE#section_8C425E43E5DD4111BBFC734A2B7ABC80) och för [Target Standard](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/users/user-management.html?lang=sv-SE#roles-permissions).

## Målgrupper {#supported-audiences}

I det här avsnittet beskrivs vilka typer av målgrupper du kan exportera till det här målet.

>[!IMPORTANT]
>
>När *kantmålgrupper aktiveras för användning av samma sida och nästa sida* måste *målgrupperna* använda en [aktiv-on-edge-sammanfogningsprincip](../../../segmentation/ui/segment-builder.md#merge-policies). Sammanslagningsprincipen [!DNL active-on-edge] säkerställer att målgrupperna hela tiden utvärderas [ vid sidan ](../../../segmentation/methods/edge-segmentation.md) och är tillgängliga för personalisering i realtid och på nästa sida.  Läs om [alla tillgängliga användningsfall](#parameter), baserat på implementeringstyp.
>Om du kopplar ut målgrupper som använder en annan sammanfogningspolicy till Adobe Target-destinationer, kommer dessa målgrupper inte att utvärderas för användning i realtid och på nästa sida.
>Följ instruktionerna på [skapa en sammanfogningsprincip](../../../profile/merge-policies/ui-guide.md#create-a-merge-policy) och se till att aktivera alternativet **[!UICONTROL Active-On-Edge Merge Policy]**.


| Målgruppsursprung | Stöds | Beskrivning |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Publiker som genererats via Experience Platform [segmenteringstjänst](../../../segmentation/home.md). |
| Anpassade överföringar | X | Publikerna [importerade](../../../segmentation/ui/audience-portal.md#import-audience) till Experience Platform från CSV-filer. |

{style="table-layout:auto"}

## Exportera typ och frekvens {#export-type-frequency}

Se tabellen nedan för information om exporttyp och frekvens för destinationen.

| Objekt | Typ | Anteckningar |
|---------|----------|---------|
| Exporttyp | **[!DNL Profile request]** | Du begär alla målgrupper som är mappade i Adobe Target-målet för en enda profil. |
| Exportfrekvens | **[!UICONTROL Streaming]** | Direktuppspelningsmål är alltid på API-baserade anslutningar. Så snart en profil uppdateras i Experience Platform baserat på målgruppsutvärdering skickar anslutningsprogrammet uppdateringen nedströms till målplattformen. Läs mer om [direktuppspelningsmål](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Anslut till målet {#connect}

>[!CONTEXTUALHELP]
>id="platform_destinations_target_datastream"
>title="Om dataStream-ID"
>abstract="Det här alternativet avgör i vilket datainsamlingsdatastam som målgrupperna ska inkluderas. I den nedrullningsbara menyn visas endast datastreams som har Target-konfigurationen aktiverad. Om du vill använda kantsegmentering måste du välja ett datastream-ID. Om du väljer Ingen inaktiveras alla användningsfall där kantsegmentering används."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/personalization/adobe-target-connection.html?lang=sv-SE#parameters" text="Läs mer om att välja datastreams"

>[!IMPORTANT]
> 
>Om du vill ansluta till målet behöver du behörigheterna **[!UICONTROL View Destinations]** och **[!UICONTROL Manage Destinations]** [åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontrollsöversikten](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få den behörighet som krävs.

Om du vill ansluta till det här målet följer du stegen som beskrivs i självstudiekursen [för destinationskonfiguration](../../ui/connect-destination.md).

Adobe Experience Platform ansluter automatiskt till ert företags Adobe Target-instans. Ingen autentisering krävs.

### Anslutningsparametrar {#parameters}

>[!CONTEXTUALHELP]
>id="platform_destinations_target_workspace"
>title="Om Adobe Target Workspaces"
>abstract="Välj den Adobe Target-arbetsyta som målgrupper ska delas med. Du kan välja en arbetsyta för varje Adobe Target-anslutning. Vid aktiveringen dirigeras målgrupperna till den valda arbetsytan och följer de tillämpliga dataanvändningsetiketterna för Experience Platform."
>additional-url="https://experienceleague.adobe.com/docs/target-learn/tutorials/administration/set-up-workspaces.html?lang=sv-SE" text="Läs mer om Adobe Target arbetsytor"

När [konfigurerar](../../ui/connect-destination.md) för det här målet måste du ange följande information:

* **Namn**: Fyll i det önskade namnet för det här målet.
* **Beskrivning**: Ange en beskrivning för målet. Du kan till exempel ange vilken kampanj du använder det här målet för. Det här fältet är valfritt.
* **Datastream-ID**: Detta avgör i vilket datamängdsdatastam som målgrupperna inkluderas. I den nedrullningsbara menyn visas endast datastreams som har tjänsterna Target och Adobe Experience Platform aktiverade. Mer information om hur du konfigurerar ett datastream för Adobe Experience Platform och Adobe Target finns i [konfigurera ett datastream](../../../datastreams/configure.md#aep).

  >[!IMPORTANT]
  >
  >DataStream-ID:t är unikt för varje Adobe Target-målanslutning. Du kan inte använda samma datastream-ID för flera Adobe Target-målanslutningar.
  >Om du behöver mappa samma målgrupper till flera datastreams måste du [skapa en ny målanslutning](../../ui/connect-destination.md) för varje datastream-ID och gå igenom [målgruppsaktiveringsflödet](#activate).

   * **[!UICONTROL None]**: Välj det här alternativet om du behöver konfigurera Adobe Target-personalisering men inte kan implementera [Experience Platform Web SDK](/help/web-sdk/home.md). När du använder det här alternativet har målgrupper som exporterats från Experience Platform till Target endast stöd för nästa sessionspersonalisering, och kantsegmentering är inaktiverat. Referera tabellen i avsnittet [Användningsfall som stöds](#supported-use-cases) för en jämförelse av tillgängliga användningsfall per implementeringstyp.

  | Adobe Target-implementering *utan* Web SDK | Adobe Target-implementering *med* Web SDK | Adobe Target-implementering *med* Web SDK *och* kantsegmentering inaktiverat |
  |---|---|---|
  | <ul><li>Datastream krävs inte. Adobe Target kan distribueras med implementeringsmetoderna [ at.js](https://experienceleague.adobe.com/docs/target-dev/developer/client-side/at-js-implementation/overview.html?lang=sv-SE), [server-side](https://experienceleague.adobe.com/docs/target-dev/developer/overview.html?lang=sv-SE#server-side-implementation) eller [hybrid](https://experienceleague.adobe.com/docs/target-dev/developer/overview.html?lang=sv-SE#hybrid-implementation).</li><li>[Edge-segmentering](../../../segmentation/methods/edge-segmentation.md) stöds inte.</li><li>[Anpassning av samma sida och nästa sida](../../ui/activate-edge-personalization-destinations.md) stöds inte.</li><li>Du kan dela målgrupper och profilattribut till Adobe Target-anslutningen för *standardproduktionssandlådan* och icke-standardsandlådor.</li><li>Använd [at.js](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/at-js/how-atjs-works.html?lang=sv-SE) om du vill konfigurera nästa sessionspersonalisering utan att använda ett datastream-ID.</li></ul> | <ul><li>Det krävs ett datastream med Adobe Target och Experience Platform konfigurerade som tjänster.</li><li>Edge segmentering fungerar som förväntat.</li><li>[Anpassning för samma sida och nästa sida](../../ui/activate-edge-personalization-destinations.md#use-cases) stöds.</li><li>Det finns stöd för att dela målgrupper och profilattribut från andra sandlådor.</li></ul> | <ul><li>Det krävs ett datastream med Adobe Target och Experience Platform konfigurerade som tjänster.</li><li>Markera inte kryssrutan **Edge-segmentering** när [dataströmmen](/help/destinations/ui/activate-edge-personalization-destinations.md#configure-datastream) konfigureras.</li><li>[Nästa sessionspersonalisering](../../ui/activate-edge-personalization-destinations.md#next-session) stöds.</li><li>Det finns stöd för att dela målgrupper och profilattribut från andra sandlådor.</li></ul> |

* **Workspace**: Markera Adobe Target [arbetsyta](https://experienceleague.adobe.com/docs/target-learn/tutorials/administration/set-up-workspaces.html?lang=sv-SE) som målgrupper ska delas med. Du kan välja en arbetsyta för varje Adobe Target-anslutning. Vid aktivering dirigeras målgrupper till den valda arbetsytan enligt de tillämpliga [Experience Platform-etiketterna för dataanvändning](../../../data-governance/labels/overview.md).

>[!NOTE]
>
>När du använder en anpassad målarbetsyta för [anpassning av samma sida och nästa sida med attribut](../../ui/activate-edge-personalization-destinations.md), skickas endast de [valda målgrupperna](../../ui/activate-edge-personalization-destinations.md#select-audiences) till den valda målarbetsytan. De [mappade attributen](../../ui/activate-edge-personalization-destinations.md#mapping) skickas till standardmålarbetsytan.
><br>
>Detta beteende ändras i en framtida uppdatering.

### Aktivera aviseringar {#enable-alerts}

Du kan aktivera varningar för att få meddelanden om dataflödets status till ditt mål. Välj en avisering i listan om du vill prenumerera och få meddelanden om statusen för ditt dataflöde. Mer information om varningar finns i guiden [prenumerera på destinationsvarningar med användargränssnittet](../../ui/alerts.md).

Välj **[!UICONTROL Next]** när du är klar med att ange information för målanslutningen.

## Aktivera målgrupper till det här målet {#activate}

>[!IMPORTANT]
> 
>För att aktivera data behöver du behörigheterna **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** och **[!UICONTROL View Segments]** [åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontrollsöversikten](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få den behörighet som krävs.

Läs [Aktivera målgrupper för att anpassa målgrupper](../../ui/activate-edge-personalization-destinations.md) om du vill ha instruktioner om hur du aktiverar målgrupper till det här målet.

## Ta bort målgrupper från ett målmål {#remove}

Det krävs extra steg för att ta bort en målgrupp från en befintlig Adobe Target-anslutning när målgruppen redan används i en Adobe Target [aktivitet](https://experienceleague.adobe.com/sv/docs/target/using/activities/activities). Om du försöker ta bort en målgrupp från en Adobe Target-anslutning uppstår ett fel om målgruppen används av en Adobe Target-aktivitet.

![Experience Platform-gränssnittsbild visar ett fel som orsakats av ett försök att ta bort en målgrupp som används av en Target-aktivitet.](../../assets/catalog/personalization/adobe-target-connection/remove-audience-error.png)

Om du vill ta bort en målgrupp från ett målmål när målgruppen används i en aktivitet måste du först ta bort målgruppen från den målaktivitet som använder den, eller ta bort aktiviteten helt och hållet. Sedan kan du ta bort målgruppen från din Target-anslutning.

Om målgruppen inte används i en aktivitet går du till **[!UICONTROL Destinations]** > **[!UICONTROL Browse]** > **[!UICONTROL Select destination dataflow]** > **[!UICONTROL Activation data]**, markerar de målgrupper som du vill ta bort och väljer sedan **[!UICONTROL Remove audiences]**.

## Exporterade data {#exported-data}

Adobe Target *läser* profildata från Adobe Experience Platform Edge Network, så inga data exporteras.

## Dataanvändning och styrning {#data-usage-governance}

Alla [!DNL Adobe Experience Platform]-mål är kompatibla med dataanvändningsprinciper när data hanteras. Mer information om hur [!DNL Adobe Experience Platform] använder datastyrning finns i [Översikt över datastyrning](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=sv-SE).
