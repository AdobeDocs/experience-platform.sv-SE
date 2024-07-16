---
keywords: tillägg för händelsevidarebefordran;braze;braze event forward extension
title: Vidarekoppling av hjärnhändelse
description: Detta Adobe Experience Platform-tillägg för händelsevidarebefordran skickar Edge Network-händelser till Braze.
last-substantial-update: 2023-03-29T00:00:00Z
exl-id: 297f48f8-2c3b-41c2-8820-35f4558c67b3
source-git-commit: d81c4c8630598597ec4e253ef5be9f26c8987203
workflow-type: tm+mt
source-wordcount: '1557'
ht-degree: 0%

---

# [!DNL Braze Track Events API]-tillägg för händelsevidarebefordring

[[!DNL Braze]](https://www.braze.com) är en plattform för kundengagemang som driver kundcentrerade interaktioner mellan konsumenter och varumärken i realtid. Med [!DNL Braze] kan du göra följande:

- Leverera data (t.ex. marknadsföringsmeddelanden) till riktade användare baserat på deras språkinställningar, positionering med mera för att öka konverteringsgraden och stödja viktiga affärsmål.
- Skicka personaliserade meddelanden till kunder i flera kanaler, inklusive e-post, push-meddelanden och meddelanden i appen, vid rätt tidpunkt och på de språk de föredrar.
- Målgruppsanpassa användare för marknadsförings- och kampanjkampanjer för att öka antalet återkommande kunder.
- Studera användarbeteenden och mönster för att inrikta er på specifika målgrupper med anpassade meddelanden, vilket kan öka intäkterna.

Med tillägget [!DNL Braze Track Events API] [ för vidarebefordran av händelser](../../../ui/event-forwarding/overview.md) kan du utnyttja data som har samlats in i Adobe Experience Platform Edge Network och skicka dem till [!DNL Braze] i form av händelser på serversidan med API:t [[!DNL Braze User Track]](https://www.braze.com/docs/api/endpoints/user_data/post_user_track) .

Det här dokumentet beskriver tilläggets användningsfall, hur du installerar det i biblioteken för vidarebefordran av händelser och hur du använder dess funktioner i en [regel](../../../ui/managing-resources/rules.md) för vidarebefordran av händelser.

## Användningsfall

Det här tillägget bör användas om du vill använda data från Edge Network i [!DNL Braze] för att utnyttja dess funktioner för kundanalys och målinriktning.

Ta till exempel en detaljhandelsorganisation som har en flerkanalsnärvaro (webbplats och mobil) och som samlar in transaktionsdata eller konverteringsdata som händelsedata från sin webbplats och sina mobila plattformar. Dessa data skickas till Edge Network i realtid med olika [tagg](../../../home.md)-regler. Härifrån skickar tillägget för [!DNL Braze]-händelsevidarebefordran automatiskt relevanta händelser till [!DNL Braze] från serversidan.

När data har skickats kan organisationens analysteam sedan utnyttja [!DNL Braze's]-funktioner för att bearbeta datauppsättningarna och härleda affärsinsikter för att generera diagram, instrumentpaneler eller andra visualiseringar för att informera affärsintressenter. På sidan [[!DNL Braze] kunder](https://www.braze.com/customers) finns mer information om de olika användningsexemplen för plattformen.

## [!DNL Braze] krav och skyddsräcken {#prerequisites}

Du måste ha ett [!DNL Braze]-konto för att kunna använda dess tekniker. Om du inte har något konto går du till sidan [Kom igång](https://www.braze.com/get-started/) på [!DNL Braze] för att ansluta till [!DNL Braze Sales] och starta kontoskapandet.

### API-skyddsräcken

Tillägget använder två av [!DNL Braze]s API:er och deras gränser beskrivs nedan:

| API | Hastighetsgränser |
| --- | --- |
| [!DNL User Track] | 50 000 förfrågningar per minut. <br>Mer information finns i [[!DNL User Track] API-dokumentationen](https://www.braze.com/docs/api/endpoints/user_data/post_user_track#rate-limit). |
| [!DNL User Identify] | 20 000 förfrågningar per minut. <br>Mer information finns i [[!DNL User Identify] API-dokumentationen](https://www.braze.com/docs/api/endpoints/user_data/post_user_identify#rate-limit). |

>[!NOTE]
>
> Mer information om begränsningar finns i guiden för [[!DNL Braze] API-gränser](https://www.braze.com/docs/api/api_limits/).

### Fakturerbara datapunkter

Om du skickar ytterligare anpassade attribut till [!DNL Braze] kan det öka datapunktskonsumtionen för [!DNL Braze]. Kontakta din [!DNL Braze]-kontohanterare innan du skickar ytterligare anpassade attribut. Mer information finns i [!DNL Braze]-dokumentationen om [fakturerbara datapunkter](https://www.braze.com/docs/user_guide/data_and_analytics/data_points/?tab=billable).

### Samla nödvändig konfigurationsinformation {#configuration-details}

Följande indata krävs för att ansluta Edge Network till [!DNL Braze]:

| Nyckeltyp | Beskrivning | Exempel |
| --- | --- | --- |
| [!DNL Braze]-instans | REST-slutpunkten som är associerad med kontot [!DNL Braze]. Mer information finns i [!DNL Braze]-dokumentationen för [instanser](https://www.braze.com/docs/user_guide/administrative/access_braze/sdk_endpoints). | `https://rest.iad-03.braze.com` |
| API-nyckel | API-nyckeln [!DNL Braze] som är associerad med kontot [!DNL Braze]. <br/>Mer information finns i [!DNL Braze]-dokumentationen för [REST API-nyckeln](https://www.braze.com/docs/api/basics/#rest-api-key). | `YOUR-BRAZE-REST-API-KEY` |

### Skapa en hemlighet

Skapa en ny [händelsevidarebefordringshemlighet](../../../ui/event-forwarding/secrets.md) och ange värdet till din [[!DNL Braze] API-nyckel](#configuration-details). Detta används för att autentisera anslutningen till ditt konto samtidigt som värdet är säkert.

## Installera och konfigurera tillägget [!DNL Braze] {#install}

Om du vill installera tillägget [skapar du en egenskap för vidarebefordring av händelser](../../../ui/event-forwarding/overview.md#properties) eller väljer en befintlig egenskap att redigera i stället.

Välj **[!UICONTROL Extensions]** i den vänstra navigeringen. På fliken **[!UICONTROL Catalog]** väljer du **[!UICONTROL Install]** på kortet för tillägget [!DNL Braze].

![Installera tillägget [!DNL Braze].](../../../images/extensions/server/braze/install-extension.png)

På nästa skärm anger du följande [konfigurationsvärden](#configuration-details) som du tidigare har hämtat från [!DNL Braze]:

- **[!UICONTROL Braze Rest Endpoint URL]**: Du kan ange värdet för [!DNL Braze] rest-URL:en som oformaterad text i angivna indata.
- **[!UICONTROL API Key]**: Välj det [hemliga dataelement](#create-a-secret) som du skapade tidigare och som innehåller din [!DNL Braze] API-nyckel.

Välj **[!UICONTROL Save]** när du är klar.

![Konfigurationssidan för [!DNL Braze]-tillägget.](../../../images/extensions/server/braze/configure-extension.png)

## Skapa en [!DNL Send Event]-regel {#tracking-rule}

När du har installerat tillägget skapar du en ny händelsevidarebefordring av [regeln](../../../ui/managing-resources/rules.md) och konfigurerar villkoren efter behov. När du konfigurerar åtgärderna för regeln väljer du tillägget **[!UICONTROL Braze]** och väljer sedan **[!UICONTROL Send Event]** som åtgärdstyp.

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
> Om du vill koppla händelsen till en användare måste du fylla i antingen fältet [!UICONTROL External User ID], fältet [!UICONTROL Braze User Identifier] eller avsnittet [!UICONTROL User Alias].

**[!UICONTROL Event Data]**

| Indata | Beskrivning | Obligatoriskt |
| --- | --- | --- |
| [!UICONTROL Event Name &#x200B;] | Händelsens namn. | Ja |
| [!UICONTROL Event Time] | Datum-tid som sträng i ISO 8601 eller i formatet `yyyy-MM-dd'T'HH:mm:ss:SSSZ`. | Ja |
| [!UICONTROL App Identifier] | Programidentifieraren eller <strong>app_id</strong> är en parameter som associerar aktivitet med en viss app i appgruppen. Det anger vilket program i appgruppen du interagerar med. Läs mer om [API-identifierartyperna](https://www.braze.com/docs/api/identifier_types/). | |
| [!UICONTROL Event Properties &#x200B;] | Ett JSON-objekt som innehåller anpassade egenskaper för händelsen. |  |

{style="table-layout:auto"}

>[!NOTE]
>
> Åtgärden **[!UICONTROL Braze Send Event]** kräver endast att **[!UICONTROL Event Name]** och **[!UICONTROL Event Time]** anges, men du bör inkludera så mycket information som möjligt i fältet för anpassade egenskaper. Mer information om händelseobjektet [!DNL Braze] finns i [officiell dokumentation](https://www.braze.com/docs/api/objects_filters/event_object/).

**[!UICONTROL User Attributes]**

Användarattribut kan vara ett JSON-objekt som innehåller fält som skapar eller uppdaterar ett attribut med det angivna namnet och värdet för den angivna användarprofilen. Följande egenskaper stöds:

| Användarattribut | Beskrivning |
| --- | --- |
| [!UICONTROL First Name] | |
| [!UICONTROL Last Name] | |
| [!UICONTROL Phone] | |
| [!UICONTROL Email] | |
| [!UICONTROL Gender] | En av följande strängar: &quot;M&quot;, &quot;F&quot;, &quot;O&quot; (annan), &quot;N&quot; (ej tillämplig), &quot;P&quot; (använd inte). |
| [!UICONTROL City] | |
| [!UICONTROL Country] | Land som en sträng i formatet [ISO-3166-1 alpha-2](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2) . |
| [!UICONTROL Language] | Språk som en sträng i formatet [ISO-639-1](https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes). |
| [!UICONTROL Date of Birth] | Sträng i formatet &quot;YYY-MM-DD&quot; (t.ex. 1980-12-21). |
| [!UICONTROL Time Zone] | Tidszonsnamn från [IANA-tidszonsdatabas](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones) (t.ex. America/New_York eller Eastern Time (USA och Kanada)). |
| [!UICONTROL Facebook] | Hash som innehåller något av id (sträng), gillar (strängmatris), num_ativ (heltal). |
| [!UICONTROL Twitter] | Hash som innehåller något av id (heltal), screen_name (Twitter, handle), follow_count (heltal), kompis_count (heltal), statuses_count(heltal). |

{style="table-layout:auto"}

## Skapa en [!DNL Send Purchase Event]-regel {#purchase-rule}

När du har installerat tillägget skapar du en ny händelsevidarebefordring av [regeln](../../../ui/managing-resources/rules.md) och konfigurerar villkoren efter behov. När du konfigurerar åtgärderna för regeln väljer du tillägget **[!UICONTROL Braze]** och väljer sedan **[!UICONTROL Send Purchase Event]** som åtgärdstyp.

![Lägg till en händelsevidarebefordringsregel för Braze Purchase-åtgärdstyp.](../../../images/extensions/server/braze/braze-purchase-event-action.png)

**[!UICONTROL User Identification]**

| Indata | Beskrivning |
| --- | --- |
| [!UICONTROL External User ID] | Lång, slumpmässig och väl distribuerad UUID eller GUID. Om du väljer en annan metod för att namnge dina användar-ID:n måste de också vara långa, slumpmässiga och väl fördelade. Läs mer om [föreslagen namnkonvention för användar-ID](https://www.braze.com/docs/developer_guide/platform_integration_guides/web/analytics/setting_user_ids#suggested-user-id-naming-convention). |
| [!UICONTROL Braze User ID] | Braze user identifier. |
| [!UICONTROL User Alias] | Ett alias fungerar som en alternativ unik användaridentifierare. Använd alias för att identifiera användare med andra dimensioner än ditt huvudanvändar-ID. <br><br> Användaraliasobjektet består av två delar: ett alias_name för själva identifieraren och ett alias_label som anger aliastypen. Användare kan ha flera alias med olika etiketter, men bara ett alias_name per alias_label. |

{style="table-layout:auto"}

>[!NOTE]
>
> Om du vill länka händelsen till en användare måste du antingen fylla i fältet [!UICONTROL External User ID], fältet [!UICONTROL Braze User Identifier] eller avsnittet [!UICONTROL User Alias].

**[!UICONTROL Purchase Data]**

| Indata | Beskrivning | Obligatoriskt |
| --- | --- | --- |
| [!UICONTROL Product ID &#x200B;] | Identifierare för inköpet. (t.ex. produktnamn eller produktkategori) | Ja |
| [!UICONTROL Purchase Time] | Datum-tid som sträng i ISO 8601 eller i formatet `yyyy-MM-dd'T'HH:mm:ss:SSSZ`. | Ja |
| [!UICONTROL Currency &#x200B;] | Valuta som en sträng i formatet [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) Alfabetisk valutakod. | Ja |
| [!UICONTROL Price &#x200B;] | Pris. | Ja |
| [!UICONTROL Quantity &#x200B;] | Om inget anges blir standardvärdet 1. Det högsta värdet måste vara lägre än 100. | |
| [!UICONTROL App Identifier] | Programidentifieraren eller <strong>app_id</strong> är en parameter som associerar aktivitet med en viss app i appgruppen. Det anger vilket program i appgruppen du interagerar med. Läs mer om [API-identifierartyperna](https://www.braze.com/docs/api/identifier_types/). | |
| [!UICONTROL Purchase Properties &#x200B;] | Ett JSON-objekt som innehåller anpassade egenskaper för köpet. |  |

{style="table-layout:auto"}

>[!NOTE]
>
> Åtgärden **[!UICONTROL Braze Send Event]** kräver endast att **[!UICONTROL Event Name]** och **[!UICONTROL Event Time]** anges, men du bör ta med så mycket information som möjligt i fältet för anpassade egenskaper. Mer information om händelseobjektet [!DNL Braze] finns i [officiell dokumentation](https://www.braze.com/docs/api/objects_filters/event_object/).

**[!UICONTROL User Attributes]**

Användarattribut kan vara ett JSON-objekt som innehåller fält som skapar eller uppdaterar ett attribut med det angivna namnet och värdet för den angivna användarprofilen. Följande egenskaper stöds:

| Användarattribut | Beskrivning |
| --- | --- |
| [!UICONTROL First Name] | |
| [!UICONTROL Last Name] | |
| [!UICONTROL Phone] | |
| [!UICONTROL Email] | |
| [!UICONTROL Gender] | En av följande strängar: &quot;M&quot;, &quot;F&quot;, &quot;O&quot; (annan), &quot;N&quot; (ej tillämplig), &quot;P&quot; (använd inte). |
| [!UICONTROL City] | |
| [!UICONTROL Country] | Land som en sträng i formatet [ISO-3166-1 alpha-2](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2) . |
| [!UICONTROL Language] | Språk som en sträng i formatet [ISO-639-1](https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes). |
| [!UICONTROL Date of Birth] | Sträng i formatet &quot;YYY-MM-DD&quot; (t.ex. 1980-12-21). |
| [!UICONTROL Time Zone] | Tidszonsnamn från [IANA-tidszonsdatabas](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones) (t.ex. America/New_York eller Eastern Time (USA och Kanada)). |
| [!UICONTROL Facebook] | Hash som innehåller något av id (sträng), gillar (strängmatris), num_ativ (heltal). |
| [!UICONTROL Twitter] | Hash som innehåller något av id (heltal), screen_name (Twitter, handle), follow_count (heltal), kompis_count (heltal), statuses_count(heltal). |

{style="table-layout:auto"}

## Validera data i [!DNL Braze] {#validate}

Om händelsesamlingen och integreringen av [!DNL Adobe Experience Platform] lyckades visas händelser i [!DNL Braze]-konsolen när [användarprofiler ](https://www.braze.com/docs/user_guide/engagement_tools/segments/user_profiles/) visades. De nya händelsedata som skickas till [!DNL Braze] visas i avsnittet [!DNL Purchases] på en viss användares [översiktsflik](https://www.braze.com/docs/user_guide/engagement_tools/segments/user_profiles/#overview-tab).

## Nästa steg

I den här guiden beskrivs hur du skickar konverteringshändelser till [!DNL Braze] med hjälp av händelsevidarebefordran. Mer information om program längre fram i kedjan för händelsedata som skickas till [!DNL Braze] finns i [officiell dokumentation](https://www.braze.com/docs).

Mer information om funktioner för att vidarebefordra händelser i Experience Platform finns i [översikten över vidarebefordran av händelser](../../../ui/event-forwarding/overview.md).
