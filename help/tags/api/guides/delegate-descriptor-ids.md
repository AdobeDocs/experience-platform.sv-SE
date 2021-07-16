---
title: Delegera beskrivnings-ID
description: Lär dig mer om delegatbeskrivnings-ID:n i Reaktors-API:t och hur de länkar resurser med tillägg.
source-git-commit: 6a1728bd995137a7cd6dc79313762ae6e665d416
workflow-type: tm+mt
source-wordcount: '501'
ht-degree: 0%

---

# Delegera beskrivnings-ID

När du använder taggar i Adobe Experience Platform tillhandahålls alla funktioner som du kan distribuera på din webbplats av tillägg. De funktioner som finns i varje tillägg definieras av tilläggsutvecklaren. När ett tillägg distribueras paketeras det med sina olika funktioner i form av ett [tilläggspaket](../endpoints/extension-packages.md). De funktioner som utvecklare lägger till i ett tilläggspaket betraktas som&quot;delegater&quot; i det paketet.

Varje delegat i ett tilläggspaket får ett unikt delegatbeskrivnings-ID. Delegatbeskrivnings-ID:t för en viss resurs talar om för systemet vilken typ av resurs det är och vilket tilläggspaket det tillhör.

## Syntax

Ett delegatbeskrivnings-ID består av tre strängar som förenas med tecken med dubbla kolon (`::`), som representerar tilläggets paketnamn, delegattypen och delegatnamnet. Strängarna är skrivbara och genereras automatiskt och tilldelas av systemet när ett tilläggspaket importeras.

Om ett tilläggspaket med namnet `example-package` har en åtgärd med namnet `custom-code`, har den åtgärden följande delegatbeskrivnings-ID: `example-package::actions::custom-code`.

## Använda delegatbeskrivnings-ID på tillämpliga resurser

Delegeringsbeskrivnings-ID:n är viktiga att förstå när det gäller att definiera regelkomponenter (händelser, villkor och åtgärder) och dataelement i API:t. Avsnitten nedan visar hur dessa ID:n spelas upp för varje resurs.

### Regelkomponenter

En [regelkomponent](../endpoints/rule-components.md) måste associeras med en händelse, ett villkor eller en åtgärd som tillhör ett tilläggspaket. Detta representerar regelkomponentens&quot;typ&quot; som den hör till logiken för den övergripande regeln (en händelse, ett villkor eller en åtgärd). När du skapar en regelkomponent måste därför ett delegatbeskrivnings-ID anges för att ange vilken händelse, vilket villkor eller vilken åtgärd regelkomponenten ska kopplas till.

Om du till exempel vill skapa en händelseregelkomponent som är baserad på en `click`-händelse i ett tilläggspaket `example-package` använder regelkomponenten följande `delegate_descriptor_id`-värde: `example-package::events::click`.

Mer information finns i avsnittet [skapa en regelkomponent](../endpoints/rule-components.md#create).

### Dataelement

Ett [dataelement](../endpoints/data-elements.md) måste associeras med ett tilläggspaket när det skapas, eftersom varje tilläggspaket definierar kompatibla typer för sina delegatdataelement samt deras avsedda beteende.

Om du till exempel vill skapa ett dataelement som använder typen `cookie` som definieras av ett tilläggspaket `example-package`, använder dataelementet följande `delegate_descriptor_id`-värde: `example-package::dataElements::cookie`.

Mer information finns i avsnittet [skapa ett dataelement](../endpoints/data-elements.md#create).

### Tillägg

Ett [tillägg](../endpoints/extensions.md) kopplas automatiskt till ett tilläggspaket när det skapas, och representeras i tilläggets `relationships`-objekt. Om tillägget kräver anpassade inställningar krävs även ett delegatbeskrivnings-ID.

>[!NOTE]
>
>Tillägg som inte kräver anpassade inställningar behöver inget delegatbeskrivnings-ID.

Om du till exempel vill lägga till ett delegatbeskrivnings-ID i ett tillägg som tillhör tilläggspaketet `example-package` använder tillägget följande `delegate_descriptor_id`-värde: `example-package::extensionConfiguration::config`.

Mer information finns i guiden [skapa ett tillägg](../endpoints/extensions.md#create).