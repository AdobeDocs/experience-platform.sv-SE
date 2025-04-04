---
title: Konfigurera en CSP
seo-title: Configuring a CSP for Adobe Experience Platform Web SDK
description: Lär dig konfigurera en CSP för Experience Platform Web SDK
seo-description: Learn how to configure a CSP for the Experience Platform Web SDK
keywords: konfigurera;konfiguration;SDK;edge;Web SDK;konfigurera;kontext;web;device;environment;web sdk settings;content security policy;
exl-id: 661d0001-9e10-479e-84c1-80e58f0e9c0b
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 0%

---

# Konfigurera en CSP

En [CSP ](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Security-Policy) (Content Security Policy) används för att begränsa vilka resurser en webbläsare får använda. CSP kan även begränsa funktionerna för skript och formatresurser. Adobe Experience Platform Web SDK kräver ingen CSP, men om du lägger till en kan det minska attackytan för att förhindra skadliga attacker.

CSP måste återspegla hur [!DNL Experience Platform Web SDK] distribueras och konfigureras. Följande CSP visar vilka ändringar som kan behövas för att SDK ska fungera korrekt. Ytterligare CSP-inställningar krävs troligen, beroende på din specifika miljö.

## Exempel på skyddsprofil för innehåll

I följande exempel visas hur du konfigurerar en CSP.

### Tillåt åtkomst till edge-domänen

```
default-src 'self';
connect-src 'self' EDGE-DOMAIN
```

I exemplet ovan bör `EDGE-DOMAIN` ersättas med förstahandsdomänen. Den första partsdomänen har konfigurerats för inställningen [edgeDomain](../commands/configure/edgedomain.md). Om ingen förstapartsdomän har konfigurerats bör `EDGE-DOMAIN` ersättas med `*.adobedc.net`. Om migrering av besökare aktiveras med [idMigrationEnabled](../commands/configure/idmigrationenabled.md) måste direktivet `connect-src` även innehålla `*.demdex.net`.

### Använd NONCE för att tillåta infogade skript och formatelement

[!DNL Experience Platform Web SDK] kan ändra sidinnehåll och måste godkännas för att kunna skapa infogade skript och formatkoder. För att uppnå detta rekommenderar Adobe att du använder en nonce för CSP-direktivet [default-src](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Security-Policy/default-src) . Ett nonce är en servergenererad kryptografiskt stark slumpvariabel som genereras en gång per varje unik sidvy.

```
default-src 'nonce-SERVER-GENERATED-NONCE'
```

Dessutom måste CSP nonce läggas till som ett attribut i skripttaggen [!DNL Experience Platform Web SDK] [base code](../install/library.md) . [!DNL Experience Platform Web SDK] kommer sedan att använda den funktionen en gång när du lägger till infogade skript eller formatkoder på sidan:

```
<script nonce="SERVER-GENERATED-NONCE">
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["alloy"]);
</script>
```

Om inget nonce används är det andra alternativet att lägga till `unsafe-inline` i CSP-direktiven `script-src` och `style-src`:

```
script-src 'unsafe-inline'
style-src 'unsafe-inline'
```

>[!NOTE]
>
>Adobe rekommenderar **inte** att du anger `unsafe-inline` eftersom det tillåter att skript körs på sidan, vilket begränsar fördelarna med CSP.

## Konfigurera en CSP för meddelanden i appen {#in-app-messaging}

När du konfigurerar [Web In-App Messaging](../personalization/web-in-app-messaging.md) måste du ta med följande direktiv i din CSP:

```
default-src  blob:;
```
