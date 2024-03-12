---
title: Första parts enhets-ID i Web SDK
description: Lär dig hur du konfigurerar FPID (First-party device ID) för Adobe Experience Platform Web SDK.
exl-id: c3b17175-8a57-43c9-b8a0-b874fecca952
source-git-commit: 9f10d48357b7fb28dc54375a4d077d0a1961a746
workflow-type: tm+mt
source-wordcount: '1986'
ht-degree: 0%

---


# Första parts enhets-ID i Web SDK

Adobe Experience Platform Web SDK tilldelar [Adobe Experience Cloud ID (ECID)](https://experienceleague.adobe.com/docs/experience-platform/identity/ecid.html) till besökare via cookies för att spåra användarbeteenden. Om du vill ta hänsyn till webbläsarbegränsningar för cookie-intervall kan du välja att ställa in och hantera dina egna enhetsidentifierare i stället. Dessa kallas för FPID (First-party device ID).

>[!NOTE]
>
>Stöd för första parts enhets-ID är endast tillgängligt när du skickar data till Platform Edge Network via Platform Web SDK.

>[!IMPORTANT]
>
>Enhets-ID:n från första part är inte kompatibla med [cookies från tredje part](../../tags/extensions/client/web-sdk/web-sdk-extension-configuration.md#identity) i Web SDK.
>Du kan antingen använda enhets-ID:n från en annan leverantör eller använda cookies från tredje part, men du kan inte använda båda funktionerna samtidigt.

I det här dokumentet beskrivs hur du konfigurerar enhets-ID:n från första part för implementeringen av Platform Web SDK.

## Förutsättningar

I den här handboken förutsätts du känna till hur identitetsdata fungerar för Platform Web SDK, inklusive rollen för ECID och `identityMap`. Se översikten på [identitetsdata i Web SDK](./overview.md) för mer information.

## Använda FPID

FPID:n spårar besökare genom att använda cookies från första part. cookies från första part är mest effektiva när de ställs in med en server som använder en DNS [En post](https://datatracker.ietf.org/doc/html/rfc1035) (för IPv4) eller [AAAA-post](https://datatracker.ietf.org/doc/html/rfc3596) (för IPv6), till skillnad från en DNS CNAME- eller JavaScript-kod.

>[!IMPORTANT]
>
>`A` eller `AAAA` poster stöds bara för att ange och spåra cookies. Den primära metoden för datainsamling är via en DNS CNAME. Med andra ord anges FPID:n med en A-post eller AAAA-post och skickas sedan till Adobe med en CNAME.
>
>The [Adobe-hanterat certifikatprogram](https://experienceleague.adobe.com/docs/core-services/interface/administration/ec-cookies/cookies-first-party.html#adobe-managed-certificate-program) stöds fortfarande för datainsamling från första part.

När en FPID-cookie har angetts kan dess värde hämtas och skickas till Adobe när händelsedata samlas in. Insamlade FPID används som frön för att generera ECID, som även fortsättningsvis är de primära identifierarna i Adobe Experience Cloud-program.

Om du vill skicka ett FPID för en webbplatsbesökare till Platform Edge Network måste du inkludera FPID i `identityMap` för besökaren. Se avsnittet senare i det här dokumentet på [använda FPID i `identityMap`](#identityMap) för mer information.

### Krav för ID-formatering

Platform Edge Network godkänner endast ID:n som uppfyller [UUIDv4-format](https://datatracker.ietf.org/doc/html/rfc4122). Enhets-ID som inte är i UUIDv4-format kommer att avvisas.

Generering av ett UUID resulterar nästan alltid i ett unikt, slumpmässigt ID, där sannolikheten för en kollision är försumbar. UUIDv4 kan inte dirigeras med IP-adresser eller någon annan personligt identifierbar information (PII). UUID är vanligt förekommande och bibliotek finns för praktiskt taget alla programmeringsspråk för att generera dem.

## Ställa in cookie för första parts-ID i användargränssnittet för datastreams {#setting-cookie-datastreams}

Du kan ange ett cookie-namn i användargränssnittet för datastreams, där [!DNL FPID] kan finnas i stället för att du behöver läsa cookie-värdet och inkludera FPID i identitetskartan.

>[!IMPORTANT]
>
>Den här funktionen kräver att du har [Insamling av data från första part](https://experienceleague.adobe.com/docs/core-services/interface/administration/ec-cookies/cookies-first-party.html?lang=en) aktiverat.

Se [datastreams-dokumentation](../../datastreams/configure.md) för detaljerad information om hur du konfigurerar ett datastream.

Aktivera **[!UICONTROL First Party ID Cookie]** alternativ. Den här inställningen anger för Edge Network att referera till en angiven cookie när du söker efter ett enhets-ID från en annan leverantör, i stället för att leta upp det här värdet i [Identitetskarta](#identityMap).

Läs dokumentationen om [cookies från första part](https://experienceleague.adobe.com/docs/core-services/interface/administration/ec-cookies/cookies-first-party.html) om du vill ha mer information om hur de arbetar med Adobe Experience Cloud.

![Bild av användargränssnittet för plattformen som visar datastream-konfigurationen och som markerar cookie-inställningen för första parts-ID](../assets/first-party-id-datastreams.png)

När du aktiverar den här inställningen måste du ange namnet på den cookie där ID:t ska lagras.

När du använder ID:n för första part kan du inte utföra synkroniseringar av ID:n från tredje part. Synkronisering av tredje parts-ID är beroende av [!DNL Visitor ID] och `UUID` genereras av den tjänsten. När du använder funktionaliteten för första parts-ID genereras ECID utan att [!DNL Visitor ID] , vilket gör det omöjligt att synkronisera tredje parts-ID.

När du använder ID:n från första part stöds inte Audience Manager-funktioner som är inriktade på aktivering på partnerplattformar, eftersom synk för Audience Manager partner-ID i huvudsak baseras på `UUIDs` eller `DIDs`. Det ECID som härleds från ett första parts-ID är inte länkat till en `UUID`, vilket gör det oadresserbart.

## Ange en cookie med din egen server

När du ställer in en cookie med en server som du äger kan olika metoder användas för att förhindra att cookien begränsas på grund av webbläsarprinciper:

* Generera cookies med serverskriptspråk
* Ange cookies som svar på en API-begäran som görs till en underdomän eller annan slutpunkt på webbplatsen
* Generera cookies med CMS
* Generera cookies med ett CDN

>[!IMPORTANT]
>
>Cookies som ställs in med JavaScript `document.cookie` Metoden skyddas nästan aldrig av webbläsarprinciper som begränsar varaktigheten för cookies.

### När cookien ska ställas in

FPID-cookien bör helst anges innan du skickar några förfrågningar till Edge Network. I scenarier där detta inte är möjligt genereras dock ett ECID fortfarande med befintliga metoder och fungerar som primär identifierare så länge som cookien finns.

Om man utgår ifrån att ECID så småningom påverkas av en policy för borttagning av webbläsare, men inte av FPID, kommer FPID att bli den primära identifieraren vid nästa besök och kommer att användas för att förorsaka ECID vid varje påföljande besök.

### Ange förfallodatum för cookien

Att ange förfallodatum för en cookie är något som du bör tänka på noga när du implementerar FPID-funktionen. När du beslutar om detta bör du ta hänsyn till de länder eller regioner där organisationen arbetar tillsammans med lagstiftningen och policyn i var och en av dessa regioner.

Som en del av det här beslutet kanske du vill anta en företagsomfattande policy för cookie-inställningar eller en som varierar för användare på de olika språkområden där du arbetar.

Oavsett vilken inställning du väljer för den första förfallodagen för en cookie måste du se till att du inkluderar logik som förlänger förfallotiden för cookien varje gång ett nytt besök på webbplatsen inträffar.

## Påverkan av cookie-flaggor

Det finns olika cookie-flaggor som påverkar hur cookies hanteras i olika webbläsare:

* [`HTTPOnly`](#http-only)
* [&quot;Säker&quot;](#secure)
* [&quot;SameSite&quot;](#same-site)

### `HTTPOnly` {#http-only}

Cookies som anges med `HTTPOnly` kan inte nås med skript på klientsidan. Det innebär att om du anger en `HTTPOnly` flagga när du anger FPID måste du använda ett skriptspråk på serversidan för att läsa cookie-värdet som ska inkluderas i `identityMap`.

Om du väljer att låta Platform Edge Network läsa värdet för FPID-cookien anger du `HTTPOnly` -flaggan säkerställer att värdet inte är tillgängligt för klientskript, men inte har någon negativ inverkan på plattformens Edge-nätverks förmåga att läsa cookien.

>[!NOTE]
>
>Användning av `HTTPOnly` -flaggan påverkar inte cookie-principerna som kan begränsa cookie-livstiden. Men det är fortfarande något du bör tänka på när du anger och läser värdet för FPID.

### `Secure` {#secure}

Cookies som anges med `Secure` -attribut skickas bara till servern med en krypterad begäran via HTTPS-protokollet. Om du använder den här flaggan kan du se till att angripare i mitten inte lätt kommer åt värdet på cookien. När det är möjligt är det alltid en bra idé att ställa in `Secure` flagga.

### `SameSite` {#same-site}

The `SameSite` -attribut låter servrar avgöra om cookies skickas med förfrågningar mellan webbplatser. Attributet ger visst skydd mot attacker med förfalskning över flera webbplatser. Det finns tre möjliga värden: `Strict`, `Lax`och `None`. Kontakta ditt interna team för att ta reda på vilken inställning som är rätt för din organisation.

Om nej `SameSite` har angetts, standardinställningen för vissa webbläsare är nu `SameSite=Lax`.

## Använda FPID i `identityMap` {#identityMap}

Nedan visas ett exempel på hur du ställer in en FPID i `identityMap`:

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

Precis som med andra identitetstyper kan du inkludera FPID med andra identiteter i `identityMap`. Följande är ett exempel på FPID som ingår i ett autentiserat CRM-ID:

```json
{
  "identityMap": {
    "FPID": [
      {
        "id": "123e4567-e89b-42d3-9456-426614174000",
        "authenticatedState": "ambiguous",
        "primary": true
      }
    ],
    "EMAIL": [
      {
        "id": "email@mail.com",
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
        "id": "email@mail.com",
        "authenticatedState": "authenticated",
        "primary": true
      }
    ]
  }
}
```

Följande `identityMap` skulle resultera i ett felsvar från Edge Network eftersom det saknar `primary` -indikator för FPID. Minst ett ID finns i `identityMap` måste markeras som `primary`.

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
        "id": "email@mail.com",
        "authenticatedState": "authenticated"
      }
    ]
  }
}
```

Felsvaret som returneras av Edge Network i det här fallet liknar följande:

```json
{
    "type": "https://ns.adobe.com/aep/errors/EXEG-0306-400",
    "status": 400,
    "title": "No primary identity set in request (event)",
    "detail": "No primary identity found in the input event. Update the request accordingly to your schema and try again.",
    "report": {
        "requestId": "{REQUEST_ID}",
        "configId": "{CONFIG_ID}",
        "orgId": "{ORG_ID}"
    }
}
```

## ID-hierarki

När både ett ECID och ett FPID finns, prioriteras ECID för att identifiera användaren. Detta garanterar att när ett befintligt ECID finns i webbläsar-cookie-arkivet förblir det den primära identifieraren och befintligt antal besökare riskerar inte att påverkas. För befintliga användare blir FPID inte den primära identiteten förrän ECID:t upphör att gälla eller tas bort som ett resultat av en webbläsarprincip eller manuell process.

Identiteter prioriteras i följande ordning:

1. ECID ingår i `identityMap`
1. ECID lagras i en cookie
1. FPID ingår i `identityMap`
1. FPID som lagras i en cookie

## Migrera till enhets-ID:n från första part

Om du migrerar till att använda FPID:n från en tidigare implementering kan det vara svårt att se hur övergången kan se ut på en låg nivå.

För att illustrera denna process bör du överväga ett scenario där en kund som tidigare besökt er webbplats deltar och vilken inverkan en FPID-migrering skulle ha på hur kunden identifieras i Adobe.

![Bild som visar hur en kunds ID-värden uppdateras mellan besök efter migrering till FPID:n](../assets/identity/tracking/visits.png)

>[!IMPORTANT]
>
>The `ECID` cookie prioriteras alltid framför `FPID`.

| Besök | Beskrivning |
| --- | --- |
| Första besök | Anta att du ännu inte har börjat ange FPID-cookie. Det ECID som finns i [AMCV cookie](https://experienceleague.adobe.com/docs/id-service/using/intro/cookies.html#section-c55af54828dc4cce89f6118655d694c8) blir den identifierare som används för att identifiera besökaren. |
| Andra besök | Utrullning av första parts enhets-ID-lösning har startats. Befintligt ECID finns fortfarande och är fortfarande den primära identifieraren för besökaridentifiering. |
| Tredje besök | Mellan det andra och tredje besöket har det gått tillräckligt lång tid innan ECID har tagits bort på grund av webbläsarprincipen. Eftersom FPID angavs med en DNS A-post kvarstår dock FPID:t. FPID betraktas nu som det primära ID:t och används för att skicka ut ECID, som skrivs till slutanvändarens enhet. Användaren skulle nu betraktas som en ny besökare i lösningarna Adobe Experience Platform och Experience Cloud. |
| Fjärde besök | Mellan det tredje och fjärde besöket har det gått tillräckligt lång tid innan ECID har tagits bort på grund av webbläsarprincipen. Precis som vid det föregående besöket beror FPID fortfarande på hur det var inställt. Nu genereras samma ECID som vid det föregående besöket. Användaren uppfattar Experience Platform och Experience Cloud som samma användare som vid det föregående besöket. |
| Femte besök | Mellan den fjärde och femte besöken rensade slutanvändaren alla cookies i sin webbläsare. Ett nytt FPID genereras och används för att skapa ett nytt ECID. Användaren skulle nu betraktas som en ny besökare i lösningarna Adobe Experience Platform och Experience Cloud. |

{style="table-layout:auto"}

## Vanliga frågor och svar

Nedan följer en lista med svar på vanliga frågor om enhets-ID:n från första part.

### Hur skickar jag ett ID annorlunda än att bara generera ett ID?

Begreppet dirigering är unikt i och med att det FPID som skickas till Adobe Experience Cloud konverteras till ett ECID med hjälp av en deterministisk algoritm. Varje gång samma FPID skickas till Adobe Experience Platform Edge Network dirigeras samma ECID från FPID.

### När ska det första parts enhets-ID genereras?

För att minska den potentiella besökarinflationen bör FPID genereras innan du gör din första begäran med Web SDK. Om du inte kan göra detta kommer dock ett ECID att genereras för den användaren och användas som primär identifierare. Det FPID som genererades kommer inte att bli den primära identifieraren förrän ECID:t inte längre finns.

### Vilka datainsamlingsmetoder stöder enhets-ID:n från första part?

För närvarande stöder endast Web SDK FPID.

### Lagras FPID:n på någon plattforms- eller Experience Cloud-lösning?

När FPID har använts för att förväxla ett ECID tas det bort från `identityMap` och ersatts med det ECID som har genererats. FPID lagras inte i någon Adobe Experience Platform- eller Experience Cloud-lösning.
