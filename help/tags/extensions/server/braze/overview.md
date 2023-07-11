---
keywords: tillägg för händelsevidarebefordran;braze;braze event forward extension
title: Vidarekoppling av hjärnhändelse
description: Detta Adobe Experience Platform-tillägg för händelsevidarebefordran skickar Adobe Experience Edge Network-händelser till Braze.
last-substantial-update: 2023-03-29T00:00:00Z
exl-id: 297f48f8-2c3b-41c2-8820-35f4558c67b3
source-git-commit: 4f75bbfee6b550552d2c9947bac8540a982297eb
workflow-type: tm+mt
source-wordcount: '1735'
ht-degree: 1%

---

# [!DNL Braze Track Events API] tillägg för händelsevidarebefordran

[[!DNL Braze]](https://www.braze.com) är en plattform för kundengagemang som driver kundcentrerad interaktion mellan konsumenter och varumärken i realtid. Använda [!DNL Braze]kan du göra följande:

- Leverera data (t.ex. marknadsföringsmeddelanden) till riktade användare baserat på deras språkinställningar, positionering med mera för att öka konverteringsgraden och stödja viktiga affärsmål.
- Skicka personaliserade meddelanden till kunder i flera kanaler, inklusive e-post, push-meddelanden och meddelanden i appen, vid rätt tidpunkt och på de språk de föredrar.
- Målgruppsanpassa användare för marknadsförings- och kampanjkampanjer för att öka antalet återkommande kunder.
- Studera användarbeteenden och mönster för att inrikta er på specifika målgrupper med anpassade meddelanden, vilket kan öka intäkterna.

The [!DNL Braze Track Events API] [händelsevidarebefordran](../../../ui/event-forwarding/overview.md) kan du utnyttja data som samlats in i Adobe Experience Platform Edge Network och skicka dem till [!DNL Braze] i form av händelser på serversidan med [[!DNL Braze User Track]](https://www.braze.com/docs/api/endpoints/user_data/post_user_track) API.

Det här dokumentet beskriver tilläggets användningsfall, hur du installerar det i biblioteken för vidarebefordring av händelser och hur du använder dess funktioner vid en vidarebefordring av händelser [regel](../../../ui/managing-resources/rules.md).

## Användningsfall

Det här tillägget bör användas om du vill använda data från Edge Network i [!DNL Braze] för att utnyttja sina funktioner för kundanalys och målgruppsanpassning.

Ta till exempel en detaljhandelsorganisation som har en flerkanalsnärvaro (webbplats och mobil) och som samlar in transaktionsdata eller konverteringsdata som händelsedata från sin webbplats och sina mobila plattformar. Använda olika [tag](../../../home.md) skickas dessa data till Edge Network i realtid. Härifrån kommer [!DNL Braze] tillägg för händelsevidarebefordran skickar automatiskt relevanta händelser till [!DNL Braze] från serversidan.

När data har skickats kan organisationens analysteam sedan utnyttja dem [!DNL Braze's] funktioner för att bearbeta datauppsättningar och få affärsinsikter för att generera diagram, instrumentpaneler eller andra visualiseringar som kan informera affärsintressenter. Se [[!DNL Braze] kunder](https://www.braze.com/customers) sida för mer information om de olika användningsexemplen för plattformen.

## [!DNL Braze] krav och skyddsräcken {#prerequisites}

Du måste ha en [!DNL Braze] för att kunna använda sina tekniker. Om du inte har något konto går du till [Sidan Kom igång](https://www.braze.com/get-started/) på [!DNL Braze] för att ansluta till [!DNL Braze Sales] och börja skapa konto.

### API-skyddsutkast

Tillägget använder två av [!DNL Braze]API:er och deras begränsningar beskrivs nedan:

| API | Hastighetsgränser |
| --- | --- |
| [!DNL User Track] | 50 000 förfrågningar per minut. <br>Se [[!DNL User Track] API-dokumentation](https://www.braze.com/docs/api/endpoints/user_data/post_user_track#rate-limit) för mer information. |
| [!DNL User Identify] | 20 000 förfrågningar per minut. <br>Se [[!DNL User Identify] API-dokumentation](https://www.braze.com/docs/api/endpoints/user_data/post_user_identify#rate-limit) för mer information. |

>[!NOTE]
>
> Se guiden på [[!DNL Braze] API-begränsningar](https://www.braze.com/docs/api/api_limits/) för närmare uppgifter om de begränsningar som de fastställer.

### Fakturerbara datapunkter

Skicka ytterligare anpassade attribut till [!DNL Braze] kan öka [!DNL Braze] datapunktskonsumtion. Kontakta [!DNL Braze] kontohanteraren innan ytterligare anpassade attribut skickas. Se [!DNL Braze] dokumentation om [fakturerbara datapunkter](https://www.braze.com/docs/user_guide/onboarding_with_braze/data_points/#billable-data-points) för mer information.

### Samla nödvändig konfigurationsinformation {#configuration-details}

För att ansluta Edge Network till [!DNL Braze]krävs följande indata:

| Nyckeltyp | Beskrivning | Exempel |
| --- | --- | --- |
| [!DNL Braze] Instans | REST-slutpunkten som är associerad med [!DNL Braze] konto. Se [!DNL Braze] dokumentation om [instanser](https://www.braze.com/docs/user_guide/administrative/access_braze/sdk_endpoints) för vägledning. | `https://rest.iad-03.braze.com` |
| API-nyckel | The [!DNL Braze] API-nyckel som är associerad med [!DNL Braze] konto. <br/>Se [!DNL Braze] dokumentation om [REST API-nyckel](https://www.braze.com/docs/api/basics/#rest-api-key) för vägledning. | `YOUR-BRAZE-REST-API-KEY` |

### Skapa en hemlighet

Skapa ett nytt [händelsevidarebefordringshemlighet](../../../ui/event-forwarding/secrets.md) och ange värdet för [[!DNL Braze] API-nyckel](#configuration-details). Detta används för att autentisera anslutningen till ditt konto samtidigt som värdet är säkert.

## Installera och konfigurera [!DNL Braze] extension {#install}

Installera tillägget genom att [skapa en egenskap för vidarebefordring av händelser](../../../ui/event-forwarding/overview.md#properties) eller välj en befintlig egenskap att redigera i stället.

Välj **[!UICONTROL Extensions]** i den vänstra navigeringen. I **[!UICONTROL Catalog]** flik, välja **[!UICONTROL Install]** på kortet för [!DNL Braze] tillägg.

![Installera [!DNL Braze] tillägg.](../../../images/extensions/server/braze/install-extension.png)

På nästa skärm anger du följande [konfigurationsvärden](#configuration-details) som du tidigare har samlat in från [!DNL Braze]:

- **[!UICONTROL Braze Rest Endpoint URL]**: Du kan ange värdet för [!DNL Braze] rest endpoint URL as plain text in the provided input.
- **[!UICONTROL API Key]**: Välj [hemligt dataelement](#create-a-secret) som du skapade tidigare, som innehåller [!DNL Braze] API-nyckel.

Välj **[!UICONTROL Save]** när du är klar.

![The [!DNL Braze] konfigurationssida för tillägg.](../../../images/extensions/server/braze/configure-extension.png)

## Skapa en [!DNL Send Event] regel {#tracking-rule}

Skapa en ny händelsevidarebefordring när du har installerat tillägget [regel](../../../ui/managing-resources/rules.md) och konfigurera villkoren efter behov. När du konfigurerar åtgärderna för regeln väljer du **[!UICONTROL Braze]** tillägg, välj **[!UICONTROL Send Event]** för åtgärdstypen.

![Lägg till en åtgärdskonfiguration för händelsevidarebefordringsregel.](../../../images/extensions/server/braze/braze-event-action.png)

**[!UICONTROL User Identification]**

| Indata | Beskrivning |
| --- | --- |
| [!UICONTROL External User ID] | Lång, slumpmässig och väl distribuerad UUID eller GUID. Om du väljer en annan metod för att namnge dina användar-ID:n måste de också vara långa, slumpmässiga och väl fördelade. Läs mer om [föreslagen namnkonvention för användar-ID](https://www.braze.com/docs/developer_guide/platform_integration_guides/web/analytics/setting_user_ids#suggested-user-id-naming-convention). |
| [!UICONTROL Braze User ID] | Braze user identifier. |
| [!UICONTROL User Alias] | Ett alias fungerar som en alternativ unik användaridentifierare. Använd alias för att identifiera användare med andra dimensioner än ditt huvudanvändar-ID. <br><br> Användaraliasobjektet består av två delar: ett alias_name för själva identifieraren och ett alias_label som anger aliastypen. Användare kan ha flera alias med olika etiketter, men bara ett alias_name per alias_label. |

{style="table-layout:auto"}

>[!NOTE]
>
> Om du vill koppla händelsen till en användare måste du fylla i antingen [!UICONTROL External User ID] eller [!UICONTROL Braze User Identifier] fält eller [!UICONTROL User Alias] -avsnitt.

**[!UICONTROL Event Data]**

| Indata | Beskrivning | Obligatoriskt |
| --- | --- | --- |
| [!UICONTROL Event Name &#x200B;] | Händelsens namn. | Ja |
| [!UICONTROL Event Time] | Datum-tid som sträng i ISO 8601 eller i `yyyy-MM-dd'T'HH:mm:ss:SSSZ` format. | Ja |
| [!UICONTROL App Identifier] | Programidentifieraren eller <strong>app_id</strong> är en parameter som associerar aktivitet med ett specifikt program i appgruppen. Det anger vilket program i appgruppen du interagerar med. Läs mer om [API-identifierartyper](https://www.braze.com/docs/api/identifier_types/). | |
| [!UICONTROL Event Properties &#x200B;] | Ett JSON-objekt som innehåller anpassade egenskaper för händelsen. |  |

{style="table-layout:auto"}

>[!NOTE]
>
> The **[!UICONTROL Braze Send Event]** funktionsmakrot kräver bara en **[!UICONTROL Event Name]** och **[!UICONTROL Event Time]** ska anges, men du bör inkludera så mycket information som möjligt i fältet för anpassade egenskaper. Mer information om [!DNL Braze] händelseobjekt, se [officiell dokumentation](https://www.braze.com/docs/api/objects_filters/event_object/).

**[!UICONTROL User Attributes]**

Användarattribut kan vara ett JSON-objekt som innehåller fält som skapar eller uppdaterar ett attribut med det angivna namnet och värdet för den angivna användarprofilen. Följande egenskaper stöds:

| Användarattribut | Beskrivning |
| --- | --- |
| [!UICONTROL First Name] | |
| [!UICONTROL Last Name] | |
| [!UICONTROL Phone] | |
| [!UICONTROL Email] | |
| [!UICONTROL Gender] | En av följande strängar: &quot;M&quot;, &quot;F&quot;, &quot;O&quot; (övrigt), &quot;N&quot; (ej tillämpligt), &quot;P&quot; (säg inte). |
| [!UICONTROL City] | |
| [!UICONTROL Country] | Land som en sträng i [ISO-3166-1 alpha-2](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2) format. |
| [!UICONTROL Language] | Språk som sträng i [ISO-639-1](https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes) format. |
| [!UICONTROL Date of Birth] | Sträng i formatet &quot;YYY-MM-DD&quot; (t.ex. 1980-12-21). |
| [!UICONTROL Time Zone] | Tidszonsnamn från [IANA-tidszonsdatabas](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones) (t.ex. &#39;America/New_York&#39; eller &#39;Eastern Time (USA &amp; Kanada)&#39;). |
| [!UICONTROL Facebook] | Hash som innehåller något av id (sträng), gillar (strängmatris), num_ativ (heltal). |
| [!UICONTROL Twitter] | Hash som innehåller något av id (heltal), screen_name (sträng, Twitter handle), follow_count (heltal), kompis_count (heltal), statuses_count(heltal). |

{style="table-layout:auto"}

## Skapa en [!DNL Send Purchase Event] regel {#purchase-rule}

Skapa en ny händelsevidarebefordring när du har installerat tillägget [regel](../../../ui/managing-resources/rules.md) och konfigurera villkoren efter behov. När du konfigurerar åtgärderna för regeln väljer du **[!UICONTROL Braze]** tillägg, välj **[!UICONTROL Send Purchase Event]** för åtgärdstypen.

![Lägg till en åtgärdskonfiguration för händelsevidarebefordringsregel för Braze Purchase-åtgärd.](../../../images/extensions/server/braze/braze-purchase-event-action.png)

**[!UICONTROL User Identification]**

| Indata | Beskrivning |
| --- | --- |
| [!UICONTROL External User ID] | Lång, slumpmässig och väl distribuerad UUID eller GUID. Om du väljer en annan metod för att namnge dina användar-ID:n måste de också vara långa, slumpmässiga och väl fördelade. Läs mer om [föreslagen namnkonvention för användar-ID](https://www.braze.com/docs/developer_guide/platform_integration_guides/web/analytics/setting_user_ids#suggested-user-id-naming-convention). |
| [!UICONTROL Braze User ID] | Braze user identifier. |
| [!UICONTROL User Alias] | Ett alias fungerar som en alternativ unik användaridentifierare. Använd alias för att identifiera användare med andra dimensioner än ditt huvudanvändar-ID. <br><br> Användaraliasobjektet består av två delar: ett alias_name för själva identifieraren och ett alias_label som anger aliastypen. Användare kan ha flera alias med olika etiketter, men bara ett alias_name per alias_label. |

{style="table-layout:auto"}

>[!NOTE]
>
> Om du vill länka händelsen till en användare måste du antingen slutföra [!UICONTROL External User ID] fält, [!UICONTROL Braze User Identifier] eller [!UICONTROL User Alias] -avsnitt.

**[!UICONTROL Purchase Data]**

| Indata | Beskrivning | Obligatoriskt |
| --- | --- | --- |
| [!UICONTROL Product ID &#x200B;] | Identifierare för inköpet. (t.ex. produktnamn eller produktkategori) | Ja |
| [!UICONTROL Purchase Time] | Datum-tid som sträng i ISO 8601 eller i `yyyy-MM-dd'T'HH:mm:ss:SSSZ` format. | Ja |
| [!UICONTROL Currency &#x200B;] | Valuta som en sträng i [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) Alfabetiskt valutakodformat. | Ja |
| [!UICONTROL Price &#x200B;] | Pris. | Ja |
| [!UICONTROL Quantity &#x200B;] | Om inget anges blir standardvärdet 1. Det högsta värdet måste vara lägre än 100. | |
| [!UICONTROL App Identifier] | Programidentifieraren eller <strong>app_id</strong> är en parameter som associerar aktivitet med ett specifikt program i appgruppen. Det anger vilket program i appgruppen du interagerar med. Läs mer om [API-identifierartyper](https://www.braze.com/docs/api/identifier_types/). | |
| [!UICONTROL Purchase Properties &#x200B;] | Ett JSON-objekt som innehåller anpassade egenskaper för köpet. |  |

{style="table-layout:auto"}

>[!NOTE]
>
> The **[!UICONTROL Braze Send Event]** funktionsmakrot kräver bara en **[!UICONTROL Event Name]** och **[!UICONTROL Event Time]** ska anges, men du bör inkludera så mycket information som möjligt i fältet för anpassade egenskaper. Mer information om [!DNL Braze] händelseobjekt, se [officiell dokumentation](https://www.braze.com/docs/api/objects_filters/event_object/).

**[!UICONTROL User Attributes]**

Användarattribut kan vara ett JSON-objekt som innehåller fält som skapar eller uppdaterar ett attribut med det angivna namnet och värdet för den angivna användarprofilen. Följande egenskaper stöds:

| Användarattribut | Beskrivning |
| --- | --- |
| [!UICONTROL First Name] | |
| [!UICONTROL Last Name] | |
| [!UICONTROL Phone] | |
| [!UICONTROL Email] | |
| [!UICONTROL Gender] | En av följande strängar: &quot;M&quot;, &quot;F&quot;, &quot;O&quot; (övrigt), &quot;N&quot; (ej tillämpligt), &quot;P&quot; (säg inte). |
| [!UICONTROL City] | |
| [!UICONTROL Country] | Land som en sträng i [ISO-3166-1 alpha-2](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2) format. |
| [!UICONTROL Language] | Språk som sträng i [ISO-639-1](https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes) format. |
| [!UICONTROL Date of Birth] | Sträng i formatet &quot;YYY-MM-DD&quot; (t.ex. 1980-12-21). |
| [!UICONTROL Time Zone] | Tidszonsnamn från [IANA-tidszonsdatabas](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones) (t.ex. &#39;America/New_York&#39; eller &#39;Eastern Time (USA &amp; Kanada)&#39;). |
| [!UICONTROL Facebook] | Hash som innehåller något av id (sträng), gillar (strängmatris), num_ativ (heltal). |
| [!UICONTROL Twitter] | Hash som innehåller något av id (heltal), screen_name (sträng, Twitter handle), follow_count (heltal), kompis_count (heltal), statuses_count(heltal). |

{style="table-layout:auto"}

## Validera data i [!DNL Braze] {#validate}

Om händelsesamlingen och [!DNL Adobe Experience Platform] integreringen lyckades, du kommer att se händelser i [!DNL Braze] konsol när [visa användarprofiler](https://www.braze.com/docs/user_guide/engagement_tools/segments/user_profiles/). De nya händelsedata som skickas till [!DNL Braze] återspeglas i [!DNL Purchases] del av en viss användares [fliken Översikt](https://www.braze.com/docs/user_guide/engagement_tools/segments/user_profiles/#overview-tab).

## Nästa steg

I den här guiden beskrivs hur du skickar konverteringshändelser till [!DNL Braze] med händelsevidarebefordran. Mer information om efterföljande program för händelsedata som skickas till [!DNL Braze], se [officiell dokumentation](https://www.braze.com/docs).

Mer information om funktioner för att vidarebefordra händelser i Experience Platform finns i [händelsevidarebefordring - översikt](../../../ui/event-forwarding/overview.md).
