---
keywords: Experience Platform;hem;populära ämnen;frågetjänst;frågetjänst;ansluta;ansluta till frågetjänst;SSL;ssl;sslmode;
title: SSL-alternativ för frågetjänst
description: Lär dig mer om SSL-stöd för tredjepartsanslutningar till Adobe Experience Platform Query Service och hur du ansluter i SSL-läge för verifiering.
source-git-commit: 92dac8e75e1ddda860d255ce1b7d278041c89325
workflow-type: tm+mt
source-wordcount: '905'
ht-degree: 1%

---

# [!DNL Query Service] SSL-alternativ

För ökad säkerhet, Adobe Experience Platform [!DNL Query Service] har inbyggt stöd för SSL-anslutningar för kryptering av klient-/serverkommunikation. Det här dokumentet innehåller tillgängliga SSL-alternativ för klientanslutningar från tredje part till [!DNL Query Service] och hur du ansluter med `verify-full` SSL-parametervärde.

## Förutsättningar

Det här dokumentet förutsätter att du redan har laddat ned ett klientprogram från tredje part för användning med plattformsdata. Specifika anvisningar om hur SSL-säkerhet ska infogas vid anslutning till en tredjepartsklient finns i respektive anslutningsguide. För en lista med alla [!DNL Query Service] klienter som stöds, se [översikt över klientanslutningar](./overview.md).

## Tillgängliga SSL-alternativ {#available-ssl-options}

Plattformen har stöd för olika SSL-alternativ som passar dina datasäkerhetsbehov och som balanserar bearbetningskostnaderna för kryptering och nyckelutbyte.

Skillnaden `sslmode` parametervärden ger olika skyddsnivåer. Genom att kryptera dina data i rörelse med SSL-certifikat hjälper det till att förhindra MITM-attacker (man-in-the-middle), tjuvlyssning och personifiering. Tabellen nedan innehåller en beskrivning av de olika SSL-lägena som är tillgängliga och den skyddsnivå de erbjuder.

>[!NOTE]
>
> SSL-värdet `disable` stöds inte av Adobe Experience Platform på grund av att dataskydd krävs.

| sslmode | Eavesdroppskydd | MITM-skydd | Beskrivning |
|---|---|---|---|
| `allow` | Delvis | Nej | Säkerhet är inte en prioritet, snabbhet och låga bearbetningskostnader är viktigare. Det här läget väljer bara kryptering om servern har tillgång till det. |
| `prefer` | Delvis | Nej | Kryptering krävs inte, men kommunikationen krypteras om servern stöder den. |
| `require` | Ja | Nej | Kryptering krävs för all kommunikation. Nätverket är betrott för att ansluta till rätt server. Server SSL-certifikatvalidering krävs inte. |
| `verify-ca` | Ja | Beroende på CA-princip | Kryptering krävs för all kommunikation. Servervalidering krävs innan data delas. Detta kräver att du skapar ett rotcertifikat i PostgreSQL-arbetskatalogen. [Mer information finns nedan](#instructions) |
| `verify-full` | Ja | Ja | Kryptering krävs för all kommunikation. Servervalidering krävs innan data delas. Detta kräver att du skapar ett rotcertifikat i PostgreSQL-arbetskatalogen. [Mer information finns nedan](#instructions). |

>[!NOTE]
>
>Skillnaden mellan `verify-ca` och `verify-full` beror på rotcertifikatutfärdarens profil. Om du har skapat en egen lokal certifikatutfärdare för att utfärda privata certifikat för dina program använder du `verify-ca` ger ofta tillräckligt skydd. Om du använder en offentlig certifikatutfärdare `verify-ca` tillåter anslutningar till en server som någon annan kan ha registrerat hos certifikatutfärdaren. `verify-full` ska alltid användas med en offentlig rotcertifikatutfärdare.

När du upprättar en tredjepartsanslutning till en plattformsdatabas bör du använda `sslmode=require` till ett minimum för att säkerställa en säker anslutning för dina data i rörelse. The `verify-full` SSL-läge rekommenderas för de flesta säkerhetskänsliga miljöer.

## Konfigurera ett rotcertifikat för serververifiering {#root-certificate}

För att säkerställa en säker anslutning måste SSL-användningen konfigureras på både klienten och servern innan anslutningen görs. Om SSL bara är konfigurerat på servern kan klienten skicka känslig information, till exempel lösenord, innan det etableras att servern kräver hög säkerhet.

Som standard [!DNL PostgreSQL] verifierar inte servercertifikatet. Verifiera serverns identitet och säkerställa en säker anslutning innan känsliga data skickas (som en del av SSL `verify-full` måste du placera ett rotcertifikat (självsignerat) på den lokala datorn (`root.crt`) och ett lövcertifikat som signerats av rotcertifikatet på servern.

Om `sslmode` parametern är inställd på `verify-full`, kommer libpq att verifiera att servern är tillförlitlig genom att kontrollera certifikatkedjan upp till rotcertifikatet som lagras på klienten. Sedan verifieras att värdnamnet matchar namnet som lagras i servercertifikatet.

Om du vill tillåta verifiering av servercertifikat måste du placera ett eller flera rotcertifikat (`root.crt`) i [!DNL PostgreSQL] i din arbetskatalog. Filsökvägen liknar `~/.postgresql/root.crt`.

## Aktivera verifieringsläge för fullständig SSL för användning med tredje part [!DNL Query Service] anslutning {#instructions}

Om du behöver striktare säkerhetskontroll än `sslmode=require`kan du följa de markerade stegen för att ansluta en tredjepartsklient till [!DNL Query Service] använda `verify-full` SSL-läge.

>[!NOTE]
>
>Det finns många alternativ för att uppnå ett SSL-certifikat. På grund av den ökande trenden när det gäller otillåtna certifikat används DigiCert i den här guiden eftersom de är en betrodd global leverantör av TLS/SSL-, PKI-, IoT- och signeringslösningar med hög säkerhet.

1. Navigera till [listan över tillgängliga DigiCert-rotcertifikat](https://www.digicert.com/kb/digicert-root-certificates.htm)
1. Sök efter &quot;[!DNL DigiCert Global Root CA]&quot; i listan över tillgängliga certifikat.
1. Välj [!DNL **Hämta PEM**] för att hämta filen till din lokala dator.
   ![Listan med tillgängliga DigiCert-rotcertifikat med nedladdnings-PEM markerad.](../images/clients/ssl-modes/digicert.png)
1. Byt namn på säkerhetscertifikatfilen till `root.crt`.
1. Kopiera filen till [!DNL PostgreSQL] mapp. Den nödvändiga filsökvägen varierar beroende på operativsystem. Om mappen inte redan finns skapar du den.
   - Om du använder macOS är sökvägen `/Users/<username>/.postgresql`
   - Om du använder Windows är sökvägen `%appdata%\postgresql`

>[!TIP]
>
>För att hitta `%appdata%` filens plats i ett Windows-operativsystem, tryck på ⊞ **Win + R** och indata `%appdata%` i sökfältet.

Efter [!DNL DigiCert Global Root CA] CRT-filen är tillgänglig i [!DNL PostgreSQL] mapp kan du ansluta till [!DNL Query Service] med `sslmode=verify-full` eller `sslmode=verify-ca` alternativ.

## Nästa steg

Genom att läsa det här dokumentet får du en bättre förståelse för de tillgängliga SSL-alternativen för att ansluta en tredjepartsklient till [!DNL Query Service]och även hur du aktiverar `verify-full` SSL-alternativ för att kryptera dina data i rörelse.

Om du inte redan har gjort det, följ anvisningarna på [ansluta en tredjepartsklient till [!DNL Query Service]](./overview.md).
