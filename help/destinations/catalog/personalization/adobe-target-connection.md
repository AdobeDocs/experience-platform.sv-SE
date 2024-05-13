---
keywords: målanpassning; mål; mål för upplevelseplattform; mål för upplevelseplattform; adobe target destination;
title: Adobe Target
description: Adobe Target är en applikation som innehåller AI-baserade personaliserings- och experimenteringsfunktioner i realtid för alla inkommande kundinteraktioner på webbplatser, i mobilappar med mera.
exl-id: 3e3c405b-8add-4efb-9389-5ad695bc9799
source-git-commit: e9777960f347e32ff6288227ef95cec9cc4c55e7
workflow-type: tm+mt
source-wordcount: '1433'
ht-degree: 1%

---

# Adobe Target {#adobe-target-connection}

## Destinationsändringslogg {#changelog}

| Releasamånad | Uppdateringstyp | Beskrivning |
|---|---|---|
| April 2024 | Funktioner och dokumentation | När du ansluter till målmålet med ett datastream-ID *behöver inte* för att nödvändigtvis aktivera datastream för kantsegmentering. Det innebär att måldestinationen fungerar med grupper och direktuppspelade målgrupper, även om de användningsfall som du kan uppnå skiljer sig åt. Visa tabellen i [anslutningsparametrar](#parameters) för mer information. |
| Januari 2024 | Funktioner och dokumentation | Nu kan du dela målgrupper och profilattribut med Adobe Target-anslutningen för standardproduktionssandlådan och andra icke-standardsandlådor. |
| Juni 2023 | Funktioner och dokumentation | Från och med juni 2023 kan du välja den Adobe Target-arbetsyta som du vill dela målgrupper med när du konfigurerar en ny Adobe Target-målanslutning. Se [anslutningsparametrar](#parameters) för mer information. Se även självstudiekursen om [konfigurera arbetsytor](https://experienceleague.adobe.com/docs/target-learn/tutorials/administration/set-up-workspaces.html) i Adobe Target om du vill ha mer information om arbetsytor. |
| Maj 2023 | Funktioner och dokumentation | Från maj 2023 **[!UICONTROL Adobe Target]** anslutningsstöd [attributbaserad personalisering](../../ui/activate-edge-personalization-destinations.md#map-attributes) och är allmänt tillgängligt för alla kunder. |

{style="table-layout:auto"}

## Översikt {#overview}

Adobe Target är en applikation som innehåller AI-baserade personaliserings- och experimenteringsfunktioner i realtid för alla inkommande kundinteraktioner på webbplatser, i mobilappar med mera.

Adobe Target är en personaliseringsanslutning i Adobe Experience Platform destinationskatalog.

## Videoöversikt {#video-overview}

Se videon nedan för en kort översikt över hur du konfigurerar Adobe Target-anslutningen i Experience Platform.

>[!VIDEO](https://video.tv.adobe.com/v/3418799/?quality=12&learn=on)

## Förutsättningar {#prerequisites}

### Dataström-ID {#datastream-id}

När Adobe Target-anslutningen konfigureras till [använd ett datastream-ID](#parameters)måste du ha [Adobe Experience Platform Web SDK](/help/web-sdk/home.md) implementerat.

Om du konfigurerar Adobe Target-anslutningen utan att använda ett datastream-ID behöver du inte implementera Web SDK.

>[!IMPORTANT]
>
>Innan du skapar [!DNL Adobe Target] anslutning, läs guiden om hur man [konfigurera anpassningsmål för personalisering på samma sida och nästa sida](../../ui/activate-edge-personalization-destinations.md). Den här guiden tar dig igenom de nödvändiga konfigurationsstegen för användning av samma sida och nästa sida för personalisering, i flera Experience Platform-komponenter. Om du vill använda samma sida och nästa sida som personalisering måste du använda ett datastream-ID när du konfigurerar Adobe Target-anslutningen.

### Förutsättningar i Adobe Target {#prerequisites-in-adobe-target}

I Adobe Target ska du kontrollera att din användare har:

* Åtkomst till [standardarbetsyta](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/property-channel.html#default-workspace);
* The **Godkännare** [roll](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/property-channel.html#roles-and-permissions).

Läs mer om att bevilja behörigheter för [Mål Premium](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/properties-overview.html#section_8C425E43E5DD4111BBFC734A2B7ABC80) och for [Målstandard](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/users/user-management.html#roles-permissions).

## Målgrupper {#supported-audiences}

I det här avsnittet beskrivs vilka typer av målgrupper du kan exportera till det här målet.

| Målgruppsursprung | Stöds | Beskrivning |
---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Målgrupper som skapats genom Experience Platform [Segmenteringstjänst](../../../segmentation/home.md). |
| Anpassade överföringar | X | Målgrupper [importerad](../../../segmentation/ui/overview.md#import-audience) till Experience Platform från CSV-filer. |

{style="table-layout:auto"}

## Exportera typ och frekvens {#export-type-frequency}

Se tabellen nedan för information om exporttyp och frekvens för destinationen.

| Objekt | Typ | Anteckningar |
---------|----------|---------|
| Exporttyp | **[!DNL Profile request]** | Du begär alla målgrupper som är mappade i Adobe Target-målet för en enda profil. |
| Exportfrekvens | **[!UICONTROL Streaming]** | Direktuppspelningsmål är alltid på API-baserade anslutningar. Så snart en profil uppdateras i Experience Platform baserat på målgruppsutvärdering skickar anslutningsprogrammet uppdateringen nedströms till målplattformen. Läs mer om [mål för direktuppspelning](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Anslut till målet {#connect}

>[!CONTEXTUALHELP]
>id="platform_destinations_target_datastream"
>title="Om dataStream-ID"
>abstract="Det här alternativet avgör i vilket datainsamlingsdatastam som målgrupperna ska inkluderas. I den nedrullningsbara menyn visas endast datastreams som har Target-konfigurationen aktiverad. Om du vill använda kantsegmentering måste du välja ett datastream-ID. Om du väljer Ingen inaktiveras alla användningsfall där kantsegmentering används."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/personalization/adobe-target-connection.html#parameters" text="Läs mer om att välja datastreams"

>[!IMPORTANT]
> 
>Om du vill ansluta till målet behöver du **[!UICONTROL View Destinations]** och **[!UICONTROL Manage Destinations]** [behörigheter för åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontroll - översikt](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få de behörigheter som krävs.

Om du vill ansluta till det här målet följer du stegen som beskrivs i [självstudiekurs om destinationskonfiguration](../../ui/connect-destination.md).

Adobe Experience Platform ansluter automatiskt till ert företags Adobe Target-instans. Ingen autentisering krävs.

### Anslutningsparametrar {#parameters}

>[!CONTEXTUALHELP]
>id="platform_destinations_target_workspace"
>title="Om Adobe Target Workspaces"
>abstract="Välj den Adobe Target-arbetsyta som målgrupper ska delas med. Du kan välja en arbetsyta för varje Adobe Target-anslutning. Vid aktiveringen dirigeras målgrupperna till den valda arbetsytan enligt Experience Platform-dataanvändningsetiketterna."
>additional-url="https://experienceleague.adobe.com/docs/target-learn/tutorials/administration/set-up-workspaces.html" text="Läs mer om Adobe Target arbetsytor"

while [konfigurera](../../ui/connect-destination.md) Om du vill ange destinationen måste du ange följande information:

* **Namn**: Fyll i det önskade namnet för det här målet.
* **Beskrivning**: Ange en beskrivning för destinationen. Du kan till exempel ange vilken kampanj du använder det här målet för. Det här fältet är valfritt.
* **Dataström-ID**: Detta avgör i vilken datainsamling som målgrupperna inkluderas. I den nedrullningsbara menyn visas endast datastreams som har tjänsterna Target och Adobe Experience Platform aktiverade. Se [konfigurera ett datastream](../../../datastreams/configure.md#aep) för detaljerad information om hur du konfigurerar ett datastam för Adobe Experience Platform och Adobe Target.

  >[!IMPORTANT]
  >
  >DataStream-ID:t är unikt för varje Adobe Target-målanslutning. Om du behöver mappa samma målgrupper till flera datastreams måste du [skapa en ny målanslutning](../../ui/connect-destination.md) för varje datastream ID och gå igenom [målgruppsaktiveringsflöde](#activate).

   * **[!UICONTROL None]**: Välj det här alternativet om du behöver konfigurera Adobe Target-personalisering men inte kan implementera [Experience Platform Web SDK](/help/web-sdk/home.md). När du använder det här alternativet har målgrupper som exporterats från Experience Platform till Target endast stöd för nästa sessionspersonalisering, och kantsegmentering är inaktiverat. Se tabellen nedan för en jämförelse av tillgängliga användningsfall per implementeringstyp.

  | Implementering av Adobe Target *utan* Web SDK | Implementering av Adobe Target *med* Web SDK | Implementering av Adobe Target *med* Web SDK *och* kantsegmentering bort |
  |---|---|---|
  | <ul><li>Datastream krävs inte. Adobe Target kan driftsättas via [at.js](https://experienceleague.adobe.com/docs/target-dev/developer/client-side/at-js-implementation/overview.html), [server-side](https://experienceleague.adobe.com/docs/target-dev/developer/overview.html#server-side-implementation), eller [hybrid](https://experienceleague.adobe.com/docs/target-dev/developer/overview.html#hybrid-implementation) implementeringsmetoder.</li><li>[Kantsegmentering](../../../segmentation/ui/edge-segmentation.md) stöds inte.</li><li>[Personalisering på samma sida och nästa sida](../../ui/activate-edge-personalization-destinations.md) stöds inte.</li><li>Du kan dela målgrupper och profilattribut med Adobe Target-anslutningen för *standardproduktionssandlåda* och icke-standardsandlådor.</li><li>Om du vill konfigurera nästa sessionspersonalisering utan att använda ett datastream-ID använder du [at.js](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/at-js/how-atjs-works.html).</li></ul> | <ul><li>Ett datastream med Adobe Target och Experience Platform konfigurerat som tjänster krävs.</li><li>Kantsegmentering fungerar som förväntat.</li><li>[Personalisering på samma sida och nästa sida](../../ui/activate-edge-personalization-destinations.md#use-cases) stöds.</li><li>Det finns stöd för att dela målgrupper och profilattribut från andra sandlådor.</li></ul> | <ul><li>Ett datastream med Adobe Target och Experience Platform konfigurerat som tjänster krävs.</li><li>När [konfigurera datastream](/help/destinations/ui/activate-edge-personalization-destinations.md#configure-datastream)markerar du inte **Kantsegmentering** kryssrutan.</li><li>[Anpassa nästa session](../../ui/activate-edge-personalization-destinations.md#next-session) stöds.</li><li>Det finns stöd för att dela målgrupper och profilattribut från andra sandlådor.</li></ul> |

* **Arbetsyta**: Välj Adobe Target [arbetsyta](https://experienceleague.adobe.com/docs/target-learn/tutorials/administration/set-up-workspaces.html) till vilka målgrupper ska delas. Du kan välja en arbetsyta för varje Adobe Target-anslutning. Vid aktivering dirigeras målgrupper till den valda arbetsytan enligt tillämpliga [Experience Platform-dataanvändningsetiketter](../../../data-governance/labels/overview.md).

>[!NOTE]
>
>När du använder en anpassad målarbetsyta för [anpassning av hela sidan och nästa sida med attribut](../../ui/activate-edge-personalization-destinations.md), bara [valda målgrupper](../../ui/activate-edge-personalization-destinations.md#select-audiences) skickas till den valda målarbetsytan. The [mappade attribut](../../ui/activate-edge-personalization-destinations.md#mapping) skickas till standardarbetsytan Mål.
><br>
>Detta beteende ändras i en framtida uppdatering.

### Aktivera aviseringar {#enable-alerts}

Du kan aktivera varningar för att få meddelanden om dataflödets status till ditt mål. Välj en avisering i listan om du vill prenumerera och få meddelanden om statusen för ditt dataflöde. Mer information om varningar finns i guiden på [prenumerera på destinationsvarningar med användargränssnittet](../../ui/alerts.md).

När du är klar med informationen för målanslutningen väljer du **[!UICONTROL Next]**.

## Aktivera målgrupper till det här målet {#activate}

>[!IMPORTANT]
> 
>För att aktivera data behöver du **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** och **[!UICONTROL View Segments]** [behörigheter för åtkomstkontroll](/help/access-control/home.md#permissions). Läs [åtkomstkontroll - översikt](/help/access-control/ui/overview.md) eller kontakta produktadministratören för att få de behörigheter som krävs.

Läs [Aktivera målgrupper för att kanalisera personaliseringsmål](../../ui/activate-edge-personalization-destinations.md) för instruktioner om hur du aktiverar målgrupper till det här målet.

## Ta bort målgrupper från ett målmål {#remove}

Det krävs ytterligare steg för att ta bort en målgrupp från en befintlig Adobe Target-anslutning när målgruppen redan används i en Adobe Target [aktivitet](https://experienceleague.adobe.com/en/docs/target/using/activities/activities). Om du försöker ta bort en målgrupp från en Adobe Target-anslutning uppstår ett fel om målgruppen används av en Adobe Target-aktivitet.

![Bild på användargränssnittet för plattformen visar ett fel som orsakats av ett försök att ta bort en målgrupp som används av en målaktivitet.](../../assets/catalog/personalization/adobe-target-connection/remove-audience-error.png)

Om du vill ta bort en målgrupp från ett målmål när målgruppen används i en aktivitet måste du först ta bort målgruppen från den målaktivitet som använder den, eller ta bort aktiviteten helt och hållet. Sedan kan du ta bort målgruppen från din Target-anslutning.

Om målgruppen inte används i en aktivitet går du till **[!UICONTROL Destinations]** > **[!UICONTROL Browse]** > **[!UICONTROL Select destination dataflow]** > **[!UICONTROL Activation data]**, väljer de målgrupper som du vill ta bort och väljer sedan **[!UICONTROL Remove audiences]**.

## Exporterade data {#exported-data}

Adobe Target *läsningar* profildata från Adobe Experience Platform Edge Network, så att inga data exporteras.

## Dataanvändning och styrning {#data-usage-governance}

Alla [!DNL Adobe Experience Platform] destinationerna är kompatibla med dataanvändningsprinciper när data hanteras. Detaljerad information om hur [!DNL Adobe Experience Platform] använder datastyrning, läs [Datastyrning - översikt](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html).
