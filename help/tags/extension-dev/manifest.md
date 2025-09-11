---
title: Extension Manifest
description: Lär dig hur du konfigurerar en JSON-manifestfil som informerar Adobe Experience Platform om hur du använder tillägget på rätt sätt.
exl-id: 7cac020b-3cfd-4a0a-a2d1-edee1be125d0
source-git-commit: a7c66b9172421510510b6acf3466334c33cdaa3d
workflow-type: tm+mt
source-wordcount: '2652'
ht-degree: 1%

---

# Extension manifest

>[!NOTE]
>
>Adobe Experience Platform Launch har omprofilerats till en serie tekniker för datainsamling i Adobe Experience Platform. Som ett resultat av detta har flera terminologiska förändringar genomförts i produktdokumentationen. Se följande [dokument](../term-updates.md) för en konsoliderad referens av terminologiändringarna.

I tilläggets baskatalog måste du skapa filen `extension.json`. Detta innehåller viktig information om tillägget som gör att Adobe Experience Platform kan använda det korrekt. En del av innehållet formateras efter sättet för [npm:s `package.json`](https://docs.npmjs.com/files/package.json).

Ett exempel `extension.json` finns i GitHub-databasen [Hello World-tillägget](https://github.com/adobe/reactor-helloworld-extension/blob/master/extension.json).

Ett tilläggsmanifest måste bestå av följande:

| Egenskap | Beskrivning |
|--------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `name` | Namnet på tillägget. Den måste vara unik från alla andra tillägg och måste uppfylla [namnreglerna](#naming-rules). **Detta används av taggar som identifierare och bör inte ändras efter att du har publicerat tillägget.** |
| `platform` | Plattformen för tillägget. Det enda värde som accepteras för tillfället är `web`. |
| `version` | Versionen av tillägget. Den måste följa versionshanteringsformatet [server](https://semver.org/). Detta stämmer överens med [npm-versionsfältet](https://docs.npmjs.com/files/package.json#version). |
| `displayName` | Tilläggets läsbara namn. Detta visas för Experience Platform-användare. Du behöver inte ange&quot;taggar&quot; eller&quot;tillägg&quot;. Användarna vet redan att de tittar på ett taggtillägg. |
| `description` | Beskrivningen av tillägget. Detta visas för Experience Platform-användare. Om tillägget ger användarna möjlighet att implementera produkten på sin webbplats, beskriv vad produkten gör. Du behöver inte ange&quot;taggar&quot; eller&quot;tillägg&quot;. Användarna vet redan att de tittar på ett taggtillägg. |
| `iconPath` *(Valfritt)* | Den relativa sökvägen till ikonen som ska visas för tillägget. Det får inte börja med ett snedstreck. Den måste referera till en SVG-fil med tillägget `.svg`. SVG ska vara fyrkantig och kan skalas av Experience Platform. |
| `author` | &quot;Författaren&quot; är ett objekt som ska struktureras enligt följande: <ul><li>`name`: Namnet på tilläggsförfattaren. Du kan också använda företagsnamnet här.</li><li>`url` *(Valfritt)*: En URL där du kan ta reda på mer om tilläggsförfattaren.</li><li>`email` *(Valfritt)*: E-postadressen till tilläggsförfattaren.</li></ul>Detta är förenligt med [npm-reglerna för författarfält](https://docs.npmjs.com/files/package.json#people-fields-author-contributors). |
| `releaseNotesUrl` *(Valfritt)* | URL:en till tilläggets versionsinformation, om du har en plats att publicera informationen på. Den här URL:en används i användargränssnittet för Adobe-taggar för att visa länken under installation och uppgradering av tillägg. Den här egenskapen stöds bara för webbtillägg och Edge-tillägg. |
| `exchangeUrl` *(Krävs för offentliga tillägg)* | URL:en till tilläggets lista på Adobe Exchange. Det måste matcha mönstret `https://www.adobeexchange.com/experiencecloud.details.######.html`. |
| `viewBasePath` | Den relativa sökvägen till underkatalogen som innehåller alla vyer och visningsrelaterade resurser (HTML, JavaScript, CSS, images). Experience Platform har den här katalogen på en webbserver och läser in iframe-innehåll från den. Detta är ett obligatoriskt fält och ska inte börja med ett snedstreck. Om alla dina vyer till exempel finns i `src/view/` blir värdet `viewBasePath` `src/view/`. |
| `hostedLibFiles` *(Valfritt)* | Många av våra användare föredrar att ha alla taggrelaterade filer på sin egen server. Detta ger användarna en ökad säkerhet vad gäller filtillgänglighet vid körning och de kan enkelt söka efter säkerhetsluckor i koden. Om biblioteksdelen av tillägget behöver läsa in JavaScript-filer vid körning bör du använda den här egenskapen för att lista dessa filer. De listade filerna lagras tillsammans med taggens körtidsbibliotek. Tillägget kan sedan läsa in filerna via en URL som hämtats med metoden [getHostedLibFileUrl](./turbine.md#get-hosted-lib-file) .<br><br>Det här alternativet innehåller en matris med relativa sökvägar för biblioteksfiler från tredje part som måste lagras. |
| `main` *(Valfritt)* | Den relativa sökvägen för en biblioteksmodul som ska köras vid körning.<br><br>Den här modulen inkluderas alltid i körningsbiblioteket och körs. Eftersom modulen alltid ingår i körningsbiblioteket rekommenderar vi att du bara använder huvudmodulen när det är absolut nödvändigt och att kodstorleken är minimal.<br><br>Det går inte att garantera att den här modulen körs först. Andra moduler kan köras innan. |
| `configuration` *(Valfritt)* | Detta beskriver delen [tilläggskonfiguration](./configuration.md) i tillägget. Detta är nödvändigt om du vill att användarna ska ange globala inställningar för tillägget. Mer information om hur det här fältet ska struktureras finns i [bilagan](#config-object). |
| `events` *(Valfritt)* | En array med [event](./web/event-types.md)-typdefinitioner. I avsnittet om tillägg för [typdefinitioner](#type-definitions) finns strukturen för varje objekt i arrayen. |
| `conditions` *(Valfritt)* | En array med [condition](./web/condition-types.md)-typdefinitioner. I avsnittet om tillägg för [typdefinitioner](#type-definitions) finns strukturen för varje objekt i arrayen. |
| `actions` *(Valfritt)* | En matris med [åtgärd](./web/action-types.md)-typdefinitioner. I avsnittet om tillägg för [typdefinitioner](#type-definitions) finns strukturen för varje objekt i arrayen. |
| `dataElements` *(Valfritt)* | En array med [dataelement](./web/data-element-types.md)-typdefinitioner. I avsnittet om tillägg för [typdefinitioner](#type-definitions) finns strukturen för varje objekt i arrayen. |
| `sharedModules` *(Valfritt)* | En array med definierade objekt för delade moduler. Varje objekt i en delad modul i arrayen ska struktureras på följande sätt: <ul><li>`name`: Namnet på den delade modulen. Observera att det här namnet kommer att användas när delade moduler från andra tillägg refereras enligt beskrivningen i [Delade moduler](./web/shared.md). Det här namnet visas aldrig i något användargränssnitt. Den ska vara unik från namnen på andra delade moduler i tillägget och måste uppfylla [namnreglerna](#naming-rules). **Detta används av taggar som identifierare och bör inte ändras efter att du har publicerat tillägget.**</li><li>`libPath`: Den relativa sökvägen till den delade modulen. Det får inte börja med ett snedstreck. Den måste referera till en JavaScript-fil med tillägget `.js`.</li></ul> |

## Bilaga

### Namngivningsregler {#naming-rules}

Värdet för alla `name`-fält i `extension.json` måste följa följande regler:

* Måste innehålla högst 214 tecken
* Får inte börja med en punkt eller ett understreck
* Får inte innehålla versaler
* Får endast innehålla URL-säkra tecken

Dessa är kompatibla med reglerna för [npm-paketnamnet](https://docs.npmjs.com/files/package.json#name).

### Egenskaper för konfigurationsobjekt {#config-object}

Konfigurationsobjektet ska struktureras på följande sätt:

<table>
  <thead>
    <tr>
      <th>Egenskap</th>
      <th>Beskrivning</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><code>viewPath</code></td>
      <td>Den relativa URL:en till tilläggskonfigurationsvyn. Den ska vara relativ till <code>viewBasePath</code> och ska inte börja med ett snedstreck. Den måste referera till en HTML-fil med tillägget <code>.html</code>. Frågesträngar och fragment-ID (hash-suffix) kan användas.</td>
    </tr>
    <tr>
      <td><code>schema</code></td>
      <td>Ett objekt av <a href="https://json-schema.org/">JSON-schema</a> som beskriver formatet för ett giltigt objekt som sparas från tilläggskonfigurationsvyn. Eftersom du är utvecklare av konfigurationsvyn är det ditt ansvar att se till att alla sparade inställningsobjekt matchar det här schemat. Det här schemat används även för validering när användare försöker spara data med Experience Platform tjänster.<br><br>Ett exempelschemaobjekt är följande:
<pre class="JSON language-JSON hljs">
{
  "$schema": "http://json-schema.org/draft-04/schema#",
  "type": "object",
  "properties": {
    "delay": {
      "type": "number",
      "minimum": 1
    }
  },
  "required": [
    "delay"
  ],
  "additionalProperties": false
}
</pre>
      Vi rekommenderar att du använder ett verktyg som <a href="https://www.jsonschemavalidator.net/">JSON-schemavalideraren</a> för att manuellt testa ditt schema.</td>
    </tr>
    <tr>
      <td><code>transforms</code> <em>(Valfritt)</em></td>
      <td>En array med objekt där varje objekt representerar en omformning som ska utföras på alla motsvarande inställningsobjekt när det skickas till körningsbiblioteket. I avsnittet <a href="#transforms">transforms</a> finns mer information om varför detta kan behövas och hur det används.</td>
    </tr>
  </tbody>
</table>

### Typdefinitioner {#type-definitions}

En typdefinition är ett objekt som används för att beskriva en händelse, ett villkor, en åtgärd eller en dataelementtyp. Objektet består av följande:

<table>
  <thead>
    <tr>
      <th>Egenskap</th>
      <th>Beskrivning</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><code>name</code></td>
      <td>Namnet på typen. Det här måste vara ett unikt namn i tillägget. Namnet måste uppfylla <a href="#naming-rules">namnreglerna</a>. <strong>Detta används av taggar som identifierare och bör inte ändras efter att du har publicerat tillägget.</strong></td>
    </tr>
    <tr>
      <td><code>displayName</code></td>
      <td>Den text som ska användas för att representera typen i användargränssnittet för datainsamling. Den ska vara läsbar för människor.</td>
    </tr>
    <tr>
      <td><code>categoryName</code> <em>(Valfritt)</em></td>
      <td>Om det anges kommer <code>displayName</code> att listas under <code>categoryName</code> i användargränssnittet. Alla typer med samma <code>categoryName</code> listas under samma kategori. Om tillägget till exempel innehöll en <code>keyUp</code>-händelsetyp och en <code>keyDown</code>-händelsetyp, och båda hade <code>categoryName</code> av <code>Keyboard</code>, skulle båda händelsetyperna listas under kategorin Tangentbord medan användaren väljer i listan över tillgängliga händelsetyper när en regel skapas. Värdet för <code>categoryName</code> ska vara läsbart för människor.</td>
    </tr>
    <tr>
      <td><code>libPath</code></td>
      <td>Den relativa sökvägen till textens biblioteksmodul. Det får inte börja med ett snedstreck. Den måste referera till en JavaScript-fil med tillägget <code>.js</code>.</td>
    </tr>
    <tr>
      <td><code>viewPath</code> <em>(Valfritt)</em></td>
      <td>Den relativa URL:en till typvyn. Den ska vara relativ till <code>viewBasePath</code> och ska inte börja med ett snedstreck. Den måste referera till en HTML-fil med tillägget <code>.html</code>. Frågesträngar och fragment-ID:n (hash) tillåts. Om typens biblioteksmodul inte använder några inställningar från en användare, kan du utelämna den här egenskapen. I stället visas en platshållare som anger att ingen konfiguration behövs.</td>
    </tr>
    <tr>
      <td><code>schema</code></td>
      <td>Ett objekt av <a href="https://json-schema.org/">JSON Schema</a> som beskriver formatet för ett giltigt inställningsobjekt som kan sparas av användaren. Inställningarna konfigureras och sparas vanligtvis av en användare med användargränssnittet i Datainsamling. I dessa fall kan tilläggsvyn vidta nödvändiga åtgärder för att validera de inställningar som användaren anger. Å andra sidan väljer vissa användare att använda tagg-API:er direkt utan hjälp av något användargränssnitt. Syftet med det här schemat är att göra det möjligt för Experience Platform att validera att inställningsobjekt som sparats av användare, oavsett om användargränssnittet används, är i ett format som är kompatibelt med biblioteksmodulen som ska agera på inställningsobjektet vid körning.<br><br>Ett exempelschemaobjekt är följande:<br>
<pre class="JSON language-JSON hljs">
{
  "$schema": "http://json-schema.org/draft-04/schema#",
  "type": "object",
  "properties": {
    "delay": {
      "type": "number",
      "minimum": 1
    }
  },
  "required": [
    "delay"
  ],
  "additionalProperties": false
}
</pre>
      Vi rekommenderar att du använder ett verktyg som <a href="https://www.jsonschemavalidator.net/">JSON-schemavalideraren</a> för att manuellt testa ditt schema.</td>
    </tr>
    <tr>
      <td><code>transforms</code> <em>(Valfritt)</em></td>
      <td>En array med objekt där varje objekt representerar en omformning som ska utföras på alla motsvarande inställningsobjekt när det skickas till körningsbiblioteket. Mer information om varför det här kan behövas och hur det används finns i avsnittet <a href="#transforms">transforms</a>.</td>
    </tr>
  </tbody>
</table>

### Omformningar {#transforms}

För vissa specifika användningsområden behöver tillägg inställningsobjekten som har sparats från en vy omvandlas av Experience Platform innan de skickas till taggens körtidsbibliotek. Du kan begära att en eller flera av dessa omformningar äger rum genom att ange egenskapen `transforms` när du definierar en typdefinition i `extension.json`. Egenskapen `transforms` är en array med objekt där varje objekt representerar en omformning som ska utföras.

Alla omformningar kräver en `type` och en `propertyPath`. `type` måste vara en av `function`, `remove` och `file` och beskriver vilken omformning av Experience Platform som ska gälla för inställningsobjektet. `propertyPath` är en periodavgränsad sträng som anger var taggar ska hitta den egenskap som behöver ändras i inställningsobjektet. Här är ett exempel på inställningsobjekt och några `propertyPath`s:

```js
{
  foo: {
    bar: "A string",
    baz: [
      "A",
      "B",
      "C"
    ]
  }
}
```

* Om du anger `propertyPath` av `foo.bar` omformas värdet `"A string"`.
* Om du anger `propertyPath` av `foo.baz[]` omformas varje värde i arrayen `baz`.
* Om du anger `propertyPath` av `foo.baz` omformas arrayen `baz`.

Egenskapssökvägar kan använda valfri kombination av array- och objektnotation för att tillämpa omformningar på alla nivåer i inställningsobjektet.

>[!WARNING]
>
>Det finns ännu inget stöd för att använda matrisnotation i attributet `propertyPath` (t.ex. `foo.baz[]`) i verktyget för tilläggssandlåda*.

Avsnitten nedan beskriver de tillgängliga omformningarna och hur de används.

#### Funktionsomformning

Funktionsomformningen gör att kod som skrivits av Experience Platform-användare kan köras av en biblioteksmodul i det utsända taggbiblioteket.

Låt oss anta att vi vill tillhandahålla en&quot;anpassad manusåtgärd&quot;. Åtgärdsvyn för anpassade skript kan innehålla ett textområde där användaren kan ange kod. Låt oss anta att en användare har angett följande kod i textområdet:

`console.log('Welcome, ' + username +'. This is ZomboCom.');`

När användaren sparar regeln kan inställningsobjektet som sparas av vyn se ut så här:

```javascript
{
  foo: {
    bar: "console.log('Welcome, ' + username +'. This is ZomboCom.');"
  }
}
```

När en regel som använder vår åtgärd utlöses i taggens körtidsbibliotek, vill vi köra användarens kod och skicka den till ett användarnamn.

När inställningsobjektet sparas från åtgärdstypens vy är användarens kod bara en sträng. Detta är bra eftersom det kan serialiseras till och från JSON, men det är också dåligt eftersom det vanligtvis skulle ha släppts som en sträng i taggens körningsbibliotek i stället för som en körbar funktion. Även om du kan försöka köra koden i åtgärdstypens biblioteksmodul med [`eval`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/eval) eller en [funktionskonstruktor](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function) , rekommenderas det inte eftersom [skyddsprofiler](https://developer.mozilla.org/en-US/docs/Web/Security/CSP) eventuellt blockerar körningen.

Som en tillfällig lösning på den här situationen kan du använda funktionsomformningen för att Experience Platform ska kapsla in användarens kod i en körbar funktion när den släpps ut i taggkörningsbiblioteket. För att lösa vårt exempelproblem definierar vi transformeringen för typdefinitionen i `extension.json` enligt följande:

```json
{
  "transforms": [
    {
      "type": "function",
      "propertyPath": "foo.bar",
      "parameters": ["username"]
    }
  ]
}
```

* `type` definierar den typ av omformning som ska användas på inställningsobjektet.
* `propertyPath` är en periodavgränsad sträng som anger för Experience Platform var den egenskap som behöver ändras i inställningsobjektet ska hittas.
* `parameters` är en array med parameternamn som ska inkluderas i radbrytningsfunktionens signatur.

När inställningsobjektet skickas i taggens körningsbibliotek omvandlas det till följande:

```javascript
{
  foo: {
    bar: function(username) {
      console.log('Welcome, ' + username +'. This is ZomboCom.');
    }
  }
}
```

Din biblioteksmodul kan sedan anropa funktionen som innehåller användarens kod och skicka argumentet `username`.

#### Filomvandling

Med filtransformeringen kan kod som skrivits av Experience Platform-användare skickas till en fil som är separat från taggens körningsbibliotek. Filen lagras tillsammans med taggens körtidsbibliotek och kan sedan läsas in efter behov av tillägget vid körning.

Låt oss anta att vi vill tillhandahålla en&quot;anpassad manusåtgärd&quot;. Åtgärdstypens vy kan innehålla ett textområde där användaren kan ange kod. Låt oss anta att en användare har angett följande kod i textområdet:

`console.log('This is ZomboCom.');`

När användaren sparar regeln kan inställningsobjektet som sparas av vyn se ut så här:

```js
{
  foo: {
    bar: "console.log('This is ZomboCom.');"
  }
}
```

Vi vill att användarens kod ska placeras i en separat fil i stället för att inkluderas i taggens körningsbibliotek. När en regel som använder vår åtgärd utlöses i taggens körtidsbibliotek, vill vi läsa in användarens kod genom att lägga till ett skriptelement i dokumentets brödtext. För att lösa vårt exempelproblem definierar vi transformeringen för åtgärdstypdefinitionen i `extension.json` enligt följande:

```json
{
  "transforms": [
    {
      "type": "file",
      "propertyPath": "foo.bar"
    }
  ]
}
```

* `type` definierar den typ av omformning som ska användas på inställningsobjektet.
* `propertyPath` är en periodavgränsad sträng som anger för Experience Platform var den egenskap som behöver ändras i inställningsobjektet ska hittas.

När inställningsobjektet skickas i taggens körningsbibliotek omvandlas det till följande:

```javascript
{
  foo: {
    bar: "//launch.cdn.com/path/abc.js"
  }
}
```

I det här fallet har värdet `foo.bar` omvandlats till en URL. Den exakta URL:en bestäms när biblioteket skapas. Filen får alltid tillägget `.js` och levereras med en JavaScript-orienterad MIME-typ. Vi kan lägga till stöd för andra MIME-typer i framtiden.

#### Ta bort omformning

Som standard skickas alla egenskaper för inställningsobjektet i taggens körtidsbibliotek. Om vissa egenskaper bara används för tilläggsvyn, särskilt om de innehåller känslig information (t.ex. hemlig token) bör du använda omformningen remove för att förhindra att informationen skickas till taggens körningsbibliotek.

Låt oss anta att vi vill tillhandahålla en ny åtgärdstyp. Åtgärdstypens vy kan innehålla en inmatning där användaren kan ange en hemlig nyckel som tillåter anslutning till ett visst API. Låt oss anta att en användare har angett följande text i indata:

`ABCDEFG`

När användaren sparar regeln kan inställningsobjektet som sparas av vyn se ut så här:

```js
{
  foo: {
    bar: "ABCDEFG"
  }
}
```

Vi vill inte inkludera egenskapen `bar` i taggens körningsbibliotek. För att lösa vårt exempelproblem definierar vi transformeringen för åtgärdstypdefinitionen i `extension.json` enligt följande:

```json
{
  "transforms": [
    {
      "type": "remove",
      "propertyPath": "foo.bar"
    }
  ]
}
```

* `type` definierar den typ av omformning som ska användas på inställningsobjektet.
* `propertyPath` är en periodavgränsad sträng som anger för Experience Platform var den egenskap som behöver ändras i inställningsobjektet ska hittas.

När inställningsobjektet skickas i taggens körningsbibliotek omvandlas det till följande:

```js
{
  foo: {
  }
}
```

I det här fallet har värdet `foo.bar` tagits bort från inställningsobjektet.
