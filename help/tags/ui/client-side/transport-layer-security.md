---
title: TLS-information (Transport Layer Security)
description: Information om vilka TLS-versioner och -ciphers som används
source-git-commit: 35ee2aca2b92cb8abe1fc69ad6cbc66b0e241e89
workflow-type: tm+mt
source-wordcount: '209'
ht-degree: 0%

---

# TLS-information (Transport Layer Security)

>[!NOTE]
>
>Adobe Experience Platform Launch har omklassificerats som en serie datainsamlingstekniker i Adobe Experience Platform. Som ett resultat av detta har flera terminologiska förändringar införts i produktdokumentationen. En konsoliderad referens till de ändrade terminologin finns i [avtalsuppdateringar](../../term-updates.md) -dokument.

TLS (Transport Layer Security) är ett kryptografiskt protokoll som ger total säkerhet för data som skickas mellan program över Internet. Mer information om TLS finns i [Grundläggande om TLS](https://www.internetsociety.org/deploy360/tls/basics/) dokumentation.

Taggar i Adobe Experience Platform är ett tagghanteringssystem som är utformat för att dynamiskt läsa in skript på din webbplats. TLS säkrar kommunikationen mellan Adobe-värden `assets.adobedtm.com` och webbplatsen när dessa skript läses in.

Det finns flera TLS-versioner, och det stöder ett antal olika ciphers. Alla versioner och ciphers är inte desamma som vissa anses vara mindre eller säkrare än andra.

## TLS-versioner och CIphers som stöds

Värdalternativet Adobe har för närvarande stöd för följande TLS-versioner och -ciphers:

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

Om du [värdtjänster](../publishing/hosts/self-hosting-libraries.md) ditt bibliotek, kommer de TLS-versioner som stöds att bestämmas av din egen värdtjänst.

## TLS-cifer som ska tas bort 1 maj 2024

```
PORT    STATE SERVICE
443/tcp open  https
| ssl-enum-ciphers:
|   TLSv1.2:
|     ciphers:
|       TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA384 (secp256r1) - A
|       TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA256 (secp256r1) - A
|       TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384 (secp256r1) - A
|       TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256 (secp256r1) - A
|       TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA (secp256r1) - A
|       TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA (secp256r1) - A
|       TLS_RSA_WITH_AES_256_GCM_SHA384 (rsa 2048) - A
|       TLS_RSA_WITH_AES_128_GCM_SHA256 (rsa 2048) - A
|       TLS_RSA_WITH_AES_256_CBC_SHA256 (rsa 2048) - A
|       TLS_RSA_WITH_AES_128_CBC_SHA256 (rsa 2048) - A
|       TLS_RSA_WITH_AES_256_CBC_SHA (rsa 2048) - A
|       TLS_RSA_WITH_AES_128_CBC_SHA (rsa 2048) - A
|     compressors:
|       NULL
|     cipher preference: server
|   TLSv1.3:
|     ciphers:
|       TLS_AKE_WITH_AES_128_CCM_8_SHA256 (secp256r1) - A
|       TLS_AKE_WITH_AES_128_CCM_SHA256 (secp256r1) - A
|     cipher preference: client
|_  least strength: A
```
