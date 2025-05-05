---
title: API-tillägg för Adobe Amazon Conversion
description: Med Adobe Experience Platform webbevent-API kan du dela webbinteraktioner direkt med Amazon.
last-substantial-update: 2025-04-17T00:00:00Z
source-git-commit: 65a3eb20dc3de62319f73be49197dacb8fc1778b
workflow-type: tm+mt
source-wordcount: '672'
ht-degree: 0%

---

# API-tilläggets [!DNL Amazon] för webbhändelser - översikt

API-tillägget [!DNL Amazon] för konvertering skapar en direkt anslutning mellan marknadsföringsdata från en annonsörs server och [!DNL Amazon]. På så sätt kan annonsörer utvärdera kampanjens effektivitet oavsett var de befinner sig och optimera kampanjer utifrån detta. Tillägget ger mer fullständig attribuering, förbättrad datatillförlitlighet och bättre optimerad leverans.

## Krav för [!DNL Amazon] {#prerequisites}

Innan du installerar och konfigurerar API-tillägget [!DNL Amazon] Conversion måste du slutföra flera nödvändiga steg för att säkerställa korrekt autentisering och dataåtkomst.

### Skapa en hemlighet och ett dataelement {#secret}

Autentisering med [!DNL Amazon] kräver en säker token som måste lagras och refereras korrekt:

1. Skapa en ny [!DNL Amazon]-händelsevidarebefordringshemlighet med ett unikt namn för autentisering.
2. Skapa ett dataelement med tillägget **Core** med datatypen **Secret** som referens till din [!DNL Amazon]-hemlighet.

Den här processen garanterar att inloggningsuppgifterna förblir säkra samtidigt som de är tillgängliga för tillägget vid behov.

## Installera och konfigurera tillägget [!DNL Amazon]

För att kunna installera tillägget måste du ha tillgång till din egenskap för vidarebefordring av händelser i Experience Platform:

- Skapa eller redigera en egenskap för vidarebefordring av händelser.
- Välj **Tillägg** i den vänstra navigeringen och välj sedan [!DNL Amazon]-tillägget på fliken Katalog.
- Välj **Installera**.

Tillägget ![[!DNL Amazon] har valts i tilläggskatalogen tillsammans med installationsknappen.](../../../images/extensions/server/amazon/amazon-extension.png)

- Konfigurera med:

- **Åtkomsttoken**: Din dataelementhemlighet som innehåller OAuth 2-token

![Individuella inställningar för att ange dataelementets hemlighet markerat.](../../../images/extensions/server/amazon/2.png)

- **Entitet-ID**: Ditt enhets-ID (finns i Campaign Manager-portalens URL med entitetsprefix)

![Kampanjhanterarportalen i den vänstra navigeringen.](../../../images/extensions/server/amazon/3.png)

- Välj **Spara**.

Dessa konfigurationsvärden upprättar anslutningen mellan plattformen och ditt [!DNL Amazon]-konto.

### [!DNL Amazon] OAuth 2 {#oauth}

Så här skapar du en [!DNL Amazon] OAuth 2-hemlighet:

- Välj [!DNL Amazon] OAuth2 i listrutan **Type** och välj **Create Secret**.

![Amazon OAuth 2 i listrutan.](../../../images/extensions/server/amazon/Oauth.png)

- Välj **Skapa och auktorisera hemlighet med Amazon** på porten om du vill auktorisera hemligheten manuellt och fortsätta.

![Skapa och auktorisera hemlighet med Amazon markerat.](../../../images/extensions/server/amazon/Oauth.1.png)

- Ange dina [!DNL Amazon]-inloggningsuppgifter i dialogrutan som visas. Följ instruktionerna för att ge händelsevidarebefordringsåtkomst till dina data.

När du är klar ser du din hemlighet med status och förfallodatum på fliken **Hemligheter**.

![Skapade hemlighet på fliken Hemligheter.](../../../images/extensions/server/amazon/Oauth.2.png)

## Konfigurera en regel för vidarebefordran av händelser {#config-rule}

När alla dataelement har konfigurerats kan du skapa regler för vidarebefordran av händelser som avgör när och hur händelser skickas till Amazon.

- Navigera till **Regler** och skapa en ny regel för vidarebefordran av händelser.
- Under **Åtgärder** väljer du **API-tillägg för Amazon-konvertering**.
- Ange **åtgärdstypen** till **Importera konverteringshändelser**.

![Alternativ för åtgärdskonfiguration är markerade.](../../../images/extensions/server/amazon/4.png)

- Konfigurera händelseegenskaperna enligt nedan:

| Indata | Beskrivning |
| --- | --- |
| **Händelsenamn** | Namnet på konverteringshändelsen. |
| **Händelsetyp** | Definierar vilken typ av händelse som spåras (t.ex. inköp, kundvagnstillägg). |
| **Tidsstämpel** | Händelsetid i ISO-format. |
| **Klientborttagnings-ID** | Ett unikt ID för deduplicering. |
| **Matcha nycklar** | Användar- och enhetsidentifierare för attribuering. |
| **Värde** | Evenemangets monetära värde. |
| **Valutakod** | Valuta i ISO-4217-format. |
| **Sålda enheter** | Antal inköpta artiklar. |
| **Landskod** | Land där händelsen inträffade. |
| **Alternativ för databearbetning** | Flaggor för begränsad dataanvändning. |
| **Godkännande** | Anger användarens samtycke för användning av annonsdata. |

- Välj **Behåll ändringar** om du vill spara regeln.

![Händelseparametrar i åtgärdskonfigurationen har markerats tillsammans med knappen för att behålla ändringar.](../../../images/extensions/server/amazon/5.png)

![Ytterligare händelseparametrar i åtgärdskonfigurationen har markerats tillsammans med knappen för att behålla ändringar.](../../../images/extensions/server/amazon/6.png)

## Borttagning av händelser {#deduplication}

Om du använder både [!DNL Amazon] Advertising Tag (AAT) och [!DNL Amazon] Conversion API-tillägget för samma händelser måste du konfigurera deduplicering. Inkludera `clientDedupeId` i varje delad händelse för att säkerställa korrekt borttagning av dubbletter.
Deduplicering behövs inte om klient- och serverhändelser inte överlappar varandra.

Korrekt borttagning av dubbletter förhindrar uppblåsta konverteringsvärden och säkerställer att optimeringsdata förblir korrekta.

Mer information finns i [Amazon-handboken om borttagning av dubbletter](https://advertising.amazon.com/).

## Nästa steg

I den här guiden beskrivs hur du konfigurerar och skickar konverteringshändelser till [!DNL Amazon] med API-tillägget [!DNL Amazon] Conversions. Mer information om funktioner för vidarebefordran av händelser i [!DNL Adobe Experience Platform] finns i [översikten över vidarebefordran av händelser](../../../ui/event-forwarding/overview.md)

Mer information om hur du felsöker implementeringen med verktyget för felsökning och övervakning av händelsevidarebefordran finns i [Adobe Experience Platform Debugger-översikten](https://experienceleague.adobe.com/sv/docs/experience-platform/debugger/home) och [Övervaka aktiviteter](https://experienceleague.adobe.com/sv/docs/experience-platform/tags/event-forwarding/monitoring) i händelsevidarebefordran.