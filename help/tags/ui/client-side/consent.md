---
title: Distribuera JavaScript-taggar för att hantera kundgodkännande
description: Lär dig hur du hanterar kundernas anmälan och avanmälningssignaler för olika Adobe-lösningar i Adobe Experience Platform.
exl-id: 7762c42f-71c8-4f29-a96b-c6c04b838a91
source-git-commit: 44e2b8241a8c348d155df3061d398c4fa43adcea
workflow-type: tm+mt
source-wordcount: '565'
ht-degree: 0%

---

# Distribuera JavaScript-taggar för att hantera kundgodkännande

Lagliga sekretessbestämmelser som den allmänna dataskyddsförordningen (GDPR) kräver att företag kan hantera sitt samtycke för sina användare. Adobe kunder kan kräva att besökarna anmäler sig innan Adobe lösningar kan köras för en viss besökare. Besökarna bör ha möjlighet att hantera sin status för anmälan och avanmälan.

Adobe Experience Cloud-kunder behöver en mängd olika implementeringar av dessa krav. En del använder sig av samverkansansvariga på företagsnivå och andra bygger sina egna.

Adobe Experience Platform tilläggsutvecklare använder tillägg och regelbyggaren för att definiera lösningar för anmälan och avanmälan.

Det här dokumentet innehåller information om hur du förhindrar att Adobe-taggar aktiveras tills du har fått samtycke.

## Advertising Cloud

Adobe Experience Platform utlöser inte [!DNL Advertising Cloud] automatiskt. [!DNL Advertising Cloud] aktiveras bara om du särskilt anger det i en regelåtgärd. Använd regelvillkoren för att avgöra när och vad som ska utlösas. Om du till exempel vill använda cookies för att bestämma anmälningsstatus, anger du ett dataelement som ska läsa den cookien och använder den som ett villkor i regeln för att avgöra när spårkonverteringsåtgärden ska utlösas.

Integreringar med medverkandehanterare (som OneTrust) kan ange och spåra cookies för kunder, som sedan kan användas i regelbyggaren.

## Analytics 

Kontrollera att följande är [!DNL Analytics]inte *markerade i delen Länkspårning i konfigurationsinställningarna för tillägget*:

* Spåra nedladdningslänkar
* Spåra utgående länkar

När de här inställningarna inte har valts utlöses inte [!DNL Adobe Analytics] automatiskt av Experience Platform. [!DNL Analytics] utlöses bara om du särskilt anger det i en regelåtgärd. Använd regelvillkoren för att avgöra när och vad som ska utlösas. Om du till exempel vill använda cookies för att bestämma anmälningsstatus anger du ett dataelement som ska läsa den cookien och använder den som ett villkor i regeln för att avgöra när åtgärden Skicka Beacon ska utlösas.

Separat kan du överväga att använda [Adobe-objektet för anmälan](https://experienceleague.adobe.com/docs/id-service/using/implementation/opt-in-service/optin-overview.html?lang=sv-SE) för att styra aktiveringen av den här taggen i kombination med din plattform för samtyckeshantering.

Integreringar med medverkandehanterare (som OneTrust) kan ange och spåra cookies för kunder, som sedan kan användas i regelbyggaren.

## Audience Manager

DIL är för närvarande inställt på att aktiveras automatiskt om det placeras på en kundsida. Överväg att använda [Adobe-avanmälningsobjekt](https://experienceleague.adobe.com/docs/id-service/using/implementation/opt-in-service/optin-overview.html?lang=sv-SE) för att styra taggens aktivering i kombination med din plattform för samtyckeshantering.

[!DNL Adobe] rekommenderar att du använder vidarebefordran på serversidan i [!DNL Analytics].

## EXPERIENCE CLOUD ID

[!DNL Experience Cloud ID] aktiveras automatiskt om det placeras på en kundsida.

Överväg att använda [Adobe-avanmälningsobjekt](https://experienceleague.adobe.com/docs/id-service/using/implementation/opt-in-service/optin-overview.html?lang=sv-SE) för att styra taggens aktivering i kombination med din plattform för samtyckeshantering.

## Target

Adobe Experience Platform utlöser inte [!DNL Target] automatiskt. [!DNL Target] utlöses bara om du särskilt anger det i en regelåtgärd. Använd regelvillkoren för att avgöra när och vad som ska utlösas. Om du till exempel vill använda cookies för att bestämma anmälningsstatus, anger du ett dataelement som ska läsa den cookien och använder den som ett villkor i regeln för att avgöra när inläsningsåtgärden [!DNL Target] ska utlösas.

Separat kan du överväga att använda [Adobe-objektet för anmälan](https://experienceleague.adobe.com/docs/id-service/using/implementation/opt-in-service/optin-overview.html?lang=sv-SE) för att styra aktiveringen av den här taggen i kombination med din plattform för samtyckeshantering.

Integreringar med medverkandehanterare (som OneTrust) kan ange och spåra cookies för kunder, som sedan kan användas i regelbyggaren.
