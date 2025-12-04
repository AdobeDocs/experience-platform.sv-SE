---
title: cookie
description: Skriv, redigera eller ta bort cookies manuellt för taggegenskapen.
source-git-commit: 434d6913ea391b127b4b52c8494730c496bbcfe2
workflow-type: tm+mt
source-wordcount: '382'
ht-degree: 2%

---

# `cookie`

Objektet `_satellite.cookie` innehåller metoder som gör att du kan skriva, redigera eller ta bort cookies som taggreglerna kan referera till. Det är en partiell kopia av [`js-cookie`](https://github.com/js-cookie/js-cookie) som innehåller många kärnfunktioner i det biblioteket.

## `cookie.set()`

Metoden `set()` skriver en cookie som taggegenskapen kan referera till.

```ts
_satellite.cookie.set(name: string, value: string, attributes?: {
  expires?: number | Date;
  path?: string;
  domain?: string;
  secure?: boolean;
  sameSite?: 'Strict' | 'Lax' | 'None';
}): string
```

Följande metodparametrar är tillgängliga:

| Namn | Typ | Obligatoriskt | Beskrivning |
|---|---|---|---|
| **`name`** | `string` | Ja | Namnet på kakan. |
| **`value`** | `string` | Ja | Värdet på cookien |
| **`attributes`** | `object` | Nej | Ytterligare attribut som du vill att cookien ska ha. |

Objektet `attributes` stöder följande egenskaper:

| Attributnamn | Typ | Obligatoriskt | Standard | Beskrivning |
|---|---|---|---|---|
| **`expires`** | `number` eller [`Date`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date) | Nej | Cookie förfaller i slutet av webbläsarsessionen | Antalet dagar som du vill att cookien ska förfalla. |
| **`path`** | `string` | Nej | Cookie, synlig på hela webbplatsen | Var på din domän cookien är synlig. |
| **`domain`** | `string` | Nej | Cookie som är synlig för domänen som den skapades under | En giltig domän (med eller utan en underdomän) där cookien är synlig. Om en domän ingår utan en underdomän är cookien synlig för alla underdomäner under den domänen. |
| **`secure`** | `boolean` | Nej | Ingen attributuppsättning | Avgör om cookien kräver ett säkert protokoll (`https://`). Om det utelämnas finns det inga säkra protokollkrav. |
| **`sameSite`** | `'Strict' \| 'Lax' \| 'None'` | Nej | Ingen attributuppsättning | Gör att du kan ange attributet [`sameSite`](https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Headers/Set-Cookie#samesitesamesite-value) för en cookie. Om du anger `sameSite` som `None` måste du även ange `secure` som `true`. |

```js
// Sets a cookie valid across the entire site, expires on session close
_satellite.cookie.set('simple_session_cookie', 'value');

// Sets a cookie that expires 7 days from now, valid across the entire site
_satellite.cookie.set('seven_day_cookie', 'value', { expires: 7 });

// Sets a cookie that expires 14 days from now, valid only on the current page
_satellite.cookie.set('page_specific_cookie', 'value', { expires: 14, path: '/' });

// Cross-site compatible cookie (requires HTTPS)
_satellite.cookie.set('cross_site_cookie', 'value', { secure: true, sameSite: 'None' });
```

Anrop av den här metoden skriver önskad cookie och returnerar den serialiserade cookie-strängen som skrivits. Strängen används främst för felsökning och loggning.

```text
'written_cookie=value; path=/'
```

>[!TIP]
>
>Tidigare versioner av taggobjektet använde `_satellite.setCookie()`. Metoden `setCookie()` har ersatts med `_satellite.cookie.set()`.

## `cookie.get()`

Metoden `get()` returnerar ett cookie-värde.

```ts
_satellite.cookie.get(name: string): string | undefined;
```

| Namn | Typ | Obligatoriskt | Beskrivning |
|---|---|---|---|
| **`name`** | `string` | Ja | Det cookie-namn som du vill hämta värdet från (skiftlägeskänsligt). |

Om cookie-namnet finns returneras cookie-värdet. Om cookie-namnet inte finns returnerar `undefined`.

>[!TIP]
>
>Tidigare versioner av taggobjektet använde `_satellite.getCookie()`. Metoden `getCookie()` har ersatts med `_satellite.cookie.get()`.

## `cookie.remove()`

Metoden `remove()` tar bort en cookie som du har angett.

```ts
_satellite.cookie.remove(name: string, attributes?: {
  path?: string;
  domain?: string;
}): void
```

| Namn | Typ | Obligatoriskt | Beskrivning |
|---|---|---|---|
| **`name`** | `string` | Ja | Det cookie-namn som du vill ta bort. |
| **`attributes`** | `object` | Nej | De attribut som är associerade med den cookie som du vill ta bort. Om du anger en cookie med attributen `path` eller `domain` ska du ta med samma attribut när du tar bort cookien. Om attributen inte tas med tas inte cookien bort. |

```js
// Creates a session cookie
_satellite.cookie.set('session_cookie', 'Cookie value');

// Removes the above cookie
_satellite.cookie.remove('session_cookie');

// Creates a cookie that is only visible on the current page
_satellite.cookie.set('page_specific_cookie', 'value', { path: '/' });

// This remove method does nothing because it does not match the path and domain attributes of the cookie set
_satellite.cookie.remove('page_specific_cookie');

// This remove method works correctly for the page-specific cookie
_satellite.cookie.remove('page_specific_cookie', { path: '/' });
```

>[!TIP]
>
>Tidigare versioner av taggobjektet använde `_satellite.removeCookie()`. Metoden `removeCookie()` har ersatts med `_satellite.cookie.remove()`.
