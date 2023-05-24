---
keywords: tillägg för händelsevidarebefordring;blandpanel;tillägg för händelsesändning med mixpanel
title: API-tillägg för händelsespårning i Mixpanel Track
description: Detta Adobe Experience Platform-tillägg för händelsevidarebefordran skickar Adobe Experience Edge Network-händelser till Mixpanel.
last-substantial-update: 2023-03-29T00:00:00Z
exl-id: 21e2e0fa-4949-4be4-859f-d449d21d8f41
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '929'
ht-degree: 1%

---

# [!DNL Mixpanel Track Events] API-händelsevidarebefordringstillägg

[[!DNL Mixpanel]](https://www.mixpanel.com) är ett verktyg för produktanalys som gör det möjligt att samla in data om hur användarna interagerar med en digital produkt. Du kan analysera produktdata med enkla, interaktiva rapporter där du kan ställa frågor och visualisera data med bara några klick. [!DNL Mixpanel] har utformats för att göra teamen mer effektiva genom att låta alla analysera användardata i realtid för att identifiera trender, förstå användarbeteende och fatta beslut om produkten.

[!DNL Mixpanel] använder en händelsebaserad, användarcentrerad modell som kopplar varje interaktion till en enskild användare. The [!DNL Mixpanel] datamodellen bygger på begreppen användare, händelser och egenskaper.

>[!NOTE]
>
>Se [!DNL Mixpanel] dokumentation om [identitetshantering](https://help.mixpanel.com/hc/en-us/articles/360041039771-Getting-Started-with-Identity-Management) för att förstå hur [!DNL Mixpanel] sammanfogar händelser för att skapa identitetskluster. Vi rekommenderar även att du granskar dokumentet på [distinkta ID:n](https://help.mixpanel.com/hc/en-us/articles/115004509426-Distinct-ID-Creation-JavaScript-iOS-Android-) för att förstå hur de används för att identifiera användare i händelsedata.

## Användningsfall

Det här tillägget bör användas om du vill använda data från Edge Network i [!DNL Mixpanel] för att utnyttja funktionerna för produktanalys.

Ta till exempel en detaljhandelsorganisation som har en flerkanalsnärvaro (webbplats och mobil). Organisationen hämtar in transaktions- eller konverteringsdata som händelsedata från sina plattformar och läser in dessa i [!DNL Mixpanel] med tillägget för händelsevidarebefordran.

Analysteam kan sedan utnyttja [!DNL Mixpanel's] funktioner för att bearbeta datauppsättningar och få affärsinsikter, som kan användas för att generera diagram, instrumentpaneler eller andra visualiseringar för att informera affärsintressenter.

Mer information om användningsfall för [!DNL Mixpanel]finns i följande dokumentation:

* [Ny på [!DNL Mixpanel]](https://help.mixpanel.com/hc/en-us/sections/360008533532-New-to-Mixpanel)
* [Vad är  [!DNL Mixpanel]?](https://developer.mixpanel.com/docs)
* [12 must-try [!DNL Mixpanel] funktioner](https://mixpanel.com/blog/12-things-you-probably-didnt-know-you-could-do-with-mixpanel/)

## [!DNL Mixpanel] krav {#prerequisites-mixpanel}

Du måste ha en giltig [!DNL Mixpanel] för att kunna använda tillägget. Gå till [[!DNL Mixpanel] registreringssida](https://mixpanel.com/register/) för att registrera och skapa ett konto om du inte redan har ett.

Se till att [[!DNL Identity Merge]](https://help.mixpanel.com/hc/en-us/articles/9648680824852-ID-Merge-Implementation-Best-Practices) inställningen är aktiverad för ditt projekt. Navigera till **[!DNL Settings]** > **[!DNL Project Setting]** > **[!DNL Identity Merge]** och växla inställning.

### Identitetskluster i [!DNL Mixpanel]

I [!DNL Mixpanel], ett identitetskluster innehåller en samling `distinct_id` värden som ansluter till en enskild användare. [!DNL Mixpanel] hanterar klustret med identiteter för varje användare och löser ett enskilt kanoniskt problem `distinct_id` från varje kluster som ska användas för rapportering. Du kan även inkludera en egen identifierare (kallas lokal `distinct_id`) för anonyma händelser som inträffar före en användaridentifieringshändelse.

[!DNL Mixpanel] löser identitetsgrupper på två sätt:

* **Identifiera** : [!DNL Mixpanel] kopplar den valda identifieraren till en anonym `distinct_id`. Om din webbplats har [!DNL Mixpanel] SDK är aktiverat, plattformen använder `distinct_id` tilldelas den användare som är inloggad.
* **Alias**: [!DNL Mixpanel] kombinerar två icke-anonyma `distinct id`är tillsammans om ytterligare villkor för sammanslagning är uppfyllda.

>[!NOTE]
>
>Se [!DNL Mixpanel] dokument på [identitetshantering](https://help.mixpanel.com/hc/en-us/articles/360041039771-Getting-Started-with-Identity-Management#user-identification) om du vill ha mer information om de här metoderna.
>
>Bekräfta att du har aktiverat [[!DNL Mixpanel] funktion för identitetssammanfogning](#prerequisites-mixpanel) för att säkerställa att identitetskluster löses på rätt sätt.

### Samla nödvändig konfigurationsinformation {#configuration-details}

För att ansluta Experience Platform till [!DNL Mixpanel] du måste ha följande indata:

| Nyckeltyp | Beskrivning | Exempel |
| --- | --- | --- |
| Projekttoken | Projekttoken som är associerad med din [!DNL Mixpanel] konto. Se [!DNL Mixpanel] dokumentation om [hitta din projekttoken](https://help.mixpanel.com/hc/en-us/articles/115004502806-Find-Project-Token-) för vägledning. | `25470xxxxxxxxxxxxxxxxxxx1289` |

## Installera och konfigurera [!DNL Mixpanel] extension {#install}

Installera tillägget genom att [skapa en egenskap för vidarebefordring av händelser](../../../ui/event-forwarding/overview.md#properties) eller välj en befintlig egenskap att redigera i stället.

Välj **[!UICONTROL Extensions]** i den vänstra navigeringen. I **[!UICONTROL Catalog]** flik, välja **[!UICONTROL Install]** på kortet för [!DNL Mixpanel] tillägg.

![Installera [!DNL Mixpanel] tillägg.](../../../images/extensions/server/mixpanel/install-extension.png)

## Skapa en [!DNL Send Event] regel

Börja skapa en ny regel i egenskapen för vidarebefordran av händelser. Under **[!UICONTROL Actions]**, lägga till en ny åtgärd och ange tillägget till **[!UICONTROL Mixpanel]**. Ange sedan åtgärdstypen till **[!UICONTROL Track Event]** skicka Adobe Experience Edge Network-händelser till [!DNL Mixpanel].

| Indata | Beskrivning | Obligatoriskt |
| --- | --- | --- |
| [!UICONTROL Project Token] | Det här fältet ska mappas till den projekttoken som är kopplad till din [!DNL Mixpanel] konto. | Ja |
| [!UICONTROL Event Type] | Händelsens namn. | Ja |
| [!UICONTROL Event Time] | Händelsens tid. |  |
| [!UICONTROL Mixpanel Distinct ID] | Den unika identifieraren för användaren som utförde händelsen. |  |
| [!UICONTROL Insert ID] | En unik identifierare för händelsen som används för borttagning av dubbletter. |  |
| [!UICONTROL Event Properties] | Ett JSON-objekt som innehåller anpassade egenskaper för händelsen. Välj mellan att tillhandahålla rå JSON eller att använda en förenklad uppsättning indata för nyckelvärden. |  |

>[!NOTE]
>
>Mer information om standardfälten för [!DNL Mixpanel] -händelsen, se [officiell dokumentation](https://developer.mixpanel.com/reference/import-events#event).

![Lägg till en åtgärdskonfiguration för händelsevidarebefordringsregel.](../../../images/extensions/server/mixpanel/track-event-action.png)

När [!UICONTROL Track Event] åtgärden läggs till i regeln, du kan konfigurera regelns villkor så att den bara aktiveras för vissa händelser, eller så kan du lämna villkorsavsnittet tomt för att få regeln att aktiveras för alla händelser.

>[!IMPORTANT]
>
>Om din webbplats använder [!DNL Mixpanel] SDK, du kan fortsätta till nästa steg i [validera data inom [!DNL Mixpanel]](#validate). Om du inte använder [!DNL Mixpanel] SDK, du måste [skapa en separat regel för identitetsspårning](#create-an-identity-tracking-rule) säkerställa att lämpliga händelser och `distinct_id` värden skickas till [!DNL Mixpanel] när en användaridentifieringshändelse inträffar.

## Validera data i [!DNL Mixpanel] {#validate}

Om implementeringen lyckas och händelser samlas in visas händelser i [[!DNL Mixpanel] konsol](https://help.mixpanel.com/hc/en-us/articles/4402837164948).

Kontrollera om [!DNL Mixpanel] har sammanfogat händelserna efter inloggning ifyllda med e-postvärden och händelserna som skapades när **[!UICONTROL Send Event]**. Om den implementeras korrekt [!DNL Mixpanel] associerar dem med en [användarprofil](https://help.mixpanel.com/hc/en-us/articles/115004501966).

## Nästa steg

I den här guiden beskrivs hur du skickar konverteringshändelser till [!DNL Mixpanel] med händelsevidarebefordran. Det här tillägget för händelsevidarebefordran utnyttjar [!DNL Mixpanel] SDK och JavaScript API. Mer information om dessa underliggande tekniker finns i den officiella dokumentationen:

* [[!DNL Mixpanel] SDK](https://developer.mixpanel.com/docs/nodejs)
* [[!DNL Mixpanel] JavaScript API](https://developer.mixpanel.com/docs/javascript-full-api-reference#mixpanelidentify)

Mer information om funktioner för att vidarebefordra händelser i Experience Platform finns i [händelsevidarebefordring - översikt](../../../ui/event-forwarding/overview.md).
