---
title: idMigrationEnabled
description: Låter Web SDK läsa AMCV-cookies.
exl-id: 33b9d645-0fbe-4fe4-8847-e6f9e78557b6
source-git-commit: bf0bb72777cacd822fd6e887ac3ef71764784214
workflow-type: tm+mt
source-wordcount: '833'
ht-degree: 0%

---

# `idMigrationEnabled`

Egenskapen `idMigrationEnabled` gör att Web SDK kan läsa AMCV-cookies som angetts av tidigare Adobe Experience Cloud-implementeringar. Om din organisation uppgraderar din implementering till Web SDK ger den här inställningen en smidigare övergång till den aktuella Adobe Experience Cloud ID-tjänsten. Den här inställningen är värdefull så att du inte ser någon större ökning av antalet unika besökare när du uppgraderar till SDK för webben.

Om din organisation kör en ny implementering av Web SDK påverkar detta inte datainsamling eller besöksidentifiering. Det finns inga nackdelar med att låta det vara aktiverat för alla implementeringar.

## Så här fungerar identitetsmigrering {#how-it-works}

Besökar-API:t lagrar Experience Cloud-ID (ECID) i en cookie med namnet `AMCV_<ORG_ID>`. När `idMigrationEnabled` är `true` (standardvärdet) läser Web SDK automatiskt ECID från AMCV-cookien och använder det som besökarens identitet på den första Edge Network-begäran.

1. En besökare kommer till en sida som nu använder Web SDK i stället för besökar-API:t.
1. Web SDK söker efter en befintlig `kndctr_`-identitetscookie (dess eget cookie-format). Om ingen hittas söker den efter en `AMCV_`-cookie.
1. Om en `AMCV_`-cookie hittas extraherar Web SDK ECID och använder det för att initiera besökarens identitet.
1. Web SDK anger en ny `kndctr_`-identitetscookie med samma ECID.
1. Vid efterföljande besök använder Web SDK cookien `kndctr_` direkt. Cookien `AMCV_` behövs inte längre.

För att migreringen ska fungera måste Web SDK konfigureras med samma [`orgId`](/help/collection/js/commands/configure/orgid.md) som Visitor-API:t använde och måste distribueras på samma domän (eller en underdomän till samma överordnade domän) där AMCV-cookien angavs.

## Migreringsscenarier som stöds

ID-migrering har stöd för följande övergångsmönster:

* **Vissa sidor använder fortfarande Visitor API medan andra sidor använder Web SDK**: SDK läser befintliga AMCV-cookies och skriver en ny cookie med det befintliga ECID:t. Dessutom skrivs AMCV-cookies så att sidor som fortfarande använder Visitor API känner igen samma besökare.
* **API:t för Web SDK och Visitor finns båda på samma sida**: Om AMCV-cookien inte är inställd söker SDK efter Visitor API på sidan och använder det för att hämta ECID.
* **Webbplatsen har flyttats helt till Web SDK**: Du kan låta migreringen vara aktiverad under en tidsperiod så att befintliga AMCV-baserade besökare behåller kontinuiteten medan deras cookies överförs.

>[!IMPORTANT]
>
>Läs inte in Visitor API och Web SDK på samma sida samtidigt om du inte har bekräftat att AMCV-cookien redan är inställd. Om du kör båda biblioteken på en enda sida kan det orsaka rasförhållanden där varje bibliotek försöker hantera identiteten oberoende av varandra, vilket kan generera dubbletter eller ECID som står i konflikt.

## Inaktiverar migrering {#turn-off-migration}

När hela webbplatsen har körts på SDK och inga besökare har bara en `AMCV_`-cookie utan en motsvarande `kndctr_`-cookie kan du inaktivera identitetsmigreringen genom att ange `idMigrationEnabled` som `false`. Detta är en mindre prestandaoptimering och minskar ytan för identitetslogiken.

Som vägledning bör du vänta tills AMCV-cookie har passerat sin längsta livstid efter att den sista sidan har migrerats. Om dina AMCV-cookies har en tvåårig förfallotid, vänta två år efter att den sista sidan klipptes över till Web SDK. I praktiken avaktiverar de flesta organisationer migreringen tidigare (efter några månader) och godtar en försumbar inflationsnivå från det fåtal besökare som för första gången kommer tillbaka efter en lång frånvaro.

## Uppdateringar för Audience Manager trait

När XDM-formaterade data skickas till Audience Manager under migreringen måste dessa data konverteras till signaler. Dina egenskaper måste uppdateras för att återspegla de nya nycklarna i XDM. Den här processen blir enklare om du använder [BAAAM-verktyget](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/bulk-management-tools/bulk-management-intro.html?lang=sv-SE#getting-started-with-bulk-management).

## Migrering av ID från tredje part {#third-party-id}

Om implementeringen av Visitor API använde ID:n från tredje part (cookien `demdex.net`) kan Web SDK även migrera dem. Konfigurera [`thirdPartyCookiesEnabled`](/help/collection/js/commands/configure/thirdpartycookiesenabled.md) till `true` i din Web SDK-konfiguration. Web SDK läser den befintliga Demdex-cookien och inkluderar tredjepartsidentiteten i sina Edge Network-förfrågningar, som följer samma migreringsmönster som AMCV-cookien.

## Validering {#validation}

Så här kontrollerar du att identitetsmigrering fungerar som den ska:

1. Öppna en sida som tidigare använt Visitor-API:t (nu med Web SDK) i en webbläsare som har en befintlig `AMCV_`-cookie.
2. I utvecklingsverktygen kontrollerar du att en `kndctr_`-identitetscookie har angetts och att ECID matchar den i `AMCV_` -cookien.
3. Efter distributionen kan du jämföra antalet unika besökare före och efter migreringen under samma tidsperiod. En betydande topp hos unika besökare kan tyda på att migreringen inte för fram identiteterna.

>[!TIP]
>
>Använd `getIdentity` för att programmässigt hämta ECID för jämförelse:
>
>```js
>alloy("getIdentity", { namespaces: ["ECID"] }).then(function(result) {
>   console.log("ECID:", result.identity.ECID);
>});
>```

## Konfigurera `idMigrationEnabled` {#configure}

Ange det booleska värdet `idMigrationEnabled` när du kör kommandot `configure`. Om du utelämnar den här egenskapen när du konfigurerar Web SDK blir standardvärdet `true`. Ange den här egenskapen om du vill inaktivera möjligheten att läsa AMCV-cookies som angetts av Visitor API. De flesta organisationer behöver inte ange den här egenskapen.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  idMigrationEnabled: false
});
```

## Aktivera migrering av besökar-ID med hjälp av taggtillägget Web SDK

Dessa inställningar kan konfigureras i taggtillägget för Web SDK med hjälp av [inställningarna för identitetskonfiguration](/help/tags/extensions/client/web-sdk/configure/identity.md).
