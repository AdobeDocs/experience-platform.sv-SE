---
keywords: Experience Platform;hem;populära ämnen;frågetjänst;frågetjänst;ansluta;ansluta till frågetjänst;SSL;ssl;sslmode;
title: SSL-alternativ för frågetjänst
description: Lär dig mer om SSL-stöd för tredjepartsanslutningar till Adobe Experience Platform Query Service och hur du ansluter i SSL-läge för verifiering.
exl-id: 41b0a71f-165e-49a2-8a7d-d809f5f683ae
source-git-commit: 37c30fc1a040efbce0c221c10b36e105d5b1a962
workflow-type: tm+mt
source-wordcount: '1008'
ht-degree: 0%

---

# SSL-alternativ för [!DNL Query Service]

För ökad säkerhet tillhandahåller Adobe Experience Platform [!DNL Query Service] inbyggt stöd för SSL-anslutningar för kryptering av klient-/serverkommunikation. Det här dokumentet innehåller tillgängliga SSL-alternativ för klientanslutningar från tredje part till [!DNL Query Service] och hur du ansluter med SSL-parametervärdet `verify-full`.

## Förhandskrav

Det här dokumentet förutsätter att du redan har laddat ned ett klientprogram från tredje part för användning med plattformsdata. Specifika anvisningar om hur SSL-säkerhet ska infogas vid anslutning till en tredjepartsklient finns i respektive anslutningsguide. En lista över alla [!DNL Query Service]-klienter som stöds finns i [Översikt över klientanslutningar](./overview.md).

## Tillgängliga SSL-alternativ {#available-ssl-options}

Plattformen har stöd för olika SSL-alternativ som passar dina datasäkerhetsbehov och som balanserar bearbetningskostnaderna för kryptering och nyckelutbyte.

De olika `sslmode`-parametervärdena ger olika skyddsnivåer. Genom att kryptera dina data i rörelse med SSL-certifikat hjälper det till att förhindra MITM-attacker (man-in-the-middle), tjuvlyssning och personifiering. Tabellen nedan innehåller en beskrivning av de olika SSL-lägena som är tillgängliga och den skyddsnivå de erbjuder.

>[!NOTE]
>
> SSL-värdet `disable` stöds inte av Adobe Experience Platform på grund av nödvändig dataskyddskompatibilitet.

| sslmode | Eavesdroppskydd | MITM-skydd | Beskrivning |
|---|---|---|---|
| `allow` | Ja | Nej | Kryptering krävs för all kommunikation. Nätverket är betrott för att ansluta till rätt server. |
| `prefer` | Ja | Nej | Kryptering krävs för all kommunikation. Nätverket är betrott för att ansluta till rätt server. |
| `require` | Ja | Nej | Kryptering krävs för all kommunikation. Nätverket är betrott för att ansluta till rätt server. Server SSL-certifikatvalidering krävs inte. |
| `verify-ca` | Ja | Beroende på CA-princip | Kryptering krävs för all kommunikation. Servervalidering krävs innan data delas. Detta kräver att du konfigurerar ett rotcertifikat i din [!DNL PostgreSQL]-arbetskatalog. [Mer information finns nedan](#instructions) |
| `verify-full` | Ja | Ja | Kryptering krävs för all kommunikation. Servervalidering krävs innan data delas. Detta kräver att du konfigurerar ett rotcertifikat i din [!DNL PostgreSQL]-arbetskatalog. [Mer information finns nedan](#instructions). |

>[!NOTE]
>
>Skillnaden mellan `verify-ca` och `verify-full` beror på principen för rotcertifikatutfärdaren (CA). Om du har skapat en egen lokal certifikatutfärdare för att utfärda privata certifikat för dina program ger `verify-ca` ofta tillräckligt skydd. Om du använder en offentlig certifikatutfärdare tillåter `verify-ca` anslutningar till en server som någon annan kan ha registrerat hos certifikatutfärdaren. `verify-full` ska alltid användas med en offentlig rotcertifikatutfärdare.

När du upprättar en tredjepartsanslutning till en plattformsdatabas bör du använda `sslmode=require` som ett minimum för att säkerställa en säker anslutning för dina data i rörelse. SSL-läget `verify-full` rekommenderas för de flesta säkerhetskänsliga miljöer.

## Konfigurera ett rotcertifikat för serververifiering {#root-certificate}

>[!IMPORTANT]
>
>TLS/SSL-certifikaten i produktionsmiljöer för API:t för frågetjänsten Interactive Postgres uppdaterades onsdagen den 24 januari 2024.<br>Även om detta är ett årligt krav har rotcertifikatet i kedjan även ändrats eftersom Adobe TLS/SSL-certifikatprovidern har uppdaterat sin certifikathierarki. Detta kan påverka vissa Postgres-klienter om deras lista över certifikatutfärdare saknar rotcertifikatet. En PSQL CLI-klient kan till exempel behöva lägga till rotcertifikaten i en explicit fil `~/postgresql/root.crt`, annars kan det leda till ett fel. Exempel: `psql: error: SSL error: certificate verify failed`. Mer information om det här problemet finns i den [officiella PostgreSQL-dokumentationen](https://www.postgresql.org/docs/current/libpq-ssl.html#LIBQ-SSL-CERTIFICATES).<br>Rotcertifikatet som ska läggas till kan hämtas från [https://cacerts.digicert.com/DigiCertGlobalRootG2.crt.pem](https://cacerts.digicert.com/DigiCertGlobalRootG2.crt.pem).

För att säkerställa en säker anslutning måste SSL-användningen konfigureras på både klienten och servern innan anslutningen görs. Om SSL bara är konfigurerat på servern kan klienten skicka känslig information, till exempel lösenord, innan det etableras att servern kräver hög säkerhet.

Som standard utför inte [!DNL PostgreSQL] någon verifiering av servercertifikatet. Om du vill verifiera serverns identitet och säkerställa en säker anslutning innan känsliga data skickas (som en del av SSL `verify-full`-läget) måste du placera ett rotcertifikat (självsignerat) på den lokala datorn (`root.crt`) och ett lövcertifikat som signerats av rotcertifikatet på servern.

Om parametern `sslmode` är inställd på `verify-full` verifierar libpq att servern är tillförlitlig genom att kontrollera certifikatkedjan upp till rotcertifikatet som lagras på klienten. Sedan verifieras att värdnamnet matchar namnet som lagras i servercertifikatet.

Om du vill tillåta verifiering av servercertifikat måste du placera ett eller flera rotcertifikat (`root.crt`) i filen [!DNL PostgreSQL] i din arbetskatalog. Filsökvägen liknar `~/.postgresql/root.crt`.

## Aktivera Verifiera fullständigt SSL-läge för användning med en anslutning från tredje part till [!DNL Query Service] {#instructions}

Om du behöver striktare säkerhetskontroll än `sslmode=require` kan du följa de steg som är markerade för att ansluta en tredjepartsklient till [!DNL Query Service] med SSL-läget `verify-full`.

>[!NOTE]
>
>Det finns många alternativ för att uppnå ett SSL-certifikat. På grund av den ökande trenden när det gäller otillåtna certifikat används DigiCert i den här guiden eftersom de är en betrodd global leverantör av TLS/SSL-, PKI-, IoT- och signeringslösningar med hög säkerhet.

1. Navigera till [listan med tillgängliga DigiCert-rotcertifikat](https://www.digicert.com/kb/digicert-root-certificates.htm)
1. Sök efter [!DNL DigiCert Global Root G2] i listan över tillgängliga certifikat.
1. Välj [!DNL **Hämta PEM**] om du vill hämta filen till den lokala datorn.
   ![Listan med tillgängliga DigiCert-rotcertifikat med nedladdnings-PEM är markerad.](../images/clients/ssl-modes/digicert.png)
1. Byt namn på säkerhetscertifikatfilen till `root.crt`.
1. Kopiera filen till mappen [!DNL PostgreSQL]. Den nödvändiga filsökvägen varierar beroende på operativsystem. Om mappen inte redan finns skapar du den.
   - Om du använder macOS är sökvägen `/Users/<username>/.postgresql`
   - Om du använder Windows är sökvägen `%appdata%\postgresql`

>[!TIP]
>
>Om du vill hitta din `%appdata%`-filplats på ett Windows-operativsystem trycker du på ⊞ **Win + R** och anger `%appdata%` i sökfältet.

När CRT-filen [!DNL DigiCert Global Root G2] är tillgänglig i mappen [!DNL PostgreSQL] kan du ansluta till [!DNL Query Service] med alternativet `sslmode=verify-full` eller `sslmode=verify-ca`.

## Nästa steg

Genom att läsa det här dokumentet får du en bättre förståelse för de tillgängliga SSL-alternativen för att ansluta en tredjepartsklient till [!DNL Query Service] och även för hur du aktiverar SSL-alternativet `verify-full` för att kryptera dina data i rörelse.

Om du inte redan har gjort det följer du vägledningen om att [ansluta en tredjepartsklient till [!DNL Query Service]](./overview.md).
