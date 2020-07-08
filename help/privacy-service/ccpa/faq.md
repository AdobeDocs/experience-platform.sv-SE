---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Vanliga frågor om CCPA
topic: troubleshooting
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '807'
ht-degree: 0%

---


# Vanliga frågor om CCPA

Det här dokumentet innehåller svar på vanliga frågor om California Consumer Protection Act (CCPA) och dess implementering i Adobe Experience Cloud.

## Vad är CCPA?

California Consumer Privacy Act (CCPA) är Kaliforniens nya integritetslag som ger sina invånare nya rättigheter när det gäller deras personuppgifter och ålägger dataskyddsansvar för vissa enheter som bedriver verksamhet i Kalifornien.

>[!NOTE]
>
>Trots att CCPA är tekniskt effektivt i januari 2020 håller de fortfarande på att finjusteras av beslutsfattarna. Dessutom kommer viktiga detaljer om genomförandet och andra riktlinjer i regler som ännu inte har skrivits av den kaliforniska tillsynsmyndigheten.

Även om CCPA delar vissa begrepp som tillhandahålls enligt EU:s allmänna dataskyddsförordning (GDPR), såsom en individs rätt att få tillgång till och ta bort personuppgifter, finns det flera viktiga sätt som CCPA skiljer sig från GDPR. CCPA ger till exempel konsumenterna en avanmälningsrätt för vissa datadelningsaktiviteter som kvalificerar som&quot;sälja&quot; personuppgifter till en tredje part, i stället för att kräva förhandsgodkännande.

## Vad är definitionen av personuppgifter inom ramen för CCPA?

Personlig information är information&quot;som identifierar, relaterar till, beskriver, kan kopplas till eller rimligen kan kopplas till, direkt eller indirekt, en konsument eller ett hushåll.&quot;

## Vilka typer av personuppgifter eller identifierare som används i Adobe Experience Cloud omfattas av dessa nya krav?

Följande identifierare används ofta i Experience Cloud och kan omfattas av CCPA-kraven:

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

Även om CCPA omfattar en mängd personuppgifter innebär Adobes standardavtalsvillkor att känslig personlig information (som SSN, information om körkort, ekonomisk kontoinformation och biometriska data) i allmänhet inte får importeras och användas i Experience Cloud.

## Hur gäller CCPA:s olika roller och ansvarsområden för Experience Cloud?

Enligt CCPA gäller följande roller Adobe och dess kunder:

- Adobes kunder (den part som begär in och använder personuppgifter från personer bosatta i Kalifornien) betraktas som ett **företag**.
- Adobe, som i sin roll att tillhandahålla tjänsten, betraktas som en **tjänsteleverantör**.

Med tanke på denna relation och Adobes avtalsspråk skulle utlämnande av information till Adobe sannolikt inte betraktas som en&quot;försäljning&quot; som företagen måste meddela och erbjuda en avanmälan för.

Adobes tjänster kan dock användas för att möjliggöra viss datadelning och överföring till tredje part. Dessa överföringar från tredje part kan betraktas som&quot;försäljning&quot; och kräver enligt lag offentliggörande och avanmälan.  Kunderna bör samarbeta med sin juridiska rådgivare för att utvärdera specifika användningsfall för att bedöma tillämpliga krav.

## Hur många dagar måste ett företag svara på en konsumentförfrågan om att få tillgång till eller ta bort personlig information?

Förutsatt att företaget har samlat in personuppgifter och kan autentisera eller verifiera identiteten hos en viss kund i Kalifornien, tillåter CCPA att konsumentförfrågningar kan uppfyllas inom 45 dagar (med några undantag).

## Vilken är Adobes roll under CCPA?

Som tjänsteleverantör samlar Adobe in och behandlar personuppgifter för företagets räkning och är enligt avtal bundet att använda dessa uppgifter endast för de särskilda ändamål som anges i avtalet.

Med tanke på detta förhållande och Adobes avtalsspråk omfattas information till Adobe av lagens bestämmelser för tjänsteleverantörer och anses sannolikt inte vara en&quot;försäljning&quot; som företag måste meddela och erbjuda en avanmälan för.

Adobes tjänster kan användas för att möjliggöra viss datadelning och överföring till tredje part. Dessa överföringar från tredje part kan betraktas som&quot;försäljning&quot; och kräver enligt lag offentliggörande och avanmälan.  Kunderna bör samarbeta med sin juridiska rådgivare för att utvärdera specifika användningsfall för att bedöma tillämpliga krav.

## Hur kan jag stödja konsumentsekretesskrav enligt CCPA om jag upprätthåller vissa typer av data som omfattas av kraven?

När du har vidtagit de åtgärder som krävs för att autentisera CA-konsumenter kan du med Adobe Experience Platform Privacy Service skicka förfrågningar om konsumentintegritet till kompatibla Experience Cloud-program. Mer information finns i översikten över [](../home.md) Privacy Servicen. Mer information om hur dina Experience Cloud-program kan uppfylla sekretesskrav finns i handboken om [Privacy Service- och Experience Cloud-program](../experience-cloud-apps.md).

>[!NOTE]
>
>Ytterligare vägledning från den kaliforniska tillsynsmyndigheten ges fortfarande om vilka typer av uppgifter som kan omfattas av konsumentsekretesskrav.

## Erbjuder Adobe andra verktyg som kan vara till hjälp för att tillgodose CCPA-kraven?

Adobe Experience Cloud-programmen har funktioner för datahantering och styrning som kan vara till hjälp för företagens sekretessbehov. Bland dessa verktyg finns etikettering av dataanvändning, rollbaserade åtkomstkontroller, IP-förfalskning och hash-funktioner.

Adobe har fått olika certifieringar av sin sekretess- och säkerhetspraxis, till exempel en ISO 27001-certifiering och en TrustArc GDPR-validering.