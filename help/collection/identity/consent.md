---
title: Medgivande och identitet i datainsamling
description: Förstå hur samtycke påverkar identitetsbeteendet i Web SDK-implementeringar, inklusive ECID-generering, cookie-beständighet och besökares kontinuitet.
source-git-commit: 696e5098ebf556bfc0fa4fc22ff637cb0835eee0
workflow-type: tm+mt
source-wordcount: '1149'
ht-degree: 0%

---

# Medgivande och identitet i datainsamling

Samtycke och identitet är nära sammankopplade i Web SDK-implementeringar. Hur och när du samlar in ditt samtycke påverkar direkt när och om Web SDK genererar ett ECID, ställer in identitetscookies och skickar data till Edge Network. När samtycke inte hanteras med omsorg blir resultatet ofta oväntad besöksinflammation, luckor i identitetskontinuiteten eller både och.

På den här sidan beskrivs hur medgivandeval interagerar med identitetsbeteenden och ger vägledning för hur du konfigurerar implementeringen för att undvika vanliga fallgropar. Bakgrund om hur Web SDK hanterar ECID:n, FPID:n och andra identitetssignaler finns i [Identitet i datainsamling](./overview.md).

## Hur samtycke påverkar identitet {#how-consent-affects-identity}

Web SDK använder både konfigurationsvariabeln [`defaultConsent`](/help/collection/js/commands/configure/defaultconsent.md) och kommandot [`setConsent`](/help/collection/js/commands/setconsent.md) för att kontrollera om data skickas till Edge Network. Medgivandestatus avgör direkt när ett ECID genereras och när identitetscookies ställs in.

I följande tabell visas den kombinerade effekten av `defaultConsent` och `setConsent` på datainsamling, cookie-inställning och identitetsbeteende.

| `defaultConsent` | `setConsent` | Datainsamling sker | Webbläsarcookies | Identitetsbeteende |
| --- | --- | --- | --- | --- |
| `in` | Ej angiven | Ja | Ja | Ett ECID genereras omedelbart vid den första begäran. Identitetskakor anges vid sidinläsning. |
| `in` | `in` | Ja | Ja | Besökarens befintliga ECID bevaras. Identitetsbeteendet är oförändrat. |
| `in` | `out` | Nej | Ja | Datainsamlingen stoppas. Befintliga ECID- och `kndctr_`-identitetscookies finns kvar i webbläsaren tills de upphör att gälla. |
| `pending` | Ej angiven | Nej | Nej | Inget ECID genereras. Inga cookies har angetts. Händelser köas lokalt tills `setConsent` anropas. |
| `pending` | `in` | Ja | Ja | Händelser som står i kö skickas. Ett ECID genereras för den första begäran och identitetscookies ställs in. |
| `pending` | `out` | Nej | Ja | Händelser i kö ignoreras. Inget ECID genereras. Medgivandecookien är inställd på att registrera besökarens önskemål. |
| `out` | Ej angiven | Nej | Nej | Inget ECID genereras. Inga cookies har angetts. Inga händelser skickas. |
| `out` | `in` | Ja | Ja | Ett ECID genereras för den första begäran och identitetscookies ställs in. |
| `out` | `out` | Nej | Ja | Inget ECID genereras. Medgivandecookien är inställd på att registrera besökarens önskemål. |

>[!NOTE]
>
>Identitets- och medgivandecookies anges även när en besökare avanmäler sig. Dessa cookies är nödvändiga för att uppfylla besökarens inställningar för datainsamling. Se [Webbcookies för SDK](https://experienceleague.adobe.com/sv/docs/core-services/interface/data-collection/cookies/web-sdk) för en fullständig lista över cookies som anges av Web SDK.

När en besökare återger sitt samtycke efter att tidigare ha återkallat det (genom att anropa `setConsent` med `"general": "in"` efter `"general": "out"`), fortsätter Web SDK att skicka händelser och använder det befintliga ECID:t från cookien om det inte har gått ut. Besökarens identitet bevaras.

När en besökare har gett eller nekat sitt samtycke, kommer Web SDK att behålla sin inställning i en cookie för `kndctr_`-samtycke. Vid efterföljande sidinläsningar läser SDK in denna cookie och tillämpar den lagrade inställningen automatiskt - du behöver inte anropa `setConsent` igen om inte besökarens inställning ändras. Observera att konfigurationsvärdet `defaultConsent` inte finns kvar mellan sidinläsningar, men besökarens lösta samtycke (som anges via `setConsent`) gör det.

>[!NOTE]
>
>Händelser som står i kö när medgivandet är `pending` finns i minnet och överlever inte sidinläsningar. Om en besökare navigerar till en ny sida innan medgivandet har lösts, går händelser i kö från föregående sida förlorade.

## Implementeringsmönster {#implementation-patterns}

### Modell för anmälan (samtycke krävs före insamling) {#opt-in}

Använd det här mönstret när bestämmelser (som GDPR) kräver uttryckligt medgivande innan data samlas in.

```js
alloy("configure", {
  orgId: "YOUR_ORG_ID@AdobeOrg",
  edgeDomain: "data.example.com",
  defaultConsent: "pending"
});

// When the visitor grants consent:
alloy("setConsent", {
  consent: [{
    standard: "Adobe",
    version: "1.0",
    value: { general: "in" }
  }]
});
```

Med detta mönster:
* Inget ECID genereras förrän medgivande beviljas.
* Händelser som utlöses innan samtycke (t.ex. den inledande sidvyn) köas och skickas när samtycke har beviljats.
* Identity cookies anges först efter den första lyckade Edge Network-begäran.

### Modell för avanmälan (samling som standard, stopp vid nekande) {#opt-out}

Använd det här mönstret när reglerna tillåter datainsamling som standard med ett alternativ att välja bort.

```js
alloy("configure", {
  orgId: "YOUR_ORG_ID@AdobeOrg",
  edgeDomain: "data.example.com",
  defaultConsent: "in"
});

// If the visitor opts out:
alloy("setConsent", {
  consent: [{
    standard: "Adobe",
    version: "1.0",
    value: { general: "out" }
  }]
});
```

Med detta mönster:
* Ett ECID genereras omedelbart vid första sidinläsningen.
* Alla händelser skickas tills besökaren avanmäler sig.
* När du har avanmält dig slutar Web SDK skicka händelser, men befintliga cookies finns kvar.

## Samtycke med enhets-ID:n från första part {#consent-with-fpids}

Om implementeringen använder [FPID:n (First-party device ID:n)](./fpid.md) anges FPID-cookien av servern oberoende av Web SDK-medgivandetillståndet. FPID-cookie är en identifierare som du hanterar på din egen infrastruktur. FPID skickas dock endast till Edge Network när webb-SDK skickar en begäran (som skapas genom samtycke):

* Med `defaultConsent: "pending"` finns FPID:t i webbläsaren, men används inte för att skicka ett ECID förrän medgivande har beviljats.
* Med `defaultConsent: "in"` används FPID på den första begäran och ECID-numret skickas omedelbart.

Om implementeringen av ditt samtycke kräver att ingen identifierare anges före samtycke, fördröjs inställningen av FPID-cookie tills efter att samtycke har skickats. Enbart SDK-samtycke förhindrar inte att FPID-cookien ställs in eftersom den hanteras av servern.

## Vanliga fallgropar {#common-pitfalls}

+++**Medgivandebanderoll rensar identitetscookies**

**Problem**: På vissa CMP-plattformar (Medgivandehanteringsplattformar) rensas alla cookies - inklusive `kndctr_` identitetscookies - när medgivandebanderollen presenteras, innan besökaren gör ett val. När besökaren ger sitt samtycke genererar Web SDK ett nytt ECID eftersom det föregående togs bort. Besökaren visas som en ny person i rapporteringen.

**Symtomen**:
* En topp i antalet unika besökare efter att ha driftsatt en banner för samtycke.
* Återkommande besökare räknas som nya besökare varje gång deras samtycke upphör och de interagerar med banderollen igen.

**Lösning**: Konfigurera din CMP för att bevara `kndctr_` cookies. Dessa cookies är identitetscookies, inte spårning av cookies, utan identifierar enheten och innehåller inga beteendedata. Om din CMP kräver att du rensar cookies lägger du till `kndctr_` prefix-cookies i en exkluderingslista. Alternativt kan du fördröja rensningen av cookies tills besökaren uttryckligen nekar samtycke i stället för att ta bort dem i förväg.

+++

+++**Fördröjt samtycke orsakar dubblettidentitet**

**Problem**: När `defaultConsent` är inställt på `pending` väntar Web SDK på godkännande innan data skickas. Om samtycke beviljas sent under sidans livscykel (till exempel efter en banderollinteraktion som utlöser en sidinläsning) kan följande sekvens orsaka problem:

1. Sidan läses in. `defaultConsent: "pending"`. Web SDK skickar inga begäranden.
2. Besökaren ger sitt samtycke. CMP utlöser en sidomladdning.
3. Sidan läses in igen. Web SDK initierar nu med medgivande och genererar ett ECID.

Detta flöde är normalt och fungerar korrekt. Problemet uppstår när CMP eller din implementering av misstag rensar cookies mellan steg 2 och 3, eller när webb-SDK konfigureras annorlunda vid omladdningen.

**Lösning**: Kontrollera att Web SDK-konfigurationen (särskilt `orgId` och `defaultConsent`) är identisk vid varje sidinläsning. Om din CMP utlöser en återinläsning efter samtycke, kontrollerar du att identitetscookies överlever återinläsningen.

+++

+++**Använda `defaultConsent: "in"` med en medgivandebanderoll**

**Problem**: Vissa implementeringar har angetts `defaultConsent: "in"` och anropar sedan `setConsent` med `"general": "out"` om besökaren avvisar. Detta tillvägagångssätt genererar ett ECID och skickar minst en begäran innan samtycke nekas. Beroende på dina lagstadgade krav kanske denna första datainsamling inte är anpassad till organisationens sekretesspolicy.

**Lösning**: Om din myndighetsmiljö kräver samtycke före datainsamling eller ECID-generering använder du `defaultConsent: "pending"` i stället. Den här inställningen säkerställer att Web SDK inte kommunicerar med Edge Network förrän medgivande uttryckligen ges.

+++
