---
title: Använd enhets-ID:n från första part i datainsamling
description: Konfigurera FPID:n (First-party device ID:n) för beständig identitet i webbimplementeringar som skickar data till Edge Network.
source-git-commit: 696e5098ebf556bfc0fa4fc22ff637cb0835eee0
workflow-type: tm+mt
source-wordcount: '1905'
ht-degree: 0%

---

# Använd enhets-ID:n från första part i datainsamling

Experience Platform Edge Network använder Experience Cloud ID (ECID) för att identifiera webbplatsbesökare. Om du vill förbättra identitetshållbarheten för egna egenskaper kan du ange och hantera egna enhetsidentifierare, så kallade FPID:n (First-party device ID:n). Edge Network använder FPID för att dirigera den ECID som används i Adobe lösningar.

Den här sidan förutsätter att du känner till ECID:n och `identityMap`. Mer information finns i [Identitet i datainsamling](./overview.md).

## När FPID ska användas {#when-to-use}

Webbläsarbegränsningar kan korta livet på cookies som Adobe använder för att identifiera återkommande besökare. Om du behöver en mer hållbar identitet på webbplatser som din organisation äger och kontrollerar, kan du med FPID hantera din egen enhetsidentifierare och använda den för att skapa en egen ECID.

FPID:n stöds för webbimplementeringar som använder Web SDK, inklusive taggtillägget Web SDK. De är idealiska när ditt huvudmål är starkare identitetskonsistens på domäner som organisationen äger, eller du vill ha bättre kontinuitet för rapportering och personalisering av ägda webbegenskaper. De gör det även möjligt att konfigurera och hantera en cookie från en egen infrastruktur som du har kontroll över.

FPID:n är inte det rätta verktyget när huvudmålet är att skicka från app till webben eller att upprätthålla identiteten i flera domäner. Se [delning av mobil-till-webbidentitet](./mobile-to-web.md) och [delning mellan domäner](./cross-domain-sharing.md) för dessa scenarier.

Fördelarna med att använda FPID är bland annat:

* Större beständighet mot ägda egenskaper.
* Mer kontroll över hur enhetsidentifieraren genereras och hanteras.
* En hållbar grund för analys och personalisering.

Övergångar till användning av FPID är bland annat:

* Mer implementeringsansvar än att förlita sig på standardidentitetsbeteendet.
* Samordning av cookie-logik på serversidan och konfiguration av datainsamling.
* Ytterligare validering som bekräftar att identifieraren används som förväntat.

### Installationsväg på hög nivå

1. Generera och hantera ett enhets-ID från en annan leverantör för infrastruktur som du kontrollerar.
1. Konfigurera implementeringen för att läsa det ID:t antingen från en [cookie](#setting-cookie-datastreams) från första part eller från [identitetsnyttolasten](#identityMap).
1. Verifiera att återkommande besökare har en konsekvent identitet över tid på dina ägda tillgångar.

## Hur FPID fungerar {#how-fpids-work}

Det FPID som skickas till Adobe Experience Cloud konverteras till ett ECID med hjälp av en deterministisk algoritm. Varje gång samma FPID skickas till Edge Network dirigeras samma ECID från FPID. När FPID har använts för att skicka ett ECID tas det bort från `identityMap` och ersätts med det genererade ECID:t. FPID lagras inte i Adobe Experience Platform- eller Experience Cloud-lösningar.

När både ett ECID och ett FPID finns används alltid ECID för att identifiera användaren först. Denna prioritering säkerställer att när ett befintligt ECID finns i cookie-butiken i webbläsaren förblir det den primära identifieraren och befintligt antal besökare inte riskerar inflationen. För befintliga användare blir FPID inte den primära identiteten förrän ECID:t upphör att gälla eller tas bort som ett resultat av webbläsarprincipen eller manuella åtgärder.

Identiteter prioriteras i följande ordning:

1. ECID ingår i `identityMap`
1. ECID lagras i en cookie
1. FPID ingår i `identityMap`
1. FPID som lagras i en cookie

## Generera och ange FPID-cookie {#set-fpid-cookie}

Edge Network godkänner endast ID:n som är kompatibla med formatet [UIDv4](https://datatracker.ietf.org/doc/html/rfc4122). Enhets-ID:n som inte är i UUIDv4-format nekas.

* UUID är unika och slumpmässiga, med försumbar sannolikhet för kollision.
* UUIDv4 kan inte dirigeras med IP-adresser eller någon annan personligt identifierbar information (PII).
* Bibliotek för att generera UUID finns tillgängliga för alla programmeringsspråk.

### Inställning för cookie på serversidan {#set-cookie-server}

När du ställer in en cookie via din egen server kan du använda olika metoder för att förhindra att cookien begränsas av webbläsarprinciper:

* Generera cookies med serverskriptspråk
* Ange cookies som svar på en API-begäran som görs till en underdomän eller annan slutpunkt på webbplatsen
* Generera cookies med ett content management-system (CMS)
* Generera cookies med ett leveransnätverk (CDN)

Första parts-cookies är mest effektiva när de ställs in med en server som använder en DNS [A-post](https://datatracker.ietf.org/doc/html/rfc1035) (för IPv4) eller [AAAA-post](https://datatracker.ietf.org/doc/html/rfc3596) (för IPv6), i motsats till en DNS `CNAME` - eller JavaScript-kod.

>[!IMPORTANT]
>
>Cookies som anges med JavaScript `document.cookie`-metoden (inklusive med tagg-metoden [`cookie.set()`](../tags/cookie.md)) skyddas nästan aldrig från webbläsarprinciper som begränsar cookie-varaktighet.

Observera att `A`- eller `AAAA`-poster bara stöds för att ange och spåra cookies. Den primära metoden för datainsamling är via en DNS `CNAME`. FPID:n anges med en `A`- eller `AAAA`-post och skickas till Adobe med en `CNAME`. Med [Adobe-hanterat certifikatprogram](https://experienceleague.adobe.com/docs/core-services/interface/administration/ec-cookies/cookies-first-party.html?lang=sv-SE#adobe-managed-certificate-program) kan du konfigurera `CNAME` för datainsamling.

### När cookien ska ställas in {#when-to-set-cookie}

FPID-cookien är idealisk innan data skickas till Edge Network. Om implementeringen kräver samtycke innan du samlar in data, se [Godkänn med enhets-ID:n från första part](./consent.md#consent-with-fpids) för vägledning om hur du koordinerar FPID-cookien med ditt medgivandeflöde. Besökarinflationen minskar när du ser till att FPID är tillgängligt för att skicka ECID från första begäran. I scenarier där detta inte är möjligt genereras ett ECID fortfarande med befintliga metoder och fungerar som primär identifierare så länge som cookien finns. Det genererade FPID:t blir inte den primära identifieraren förrän ECID:t inte längre finns. Om man utgår ifrån att ECID så småningom påverkas av en policy för borttagning av webbläsare, men inte av FPID, blir FPID den primära identifieraren vid nästa besök och används för att förorsaka ECID vid varje påföljande besök.

### Ange förfallodatum {#set-expiration}

Adobe rekommenderar att du noggrant undersöker livstiden för din FPID-cookie. Se till att ni tar hänsyn till organisationens integritetspolicy tillsammans med lagstiftningen och policyn i de länder eller regioner där organisationen är verksam. Beroende på hur din organisation är konfigurerad kan du anta en företagsomfattande cookie-inställningsprincip eller en som varierar för användare på de olika språkområden där du arbetar. Oavsett hur länge cookie-filen förfaller ska du se till att inkludera logik som förlänger förfallotiden varje gång ett nytt webbplatsbesök inträffar.

### Cookie-flaggor {#cookie-flags}

Det finns flera cookie-flaggor som påverkar hur cookies hanteras i olika webbläsare:

* **`HTTPOnly`**: Det går inte att komma åt cookies som har angetts med flaggan `HTTPOnly` med skript på klientsidan. Det innebär att om du anger en `HTTPOnly`-flagga när du anger FPID måste du använda ett skriptspråk på serversidan för att läsa cookie-värdet som ska inkluderas i `identityMap`. Om du väljer att låta Edge Network läsa värdet för FPID-cookien säkerställer en inställning av flaggan `HTTPOnly` att värdet inte är tillgängligt för klientskript, men att det inte påverkar Edge Network förmåga att läsa cookien negativt. Användningen av flaggan `HTTPOnly` påverkar inte cookie-principer som kan begränsa cookie-livstid. Men det är fortfarande något att tänka på när du anger och läser värdet för FPID.
* **`Secure`**: Cookies som angetts med attributet `Secure` skickas bara till servern med en krypterad begäran via HTTPS-protokollet. Om du använder den här flaggan kan du se till att angripare som bär i mitten inte kommer åt cookie-värdet på ett enkelt sätt. När det är möjligt är det alltid en bra idé att ange flaggan `Secure`.
* **`SameSite`**: Med attributet `SameSite` kan servrar avgöra om cookies skickas med förfrågningar mellan webbplatser. Attributet ger visst skydd mot attacker med förfalskning över flera webbplatser. Det finns tre möjliga värden: `Strict`, `Lax` och `None`. Kontakta ditt interna team för att ta reda på vilken inställning som är rätt för din organisation. Om inget `SameSite`-attribut anges är standardinställningen för vissa webbläsare `SameSite=Lax`.

## Skicka FPID till Edge Network {#send-fpid}

Du kan skicka FPID:n till Edge Network på två sätt:

* **[Metod 1](#setting-cookie-datastreams)**: Konfigurera en `CNAME` för dina SDK-webbanrop och inkludera namnet på din FPID-cookie i din datastream-konfiguration.
* **[Metod 2](#identityMap)**: Inkludera FPID i identitetskartan.

### Metod 1: Konfigurera en `CNAME` och ange en cookie för ett första part-ID i ditt datastream {#setting-cookie-datastreams}

Om du vill ange en FPID-cookie från din egen domän måste du konfigurera din egen `CNAME` för dina SDK-webbsamtal och sedan aktivera cookie-funktionen för första parts-ID i din datastream-konfiguration. Med en `CNAME`-post i din DNS kan du skapa ett alias från ett domännamn till ett annat. Det här aliaset kan hjälpa till att få tredjepartstjänster att se ut som om de är en del av din egen domän, så att deras cookies ser ut som cookies från första part. När datainsamling från första part har aktiverats med en `CNAME` skickas alla cookies för din domän på begäranden som görs till datainsamlingsslutpunkten.

1. Arbeta med Adobe för att skapa en `CNAME`-post för datainsamling som används i din organisation. Se det [Adobe-hanterade certifikatprogrammet](https://experienceleague.adobe.com/sv/docs/core-services/interface/data-collection/adobe-managed-cert) för hela processen.
1. Aktivera alternativet **[!UICONTROL First Party ID Cookie]** i din datastream. Den här inställningen anger för Edge Network att referera till den angivna cookien vid sökning efter ett enhets-ID från en annan leverantör i stället för att leta upp värdet i identitetskartan. När du aktiverar den här inställningen måste du ange namnet på den cookie där FPID förväntas lagras. Mer information finns i [Skapa och konfigurera datastreams](/help/datastreams/configure.md#advanced-options).

   ![Plattformens gränssnittsbild visar datastream-konfigurationen som markerar cookie-inställningen för första parts-ID](/help/collection/js/assets/first-party-id-datastreams.png)

### Metod 2: Använd FPID i `identityMap` {#identityMap}

Som ett alternativ till att lagra FPID i din egen cookie kan du skicka FPID:t till Edge Network via identitetskartan.

Nedan visas ett exempel på hur du anger ett FPID i `identityMap`:

```json
{
  "identityMap": {
    "FPID": [
      {
        "id": "123e4567-e89b-42d3-9456-426614174000",
        "authenticatedState": "ambiguous",
        "primary": true
      }
    ]
  }
}
```

Precis som med andra identitetstyper kan du inkludera FPID med andra identiteter i `identityMap`. Följande exempel innehåller FPID med ett autentiserat CRM-ID:

```json
{
  "identityMap": {
    "FPID": [
      {
        "id": "123e4567-e89b-42d3-9456-426614174000",
        "authenticatedState": "ambiguous",
        "primary": false
      }
    ],
    "EMAIL": [
      {
        "id": "user@example.com",
        "authenticatedState": "authenticated",
        "primary": true
      }
    ]
  }
}
```

Om FPID finns i en cookie som läses av Edge Network när datainsamling från första part är aktiverat, ska du endast hämta det autentiserade CRM-ID:t:

```json
{
  "identityMap": {
    "EMAIL": [
      {
        "id": "user@example.com",
        "authenticatedState": "authenticated",
        "primary": true
      }
    ]
  }
}
```

Följande `identityMap` ger ett felsvar från Edge Network eftersom den saknar `primary`-indikatorn för FPID. Minst ett ID i `identityMap` måste markeras som `primary`.

```json
{
  "identityMap": {
    "FPID": [
      {
        "id": "123e4567-e89b-12d3-a456-426614174000",
        "authenticatedState": "ambiguous"
      }
    ],
    "EMAIL": [
      {
        "id": "user@example.com",
        "authenticatedState": "authenticated"
      }
    ]
  }
}
```

## Migrera till FPID {#migrating-to-fpid}

Om du migrerar till enhets-ID:n från en tidigare implementering kan det vara svårt att se hur övergången kan se ut på en låg nivå. För att illustrera denna process bör du överväga ett scenario där en kund som tidigare besökt er webbplats deltar och vilken effekt en FPID-migrering skulle ha på hur kunden identifieras i Adobe-lösningar.

![Diagram som visar hur en kunds ID-värden uppdateras mellan besök efter migrering till FPID](/help/collection/js/assets/identity/tracking/visits.png)

| Besök | Beskrivning |
| --- | --- |
| Första besök | Anta att du ännu inte har börjat ange FPID-cookie. Det ECID som finns i [AMCV-cookien](https://experienceleague.adobe.com/docs/id-service/using/intro/cookies.html?lang=sv-SE#section-c55af54828dc4cce89f6118655d694c8) är den identifierare som används för att identifiera besökaren. |
| Andra besöket | Utrullningen av FPID-lösningen har startats. Befintligt ECID finns fortfarande och är fortfarande den primära identifieraren för besökaridentifiering. |
| Tredje besök | Mellan det andra och tredje besöket har det gått tillräckligt lång tid innan ECID har tagits bort på grund av webbläsarprincipen. Eftersom FPID angavs med en DNS `A`-post kvarstår dock FPID:t. FPID betraktas nu som det primära ID:t och används för att skicka ut ECID, som skrivs till slutanvändarens enhet. Användaren betraktas nu som en ny besökare i Adobe Experience Platform- och Experience Cloud-lösningar. |
| Fjärde besöket | Mellan det tredje och fjärde besöket har det gått tillräckligt lång tid innan ECID har tagits bort på grund av webbläsarprincipen. Precis som vid det föregående besöket beror FPID fortfarande på hur det var inställt. Nu genereras samma ECID som vid det föregående besöket. Användaren ser samma användare som vid föregående besök i Adobe Experience Platform- och Experience Cloud-lösningar. |
| Femte besöket | Mellan den fjärde och femte besöken rensade slutanvändaren alla cookies i webbläsaren. Ett nytt FPID genereras och används för att skapa ett nytt ECID. Användaren betraktas nu som en ny besökare i Adobe Experience Platform- och Experience Cloud-lösningar. |
