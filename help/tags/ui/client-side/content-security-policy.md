---
title: Stöd för CSP (Content Security Policy)
description: Lär dig hur du hanterar begränsningar för CSP (Content Security Policy) när du integrerar webbplatsen med taggar i Adobe Experience Platform.
exl-id: 9232961e-bc15-47e1-aa6d-3eb9b865ac23
source-git-commit: a8b0282004dd57096dfc63a9adb82ad70d37495d
workflow-type: tm+mt
source-wordcount: '1080'
ht-degree: 0%

---

# Stöd för CSP (Content Security Policy)

>[!NOTE]
>
>Adobe Experience Platform Launch har omklassificerats som en serie datainsamlingstekniker i Adobe Experience Platform. Som ett resultat av detta har flera terminologiska förändringar införts i produktdokumentationen. Se följande [dokument](../../term-updates.md) för en konsoliderad hänvisning till terminologiska förändringar.

En CSP (Content Security Policy) är en säkerhetsfunktion som hjälper till att förhindra serveröverskridande skriptattacker (XSS). Det här händer när webbläsaren tricks med att köra skadligt innehåll som verkar komma från en betrodd källa men som verkligen kommer från någon annan. Med CSP:er kan webbläsaren (för användarens räkning) verifiera att skriptet verkligen kommer från en betrodd källa.

CSP implementeras genom att lägga till en `Content-Security-Policy` HTTP-huvud till serversvar eller genom att lägga till en konfigurerad `<meta>` -elementet i `<head>` i dina HTML-filer.

>[!NOTE]
>
> Mer detaljerad information om CSP finns i [MDN-webbdokument](https://developer.mozilla.org/en-US/docs/Web/HTTP/CSP).

Taggar i Adobe Experience Platform är ett tagghanteringssystem som är utformat för att dynamiskt läsa in skript på din webbplats. En standard-CSP blockerar dessa dynamiskt inlästa skript på grund av potentiella säkerhetsproblem. Det här dokumentet innehåller riktlinjer för hur du konfigurerar din CSP så att dynamiskt inlästa skript från taggar tillåts.

Om du vill att taggar ska fungera med din CSP finns det två stora utmaningar att övervinna:

* **Källan för ditt taggbibliotek måste vara betrodd.** Om det här villkoret inte uppfylls blockeras taggbiblioteket och andra nödvändiga JavaScript-filer av webbläsaren och läses inte in på sidan.
* **Textbundna skript måste tillåtas.** Om det här villkoret inte uppfylls blockeras åtgärder för regler för anpassad kod på sidan och de kommer inte att utföras korrekt.

Ökad säkerhet kräver mer arbete för innehållsskaparens räkning. Om du vill använda taggar och ha en CSP på plats måste du åtgärda båda dessa problem utan att felaktigt markera andra skript som säkra. Resten av detta dokument innehåller riktlinjer för hur du ska uppnå detta.

## Lägg till taggar som en betrodd källa

När du använder en CSP måste du inkludera alla betrodda domäner inom värdet för `Content-Security-Policy` header. Vilket värde du måste ange för taggar varierar beroende på vilken typ av värdtjänst du använder.

### Självvärdande

Om du [värdtjänster](../publishing/hosts/self-hosting-libraries.md) ditt bibliotek, är källan för ditt bygge troligtvis din egen domän. Du kan ange att värddomänen är en säker källa med följande konfiguration:

**HTTP-huvud**

```http
Content-Security-Policy: script-src 'self'
```

**HTML `<meta>` tag**

```html
<meta http-equiv="Content-Security-Policy" content="script-src 'self'">
```

### Värdtjänster som hanteras av Adobe

Om du använder en [värddator som hanteras av Adobe](../publishing/hosts/managed-by-adobe-host.md)och din version underhålls på `assets.adobedtm.com`. Du bör ange `self` som en säker domän så att du inte bryter några skript som du redan läser in, men du behöver också `assets.adobedtm.com` för att anges som säker, annars läses inte taggbiblioteket in på sidan. I så fall bör du använda följande konfiguration:

**HTTP-huvud**

```http
Content-Security-Policy: script-src 'self' assets.adobedtm.com
```

**HTML `<meta>` tag**


Det finns en mycket viktig förutsättning: Du måste läsa in taggbiblioteket [asynkront](./asynchronous-deployment.md). Detta fungerar inte med synkron inläsning av taggbiblioteket (vilket resulterar i konsolfel och att reglerna inte körs som de ska).

```html
<meta http-equiv="Content-Security-Policy" content="script-src 'self' assets.adobedtm.com">
```

Du bör ange `self` som en säker domän så att alla skript som du redan läser in fortsätter att fungera, men du behöver också `assets.adobedtm.com` för att anges som säker, annars läses inte ditt bibliotek in på sidan.

## Textbundna skript

CSP tillåter inte infogade skript som standard och måste därför konfigureras manuellt för att tillåta dem. Du kan välja mellan två alternativ:

* [Tillåt som en gång](#nonce) (god säkerhet)
* [Tillåt alla textbundna skript](#unsafe-inline) (minst säkert)

>[!NOTE]
>
>CSP-specifikationen innehåller information om ett tredje alternativ som använder hash-koder, men det här tillvägagångssättet går inte att använda med tagghanteringssystem som taggar. Mer information om begränsningar för att använda hash-koder med taggar i Platform finns i [Stödlinje för delresursintegritet (SRI)](./sri.md).

### Tillåt som en gång {#nonce}

Den här metoden innebär att generera en kryptografisk engångsversion och lägga till den i din CSP och alla infogade skript på din plats. När webbläsaren tar emot en instruktion om att läsa in ett textbundet skript med ett nonce, jämför webbläsaren värdet nonce med vad som finns i CSP-huvudet. Om det matchar läses skriptet in. Det här värdet ska ändras för varje ny sidinläsning.

>[!IMPORTANT]
>
>Om du vill använda den här metoden måste du läsa in bygget asynkront. Detta fungerar inte när bygget läses in synkront, vilket resulterar i konsolfel och att reglerna inte körs som de ska. Se guiden [asynkron distribution](./asynchronous-deployment.md) för mer information.

I exemplen nedan visas hur du kan lägga till ditt namn i CSP-konfigurationen för en värddator som hanteras med Adobe. Om du använder värdtjänster kan du utesluta `assets.adobedtm.com`.

**HTTP-huvud**

```http
Content-Security-Policy: script-src 'self' assets.adobedtm.com 'nonce-2726c7f26c'
```

**HTML `<meta>` tag**

```html
<meta http-equiv="Content-Security-Policy" content="script-src 'self' assets.adobedtm.com 'nonce-2726c7f26c'">
```

När du har konfigurerat sidhuvudet eller HTML-taggen måste du ange var taggen ska hittas när ett textbundet skript läses in. För att en tagg ska kunna använda nonce när skriptet läses in måste du:

1. Skapa ett dataelement som refererar till var nonce finns i datalagret.
1. Konfigurera Core Extension och ange vilket dataelement du använde.
1. Publicera dataelement och ändringar i Core Extension.

>[!NOTE]
>
>Processen ovan hanterar bara inläsning av din anpassade kod, inte vad den anpassade koden gör. Om ett infogat skript innehåller anpassad kod som inte är kompatibel med din CSP har CSP företräde. Om du till exempel använder anpassad kod för att läsa in ett infogat skript genom att lägga till det i DOM, kan taggen inte lägga till det på rätt sätt, så att en viss anpassad kodsåtgärd inte fungerar som förväntat.

### Tillåt alla textbundna skript {#unsafe-inline}

Om det inte fungerar att använda funktioner för dig kan du konfigurera din CSP så att alla infogade skript tillåts. Det här är det minst säkra alternativet, men det är också enklare att implementera och underhålla.

Exemplen nedan visar hur kan tillåta alla infogade skript i CSP-huvudet.

#### Självvärdande

Använd följande konfigurationer om du använder värdtjänster:

**HTTP-huvud**

```http
Content-Security-Policy: script-src 'self' 'unsafe-inline'
```

**HTML `<meta>` tag**

```html
<meta http-equiv="Content-Security-Policy" content="script-src 'self' 'unsafe-inline'">
```

#### Värdtjänster som hanteras av Adobe

Använd följande konfigurationer om du använder värdtjänster som hanteras i Adobe:

**HTTP-huvud**

```http
Content-Security-Policy: script-src 'self' assets.adobedtm.com 'unsafe-inline'
```

**HTML `<meta>` tag**

```html
<meta http-equiv="Content-Security-Policy" content="script-src 'self' assets.adobedtm.com 'unsafe-inline'">
```

## Nästa steg

Genom att läsa det här dokumentet bör du nu förstå hur du konfigurerar CSP-huvudet så att det godkänner taggbiblioteksfilen och infogade skript.

Som en extra säkerhetsåtgärd kan du även välja att använda SRI (Subresource Integrity) för att validera hämtade biblioteksbyggen. Den här funktionen har dock vissa begränsningar när den används med tagghanteringssystem som taggar. Se guiden [SRI-kompatibilitet för plattform](./sri.md) för mer information.
