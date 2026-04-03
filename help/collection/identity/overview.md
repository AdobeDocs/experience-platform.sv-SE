---
title: Identitet i datainsamling
description: Läs om hur datainsamlingen använder ECID:n, CORE ID:n, beständighet från första part och identityMap för olika webblösningar.
exl-id: 03060cdb-becc-430a-b527-60c055c2a906
source-git-commit: 696e5098ebf556bfc0fa4fc22ff637cb0835eee0
workflow-type: tm+mt
source-wordcount: '654'
ht-degree: 0%

---

# Identitet i datainsamling

Adobe Data Collection använder identitetssignaler för att identifiera återkommande besökare och föra samman upplevelser. När en besökare kommer till er webbplats genererar Edge Network ett Experience Cloud-ID (ECID) och behåller det i en cookie från en annan leverantör. ECID är den primära enhetsidentifieraren som används i olika Adobe Experience Cloud-program och är den grund som analys, personalisering och målgruppsaktivering bygger på. I din implementering kan du komma åt besökarens ECID på klientsidan via kommandot [`getIdentity`](/help/collection/js/commands/getidentity.md). På datastream-nivå kan du använda [Data Prep för datainsamling](/help/datastreams/data-prep.md) för att mappa ECID till ett anpassat XDM-fält innan det når underordnade tjänster.

ECID:t identifierar en enhet, inte en person. Om du vill koppla aktiviteten till en känd person kan du skicka ytterligare identifierare, till exempel ett CRM-ID eller hashad e-post, tillsammans med ECID med hjälp av XDM [`identityMap`](./identity-map.md). Adobe rekommenderar att du anger ett namnutrymme på personnivå som [primär identitet](/help/tags/extensions/client/web-sdk/data-element-types.md#identity-map) när det finns en sådan.

Förutom standard-ECID stöder datainsamling ytterligare identitetssignaler beroende på implementeringen:

* **Första parts enhets-ID (FPID)**: Enhetsidentifierare som du genererar och hanterar på infrastruktur som du kontrollerar. Edge Network använder ett FPID för att [dirigera om ECID](./fpid.md), vilket ger dig starkare cookie-beständighet för ägda egenskaper när webbläsarbegränsningar kortar livet för Adobe-hanterade cookies.
* **CORE-ID**: En separat, demonstrationsbaserad identifierare som deltar i arbetsflöden för tredjepartsidentitet när cookies från tredje part är tillgängliga. CORE ID skiljer sig från ECID och kan hämtas via [`getIdentity`](/help/collection/js/commands/getidentity.md). Mer information om hur kontexter för första parts- och tredjepartsidentitet fungerar tillsammans finns i [Stöd för enhetlig identitet](./unified-identity-support.md).

Om du uppgraderar från Visitor-API:t eller förenar äldre identitetsbeteenden läser du [`idMigrationEnabled`](/help/collection/js/commands/configure/idmigrationenabled.md) för att migrera befintliga AMCV-cookies.

## Samling med första och tredje part {#first-party-and-third-party-collection}

SDK anger alltid identiteten [cookies](https://experienceleague.adobe.com/sv/docs/core-services/interface/data-collection/cookies/web-sdk) (till exempel `kndctr_` cookies) som cookies från första part på din domän, oavsett vilken slutpunkt som tar emot datainsamlingsbegäran. Samlingsslutpunkten (domänen som implementeringen skickar data till) är ett separat alternativ som påverkar hur webbläsare och nätverksprinciper hanterar själva begäran.

**Första part-samlingen** skickar datainsamlingsbegäranden via en domän som din organisation kontrollerar (till exempel `data.example.com`), med en CNAME som pekar på Adobe Edge Network. Eftersom begäran finns kvar på din domän är det mindre troligt att den blockeras av annonsblockerare eller webbläsarens nätverksbegränsningar. Samling med första part är också en förutsättning för att ställa in [enhets-ID:n från första part](./fpid.md) från din egen serverinfrastruktur, vilket är den mest varaktiga identitetsstrategi som finns. Adobe rekommenderar att du använder det [Adobe-hanterade certifikatprogrammet](https://experienceleague.adobe.com/sv/docs/core-services/interface/data-collection/adobe-managed-cert) för att konfigurera förstapartssamlingen för din implementering.

**Tredjepartssamlingen** skickar begäranden direkt till en [`edgeDomain`](/help/collection/js/commands/configure/edgedomain.md) som ägs av Adobe (till exempel `example.data.adobedc.net`). Även om identitetscookies fortfarande är angivna som förstahandsval på din domän, skickas själva begäran till en tredjepartsdomän, som vissa webbläsare och annonsblockerare kan begränsa.

## Välj rätt identitetsmönster {#choose-your-path}

* **Stärk identitetsbeständighet för ägda egenskaper**: Använd [enhets-ID:n från första part](./fpid.md) när webbläsarbegränsningar kortar cookie-livstiden och du behöver större kontinuitet för analys och personalisering på webbplatser du kontrollerar.
* **Lämna över identitet från en app till en mobil-webb**: Använd [delning av mobil-till-webbidentitet](./mobile-to-web.md) när besökaren startar i din mobilapp och fortsätter i en WebView- eller mobilwebbsida.
* **Håll identiteten kontinuerlig över alla domäner**: Använd [domändelning](./cross-domain-sharing.md) när besökare flyttar mellan webbegenskaper som organisationen äger och du vill ha konsekvent rapportering och personalisering.
* **Kombinera förstapartsbeständighet med tredjepartsaktivering**: Använd [enhetligt identitetsstöd](./unified-identity-support.md) när du behöver beständig förstapartidentifiering tillsammans med aktiveringsflöden från tredje part som stöds.
* **Skicka identifierare på personnivå**: Använd [`identityMap`](./identity-map.md) för att skicka CRM-ID:n, hashade e-postmeddelanden och andra identifierare på personnivå tillsammans med ECID så att underordnade tjänster kan sy ihop aktiviteter med en känd person.
* **Förstå hur samtycke påverkar identitet**: Läs [Godkännande och identitet](./consent.md) om du vill veta hur `defaultConsent` och `setConsent` styr när Web SDK genererar ett ECID, ställer in cookies och skickar data.

Hjälp med att diagnostisera identitetsproblem som besökaruppblåsning, ECID-inkonsekvenser eller FPID-problem finns i [Felsökning av identitet](./troubleshooting.md).
