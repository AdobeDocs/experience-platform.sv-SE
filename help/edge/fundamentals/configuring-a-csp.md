---
title: Konfigurera en CSP
seo-title: Konfigurera en CSP för Adobe Experience Platform Web SDK
description: Lär dig hur du konfigurerar en CSP för Experience Platform Web SDK
seo-description: Lär dig hur du konfigurerar en CSP för Experience Platform Web SDK
keywords: konfigurera;konfiguration;SDK;edge;Web SDK;konfigurera;kontext;webb;enhet;miljö;web sdk-inställningar;content security policy;
translation-type: tm+mt
source-git-commit: 4f07d41197add406fbdd82caee5177a1ddaa7d7e
workflow-type: tm+mt
source-wordcount: '354'
ht-degree: 0%

---


# Konfigurera en CSP

En [skyddsprofil för innehåll](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Security-Policy) (CSP) används för att begränsa vilka resurser en webbläsare får använda. CSP kan även begränsa funktionerna för skript och formatresurser. Adobe Experience Platform Web SDK kräver ingen CSP, men om du lägger till en kan det minska attackytan för att förhindra skadliga attacker.

CSP måste återspegla hur [!DNL Platform Web SDK] distribueras och konfigureras. Följande CSP visar vilka ändringar som kan behövas för att SDK ska fungera korrekt. Ytterligare CSP-inställningar krävs troligen, beroende på din specifika miljö.

## Exempel på skyddsprofil för innehåll

I följande exempel visas hur du konfigurerar en CSP.

### Tillåt åtkomst till edge-domänen

```
default-src 'self';
connect-src 'self' EDGE-DOMAIN
```

I ovanstående exempel ska `EDGE-DOMAIN` ersättas med förstapartsdomänen. Första part-domänen är konfigurerad för [edgeDomain](configuring-the-sdk.md#edge-domain)-inställningen. Om ingen förstapartsdomän har konfigurerats bör `EDGE-DOMAIN` ersättas med `*.adobedc.net`. Om migrering av besökare är aktiverat med [idMigrationEnabled](configuring-the-sdk.md#id-migration-enabled) måste `connect-src`-direktivet även innehålla `*.demdex.net`.

### Använd NONCE för att tillåta infogade skript och formatelement

[!DNL Platform Web SDK] kan ändra sidinnehåll och måste godkännas för att kunna skapa infogade skript och formattaggar. För att uppnå detta rekommenderar Adobe att du använder ett nonce för CSP-direktivet [default-src](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Security-Policy/default-src). Ett nonce är en servergenererad kryptografiskt stark slumpvariabel som genereras en gång per varje unik sidvy.

```
default-src 'nonce-SERVER-GENERATED-NONCE'
```

Dessutom måste CSP nonce läggas till som ett attribut i [!DNL Platform Web SDK] [baskod](installing-the-sdk.md#adding-the-code)-skripttaggen. [!DNL Platform Web SDK] kommer sedan att använda den funktionen en gång när du lägger till infogade skript eller formatkoder på sidan:

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
