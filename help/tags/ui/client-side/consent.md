---
title: Distribuera JavaScript-taggar för att hantera kundgodkännande
description: Lär dig hur du hanterar kundernas anmälan och avanmälningssignaler för olika Adobe-lösningar i Adobe Experience Platform.
source-git-commit: 39d9468e5d512c75c9d540fa5d2bcba4967e2881
workflow-type: tm+mt
source-wordcount: '650'
ht-degree: 0%

---

# Distribuera JavaScript-taggar för att hantera kundernas samtycke

>[!NOTE]
>
>Adobe Experience Platform Launch omdöms till en serie datainsamlingstekniker i Experience Platform. Som ett resultat av detta har flera terminologiska förändringar införts i produktdokumentationen. Se följande [dokument](../../term-updates.md) för en konsoliderad referens till terminologiska ändringar.

Kombinationen av EU:s [allmänna dataskyddsförordning (GDPR)](https://gdpr-info.eu/art-7-gdpr/) och [ePrivacy](https://medium.com/mydata/consent-lost-gdpr-and-found-eprivacy-e85cf881ffb)-lagstiftning kräver att företagen kan hantera användarnas samtycke. Adobe kunder kan kräva att besökarna anmäler sig innan Adobe lösningar kan köras för en viss besökare. Besökarna bör kunna hantera sin status för anmälan och avanmälan.

Adobe Experience Cloud-kunder behöver en mängd olika implementeringar av dessa krav. En del använder sig av samverkansansvariga på företagsnivå och andra bygger sina egna.

Adobe Experience Platform tilläggsutvecklare använder tillägg och regelbyggaren för att definiera lösningar för anmälan och avanmälan.

Det här dokumentet innehåller information om hur du förhindrar att Adobe-taggar avfyras tills du har fått samtycke.

## Advertising Cloud

Adobe Experience Platform utlöser inte [!DNL Advertising Cloud] automatiskt. [!DNL Advertising Cloud] aktiveras bara om du uttryckligen säger det i en regelåtgärd. Använd regelvillkoren för att avgöra när och vad som ska utlösas. Om du till exempel vill använda cookies för att bestämma anmälningsstatus, anger du ett dataelement som ska läsa den cookien och använder den som ett villkor i regeln för att avgöra när spårkonverteringsåtgärden ska utlösas.

Integreringar med medverkandehanterare (som OneTrust) kan ange och spåra cookies för kunder, som sedan kan användas i regelbyggaren.

## Analytics 

Kontrollera att *inte* är markerat i delen Länkspårning i konfigurationsinställningarna för tillägget [!DNL Analytics]:

* Spåra nedladdningslänkar
* Spåra utgående länkar

När de här inställningarna inte har valts utlöses inte [!DNL Adobe Analytics] automatiskt av plattformen. [!DNL Analytics] utlöses bara om du uttryckligen säger det i en regelåtgärd. Använd regelvillkoren för att avgöra när och vad som ska utlösas. Om du till exempel vill använda cookies för att bestämma anmälningsstatus anger du ett dataelement som ska läsa den cookien och använder den som ett villkor i regeln för att avgöra när åtgärden Skicka Beacon ska utlösas.

Separat kan du överväga att använda [Adobe-objektet](https://experienceleague.adobe.com/docs/id-service/using/implementation/opt-in-service/optin-overview.html) för att styra taggens aktivering i kombination med din samtyckeshanteringsplattform.

Integreringar med medverkandehanterare (som OneTrust) kan ange och spåra cookies för kunder, som sedan kan användas i regelbyggaren.

## Audience Manager

DIL är för närvarande inställt på att avfyras automatiskt om det placeras på en kundsida. Överväg att använda [Adobe opt-in-objektet](https://experienceleague.adobe.com/docs/id-service/using/implementation/opt-in-service/optin-overview.html) för att styra taggens aktivering tillsammans med din samtyckeshanteringsplattform.

[!DNL Adobe] rekommenderar att du använder vidarebefordran på serversidan i  [!DNL Analytics].

## Experience Cloud ID

[!DNL Experience Cloud ID] aktiveras automatiskt om det placeras på en kundsida.

Överväg att använda [Adobe opt-in-objektet](https://experienceleague.adobe.com/docs/id-service/using/implementation/opt-in-service/optin-overview.html) för att styra taggens aktivering tillsammans med din samtyckeshanteringsplattform.

## Målgrupp

Adobe Experience Platform utlöser inte [!DNL Target] automatiskt. [!DNL Target] utlöses bara om du uttryckligen säger det i en regelåtgärd. Använd regelvillkoren för att avgöra när och vad som ska utlösas. Om du till exempel vill använda cookies för att bestämma anmälningsstatus, anger du ett dataelement som ska läsa den cookien och använder det som ett villkor i regeln för att avgöra när åtgärden Läs in [!DNL Target] ska utlösas.

Separat kan du överväga att använda [Adobe-objektet](https://experienceleague.adobe.com/docs/id-service/using/implementation/opt-in-service/optin-overview.html) för att styra taggens aktivering i kombination med din samtyckeshanteringsplattform.

Integreringar med medverkandehanterare (som OneTrust) kan ange och spåra cookies för kunder, som sedan kan användas i regelbyggaren.
