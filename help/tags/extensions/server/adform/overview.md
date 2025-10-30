---
keywords: integrering av adform; adform;
title: Integrering för oautentiserad återmarknadsföring
description: Tack vare den här Adobe Experience Platform-integreringen kan du omdirigera användare baserat på ECID.
last-substantial-update: 2025-03-26T00:00:00Z
exl-id: 37eb9453-fc3c-481e-94ea-54d9b1545631
source-git-commit: be2ad7a02d4bdf5a26a0847c8ee7a9a93746c2ad
workflow-type: tm+mt
source-wordcount: '726'
ht-degree: 0%

---

# Översikt över tillägget [!DNL Adform]

Tillägget [[!DNL Adform]](https://www.adformhelp.com/hc/en-us/articles/29635608709137-Use-the-Adform-S2S-Site-Tracking-Extension-With-Adobe-Experience-Cloud) möjliggör vidarebefordran av händelser på serversidan i Adobe Experience Platform, vilket gör att annonsörer, medieutgivare och utgivare kan synkronisera data direkt med ID Fusion-systemet i Adform. Tack vare den här integreringen kan företag engagera målgrupper över flera kanaler, förbättra kampanjresultatet och tillhandahålla skräddarsydda lösningar för att förfina digitala annonseringsstrategier och maximera annonsutgifternas effektivitet.

Till skillnad från traditionell spårning på klientsidan eliminerar det här tillägget behovet av cookies från tredje part genom att utnyttja ID:n från första part - närmare bestämt ECID (Experience Cloud ID) som synkroniseras med Adform. Detta möjliggör smidig återannonsering av målgrupper utan att JavaScript behöver driftsättas på klientsidan.

Den här guiden beskriver hur du installerar, konfigurerar och distribuerar tillägget för att vidarebefordra händelser från ett varumärkes digitala egendom via Adobe Edge Network till Adform för att möjliggöra en smidig omdirigering av besökare.

## Återmarknadsföring utanför webbplatsen

Genom omdirigering på annan plats kan ni engagera potentiella kunder som besökt er webbplats men inte konverterat. Med Adobe kan ni nå dessa målgrupper på olika plattformar, stärka varumärkets närvaro och öka konverteringsmöjligheterna. Använd den här integreringen för att:

* Engagera okända besökare på nytt utan att använda cookies från tredje part.
* Aktivera målgrupper direkt på ECID:n utan att använda cookie-alternativa identifierare eller extra taggar från tredje part på era digitala egenskaper.

Med Adform kan du

* Omvandla enkelt era första målgrupper med ECID till adresserbara ID:n för digitala annonskampanjer.
* Länka ECID:n till över 40 buddbara ID-lösningar för att optimera er räckvidd, frekvens och prestanda mot era målgrupper.

### Målgruppsaktivering på serversidan med [!DNL Adform] {#server-side-activation}

Till skillnad från traditionella ID-distributioner på klientsidan kräver den här integreringen inte att du distribuerar en ID-leverantörslösning på dina digitala egenskaper. Istället aktiveras målgruppsaktivering på serversidan genom att ECID:n som redan är synkroniserade med Adform används. Några viktiga fördelar:

* **Ingen JavaScript-distribution på klientsidan**: Du behöver inte hantera logik för identifiering av besökare på klientsidan eller dekryptera ID:n på klientsidan till stabila versioner med längre livslängd.
* **Sömlös målgruppssynkronisering**: ECID:n mappas till Adforms interna ID-diagram, vilket möjliggör effektiv återmarknadsföring på olika plattformar.
* **Förbättrad räckvidd och borttagning av dubbletter**: I ID Fusion-diagrammet kopplas ECID:n till flera identifierare, vilket ger högklassig målgruppsmatchning.

## Förhandskrav {#prerequisites}

Innan du integrerar Adobe med Adobe måste du kontrollera att följande krav är uppfyllda:

1. **Installation av Adobe Web SDK**: Adobe Web SDK måste implementeras för att underlätta datainsamling och vidarebefordran av händelser.

2. **CDP- eller Anslutnings-SKU**: Du måste ha antingen Adobe Customer Data Platform (CDP) Prime eller Ultimate SKU, eller Connection SKU, för att kunna aktivera smidig kommunikation på både klient- och serversidan.

3. **Adobe Experience Platform Edge Network-konfiguration**:
   * Kontrollera att Edge Network har konfigurerats för att stödja händelsevidarebefordran i realtid för återmarknadsföring utanför webbplatsen. Mer information finns i guiden [Komma igång med händelsevidarebefordran](https://experienceleague.adobe.com/sv/docs/experience-platform/tags/event-forwarding/getting-started).
   * Det här steget är avgörande för att effektivt kunna överföra data till Adforms slutpunkt på serversidan.

När dessa krav är uppfyllda kan du fortsätta att konfigurera och distribuera tillägget [!DNL Adform].

## Konfigurera tillägget [!DNL Adform] {#configure-adform-extension}

Om du vill konfigurera tillägget [!DNL Adform] följer du de steg som beskrivs i avsnitten nedan.

### Installera och konfigurera tillägget

Navigera till [!DNL Adform extension] i gränssnittet för vidarebefordring av händelser och ange de värden som krävs:

| Indata | Beskrivning |
| --- | --- |
| ID för spårningsinställning | Den unika identifieraren som tillhandahålls av Adform för att spåra händelser. |
| Global domän | Använd `a1.adform.net` för att optimera prestanda och undvika problem med regional fördröjning. |

Spara konfigurationen när du har angett dessa uppgifter.

<!-- ![Installing and configuring the Adform extension in Adobe Experience Platorm]() -->

### Definiera spårningsparametrar

Åtgärden &quot;track&quot; är den primära händelseregeln. Den utlöses baserat på fördefinierade åtgärder, vanligen `page load.` Inkludera följande parametrar:

**Obligatoriska parametrar:**

| Parametrar | Beskrivning |
| --- | --- |
| `Page Name` | Identifierar sidan eller användaråtgärden. |
| `User Agent` | Hämtar information för målgruppsmatchning. |
| `IP Address` | En avgörande faktor för korrekt målinriktning och återmarknadsföring. |

**Rekommenderade parametrar:**

| Parametrar | Beskrivning |
| --- | --- |
| `Page URL` | Identifierar sidan eller användaråtgärden. |
| `Referral URL` | Hämtar information för målgruppsmatchning. |
| `ECID` | En avgörande faktor för korrekt målinriktning och återmarknadsföring. |
| `Source Domain` | En avgörande faktor för korrekt målinriktning och återmarknadsföring. |

<!-- ![Tracking parameters for Adform]() -->

### Koppla regel

Tillägget måste kopplas till en regel för att fungera korrekt. Om inga villkor är angivna skapar du en global regel som ser till att den alltid körs.

>[!NOTE]
>
>Om tillägget inte fungerar kontrollerar du att det är kopplat till en giltig regel i Adobe Experience Platform Data Collection.

<!-- ![Attach a rule to the Adform extension]() -->

## Validera och distribuera

Kontrollera att tillägget är installerat och konfigurerat korrekt och att alla nödvändiga dataelement mappas, inklusive:

* [ECID](/help/identity-service/features/ecid.md)
* Sidnamn
* Hänvisnings-URL
* Användaragent
* IP-adress

När du har angett alla obligatoriska fält och avslutat testningen väljer du **bygg** för att distribuera tillägget.

## Nästa steg

Du bör nu förstå hur Adform kan integreras med Adobe serverfunktioner och bedöma om integreringen kan genomföras i din befintliga infrastruktur. Mer information finns i [Adforms officiella dokumentation](https://www.adformhelp.com/hc/en-us/articles/29635608709137-Use-the-Adform-S2S-Site-Tracking-Extension-With-Adobe-Experience-Cloud).
