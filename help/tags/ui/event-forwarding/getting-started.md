---
title: Komma igång med händelsevidarebefordran
description: Följ den här steg-för-steg-självstudiekursen för att komma igång med att vidarebefordra event i Adobe Experience Platform.
feature: Event Forwarding
exl-id: f82bfac9-dc2d-44de-a308-651300f107df
source-git-commit: 45d881a810782f734ed030fbf29e802fa535400a
workflow-type: tm+mt
source-wordcount: '830'
ht-degree: 1%

---

# Komma igång med händelsevidarebefordran

>[!NOTE]
>
>Adobe Experience Platform Launch har omklassificerats som en serie datainsamlingstekniker i Adobe Experience Platform. Som ett resultat av detta har flera terminologiska förändringar införts i produktdokumentationen. Se följande [dokument](../../term-updates.md) för en konsoliderad hänvisning till terminologiska förändringar.

Om du vill använda händelsevidarebefordran i Adobe Experience Platform måste data skickas till Adobe Experience Platform Edge Network med ett eller flera av följande tre alternativ:

* [Webb-SDK för Adobe Experience Platform](../../extensions/client/web-sdk/overview.md)
* [Adobe Experience Platform Mobile SDK](https://sdkdocs.com)
* [Server till server-API](/help/server-api/overview.md)

>[!NOTE]
>Platform Web SDK och Platform Mobile SDK kräver inte distribution via taggar i Adobe Experience Platform. Vi rekommenderar dock att du använder taggar för att distribuera dessa SDK:er.

När du har skickat data till Edge-nätverket kan du aktivera Adobe-lösningar för att skicka data dit. Om du vill skicka data till en icke-Adobe-lösning anger du den i händelsevidarebefordran.

## Förutsättningar

* Adobe Real-Time CDP Connections, Prime, or Ultimate (kontakta ditt Adobe-kontoteam för att få priser)
* Vidarebefordran av händelser i Adobe Experience Platform
* Adobe Experience Platform Web SDK, Mobile SDK eller Edge Network Server API har konfigurerats för att skicka data till Edge Network
* Mappa data till Experience Data Model (XDM) (Den här mappningen kan göras med taggar)

## Skapa ett XDM-schema

Skapa ditt schema i Adobe Experience Platform.

1. Skapa ett schema genom att välja **[!UICONTROL Schemas]**>**[!UICONTROL Create Schema]** och välja **[!UICONTROL XDM ExperienceEvent]** alternativ.

1. Ge schemat ett namn och en kort beskrivning.

1. Du kan lägga till fältgruppen&quot;ExperienceEvent-webbinformation&quot; genom att välja **[!UICONTROL Add]** nästa **[!UICONTROL Field Groups]**.

   >[!NOTE]
   >
   >Om du vill kan du lägga till flera fältgrupper.

1. Spara schemat och notera namnet som du gav det.

Mer information om scheman finns i [Experience Data Model (XDM) - systemhjälp](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=sv).

## Skapa en egenskap för vidarebefordring av händelser

I **[!UICONTROL Tags]** arbetsyta, skapa en egenskap av typen **[!UICONTROL Edge]**.

1. Välj **[!UICONTROL New Property]**.

1. Namnge egenskapen.

1. Välj plattformstypen&quot;Edge&quot;.

1. Välj **[!UICONTROL Save]**.

När du har skapat egenskapen går du till **[!UICONTROL Environments]** för den nya egenskapen och notera miljö-ID:n. Om den Adobe-organisation som används i datastream skiljer sig från den Adobe-organisation som används vid vidarebefordran av händelser, kan du kopiera miljö-ID:t från **[!UICONTROL Environments]** och klistra in den när du skapar ett datastream. I annat fall kan du välja miljö i en listruta.

## Skapa ett datastream

Om du vill skapa ett dataflöde i Adobe Experience Platform använder du det miljö-ID som genererades när du skapade egenskapen för vidarebefordran av händelser.

1. Välj **[!UICONTROL Datastreams]** i den vänstra navigeringen.

1. Ge konfigurationen ett namn och ange en valfri beskrivning.
Beskrivningen hjälper till att identifiera konfigurationer i en lista med flera konfigurationer.

1. Välj **[!UICONTROL Save]**.

## Aktivera vidarebefordran av händelser

Konfigurera sedan Edge Network för att skicka data till händelsevidarebefordran och till andra Adobe-produkter.

1. I **[!UICONTROL Datastreams]** markerar du den egenskap du skapade.

1. Välj utvecklingsmiljö, produktionsmiljö eller mellanlagringsmiljö.

   Om du vill skicka data till en händelsevidarebefordringsmiljö utanför Adobe-organisationen väljer du **[!UICONTROL Switch to Advanced Mode]** och klistra in ett ID. ID:t anges när du skapar en egenskap för vidarebefordring av händelser.

1. Växla mellan nödvändiga verktyg och konfigurera efter behov.

   * Adobe Analytics kräver ett rapportsvit-ID.

   * Händelsevidarebefordran i Adobe Experience Platform kräver ett egenskaps-ID och ett miljö-ID. Det här är publiceringssökvägen för egenskapen för vidarebefordran av händelse.

Observera miljö-ID:n för den nya egenskapen när du har konfigurerat den.

## Konfigurera Platform Web SDK-tillägget för att skicka data till dataströmmen som skapats tidigare

Skapa din egenskap i dialogrutan **[!UICONTROL Tags]** arbetsyta och sedan navigera till **[!UICONTROL Extensions]** och välj tillägget Experience Platform Web SDK i katalogen för att konfigurera och installera det.

Se [Dokumentation för Web SDK-tillägg](../../extensions/client/web-sdk/overview.md) för mer information om konfigurationsalternativ.

## Skapa en taggregel för att skicka data till Platform Web SDK

När ovanstående är på plats kan du skapa datadefinitioner, regler och så vidare, som använder händelsevidarebefordran och taggar, men som bara behöver en enda begäran från sidan.

Skapa en sidinläsningsregel med hjälp av plattformens SDK-tillägg och åtgärdstypen &quot;Skicka händelse&quot;:

1. Öppna **[!UICONTROL Rules]** tabbtangenten och sedan välja **[!UICONTROL Create New Rule]**.

1. Namnge regeln.

1. Välj **[!UICONTROL Events Add]**.

1. Lägg till en händelse genom att välja ett tillägg och en av de händelsetyper som är tillgängliga för tillägget och konfigurera sedan inställningarna för händelsen. Välj till exempel **[!UICONTROL Core - Window Loaded]**.

1. Lägg till en åtgärd med plattformens SDK-tillägg. Välj **[!UICONTROL Send Event]** från **[!UICONTROL Action Type]** markerar du önskad instans (Alloy-instans konfigurerad tidigare) och väljer sedan ett dataelement som ska läggas till i XDM-datablocket i Alloy-träffen.

1. Lämna resten av inställningarna som standard för det här exemplet och välj **[!UICONTROL Save]**.

Du kan till exempel skapa en regel som skickar datalagret till Edge om användaren hovrar över en angiven knapp.

## Sammanfattning

Med följande på plats kan du nu skapa regler för vidarebefordran av händelser för att vidarebefordra data till destinationer utanför Adobe.

* Experience Data Model-schema (observera namnet som du gav det).
* En egenskap för vidarebefordran av händelser (håll reda på egenskaps-ID och miljö-ID:n.)
* En datastream (Observera att miljö-ID inte ska blandas ihop med miljö-ID:t från händelsevidarebefordran.)
* En taggegenskap
