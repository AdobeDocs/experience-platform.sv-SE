---
title: Exempelkonfigurationer
description: Lär dig mer om exempelkonfigurationer med verktyget för diagramsimulering.
badge: Beta
source-git-commit: 536770d0c3e7e93921fe40887dafa5c76e851f5e
workflow-type: tm+mt
source-wordcount: '814'
ht-degree: 2%

---

# Exempel på diagramkonfigurationer

>[!AVAILABILITY]
>
>Länkningsregler för identitetsdiagram finns för närvarande i betaversionen. Kontakta ditt Adobe-kontoteam för att få information om deltagandekriterierna. Funktionen och dokumentationen kan komma att ändras.

>[!NOTE]
>
>* &quot;CRMID&quot; och &quot;loginID&quot; är egna namnutrymmen. I det här dokumentet är &quot;CRMID&quot; en personidentifierare och &quot;loginID&quot; är en inloggningsidentifierare som är associerad med en viss person.
>* Om du vill simulera de exempeldiagramscenarier som beskrivs i det här dokumentet måste du först skapa två anpassade namnutrymmen, ett med identitetssymbolen &quot;CRMID&quot; och ett annat med identitetssymbolen &quot;loginID&quot;. Identitetssymboler är skiftlägeskänsliga.

Det här dokumentet innehåller exempel på diagramkonfigurationer av vanliga scenarier som du kan stöta på när du arbetar med identitetsdata.

## Endast CRMID

Detta är ett exempel på ett enkelt implementeringsscenario där online-händelser (CRMID och ECID) importeras och offline-händelser (profilposter) bara lagras mot CRMID.

**Implementering:**

| Använda namnutrymmen | Samlingsmetod för webbeteenden |
| --- | --- |
| CRMID, ECID | Webb-SDK |

**Händelser:**

Du kan skapa det här scenariot i diagramsimulering genom att kopiera följande händelser till textläge:

* CRMID: Tom, ECID: 111

**Algoritmkonfiguration:**

Du kan skapa det här scenariot i diagramsimulering genom att konfigurera följande inställningar för algoritmkonfigurationen:

| Prioritet | Visningsnamn | Identitetstyp | Unikt per diagram |
| ---| --- | --- | --- |
| 1 | CRMID | CROSS_DEVICE | Ja |
| 2 | ECID | COOKIE | Nej |

**Val av primär identitet för kundprofil i realtid:**

I den här konfigurationen definieras den primära identiteten så här:

| Autentiseringsstatus | Namnutrymme i händelser | Primär identitet |
| --- | --- | --- |
| Autentiserad | CRMID, ECID | CRMID |
| Oautentiserad | ECID | ECID |

>[!BEGINTABS]

>[!TAB Idealiskt enpersonsdiagram ]

Följande är ett exempel på ett idealiskt enpersonsdiagram, där CRMID är unikt och har högsta prioritet.

![Ett simulerat exempel på ett idealiskt enpersonsdiagram, där CRMID är unikt och har högsta prioritet.](../images/graph-examples/crmid_only_single.png)

>[!TAB flerpersonsdiagram]

Följande är ett exempel på ett flerpersonsdiagram. I det här exemplet visas ett scenario med delade enheter, där det finns två CRMID:n och där den med den äldre etablerade länken tas bort.

![Ett simulerat exempel på ett flerpersonsdiagram. I det här exemplet visas ett delat enhetsscenario där det finns två CRMID:n och den äldre etablerade länken tas bort.](../images/graph-examples/crmid_only_multi.png)

>[!ENDTABS]

## CRMID med hash-kodad e-post

I det här scenariot är ett CRMID inkapslat och representerar både online- (upplevelsehändelse) och offlinedata (profilpost). Det här scenariot innebär även att ett hashade e-postmeddelande som representerar ett annat namnområde som skickas i CRM-postdatauppsättningen tillsammans med CRMID skickas.

**Implementering:**

| Använda namnutrymmen | Samlingsmetod för webbeteenden |
| --- | --- |
| CRMID, Email_LC_SHA256, ECID | Webb-SDK |

**Händelser:**

Du kan skapa det här scenariot i diagramsimulering genom att kopiera följande händelser till textläge:

* CRMID: Tom, Email_LC_SHA256: tom<span>@acme.com
* CRMID: Tom, ECID: 111
* CRMID: Sommar, Email_LC_SHA256: Sommar<span>@acme.com
* CRMID: Sommar, ECID: 222

**Algoritmkonfiguration:**

Du kan skapa det här scenariot i diagramsimulering genom att konfigurera följande inställningar för algoritmkonfigurationen:

| Prioritet | Visningsnamn | Identitetstyp | Unikt per diagram |
| ---| --- | --- | --- |
| 1 | CRMID | CROSS_DEVICE | Ja |
| 2 | E-post (SHA256, nedsänkt) | E-post | Nej |
| 3 | ECID | COOKIE | Nej |

**Val av primär identitet för profil:**

I den här konfigurationen definieras den primära identiteten så här:

| Autentiseringsstatus | Namnutrymme i händelser | Primär identitet |
| --- | --- | --- |
| Autentiserad | CRMID, ECID | CRMID |
| Oautentiserad | ECID | ECID |

>[!BEGINTABS]

>[!TAB Idealiskt enpersonsdiagram ]

![I det här exemplet skapas två separata diagram som representerar en entitet för en person.](../images/graph-examples/crmid_hashed_single.png)

>[!TAB flerpersonsdiagram: delad enhet]

![I det här exemplet visar det simulerade diagrammet ett &quot;delat enhetsscenario&quot; eftersom både Tom och sommaren är associerade med samma ECID.](../images/graph-examples/crmid_hashed_shared_device.png)

>[!TAB flerpersonsdiagram: icke-unik e-post]

![Det här scenariot liknar ett scenario där en delad enhet används. I stället för att låta personentiteterna dela ECID är de kopplade till samma e-postkonto.](../images/graph-examples/crmid_hashed_nonunique_email.png)

>[!ENDTABS]

## CRMID med hash-kodad e-post, hash-kodad telefon, GAID och IDFA

Detta scenario liknar det föregående. I det här scenariot markeras däremot hashad e-post och telefon som identiteter som ska användas i segmentmatchning.

**Implementering:**

| Använda namnutrymmen | Samlingsmetod för webbeteenden |
| --- | --- |
| CRMID, Email_LC_SHA256, Phone_SHA256, GAID, IDFA, ECID | Webb-SDK |

**Händelser:**

Du kan skapa det här scenariot i diagramsimulering genom att kopiera följande händelser till textläge:

* CRMID: Tom, Email_LC_SHA256: aabbcc, Phone_SHA256: 123-4567
* CRMID: Tom, ECID: 111
* CRMID: Tom, ECID: 222, IDFA: A-A-A
* CRMID: Sommar, Email_LC_SHA256: ddeeff, Phone_SHA256: 765-4321
* CRMID: Sommar, ECID: 333
* CRMID: Sommar, ECID: 444, GAID:B-B-B

**Algoritmkonfiguration:**

Du kan skapa det här scenariot i diagramsimulering genom att konfigurera följande inställningar för algoritmkonfigurationen:

| Prioritet | Visningsnamn | Identitetstyp | Unikt per diagram |
| ---| --- | --- | --- |
| 1 | CRMID | CROSS_DEVICE | Ja |
| 2 | E-post (SHA256, nedsänkt) | E-post | Nej |
| 3 | Telefon (SHA256) | Telefon | Nej |
| 4 | Google Ad ID (GAID) | ENHET | Nej |
| 5 | Apple IDFA (ID för Apple) | ENHET | Nej |
| 6 | ECID | COOKIE | Nej |

**Val av primär identitet för profil:**

I den här konfigurationen definieras den primära identiteten så här:

| Autentiseringsstatus | Namnutrymme i händelser | Primär identitet |
| --- | --- | --- |
| Autentiserad | CRMID, IDFA, ECID | CRMID |
| Autentiserad | CRMID, GAID, ECID | CRMID |
| Autentiserad | CRMID, ECID | CRMID |
| Oautentiserad | GAID, ECID | GAID |
| Oautentiserad | IDFA, ECID | IDFA |
| Oautentiserad | ECID | ECID |

>[!BEGINTABS]

>[!TAB Idealiskt enpersonsdiagram ]

![](../images/graph-examples/crmid_hashed_single_seg_match.png)

>[!ENDTABS]

<!-- 
## Single CRMID with multiple login IDs (simple)

In this scenario, there is a single CRMID that represents a person entity. However, a person entity may have multiple login identifiers:

* A given person entity can have different account account types (personal vs. business, account by state, account by brand, etc.)
* A given person entity may use different email addresses for any number of accounts.

Therefore, **it is crucial that the CRMID is always sent for every user**. Failure to do so may result in a "dangling" login ID scenario, where a single person entity is assumed to be sharing a device with another person.

**Implementation:**

| Namespaces used | Web behavior collection method |
| --- | --- |
| CRMID, loginID, ECID | Web SDK |

**Events:**

You can create this scenario in graph simulation by copying the following events to text mode:

* CRMID: John, loginID: ID_A
* CRMID: John, loginID: ID_B
* loginID: ID_A, ECID: 111
* CRMID: Jane, loginID: ID_C
* CRMID: Jane, loginID: ID_D
* loginID: ID_C, ECID: 222

**Algorithm configuration:**

You can create this scenario in graph simulation by configuring the following setup for your algorithm configuration:

| Priority | Display name | Identity symbol | Identity type | Unique per graph |
| ---| --- | --- | --- | --- |
| 1 | CRMID | CRMID | CROSS_DEVICE | Yes |
| 2 | loginID | loginID | CROSS_DEVICE | No |
| 3 | ECID | ECID | COOKIE | No |

## Single CRMID with multiple login IDs (complex)

In this scenario, there is a single CRMID that represents a person entity. However, a person entity may have multiple login identifiers:

* A given person entity can have different account account types (personal vs. business, account by state, account by brand, etc.)
* A given person entity may use different email addresses for any number of accounts.

The case of "dangling" loginID also applies for this scenario.

**Implementation:**

| Namespaces used | Web behavior collection method |
| --- | --- |
| CRMID, Email_LC_SHA256, Phone_SHA256, loginID, ECID, AAID | Adobe Analytics source connector |


**Events:**

You can create this scenario in graph simulation by copying the following events to text mode:

* CRMID: John, Email_LC_SHA256: aabbcc, Phone_SHA256: 123-4567
* CRMID: John, loginID: ID_A
* CRMID: John, loginID: ID_B
* loginID:ID_A, ECID: 111, AAID: AAA
* CRMID: Jane, Email_LC_SHA256: ddeeff, Phone_SHA256: 765-4321
* CRMID: Jane, loginID: ID_C
* CRMID: Jane, loginID: ID_D
* loginID: ID_C, ECID: 222, AAID: BBB

**Algorithm configuration:**

You can create this scenario in graph simulation by configuring the following setup for your algorithm configuration:

| Priority | Display name | Identity symbol | Identity type | Unique per graph |
| ---| --- | --- | --- | --- |
| 1 | CRMID | CRMID | CROSS_DEVICE | Yes |
| 2 | Email_LC_SHA256 | Email_LC_SHA256 | EMAIL | No |
| 3 | Phone_SHA256 | Phone_SHA256 | PHONE | No |
| 4 | loginID | loginID | CROSS_DEVICE | No |
| 5 | ECID | ECID | COOKIE | No |
| 6 | AAID | AAID | COOKIE | No |
 -->
