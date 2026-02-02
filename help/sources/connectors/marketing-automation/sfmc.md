---
title: Salesforce Marketing Cloud (V2) Source - översikt
description: Lär dig hur du ansluter Salesforce Marketing Cloud (V2) till Adobe Experience Platform med hjälp av API:er eller användargränssnittet.
last-substantial-update: 2025-02-02T00:00:00Z
source-git-commit: 4d47eae91711596677335b03568add9f6fbade74
workflow-type: tm+mt
source-wordcount: '1014'
ht-degree: 0%

---

# Översikt över källan [!DNL Salesforce Marketing Cloud] (V2)

>[!IMPORTANT]
>
>Den ursprungliga källan [[!DNL Salesforce Marketing Cloud] (V1)](salesforce-marketing-cloud.md) har tagits bort från januari 2026. Det finns inga tillgängliga migreringar för den här inaktuella källan och du måste implementera dina data igen med den nya [!DNL Salesforce Marketing Cloud] (V2)-källan.

Integrationen mellan Adobe [Real-Time CDP](../../../rtcdp/overview.md) och [!DNL Salesforce Marketing Cloud] är utformad för att utnyttja datatillägg på grund av den flexibilitet och kontroll de ger. Till skillnad från standardsystemtabeller (datavyer och inbyggda objekt), som är begränsade till fördefinierade fält och främst används för spårning på systemnivå, kan du använda datatillägg för att definiera anpassade fält, ordna en mängd olika företagsspecifika data och anpassa dina datastrukturer för att uppfylla unika krav.

På grund av den här anpassningsnivån och skalbarheten är integrationen mellan Real-Time CDP och [!DNL Salesforce Marketing Cloud] beroende av datatillägg snarare än standardsystemtabeller. Den här metoden erbjuder en flexiblare, skalbar och integrerad grund för datahantering, vilket säkerställer att den är anpassad till era affärsmål

Du kan använda källan [!DNL Salesforce Marketing Cloud] för att ansluta ditt [!DNL Salesforce Marketing Cloud]-konto till Real-Time CDP och Adobe Experience Platform. Läs dokumentationen nedan för att lära dig hur du kommer igång.

## Använd exempel på exempel {#use-case-examples}

### Anpassa e-postkampanjer med kontaktdata

Ett varumärke inom detaljhandeln vill personalisera e-postkampanjer baserat på kundens livscykler (t.ex. nya kunder, återkommande köpare, lojala kunder). För att göra detta skapar de ett kontaktdatatillägg för att lagra viktig kundinformation, inklusive namn, e-postadress, livscykelstadium och köpbeteende. Dessa data importeras sedan till Experience Platform för mer detaljerad segmentering och målinriktning.

Genom att importera data från kontaktdatatillägget till Experience Platform kan varumärket segmentera kunderna baserat på deras livscykelstadium och köpbeteende. De kan till exempel skicka ett välkomsterbjudande till nya kunder, en lojalitetsbelöning till återkommande köpare eller till och med återengagera inaktiva kunder med riktade erbjudanden. Detta tillvägagångssätt säkerställer personaliserad kommunikation och möjliggör mer relevant och effektivt kundengagemang.

### Insamlade kampanjdata för anpassad segmentering

Ett marknadsföringsteam vill optimera sina e-postkampanjer genom att inrikta sig på kunder baserat på deras engagemang med tidigare kampanjer. För att göra detta skapar de ett Campaign Data Extension i [!DNL Salesforce Marketing Cloud] för att lagra kundinteraktionsdata, som e-postöppningar, klick och kampanjsvar. Dessa data importeras sedan till Experience Platform för ytterligare segmentering och personalisering.

Genom att importera dessa data från Campaign Data Extension till Experience Platform kan marknadsföringsteamet segmentera kunder baserat på tidigare engagemang, t.ex. de som klickade på produkterbjudanden eller reagerade positivt. Kunder som har engagerat sig kan få riktade kampanjer i framtida e-postmeddelanden, medan de som har svarat negativt kan få uppföljning av kundtjänst. Tack vare integreringen med Experience Platform kan marknadsföringsteamet leverera mer personaliserat och relevant innehåll baserat på kundbeteende.

### Målinrikta kunder baserat på aktivitetsdata

Ett marknadsföringsteam vill inrikta sig på kunderna baserat på deras aktiviteter, som webbplatsbesök, inskickade formulär eller interaktioner med tidigare e-postkampanjer. För att uppnå detta skapar de ett aktivitetsdatatillägg för att lagra information om varje kunds engagemangsaktiviteter. Dessa data hämtas sedan in i Experience Platform för ytterligare segmentering och personaliserad kampanjanpassning.

Genom att importera data från aktivitetsdatatillägget till Experience Platform kan marknadsföringsteamet segmentera kunder utifrån deras engagemangshistorik. Till exempel kan kunder som nyligen besökt webbplatsen men inte slutfört ett köp få påminnelser via e-post med specialerbjudanden. På samma sätt kan kunder som fyller i ett formulär få personliga uppföljningar. Detta tillvägagångssätt garanterar att varje kund får relevant innehåll baserat på deras senaste aktiviteter, vilket förbättrar engagemanget och konverteringsgraden.

## Förhandskrav {#prerequisites}

I avsnitten nedan finns information om vilka krav som måste uppfyllas innan du kan ansluta källan till Experience Platform.

### Konfigurera autentiseringsprogram {#set-up-application-for-authentication}

När du skapar en integrering med [!DNL Salesforce Marketing Cloud] är ett av de första stegen att skapa ett **installerat paket** i [!DNL Salesforce Marketing Cloud]. Det installerade paketet genererar de klientautentiseringsuppgifter som krävs för att autentisera API-anrop, definierar integreringstypen och associerade behörighetsomfattningar. Dessutom innehåller det installerade paketet rätt API-slutpunkter för din klientorganisation. Det fungerar också som en hanterad behållare för att administrera, övervaka och återkalla åtkomst, vilket säkerställer att alla integreringar är säkra, spårbara och anpassade till Salesforce rekommenderade autentiseringsmodell.

Om du vill skapa ett installerat paket använder du [!DNL Salesforce Marketing Cloud]-gränssnittet och går till **[!DNL Setup]** > **[!DNL Apps]** > **[!DNL Installed Packages]** och väljer sedan **[!DNL New]**. Använd gränssnittet [!DNL New Package Details] för att ange ett namn och information för ditt paket. När du är klar väljer du **[!DNL Save]**.

![Det nya paketgränssnittet för Salesforce Marketing Cloud-gränssnittet.](../../images/tutorials/create/sfmc/new-package.png)

När det nya paketet har skapats väljer du **[!DNL Add Component]**.

![Gränssnittet Lägg till komponent i användargränssnittet för Salesforce Marketing Cloud.](../../images/tutorials/create/sfmc/add-component.png)

Välj **[!DNL API Integration]** som komponenttyp.

![Fönstret för komponentval med &quot;API-integrering&quot; markerat.](../../images/tutorials/create/sfmc/api-integration.png)

Välj **[!DNL Server-to-Server]** som integrationstyp.

![Markeringsfönstret för integreringstyp](../../images/tutorials/create/sfmc/server-to-server.png)

Navigera till **[!DNL Scope]** > **[!DNL Data]**. Välj **[!DNL Data Extensions]** under **[!DNL Read]**.

![Avsnittet med datatillägg i scopet i Salesforce Marketing](../../images/tutorials/create/sfmc/data-extensions.png)

Välj **[!DNL Save]** och kopiera och spara sedan din **klienthemlighet**. När du är klar väljer du **[!DNL Finish]**.

![Salesforce Marketing Cloud-fönstret för att generera en klienthemlighet.](../../images/tutorials/create/sfmc/generate-secret.png)

Innan du lämnar användargränssnittet för [!DNL Salesforce Marketing Cloud] kopierar du **klient-ID** och **unikt bas-URI-prefix** eftersom du använder båda värdena för att skapa en anslutning till Experience Platform. Kontrollera att du tar bort allt efter `.auth.marketingcloudapis.com/` för autentiseringsbasens URI

![Komponentgränssnittet i Salesforce Marketing Cloud där klient-ID och unik bas-URI kan hämtas.](../../images/tutorials/create/sfmc/client-id-and-uri.png)

Mer information om hur du skapar ett installerat paket finns i [[!DNL Salesforce] dokumentationen](https://trailhead.salesforce.com/content/learn/modules/marketing-cloud-developer-basics/set-up-your-developer-environment).

### Samla in nödvändiga inloggningsuppgifter {#gather-required-credentials}

Du måste ange värden för följande autentiseringsuppgifter för att kunna ansluta [!DNL Salesforce Marketing Cloud] till Experience Platform.

| Autentiseringsuppgifter | Beskrivning |
| --- | --- |
| Klient-ID | Den offentligt exponerade identifierare som används av [!DNL Salesforce Marketing Cloud] för att identifiera ditt konto vid auktorisering till Experience Platform. Klient-ID kan hämtas från komponentpanelen i användargränssnittet för [!DNL Salesforce Marketing Cloud]. |
| Klienthemlighet | Den konfidentiella nyckeln som bara är känd för klientprogrammet och auktoriseringsservern. Du kan generera din klienthemlighet genom att följa anvisningarna för [konfiguration av program som beskrivs ovan](#set-up-application-for-authentication). |
| Basslutpunkt | Prefixet för din autentiseringsbas-URI för [!DNL Salesforce Marketing Cloud]. |

{style="table-layout:auto"}

## Anslut [!DNL Salesforce Marketing Cloud] till Experience Platform

Fortsätt med att konfigurera [!DNL Salesforce Marketing Cloud]-källanslutningen i Experience Platform. En steg-för-steg-guide om hur du konfigurerar anslutningen via användargränssnittet finns i [självstudiekursen här](../../tutorials/ui/create/marketing-automation/sfmc.md). Läs den här självstudiekursen om du vill lära dig att ansluta ditt [!DNL Salesforce Marketing Cloud]-konto, välja data, mappningsfält, schemalägga ingivelser och övervaka dina dataflöden.
