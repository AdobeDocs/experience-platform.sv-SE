---
title: Felhantering
description: Lär dig hur fel hanteras i Reactor API.
exl-id: 336c0ced-1067-4519-94e1-85aea700fce6
source-git-commit: f3c23665229a83d6c63c7d6026ebf463069d8ad9
workflow-type: tm+mt
source-wordcount: '1062'
ht-degree: 0%

---

# Felhantering

När ett problem inträffar när ett anrop görs till Reactor API, kan ett fel returneras på något av följande sätt:

* **Omedelbara fel**: När du utför en begäran som resulterar i ett omedelbart fel returneras ett felsvar av API:t, där HTTP-statusen återspeglar den allmänna feltypen som inträffade.
* **Försenade fel**: När du utför en API-begäran som resulterar i ett fördröjt fel (t.ex. en asynkron aktivitet) kan ett fel returneras av API:t i `meta.status_details` för en relaterad resurs.

## Felformat

Felsvar syftar till att anpassa [JSON:API-felspecifikation](http://jsonapi.org/format/#errors)och i allmänhet följa följande struktur:

```json
{
  "errors": [
    {
      "id": "8a5526da-ab12-4be9-b084-2efe537f388c",
      "status": "404",
      "code": "not-found",
      "title": "Record Not Found",
      "meta": {
        "request_id": "jfb0dQ2e0XVTkQ6AOfEJFfTDjguw9x3d"
      },
      "source": {
        "pointer": "/data"
      }
    }
  ]
}
```

| Egenskap | Beskrivning |
| --- | --- |
| `id` | En unik identifierare för den aktuella förekomsten av problemet. |
| `status` | HTTP-statuskoden som gäller det här problemet, uttryckt som ett strängvärde. |
| `code` | En programspecifik felkod, uttryckt som ett strängvärde. |
| `title` | En kort, läsbar sammanfattning av problemet som **bör inte ändras** från förekomst till förekomst, utom för lokalisering. |
| `detail` | En läsbar förklaring som är specifik för den här förekomsten av problemet. Gilla `title`kan fältets värde lokaliseras. |
| `source` | Ett objekt som innehåller referenser till felets källa, eventuellt inklusive någon av följande medlemmar:<ul><li>`pointer`: a [JSON-pekare (RFC6901)](https://datatracker.ietf.org/doc/html/rfc6901) sträng som refererar till den associerade entiteten i begärandedokumentet (som `/data` för ett primärt dataobjekt, eller `/data/attributes/title` för ett specifikt attribut).</li></ul> |
| `meta` | Ett objekt som innehåller metadata om felet som inte är standard. |

{style="table-layout:auto"}

## Felreferens

I följande tabell visas de olika fel som API:t kan returnera.

| Feltitel | Beskrivning |
| --- | --- |
| `authentication-failure` | Din IMS-åtkomsttoken är ogiltig. Du kan hämta en ny åtkomsttoken genom att logga in igen. Eller för tekniska konton: skapa en ny JWT och byta ut en IMS-åtkomsttoken. |
| `connection-refused` | Det gick inte att upprätta en anslutning till servern. |
| `decrypt-bad-passphrase` | Det gick inte att dekryptera data med den angivna lösenfrasen. |
| `decrypt-failed` | Det gick inte att dekryptera data med den angivna privata nyckeln. Kontrollera att nyckeln fungerar lokalt och att mellanrummet har trimmats. |
| `decrypt-no-data` | Data kan inte dekrypteras utan en privat nyckel. Ange en krypterad privat nyckel. |
| `delegate-descriptor-unresolved` | Tillägget tillhandahöll inte den förväntade definitionen för den här delegatbeskrivningen. Tillägget kan behöva uppdateras. |
| `deleted-resources` | Resurserna som du försöker lägga till i biblioteket har tagits bort. |
| `environment-in-use` | En miljö kan bara tilldelas ett bibliotek i taget. Alternativ 1 är att välja en annan miljö. Alternativ 2 är att frigöra miljön genom att flytta biblioteket till en annan miljö eller ta bort biblioteket. |
| `environment-required` | Biblioteket måste ha tilldelats en miljö innan du kan skapa ett bygge. |
| `extension-not-found` | Tillägget som definierar ett dataelement eller en regelkomponent inkluderas inte i biblioteket. Kontrollera att alla nödvändiga tillägg har lagts till i biblioteket. |
| `extension-package-path-error` | En sökväg som definierats i extension.json var felaktigt konstruerad. |
| `extension-package-transform-definition-error` | Du har definierat en ogiltig omformning för en objektegenskap. Varje objektegenskap kan ha en definierad omformning och måste vara en filomformning eller en funktionsomformning. |
| `extension-package-zip-error` | Ett fel inträffade när ExtensionPackage packades upp eller när filerna packades upp för distribution. |
| `host-in-use` | En värd kan inte tas bort om en eller flera miljöer använder den. |
| `host-required` | Den miljö som är tilldelad det här biblioteket har ingen giltig värd. Kontrollera vilken miljö som är tilldelad biblioteket. Tilldela sedan en giltig värd till den miljön. |
| `host-type-error` | Endast SFTP-värdar måste ha autentiseringsuppgifter verifierade innan de kan användas, så pretestet är bara tillgängligt för den värdtypen. |
| `illegal-custom-code-transform` | Du får inte använda transform för customCode. Ange en funktion eller filomformning. |
| `ims-not-authorized` | Ett okänt fel uppstod när ditt konto autentiserades. Försök igen senare. |
| `ims-session-error` | Det har uppstått ett problem med den inloggade sessionen. Logga ut och logga in igen. |
| `internal-error` | Ett internt fel inträffade. Vänta några minuter och försök igen. Kontakta kundtjänst om problemet kvarstår. |
| `invalid-data_element` | Ett ogiltigt dataelement kan inte läggas till i ett bibliotek. |
| `invalid-embed_code` | Antingen är detta inte en giltig inbäddningskod eller så försöker du länka den till en utvecklings- eller staging-miljö. Inbäddningskoder för dynamiska Tag Management (DTM) kan bara länkas till produktionsmiljöer. |
| `invalid-extension` | Ett ogiltigt tillägg kan inte läggas till i ett bibliotek. |
| `invalid-extension_package_id` | Du kan bara ändra vissa av objektegenskaperna i ett tilläggspaket. Du försökte ändra en av de som inte är tillåtna. |
| `invalid-new-owner-org-id` | Org-ID:t som du försökte tilldela är inte ett giltigt Org-ID. |
| `invalid-org` | Din aktiva organisation har inte åtkomst till API:t. Kontrollera att du använder rätt organisation. |
| `invalid-rule` | Det går inte att lägga till en ogiltig regel i ett bibliotek. |
| `invalid-settings-syntax` | Ett syntaxfel påträffades när inställningarna för JSON parsades. |
| `library-file-not-found` | Det gick inte att hitta en nödvändig fil som definierats i extension.json inuti zip-paketet. |
| `minification-error` | Koden kunde inte kompileras på grund av ogiltig kod. |
| `multiple-revisions` | Endast en revision av varje resurs kan inkluderas i ett bibliotek. |
| `no-available-orgs` | Det här användarkontot tillhör inte en produktprofil som har åtkomst till taggar. Använd Admin Console för att lägga till den här användaren i en produktprofil med taggrättigheter. |
| `not-authorized` | Det här användarkontot har inte den behörighet som krävs för att utföra den här åtgärden. |
| `not-found` | Posten kunde inte hittas. Verifiera ID:t för objektet som du försöker hämta. |
| `not-unique` | Namnet som du försöker använda används redan. Egenskapen name måste vara unik för den här resursen. |
| `public-release-not-authorized` | Den offentliga releasen av förlängningar samordnas av `launch-ext-dev@adobe.com`. Visa dokumentet på [frigöra tillägg](../../extension-dev/submit/release.md) för mer information. |
| `read-only` | Den här resursen är skrivskyddad och kan inte ändras. |
| `session-timeout` | Användarsessionen har gått ut. Logga ut och logga in igen. |
| `sftp-authentication-failed` | Autentiseringen misslyckades för SFTP-anslutningen. |
| `sftp-connection-timeout` | Tidsgränsen för SFTP-anslutningen har uppnåtts. |
| `sftp-exception` | Ett undantag påträffades när SFTP användes för att ansluta till servern. |
| `sftp-status-exception` | Ett SFTP-undantag påträffades vid kommunikation med servern. |
| `socket-error` | Ett socketfel påträffades vid kommunikation med servern. |
| `ssh-disconnect` | SSH-sessionen kopplades från. |
| `timeout-error` | Tidsgränsen för anslutningen till servern överskreds. |
| `unknown-error` | Ett oväntat fel uppstod. Du kan försöka igen senare eller ringa kundtjänst och förklara vad du gjorde när det hände. |
| `unsupported-custom-code-language` | Ett anpassat kodspråk som inte stöds angavs. |
| `upgraded-extension-required` | När du har installerat en tilläggsuppgradering måste du inkludera den i alla bibliotek tills uppgraderingen når Production. Det enda undantaget är om tillägget inte har publicerats än. |
| `upstream-build-required` | Det krävs en lyckad version av det överordnade biblioteket innan du kan skapa det här. |

{style="table-layout:auto"}
