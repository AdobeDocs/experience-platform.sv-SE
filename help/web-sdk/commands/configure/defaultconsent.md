---
title: defaultConsent
description: Ange standardmetoden för insamling av samtycke för din webbegenskap.
exl-id: 2a22fa8b-a234-4d3e-9b55-c7482a928fe6
source-git-commit: 8fc0fd96f13f0642f7671d0e0f4ecfae8ab6761f
workflow-type: tm+mt
source-wordcount: '783'
ht-degree: 0%

---


# `defaultConsent`

Egenskapen `defaultConsent` avgör hur du hanterar datainsamlingssamtycke innan du anropar kommandot [`setConsent`](../setconsent.md). Den här egenskapen är värdefull när du inte av misstag vill samla in data från personer som bor i områden där samtycke krävs innan data samlas in.

Som standard är användarna inställda för alla syften och Web SDK tillåts utföra följande uppgifter:

* Skicka data till och från Adobe-servrar.
* Läs och skriv cookies eller webblagringsobjekt.

Om användaren avanmäler sig från alla syften utför inte Web SDK någon av dessa åtgärder.

Egenskapen `defaultConsent` har stöd för tre värden:

* **`in`**: Datainsamlingen fortsätter som vanligt tills användaren avanmäler sig.
* **`out`**: Data ignoreras permanent tills användaren väljer att gå in.
* **`pending`**: Data lagras lokalt tills användaren väljer att använda kommandot [`setConsent`](../setconsent.md). När standardmedgivandet för det allmänna syftet har angetts till `pending`, kommer ett försök att köra kommandon som är beroende av användarens inställningar för deltagande (till exempel kommandot [`sendEvent`](../sendevent/overview.md)) att resultera i att kommandot köas i Web SDK. Kommandon som står i kö bearbetas inte förrän du har meddelat användarens inställningar för deltagande till Web SDK.

>[!NOTE]
>
> Samtyckesdata bevaras inte mellan sidinläsningar.

Om du har en besökare som inte omfattas av den allmänna dataskyddsförordningen (GDPR) kan standardmedgivandet anges till `in`. Besökare inom GDPR:s jurisdiktion kan ha sitt standardsamtycke inställt på `pending`. Din CMP (Consent Management Platform) kan identifiera kundens region och ange flaggan `gdprApplies` till IAB TCF 2.0. Den här flaggan kan användas för att ange standardsamtycke.

Om du inte vill samla in händelser som inträffat innan användarens inställningar för deltagande har angetts, kan du skicka `"defaultConsent": "out"` under Web SDK-konfigurationen. Försök att köra kommandon som är beroende av användarens inställningar för deltagande kommer inte att ha någon effekt förrän du har meddelat användarens inställningar för deltagande till Web SDK.

>[!NOTE]
>
>För närvarande stöder Web SDK endast ett enda syfte med allt eller inget. Även om vi planerar att bygga ut en mer robust uppsättning syften eller kategorier som motsvarar de olika möjligheterna och produkterbjudandena för Adobe, är den nuvarande implementeringen en strategi där man väljer att inte göra något.  Detta gäller endast [!DNL Web SDK] och INTE andra Adobe JavaScript-bibliotek.

## Använder `defaultConsent` tillsammans med `setConsent` {#using-consent}

Web SDK har två extra konfigurationskommandon för samtycke:

* [`defaultConsent`](defaultconsent.md): Det här kommandot är avsett att fånga upp medgivandepreferenser för Adobe-kunder med hjälp av Web SDK.
* [`setConsent`](../setconsent.md): Det här kommandot är avsett att fånga upp webbplatsbesökarnas medgivandeinställningar.

När de används tillsammans kan de här inställningarna leda till olika resultat för datainsamling och cookie-inställning, beroende på deras konfigurerade värden.

Se tabellen nedan för att förstå när datainsamling sker och när cookies ställs in, baserat på inställningar för samtycke.

| defaultConsent | setConsent | Datainsamling sker | Webb-SDK anger webbläsarcookies |
|---------|----------|---------|---------|
| `in` | `in` | Ja | Ja |
| `in` | `out` | Nej | Ja |
| `in` | Ej angiven | Ja | Ja |
| `pending` | `in` | Ja | Ja |
| `pending` | `out` | Nej | Ja |
| `pending` | Ej angiven | Nej | Nej |
| `out` | `in` | Ja | Ja |
| `out` | `out` | Nej | Ja |
| `out` | Ej angiven | Nej | Nej |

Följande cookies anges när medgivandekonfigurationen tillåter:

| Namn | Maximal ålder | Beskrivning |
|---|---|---|
| **AMCV_###@AdobeOrg** | 34128000 (395 dagar) | Visas när [`idMigrationEnabled`](../configure/idmigrationenabled.md) är aktiverat. Det är till hjälp vid övergång till Web SDK medan vissa delar av webbplatsen fortfarande använder `visitor.js`. |
| **Demdex-cookie** | 15552000 (180 dagar) | Visas om ID-synkronisering är aktiverat. Audience Manager ställer in denna cookie så att den tilldelar ett unikt ID till en besökare. Demdex-cookie hjälper Audience Manager att utföra grundläggande funktioner som besökaridentifiering, ID-synkronisering, segmentering, modellering, rapportering och så vidare. |
| **kndctr_orgid_Cluster** | 1 800 (30 minuter) | Lagrar det Edge Network-område som betjänar den aktuella användarens begäran. Regionen används i URL-sökvägen så att Edge Network kan dirigera begäran till rätt region. Om en användare ansluter till en annan IP-adress eller i en annan session dirigeras begäran igen till närmaste region. |
| **kndct_orgid_identity** | 34128000 (395 dagar) | Lagrar ECID samt annan information som rör ECID. |
| **kndctr_orgid_medgivande** | 15552000 (180 dagar) | Lagrar användarens medgivandeinställning för webbplatsen. |
| **s_ecid** | 63115200 (två år) | Innehåller en kopia av Experience Cloud-ID ([!DNL ECID]) eller MID. MID lagras i ett nyckel/värde-par som följer syntaxen `s_ecid=MCMID\|<ECID>`. |

## Ange standardsamtycke med hjälp av taggtillägget Web SDK

Välj önskad alternativknapp under **[!UICONTROL Default consent]** när [taggtillägget ](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md) konfigureras.

1. Logga in på [experience.adobe.com](https://experience.adobe.com) med dina Adobe ID-inloggningsuppgifter.
1. Navigera till **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Välj önskad taggegenskap.
1. Navigera till **[!UICONTROL Extensions]** och klicka sedan på **[!UICONTROL Configure]** på [!UICONTROL Adobe Experience Platform Web SDK]-kortet.
1. Bläddra ned till avsnittet [!UICONTROL Privacy] och markera sedan önskad **[!UICONTROL Default consent]**.
1. Klicka på **[!UICONTROL Save]** och publicera sedan ändringarna.

## Ange standardsamtycke med hjälp av JavaScript-biblioteket för Web SDK

Ange strängegenskapen `defaultConsent` till önskad medgivandenivå när du kör kommandot `configure`. Den här egenskapen är skiftlägeskänslig och stöder endast följande tre värden: `"in"`, `"out"` och `"pending"`. Om du försöker använda något annat värde genereras ett fel i biblioteket.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  defaultConsent: "pending"
});
```
