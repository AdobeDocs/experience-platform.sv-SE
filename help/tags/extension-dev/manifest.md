---
title: Extension Manifest
description: Lär dig hur du konfigurerar en JSON-manifestfil som informerar Adobe Experience Platform om hur du använder tillägget på rätt sätt.
exl-id: 7cac020b-3cfd-4a0a-a2d1-edee1be125d0
source-git-commit: 77313baabee10e21845fa79763c7ade4e479e080
workflow-type: tm+mt
source-wordcount: '2645'
ht-degree: 0%

---

# Extension manifest

>[!NOTE]
>
>Adobe Experience Platform Launch har omklassificerats som en serie datainsamlingstekniker i Adobe Experience Platform. Som ett resultat av detta har flera terminologiska förändringar införts i produktdokumentationen. Se följande [dokument](../term-updates.md) för en konsoliderad hänvisning till terminologiska förändringar.

I tilläggets baskatalog måste du skapa en fil med namnet `extension.json`. Detta innehåller viktig information om tillägget som gör att Adobe Experience Platform kan använda det korrekt. En del av innehållet formateras efter [npm `package.json`](https://docs.npmjs.com/files/package.json).

Ett exempel `extension.json` finns på [Hello World-tillägg](https://github.com/adobe/reactor-helloworld-extension/blob/master/extension.json) GitHub-databas.

Ett tilläggsmanifest måste bestå av följande:

| Egenskap | Beskrivning |
| --- | --- |
| `name` | Namnet på tillägget. Den måste vara unik från alla andra tillägg och måste uppfylla [namnregler](#naming-rules). **Detta används av taggar som identifierare och bör inte ändras efter att du har publicerat tillägget.** |
| `platform` | Plattformen för tillägget. Det enda värde som accepteras för tillfället är `web`. |
| `version` | Versionen av tillägget. Den måste följa efter [semester](https://semver.org/) versionshanteringsformat. Detta är i linje med [npm-versionsfält](https://docs.npmjs.com/files/package.json#version). |
| `displayName` | Tilläggets läsbara namn. Detta visas för plattformsanvändare. &quot;taggar&quot; eller &quot;filtillägg&quot; behöver inte anges. användarna kommer redan att veta att de tittar på ett taggtillägg. |
| `description` | Beskrivning av tillägget. Detta visas för plattformsanvändare. Om tillägget ger användarna möjlighet att implementera produkten på sin webbplats, beskriv vad produkten gör. &quot;taggar&quot; eller &quot;filtillägg&quot; behöver inte anges. användarna kommer redan att veta att de tittar på ett taggtillägg. |
| `iconPath` *(Valfritt)* | Den relativa sökvägen till ikonen som ska visas för tillägget. Det får inte börja med ett snedstreck. Den måste referera till en SVG-fil med en `.svg` tillägg. SVG ska vara fyrkantig och kan skalas av Platform. |
| `author` | &quot;Författaren&quot; är ett objekt som ska struktureras enligt följande: <ul><li>`name`: Namnet på tilläggsförfattaren. Du kan också använda företagsnamnet här.</li><li>`url` *(Valfritt)*: En URL där du kan ta reda på mer om tilläggsförfattaren.</li><li>`email` *(Valfritt)*: E-postadressen till tilläggsförfattaren.</li></ul>Detta är i linje med [npm-författarfält](https://docs.npmjs.com/files/package.json#people-fields-author-contributors) regler. |
| `exchangeUrl` *(Krävs för offentliga tillägg)* | URL:en till tilläggets lista på Adobe Exchange. Det måste matcha mönstret `https://www.adobeexchange.com/experiencecloud.details.######.html`. |
| `viewBasePath` | Den relativa sökvägen till underkatalogen som innehåller alla vyer och visningsrelaterade resurser (HTML, JavaScript, CSS, bilder). Plattformen har den här katalogen på en webbserver och läser in iframe-innehåll från den. Detta är ett obligatoriskt fält och ska inte börja med ett snedstreck. Om till exempel alla vyer finns i `src/view/`, värdet av `viewBasePath` skulle vara `src/view/`. |
| `hostedLibFiles` *(Valfritt)* | Många av våra användare föredrar att ha alla taggrelaterade filer på sin egen server. Detta ger användarna en ökad säkerhet vad gäller filtillgänglighet vid körning och de kan enkelt söka efter säkerhetsluckor i koden. Om biblioteksdelen av tillägget behöver läsa in JavaScript-filer under körning bör du använda den här egenskapen för att lista de filerna. De listade filerna lagras tillsammans med taggens körtidsbibliotek. Tillägget kan sedan läsa in filerna via en URL som hämtats med [getHostedLibFileUrl](./turbine.md#get-hosted-lib-file) -metod.<br><br>Det här alternativet innehåller en array med relativa sökvägar för biblioteksfiler från tredje part som måste lagras. |
| `main` *(Valfritt)* | Den relativa sökvägen för en biblioteksmodul som ska köras vid körning.<br><br>Den här modulen inkluderas alltid i körningsbiblioteket och körs. Eftersom modulen alltid ingår i körningsbiblioteket rekommenderar vi att du bara använder huvudmodulen när det är absolut nödvändigt och att kodstorleken är minimal.<br><br>Denna modul är inte garanterad att utföras först. andra moduler kan köras innan. |
| `configuration` *(Valfritt)* | Detta beskriver [tilläggskonfiguration](./configuration.md) del av tillägget. Detta är nödvändigt om du vill att användarna ska ange globala inställningar för tillägget. Se [appendix](#config-object) om du vill ha mer information om hur det här fältet ska struktureras. |
| `events` *(Valfritt)* | En array med [event](./web/event-types.md) typdefinitioner. Se avsnittet om bilagan [typdefinition](#type-definitions) för strukturen för varje objekt i arrayen. |
| `conditions` *(Valfritt)* | En array med [villkor](./web/condition-types.md) typdefinitioner. Se avsnittet om bilagan [typdefinition](#type-definitions) för strukturen för varje objekt i arrayen. |
| `actions` *(Valfritt)* | En array med [åtgärd](./web/action-types.md) typdefinitioner. Se avsnittet om bilagan [typdefinition](#type-definitions) för strukturen för varje objekt i arrayen. |
| `dataElements` *(Valfritt)* | En array med [dataelement](./web/data-element-types.md) typdefinitioner. Se avsnittet om bilagan [typdefinition](#type-definitions) för strukturen för varje objekt i arrayen. |
| `sharedModules` *(Valfritt)* | En array med definierade objekt för delade moduler. Varje objekt i en delad modul i arrayen ska struktureras på följande sätt: <ul><li>`name`: Namnet på den delade modulen. Observera att det här namnet kommer att användas när delade moduler från andra tillägg refereras enligt beskrivningen i [Delade moduler](./web/shared.md). Det här namnet visas aldrig i något användargränssnitt. Den ska vara unik från namnen på andra delade moduler i tillägget och måste uppfylla [namnregler](#naming-rules). **Detta används av taggar som identifierare och bör inte ändras efter att du har publicerat tillägget.**</li><li>`libPath`: Den relativa sökvägen till den delade modulen. Det får inte börja med ett snedstreck. Den måste referera till en JavaScript-fil med en `.js` tillägg.</li></ul> |

## Bilaga

### Namngivningsregler {#naming-rules}

Värdet för `name` fält inom `extension.json` måste uppfylla följande regler:

* Måste vara mindre än eller lika med 214 tecken
* Får inte börja med en punkt eller ett understreck
* Får inte innehålla versaler
* Får endast innehålla URL-säkra tecken

Dessa stämmer överens med [namn på npm-paket](https://docs.npmjs.com/files/package.json#name) regler.

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
      <td>Den relativa URL:en till tilläggskonfigurationsvyn. Den ska vara relativ till <code>viewBasePath</code> och ska inte börja med ett snedstreck. Den måste referera till en HTML-fil med en <code>.html</code> tillägg. Frågesträngar och fragment-ID (hash-suffix) kan användas.</td>
    </tr>
    <tr>
      <td><code>schema</code></td>
      <td>Ett objekt av <a href="https://json-schema.org/">JSON-schema</a> som beskriver formatet för ett giltigt objekt som sparas från tilläggskonfigurationsvyn. Eftersom du är utvecklare av konfigurationsvyn är det ditt ansvar att se till att alla sparade inställningsobjekt matchar det här schemat. Det här schemat används även för validering när användare försöker spara data med hjälp av plattformstjänster.<br><br>Ett exempel på schemaobjekt är följande:
<pre class="JSON language-JSON hljs">
{ "$schema": "http://json-schema.org/draft-04/schema#", "type": "object", "properties": { "delay": { "type": "number", "minimum": 1 }, "required": [ "delay" ], "additionalProperties": false }
</pre>
      Vi rekommenderar att du använder ett verktyg som <a href="https://www.jsonschemavalidator.net/">JSON-schemavaliderare</a> för att manuellt testa ditt schema.</td>
    </tr>
    <tr>
      <td><code>transforms</code> <em>(Valfritt)</em></td>
      <td>En array med objekt där varje objekt representerar en omformning som ska utföras på alla motsvarande inställningsobjekt när det skickas till körningsbiblioteket. Se <a href="#transforms">omformningar</a> för mer information om varför detta kan behövas och hur det används.</td>
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
      <td>Namnet på typen. Det här måste vara ett unikt namn i tillägget. Namnet måste överensstämma med <a href="#naming-rules">namnregler</a>. <strong>Detta används av taggar som identifierare och bör inte ändras efter att du har publicerat tillägget.</strong></td>
    </tr>
    <tr>
      <td><code>displayName</code></td>
      <td>Den text som ska användas för att representera typen i användargränssnittet för datainsamling. Den ska vara läsbar för människor.</td>
    </tr>
    <tr>
      <td><code>categoryName</code> <em>(Valfritt)</em></td>
      <td>När det finns <code>displayName</code> listas under <code>categoryName</code> i användargränssnittet. Alla typer med samma <code>categoryName</code> kommer att listas under samma kategori. Om tillägget till exempel innehöll en <code>keyUp</code> händelsetyp och <code>keyDown</code> händelsetyp och båda hade <code>categoryName</code> av <code>Keyboard</code>, skulle båda händelsetyperna listas under kategorin Tangentbord när användaren väljer i listan över tillgängliga händelsetyper när en regel skapas. Värdet för <code>categoryName</code> ska vara läsbart för människor.</td>
    </tr>
    <tr>
      <td><code>libPath</code></td>
      <td>Den relativa sökvägen till textens biblioteksmodul. Det får inte börja med ett snedstreck. Den måste referera till en JavaScript-fil med en <code>.js</code> tillägg.</td>
    </tr>
    <tr>
      <td><code>viewPath</code> <em>(Valfritt)</em></td>
      <td>Den relativa URL:en till typvyn. Den ska vara relativ till <code>viewBasePath</code> och ska inte börja med ett snedstreck. Den måste referera till en HTML-fil med en <code>.html</code> tillägg. Frågesträngar och fragment-ID:n (hash) tillåts. Om typens biblioteksmodul inte använder några inställningar från en användare, kan du exkludera den här egenskapen. I stället visas en platshållare som anger att ingen konfiguration behövs.</td>
    </tr>
    <tr>
      <td><code>schema</code></td>
      <td>Ett objekt av <a href="https://json-schema.org/">JSON-schema</a> som beskriver formatet för ett giltigt inställningsobjekt som kan sparas av användaren. Inställningarna konfigureras och sparas vanligtvis av en användare med användargränssnittet för datainsamling. I dessa fall kan tilläggsvyn vidta nödvändiga åtgärder för att validera inställningar som användaren anger. Å andra sidan väljer vissa användare att använda tagg-API:er direkt utan hjälp av något användargränssnitt. Syftet med det här schemat är att göra det möjligt för Platform att på rätt sätt validera att inställningsobjekt som sparats av användare, oavsett om ett användargränssnitt används, har ett format som är kompatibelt med biblioteksmodulen som ska agera på inställningsobjektet vid körning.<br><br>Ett exempel på schemaobjekt är följande:<br>
<pre class="JSON language-JSON hljs">
{ "$schema": "http://json-schema.org/draft-04/schema#", "type": "object", "properties": { "delay": { "type": "number", "minimum": 1 }, "required": [ "delay" ], "additionalProperties": false }
</pre>
      Vi rekommenderar att du använder ett verktyg som <a href="https://www.jsonschemavalidator.net/">JSON-schemavaliderare</a> för att manuellt testa ditt schema.</td>
    </tr>
    <tr>
      <td><code>transforms</code> <em>(Valfritt)</em></td>
      <td>En array med objekt där varje objekt representerar en omformning som ska utföras på alla motsvarande inställningsobjekt när det skickas till körningsbiblioteket. Se avsnittet om <a href="#transforms">omformningar</a> för mer information om varför detta kan behövas och hur det används.</td>
    </tr>
  </tbody>
</table>

### Omformningar {#transforms}

För vissa specifika användningsområden behöver tillägg inställningsobjekten som har sparats från en vy omvandlas av plattformen innan de skickas till taggens körtidsbibliotek. Du kan begära att en eller flera av dessa omformningar görs genom att ställa in `transforms` egenskap när en typdefinition definieras i `extension.json`. The `transforms` är en array med objekt där varje objekt representerar en omformning som ska utföras.

Alla omformningar kräver en `type` och `propertyPath`. The `type` måste vara en av `function`, `remove`och `file` och beskriver vilken transformationsplattform som ska användas för inställningsobjektet. The `propertyPath` är en periodavgränsad sträng som anger var taggen ska hitta den egenskap som behöver ändras i inställningsobjektet. Här är ett exempel på inställningsobjekt och några `propertyPath`s:

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

* Om du anger en `propertyPath` av `foo.bar` du skulle omvandla `"A string"` värde.
* Om du anger en `propertyPath` av `foo.baz[]` du omformar varje värde i `baz` array.
* Om du anger en `propertyPath` av `foo.baz` du skulle omvandla `baz` array.

Egenskapssökvägar kan använda valfri kombination av array- och objektnotation för att tillämpa omformningar på alla nivåer i inställningsobjektet.

>[!WARNING]
>
>Använda arraynotation i `propertyPath` attribut (t.ex. `foo.baz[]`) stöds ännu inte i tilläggets sandlåda*verktyg.

Avsnitten nedan beskriver de tillgängliga omformningarna och hur de används.

#### Funktionsomformning

Funktionstransformeringen gör att kod som skrivits av plattformsanvändare kan köras av en biblioteksmodul i det utsända taggbiblioteket.

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

När inställningsobjektet sparas från åtgärdstypens vy är användarens kod bara en sträng. Detta är bra eftersom det kan serialiseras till och från JSON. Men det är också dåligt eftersom det vanligtvis skulle skickas som en sträng i taggens körningsbibliotek i stället för som en körbar funktion. Även om du kan försöka köra koden i åtgärdstypens biblioteksmodul med [`eval`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/eval) eller en [Funktionskonstruktor](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function), vilket är mycket modfällt på grund av [skyddsprofiler för innehåll](https://developer.mozilla.org/en-US/docs/Web/Security/CSP) kan blockera exekvering.

Som en tillfällig lösning på den här situationen kan du använda funktionsomformningen för att få Platform att kapsla in användarens kod i en körbar funktion när den släpps ut i taggens körningsbibliotek. För att lösa vårt exempelproblem definierar vi omformningen i typdefinitionen i `extension.json` enligt följande:

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

* `type` definierar vilken typ av omformning som ska användas på inställningsobjektet.
* `propertyPath` är en periodavgränsad sträng som anger för plattformen var den egenskap som behöver ändras i inställningsobjektet ska hittas.
* `parameters` är en array med parameternamn som ska inkluderas i radbrytningsfunktionens signatur.

När inställningsobjektet skickas i taggens körningsbibliotek omformas det till följande:

```javascript
{
  foo: {
    bar: function(username) {
      console.log('Welcome, ' + username +'. This is ZomboCom.');
    }
  }
}
```

Din biblioteksmodul kan sedan anropa funktionen som innehåller användarens kod och skicka in `username` argument.

#### Filomvandling

Med filtransformeringen kan kod som skrivits av plattformsanvändare skickas till en fil som är separat från taggens körningsbibliotek. Filen lagras tillsammans med taggens körtidsbibliotek och kan sedan läsas in efter behov av tillägget vid körning.

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

Vi vill att användarens kod ska placeras i en separat fil i stället för att inkluderas i taggens körningsbibliotek. När en regel som använder vår åtgärd utlöses i taggens körtidsbibliotek, vill vi läsa in användarens kod genom att lägga till ett skriptelement i dokumentets brödtext. För att lösa vårt exempelproblem definierar vi omformningen för åtgärdstypdefinitionen i `extension.json` enligt följande:

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

* `type` definierar vilken typ av omformning som ska användas på inställningsobjektet.
* `propertyPath` är en periodavgränsad sträng som anger för plattformen var den egenskap som behöver ändras i inställningsobjektet ska hittas.

När inställningsobjektet skickas i taggens körningsbibliotek omformas det till följande:

```javascript
{
  foo: {
    bar: "//launch.cdn.com/path/abc.js"
  }
}
```

I det här fallet är värdet för `foo.bar` har omvandlats till en URL. Den exakta URL:en bestäms när biblioteket skapas. Filen ges alltid en `.js` och levereras med en JavaScript-orienterad MIME-typ. Vi kan lägga till stöd för andra MIME-typer i framtiden.

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

Vi vill inte inkludera egendomen `bar` inuti taggens körningsbibliotek. För att lösa vårt exempelproblem definierar vi omformningen för åtgärdstypdefinitionen i `extension.json` enligt följande:

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

* `type` definierar vilken typ av omformning som ska användas på inställningsobjektet.
* `propertyPath` är en periodavgränsad sträng som anger för plattformen var den egenskap som behöver ändras i inställningsobjektet ska hittas.

När inställningsobjektet skickas i taggens körningsbibliotek omformas det till följande:

```js
{
  foo: {
  }
}
```

I det här fallet är värdet för `foo.bar` har tagits bort från inställningsobjektet.
