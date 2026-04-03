---
title: Använda identityMap i datainsamling
description: Lär dig hur du skapar och skickar identityMap-nyttolaster för att identifiera kända besökare i olika namnutrymmen i din Web SDK-implementering.
source-git-commit: 696e5098ebf556bfc0fa4fc22ff637cb0835eee0
workflow-type: tm+mt
source-wordcount: '1671'
ht-degree: 0%

---

# Använda identityMap i datainsamling

Nyttolastobjektet `identityMap` är det sätt som du talar om för Edge Network vilka besökare som befinner sig utanför sin enhetsnivå, [ECID](./overview.md). När en besökare loggar in, slutför ett köp eller på annat sätt blir känd, kan du skicka identifierare på personnivå (CRM-ID, hashad e-post, lojalitets-ID osv.) tillsammans med ECID. Dessa identifierare på personnivå ger värdefull information till tjänster i senare led så att de kan

* **Häfta aktivitet till en person över olika enheter och kanaler.** [Identitetstjänsten](/help/identity-service/home.md) länkar identiteterna som du skickar till ett [identitetsdiagram](/help/identity-service/features/identity-graph-viewer.md) och kopplar anonyma beteenden på enhetsnivå till en känd person.
* **Skapa enhetliga kundprofiler.** [Kundprofilen i realtid](/help/profile/home.md) använder den primära identitet som du anger för att förankra händelser och attribut i en enda profil, vilket möjliggör segmentering på personnivå och målgruppsbyggande.
* **Aktivera målgrupper på underordnade mål.** Många [Destinationer](/help/destinations/home.md) kräver matchade identiteter på personnivå (hash-kodade e-postmeddelanden, telefonnummer osv.) för att matcha målgrupperna mot deras användarbaser.
* **Samordna flerkanalsresor.** [Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html) använder lösta identiteter för att utlösa och personalisera resor över e-post-, push- och appkanaler baserat på en besökares autentiserade beteende.

På den här sidan beskrivs hur du skapar `identityMap`-nyttolaster, väljer rätt inställningar för varje identitet och hanterar vanliga implementeringsscenarier.

## Nyttolaststruktur {#structure}

`identityMap` är ett JSON-objekt där varje nyckel på den översta nivån är ett namnutrymme och värdet är en array med identitetsbeskrivare. Du kan inkludera ett eller flera namnutrymmen i en enskild nyttolast och varje beskrivning innehåller tre fält: `id`, `authenticatedState` och `primary`.

```json
{
  "identityMap": {
    "CRMID": [
      {
        "id": "abc-123-xyz",
        "authenticatedState": "authenticated",
        "primary": true
      }
    ]
  }
}
```

| Fält | Typ | Obligatoriskt | Beskrivning |
| --- | --- | --- | --- |
| `id` | Sträng | Ja | Identifierarvärdet (till exempel `user@example.com` eller `ABC123`). |
| `authenticatedState` | Sträng | Ja | Hur tryggt du vet att den här identiteten tillhör besökaren. Giltiga värden är `ambiguous`, `authenticated` och `loggedOut`. |
| `primary` | Boolean | Ja | Anger om den här identiteten ska vara den primära identifieraren för händelsen. Exakt en identitet för alla namnutrymmen måste markeras som `primary: true`. |

Avsnitten nedan täcker varje del av nyttolasten i detalj.

### Namnutrymmesnycklar {#namespace-keys}

Varje nyckel på den översta nivån i `identityMap` är ett [identitetsnamnutrymme](/help/identity-service/features/namespaces.md) - en sträng som klassificerar typen av identifierare (till exempel `CRMID`, `Email`, `Phone` eller `LoyaltyId`). Namnutrymmen måste finnas i identitetstjänsten innan du refererar till dem i en nyttolast. Du kan inkludera flera namnutrymmesnycklar i samma händelse om du har mer än en identifierare för besökaren.

Du behöver inte inkludera ECID som namnutrymmesnyckel. Edge Network lägger automatiskt till ECID till identitetsnyttolasten. Om du inkluderar ECID explicit ska du inte markera det som `primary` när det också finns en identitet på personnivå.

### `id` {#id}

Fältet `id` är själva identifierarsträngen - det värde som talar om för Experience Platform vilken specifik person eller enhet den här identiteten representerar. Varje [identitetsnamnområde](/help/identity-service/features/namespaces.md) förväntar sig ett specifikt värdeformat, och om du skickar ett värde i fel format skapas en distinkt identitet som inte kan sammanfogas med rätt formaterad version, vilket resulterar i fragmenterade profiler.

Innan du tar med ett värde i `identityMap` förbereder du det enligt det format som målnamnutrymmet förväntar sig:

| Vanliga namnområdestyper | Så här förbereder du värdet | Exempel |
| --- | --- | --- |
| **CRM/internt ID** | Använd den exakta identifieraren som systemet för posttilldelningar har. Använd samma format för alla händelser (skiftläge, inledande nollor, prefix). | `ABC-12345`, `00098765` |
| **E-post (råformat)** | Använd gemener för den fullständiga e-postadressen och beskär inledande och avslutande blanksteg. | `user@example.com` |
| **E-post (hashas)** | Gemener och trimma först e-postadressen och hash med SHA-256. Skicka den resulterande hexadecimala strängen på 64 tecken. Lägg inte till ett salt-värde om inte namnutrymmesdefinitionen kräver det. | `a1b2c3d4e5f6a7b8c9...` |
| **Telefon (E.164)** | Formatera talet i [E.164](https://en.wikipedia.org/wiki/E.164): radavstånd `+`, landskoden och prenumerantnumret utan mellanslag eller skiljetecken. | `+15551234567` |
| **FPID** | Generera en [UIDv4](https://datatracker.ietf.org/doc/html/rfc4122)-sträng. Se [enhets-ID:n från första part](./fpid.md) för att se vilka krav som gäller för generering. | `123e4567-e89b-42d3-9456-426614174000` |

En fullständig lista över standardnamnutrymmen och definitioner av dessa finns i [Översikt över identitetsnamnrymden](/help/identity-service/features/namespaces.md#standard).

>[!TIP]
>
>Värdet `id` är skiftlägeskänsligt. `User@Example.com` och `user@example.com` behandlas som två separata identiteter. Normalisera gemener/versaler innan du skickar värdet (vanligtvis genom att minska antalet e-postmeddelanden och trimma mellanrum) för att undvika att skapa duplicerade identiteter i diagrammet.

#### Samlar in `id` vid körning {#collect-id}

Den identifierare du behöver är sällan tillgänglig direkt på sidan. Gemensamma strategier för insamling innefattar:

* **Datalager**: Läs identifieraren från webbplatsens datalager när besökaren har loggat in. Den här platsen är den mest tillförlitliga metoden eftersom datalagret fylls i av programmets serverdel och återspeglar det autentiserade sessionstillståndet.
* **Autentiseringstoken eller sessionscookie**: Avkoda eller slå upp identifieraren från en JWT-fil eller sessionscookie som autentiseringssystemet ställer in. Verifiera att token fortfarande är aktiv innan du använder värdet.
* **Berikning på serversidan**: Använd [Dataprep för datainsamling](/help/datastreams/data-prep.md) eller en [regel för vidarebefordran av händelser](/help/tags/ui/event-forwarding/overview.md) om du vill mappa eller omvandla identifieraren på Edge innan den når underordnade tjänster. Den här platsen är användbar när klienten bara har en ogenomskinlig sessionstoken som mappar till ett internt ID på serversidan.

>[!TIP]
>
>Om ett givet `id`-värde tolkas som en tom sträng, `null` eller `undefined`, ska namnutrymmet inte inkluderas i `identityMap`. Om du skickar en tom `id` skapas en bruten identitetspost. Skydda implementeringen med en kontroll innan du bygger nyttolasten.

### `authenticatedState` {#authenticated-state}

Fältet `authenticatedState` anger för underordnade tjänster hur mycket förtroende som ska placeras i en viss identitet. Följande värden är giltiga för det här fältet:

| Värde | När ska du använda |
| --- | --- |
| **`authenticated`** | Besökaren har aktivt bevisat sin identitet under den aktuella sessionen (till exempel genom att logga in med inloggningsuppgifter, slutföra MFA eller liknande verifiering). |
| **`loggedOut`** | Besökaren autentiserades tidigare men har sedan dess loggat ut. Identiteten är fortfarande associerad med enheten men sessionen är inte längre aktiv. |
| **`ambiguous`** | Det går inte att bekräfta att identiteten tillhör den aktuella besökaren. Använd det här värdet för identifierare på enhetsnivå som FPID eller annan identifierare där autentisering ännu inte har skett. |

>[!TIP]
>
>Värdet `authenticatedState` påverkar hur Adobe Experience Platform Identity Service skapar och sammanfogar identitetsdiagram. Om du skickar `authenticated` för en identitet som inte har verifierats kan det skapa felaktiga länkar mellan enheter som är svåra att ångra.

### `primary` {#primary-identity}

Varje `identityMap`-nyttolast måste ha exakt en identitet markerad som `primary: true`. Den primära identiteten avgör vilken identitet som används som ankarpunkt för händelsen i Experience Platform.

Följ de här riktlinjerna när du anger primär identitet:

* **När en identitet på personnivå är tillgänglig** (besökaren är inloggad) markerar du namnutrymmet på personnivå som primärt och ECID som icke-primärt. Detta anger för Experience Platform att förankra händelsen för personen i stället för enheten.
* **När endast identiteter på enhetsnivå är tillgängliga** (besökaren är anonym) används ECID automatiskt som primär identitet. Du behöver inte inkludera ECID i din `identityMap` - Edge Network lägger till det automatiskt.

```json
{
  "identityMap": {
    "CRMID": [
      {
        "id": "abc-123-xyz",
        "authenticatedState": "authenticated",
        "primary": true
      }
    ],
    "Email": [
      {
        "id": "user@example.com",
        "authenticatedState": "authenticated",
        "primary": false
      }
    ]
  }
}
```

## Skicka identityMap i implementeringen {#send-identity}

>[!BEGINTABS]

>[!TAB JavaScript-bibliotek]

Skicka `identityMap` i `xdm`-objektet för ett [`sendEvent`](/help/collection/js/commands/sendevent/overview.md)-anrop:

```js
alloy("sendEvent", {
  xdm: {
    identityMap: {
      CRMID: [
        {
          id: "abc-123-xyz",
          authenticatedState: "authenticated",
          primary: true
        }
      ]
    },
    eventType: "web.webpagedetails.pageViews"
  }
});
```

>[!TAB Webbtaggtillägg för SDK]

Använd dataelementtypen [Identitetskarta](/help/tags/extensions/client/web-sdk/data-element-types.md#identity-map) för att skapa identitetsnyttolasten i tagggränssnittet:

1. Skapa ett dataelement med tillägget **[!UICONTROL Adobe Experience Platform Web SDK]** och dataelementtypen **[!UICONTROL Identity map]**.
2. Lägg till identiteter genom att ange namnutrymmet, dataelementet eller värdet som matchar identifieraren och det autentiserade läget.
3. Markera en identitet som primär.
4. Referera det här dataelementet i din **[!UICONTROL Send event]**-åtgärd under **[!UICONTROL Identity map]**.

>[!ENDTABS]

## Vanliga scenarier {#common-scenarios}

+++**Inloggning**

När en besökare loggar in skickar du identifieraren på personnivå med `authenticatedState: "authenticated"` och `primary: true`. Inkludera den här identiteten i den första händelsen efter autentisering och i alla efterföljande händelser i sessionen.

```json
{
  "identityMap": {
    "CRMID": [
      {
        "id": "abc-123-xyz",
        "authenticatedState": "authenticated",
        "primary": true
      }
    ]
  }
}
```

+++

+++**Logga ut**

När en besökare loggar ut uppdaterar du `authenticatedState` till `loggedOut` med samma identifierare. Detta bevarar kopplingen mellan enheten och personen samtidigt som det signalerar att sessionen inte längre är aktiv.

```json
{
  "identityMap": {
    "CRMID": [
      {
        "id": "abc-123-xyz",
        "authenticatedState": "loggedOut",
        "primary": false
      }
    ]
  }
}
```

Efter utloggning blir ECID tillbaka till den faktiska primära identiteten (Edge Network använder det automatiskt). Markera inte en annan identitet på personnivå som primär såvida inte besökaren loggar in med ett annat konto.

>[!IMPORTANT]
>
>Sluta inte skicka identifieraren helt efter utloggningen. Om du växlar från `authenticated` till `loggedOut` visas för underordnade tjänster att sessionen har avslutats. Om identifieraren utelämnas blir det ett mellanrum i identitetsdiagrammet som kan orsaka fragmenterade profiler.

+++

+++**Flera namnutrymmen**

Du kan skicka flera identitetsnamnutrymmen i samma händelse. Det här scenariot är vanligt när en besökare är inloggad och du har flera identifierare tillgängliga (till exempel ett CRM-ID, hashad e-post och lojalitets-ID). Inkludera alla kända identifierare, markera bara en som primär och ange de andra till `primary: false`.

```json
{
  "identityMap": {
    "CRMID": [
      {
        "id": "abc-123-xyz",
        "authenticatedState": "authenticated",
        "primary": true
      }
    ],
    "Email_LC_SHA256": [
      {
        "id": "a1b2c3d4e5f6...",
        "authenticatedState": "authenticated",
        "primary": false
      }
    ],
    "LoyaltyId": [
      {
        "id": "LOY-98765",
        "authenticatedState": "authenticated",
        "primary": false
      }
    ]
  }
}
```

>[!TIP]
>
>Om du skickar flera namnutrymmen med samma `authenticatedState` på samma händelse får identitetstjänsten den starkaste signalen för att länka dessa identiteter. Inkludera alla tillgängliga identifierare vid autentiseringstillfället i stället för att sprida dem över olika händelser.

+++

+++**Anonyma besökare**

För anonyma besökare behöver du vanligtvis inte skicka `identityMap` alls. Edge Network tilldelar automatiskt ett ECID och använder det som primär identitet. Om du använder [enhets-ID:n från första part](./fpid.md) är FPID den enda identitet du behöver inkludera för anonyma besökare.

+++

## Hur identityMap påverkar identitetsdiagrammet {#identity-graph}

Varje `identityMap`-nyttolast som når Experience Platform behandlas av [identitetstjänsten](/help/identity-service/home.md) som länkar de identiteter som du skickar till ett [identitetsdiagram](/help/identity-service/features/identity-graph-viewer.md). Vilka namnutrymmen du inkluderar, hur du anger `authenticatedState` och vilken identitet du markerar som `primary`, skapar och sammanfogar identitetstjänsten dessa diagram direkt.

Viktiga beteenden att vara medveten om:

* **Identiteter som skickas för samma händelse länkas tillsammans.** Om du inkluderar ett CRMID och ett e-postnamnområde i samma `sendEvent`-anrop skapar identitetstjänsten en länk mellan dessa två identiteter. Att sprida identifierare över olika händelser ger svagare länkar och kan resultera i fragmenterade diagram.
* **Identiteten `primary` förankrar händelsen i kundprofilen i realtid.Profilen** använder den primära identiteten för att avgöra vilken profil händelsen tillhör. Om du markerar fel identitet som primär (t.ex. anger ECID som primärt när ett ID på personnivå är tillgängligt) kan det leda till att händelser lagras mot profiler på enhetsnivå i stället för profiler på personnivå.
* **Värdet `authenticatedState` påverkar diagramsäkerheten.** Om du skickar `authenticated` för en identitet som inte har verifierats kan det skapa felaktiga länkar mellan enheter som är svåra att ångra. Använd bara `authenticated` när besökaren aktivt har bevisat sin identitet under den aktuella sessionen.

Om din implementering använder [länkningsregler för identitetsdiagram](/help/identity-service/identity-graph-linking-rules/overview.md) (till exempel namnområdesprioritet eller algoritmen för identitetsoptimering) kan du läsa [implementeringsguiden](/help/identity-service/identity-graph-linking-rules/implementation-guide.md) för att förstå hur dessa regler interagerar med de identiteter du skickar via `identityMap`.

>[!NOTE]
>
>`identityMap` skickas endast när webb-SDK skickar en begäran till Edge Network, som baseras på besökarens samtycke. Om din implementering använder `defaultConsent: "pending"` skickas inte identiteter förrän du har gett ditt medgivande. Mer information finns i [Medgivande och identitet](./consent.md).
