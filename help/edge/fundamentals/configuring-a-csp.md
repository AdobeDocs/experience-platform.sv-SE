---
title: Konfigurera en CSP
seo-title: Configuring a CSP for Adobe Experience Platform Web SDK
description: Lär dig hur du konfigurerar en CSP för Experience Platform Web SDK
seo-description: Learn how to configure a CSP for the Experience Platform Web SDK
keywords: konfigurera;konfiguration;SDK;edge;Web SDK;konfigurera;kontext;webb;enhet;miljö;web sdk-inställningar;content security policy;
exl-id: 661d0001-9e10-479e-84c1-80e58f0e9c0b
source-git-commit: 0085306a2f5172eb19590cc12bc9645278bd2b42
workflow-type: tm+mt
source-wordcount: '333'
ht-degree: 0%

---

# Konfigurera en CSP

A [Skyddsprofil för innehåll](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Security-Policy) (CSP) används för att begränsa vilka resurser en webbläsare får använda. CSP kan även begränsa funktionerna för skript och formatresurser. Adobe Experience Platform Web SDK kräver ingen CSP, men om du lägger till en kan det minska attackytan för att förhindra skadliga attacker.

CSP måste återspegla hur [!DNL Platform Web SDK] distribueras och konfigureras. Följande CSP visar vilka ändringar som kan behövas för att SDK ska fungera korrekt. Ytterligare CSP-inställningar krävs troligen, beroende på din specifika miljö.

## Exempel på skyddsprofil för innehåll

I följande exempel visas hur du konfigurerar en CSP.

### Tillåt åtkomst till edge-domänen

```
default-src 'self';
connect-src 'self' EDGE-DOMAIN
```

I exemplet ovan `EDGE-DOMAIN` ska ersättas med förstahandsdomänen. Första part-domänen är konfigurerad för [edgeDomain](configuring-the-sdk.md#edge-domain) inställning. Om ingen förstahandsdomän har konfigurerats, `EDGE-DOMAIN` bör ersättas med `*.adobedc.net`. Om migrering av besökare är aktiverat med [idMigrationEnabled](configuring-the-sdk.md#id-migration-enabled), `connect-src` direktivet måste även innehålla `*.demdex.net`.

### Använd NONCE för att tillåta infogade skript och formatelement

[!DNL Platform Web SDK] kan ändra sidinnehåll och måste godkännas för att kunna skapa infogade skript och formattaggar. För att uppnå detta rekommenderar Adobe att du använder ett nonce för [default-src](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Security-Policy/default-src) CSP-direktiv. Ett nonce är en servergenererad kryptografiskt stark slumpvariabel som genereras en gång per varje unik sidvy.

```
default-src 'nonce-SERVER-GENERATED-NONCE'
```

Dessutom måste CSP nonce läggas till som ett attribut i [!DNL Platform Web SDK] [baskod](installing-the-sdk.md#adding-the-code) script-tagg. [!DNL Platform Web SDK] kommer sedan att använda den funktionen en gång när du lägger till infogade skript eller formatkoder på sidan:

```
<script nonce="SERVER-GENERATED-NONCE">
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["alloy"]);
</script>
```

Om ett nonce inte används är det andra alternativet att lägga till `unsafe-inline` till `script-src` och `style-src` CSP-direktiv:

```
script-src 'unsafe-inline'
style-src 'unsafe-inline'
```

>[!NOTE]
>
>Adobe gör **not** rekommendera `unsafe-inline` eftersom det tillåter att skript körs på sidan, vilket begränsar fördelarna med CSP.
