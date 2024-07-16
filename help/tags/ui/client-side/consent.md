---
title: Distribuera JavaScript-taggar för att hantera kundgodkännande
description: Lär dig hur du hanterar kundernas anmälan och avanmälningssignaler för olika Adobe-lösningar i Adobe Experience Platform.
exl-id: 7762c42f-71c8-4f29-a96b-c6c04b838a91
source-git-commit: 3bb0fc7b2807889d0a759e81c8ff728de3c0cbde
workflow-type: tm+mt
source-wordcount: '609'
ht-degree: 0%

---

# Distribuera JavaScript-taggar för att hantera kundgodkännande

>[!NOTE]
>
>Adobe Experience Platform Launch har omklassificerats som en serie datainsamlingstekniker i Adobe Experience Platform. Som ett resultat av detta har flera terminologiska förändringar införts i produktdokumentationen. I följande [dokument](../../term-updates.md) finns en konsoliderad referens till de ändrade terminologin.

Lagliga sekretessbestämmelser som den allmänna dataskyddsförordningen (GDPR) kräver att företag kan hantera sitt samtycke för sina användare. Adobe kunder kan kräva att besökarna anmäler sig innan Adobe lösningar kan köras för en viss besökare. Besökarna bör ha möjlighet att hantera sin status för anmälan och avanmälan.

Adobe Experience Cloud-kunder behöver en mängd olika implementeringar av dessa krav. En del använder sig av samverkansansvariga på företagsnivå och andra bygger sina egna.

Adobe Experience Platform tilläggsutvecklare använder tillägg och regelbyggaren för att definiera lösningar för anmälan och avanmälan.

Det här dokumentet innehåller information om hur du förhindrar att Adobe-taggar avfyras tills du har fått samtycke.

## Advertising Cloud

Adobe Experience Platform utlöser inte [!DNL Advertising Cloud] automatiskt. [!DNL Advertising Cloud] aktiveras bara om du särskilt anger det i en regelåtgärd. Använd regelvillkoren för att avgöra när och vad som ska utlösas. Om du till exempel vill använda cookies för att bestämma anmälningsstatus, anger du ett dataelement som ska läsa den cookien och använder den som ett villkor i regeln för att avgöra när spårkonverteringsåtgärden ska utlösas.

Integreringar med medverkandehanterare (som OneTrust) kan ange och spåra cookies för kunder, som sedan kan användas i regelbyggaren.

## Analytics 

Kontrollera att följande är *inte* markerade i delen Länkspårning i konfigurationsinställningarna för tillägget [!DNL Analytics]:

* Spåra nedladdningslänkar
* Spåra utgående länkar

När de här inställningarna inte har valts utlöses inte [!DNL Adobe Analytics] automatiskt av plattformen. [!DNL Analytics] utlöses bara om du särskilt anger det i en regelåtgärd. Använd regelvillkoren för att avgöra när och vad som ska utlösas. Om du till exempel vill använda cookies för att bestämma anmälningsstatus anger du ett dataelement som ska läsa den cookien och använder den som ett villkor i regeln för att avgöra när åtgärden Skicka Beacon ska utlösas.

Separat kan du överväga att använda objektet [Adobe för anmälan](https://experienceleague.adobe.com/docs/id-service/using/implementation/opt-in-service/optin-overview.html) för att styra aktiveringen av den här taggen i kombination med din plattform för samtyckeshantering.

Integreringar med medverkandehanterare (som OneTrust) kan ange och spåra cookies för kunder, som sedan kan användas i regelbyggaren.

## Audience Manager

DIL är för närvarande inställt på att avfyras automatiskt om det placeras på en kundsida. Använd objektet [Adobe för anmälan](https://experienceleague.adobe.com/docs/id-service/using/implementation/opt-in-service/optin-overview.html) för att styra taggens start tillsammans med din plattform för samtyckeshantering.

[!DNL Adobe] rekommenderar att du använder vidarebefordran på serversidan i [!DNL Analytics].

## EXPERIENCE CLOUD ID

[!DNL Experience Cloud ID] aktiveras automatiskt om det placeras på en kundsida.

Använd objektet [Adobe för anmälan](https://experienceleague.adobe.com/docs/id-service/using/implementation/opt-in-service/optin-overview.html) för att styra taggens start tillsammans med din plattform för samtyckeshantering.

## Target

Adobe Experience Platform utlöser inte [!DNL Target] automatiskt. [!DNL Target] utlöses bara om du särskilt anger det i en regelåtgärd. Använd regelvillkoren för att avgöra när och vad som ska utlösas. Om du till exempel vill använda cookies för att bestämma anmälningsstatus, anger du ett dataelement som ska läsa den cookien och använder den som ett villkor i regeln för att avgöra när inläsningsåtgärden [!DNL Target] ska utlösas.

Separat kan du överväga att använda objektet [Adobe för anmälan](https://experienceleague.adobe.com/docs/id-service/using/implementation/opt-in-service/optin-overview.html) för att styra aktiveringen av den här taggen i kombination med din plattform för samtyckeshantering.

Integreringar med medverkandehanterare (som OneTrust) kan ange och spåra cookies för kunder, som sedan kan användas i regelbyggaren.
