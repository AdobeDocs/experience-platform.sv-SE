---
title: Använda Adobe Experience Platform Assurance
description: I den här guiden beskrivs hur du använder Adobe Experience Platform Assurance när det har installerats och implementerats.
exl-id: 872c83d1-82e8-40d8-9b66-3e51a91a955f
source-git-commit: f8576e7f7e1da7351f7860cba27d5d09d0161132
workflow-type: tm+mt
source-wordcount: '674'
ht-degree: 0%

---

# Använda Adobe Experience Platform Assurance

I den här självstudiekursen beskrivs hur du använder Adobe Experience Platform Assurance. Instruktioner om hur du installerar och implementerar Adobe Experience Platform Assurance-tillägget finns i självstudiekursen [Implementera Assurance-tillägget](./implement-assurance.md).

## Skapa sessioner

När du har loggat in på [Assurance-gränssnittet](https://experience.adobe.com/assurance) kan du välja **[!UICONTROL Create Session]** för att börja skapa en session.

![Knappen för att skapa session är markerad och visar var du kan skapa en session.](./images/using-assurance/create-session.png)

Dialogrutan **[!UICONTROL Create New Session]** visas med två alternativ för att skapa en session:

### Koppling till djup länk

Välj det här alternativet om du vill generera en unik sessions-URL, QR-kod och PIN-kod. Skanna QR-koden eller öppna sessionslänken i appen manuellt och ange PIN-koden för att upprätta anslutningen.

Välj **[!UICONTROL Deep link connect]** och fortsätt genom att välja **[!UICONTROL Start]**.

![Dialogrutan Skapa ny session visar alternativet för anslutning av djuplänk markerat.](./images/using-assurance/create-new-session-deep-link.png)

Du kan nu ange ett namn som identifierar sessionen och sedan ange en **[!UICONTROL Base URL]** (djuplänknings-URL för din app). Välj **[!UICONTROL Next]** när du har angett dessa uppgifter.

>[!INFO]
>
>Bas-URL är rotdefinitionen som används för att starta programmet från en URL. En sessions-URL skapas som du kan använda för att starta Assurance-sessionen. Ett exempelvärde kan se ut så här: `myapp://default` I fältet **[!UICONTROL Base URL]** skriver du appens grundläggande djuplänksdefinition.

![Indatafälten för sessionsnamn och bas-URL visas.](./images/using-assurance/create-session-form-deep-link.png)

### Snabb anslutning

Utlös en anslutning från appen så visas enheten i en lista över tillgängliga enheter. Välj **[!UICONTROL Quick connect]** om du vill skapa Assurance-sessionen.

#### Förhandskrav

Innan du använder Quick Connect bör du kontrollera att appen har de SDK-versioner och implementeringar som krävs:

**Krav för Android SDK:**

- Mobile Core v3.1.0 eller senare
- Adobe Journey Optimizer v3.1.0 eller senare
- Adobe Experience Platform Assurance v3.0.4 eller senare

**Krav för iOS SDK:**

- Mobile Core v5.2.0 eller senare
- Adobe Journey Optimizer v5.1.1 eller senare
- Adobe Experience Platform Assurance v5.0.0 eller senare

**Implementering:**

Ditt program måste implementera [`startSession` API ](https://developer.adobe.com/client-sdks/home/base/assurance/api-reference/#startsession-quick-connect) för att utlösa Assurance-anslutningen. Detta API-anrop ingår vanligtvis i en åtgärdsuppsättning eller aktiveras i din app.

#### Skapa en snabbanslutningssession

![Dialogrutan Skapa ny session visar alternativet Snabbanslutning markerat.](./images/using-assurance/create-new-session-quick-connect.png)

Välj **[!UICONTROL Quick connect]** och fortsätt genom att välja **[!UICONTROL Start]**. Du ser gränssnittet för enhetsväljaren:

1. **Utlös Assurance-anslutningen** - I mobilappen eller implementeringen utlöser du åtgärden som initierar Assurance-anslutningen med API:t `startSession`. Detta gör att din enhet kan upptäckas.

2. **Markera och anslut enheten** - När enheten visas i listan över tillgängliga enheter markerar du den och klickar på **[!UICONTROL Connect]**.

![Enhetsväljargränssnittet för Snabbanslutning visar tillgängliga enheter.](./images/using-assurance/quick-connect-device-picker.png)

## Anslut till en session

Vilka steg du ska ansluta beror på vilken sessionstyp du använder:

### Anslutningssessioner med djupgående länkar

För sessioner som skapats med **[!UICONTROL Deep Link Connect]**:

1. Navigera till sidan med sessionsinformation (för befintliga sessioner) eller fortsätt från att skapa sessionen för att se länken, QR-koden och PIN-koden
2. Använd enhetens kameraapp för att skanna QR-koden, eller kopiera länken och öppna den i din app
3. När appen startas visas skärmen för PIN-koden. Ange PIN-koden och tryck på **[!UICONTROL Connect]**

![En dialogruta med alternativ för att ansluta till din Assurance-session visas.](./images/using-assurance/deep-link-connection.png)

### Snabbanslutningssessioner

För sessioner som skapats med **[!UICONTROL Quick Connect]** (identifierbara av en sessions-URL som börjar med `adobeassurance://`) sker anslutningen automatiskt via enhetens väljargränssnitt:

1. Navigera till sidan med sessionsinformation (för befintliga sessioner) eller fortsätt från att skapa sessionen
2. I avsnittet **[!UICONTROL Connect Device]** visas enhetsväljargränssnittet
3. Utlös de funktionsmakron som finns i appen så att enheten kan identifieras
4. Välj din enhet i listan och klicka på **[!UICONTROL Connect]**

![Enhetens väljargränssnitt visar tillgängliga enheter att ansluta till.](./images/using-assurance/quick-connect-device-picker.png)

### Verifierar anslutning

Du kan verifiera att din app är ansluten till Assurance när Adobe Experience Platform-ikonen (röd Adobe &quot;A&quot;) visas i din app.

## Exportera en session

Om du vill exportera en Assurance-session väljer du **[!UICONTROL Export to JSON]** i en session på sidan med sessionsinformation för din app:

![Exporterar en session](./images/using-assurance/export-session.png)

Exportalternativet respekterar sökfilterresultat och exporterar endast händelser som visas i händelseläget. Om du till exempel sökte efter &quot;track&quot;-händelser och sedan väljer **[!UICONTROL Export to JSON]** exporteras bara &quot;track&quot;-händelseresultatet.