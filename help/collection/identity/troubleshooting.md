---
title: Felsöka identitet i datainsamling
description: Diagnostisera vanliga identitetsproblem i Web SDK-implementeringar, inklusive inflationsförändringar hos besökare, ECID-inkonsekvenser, cookie-konflikter och FPID-problem.
source-git-commit: 696e5098ebf556bfc0fa4fc22ff637cb0835eee0
workflow-type: tm+mt
source-wordcount: '1034'
ht-degree: 0%

---

# Felsöka identitet i datainsamling

Identitetsproblem uppstår ofta som symtom i efterföljande rapporter (uppblåst besökarantal, fragmenterade profiler eller trasig personalisering) snarare än som fel i själva implementeringen. På den här sidan kan du diagnostisera och lösa de vanligaste identitetsproblemen i Web SDK-implementeringar. Bakgrund om hur identiteter fungerar i datainsamling finns i [identitetöversikten](./overview.md).

## Inspektera identitetsvärden {#inspect-identity}

Innan du felsöker ett specifikt problem bör du hämta de aktuella identitetsvärden som används av Web SDK. Använd kommandot [`getIdentity`](/help/collection/js/commands/getidentity.md) för att visa ECID och andra identitetssignaler:

```js
alloy("getIdentity", { namespaces: ["ECID", "CORE"] }).then(function(result) {
  console.log("ECID:", result.identity.ECID);
  console.log("CORE ID:", result.identity.CORE);
  console.log("Edge region:", result.edge.regionID);
});
```

Du kan också kontrollera identitetsvärden i webbläsarens utvecklingsverktyg:

1. Öppna fliken **Program** (Chrome/Edge) eller fliken **Lagring** (Firefox/Safari).
2. Leta efter cookies som har prefixats med `kndctr_` på din domän. Cookien `kndctr_<ORG_ID>_AdobeOrg_identity` innehåller ECID.
3. Öppna fliken **Nätverk** och sök efter en `interact` - eller `collect` -förfrågan till Edge Network. Granska nyttolasten för begäran för `identityMap` och svarsnyttolasten för identitetshandtag.

## Vanliga problem {#common-issues}

+++**Inflammation för antal besökare**

**Symptom**: Analysrapporter visar fler unika besökare än förväntat, eller så visas samma person som flera besökare mellan sessioner.

**Möjliga orsaker**:

| Orsak | Identifiera | Upplösning |
| --- | --- | --- |
| Kort cookie-livstid | Kontrollera förfallotiden för `kndctr_` cookies i webbläsaren. Om de upphör att gälla inom 7 dagar eller mindre begränsar webbläsarreglerna troligtvis cookie-varaktighet. | Implementera [FPID:n (First-party device ID:n)](./fpid.md) som angetts från en server med en DNS A/AAAA-post för längre cookie-beständighet. |
| FPID saknas för första begäran | Granska den första Edge Network-förfrågan vid sidinläsning. Om det inte finns någon FPID-cookie genererar Edge Network ett nytt ECID. Om FPID anges efter den första begäran blir det ECID som skapades för den första begäran överblivet. | Ställ in FPID-cookie innan webbservern SDK skickar sin första begäran. Se [När cookien ska anges](./fpid.md#when-to-set-cookie). |
| `orgId` matchar inte mellan domäner | Jämför `orgId`-konfigurationsvärdet i alla domäner. Felmatchade värden orsakar separata identitetsomfattningar. | Använd samma [`orgId`](/help/collection/js/commands/configure/orgid.md) på alla domäner i organisationen. |
| Banderoll för godkännande tar bort cookies | Om implementeringen av ditt samtycke rensar alla cookies innan samtycke beviljas och sedan webbversionen av SDK initieras, genereras ett nytt ECID. | Konfigurera din medgivandebanderoll så att `kndctr_` cookies bevaras eller så fördröjs initieringen av Web SDK tills du har godkänt detta. Se även [Medgivande och identitet](./consent.md). |
| JavaScript-set FPID cookies | Cookies som anges med `document.cookie` omfattas av webbläsarbegränsningar (ITP, ETP) som begränsar deras livstid, ibland till så lite som 24 timmar. | Ange FPID-cookies från servern med en DNS A/AAA-post, inte från JavaScript. |

+++

+++**ECID ändras oväntat mellan sidor**

**Symptom**: ECID är olika på olika sidor i samma domän, eller ändringar på varje sida som läses in.

**Diagnostiksteg**:

1. Bekräfta att identitetscookien `kndctr_` finns på båda sidorna. Om det saknas på en sida kontrollerar du att Web SDK är konfigurerat på den sidan.
2. Kontrollera att cookie-domänen är tillräckligt stor. En cookie som har angetts för `shop.example.com` är inte tillgänglig på `www.example.com`. Se till att infrastrukturen för första parts insamling och cookie-inställning använder samma domänomfång.
3. Sök efter JavaScript som rensar cookies i navigering (till exempel aggressiva cookie-medgivande-skript eller sekretessverktyg).
4. Om du använder ett ensidigt program bör du kontrollera att Web SDK har konfigurerats en gång vid appinitieringen, och inte initieras om vid varje vägändring. Ominitiering kan generera ett nytt ECID.

+++

+++**FPID skickar inte ECID**

**Symptom**: Du har angett en FPID-cookie, men `getIdentity` returnerar ett ECID som inte är konsekvent vid alla besök, eller så visas inte FPID vid nyttolaster för Edge Network-begäranden.

**Diagnostiksteg**:

1. **Verifiera FPID-cookie-formatet**: FPID måste vara ett giltigt [UIDv4](https://datatracker.ietf.org/doc/html/rfc4122). Öppna webbläsarens utvecklarverktyg, sök efter FPID-cookien och bekräfta att värdet matchar mönstret `xxxxxxxx-xxxx-4xxx-yxxx-xxxxxxxxxxxx`.
2. **Kontrollera cookie-namnet i datastream**: Om du använder cookie-metoden [datastream](./fpid.md#setting-cookie-datastreams) måste det cookie-namn som är konfigurerat i datastream exakt matcha namnet på den cookie som servern anger.
3. **Bekräfta att cookien skickas på begäran**: Gå till fliken Nätverk och kontrollera rubriken `Cookie` på Edge Network-begäran. FPID-cookie måste inkluderas.
4. **Kontrollera identitetsprioritet**: Om ett befintligt ECID redan har lagrats i en `kndctr_` -cookie har det företräde framför FPID. FPID:t ger bara ett nytt ECID när det inte finns något befintligt ECID. Se [Hur FPID:n fungerar](./fpid.md#how-fpids-work) för den fullständiga prioritetsordningen.
5. **Verifiera CNAME**: Om du använder cookie-metoden för datastream bekräftar du att din CNAME-samling är korrekt konfigurerad och att förfrågningar dirigeras genom den.

+++

+++**Domänövergripande identitet fungerar inte**

**Symptom**: En besökare som klickar från en av dina domäner till en annan behandlas som en ny besökare på måldomänen.

**Diagnostiksteg**:

1. **Kontrollera URL:en**: Granska mål-URL:en när besökaren klickar på länken. Den måste innehålla en `adobe_mc`-frågesträngsparameter. Om parametern saknas läggs den inte till i källdomänen. Se [Implementera domändelning](./cross-domain-sharing.md#implement-cross-domain-sharing).
2. **Kontrollera timing**: Parametern `adobe_mc` upphör att gälla efter fem minuter. Om målsidan tar för lång tid att läsa in (till exempel på grund av omdirigeringar eller långsamma nätverk) kan parametern förfalla innan Web SDK kan läsa den.
3. **Verifiera `orgId` match**: Båda domänerna måste använda samma [`orgId`](/help/collection/js/commands/configure/orgid.md). Organisations-ID:n som inte matchar gör att måldomänen avvisar identiteten.
4. **Bekräfta att Web SDK finns på målet**: Målsidan måste ha Web SDK installerat och konfigurerat. Utan den ignoreras parametern `adobe_mc`.
5. **Kontrollera om det finns URL-stripping**: Vissa omdirigeringstjänster, CDN:er eller logikstrimmor på serversidan innehåller okända frågesträngsparametrar. Verifiera att `adobe_mc` överlever eventuella mellanliggande omdirigeringar mellan käll- och målsidorna.

+++

+++**Överföring av identitet från mobilen till webben misslyckas**

**Symptom**: En besökare som startar i mobilappen och öppnar en WebView eller en mobilwebbläsare behandlas som en ny besökare på webbsidan.

**Diagnostiksteg**:

1. **Verifiera URL:en**: Logga URL:en som skickas till WebView. Den måste innehålla en `adobe_mc`-parameter som har genererats av [`getUrlVariables`](https://developer.adobe.com/client-sdks/edge/identity-for-edge-network/api-reference/#geturlvariables).
2. **Kontrollera SDK-versioner**: Mobile Identity för Edge Network-tillägget måste vara version 1.1.0 eller senare och Web SDK måste vara version 2.11.0 eller senare.
3. **Kontrollera timingen**: Precis som för korsdomänsdelning upphör parametern `adobe_mc` att gälla efter fem minuter. Kontrollera att WebView-objektet läses in snabbt när URL:en har skapats.
4. **Bekräfta `orgId` match**: Experience Cloud organisations-ID måste vara samma i både SDK- och Web SDK-konfigurationer för mobila enheter.

+++
