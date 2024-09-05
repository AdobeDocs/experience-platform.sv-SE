---
title: Första parts enhets-ID i Web SDK
description: Lär dig hur du konfigurerar FPID (First-party device ID) i Adobe Experience Platform Web SDK.
exl-id: c3b17175-8a57-43c9-b8a0-b874fecca952
source-git-commit: 1cb38e3eaa83f2ad0e7dffef185d5edaf5e6c38c
workflow-type: tm+mt
source-wordcount: '1900'
ht-degree: 0%

---


# Första parts enhets-ID i Web SDK

Adobe Experience Platform Web SDK tilldelar [Adobe Experience Cloud ID:n (ECID:n)](https://experienceleague.adobe.com/docs/experience-platform/identity/ecid.html) till webbplatsbesökare genom att använda cookies för att spåra användarbeteenden. Om du vill ta hänsyn till webbläsarbegränsningar för cookie-intervall kan du välja att ställa in och hantera dina egna enhetsidentifierare i stället. Dessa kallas för enhets-ID:n från första part (`FPIDs`).

>[!NOTE]
>
>Stöd för första parts enhets-ID är endast tillgängligt när data skickas till Experience Platform Edge Network via Web SDK.

>[!IMPORTANT]
>
>Första parts enhets-ID är inte kompatibelt med funktionen [cookies](../../tags/extensions/client/web-sdk/web-sdk-extension-configuration.md#identity) från tredje part i Web SDK.
>Du kan antingen använda enhets-ID:n från en annan leverantör eller använda cookies från tredje part, men du kan inte använda båda funktionerna samtidigt.

I det här dokumentet beskrivs hur du konfigurerar enhets-ID:n från första part för Web SDK-implementeringen.

## Förhandskrav

I den här handboken förutsätts du känna till hur identitetsdata fungerar för Platform Web SDK, inklusive rollen för ECID:n och `identityMap`. Mer information finns i översikten över [identitetsdata i Web SDK](./overview.md).

## Använda FPID (First-party device ID) {#using-fpid}

Första parts enhets-ID ([!DNL FPIDs]) spårar besökare med hjälp av cookies från första part. Första parts-cookies är mest effektiva när de ställs in med en server som använder en DNS [A-post](https://datatracker.ietf.org/doc/html/rfc1035) (för IPv4) eller [AAAA-post](https://datatracker.ietf.org/doc/html/rfc3596) (för IPv6), i motsats till en DNS [!DNL CNAME] - eller [!DNL JavaScript] -kod.

>[!IMPORTANT]
>
>[!DNL A]- eller [!DNL AAAA]-poster stöds bara för att ange och spåra cookies. Den primära metoden för datainsamling är via en [!DNL DNS] [!DNL CNAME]. [!DNL FPIDs] anges med andra ord med en [!DNL A]- eller [!DNL AAAA]-post och skickas sedan till Adobe med en [!DNL CNAME].
>
>Det [Adobe-hanterade certifikatprogrammet](https://experienceleague.adobe.com/docs/core-services/interface/administration/ec-cookies/cookies-first-party.html#adobe-managed-certificate-program) stöds fortfarande för datainsamling från första part.

När en [!DNL FPID]-cookie har angetts kan dess värde hämtas och skickas till Adobe när händelsedata samlas in. Insamlade [!DNL FPIDs] används som startvärde för att generera [!DNL ECIDs], som även fortsättningsvis är de primära identifierarna i Adobe Experience Cloud-program.

Om du vill skicka en [!DNL FPID] för en webbplatsbesökare till Edge Network måste du inkludera [!DNL FPID] i `identityMap` för den besökaren. Mer information finns i avsnittet längre ned i det här dokumentet om [att använda FPID:n i `identityMap`](#identityMap).

### Krav för formatering av enhets-ID från första part {#formatting-requirements}

Edge Network accepterar bara [!DNL IDs] som överensstämmer med [UIDv4-formatet](https://datatracker.ietf.org/doc/html/rfc4122). Enhets-ID:n som inte är i formatet [!DNL UUIDv4] kommer att avvisas.

Generering av [!DNL UUID] resulterar nästan alltid i ett unikt, slumpmässigt ID, med sannolikheten för att en kollision inträffar är försumbar. [!DNL UUIDv4] kan inte dirigeras med IP-adresser eller annan personlig identifierbar information ([!DNL PII]). [!DNL UUIDs] är vanligt förekommande och bibliotek kan hittas för praktiskt taget alla programmeringsspråk för att generera dem.

## Ställa in en cookie för ett första parts-ID i användargränssnittet för datastreams {#setting-cookie-datastreams}

Du kan ange ett cookie-namn i Datastreams-användargränssnittet, där [!DNL FPID] kan finnas, i stället för att behöva läsa cookie-värdet och inkludera [!DNL FPID] i identitetskartan.

>[!IMPORTANT]
>
>Den här funktionen kräver att du har [Första part-datainsamling](https://experienceleague.adobe.com/docs/core-services/interface/administration/ec-cookies/cookies-first-party.html?lang=en) aktiverad.

Mer information om hur du konfigurerar ett datastream finns i [datastreams-dokumentationen](../../datastreams/configure.md).

Aktivera alternativet **[!UICONTROL First Party ID Cookie]** när du konfigurerar ditt datastream. Den här inställningen instruerar Edge Network att referera till en angiven cookie när ett enhets-ID från en annan tillverkare identifieras, i stället för att det här värdet slås upp i [identitetskartan](#identityMap).

Mer information om hur de fungerar med Adobe Experience Cloud finns i dokumentationen om [cookies från första part](https://experienceleague.adobe.com/docs/core-services/interface/administration/ec-cookies/cookies-first-party.html).

![Plattformens gränssnittsbild visar datastream-konfigurationen som markerar cookie-inställningen för första parts-ID](../assets/first-party-id-datastreams.png)

När du aktiverar den här inställningen måste du ange namnet på den cookie där ID:t ska lagras.

När du använder ID:n från första part kan du inte synkronisera ID:n från tredje part. Synkronisering av tredjeparts-ID är beroende av tjänsten [!DNL Visitor ID] och den `UUID` som genereras av den tjänsten. När du använder funktionen för första parts-ID genereras [!DNL ECID] utan att tjänsten [!DNL Visitor ID] används, vilket gör det omöjligt att synkronisera tredje parts-ID.

När du använder förstaparts-ID:n stöds inte [Audience Manager](https://experienceleague.adobe.com/en/docs/audience-manager)-funktioner som är avsedda för aktivering på partnerplattformar, eftersom Audience Manager partner-ID-synk oftast baseras på `UUIDs` eller `DIDs`. [!DNL ECID] som härleds från ett första part-ID är inte länkat till en `UUID`, vilket gör den oadresserbar.

## Ange en cookie med din egen server {#set-cookie-server}

När du ställer in en cookie med en server som du äger kan du använda olika metoder för att förhindra att cookien begränsas på grund av webbläsarprinciper:

* Generera cookies med serverskriptspråk
* Ange cookies som svar på en API-begäran som görs till en underdomän eller annan slutpunkt på webbplatsen
* Generera cookies med en [!DNL CMS]
* Generera cookies med en [!DNL CDN]

>[!IMPORTANT]
>
>Cookies som anges med JavaScript `document.cookie`-metod kommer nästan aldrig att skyddas från webbläsarprinciper som begränsar cookie-varaktighet.

### När cookien ska ställas in {#when-to-set-cookie}

Cookien [!DNL FPID] bör helst anges innan någon begäran görs till Edge Network. I scenarier där detta inte är möjligt genereras dock [!DNL ECID] fortfarande med befintliga metoder och fungerar som primär identifierare så länge som cookien finns.

Om [!DNL ECID] så småningom påverkas av en princip för borttagning av webbläsare, men [!DNL FPID] inte gör det, kommer [!DNL FPID] att bli den primära identifieraren vid nästa besök och kommer att användas för att dirigera [!DNL ECID] vid varje efterföljande besök.

### Ange förfallodatum för cookien {#set-expiration}

Att ange förfallodatum för en cookie är något som du bör tänka på noga när du implementerar funktionen [!DNL FPID]. När du beslutar om detta bör du ta hänsyn till de länder eller regioner där organisationen arbetar tillsammans med lagstiftningen och policyn i var och en av dessa regioner.

Som en del av det här beslutet kanske du vill anta en företagsomfattande policy för cookie-inställningar eller en som varierar för användare på de olika språkområden där du arbetar.

Oavsett vilken inställning du väljer för den första förfallodagen för en cookie måste du se till att du inkluderar logik som förlänger förfallotiden för cookien varje gång ett nytt besök på webbplatsen inträffar.

## Påverkan av cookie-flaggor {#cookie-flag-impact}

Det finns olika cookie-flaggor som påverkar hur cookies hanteras i olika webbläsare:

* [`HTTPOnly`](#http-only)
* [&quot;Säker&quot;](#secure)
* [&quot;SameSite&quot;](#same-site)

### `HTTPOnly` {#http-only}

Det går inte att komma åt cookies som har angetts med flaggan `HTTPOnly` med skript på klientsidan. Det innebär att om du anger en `HTTPOnly`-flagga när du anger [!DNL FPID] måste du använda ett skriptspråk på serversidan för att läsa cookie-värdet som ska inkluderas i `identityMap`.

Om du väljer att låta Edge Network läsa värdet för cookien [!DNL FPID] kan du genom att ställa in flaggan `HTTPOnly` se till att värdet inte är tillgängligt för klientskript, men inte har någon negativ inverkan på Edge Network för att läsa cookien.

>[!NOTE]
>
>Användning av flaggan `HTTPOnly` påverkar inte cookie-principerna som kan begränsa cookie-livstiden. Men det är fortfarande något du bör tänka på när du anger och läser värdet för [!DNL FPID].

### `Secure` {#secure}

Cookies som angetts med attributet `Secure` skickas bara till servern med en krypterad begäran via protokollet [!DNL HTTPS]. Om du använder den här flaggan kan du se till att angripare i mitten inte lätt kommer åt värdet på cookien. När det är möjligt är det alltid en bra idé att ange flaggan `Secure`.

### `SameSite` {#same-site}

Med attributet `SameSite` kan servrar avgöra om cookies skickas med förfrågningar mellan webbplatser. Attributet ger visst skydd mot attacker med förfalskning över flera webbplatser. Det finns tre möjliga värden: `Strict`, `Lax` och `None`. Kontakta ditt interna team för att ta reda på vilken inställning som är rätt för din organisation.

Om inget `SameSite`-attribut anges är standardinställningen för vissa webbläsare nu `SameSite=Lax`.

## Använda FPID i `identityMap` {#identityMap}

Nedan visas ett exempel på hur du skulle ange en [!DNL FPID] i `identityMap`:

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

Precis som med andra identitetstyper kan du inkludera [!DNL FPID] med andra identiteter i `identityMap`. Följande är ett exempel på [!DNL FPID] som ingår i en autentiserad [!DNL CRM ID]:

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
        "id": "email@mail.com",
        "authenticatedState": "authenticated",
        "primary": true
      }
    ]
  }
}
```

Om [!DNL FPID] finns i en cookie som läses av Edge Network när datainsamling från första part är aktiverad, ska du bara hämta den autentiserade [!DNL CRM ID]:

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

Följande `identityMap` skulle resultera i ett felsvar från Edge Network eftersom `primary`-indikatorn för [!DNL FPID] saknas. Minst ett av ID:n i `identityMap` måste markeras som `primary`.

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

Felsvaret som Edge Network returnerade i det här fallet liknar följande:

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

## ID-hierarki {#id-hierarchy}

När både [!DNL ECID] och [!DNL FPID] finns med prioriteras [!DNL ECID] när användaren identifieras. Detta garanterar att när en befintlig [!DNL ECID] finns i webbläsar-cookie-arkivet förblir den primära identifieraren och befintligt antal besökare riskerar inte att påverkas. För befintliga användare blir [!DNL FPID] inte den primära identiteten förrän [!DNL ECID] förfaller eller tas bort som ett resultat av en webbläsarprincip eller manuell process.

Identiteter prioriteras i följande ordning:

1. [!DNL ECID] ingår i `identityMap`
1. [!DNL ECID] lagras i en cookie
1. [!DNL FPID] ingår i `identityMap`
1. [!DNL FPID] lagras i en cookie

## Migrera till enhets-ID:n från första part {#migrating-to-fpid}

Om du migrerar till enhets-ID:n från en tidigare implementering kan det vara svårt att se hur övergången kan se ut på en låg nivå.

För att illustrera den här processen bör du överväga ett scenario där en kund som tidigare besökt din webbplats deltar och vilken inverkan en [!DNL FPID]-migrering skulle ha på hur kunden identifieras i Adobe-lösningar.

![Diagram som visar hur en kunds ID-värden uppdateras mellan besök efter migrering till FPID](../assets/identity/tracking/visits.png)

>[!IMPORTANT]
>
>Cookien `ECID` prioriteras alltid framför `FPID`.

| Besök | Beskrivning |
| --- | --- |
| Första besök | Anta att du ännu inte har börjat ange cookien [!DNL FPID]. [!DNL ECID] i [AMCV-cookien](https://experienceleague.adobe.com/docs/id-service/using/intro/cookies.html#section-c55af54828dc4cce89f6118655d694c8) är den identifierare som används för att identifiera besökaren. |
| Andra besöket | Rollout of the [!DNL FPID] solution has started. Befintlig [!DNL ECID] finns fortfarande och är fortfarande den primära identifieraren för besökaridentifiering. |
| Tredje besök | Mellan det andra och tredje besöket har det gått tillräckligt lång tid att ta bort [!DNL ECID] på grund av webbläsarprincipen. Eftersom [!DNL FPID] angavs med en [!DNL DNS] [!DNL A]-post kvarstår [!DNL FPID]. [!DNL FPID] betraktas nu som primärt ID och används för att skapa startvärde för [!DNL ECID], som skrivs till slutanvändarens enhet. Användaren skulle nu betraktas som en ny besökare i lösningarna Adobe Experience Platform och Experience Cloud. |
| Fjärde besöket | Mellan det tredje och fjärde besöket har det gått tillräckligt lång tid att ta bort [!DNL ECID] på grund av webbläsarprincipen. Precis som vid det föregående besöket beror [!DNL FPID] fortfarande på hur det var inställt. Den här gången genereras samma [!DNL ECID] som det föregående besöket. Användaren uppfattar Experience Platform och Experience Cloud som samma användare som vid det föregående besöket. |
| Femte besöket | Mellan den fjärde och femte besöken rensade slutanvändaren alla cookies i sin webbläsare. En ny [!DNL FPID] genereras och används för att skapa en ny [!DNL ECID]. Användaren skulle nu betraktas som en ny besökare i lösningarna Adobe Experience Platform och Experience Cloud. |

{style="table-layout:auto"}

## Vanliga frågor och svar {#faq}

Nedan följer en lista med svar på vanliga frågor om enhets-ID:n från första part.

### Hur skickar jag ett ID annorlunda än att bara generera ett ID?

Begreppet dirigering är unikt i och med att [!DNL FPID] som skickas till Adobe Experience Cloud konverteras till [!DNL ECID] med hjälp av en deterministisk algoritm. Varje gång samma [!DNL FPID] skickas till Edge Network dirigeras samma [!DNL ECID] från [!DNL FPID].

### När ska det första parts enhets-ID genereras?

Om du vill minska den potentiella besökarinflationen bör [!DNL FPID] genereras innan du gör din första begäran med Web SDK. Om du inte kan göra detta kommer dock [!DNL ECID] fortfarande att genereras för den användaren och kommer att användas som primär identifierare. [!DNL FPID] som skapades blir inte primär identifierare förrän [!DNL ECID] inte längre finns.

### Vilka datainsamlingsmetoder stöder enhets-ID:n från första part?

För närvarande stöder endast Web SDK enhets-ID:n från första part.

### Lagras första parts enhets-ID på någon plattforms- eller Experience Cloud-lösning?

När [!DNL FPID] har använts för att skapa startvärdet för en [!DNL ECID] tas den bort från `identityMap` och ersätts med [!DNL ECID] som har genererats. [!DNL FPID] lagras inte i några Adobe Experience Platform- eller Experience Cloud-lösningar.
