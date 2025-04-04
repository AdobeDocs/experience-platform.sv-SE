---
keywords: tillägg för händelsevidarebefordring;blandpanel;tillägg för händelsesändning med mixpanel
title: API-tillägg för händelsespårning i Mixpanel Track
description: Detta Adobe Experience Platform-tillägg för händelsevidarebefordran skickar Edge Network-händelser till Mixpanel.
last-substantial-update: 2023-03-29T00:00:00Z
exl-id: 21e2e0fa-4949-4be4-859f-d449d21d8f41
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '869'
ht-degree: 0%

---

# API-händelsevidarebefordringstillägg för [!DNL Mixpanel Track Events]

[[!DNL Mixpanel]](https://www.mixpanel.com) är ett produktanalysverktyg som gör att du kan samla in data om hur användare interagerar med en digital produkt. Du kan analysera produktdata med enkla, interaktiva rapporter där du kan ställa frågor och visualisera data med bara några klick. [!DNL Mixpanel] har utformats för att göra team mer effektiva genom att låta alla analysera användardata i realtid för att identifiera trender, förstå användarbeteende och fatta beslut om din produkt.

[!DNL Mixpanel] använder en händelsebaserad, användarcentrerad modell som kopplar varje interaktion till en enskild användare. Datamodellen [!DNL Mixpanel] bygger på begreppen användare, händelser och egenskaper.

>[!NOTE]
>
>Läs [!DNL Mixpanel]-dokumentationen om [identitetshantering](https://help.mixpanel.com/hc/en-us/articles/360041039771-Getting-Started-with-Identity-Management) om du vill veta hur [!DNL Mixpanel] sammanfogar händelser för att skapa identitetskluster. Vi rekommenderar också att du granskar dokumentet på [distinkta ID:n](https://help.mixpanel.com/hc/en-us/articles/115004509426-Distinct-ID-Creation-JavaScript-iOS-Android-) för att förstå hur de används för att identifiera användare i händelsedata.

## Användningsfall

Det här tillägget bör användas om du vill använda data från Edge Network i [!DNL Mixpanel] för att utnyttja produktanalysfunktionerna.

Ta till exempel en detaljhandelsorganisation som har en flerkanalsnärvaro (webbplats och mobil). Organisationen hämtar transaktions- eller konverteringsdata som händelsedata från sina plattformar och läser in dem till [!DNL Mixpanel] med hjälp av tillägget för händelsevidarebefordran.

Analysteamen kan sedan utnyttja [!DNL Mixpanel's]-funktioner för att bearbeta datauppsättningarna och få affärsinsikter, som kan användas för att generera diagram, instrumentpaneler eller andra visualiseringar för att informera affärsintressenter.

Mer information om användningsfall som är specifika för [!DNL Mixpanel] finns i följande dokumentation:

* [Ny i [!DNL Mixpanel]](https://docs.mixpanel.com/docs)
* [Vad är  [!DNL Mixpanel]?](https://developer.mixpanel.com/docs)
* [12 must-try [!DNL Mixpanel] features](https://mixpanel.com/blog/12-things-you-probably-didnt-know-you-could-do-with-mixpanel/)

## Krav för [!DNL Mixpanel] {#prerequisites-mixpanel}

Du måste ha ett giltigt [!DNL Mixpanel]-konto för att kunna använda det här tillägget. Gå till registreringssidan [[!DNL Mixpanel] för att registrera dig och skapa ett konto om du inte redan har ett.](https://mixpanel.com/register/)

Kontrollera att inställningen [[!DNL Identity Merge]](https://help.mixpanel.com/hc/en-us/articles/9648680824852-ID-Merge-Implementation-Best-Practices) är aktiverad för ditt projekt. Navigera till **[!DNL Settings]** > **[!DNL Project Setting]** > **[!DNL Identity Merge]** och växla inställningen.

### Identitetskluster i [!DNL Mixpanel]

I [!DNL Mixpanel] innehåller ett identitetskluster en samling `distinct_id`-värden som ansluter till en enskild användare. [!DNL Mixpanel] hanterar klustret med identiteter för varje användare och löser en enkel kanoniskt `distinct_id` från varje kluster som ska användas för rapportering. Du kan även inkludera din egen identifierare (kallas lokal `distinct_id`) för anonyma händelser som inträffar före en användaridentifieringshändelse.

[!DNL Mixpanel] löser identitetskluster på två sätt:

* **Identifiera** : [!DNL Mixpanel] ansluter den valda identifieraren till en anonym `distinct_id`. Om [!DNL Mixpanel] SDK är aktiverat på webbplatsen använder Experience Platform `distinct_id` som tilldelats den användare som är inloggad.
* **Alias**: [!DNL Mixpanel] kombinerar två icke-anonyma `distinct id` om ytterligare villkor för sammanslagning uppfylls.

>[!NOTE]
>
>Mer information om de här metoderna finns i [!DNL Mixpanel]-dokumentet om [identitetshantering](https://help.mixpanel.com/hc/en-us/articles/360041039771-Getting-Started-with-Identity-Management#user-identification).
>
>Bekräfta att du har aktiverat funktionen [[!DNL Mixpanel] för identitetskoppling](#prerequisites-mixpanel) för att se till att identitetskluster löses korrekt.

### Samla nödvändig konfigurationsinformation {#configuration-details}

För att kunna ansluta Experience Platform till [!DNL Mixpanel] måste du ha följande indata:

| Nyckeltyp | Beskrivning | Exempel |
| --- | --- | --- |
| Projekttoken | Projekttoken som är associerad med ditt [!DNL Mixpanel]-konto. Mer information finns i [!DNL Mixpanel]-dokumentationen om att [hitta din projekttoken](https://help.mixpanel.com/hc/en-us/articles/115004502806-Find-Project-Token-). | `25470xxxxxxxxxxxxxxxxxxx1289` |

## Installera och konfigurera tillägget [!DNL Mixpanel] {#install}

Om du vill installera tillägget [skapar du en egenskap för vidarebefordring av händelser](../../../ui/event-forwarding/overview.md#properties) eller väljer en befintlig egenskap att redigera i stället.

Välj **[!UICONTROL Extensions]** i den vänstra navigeringen. På fliken **[!UICONTROL Catalog]** väljer du **[!UICONTROL Install]** på kortet för tillägget [!DNL Mixpanel].

![Installerar tillägget [!DNL Mixpanel].](../../../images/extensions/server/mixpanel/install-extension.png)

## Skapa en [!DNL Send Event]-regel

Börja skapa en ny regel i egenskapen för vidarebefordran av händelser. Under **[!UICONTROL Actions]** lägger du till en ny åtgärd och anger tillägget till **[!UICONTROL Mixpanel]**. Ange sedan åtgärdstypen till **[!UICONTROL Track Event]** för att skicka Edge Network-händelser till [!DNL Mixpanel].

| Indata | Beskrivning | Obligatoriskt |
| --- | --- | --- |
| [!UICONTROL Project Token] | Det här fältet ska mappas till den projekttoken som är associerad med ditt [!DNL Mixpanel]-konto. | Ja |
| [!UICONTROL Event Type] | Händelsens namn. | Ja |
| [!UICONTROL Event Time] | Händelsens tid. | |
| [!UICONTROL Mixpanel Distinct ID] | Den unika identifieraren för användaren som utförde händelsen. | |
| [!UICONTROL Insert ID] | En unik identifierare för händelsen som används för borttagning av dubbletter. | |
| [!UICONTROL Event Properties] | Ett JSON-objekt som innehåller anpassade egenskaper för händelsen. Välj mellan att tillhandahålla rå JSON eller att använda en förenklad uppsättning indata för nyckelvärden. | |

>[!NOTE]
>
>Mer information om standardfälten för en [!DNL Mixpanel]-händelse finns i den [officiella dokumentationen](https://developer.mixpanel.com/reference/import-events#event).

![Lägg till en åtgärdskonfiguration för händelsevidarebefordringsregel.](../../../images/extensions/server/mixpanel/track-event-action.png)

När åtgärden [!UICONTROL Track Event] har lagts till i regeln kan du konfigurera regelns villkor så att den bara aktiveras för vissa händelser. Du kan också lämna villkorsavsnittet tomt så att regeln aktiveras för alla händelser.

>[!IMPORTANT]
>
>Om din webbplats använder SDK [!DNL Mixpanel] kan du fortsätta till nästa steg i [valideringen av dina data inom [!DNL Mixpanel]](#validate). Om du inte använder [!DNL Mixpanel] SDK måste du [skapa en separat regel för identitetsspårning](#create-an-identity-tracking-rule) för att säkerställa att lämpliga händelser och `distinct_id` värden skickas till [!DNL Mixpanel] när en användaridentifieringshändelse inträffar.

## Validera data i [!DNL Mixpanel] {#validate}

Om implementeringen lyckas och händelser samlas in visas händelser i [[!DNL Mixpanel] konsolen](https://help.mixpanel.com/hc/en-us/articles/4402837164948).

Kontrollera om [!DNL Mixpanel] har sammanfogat händelserna efter inloggning med e-postvärden och händelserna som skapades när **[!UICONTROL Send Event]** användes. Om den implementeras korrekt associerar [!DNL Mixpanel] dem med en enda [användarprofil](https://help.mixpanel.com/hc/en-us/articles/115004501966).

## Nästa steg

I den här guiden beskrivs hur du skickar konverteringshändelser till [!DNL Mixpanel] med hjälp av händelsevidarebefordran. Det här tillägget för vidarebefordran av händelser utnyttjar SDK- och JavaScript-API:t [!DNL Mixpanel]. Mer information om dessa underliggande tekniker finns i den officiella dokumentationen:

* [[!DNL Mixpanel] SDK](https://developer.mixpanel.com/docs/nodejs)
* [[!DNL Mixpanel] JavaScript API](https://developer.mixpanel.com/docs/javascript-full-api-reference#mixpanelidentify)

Mer information om funktioner för vidarebefordran av händelser i Experience Platform finns i [översikten över vidarebefordran av händelser](../../../ui/event-forwarding/overview.md).
