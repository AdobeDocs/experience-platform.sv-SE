---
title: Delning av mobil-till-webb och domänövergripande ID
description: Lär dig hur du behåller besökar-ID:n från mobil- till webbegenskaper och mellan domäner
keywords: Identitet;mobil;id;sharing;domain;cross-domain;sdk;platform;
exl-id: b9bb236f-52cf-4615-96d8-1137d957de8c
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '457'
ht-degree: 0%

---

# Delning av mobil-till-webb och domänövergripande ID

## Översikt

Adobe Experience Platform Web SDK har stöd för delning av besökar-ID, vilket gör det möjligt för kunderna att leverera personaliserade upplevelser på ett mer korrekt sätt, mellan mobilappar och mobilwebbinnehåll samt mellan domäner.

## Användningsfall {#use-cases}

### Leverera enhetlig personalisering mellan mobilappar och mobilwebbplatser

Ett klädföretag vill personalisera sina kunders upplevelse utifrån deras intressen och hålla personaliseringen korrekt i en mobilapplikation som även läser in WebViews. Genom att använda funktionen för delning av mobil-till-webb-ID kan de se till att de mest korrekta erbjudandena presenteras för kunderna, med samma besökaridentifierare i appen och mobilwebbinnehållet, genom att skicka [!DNL ECID] till mobilwebbadressen.

### Leverera enhetlig personalisering över domäner

En återförsäljare med flera onlinebutiker vill personalisera shoppingupplevelsen över sina domäner utifrån kundernas intressen. Med hjälp av funktionen för delning av domänövergripande ID i Web SDK kan återförsäljaren leverera korrekta erbjudanden baserat på kundernas intressen i alla sina domäner.

### Förbättra rapporter om besöksaktivitet

En teknikhandlare vill förbättra sin rapportering om besökaraktivitet med information om när besökarna flyttar från mobilappen till mobilwebbplatsen eller till andra domäner. Med hjälp av funktionen för delning av domänövergripande ID i Web SDK kan marknadsföringsteamet spåra besökare på deras webbsajter och generera aktivitetsrapporter.

## Förhandskrav {#prerequisites}

Om du vill använda delning av mobil-till-webb och domänövergripande ID måste du använda [!DNL Web SDK] version 2.11.0 eller senare.

För mobilimplementeringar i Edge Network stöds den här funktionen i tillägget [Identity for Edge Network](https://developer.adobe.com/client-sdks/documentation/identity-for-edge-network/) med början i version 1.1.0 (iOS och Android).

Den här funktionen är även kompatibel med [!DNL VisitorAPI.js] version 1.7.0 eller senare.

## Delning av mobil-till-webb-ID {#mobile-to-web}

Använd `getUrlVariables`-API:t från tillägget [ Identitet för Edge Network](https://developer.adobe.com/client-sdks/documentation/identity-for-edge-network/api-reference/#geturlvariables) för att hämta identifierare som frågeparametrar och koppla dem till din URL när du öppnar [!DNL webViews].

Ingen ytterligare konfiguration krävs för att Web SDK ska acceptera `ECID` värden i frågesträngen.

Frågesträngsparametern innehåller:

* `MCID`: Experience Cloud-ID (`ECID`)
* `MCORGID`: Experience Cloud `orgID` som måste matcha `orgID` som konfigurerats i [!DNL Web SDK].
* `TS`: En tidsstämpelparameter som inte kan vara äldre än fem minuter.


För delning av mobil-till-webb-ID används parametern `adobe_mc`. När parametern `adobe_mc` finns och är giltig läggs `ECID` från frågesträngen automatiskt till i identitetskartan i den första begäran som görs i Edge Network. Alla efterföljande Edge Network-interaktioner kommer att använda `ECID`.

Mer information om hur du skickar besökar-ID:n från en mobilapp till en WebView finns i dokumentationen om [hantering av WebViews](https://experienceleague.adobe.com/docs/platform-learn/implement-mobile-sdk/app-implementation/web-views.html#implementation).

## Implementera delning av domänöverskridande ID {#cross-domain-sharing}

Se [`appendIdentityToUrl`](../commands/appendidentitytourl.md)-kommandot för implementeringsinstruktioner med både Web SDK-taggtillägget och Web SDK JavaScript-biblioteket.
