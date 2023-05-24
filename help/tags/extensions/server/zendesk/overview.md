---
title: Tillägg för vidarebefordran av Zendesk-händelse
description: Zendesk-tillägg för händelsevidarebefordran för Adobe Experience Platform.
exl-id: 22e94699-5b84-4a73-b007-557221d3e223
source-git-commit: bfbad3c11df64526627e4ce2d766b527df678bca
workflow-type: tm+mt
source-wordcount: '1263'
ht-degree: 4%

---

# [!DNL Zendesk] Översikt över API-tillägg för händelser

[Zendesk](https://www.zendesk.com) är en kundtjänstlösning och ett säljverktyg. Zendesk [händelsevidarebefordran](../../../ui/event-forwarding/overview.md) tillägget utnyttjar [[!DNL Zendesk Events API]](https://developer.zendesk.com/api-reference/custom-data/events-api/events-api/) för att skicka händelser från Adobe Experience Platform Edge Network till Zendesk för vidare bearbetning. Du kan använda tillägget för att samla in interaktioner med kundprofiler för användning i analyser och åtgärder längre fram i kedjan.

Det här dokumentet beskriver hur du installerar och konfigurerar tillägget i användargränssnittet.

## Förutsättningar

Du måste ha ett Zendesk-konto för att kunna använda det här tillägget. Du kan registrera dig för ett Zendesk-konto på [Zendesk webbplats](https://www.zendesk.com/register/).

Du måste även samla in följande information för din Zendesk-konfiguration:

| Nyckeltyp | Beskrivning | Exempel |
| --- | --- | --- |
| Underdomän | Under registreringsprocessen finns en unik **underdomän** har skapats specifikt för kontot. Se [Zendesk-dokumentation](https://developer.zendesk.com/documentation/ticketing/working-with-oauth/creating-and-using-oauth-tokens-with-the-api/) för mer information. | `xxxxx.zendesk.com` (där `xxxxx` är värdet som angavs när kontot skapades) |
| API-token | Zendesk använder bearer-tokens som en autentiseringsmekanism för att kommunicera med Zendesk API. Generera en API-token när du har loggat in på Zendesk-portalen. Se [Zendesk-dokumentation](https://support.zendesk.com/hc/en-us/articles/4408889192858-Generating-a-new-API-token) för mer information. | `cwWyOtHAv12w4dhpiulfe9BdZFTz3OKaTSzn2QvV` |

{style="table-layout:auto"}

Slutligen måste du skapa en händelsevidarebefordringshemlighet för API-token. Ange hemlig typ till **[!UICONTROL Token]** och ange värdet till den API-token som du hämtade från din Zendesk-konfiguration. Läs dokumentationen om [hemligheter vid vidarebefordran av händelser](../../../ui/event-forwarding/secrets.md) om du vill ha mer information om hur du konfigurerar hemligheter.

## Installera tillägget {#install}

Om du vill installera Zendesk-tillägget i användargränssnittet går du till **Vidarebefordran av händelser** och välj en egenskap som tillägget ska läggas till i eller skapa en ny egenskap i stället.

När du har valt eller skapat den önskade egenskapen går du till **Tillägg** > **Katalog**. Sök efter &quot;[!DNL Zendesk]&quot; och sedan markera **[!DNL Install]** på Zendesk Extension.

![Installationsknappen för Zendesk-tillägget som väljs i användargränssnittet](../../../images/extensions/server/zendesk/install.png)

## Konfigurera tillägget {#configure}

>[!IMPORTANT]
>
>Beroende på implementeringsbehoven kan du behöva skapa ett schema, dataelement och en datauppsättning innan du konfigurerar tillägget. Granska alla konfigurationssteg innan du startar för att avgöra vilka enheter du måste konfigurera för ditt användningsfall.

Välj **Tillägg** i den vänstra navigeringen. Under **Installerad**, markera **Konfigurera** i Zendesk-tillägget.

![Knappen Konfigurera för Zendesk-tillägget som väljs i användargränssnittet](../../../images/extensions/server/zendesk/configure.png)

Under **[!UICONTROL Zendesk Domain]**, anger du värdet för din Zendesk-underdomän. Under **[!UICONTROL Zendesk Token]** markerar du den hemlighet som du skapade tidigare och som innehåller API-token.

![Konfigurationsalternativ som fylls i i användargränssnittet](../../../images/extensions/server/zendesk/input.png)

## Konfigurera en regel för vidarebefordran av händelser

Börja skapa en ny regel för vidarebefordran av händelse [regel](../../../ui/managing-resources/rules.md) och konfigurera villkoren efter behov. När du väljer åtgärder för regeln väljer du [!UICONTROL Zendesk] och välj sedan [!UICONTROL Create Event] åtgärdstyp.

![Definiera regel](../../../images/extensions/server/zendesk/rule.png)

När du konfigurerar åtgärdskonfigurationen uppmanas du att tilldela dataelement till de olika egenskaper som ska skickas till Zendesk.

![Definiera åtgärdskonfiguration](../../../images/extensions/server/zendesk/action-configurations.png)

Dessa dataelement ska mappas enligt nedan.

### `event` tangenter

`event` är ett JSON-objekt som representerar den händelse som utlöses av användaren. Se Zendesk-dokumentet på [anatomi för en händelse](https://developer.zendesk.com/documentation/custom-data/events/anatomy-of-an-event/) om du vill ha information om de egenskaper som hämtats av `event` -objekt.

Följande nycklar kan refereras i `event` objekt vid mappning till dataelement:

| `event` key | Typ | Plattformssökväg | Beskrivning | Obligatoriskt | Gränser |
| --- | --- | --- | --- | --- | --- |
| `source` | Sträng | `arc.event.xdm._extconndev.event_source` | Programmet som skickade händelsen. | Ja | Använd inte `Zendesk` som ett värde eftersom det är ett skyddat källnamn för Zendesk-standardhändelser. Försök att använda den kommer att resultera i ett fel.<br>Värdet får inte vara längre än 40 tecken. |
| `type` | Sträng | `arc.event.xdm._extconndev.event_type` | Ett namn för händelsetypen. Du kan använda det här fältet för att ange olika typer av händelser för en viss källa. Du kan till exempel skapa en uppsättning händelser för användarinloggningar och en annan för kundvagnar. | Ja | Värdet får inte vara längre än 40 tecken. |
| `description` | Sträng | `arc.event.xdm._extconndev.description` | En beskrivning av händelsen. | Nej | (Ej tillämpligt) |
| `created_at` | Sträng | `arc.event.xdm.timestamp` | En ISO-8601-tidsstämpel som visar när händelsen skapades. | Nej | (Ej tillämpligt) |
| `properties` | Objekt | `arc.event.xdm._extconndev.EventProperties` | Ett anpassat JSON-objekt med information om händelsen. | Ja | (Ej tillämpligt) |

{style="table-layout:auto"}

>[!NOTE]
>
>Se [[!DNL Zendesk Events API] dokumentation](https://developer.zendesk.com/api-reference/custom-data/events-api/events-api/) om du vill ha ytterligare vägledning om händelseegenskaper.

### `profile` tangenter

`profile` är ett JSON-objekt som representerar användaren som utlöste händelsen. Se Zendesk-dokumentet på [en profils anatomi](https://developer.zendesk.com/documentation/custom-data/profiles/anatomy-of-a-profile/) om du vill ha information om de egenskaper som hämtats av `profile` -objekt.

Följande nycklar kan refereras i `profile` objekt vid mappning till dataelement:

| `profile` key | Typ | Plattformssökväg | Beskrivning | Obligatoriskt | Gränser |
| --- | --- | --- | --- | --- | --- |
| `source` | Sträng | `arc.event.xdm._extconndev.profile_source` | Den produkt eller tjänst som är associerad med profilen, till exempel `Support`, `CompanyName`, eller `Chat`. | Ja | (Ej tillämpligt) |
| `type` | Sträng | `arc.event.xdm._extconndev.profile_type` | Ett namn för profiltypen. Du kan använda det här fältet för att skapa olika typer av profiler för en viss källa. Du kan till exempel skapa en uppsättning företagsprofiler för kunder och en annan för anställda. | Ja | Profiltypens längd får inte vara längre än 40 tecken. |
| `name` | Sträng | `arc.event.xdm._extconndev.name` | Namnet på personen från profilen | Nej | (Ej tillämpligt) |
| `user_id` | Sträng | `arc.event.xdm._extconndev.user_id` | Personens användar-ID i Zendesk. | Nej | (Ej tillämpligt) |
| `identifiers` | Array | `arc.event.xdm._extconndev.identifiers` | En array som innehåller minst en identifierare. Varje identifierare består av en typ och ett värde. | Ja | Se [Zendesk-dokumentation](https://developer.zendesk.com/api-reference/custom-data/profiles_api/profiles_api/#identifiers-array) för mer information om `identifiers` array. Alla fält och värden måste vara unika. |
| `attributes` | Objekt | `arc.event.xdm._extconndev.attrbutes` | Ett objekt som innehåller användardefinierade egenskaper för personen. | Nej | Se [Zendesk-dokumentation](https://developer.zendesk.com/documentation/custom-data/profiles/anatomy-of-a-profile/#attributes) om du vill ha mer information om profilattribut. |

{style="table-layout:auto"}

## Validera data i Zendesk {#validate}

Om händelseinsamlingen och Adobe Experience Platform-integreringen lyckas visas händelserna i Zendesk-konsolen enligt nedan. Detta indikerar en lyckad integrering.

Profiler:

![Zendesk Profiles page](../../../images/extensions/server/zendesk/zendesk-profiles.png)

Händelser:

![Sidan Zendesk Events](../../../images/extensions/server/zendesk/zendesk-events.png)

## Begärandebegränsningar {#limits}

Zendesk [!DNL Events API] kan hantera följande antal begäranden per minut:

| [!DNL Account Type] | Begäranden per minut |
| --- | --- |
| [!DNL Team] | 250 |
| [!DNL Growth] | 250 |
| [!DNL Professional] | 500 |
| [!DNL Enterprise] | 750 |
| [!DNL Enterprise Plus] | 1000 |

{style="table-layout:auto"}

Se [Zendesk-dokumentation](https://developer.zendesk.com/api-reference/ticketing/account-configuration/usage_limits/#:~:text=API%20requests%20made%20by%20Zendesk%20apps%20are%20subject,sources%20for%20the%20account%2C%20including%20internal%20product%20requests.) för mer information om dessa gränser.

## Fel och felsökning {#errors-and-troubleshooting}

När tillägget används eller konfigureras kan felen nedan returneras av Zendesk Events-API:

| Felkod | Beskrivning | Upplösning | Exempel |
|---|---|---|---|
| 400 | **Ogiltig profillängd:** Det här felet inträffar när längden på ett profilattribut innehåller fler än 40 tecken. | Begränsa längden på profilattributsdata till högst 40 tecken. | `{"error": [{"code":"InvalidProfileTypeLength","title": "Profile type length > 40 chars"}]}` |
| 401 | **Flödet hittades inte:** Det här felet inträffar när en ogiltig domän har angetts. | Kontrollera att en giltig domän har angetts i följande format: `{subdomain}.zendesk.com` | `{"error": [{"description": "No route found for host {subdomain}.zendesk.com","title": "RouteNotFound"}]}` |
| 401 | **Ogiltig eller saknad autentisering:** Det här felet inträffar när åtkomsten till token är ogiltig, saknas eller har upphört att gälla. | Kontrollera att åtkomsttoken är giltig och inte har gått ut. | `{"error": [{"code":"MissingOrInvalidAuthentication","title": "Invalid or Missing Authentication"}]}` |
| 403 | **Otillräckliga behörigheter:** Det här felet inträffar när det inte finns tillräcklig behörighet för att komma åt resursen. | Verifiera att de nödvändiga behörigheterna har angetts. | `{"error": [{"code":"PermissionDenied","title": "Insufficient permisssions to perform operation"}]}` |
| 429 | **För många förfrågningar:** Det här felet inträffar när postgränsen för slutpunktsobjektet har överskridits. | Se avsnittet ovan på [begärandebegränsningar](#limits) för uppgifter om tröskelvärden per gräns. | `{"error": [{"code":"TooManyRequests","title": "Too Many Requests"}]}` |

{style="table-layout:auto"}

## Nästa steg

I det här dokumentet beskrivs hur du installerar och konfigurerar tillägget för vidarebefordran av Zendesk-händelser i användargränssnittet. Mer information om hur du samlar in händelsedata i Zendesk finns i den officiella dokumentationen:

* [Komma igång med händelser](https://developer.zendesk.com/documentation/custom-data/events/getting-started-with-events/)
* [Zendesk Events API](https://developer.zendesk.com/api-reference/custom-data/events-api/events-api/)
* [Om API:t för händelser](https://developer.zendesk.com/documentation/custom-data/events/about-the-events-api/)
* [Anatomi för en händelse](https://developer.zendesk.com/documentation/custom-data/events/anatomy-of-an-event/)
* [Zendesk-profils-API](https://developer.zendesk.com/api-reference/custom-data/events-api/events-api/#profile-object)
* [Om Profiles API](https://developer.zendesk.com/documentation/custom-data/profiles/about-the-profiles-api/)
* [Anatomi i en profil](https://developer.zendesk.com/documentation/custom-data/profiles/anatomy-of-a-profile/)
