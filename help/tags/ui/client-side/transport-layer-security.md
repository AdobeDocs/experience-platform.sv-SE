---
title: TLS-information (Transport Layer Security)
description: Information om vilka TLS-versioner och -ciphers som används
exl-id: 04948cd8-6cf0-4159-a9d3-3130b97af106
source-git-commit: 236c5a11f40490fc7ee536358fb146027fe64545
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 15%

---

# TLS-information (Transport Layer Security)

>[!NOTE]
>
>Adobe Experience Platform Launch har omprofilerats till en serie tekniker för datainsamling i Adobe Experience Platform. Som ett resultat av detta har flera terminologiska förändringar genomförts i produktdokumentationen. En konsoliderad referens till de ändrade terminologin finns i dokumentet [Termuppdatering](../../term-updates.md).

TLS (Transport Layer Security) är ett kryptografiskt protokoll som ger total säkerhet för data som skickas mellan program över Internet. Mer detaljerad information om TLS finns i dokumentationen om [TLS-grunder](https://www.internetsociety.org/deploy360/tls/basics/).

Taggar i Adobe Experience Platform är ett tagghanteringssystem som är utformat för att dynamiskt läsa in skript på din webbplats. TLS skyddar kommunikationen mellan Adobe-värden `assets.adobedtm.com` och din webbplats när dessa skript läses in.

Det finns flera TLS-versioner, och det stöder ett antal olika ciphers. Alla versioner och ciphers är inte desamma som vissa anses vara mindre eller säkrare än andra.

## TLS-versioner och CIphers som stöds

Adobe värdalternativ har för närvarande stöd för följande TLS-versioner och -ciphers:

```
PORT    STATE SERVICE
443/tcp open  https
| ssl-enum-ciphers:
|   TLSv1.2:
|     ciphers:
|       TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384 (secp256r1) - A
|       TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256 (secp256r1) - A
|       TLS_ECDHE_ECDSA_WITH_CHACHA20_POLY1305_SHA256 (secp256r1) - A
|       TLS_ECDHE_RSA_WITH_CHACHA20_POLY1305_SHA256 (secp256r1) - A
|       TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384 (secp256r1) - A
|       TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256 (secp256r1) - A
|     compressors:
|       NULL
|     cipher preference: server
|   TLSv1.3:
|     ciphers:
|       TLS_AKE_WITH_AES_128_GCM_SHA256 (secp256r1) - A
|       TLS_AKE_WITH_AES_256_GCM_SHA384 (secp256r1) - A
|       TLS_AKE_WITH_CHACHA20_POLY1305_SHA256 (secp256r1) - A
|     cipher preference: client
|_  least strength: A
```

### Självvärdande

Om du är [självvärd](../publishing/hosts/self-hosting-libraries.md) för ditt bibliotek bestäms vilka TLS-versioner som stöds av din egen värdtjänst.
