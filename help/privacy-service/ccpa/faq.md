---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Vanliga frågor om CCPA
topic: troubleshooting
translation-type: tm+mt
source-git-commit: 5b32c1955fac4f137ba44e8189376c81cdbbfc40
workflow-type: tm+mt
source-wordcount: '787'
ht-degree: 0%

---


# Vanliga frågor om CCPA

Det här dokumentet innehåller svar på vanliga frågor om [!DNL California Consumer Protection Act] (CCPA) och dess implementering i Adobe Experience Cloud.

## Vad är CCPA?

CCPA ( [!DNL California Consumer Privacy Act] California’s new privacy law) ger sina invånare nya rättigheter när det gäller personuppgifter och ålägger vissa enheter som bedriver verksamhet i Kalifornien dataskydd.

>[!NOTE]
>
>Trots att CCPA är tekniskt effektivt i januari 2020 håller de fortfarande på att finjusteras av beslutsfattarna. Dessutom kommer viktiga detaljer om genomförandet och andra riktlinjer i regler som ännu inte har skrivits av den kaliforniska tillsynsmyndigheten.

Även om CCPA delar vissa begrepp som tillhandahålls enligt EU:s allmänna dataskyddsförordning (GDPR), såsom en individs rätt att få tillgång till och ta bort personuppgifter, finns det flera viktiga sätt som CCPA skiljer sig från GDPR. CCPA ger till exempel konsumenterna en avanmälningsrätt för vissa datadelningsaktiviteter som kvalificerar som&quot;sälja&quot; personuppgifter till en tredje part, i stället för att kräva förhandsgodkännande.

## Vad är definitionen av personuppgifter inom ramen för CCPA?

Personlig information är information&quot;som identifierar, relaterar till, beskriver, kan kopplas till eller rimligen kan kopplas till, direkt eller indirekt, en konsument eller ett hushåll.&quot;

## Vilka typer av personuppgifter eller identifierare som används i Adobe Experience Cloud omfattas av dessa nya krav?

Följande identifierare används ofta i [!DNL Experience Cloud] program och kan vara föremål för CCPA-krav:

- Namn
- Postadress
- Unik personlig identifierare
- Online-ID
- IP-adress
- E-postadress
- Kontonamn

Personlig information kan också omfatta information om internetaktiviteter eller andra aktiviteter i elektroniska nätverk. Detta omfattar, men är inte begränsat till:

- Webbhistorik
- Sökhistorik
- Information om en kunds interaktion med en webbplats, tillämpning eller annons

Även om CCPA omfattar en stor mängd personuppgifter innebär Adobe:s standardavtalsvillkor att känslig personlig information (som SSN, körkortsinformation, ekonomisk kontoinformation och biometriska data) i allmänhet inte får importeras och användas i [!DNL Experience Cloud] ansökningar.

## Hur gäller CCPA:s olika roller och ansvarsområden [!DNL Experience Cloud]?

Enligt CCPA gäller följande roller Adobe och dess kunder:

- Kunder i Adobe (den part som begär att få samla in och använda personuppgifter från personer bosatta i Kalifornien) betraktas som ett **företag**.
- Adobe, i sin roll att tillhandahålla tjänsten, skulle betraktas som en **tjänsteleverantör**.

Med tanke på detta förhållande och Adobe avtalsspråk skulle utlämnande av information till Adobe sannolikt inte betraktas som en&quot;försäljning&quot; som företagen måste meddela och erbjuda en avanmälan för.

Adobe tjänster kan dock användas för att möjliggöra viss datadelning och överföring till tredje part. Dessa överföringar från tredje part kan betraktas som&quot;försäljning&quot; och kräver enligt lag offentliggörande och avanmälan.  Kunderna bör samarbeta med sin juridiska rådgivare för att utvärdera specifika användningsfall för att bedöma tillämpliga krav.

## Hur många dagar måste ett företag svara på en konsumentförfrågan om att få tillgång till eller ta bort personlig information?

Förutsatt att företaget har samlat in personuppgifter och kan autentisera eller verifiera identiteten hos en viss kund i Kalifornien, tillåter CCPA att konsumentförfrågningar kan uppfyllas inom 45 dagar (med några undantag).

## Vad är Adobe under CCPA?

Som tjänsteleverantör samlar Adobe in och behandlar personuppgifter för företagets räkning och är enligt avtal bundet att använda dessa uppgifter endast för de särskilda ändamål som anges i avtalet.

Med tanke på detta förhållande och Adobe avtalsspråk omfattas information till Adobe av lagens bestämmelser om tjänsteleverantörer, och skulle sannolikt inte betraktas som en&quot;försäljning&quot; som företagen skulle behöva meddela och erbjuda en avanmälan för.

Adobe kan användas för att möjliggöra viss datadelning och överföring till tredje part. Dessa överföringar från tredje part kan betraktas som&quot;försäljning&quot; och kräver enligt lag offentliggörande och avanmälan.  Kunderna bör samarbeta med sin juridiska rådgivare för att utvärdera specifika användningsfall för att bedöma tillämpliga krav.

## Hur kan jag stödja konsumentsekretesskrav enligt CCPA om jag upprätthåller vissa typer av data som omfattas av kraven?

När du har vidtagit de åtgärder som krävs för att autentisera CA-konsumenter kan du med Adobe Experience Platform [!DNL Privacy Service] skicka förfrågningar om konsumentintegritet till kompatibla [!DNL Experience Cloud] program. Mer information finns i översikten över [](../home.md) Privacy Servicen. Mer information om hur dina [!DNL Experience Cloud] program kan uppfylla sekretesskrav finns i handboken om [Privacy Service och Experience Cloud-program](../experience-cloud-apps.md).

>[!NOTE]
>
>Ytterligare vägledning från den kaliforniska tillsynsmyndigheten ges fortfarande om vilka typer av uppgifter som kan omfattas av konsumentsekretesskrav.

## Erbjuder Adobe andra verktyg som kan vara till hjälp för att tillgodose CCPA-kraven?

Adobe Experience Cloud-programmen har funktioner för datahantering och styrning som kan vara till hjälp för företagens integritetsbehov. Bland dessa verktyg finns etikettering av dataanvändning, rollbaserade åtkomstkontroller, IP-förfalskning och hash-funktioner.

Adobe har fått olika certifieringar av sin sekretess- och säkerhetspraxis, till exempel en ISO 27001-certifiering och en TrustArc GDPR-validering.