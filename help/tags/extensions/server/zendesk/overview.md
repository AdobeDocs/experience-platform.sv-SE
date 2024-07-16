---
title: Tillägg för vidarebefordran av Zendesk-händelse
description: Zendesk-tillägg för händelsevidarebefordran för Adobe Experience Platform.
exl-id: 22e94699-5b84-4a73-b007-557221d3e223
source-git-commit: d81c4c8630598597ec4e253ef5be9f26c8987203
workflow-type: tm+mt
source-wordcount: '1162'
ht-degree: 1%

---

# Översikt över tillägget [!DNL Zendesk] för API:t för händelser

[Zendesk](https://www.zendesk.com) är en kundtjänst och ett säljverktyg. Tillägget [[!DNL Zendesk Events API]](https://developer.zendesk.com/documentation/ticketing/events/about-the-events-api/) används för att skicka händelser från Adobe Experience Platform Edge Network till Zendesk för vidare bearbetning, vilket innebär att händelsen [vidarebefordras](../../../ui/event-forwarding/overview.md). Du kan använda tillägget för att samla in interaktioner med kundprofiler för användning i analyser och åtgärder längre fram i kedjan.

Det här dokumentet beskriver hur du installerar och konfigurerar tillägget i användargränssnittet.

## Förhandskrav

Du måste ha ett Zendesk-konto för att kunna använda det här tillägget. Du kan registrera dig för ett Zendesk-konto på [Zendesk-webbplatsen](https://www.zendesk.com/register/).

Du måste även samla in följande information för din Zendesk-konfiguration:

| Nyckeltyp | Beskrivning | Exempel |
| --- | --- | --- |
| Underdomän | Under registreringsprocessen skapas en unik **underdomän** som är specifik för kontot. Mer information finns i [Zendesk-dokumentationen](https://developer.zendesk.com/documentation/ticketing/working-with-oauth/creating-and-using-oauth-tokens-with-the-api/). | `xxxxx.zendesk.com` (där `xxxxx` är värdet som angavs när kontot skapades) |
| API-token | Zendesk använder bearer-tokens som en autentiseringsmekanism för att kommunicera med Zendesk API. Generera en API-token när du har loggat in på Zendesk-portalen. Mer information finns i [Zendesk-dokumentationen](https://support.zendesk.com/hc/en-us/articles/4408889192858-Generating-a-new-API-token). | `cwWyOtHAv12w4dhpiulfe9BdZFTz3OKaTSzn2QvV` |

{style="table-layout:auto"}

Slutligen måste du skapa en händelsevidarebefordringshemlighet för API-token. Ange den hemliga typen till **[!UICONTROL Token]** och ange värdet till den API-token som du samlade in från din Zendesk-konfiguration. Mer information om hur du konfigurerar hemligheter finns i dokumentationen om [hemligheter i händelsevidarebefordran](../../../ui/event-forwarding/secrets.md).

## Installera tillägget {#install}

Om du vill installera Zendesk-tillägget i användargränssnittet går du till **Vidarebefordra händelser** och väljer en egenskap som tillägget ska läggas till i. Du kan också skapa en ny egenskap i stället.

När du har markerat eller skapat den önskade egenskapen går du till **Tillägg** > **Katalog**. Sök efter [!DNL Zendesk] och välj sedan **[!DNL Install]** i Zendesk-tillägget.

![Installationsknappen för Zendesk-tillägget som väljs i användargränssnittet](../../../images/extensions/server/zendesk/install.png)

## Konfigurera tillägget {#configure}

>[!IMPORTANT]
>
>Beroende på ditt implementeringsbehov kan du behöva skapa ett schema, dataelement och en datauppsättning innan du konfigurerar tillägget. Granska alla konfigurationssteg innan du startar för att avgöra vilka enheter du måste konfigurera för ditt användningsfall.

Välj **Tillägg** i den vänstra navigeringen. Under **Installerad** väljer du **Konfigurera** i Zendesk-tillägget.

![Konfigurera-knappen för Zendesk-tillägget som väljs i användargränssnittet](../../../images/extensions/server/zendesk/configure.png)

Under **[!UICONTROL Zendesk Domain]** anger du värdet för din Zendesk-underdomän. Under **[!UICONTROL Zendesk Token]** väljer du den hemlighet som du skapade tidigare och som innehåller API-token.

![Konfigurationsalternativen är ifyllda i användargränssnittet](../../../images/extensions/server/zendesk/input.png)

## Konfigurera en regel för vidarebefordran av händelser

Börja skapa en ny regel för vidarebefordran av händelse [regel](../../../ui/managing-resources/rules.md) och konfigurera villkoren efter behov. När du väljer åtgärder för regeln väljer du tillägget [!UICONTROL Zendesk] och sedan åtgärdstypen [!UICONTROL Create Event].

![Definiera regel](../../../images/extensions/server/zendesk/rule.png)

När du konfigurerar åtgärdskonfigurationen uppmanas du att tilldela dataelement till de olika egenskaper som ska skickas till Zendesk.

![Definiera åtgärdskonfiguration](../../../images/extensions/server/zendesk/action-configurations.png)

Dessa dataelement ska mappas enligt nedan.

### `event` tangenter

`event` är ett JSON-objekt som representerar den händelse som utlöses av användaren. Se Zendesk-dokumentet på [anatomin för en händelse](https://developer.zendesk.com/documentation/ticketing/events/anatomy-of-an-event/) om du vill ha mer information om egenskaperna som har hämtats av `event`-objektet.

Följande nycklar kan refereras inom objektet `event` vid mappning till dataelement:

| `event`-tangenten | Typ | Plattformssökväg | Beskrivning | Obligatoriskt | Gränser |
| --- | --- | --- | --- | --- | --- |
| `source` | Sträng | `arc.event.xdm._extconndev.event_source` | Programmet som skickade händelsen. | Ja | Använd inte `Zendesk` som ett värde eftersom det är ett skyddat källnamn för Zendesk-standardhändelser. Försök att använda den kommer att resultera i ett fel.<br>Värdet får inte vara längre än 40 tecken. |
| `type` | Sträng | `arc.event.xdm._extconndev.event_type` | Ett namn för händelsetypen. Du kan använda det här fältet för att ange olika typer av händelser för en viss källa. Du kan till exempel skapa en uppsättning händelser för användarinloggningar och en annan för kundvagnar. | Ja | Värdet får inte vara längre än 40 tecken. |
| `description` | Sträng | `arc.event.xdm._extconndev.description` | En beskrivning av händelsen. | Nej | (Ej tillämpligt) |
| `created_at` | Sträng | `arc.event.xdm.timestamp` | En ISO-8601-tidsstämpel som visar när händelsen skapades. | Nej | (Ej tillämpligt) |
| `properties` | Objekt | `arc.event.xdm._extconndev.EventProperties` | Ett anpassat JSON-objekt med information om händelsen. | Ja | (Ej tillämpligt) |

{style="table-layout:auto"}

>[!NOTE]
>
>Mer information om händelseegenskaper finns i [[!DNL Zendesk Events API] dokumentationen](https://developer.zendesk.com/documentation/ticketing/events/about-the-events-api/).

### `profile` tangenter

`profile` är ett JSON-objekt som representerar användaren som utlöste händelsen. Mer information om egenskaperna som har hämtats av objektet `profile` finns i Zendesk-dokumentet på [anatomin för en profil](https://developer.zendesk.com/documentation/ticketing/profiles/anatomy-of-a-profile/).

Följande nycklar kan refereras inom objektet `profile` vid mappning till dataelement:

| `profile`-tangenten | Typ | Plattformssökväg | Beskrivning | Obligatoriskt | Gränser |
| --- | --- | --- | --- | --- | --- |
| `source` | Sträng | `arc.event.xdm._extconndev.profile_source` | Produkten eller tjänsten som är associerad med profilen, till exempel `Support`, `CompanyName` eller `Chat`. | Ja | (Ej tillämpligt) |
| `type` | Sträng | `arc.event.xdm._extconndev.profile_type` | Ett namn för profiltypen. Du kan använda det här fältet för att skapa olika typer av profiler för en viss källa. Du kan till exempel skapa en uppsättning företagsprofiler för kunder och en annan för anställda. | Ja | Profiltypens längd får inte överstiga 40 tecken. |
| `name` | Sträng | `arc.event.xdm._extconndev.name` | Namnet på personen från profilen | Nej | (Ej tillämpligt) |
| `user_id` | Sträng | `arc.event.xdm._extconndev.user_id` | Personens användar-ID i Zendesk. | Nej | (Ej tillämpligt) |
| `identifiers` | Array | `arc.event.xdm._extconndev.identifiers` | En array som innehåller minst en identifierare. Varje identifierare består av en typ och ett värde. | Ja | Mer information om `identifiers`-arrayen finns i [Zendesk-dokumentationen](https://developer.zendesk.com/api-reference/ticketing/users/profiles_api/profiles_api/#identifiers-array). Alla fält och värden måste vara unika. |
| `attributes` | Objekt | `arc.event.xdm._extconndev.attrbutes` | Ett objekt som innehåller användardefinierade egenskaper för personen. | Nej | Mer information om profilattribut finns i [Zendesk-dokumentationen](https://developer.zendesk.com/documentation/ticketing/profiles/anatomy-of-a-profile/#attributes). |

{style="table-layout:auto"}

## Validera data i Zendesk {#validate}

Om händelseinsamlingen och Adobe Experience Platform-integreringen lyckas visas händelserna i Zendesk-konsolen enligt nedan. Detta indikerar en lyckad integrering.

Profiler:

![Sidan Zendesk-profiler](../../../images/extensions/server/zendesk/zendesk-profiles.png)

Händelser:

![Sidan Zendesk Events](../../../images/extensions/server/zendesk/zendesk-events.png)

## Begärandebegränsningar {#limits}

Baserat på kontotypen kan Zendesk [!DNL Events API] hantera följande antal begäranden per minut:

| [!DNL Account Type] | Begäranden per minut |
| --- | --- |
| [!DNL Team] | 250 |
| [!DNL Growth] | 250 |
| [!DNL Professional] | 500 |
| [!DNL Enterprise] | 750 |
| [!DNL Enterprise Plus] | 1000 |

{style="table-layout:auto"}

Mer information om dessa begränsningar finns i [Zendesk-dokumentationen](https://developer.zendesk.com/api-reference/ticketing/account-configuration/usage_limits/#:~:text=API%20requests%20made%20by%20Zendesk%20apps%20are%20subject,sources%20for%20the%20account%2C%20including%20internal%20product%20requests.).

## Fel och felsökning {#errors-and-troubleshooting}

När tillägget används eller konfigureras kan felen nedan returneras av Zendesk Events-API:

| Felkod | Beskrivning | Upplösning | Exempel |
|---|---|---|---|
| 400 | **Ogiltig profillängd:** Det här felet inträffar när längden på ett profilattribut innehåller mer än 40 tecken. | Begränsa längden på profilattributsdata till högst 40 tecken. | `{"error": [{"code":"InvalidProfileTypeLength","title": "Profile type length > 40 chars"}]}` |
| 401 | **Det gick inte att hitta vägen:** Det här felet inträffar när en ogiltig domän har angetts. | Kontrollera att en giltig domän har angetts i följande format: `{subdomain}.zendesk.com` | `{"error": [{"description": "No route found for host {subdomain}.zendesk.com","title": "RouteNotFound"}]}` |
| 401 | **Ogiltig eller saknad autentisering:** Det här felet inträffar när åtkomst till token är ogiltig, saknas eller har upphört att gälla. | Kontrollera att åtkomsttoken är giltig och inte har gått ut. | `{"error": [{"code":"MissingOrInvalidAuthentication","title": "Invalid or Missing Authentication"}]}` |
| 403 | **Otillräckliga behörigheter:** Det här felet inträffar när det inte finns tillräcklig behörighet för att komma åt resursen. | Verifiera att de nödvändiga behörigheterna har angetts. | `{"error": [{"code":"PermissionDenied","title": "Insufficient permisssions to perform operation"}]}` |
| 429 | **För många begäranden:** Det här felet inträffar när postgränsen för slutpunktsobjekt har överskridits. | Mer information om tröskelvärden per gräns finns i avsnittet ovan om [begärandegränser](#limits). | `{"error": [{"code":"TooManyRequests","title": "Too Many Requests"}]}` |

{style="table-layout:auto"}

## Nästa steg

I det här dokumentet beskrivs hur du installerar och konfigurerar tillägget för vidarebefordran av Zendesk-händelser i användargränssnittet. Mer information om hur du samlar in händelsedata i Zendesk finns i den officiella dokumentationen:

* [Komma igång med händelser](https://developer.zendesk.com/documentation/ticketing/events/getting-started-with-events/)
* [Zendesk Events-API](https://developer.zendesk.com/api-reference/ticketing/users/events-api/events-api/)
* [Om API:t för händelser](https://developer.zendesk.com/documentation/ticketing/events/about-the-events-api/)
* [Anatomi för en händelse](https://developer.zendesk.com/documentation/ticketing/events/anatomy-of-an-event/)
* [Zendesk-profils-API](https://developer.zendesk.com/api-reference/ticketing/users/events-api/events-api/#profile-object)
* [Om Profiles-API:t](https://developer.zendesk.com/documentation/ticketing/profiles/about-the-profiles-api/)
* [Anatomi för en profil](https://developer.zendesk.com/documentation/ticketing/profiles/anatomy-of-a-profile/)
