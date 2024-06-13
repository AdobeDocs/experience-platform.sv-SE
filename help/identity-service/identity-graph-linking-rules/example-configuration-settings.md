---
title: Exempelkonfigurationer
description: Lär dig mer om exempelkonfigurationer med verktyget för diagramsimulering.
hide: true
hidefromtoc: true
badge: Beta
source-git-commit: ba72abd9febc6d9e6491748519199b54a26ae1c5
workflow-type: tm+mt
source-wordcount: '312'
ht-degree: 4%

---

# Exempel på diagramkonfigurationer

>[!NOTE]
>
>CRM ID är ett anpassat namnutrymme. Därför kräver exemplen nedan att du skapar ett anpassat namnutrymme med ett visningsnamn och en identitetssymbol som är &quot;CRM ID&quot;.

I följande avsnitt visas exempel på diagramscenarier som du kan stöta på vid diagramsimulering.

## Endast CRM-ID

Händelser:

* CRM-ID: Tom, ECID: 111

Algoritmkonfiguration:

| Prioritet | Visningsnamn | Identitetssymbol | Identitetstyp | Unikt per diagram |
| ---| --- | --- | --- | --- |
| 1 | CRM-ID | CRM-ID | CROSS_DEVICE | Ja |
| 2 | ECID | ECID | COOKIE | NEJ |

+++Markera för att visa det simulerade diagrammet

+++

## CRM-ID med hashad e-post

I det här scenariot är ett CRM-ID inkapslat och representerar både online- (upplevelsehändelse) och offlinedata (profilpost). Det här scenariot innebär även att ett hashade e-postmeddelande, som representerar ett annat namnområde som skickas i CRM-postens datauppsättning tillsammans med CRM-ID, matas in.

Händelser:

* CRM-ID: Tom, Email_LC_SHA256: Tom<span>@acme.com
* CRM-ID: Tom, ECID: 111
* CRM ID: Sommar, Email_LC_SHA256: Sommar<span>@acme.com
* CRM-ID: Sommar, ECID: 222

Algoritmkonfiguration:

| Prioritet | Visningsnamn | Identitetssymbol | Identitetstyp | Unikt per diagram |
| ---| --- | --- | --- | --- |
| 1 | CRM-ID | CRM-ID | CROSS_DEVICE | Ja |
| 2 | E-post (SHA256, nedsänkt) | Email_LC_SHA256 | E-post | NEJ |
| 3 | ECID | ECID | COOKIE | NEJ |

+++Markera för att visa det simulerade diagrammet

+++

## CRM-ID med hashad e-post, hashad telefon, GAID och IDFA

Händelser:

* CRM ID: Tom, Email_LC_SHA256: aabbcc, Phone_SHA256: 123-4567
* CRM-ID: Tom, ECID: 111
* CRM-ID: Tom, ECID: 222, IDFA: A-A-A
* CRM ID: Sommar, Email_LC_SHA256: ddeeff, Phone_SHA256: 765-4321
* CRM-ID: Sommar, ECID: 333
* CRM ID: Sommar, ECID: 444, GAID:B-B-B

Algoritmkonfiguration:

| Prioritet | Visningsnamn | Identitetssymbol | Identitetstyp | Unikt per diagram |
| ---| --- | --- | --- | --- |
| 1 | CRM-ID | CRM-ID | CROSS_DEVICE | Ja |
| 2 | E-post (SHA256, nedsänkt) | Email_LC_SHA256 | E-post | NEJ |
| 3 | Telefon (SHA256) | Phone_SHA256 | Telefon | NEJ |
| 4 | Google Ad ID (GAID) | GAID | ENHET | NEJ |
| 5 | Apple IDFA (ID för Apple) | IDFA | ENHET | NEJ |
| 6 | ECID | ECID | COOKIE | NEJ |

+++Markera för att visa det simulerade diagrammet

+++