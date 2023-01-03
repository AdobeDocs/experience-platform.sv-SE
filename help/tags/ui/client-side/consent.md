---
title: Distribuera JavaScript-taggar för att hantera kundgodkännande
description: Lär dig hur du hanterar kundernas anmälan och avanmälningssignaler för olika Adobe-lösningar i Adobe Experience Platform.
exl-id: 7762c42f-71c8-4f29-a96b-c6c04b838a91
source-git-commit: 3bb0fc7b2807889d0a759e81c8ff728de3c0cbde
workflow-type: tm+mt
source-wordcount: '637'
ht-degree: 0%

---

# Distribuera JavaScript-taggar för att hantera kundernas samtycke

>[!NOTE]
>
>Adobe Experience Platform Launch har omklassificerats som en serie datainsamlingstekniker i Adobe Experience Platform. Som ett resultat av detta har flera terminologiska förändringar införts i produktdokumentationen. Se följande [dokument](../../term-updates.md) för en konsoliderad hänvisning till terminologiska förändringar.

Lagliga sekretessbestämmelser som den allmänna dataskyddsförordningen (GDPR) kräver att företag kan hantera sitt samtycke för sina användare. Adobe kunder kan kräva att besökarna anmäler sig innan Adobe lösningar kan köras för en viss besökare. Besökarna bör kunna hantera sin status för anmälan och avanmälan.

Adobe Experience Cloud-kunder behöver en mängd olika implementeringar av dessa krav. En del använder sig av samverkansansvariga på företagsnivå och andra bygger sina egna.

Adobe Experience Platform tilläggsutvecklare använder tillägg och regelbyggaren för att definiera lösningar för anmälan och avanmälan.

Det här dokumentet innehåller information om hur du förhindrar att Adobe-taggar avfyras tills du har fått samtycke.

## Advertising Cloud

Adobe Experience Platform utlöses inte [!DNL Advertising Cloud] automatiskt. [!DNL Advertising Cloud] aktiveras bara om du uttryckligen säger det i en regelåtgärd. Använd regelvillkoren för att avgöra när och vad som ska utlösas. Om du till exempel vill använda cookies för att bestämma anmälningsstatus, anger du ett dataelement som ska läsa den cookien och använder den som ett villkor i regeln för att avgöra när spårkonverteringsåtgärden ska utlösas.

Integreringar med medverkandehanterare (som OneTrust) kan ange och spåra cookies för kunder, som sedan kan användas i regelbyggaren.

## Analytics 

I delen Länkspårning i [!DNL Analytics] tilläggets konfigurationsinställningar, kontrollera att följande är *not* markerat:

* Spåra nedladdningslänkar
* Spåra utgående länkar

När de här inställningarna inte har valts utlöses inte plattformen [!DNL Adobe Analytics] automatiskt. [!DNL Analytics] utlöses bara om du uttryckligen säger det i en regelåtgärd. Använd regelvillkoren för att avgöra när och vad som ska utlösas. Om du till exempel vill använda cookies för att bestämma anmälningsstatus anger du ett dataelement som ska läsa den cookien och använder den som ett villkor i regeln för att avgöra när åtgärden Skicka Beacon ska utlösas.

Du kan använda [Anmälningsobjekt för Adobe](https://experienceleague.adobe.com/docs/id-service/using/implementation/opt-in-service/optin-overview.html) för att kontrollera aktiveringen av den här taggen i samråd med er plattform för hantering av samtycke.

Integreringar med medverkandehanterare (som OneTrust) kan ange och spåra cookies för kunder, som sedan kan användas i regelbyggaren.

## Audience Manager

DIL är för närvarande inställt på att avfyras automatiskt om det placeras på en kundsida. Använd [Anmälningsobjekt för Adobe](https://experienceleague.adobe.com/docs/id-service/using/implementation/opt-in-service/optin-overview.html) för att kontrollera aktiveringen av den här taggen i samråd med er plattform för hantering av samtycke.

[!DNL Adobe] rekommenderar att du använder vidarebefordran på serversidan i [!DNL Analytics].

## Experience Cloud ID

[!DNL Experience Cloud ID] aktiveras automatiskt om det placeras på en kundsida.

Använd [Anmälningsobjekt för Adobe](https://experienceleague.adobe.com/docs/id-service/using/implementation/opt-in-service/optin-overview.html) för att kontrollera aktiveringen av den här taggen i samråd med er plattform för hantering av samtycke.

## Målgrupp

Adobe Experience Platform utlöses inte [!DNL Target] automatiskt. [!DNL Target] utlöses bara om du uttryckligen säger det i en regelåtgärd. Använd regelvillkoren för att avgöra när och vad som ska utlösas. Om du till exempel vill använda cookies för att bestämma anmälningsstatus anger du ett dataelement som ska läsa den cookien och använder den som ett villkor i regeln för att avgöra när inläsningen ska starta [!DNL Target] åtgärd.

Du kan använda [Anmälningsobjekt för Adobe](https://experienceleague.adobe.com/docs/id-service/using/implementation/opt-in-service/optin-overview.html) för att kontrollera aktiveringen av den här taggen i samråd med er plattform för hantering av samtycke.

Integreringar med medverkandehanterare (som OneTrust) kan ange och spåra cookies för kunder, som sedan kan användas i regelbyggaren.
